--  Car_Rental_Management_System_SQL_project

-- The scope of this project is to design a Car Rental Management System. 
-- Problem statement/ idea x
-- 1. Think how we're going to create lots of object first, before adding more attributes. 
-- 2. Think and create about entities or attributes inside lots of objects. 
-- 3. Design and create ER diagram. 
-- 4. Finally, run each table to make sure that ER diagram are in one place. 

-- Below are the processes and questions that I'm going to create step by step based on this project here. 

-- Step 1: I'm going to create 10 objects for a Car Rental Management System. 
-- These are all our objects. 
-- 1. Vehicle 
-- 2. Customer 
-- 3. Employee 
-- 4. Transaction 
-- 5. Appointments 
-- 6. Payment 
-- 7. Maintenance_records 
-- 8. License_record 
-- 9. Feedback_and_review


-- Step 2: Let's create our table. 
-- Let's create our own entities of Vehicle table.
CREATE TABLE Vehicles (
    Veh_id INT PRIMARY KEY, 
    Veh_brand VARCHAR(100),
    Veh_model VARCHAR(100), 
    Veh_color VARCHAR(100), 
    Veh_manufactured_year INT,
    Veh_manufactured_date DATE,
    Veh_wheels INT, 
    Veh_seats INT, 
    Veh_engine_power INT
);


-- Let's create our own entities of Customer table.
CREATE TABLE Customer (
    Cus_id INT PRIMARY KEY, 
    Cus_firstname VARCHAR(100), 
    Cus_lastname VARCHAR(100), 
    Cus_age INT, 
    Cus_gender VARCHAR(100), 
    Cus_nationality VARCHAR(100), 
    Cus_ph_number VARCHAR(100), 
    Cus_email VARCHAR(100), 
    Cus_address VARCHAR(100)
);

-- Let's create our own entities of Employee table.
CREATE TABLE Employee_table (
    Emp_id INT PRIMARY KEY, 
    Emp_firstname VARCHAR(100), 
    Emp_lastname VARCHAR(100), 
    Emp_age INT, 
    Emp_gender VARCHAR(100), 
    Emp_jobs_roles VARCHAR(100), 
    Emp_contact_num VARCHAR(100)
);

-- Let's create our own entities of Transaction table.
CREATE TABLE Transaction_table (
    Tran_id INT PRIMARY KEY, 
    Tran_name VARCHAR(100), 
    Tran_type VARCHAR(100), 
    Tran_date DATE, 
    Tran_amount DECIMAL(10,2), 
    Veh_id INT, 
    Cus_id INT, 
    Emp_id INT, 
    FOREIGN KEY (Veh_id) REFERENCES Vehicles(Veh_id), 
    FOREIGN KEY (Cus_id) REFERENCES Customer(Cus_id), 
    FOREIGN KEY (Emp_id) REFERENCES Employee_table(Emp_id)
);

-- Let's create our own entities of Appointments table.
CREATE TABLE Appointment (
    Appt_id INT PRIMARY KEY, 
    Appt_date DATE, 
    Appt_time DATETIME,  -- Change to DATETIME
    Veh_id INT, 
    Cus_id INT, 
    Emp_id INT, 
    FOREIGN KEY (Veh_id) REFERENCES Vehicles(Veh_id),  
    FOREIGN KEY (Emp_id) REFERENCES Employee_table(Emp_id),
    FOREIGN KEY (Cus_id) REFERENCES Customer(Cus_id)
);

-- Let's create our own entities of Payment table.
CREATE TABLE Payment (
    Payment_id INT PRIMARY KEY, 
    Payment_name VARCHAR(100), 
    Payment_method VARCHAR(100), 
    Payment_amount DECIMAL(10,2), 
    Payment_date DATE,
    Payment_status VARCHAR(100), 
    Tran_id INT, 
    FOREIGN KEY (Tran_id) REFERENCES Transaction_table(Tran_id)
);

-- Let's create our own entities of Maintenance records table.
CREATE TABLE Maintenance_records (
    Main_record_id INT PRIMARY KEY, 
    Main_record_date DATE, 
    Main_record_type VARCHAR(100), 
    Main_record_description VARCHAR(100), 
    Main_record_cost DECIMAL(10,2), 
    Main_record_status VARCHAR(100), 
    Veh_id INT, 
    FOREIGN KEY (Veh_id) REFERENCES Vehicles(Veh_id)
);

-- Let's create our own entities of License Record table here.
CREATE TABLE License_record (
    License_id INT PRIMARY KEY, 
    License_number VARCHAR(100), 
    License_holder_name VARCHAR(100), 
    License_issue_date DATE, 
    License_expiry_date DATE, 
    License_type VARCHAR(100), 
    License_holder_contact_num VARCHAR(100), 
    Veh_id INT, 
    FOREIGN KEY (Veh_id) REFERENCES Vehicles(Veh_id)
);

-- Let's create our own entities of Feedback and review table here.
CREATE TABLE feedback_review(
    Feed_review_id INT PRIMARY KEY, 
    Feed_review_rate INT, 
    Feed_review_comments VARCHAR(100), 
    Feed_review_submission_date DATE, 
    Emp_id INT, 
    Tran_id INT,  
    Cus_id INT,
    FOREIGN KEY (Emp_id) REFERENCES Employee_table(Emp_id), 
    FOREIGN KEY (Tran_id) REFERENCES Transaction_table(Tran_id),
    FOREIGN KEY (Cus_id) REFERENCES Customer(Cus_id)
);

-- Step 3: We're going to insert some data using INSERT fuction. 
-- Inserting data into Vehicles table.
INSERT INTO Vehicles(Veh_id, Veh_brand, Veh_model, Veh_color, Veh_manufactured_year, Veh_manufactured_date, Veh_wheels, Veh_seats, Veh_engine_power) 
VALUES 
(1, 'Toyota', 'Camry', 'Blue', 2023, '2023-01-15', 4, 5, 200),
(2, 'Honda', 'Civic', 'Red', 2022, '2022-05-20', 4, 5, 180),
(3, 'Ford ', 'Escape', 'Green', 2021, '2021-11-10', 4, 5, 220),
(4, 'Chevrolet', 'Malibu', 'Silver', 2023, '2023-03-25', 4, 5, 190),
(5, 'Nissan', 'Altima', 'Black', 2022, '2022-09-08', 4, 5, 210),
(6, 'Hyundai', 'Elantra', 'White', 2021, '2021-07-12', 4, 5, 170),
(7, 'Volkswagen', 'Jetta', 'Gray', 2023, '2023-02-28', 4, 5, 200),
(8, 'Subaru', 'Outback', 'Brown', 2022, '2022-04-05', 4, 5, 230),
(9, 'Mazda ', 'CX-3', 'Yellow', 2021, '2021-10-15', 4, 5, 180),
(10, 'Kia ', 'Optima', 'Purple', 2023, '2023-06-30', 4, 5, 200);

-- Newid function used to generate any random information. 
SELECT * FROM Vehicles ORDER BY NEWID();
-- Inserting data into Customer table.
INSERT INTO Customer(Cus_id, Cus_firstname, Cus_lastname, Cus_age, Cus_gender, Cus_nationality, Cus_ph_number, Cus_email, Cus_address) 
VALUES 
(1, 'Somchai', 'Pannich', 28, 'Male', 'Thailand', '088-985-4423', 'somchai.p@email.com', '123 Purple Road'),
(2, 'Natcha', 'Charoensuk', 25, 'Female', 'Thailand', '084-335-0016', 'natcha.c@email.com', '456 Green Road'),
(3, 'Kritsana', 'Suksomboon', 32, 'Male', 'Thailand', '082-119-0564', 'kritsana.s@email.com', '789 Blue Road'),
(4, 'Ariya', 'Wongsuwon', 27, 'Female', 'Thailand', '085-534-1167', 'ariya.w@email.com', '101 Yellow Road'),
(5, 'Cholathit', 'Taptimthong', 30, 'Male', 'Thailand', '080994-0047', 'cholathit.t@email.com', '202 Cornflower Road'),
(6, 'Wipha', 'Ratnaruang', 29, 'Female', 'Thailand', '093-147-2513', 'wipha.r@email.com', '303 Red Road'),
(7, 'Prapaporn', 'Jantanasathu', 26, 'Male', 'Thailand', '090-743-2235', 'prapaporn.j@email.com', '404 Orange Road'),
(8, 'Naree', 'Wongwiwat', 31, 'Female', 'Thailand', '094-335-1127', 'naree.w@email.com', '505 Lavender Road'),
(9, 'Nattapon', 'Wongwiwat', 33, 'Male', 'Thailand', '096-664-7782', 'nattapon.w@email.com', '606 Pink Road'),
(10, 'Pawina', 'Chuthong', 28, 'Female', 'Thailand', '091-741-2814', 'pawina.c@email.com', '707 Turquoise Road');

-- Newid () function used to generate any random information. 
SELECT * FROM Customer 
ORDER  BY NEWID();


-- Inserting data into Employee table.
INSERT INTO Employee_table(Emp_id, Emp_firstname, Emp_lastname, Emp_age, Emp_gender, Emp_jobs_roles, Emp_contact_num) VALUES 
(2, 'Eva', 'Brown', 27, 'Female', 'Customer Service Representative', '076-234-5678'), 
(3, 'Daniel', 'Smith', 32, 'Male', 'Mechanic', '089-876-5432'),
(4, 'Sophia', 'Williams', 28, 'Female', 'Sales Agent', '065-432-1098'),
(5, 'Christopher', 'Johnson', 35, 'Male', 'Finance Manager', '054-321-0987'),
(6, 'Ava', 'Davis', 30, 'Female', 'IT Specialist', '043-210-9876'),
(7, 'James', 'Miller', 38, 'Male', 'Marketing Coordinator', '032-109-8765'),
(8, 'Emma', 'Wilson', 29, 'Female', 'HR Manager', '021-098-7654'),
(9, 'Ryan', 'Thompson', 33, 'Male', 'Logistics Coordinator', '010-987-6543'),
(10, 'Olivia', 'Moore', 31, 'Female', 'Operations Supervisor', '099-876-5432'),
(11, 'Samuel', 'Jackson', 36, 'Male', 'Rental Agent', '088-765-4321');
-- Newid function used to generate any random information.
SELECT * FROM Employee_table 
ORDER BY NEWID();

-- Inserting data into Transaction table.
INSERT INTO Transaction_table(Tran_id, Tran_name, Tran_type, Tran_date, Tran_amount, Veh_id, Cus_id, Emp_id) VALUES 
(24, 'Rental-008', 'Rent', '2023-08-10', 180.00, 5, 7, 2),
(25, 'Service-005', 'Service', '2023-05-25', 120.00, 4, 6, 11),
(26, 'Rental-009', 'Rent', '2023-09-15', 250.00, 3, 5, 3),
(27, 'Service-006', 'Service', '2023-06-05', 100.00, 2, 4, 5),
(28, 'Rental-010', 'Rent', '2023-10-20', 220.00, 1, 3, 6),
(29, 'Rental-011', 'Rent', '2023-11-25', 270.00, 6, 2, 7),
(30, 'Service-007', 'Service', '2023-07-10', 150.00, 9, 1, 8),
(31, 'Rental-012', 'Rent', '2023-12-15', 200.00, 8, 8, 9),
(32, 'Service-008', 'Service', '2023-08-20', 80.00, 10, 9, 10),
(33, 'Rental-013', 'Rent', '2024-01-25', 300.00, 7, 10, 4);
-- Newid () function used to generate any random information. 
SELECT * FROM Transaction_table
ORDER BY NEWID();

-- Inserting data into Appointment table.
INSERT INTO Appointment(Appt_id, Appt_date, Appt_time, Veh_id, Emp_id, Cus_id) VALUES 
(51, '2023-09-05', '08:30:00', 2, 2, 3),
(52, '2023-10-15', '13:15:00', 5, 3, 9),
(53, '2023-07-25', '10:00:00', 9, 4, 1),
(54, '2023-11-10', '16:45:00', 4, 5, 8),
(55, '2023-12-30', '11:30:00', 7, 6, 5),
(56, '2023-08-12', '14:20:00', 3, 7, 7),
(57, '2024-01-20', '09:00:00', 10, 8, 4),
(58, '2023-09-28', '12:40:00', 6, 9, 2),
(59, '2024-02-15', '15:30:00', 1, 11, 10),
(60, '2024-03-05', '10:00:00', 8, 10, 6);
-- Newid function () used to generate any random information. 
SELECT * FROM Appointment 
ORDER BY NEWID();

-- Inserting data into Payment table.
INSERT INTO Payment(Payment_id, Payment_name, Payment_method, Payment_amount, Payment_date, Payment_status, Tran_id) VALUES 
(61, 'Krung Thai Bank', 'Credit Card', 150.00, '2023-09-05', 'Success', 33),
(62, 'Cash Payment', 'Cash', 120.50, '2023-10-15', 'Success', 24),
(63, 'Maestro', 'Debit Card', 180.75, '2023-07-25', 'Pending', 25),
(64, 'E Wallet', 'Online', 200.00, '2023-11-10', 'Success', 26),
(65, 'Cash Payment', 'Cash', 160.25, '2023-12-30', 'Success', 27),
(66, 'Kasikorn Bank', 'Credit Card', 190.50, '2023-08-12', 'Pending', 28),
(67, 'Visa', 'Debit Card', 220.00, '2024-01-20', 'Success', 29),
(68, 'E Wallet', 'Online', 130.75, '2023-09-28', 'Pending', 30),
(69, 'Cash Payment', 'Cash', 170.00, '2024-02-15', 'Success', 31),
(70, 'TMB Bank', 'Credit Card', 140.25, '2024-03-05', 'Pending', 32);
-- Newid () function used to generate any random information. 
SELECT * FROM Payment 
ORDER BY NEWID();

-- Inserting data into Maintenance Records table.
INSERT INTO Maintenance_records(Main_record_id, Main_record_date, Main_record_type, Main_record_description, Main_record_cost, 
Main_record_status, Veh_id) VALUES 
(71, '2023-08-05', 'Regular Checkup', 'Routine inspection and maintenance', 100.00, 'Completed', 1),
(72, '2023-09-12', 'Engine Repair', 'Repairing engine components', 250.50, 'In Progress', 2),
(73, '2023-07-20', 'Tire Replacement', 'Replacing worn-out tires', 180.75, 'Scheduled', 3),
(74, '2023-10-10', 'Oil Change', 'Changing engine oil and filter', 80.00, 'Completed', 4),
(75, '2023-11-15', 'Brake Inspection', 'Checking and maintaining brakes', 120.25, 'In Progress', 5),
(76, '2023-06-30', 'Transmission Service', 'Servicing transmission system', 200.50, 'Scheduled', 6),
(77, '2023-12-20', 'Suspension Repair', 'Repairing suspension components', 150.00, 'In Progress', 7),
(78, '2023-08-25', 'Electrical System Check', 'Checking and fixing electrical issues', 90.75, 'Completed', 8),
(79, '2024-01-05', 'Cooling System Maintenance', 'Maintaining cooling system components', 130.00, 'Scheduled', 9),
(80, '2023-09-28', 'Exhaust System Repair', 'Repairing exhaust system components', 110.25, 'In Progress', 10);
-- Newid () function used to generate any random information. 
SELECT * FROM Maintenance_records 
ORDER BY NEWID();

-- Inserting data into License Record table.
INSERT INTO License_record(License_id, License_number, License_holder_name, License_issue_date, License_expiry_date, License_type, 
License_holder_contact_num, Veh_id) VALUES 
(81, 2246, 'John Doe', '2022-05-15', '2025-05-15', 'Class C', '555-1234', 1),
(82, 7890, 'Jane Smith', '2021-08-20', '2024-08-20', 'Class D', '555-5678', 2),
(83, 4567, 'Robert Johnson', '2023-02-10', '2026-02-10', 'Class A', '555-9876', 3),
(84, 6680, 'Emily Davis', '2022-11-30', '2025-11-30', 'Class B', '555-4321', 4),
(85, 6789, 'Michael Brown', '2021-06-05', '2024-06-05', 'Class C', '555-8765', 5),
(86, 3456, 'Jessica White', '2023-09-18', '2026-09-18', 'Class D', '555-2345', 6),
(87, 9012, 'Daniel Garcia', '2022-04-12', '2025-04-12', 'Class A', '555-7890', 7),
(88, 5678, 'Olivia Miller', '2023-12-05', '2026-12-05', 'Class B', '555-3210', 8),
(89, 2345, 'Matthew Lee', '2021-10-25', '2024-10-25', 'Class C', '555-6789', 9),
(90, 4452, 'Sophia Taylor', '2023-07-15', '2026-07-15', 'Class D', '555-8901', 10);
-- Newid () function used to generate any random information. 
SELECT * FROM License_record 
ORDER BY NEWID();

-- Inserting data into Feedback Review table.
INSERT INTO feedback_review(Feed_review_id, Feed_review_rate, Feed_review_comments, Feed_review_submission_date, Emp_id, Tran_id, 
Cus_id) VALUES
(91, 4, 'Great service and clean vehicles.', '2023-08-10', 2, 24, 4),
(92, 5, 'The staff was very helpful and friendly.', '2023-09-15', 4, 28, 8),
(93, 3, 'Average experience can be improved.', '2023-06-05', 3, 25, 2),
(94, 5, 'Smooth transaction, highly recommend.', '2023-10-20', 5, 26, 6),
(95, 2, 'Vehicle had some issues, not satisfied.', '2023-11-25', 6, 27, 1),
(96, 4, 'Overall good experience will come again.', '2023-07-10', 8, 29, 9),
(97, 5, 'Excellent service, no complaints.', '2023-12-15', 7, 33, 3),
(98, 3, 'Average cleanlinesS could be better.', '2023-08-20', 9, 30, 7),
(99, 4, 'Friendly staff and quick process.', '2024-01-25', 11, 31, 10),
(100, 5, 'Highly satisfied, will recommend to others.', '2024-02-10', 10, 32, 5);
-- Newid () function used to generate any random information. 
SELECT * FROM feedback_review
ORDER BY NEWID();

-- Step 4: We're going to make our own questions and answers using the JOIN function. 
-- Q1: I want to retrieve the details of all transactions along with the customer names. 
SELECT Transaction_table.*, Customer.Cus_firstname, Customer.Cus_lastname
FROM Transaction_table 
JOIN Customer ON Transaction_table.Cus_id = Customer.Cus_id;

-- Q2: I want to see a list of vehicles under maintenance with their maintenance records. 
SELECT Vehicles.*, Maintenance_records.*
FROM Vehicles 
JOIN Maintenance_records ON Vehicles.Veh_id = Maintenance_records.Veh_id 
WHERE Maintenance_records.Main_record_status = 'In Progress';


-- Q3: I want to see the appointments scheduled, including customer and employee information. 
SELECT Appointment.*, Customer.Cus_firstname AS Customer_firstname, Customer.Cus_lastname AS Customer_lastname, 
Employee_table.Emp_firstname AS Employee_firstname, Employee_table.Emp_lastname AS Employee_lastname 
FROM Appointment 
JOIN Customer ON Appointment.Cus_id = Customer.Cus_id 
JOIN Employee_table ON Appointment.Emp_id = Employee_table.Emp_id;

-- Q4: I want to see feedback and reviews along with the employee names. 
SELECT feedback_review.*, Employee_table.Emp_firstname, Employee_table.Emp_lastname 
FROM feedback_review 
JOIN Employee_table ON feedback_review.Emp_id = Employee_table.Emp_id;


-- Q5: I want to see the vehicles with their license details, including License Holder's name. 
SELECT Vehicles.*, License_record.License_number, License_record.License_holder_name
FROM Vehicles
JOIN License_record ON Vehicles.Veh_id = License_record.Veh_id;

-- Q6: I want to see the payment information for transactions along with the payment method used. 
SELECT Payment.*, Transaction_table.Tran_name, Transaction_table.Tran_type
FROM Payment
JOIN Transaction_table ON Payment.Tran_id = Transaction_table.Tran_id;

Step 5: I’m going to show you the table diagram of all objects and entities here.
![entity relationship_car rental](https://github.com/AuntBawHein/Car_Rental_Management_System_SQL_project/assets/150255399/167142c5-98d9-490a-850b-364bfc59fc6b)


Step 6: I’m going to show you SQL Car Rental Management System Project database.
 [Car_Rental_Management_System_project_datbase_words_sql.docx](https://github.com/AuntBawHein/Car_Rental_Management_System_SQL_project/files/14391958/Car_Rental_Management_System_project_datbase_words_sql.docx)


Thank you very much. 





