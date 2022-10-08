# Pewlett_Hackard_Analysis

## Overview of Analysis

The purpose of the analysis was to determine how many employees per title are retiring from Pewlett Hackard, and how many of those employeees are eligible to participate in a mentorship program. Some preliminary questions we had to find the answers to in order to get to our final conclusion included: Who will be retiring in the next few years? And how many positions will Pewlett Hackard need to fill? By using only 6 csv files provided, we used SQL not only to find answers to these questions, but also to create various tables showcasing the data in different ways.  

## Results

There are a number of points that we can take away from the tables we've produced.

- One, of those retiring, Engineer, Staff and Senior Engineer are the top three titles. By using the following code, we can produce a table that shows us this information clearly:

SELECT COUNT(title), title FROM retirement_titles
GROUP BY title
ORDER BY count DESC;

<img width="258" alt="Screen Shot 2022-10-08 at 1 22 11 PM" src="https://user-images.githubusercontent.com/110838228/194719782-02447d8d-fb81-49bf-b4d4-364d7d22524e.png">

- Additionally, the above table brings an interesting fact to light - there are a significant amount of people retiring without Senior or otherwise 'senority insinuating' titles. This could mean two things: one, PH does not give away many promotions during their employees time at their company. This is a problem! Two, it raises questions regarding what "retirement" might mean for these individuals. It very well could mean that each employees are retiring under the traditional assumption that they are done working, or, it could insinuate that, because many of these job titles are lower-level (i.e. Assistant Engineer) that some employees are "retiring" to move onto another company that might promote them to a higher-ranking title.

- There are 1,549 employees eligible for the mentorship program upon retiring. By using the code below, we can create a table that counts each unique employee number. If we scroll to the bottom of the table, we can see the index number that essentially gives us a count.

SELECT COUNT(emp_no), emp_no FROM mentorship_eligibility
GROUP BY emp_no;

<img width="208" alt="Screen Shot 2022-10-08 at 1 34 53 PM" src="https://user-images.githubusercontent.com/110838228/194720305-482b26b8-fdf7-4ff9-8fa3-e720aa708315.png">

- Among those who are eligible for the mentorship opportunity, the starting dates each employee spent in their department ranges from Feb 17, 1989, to July 27, 2002. That is quite the span of time! This data can be used to inform PW how to navigate internal employee efforts, including various programs, celebrations and connection points between folks of different generations and life experiences. The code below is what we can use to get this date range:

SELECT DISTINCT ON (from_date) from_date FROM mentorship_eligibility
GROUP BY from_date
ORDER BY from_date ASC;


## Summary

- How many roles will need to be filled as the "silver tsunami" begins to make an impact? Put simply, 1,637 roles will need to be filled if PW wants to replace employees 1:1. The query we can run to figure out this number is below:

SELECT DISTINCT ON (last_name) last_name FROM retirement_titles;

Here, we are selecting each distinct last name from our retirement_titles table, which is already filtered to those who are retiring. If we scroll to the bottom of the table, we find this number in the index column.

- Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees? Yes. As we saw above, there are 1,549 employees eligible for the mentorship program, which is roughly 95% of the employees who are retiring. This means that if PW hired one new employee for every employee retiring, almost all new employees would be able to have their own mentor, and their mentor each have their own employee. Here is the code to answer this question:

SELECT COUNT(emp_no), emp_no FROM mentorship_eligibility
GROUP BY emp_no;
 








