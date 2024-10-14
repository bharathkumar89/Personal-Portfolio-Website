# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh



CREATE SCHEMA library;
CREATE TABLE library.Worker (
    WORKER_ID SERIAL PRIMARY KEY,
    FIRST_NAME VARCHAR(50) NOT NULL,
    LAST_NAME VARCHAR(50) NOT NULL,
    SALARY DECIMAL(10, 2) NOT NULL,
    JOINING_DATE DATE NOT NULL,
    DEPARTMENT VARCHAR(50) NOT NULL
);
CREATE TABLE library.Title (
    WORKER_REF_ID INT REFERENCES library.Worker(WORKER_ID) ON DELETE CASCADE,
    WORKER_TITLE VARCHAR(50) NOT NULL,
    AFFECTED_FROM DATE NOT NULL,
    PRIMARY KEY (WORKER_REF_ID, AFFECTED_FROM)
);
CREATE TABLE library.Bonus (
    WORKER_REF_ID INT REFERENCES library.Worker(WORKER_ID) ON DELETE CASCADE,
    BONUS_AMOUNT DECIMAL(10, 2) NOT NULL,
    BONUS_DATE DATE NOT NULL,
    PRIMARY KEY (WORKER_REF_ID, BONUS_DATE)
);
INSERT INTO library.Worker (FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
('Monika', 'Arora', 100000, '2020-02-14', 'HR'),
('Niharika', 'Verma', 80000, '2011-02-14', 'Admin'),
('Vishal', 'Singhal', 300000, '2020-02-14', 'HR'),
('Amitabh', 'Singh', 500000, '2020-02-14', 'Admin'),
('Vivek', 'Bhati', 500000, '2011-06-14', 'Admin'),
('Vipul', 'Diwan', 200000, '2011-06-14', 'Account'),
('Satish', 'Kumar', 75000, '2020-01-14', 'Account'),
('Geetika', 'Chauhan', 90000, '2011-04-14', 'Admin');

INSERT INTO library.Title (WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM) VALUES
(1, 'Manager', '2016-02-20'),
(2, 'Executive', '2016-06-11'),
(3, 'Executive', '2016-06-11'),
(4, 'Manager', '2016-06-11'),
(5, 'Asst. Manager', '2016-06-11'),
(6, 'Executive', '2016-06-11'),
(7, 'Lead', '2016-06-11'),
(8, 'Lead', '2016-06-11');

INSERT INTO library.Bonus (WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES
(1, 5000, '2020-02-16'),
(2, 3000, '2011-06-16'),
(3, 4000, '2020-02-16'),
(1, 4500, '2020-02-16'),
(2, 3500, '2011-02-16'),
(4, 4500, '2020-02-16'),
(5, 3500, '2011-02-16');

SELECT 
    Worker.FIRST_NAME, 
    Worker.SALARY, 
    Title.WORKER_TITLE 
FROM 
    Worker 
INNER JOIN 
    Title 
ON 
    Worker.WORKER_ID = Title.WORKER_REF_ID;
