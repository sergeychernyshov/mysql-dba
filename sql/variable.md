#Переменные в MySQL

select @n:=title from film f where f.film_id  = 1

select @n

select @n:=(select title from film f where f.film_id  = 10 )

select @n

select title into @n from film f where f.film_id  = 100 
		
select @n

set @counter:=0, @total:=15

select @counter, @total

select 1, 3 into @counter, @total 

select @counter, @total

select 11 into @fid

select * from film f where f.film_id = @fid

select * from film f where f.film_id = @FID