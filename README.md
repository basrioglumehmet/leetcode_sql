# Duplicate Email
Tekrar eden email adresten sadece bir adet dönülmesi istenmektedir.
```sql
select email as 'Email' from Person group by email limit 1;
```
