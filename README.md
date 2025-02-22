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

# Customers Who Never Order
Sipariş etmemiş kullanıcıların getirilmesi istenmektedir.
```sql
Select c.name AS 'Customers' from Customers c LEFT JOIN Orders o ON o.customerId = c.id where o.customerId is null;
```

# Delete Duplicate Record
Bu SQL sorgusu, Person tablosundaki her bir e-posta adresi için yalnızca birinci kaydı (min id) tutarak, e-posta adresi tekrar eden kişileri silmeyi amaçlar. Yani, her e-posta için sadece en düşük id'ye sahip olan kişi kalacak şekilde, diğer tüm kayıtlar silinir. Bu işlem, birleştirme (join) mantığıyla, aynı e-posta adresine sahip tüm kişilerden yalnızca bir tanesini seçip geri kalanlarını silmeye benzer.
```sql
DELETE
FROM Person  where Id not in 
(Select others_id from (Select min(id) as others_id from Person group by email) as tmp)
```
