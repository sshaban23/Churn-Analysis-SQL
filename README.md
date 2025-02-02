# Churn SQL Analysis

This is an Analysis on a telecom client that wanted to decrease their churn rates. 

A: QUESTION:

How many customers with DSL internet - that are on a month-to-month contract - have churned?

A1: QUESTION JUSTIFICATION:

I believe this is a good question because we can find out how many people have churned that have DSL and also maybe it can give us insights into why they churned. This question will make us ask think about possible issues like “is our service lacking in any way?” or “Are our prices too high and customers are finding better deals?”
I will answer the question by searching the data to see which customers have a DSL internet service from the services.csv file, then I would look at the contracts table to see which customers have a month-to-month contract and finally look at the customers table to see how many customers have churned.

A2: IDENTIFYING DATA:

I decided to use the churn database and the services.csv. I specifically used the contract table, the customers table, and the services table that I created from the csv file. I also used the internetService column to be able to see which customers have “DSL” internet service from the services table. Then from the contract table I used the contract_id and looked for the ID that shows a month-to-month contract which is 1. After that I looked at the customer table to get the churn column and filtered it to only show the rows that were ‘Yes’.
I used the customer_id column to link the customers table to the Services.csv table, then I used the churn column, contracts column from the customers table and also the contract_id from the contract’s table.

B: ENTITY RELATIONSHIP DIAGRAM:

![image](https://github.com/user-attachments/assets/dd08f9df-9df6-4046-866e-6b87fe83f975)

B1: RELATIONSHIP DISCUSSION:

In the services to customer table, it is a 1:M relationship because one customer can have multiple services, but each service entry in the "Services" table is related to only one customer.
In the Customer to Contract table the relationship is 1:1 because each customer is associated with a single contract, and each contract relates to only one customer.

B2: STATEMENT FOR THE ERD:

      CREATE TABLE "Services" (

        "customer_id" text,
  
        "internetservice" text,
  
        "phone" boolean,
  
        "multiple" boolean,
  
        "onlinesecurity" boolean,
  
        "onlinebackup" boolean,
  
        "deviceprotection" boolean,
  
         "teachsupport" boolean,
  
          CONSTRAINT "FK_Services.customer_id"
  
          FOREIGN KEY ("customer_id")
    
           REFERENCES "Customer”
              );



B3: LOADING CSV DATA:


      --command " "\\copy public.services 

      FROM 'C:/LabFiles/Services.csv' 

      DELIMITER ',' CSV HEADER QUOTE '\"' ESCAPE '''';""


C: SQL QUERY:


      SELECT churn, internetservice, contract_id, COUNT(internetservice)
      FROM customer
      INNER JOIN services ON customer.customer_id = services.customer_id
      WHERE churn = 'Yes' AND internetservice = 'DSL' AND contract_id = 1
      GROUP BY churn, internetservice, contract_id;



































