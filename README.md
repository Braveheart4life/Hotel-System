# Hotel-System
A hotel business gave the analytics team their database to provide business insights, and to give recommendations about the technicalities of running the database.
Five tables were provided: bookings, requests, food_orders, menu and rooms (CSV files).
The first priority was to establish an Entity Relationship Diagram (ERD). This was done on Power Bi under the Model view.
After creating the ERD, I imported the tables into SQL server to make more meaning of the tables by joining them were necessary.
The CSV files became more readable after importing into SQL server and were properly arranged into rowsand columns.
Then i wrote the following queries to join different tables and have two final tables:

I created two main tables to be analysed. The first table is a combination of the "Food_ Orders" and the "Menu"
The second table is the combination of the "Requests", "rooms" and "bookings" tables.
This way, i could export both tables to Power BI and create explanatory dashboards based on revenue generated from 
food and boarding in the Hotel.
*/

--STEPS:
/* 1:
    This query joins the "food_orders" and the "menu" tables together to form the "Food_Menu_Tables":

        SELECT fo.dest_room, fo.bill_room, fo.date, fo.time, fo.orders,
               m.name, m.price, m.category
            FROM food_orders fo 
            JOIN menu m 
        ON fo.menu_id = m.id
*/

/* 2:
    Then i created a second table to join the "bookings", "requests" and "rooms" tables. To make that work, 
    I joined the "requests" and "bookings" tables first and called it "Temporary_Table" as shown below:

        SELECT rq.client_name, rq.room_type, rq.start_date, rq.end_date, rq.adults, rq.children,
               b.room, b.start_date, b.end_date
            FROM requests rq 
            JOIN bookings b 
        ON rq.request_id = b.request_id
This was named "Temporary_Table" created in "Views"
    Then i joined the "Temporary Table" to "rooms" table to create the "Request_Booking_Rooms_Table" as seen below:

    THIS QUERY JOINS THE TEMPORARY TABLE (CONTAINING "REQUESTS" AND "BOOKINGS") to the "rooms" table because 
    This was the only way i could join them both:

        SELECT t.client_name, t.room_type, t.start_date, t.end_date, t.adults, t.children, t.room, t.Booking_end_date, t.booking_start_date,
               r.price_day, r.capacity, r.prefix
            FROM Temporary_Table t
            JOIN rooms r 
        ON t.room_type = r.[type]
*/


<img width="704" alt="table 2" src="https://user-images.githubusercontent.com/107772115/190056254-de4ec57e-5f23-4b3c-a902-d006b7f3dd97.png">
<img width="705" alt="table 1" src="https://user-images.githubusercontent.com/107772115/190056264-97f2b377-11df-443f-b654-bc39527cc6a8.png">

Then I gave some recommendations such as implementing Data Validation in excel during data entry process, to minimize chances of typo errors like I found in the bookings table.

I also used DAX in power Bi to create new columns to create insightful tables and performed some data cleaning during the transformation process in Power Bi
