# Duplicate Email
Tekrar eden email adresten sadece bir adet dönülmesi istenmektedir. Null veri olabilir null olmama garantisi yoktur. Veri yoksa dönmemelidir.
```sql
select email as 'Email' from Person p where p.email is not null group by p.email having count(*)>1;
```

# Combine Tables (Join'ler)
İki tablonun belirli alanların olduğu sonuç istenmektedir. İlişkili tablo sonucu dönülecektir.

```sql
Select person.firstName, person.lastName, adres.city, adres.state from Person person 
left join Address adres on person.personId = adres.personId;
```
# Employees Earning More Than Their Managers
```sql
/*
Sub Query: Alt sorgular aracılığı ile manager'dan yüksek maaş alanı getireceğiz.
SELECT emp.name AS Employee 
FROM Employee emp 
WHERE emp.salary > (
    SELECT MAX(emp2.salary) 
    FROM Employee emp2 
    WHERE emp2.id = emp.managerId
)
AND emp.managerId IS NOT NULl;

fakat daha hızlı yolu var: JOIN
*/

SELECT emp.name AS Employee 
FROM Employee emp
LEFT JOIN Employee emp2 ON emp.managerId = emp2.id
WHERE emp.salary > emp2.salary
AND emp.managerId IS NOT NULL;

```
