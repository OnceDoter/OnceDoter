# Portfolio of tasks
## 'Loymax' a. 3 years experience
> Loymax - loyalty program management and marketing communications automation platform for retail chains
1.  Integration of Quartz.net task scheduler as a Windows service. Implementation of the following features:
    -   Default calendars (daily, weekly, etc.).
    -   Ability to manually start and interrupt tasks.
    -   Ability to pause recurring tasks.
    -  User interface (UI).

2.  Adding a `/health` route to all ASP.NET472 services for health checks and incorporating these checks into CI/CD pipelines after deployment (utilized Azure DevOps). 

3.  Optimization of hierarchical structures (product catalogs) based on `hierarchicallyId`. Later, implementation of pre-calculations and transition to the `table-closure` structure resulting in a computation increase of up to 15 times.

4.  Target Audience Optimization (CRM). The main idea was to create a single entry for pre-calculation of target audiences. The client had to aggregate in itself all methods of interaction + results (client attributes).
General information about customer attributes was presented in JSON format (cards, balance, purchases, favorite products, registrations, personalized offers, etc.). Client attributes were retrieved in one request. All target audiences were cached, which made it possible to check and match the target audience filters in the application's memory and determine which promotions should be applied.

### Most Important Task. Event-source purchase History service
1. Formulation of the problem:
    -   The purchase has a pipeline. Conditionally: discount calculations + accrual of bonuses at least.
    -   By that time, the number of purchases was more than int32.
    -   Each historical record weighed 1.5kb.
    -   The consumer did not have time to process the purchase history queue.
    -   History needs to be constantly updated.

2. Solve:
    -   Batch consuming.
    -   Event-source. To avoid long inserts and decisions about what to insert and what to update. Just bulk insert.
    -   Non-relational representation of an entity. All information that is not needed for indexing is stored in the document view(.proto). 
    -   Background gluing of records, to reduce memory.
    -   Using flags to save all combinations of activity types and types of accruals or write-offs in a purchase.

3. In total:
    -   Reducing the occupied disk space of the database by 5 times.
    -   Processing speed 12 thousand records per minute.
    -   API fast. Because there are no joins and it is easy to get all the customer's purchases, with all the information in them (discounts, checking positions, accruals, etc.). 
## 'AgroHistory' a. half years experience
> Loymax - integrated automation  agricultural enterprise
1.  Refactoring. Implementing soft delete everywhere.
2. Optimization of vehicle tracks.
