# sqlpractice

# 1. How many users are there?

`select Count(users.id) from users;`

Result: 50

# 2. What are the 5 most expensive items

`select items.title, items.price from items order by price desc limit 5`

Result:

"Small Cotton Gloves"	"9984"
"Small Wooden Computer"	"9859"
"Awesome Granite Pants"	"9790"
"Sleek Wooden Hat"	"9390"
"Ergonomic Steel Car"	"9341"

# 3. What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

`select items.title, items.price from items where items.category = "%Books%" order by price asc limit 1`

Result: 

"Ergonomic Granite Chair"	"1496"

# 4a. Who lives at "6439 Zetta Hills, Willmouth, WY"?

`select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state, addresses.zip from users inner join addresses on users.id = addresses.user_id
where addresses.street = "6439 Zetta Hills" `

Result: Corrine Little

# 4b. Do they have another address?

`select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state, addresses.zip 
from addresses inner join users on addresses.user_id = users.id
where users.first_name = "Corrine"`

Result:

"Corrine"	"Little"	"6439 Zetta Hills"	"Willmouth"	"WY"	"15029"
"Corrine"	"Little"	"54369 Wolff Forges"	"Lake Bryon"	"CA"	"31587"

# Also did a single left join

`select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state, addresses.zip, users.id from users left join addresses on users.id = addresses.user_id
where users.id = 40;`

# 5. Correct Virginie Mitchell's address to "New York, NY, 10108".

`update addresses set city = "New York"where id = 42;
update addresses set state = "NY" where id = 42;
update addresses set zip = "10108" where id = 42;`

Question: Is there a way to combine these update statements into one?

# 6. How much would it cost to buy one of each tool?

I assummed that tools exist across categories that include the word "tools."

`select SUM(items.price) from items where items.category like "%tools%" order by price`

Result: 46477

# 7. How many total items did we sell?

`select Sum(orders.quantity) from orders`

Result: 2125

# 8. How much was spent on books?

`Select SUM(items.price) from orders inner join items on orders.item_id = items.id
 where  items.category like "%books%";`
 
 Result: 180356
 
 # 9. Simulate buying an item by inserting a User for yourself and an Order for that User.
 
 `insert into users (id, first_name, last_name, email) values(51, "Danielle", "Williams", "danielle@boomtownroi.com");`
 `insert into orders (id, user_id, item_id, quantity, created_at) values(378, 51, 100, 2, current_timestamp)`
 




