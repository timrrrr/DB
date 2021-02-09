SELECT * from country
ORDER by country_id
OFFSET 11 limit 6;
SELECT address, city
FROM address inner JOIN city on address.city_id = city.city_id
WHERE city like 'A%';

SELECT first_name, last_name, city
FROM customer inner join address
ON customer.address_id = address.address_id
inner join city
ON address.city_id = city.city_id;

SELECT first_name, last_name, amount
FROM payment inner join customer on payment.customer_id = customer.customer_id
WHERE amount > 11;

SELECT first_name from customer out
WHERE (select count(*) from customer inr
WHERE inr.first_name = out.first_name) > 1;





DROP view if exists v1;
CREATE view v1 as
SELECT f.title, c.name
FROM film f
INNER join film_category fc on f.film_id = fc.film_id
INNER join category c on c.category_id = fc.category_id and c.name='Horror';

SELECT * from v1;

DROP function if exists func() cascade;
CREATE FUNCTION func()
RETURNS TRIGGER
LANGUAGE PLPGSQL
AS
$$
BEGIN
-- trigger logic
perform version();
return null;
END

$$;




DROP trigger if exists t1 on payment;

CREATE TRIGGER t1
   AFTER INSERT
   ON payment
   FOR EACH STATEMENT
       EXECUTE PROCEDURE func();



INSERT into payment(payment_id, customer_id, staff_id, rental_id, amount, payment_date) values
(182323, 1, 1, 1, 500, '1996-12-02');



