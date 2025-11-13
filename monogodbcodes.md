Q.1 Demonstrate all types of JOIN on following schema customer (customer_id, first_name) orders(order_id,amount,customer_id)
DROP TABLE IF EXISTS orders;
DROP TABLE IF EXISTS customer;

CREATE TABLE customer (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    amount DECIMAL(10,2),
    customer_id INT
);


INSERT INTO customer (customer_id, first_name) VALUES
(1, 'Alice'),
(2, 'Bob'),
(3, 'Charlie');

INSERT INTO orders (order_id, amount, customer_id) VALUES
(101, 250, 1),
(102, 450, 1),
(103, 300, 2),
(104, 150, 4);   
SELECT 
    c.customer_id,
    c.first_name,
    o.order_id,
    o.amount
FROM customer c
INNER JOIN orders o
ON c.customer_id = o.customer_id;


SELECT 
    c.customer_id,
    c.first_name,
    o.order_id,
    o.amount
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id;

SELECT 
    c.customer_id,
    c.first_name,
    o.order_id,
    o.amount
FROM customer c
RIGHT JOIN orders o
ON c.customer_id = o.customer_id;








Q6. Create a collection Employee in MongoDB(emp_id,emp_name,dept_name,sal) 1. Insert few documents in collection. 2. Find employees having salary greater than 50000 3. Find employees having salary between 50000 and80000 4. Find employees having salary more than 60000 from ‘HR’ department 5. Delete employees from ‘Finance’ department having salary less than 10000.
ANS:
use companyDB;

db.Employee.insertMany([
  { emp_id: 1, emp_name: "Alice", dept_name: "HR", sal: 55000 },
  { emp_id: 2, emp_name: "Bob", dept_name: "Finance", sal: 9000 },
  { emp_id: 3, emp_name: "Charlie", dept_name: "IT", sal: 75000 },
  { emp_id: 4, emp_name: "David", dept_name: "HR", sal: 62000 },
  { emp_id: 5, emp_name: "Eve", dept_name: "Finance", sal: 15000 },
  { emp_id: 6, emp_name: "Frank", dept_name: "IT", sal: 82000 },
  { emp_id: 7, emp_name: "Grace", dept_name: "Sales", sal: 48000 }
]);

db.Employee.find({ sal: { $gt: 50000 } });

db.Employee.find({ sal: { $gte: 50000, $lte: 80000 } });

db.Employee.find({ dept_name: "HR", sal: { $gt: 60000 } });

db.Employee.deleteMany({ dept_name: "Finance", sal: { $lt: 10000 } });

db.Employee.find().pretty();






Q7. Create a collection Student in Mongo DB(stud_id,stud_name,dept_name,marks) 
1. Insert few documents in collection. 2. Find students having marks greater than 50. 3. Find students having marks between50and 80. 4. Find students having marks more than 60from ‘Computer’ department. 5. Update marks of all students from ‘Civil’ department. Set marks to 30.(Use update()) 6. Delete students from ‘Chemical’ department having marks less than 30
ANS:
use collegeDB;

db.Student.insertMany([
  { stud_id: 1, stud_name: "Amit", dept_name: "Computer", marks: 75 },
  { stud_id: 2, stud_name: "Bhavna", dept_name: "Civil", marks: 45 },
  { stud_id: 3, stud_name: "Chirag", dept_name: "Mechanical", marks: 82 },
  { stud_id: 4, stud_name: "Deepa", dept_name: "Computer", marks: 65 },
  { stud_id: 5, stud_name: "Esha", dept_name: "Chemical", marks: 25 },
  { stud_id: 6, stud_name: "Farhan", dept_name: "Civil", marks: 55 },
  { stud_id: 7, stud_name: "Gauri", dept_name: "Electrical", marks: 90 }
]);

db.Student.find({ marks: { $gt: 50 } });

db.Student.find({ marks: { $gte: 50, $lte: 80 } });

db.Student.find({ dept_name: "Computer", marks: { $gt: 60 } });

db.Student.updateMany({ dept_name: "Civil" }, { $set: { marks: 30 } });

db.Student.deleteMany({ dept_name: "Chemical", marks: { $lt: 30 } });

db.Student.find().pretty();



Q.8 Create a collection Book in MongoDB(Title,Description,Author,Publisher, URL,no_of_likes) 1. Add documents in collection. 2. Display all documents in collection. 3. Display a list stating how many books are written by each author. 4. Calculate the sum of no_of_likes from all documents in the collection for each Author. 5. Calculates the average of no_of_likes from all documents in the collection for each Author.
ANS:
use libraryDB;

db.Book.insertMany([
  { Title: "Book A", Description: "About A", Author: "Author1", Publisher: "Pub1", URL: "http://a.com", no_of_likes: 50 },
  { Title: "Book B", Description: "About B", Author: "Author1", Publisher: "Pub2", URL: "http://b.com", no_of_likes: 70 },
  { Title: "Book C", Description: "About C", Author: "Author2", Publisher: "Pub1", URL: "http://c.com", no_of_likes: 40 },
  { Title: "Book D", Description: "About D", Author: "Author2", Publisher: "Pub3", URL: "http://d.com", no_of_likes: 60 },
  { Title: "Book E", Description: "About E", Author: "Author3", Publisher: "Pub2", URL: "http://e.com", no_of_likes: 30 }
]);

db.Book.find().pretty();

db.Book.aggregate([
  { $group: { _id: "$Author", total_books: { $sum: 1 } } }
]);

db.Book.aggregate([
  { $group: { _id: "$Author", total_likes: { $sum: "$no_of_likes" } } }
]);

db.Book.aggregate([
  { $group: { _id: "$Author", avg_likes: { $avg: "$no_of_likes" } } }
]);
Q.9 Create a collection Book in MongoDB(Title,Description,Author,Publisher, URL,no_of_likes) 1. Add documents in collection. 2. Display all documents in collection. 3. Display a list stating how many books are published by each Publisher. 4. Gets the minimum of no_of_likes from all documents in the collection for each Author. 5. Gets the maximum of no_of_likes from all documents in the collection for each Author.
ANS:
use libraryDB;

db.Book.insertMany([
  { Title: "Book A", Description: "About A", Author: "Author1", Publisher: "Pub1", URL: "http://a.com", no_of_likes: 50 },
  { Title: "Book B", Description: "About B", Author: "Author1", Publisher: "Pub2", URL: "http://b.com", no_of_likes: 70 },
  { Title: "Book C", Description: "About C", Author: "Author2", Publisher: "Pub1", URL: "http://c.com", no_of_likes: 40 },
  { Title: "Book D", Description: "About D", Author: "Author2", Publisher: "Pub3", URL: "http://d.com", no_of_likes: 60 },
  { Title: "Book E", Description: "About E", Author: "Author3", Publisher: "Pub2", URL: "http://e.com", no_of_likes: 30 }
]);

db.Book.find().pretty();

db.Book.aggregate([
  { $group: { _id: "$Publisher", total_books: { $sum: 1 } } }
]);

db.Book.aggregate([
  { $group: { _id: "$Author", min_likes: { $min: "$no_of_likes" } } }
]);

db.Book.aggregate([
  { $group: { _id: "$Author", max_likes: { $max: "$no_of_likes" } } }
]);
