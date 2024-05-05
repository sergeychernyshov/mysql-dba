insert into actor_2(actor_id,first_name,last_name)
values(1,'Pen','Gu')
on Duplicate key update first_name = 'Pen', last_name = 'Gu'


insert into actor_2(actor_id,first_name,last_name)
values(1,'Pen2','Gu2')
on Duplicate key update first_name = values(first_name), last_name = values(last_name)
