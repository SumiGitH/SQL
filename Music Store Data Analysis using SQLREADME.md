Music Store Data Analysis Project using SQL

The main objective of this data is to understand the business growth by answering some basic and simple questions.

DATABASE & TOOLS: SQL



SCHEMA

<img width="710" height="574" alt="SCHEMA" src="https://github.com/user-attachments/assets/f1d19dcd-d564-4d28-b246-b14ee76a67a6" />  

Questions & Answers
SET 1
1. Who's the senior most employee based on job title
<img width="743" height="333" alt="image" src="https://github.com/user-attachments/assets/e590ea43-21aa-4066-a51f-0345ffd6513a" />   

   
2. Which countries have the most Invoices?
<img width="426" height="391" alt="image" src="https://github.com/user-attachments/assets/3019ca4c-187d-410c-b543-152de2d4506c" />

   
3. What are the top 3 values of total invoice?
<img width="744" height="391" alt="image" src="https://github.com/user-attachments/assets/7da9e03f-5b6f-49cf-8fe0-8fd9050d2858" />

   
4. Which city has the best customers? We would like to throw a promotional Music Festival in the city we made the most money. Write a query that returns one city that has the highest sum of invoice totals. Return both the city name & sum of all invoice total
<img width="746" height="403" alt="image" src="https://github.com/user-attachments/assets/e8cbfb75-ca88-45e5-9e7d-68acc694efa0" />



5. Who is the best customer? The customer who has spent the most money will be declared the best customer. Write a query that returns the person who has spent the most money.
<img width="743" height="389" alt="image" src="https://github.com/user-attachments/assets/ac2fc2a9-d0da-49cc-b076-1ef33997e8f5" />



   
SET 2
1. Write query to return the email, first name, last name, & Genre of all Rock Music Listeners. Return your list ordered alphabetically by email starting with A
<img width="742" height="394" alt="image" src="https://github.com/user-attachments/assets/d1ff1ee4-37d0-4a5c-a661-3d631b0534b0" />



   
2. Let's invite the artists who have written the most rock music in our dataset. Write a query that returns the Artist name & total track count of the top 10 rock bands
<img width="745" height="394" alt="image" src="https://github.com/user-attachments/assets/562d2884-b5da-4afb-b3c1-69dbfa83822b" />


   
3. Return all the track names that have a song length longer than the average song length. Return the Name and Milliseconds for each track. Order by the song length with the longest songs listed first.
<img width="744" height="394" alt="image" src="https://github.com/user-attachments/assets/ba06e67b-7ba2-418c-9199-e8d7eb377a4a" />








SET 3
1. Find how much amount spent by each customer on artists? Write a query to return customer name, artist name and total spent
   
WITH best_selling_artist AS (
	SELECT artist.artist_id AS artist_id, artist.name AS artist_name, SUM(invoice_line.unit_price*invoice_line.quantity) AS total_sales
	FROM invoice_line
	JOIN track ON track.track_id = invoice_line.track_id
	JOIN album ON album.album_id = track.album_id
	JOIN artist ON artist.artist_id = album.artist_id
	GROUP BY 1
	ORDER BY 3 DESC
	LIMIT 1
)
SELECT c.customer_id, c.first_name, c.last_name, bsa.artist_name, SUM(il.unit_price*il.quantity) AS amount_spent
FROM invoice i
JOIN customer c ON c.customer_id = i.customer_id
JOIN invoice_line il ON il.invoice_id = i.invoice_id
JOIN track t ON t.track_id = il.track_id
JOIN album alb ON alb.album_id = t.album_id
JOIN best_selling_artist bsa ON bsa.artist_id = alb.artist_id
GROUP BY 1,2,3,4
ORDER BY 5 DESC;
<img width="744" height="384" alt="image" src="https://github.com/user-attachments/assets/34a805b6-a23f-4bdb-bc20-95f5cac92d03" />




 

2. We want to find out the most popular music genre for each country. We determine the most popular genre as the genre with the highest amount of purchases. Write a query that returns each country along with the top genre. For countries where the maximum number of purchases is shared return all genres.
/* Steps to Solve:  There are two parts in question- first most popular music genre and second need data at country level. */

/* Method 1: Using CTE */

WITH popular_genre AS 
(
    SELECT COUNT(invoice_line.quantity) AS purchases, customer.country, genre.name, genre.genre_id, 
	ROW_NUMBER() OVER(PARTITION BY customer.country ORDER BY COUNT(invoice_line.quantity) DESC) AS RowNo 
    FROM invoice_line 
	JOIN invoice ON invoice.invoice_id = invoice_line.invoice_id
	JOIN customer ON customer.customer_id = invoice.customer_id
	JOIN track ON track.track_id = invoice_line.track_id
	JOIN genre ON genre.genre_id = track.genre_id
	GROUP BY 2,3,4
	ORDER BY 2 ASC, 1 DESC
) 
SELECT * FROM popular_genre WHERE RowNo <= 1


/* Method 2: : Using Recursive */

WITH RECURSIVE
	sales_per_country AS(
		SELECT COUNT(*) AS purchases_per_genre, customer.country, genre.name, genre.genre_id
		FROM invoice_line
		JOIN invoice ON invoice.invoice_id = invoice_line.invoice_id
		JOIN customer ON customer.customer_id = invoice.customer_id
		JOIN track ON track.track_id = invoice_line.track_id
		JOIN genre ON genre.genre_id = track.genre_id
		GROUP BY 2,3,4
		ORDER BY 2
	), 
   max_genre_per_country AS (SELECT MAX(purchases_per_genre) AS max_genre_number, country
		FROM sales_per_country
		GROUP BY 2
		ORDER BY 2)

SELECT sales_per_country.* 
FROM sales_per_country
JOIN max_genre_per_country ON sales_per_country.country = max_genre_per_country.country
WHERE sales_per_country.purchases_per_genre = max_genre_per_country.max_genre_number;













3. Write a query that determines the customer that has spent the most on music for each country. Write a query that returns the country along with the top customer and how much they spent. For countries where the top amount spent is shared, provide all customers who spent this amount

/* Method 1: using CTE */

WITH Customter_with_country AS (
		SELECT customer.customer_id,first_name,last_name,billing_country,SUM(total) AS total_spending,
	    ROW_NUMBER() OVER(PARTITION BY billing_country ORDER BY SUM(total) DESC) AS RowNo 
		FROM invoice
		JOIN customer ON customer.customer_id = invoice.customer_id
		GROUP BY 1,2,3,4
		ORDER BY 4 ASC,5 DESC)
SELECT * FROM Customter_with_country WHERE RowNo <= 1


/* Method 2: Using Recursive */

WITH RECURSIVE 
	customter_with_country AS (
		SELECT customer.customer_id,first_name,last_name,billing_country,SUM(total) AS total_spending
		FROM invoice
		JOIN customer ON customer.customer_id = invoice.customer_id
		GROUP BY 1,2,3,4
		ORDER BY 2,3 DESC),

	country_max_spending AS(
		SELECT billing_country,MAX(total_spending) AS max_spending
		FROM customter_with_country
		GROUP BY billing_country)

SELECT cc.billing_country, cc.total_spending, cc.first_name, cc.last_name, cc.customer_id
FROM customter_with_country cc
JOIN country_max_spending ms
ON cc.billing_country = ms.billing_country
WHERE cc.total_spending = ms.max_spending
ORDER BY 1;
