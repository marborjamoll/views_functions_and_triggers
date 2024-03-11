# Views, functions and triggers
## Views exercises
### Exercise 1: Create a Complex View
Suppose you have a sales table with sale_id, employee_id, sale_amount, and sale_date columns, and you want to create a view that shows the total sales amount for each employee this year. Create a view named view_employee_sales_year that accomplishes this.

Given a `sales` table, we want to create a view that shows the total sales amount for each employee this year. Assuming our `sales` table looks like this:

-   `sale_id` INT
-   `employee_id` INT
-   `sale_amount` DECIMAL
-   `sale_date` DATE

And assuming "this year" refers to the current year dynamically, here is how you could create the view:
``` sql 
CREATE  VIEW view_employee_sales_year AS
SELECT employee_id, SUM(sale_amount) AS total_sales 
FROM sales 
WHERE sale_date >= '01-01-2024'  
GROUP  BY employee_id;
``` 
This view calculates the sum of `sale_amount` for each `employee_id` where the `sale_date` falls within the current year, from January 1st.

### Exercise 2: Update View
To update the `view_employee_details` view to include the `salary` column, we would first need to drop the existing view and then recreate it with the additional column, as PostgreSQL doesn't allow the direct modification of view definitions. Here's how you can do it:
```  sql 
DROP VIEW view_employee_details;

CREATE VIEW view_employee_details AS
SELECT name, department, salary
FROM employees;
```

or

```  sql 
CREATE OR REPLACE VIEW view_employee_details AS
SELECT name, department, salary
FROM employees;
```

This recreates the `view_employee_details` view to now include the `name`, `department`, and `salary` columns from the `employees` table.

### Exercise 3: Using a View in a Query
To find all employees who work in the "IT" department using the `view_employee_department` view, we'll assume that the `department_name` is a straightforward match for "IT". The query might look like this:

``` sql
SELECT *
FROM view_employee_department
WHERE department_name = 'IT';
```
This query selects all columns from the `view_employee_department` where the `department_name` is "IT". Note that for this query to work as intended, the `view_employee_department` view must be correctly defined to include the `department_name` field, which relates to departments including an "IT" department.
