https://whimsical.com/test-MEroDVsnq8DgZp5d4SEZnL

Notes:

What will the system achieve?
What are the requirements?

About order promising - 
The Order Promising functionality enables us to promise an order to be shipped or delivered to a customer on a specific date. The functionality calculates the earliest possible date that an item is available for shipment or delivery. It also creates order lines or requisition lines in case the items must first be purchased or produced, for those dates. 
It can interact with systems such as Order, Inventory, Sales Returns, production planning, transfers, and shipping/delivery system etc.
Some considerations will come to play too such as – 
Are we to consider multiple warehouses in our calculations?
If so no transfers, if not use scheduled transfers in calculations.
This can be done using 2 fundamental concepts:
•	Available to Promise Date (ATPD)
•	Capable to Promise Date (CTPD)

Available to promise Date:
Available to promise Date (ATPD) calculates dates based on availability of stock/ inventory, planned production, purchases, transfers, and sales returns. 
When requested delivery date is provided for a Sales Order line, the shipment date can be calculated as follows:  

•	requested delivery date - shipping time = planned shipment date
•	planned shipment date - outbound WH handling time = shipment date
If the items are available to pick on the shipment date, then the sales process can continue. If the requested delivery date can't be met, then the earliest date on which that items are available is calculated using Capable to Promise Date (CTPD).
Capable to promise Date:
Capable to promise (CTPD) assumes a “what if” scenario, which only applies to item quantities that aren't in inventory or on scheduled orders. Based on this scenario, we can calculate the earliest date that the item can be available if it's to be produced, purchased, or transferred.
Example
If there's an order for 10 pieces, and 6 pieces are available in inventory or on scheduled orders, then the capable to promise calculation will be based on 4 pieces.
Calculations
•	Shipment Date + Outbound Warehouse Handling Time = Planned Shipment Date
•	Planned Shipment Date + Shipping Time = Planned Delivery Date
The CTP calculation takes longer but it gives an accurate date when the customer can expect to have the item delivered.
Non-Functional Requirements:
Availability – Highly available we aim for 99.9% availability.
Reliability – error free, consistent in output, and gracefully recover from errors.
Performance – process request and respond fast, we aim 2 seconds response time.
Scalability – Should scale efficiently to handle increases in users and request.
Security – Secure access, protect personal information and comply with GDPR.

Functional Requirements:


Reliability: 
Use coding standards, Reviews, Code analysis (SonarQuebe, sonarlite, checkstyle), Partition Database, cluster multiple servers, handle exceptions and implement logging for diagnosis and debugging, Use version control to track changes, keep development, testing and production servers and environments as similar as possible to avoid env change issues. Use CICD pipelines, implement Blue/Green deployments, Monitor and Alert and track metrics, Take regular backups, and have a disaster recovery plan.
 
Performance: 
Load times, response time should be less than 3 seconds 
To achieve – 
Use Microservices
Review code to spot issues and refactor – using SCM
Use best algorithms and efficient data structures.
Performance Testing and profiling of code.
Introduce data caching – Hazelcast, Redis, Ehcache, Memcache, Guava Cache, CDN
Database query caching
Resource caching using CDN and external object storage such as AWS 
Introduce continuous monitoring – using tools like Grafana, Splunk, New Relic, Dynatrace, AppDynamics, Datadog, Amazon cloudwatch etc.
Optimise critical code blocks like IO operations, loops etc using concurrency, asynchronous and parallel functions.
Use Load balancers for API servers and database servers.
Run multiple instances using containers and manage them with Kubernetes.
Leverage database partitioning and shardding.
Avoid calculations in loops.

Scalability: Load Balancer, Kubernetes autoscaling
Availability: Swarm, compose, Kubernetes autoscaling
Security: OAuth2, Encryption, Hashing


 


APIs

Create customer - POST /customer
Fetch customer - GET /customer/{customerid}
Update customer - PUT /customer/{customerid}

Create order – POST /order
Fetch order – GET /order/{orderid}
Fetch orders – GET /order/{customerid}/
Update Order - POST /order/{orderid}

Reserve orderline – POST /orderline/{inventoryid}
Fetch ordelines – GET /orderline/{orderid}
Update orderrline – PUT /orderline/{orderlineid}

Send Notification - POST /notification

Internal APIs:
Get available quantity – GET /inventory/{inventoryid}

Get available planned production quantity - /production/{inventoryid}
Get planned purchase quantity - /purchase/{inventoryid}
Get planned transfer quantity - /inventory-transfer/{inventoryid}
Get planned sales return quantity - /sales-return/{inventoryid}

Get invoice link – GET /resources/{orderid}




CustomerService - 
OrderService - 
OrderReservationService - 
InventoryService - 
OrderPromiseDateService - 
ResourceService – 
NotificationService –
DeliveryService -


PaymentService – External (stripe, worldpay etc.)


To scale:

OrderMessageService – publish subscribe – (Active MQ, RabbitMQ)
InventoryService - publish subscribe – (Active MQ, RabbitMQ
Using Streams API

Write a Java program that creates a List of Integers called intList. 

Add Integer 1, 3, 2, 4 and 6 into intList and display the numbers added to intList. 

Create and display a new List from intList containing only even numbers in intList without using the new ArrayList construct and without losing the contents of intList. 

Now using Java 8 fiirst display the min number in the intList. 

Second display the max number in intList. 

Sort intList in ascending Order and display the contents

Next find the Mean number and the median number of the numbers in intList and display them using Java 8 streams. 

Now stream intList and display all even numbers if the number encountered is not even then display 0 using Java8 construct and avoid casting to Optional. 

Finally, go through intList stream and use 2 buckets to store first bucket stores even numbers and second bucket stores odd number and display the contents of these 2 buckets using java8. 

What is the different between partitioningBy and groupingBy 

Show how you would use partitioningBy and groupingBy respectively to achieve the filtering and storage of the even and the odd numbers in intList into 2 buckets and display them.

Document your work and explain your solution at every stage.  


![image](https://github.com/betrand/reservation/assets/5835727/00b464c2-5733-4532-8fd9-a8153840143f)
