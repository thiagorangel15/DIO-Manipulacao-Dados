# Processando e Transformando Dados com Power BI

Projeto feito seguindo o Bootcamp da DIO de Python Data Analytics onde precisei efetuar certas transformações nos dados com o PowerBI.

Durante este processo precisei efetuar o seguinte passo a passo e encontrei alguns problemas ao longo do caminho:

* Ao analisar Employee temos apenas um registro com o Super_ssn null, percebi que ele possui o Dno de valor 1 que possui o nome de HeadQuarters. Ou seja, provavelmente ele é o dono da companhia e não possui nenhum superior a ele.

* Não há departamentos sem gerentes 

* Diferentes funcionários de departamentos gastam horas diferentes para o mesmo projeto.

* Ao separar a coluna Address de Employee vi que um registro possui um nome composto chamado Fire-Oak, isso estava dando problema na hora de separar pelo limitador -, tratei o dado transformando Fire-Oak em FireOak e depois separando os dados de endereço.

* Consulta SQL que utilizei para juntar colaboradores com seus respectivos gerentes: 

``` sql
WITH manager AS(
	SELECT e.Fname,e.Lname, e.Ssn FROM employee e
    JOIN departament d ON e.Dno = d.Dnumber
    WHERE e.Ssn = d.Mgr_ssn
) 
SELECT CONCAT(m.Fname," ",m.Lname) AS manager_name, e.* FROM employee e
LEFT JOIN manager m ON e.Super_ssn = m.Ssn OR e.Super_ssn IS NULL
WHERE e.Super_ssn IS NOT NULL OR m.Fname = "James";
```


* Ao mesclar departamento com localização temos o departamento Research em 3 locais diferentes porém com o mesmo ID oque causou duplicatas nos dados, portanto preferi nesse momento não efetuar a mescla com localização e apenas deixar o departamento por funcionario. 
