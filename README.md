# Duplicate Email
Tekrar eden email adresten sadece bir adet dönülmesi istenmektedir. Null veri olabilir null olmama garantisi yoktur. Veri yoksa dönmemelidir.
```sql
select email as 'Email' from Person p where p.email is not null group by p.email having count(*)>1;
```
# Combine Tables (Join'ler)
İki tablonun belirli alanların olduğu sonuç istenmektedir. İlişkili tablo sonucu dönülecektir.
```sql
Select person.firstName, person.lastName, adres.city, adres.state from Person person 
left join Address adres on person.personId = adres.personId;```
