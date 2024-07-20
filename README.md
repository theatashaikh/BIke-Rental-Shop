# Bike Rental Shop

This project implements a simple command-line bike rental shop application using BASH scripting and interacts with a PostgreSQL database.

## Project Overview

### Functionality

The script provides three main functionalities:

- **Rent a Bike:**
  Users can browse available bikes, choose one to rent, and provide their phone number. If a customer is new, their information will be stored. The bike's availability will be updated to reflect being rented.
- **Return a Bike:**
  Users can enter their phone number to view their current rentals and choose a bike to return. The script updates the rental record and sets the bike's availability back to true.
- **Exit:**
  Users can exit the program.

The Bike Rental Shop allows customers to rent and return bikes. The project consists of a PostgreSQL database with three tables: `bikes`, `customers`, and `rentals`, and a Bash script (`bike-shop.sh`) to manage the rental process.

## Database Schema

### `bikes` Table

- `bike_id SERIAL PRIMARY KEY`
- `type VARCHAR(50) NOT NULL`
- `size INT NOT NULL`
- `available BOOLEAN NOT NULL`

### `customers` Table

- `customer_id SERIAL PRIMARY KEY`
- `name VARCHAR(40) NOT NULL`
- `phone VARCHAR(15) NOT NULL UNIQUE`

### `rentals` Table

- `rental_id SERIAL PRIMARY KEY`
- `customer_id INT REFERENCES customers(customer_id) NOT NULL`
- `bike_id INT REFERENCES bikes(bike_id) NOT NULL`
- `date_rented DATE DEFAULT NOW() NOT NULL`
- `date_returned DATE`

## How to Use

### Prerequisites

- PostgreSQL installed and running
- A bash terminal

### Setup

1. **Create the database tables**:

   ```sql
   CREATE TABLE bikes (
     bike_id SERIAL PRIMARY KEY,
     type VARCHAR(50) NOT NULL,
     size INT NOT NULL,
     available BOOLEAN NOT NULL
   );

   CREATE TABLE customers (
     customer_id SERIAL PRIMARY KEY,
     name VARCHAR(40) NOT NULL,
     phone VARCHAR(15) NOT NULL UNIQUE
   );

   CREATE TABLE rentals (
     rental_id SERIAL PRIMARY KEY,
     customer_id INT REFERENCES customers(customer_id) NOT NULL,
     bike_id INT REFERENCES bikes(bike_id) NOT NULL,
     date_rented DATE DEFAULT NOW() NOT NULL,
     date_returned DATE
   );
   ```

2. **Populate the bikes table with sample data:**

   ```sql
   INSERT INTO bikes (type, size, available) VALUES
   ('Mountain', 26, TRUE),
   ('Road', 28, TRUE),
   ('Hybrid', 24, TRUE),
   ('Electric', 20, TRUE),
   ('Mountain', 24, TRUE),
   ('Road', 26, TRUE),
   ('Hybrid', 28, TRUE),
   ('Electric', 24, TRUE),
   ('Mountain', 28, TRUE),
   ('Road', 24, TRUE),
   ('Hybrid', 26, TRUE),
   ('Electric', 28, TRUE),
   ('Mountain', 22, TRUE),
   ('Road', 22, TRUE),
   ('Hybrid', 22, TRUE),
   ('Electric', 26, TRUE),
   ('Mountain', 20, TRUE),
   ('Road', 20, TRUE),
   ('Hybrid', 20, TRUE),
   ('Electric', 22, TRUE);

   ```

3. **Run the script:**

```bash
./bike-shop.sh
```

### Script Functionality

- **Main Menu:** Provides options to rent a bike, return a bike, or exit.
- **Rent a Bike:**
  - Displays available bikes.
  - Prompts the user for bike selection and customer information.
  - Records the rental and updates bike availability.
- **Return a Bike:**
  - Prompts the user for their phone number.
  - Displays the bikes currently rented by the customer.
  - Updates the rental record and bike availability.

### Sample Interactions

#### Renting a bike

```bash
## ~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit

1

Here are the bikes we have available:
1) 26" Mountain Bike
2) 28" Road Bike
3) 24" Hybrid Bike
4) 20" Electric Bike
5) 24" Mountain Bike
6) 26" Road Bike
7) 28" Hybrid Bike
8) 24" Electric Bike
9) 28" Mountain Bike
10) 24" Road Bike
11) 26" Hybrid Bike
12) 28" Electric Bike
13) 22" Mountain Bike
14) 22" Road Bike
15) 22" Hybrid Bike
16) 26" Electric Bike
17) 20" Mountain Bike
18) 20" Road Bike
19) 20" Hybrid Bike
20) 22" Electric Bike

Which one would you like to rent?
1

What's your phone number?
123-456-7890

What's your name?
John Doe

I have put you down for the 26" Mountain Bike, John Doe.
```

#### Returning a bike

```bash
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit

2

What's your phone number?
123-456-7890

Here are your rentals:
1) 26" Mountain Bike

Which one would you like to return?
1

Thank you for returning your bike.

```

### Contributing

This is a basic educational script. Feel free to fork the repository and modify it to add features or improve functionality!

This script is for educational purposes and lacks features like user authentication and error handling for a production environment.

## License

This project is licensed under the MIT License.
