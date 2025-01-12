# CV Pavel Gordeev  

### .NET C# | Backend Developer  

## Contacts  
- **Email:** [kreozenbook@outlook.com](mailto:kreozenbook@outlook.com)  
- **Skype:** kreozenbook@outlook.com  
- **LinkedIn:** [linkedin.com/in/paveld271](https://www.linkedin.com/in/paveld271)  
- **Telegram:** [@epashora](https://t.me/epashora)  

---

## Profile  

Experienced software developer with deep knowledge and extensive experience in the development of geoinformation systems, payment solutions, and electronic document management systems. I specialize in building applications with complex architectures designed for high loads, including modular monoliths and microservices using gRPC/REST.  

I have extensive experience integrating with third-party services such as Zapier, as well as social networks (VK, Facebook, and others). My significant expertise in Observability enables me to make projects more efficient, stable, and convenient for diagnostics and troubleshooting.  

---

## Skills  

- **Programming:** .NET, C#, MS SQL, PostgreSQL, Redis  
- **Messaging & Cloud:** RabbitMQ, Azure Service Bus, AWS SES  
- **Monitoring & Logging:** ELK, Azure Log Analytics, Prometheus  
- **ORM & Tools:** Entity Framework, Dapper  
- **Infrastructure as Code:** Terraform  
- **Authentication:** Identity Server 4  
- **Version Control & CI/CD:** Azure DevOps, GitHub, GitLab, Bitbucket  

---

## Courses  

- **AWS Services for C# Developers (2024)**  

---

## Experience  

### **2024 – Present: ApprovalMax ([approvalmax.com](https://approvalmax.com))**  
**Responsibilities:** Feature implementation for a document approval project.  

**Key tasks:**  
- Configured GitHub Actions for automatic code formatting to maintain a unified code style.  
- Migrated from vulnerable or unsupported libraries and split internal builds into smaller components to optimize dependency management and build performance in CI/CD pipelines.  
- Developed a logger for third-party developers based on Azure Log Analytics tables, supporting flexible date filters in ISO 8601 format.  
- Integrated with Zapier to enable custom automation workflows.  

---

### **2023 – 2024: AgroHistory ([info.agrohistory.com](https://info.agrohistory.com))**  
**Responsibilities:** Maintenance and global refactoring of the existing solution for an agricultural enterprise automation system.  

**Key tasks:**  
- Architectural-level optimization: implemented pagination, added support for request cancellation, and redesigned database indexing.  
- Refactored the authorization system and transitioned to a CQRS pattern.  

---

### **2020 – 2023: Loymax ([loymax.ru](https://loymax.ru))**  
**Responsibilities:** Initially supported the loyalty program system. Later, as a team lead, was responsible for implementing and optimizing high-load services and aligning requirements with partners.  

**Key tasks:**  
- Designed indexes, reengineered complex queries, and implemented bulk operations.  
- Developed an event-source pattern for efficient historical data processing.  
- Justified and executed a migration from relational to document-based storage.  
- Created an internal project library for metrics collection, including tail-sampling support and integrations with RabbitMQ, EF, and Quartz.  
- Integrated Quartz.net task scheduler and developed a custom user interface for it.  
- Implemented health checks for service state monitoring and integrated them into the CI/CD pipeline.  
- Optimized hierarchical catalog structures by transitioning from HID to closure-table, improving catalog performance by 15 times.  
- Integrated APIs for VK and Huawei Mobile Services.  


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
