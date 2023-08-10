# Company-RDBMS-With--MySQl.

CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(40),
    last_name VARCHAR(40),
    birth_day DATE,
    sex VARCHAR(1),
    salary INT,
    super_id INT,
    branch_id INT
);


CREATE TABLE branch (
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(40),
    mgr_id INT,
    mgr_start_date DATE,
    FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
);


ALTER TABLE employee
ADD FOREIGN KEY(branch_id)
REFERENCES branch(branch_id)
ON DELETE SET NULL;

ALTER TABLE employee
ADD FOREIGN KEY(super_id)
REFERENCES employee(emp_id)
ON DELETE SET NULL;


CREATE TABLE client(
    client_id INT PRIMARY KEY,
    client_name VARCHAR(40),
    branch_id INT,
    FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE SET NULL
);


CREATE TABLE works_with(
    emp_id INT,
    client_id INT,
    total_sales INT,
    PRIMARY KEY(emp_id, client_id),
    FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE,
    FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE
);


CREATE TABLE branch_supplier (
    branch_id INT,
    supplier_name VARCHAR(40),
    supply_type VARCHAR(40),
    PRIMARY KEY(branch_id, supplier_name),
    FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
);

INSERT INTO employee VALUES(100, 'David', 'Wallace', '1999-11-11', 'M', 25000, NULL, NULL);

INSERT INTO branch VALUES(1, 'Corporate', 100, '2006-01-01');

UPDATE employee
SET branch_id = 1
WHERE emp_id = 100;


INSERT INTO employee VALUES(101, 'jane', 'Levinson', '1999-11-11', 'F', 25000, 100, 1);

INSERT INTO employee VALUES(102, 'Michael', 'Scott', '1999-11-11', 'F', 25000, 100, NULL);

INSERT INTO branch VALUES(2, 'Scrant', 102, '2006-01-01');

UPDATE employee
SET branch_id = 2
WHERE emp_id = 102;


INSERT INTO employee VALUES(103, 'Angela', 'Martin', '1999-11-11', 'F', 25000, 102, 2);
INSERT INTO employee VALUES(104, 'Kelly', 'Kapoor', '1999-11-11', 'F', 25000, 102, 2);
INSERT INTO employee VALUES(105, 'Stanley', 'Hudson', '1999-11-11', 'M', 25000, 102, 2);


INSERT INTO branch VALUES(3, 'Stamp', NULL, '2006-01-01');

INSERT INTO branch_supplier VALUES(2, 'HAMMER MILL', 'PAPER');
INSERT INTO branch_supplier VALUES(2, 'Uni_ball', 'INK');
INSERT INTO branch_supplier VALUES(3, 'Patriot Paper', 'PAPER');
INSERT INTO branch_supplier VALUES(2, 'PENCİL CO', 'Pencil');
INSERT INTO branch_supplier VALUES(3, 'Uni_ball', 'Ink');
INSERT INTO branch_supplier VALUES(3, 'HAMMER MILL', 'PAPER');
INSERT INTO branch_supplier VALUES(3, 'Stamp Lables', 'Pencil');

INSERT INTO employee VALUES(106, 'Josh', 'Porter', '1999-11-11', 'M', 25000, 100, 3);
INSERT INTO employee VALUES(107, 'Andy', 'Brnard', '1999-11-11', 'M', 25000, 106, 3);
INSERT INTO employee VALUES(108, 'Jim', 'Harper', '1999-11-11', 'M', 25000, 106, 3);


UPDATE branch
SET mgr_id = 106
WHERE branch_id = 3;

INSERT INTO client VALUES(400, 'D HighSchool', 2);
INSERT INTO client VALUES(401, 'L Country', 2);
INSERT INTO client VALUES(402, 'FEDEX', 3);
INSERT INTO client VALUES(403, 'Jon Law, LLC', 3);
INSERT INTO client VALUES(404, 'S Whitepages', 2);
INSERT INTO client VALUES(405, 'X NewsPaper', 3);
INSERT INTO client VALUES(406, 'FEDEX', 2);




INSERT INTO works_with VALUES(105, 400, 55000);
INSERT INTO works_with VALUES(102, 401, 65000);
INSERT INTO works_with VALUES(108, 402, 58000);
INSERT INTO works_with VALUES(107, 403, 78000);
INSERT INTO works_with VALUES(108, 403, 62000);
INSERT INTO works_with VALUES(105, 404, 55000);
INSERT INTO works_with VALUES(107, 405, 55000);
INSERT INTO works_with VALUES(102, 406, 55000);
INSERT INTO works_with VALUES(105, 406, 55000);
