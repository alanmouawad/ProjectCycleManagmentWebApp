Project Management System (PMS)

📌 Overview

PMS is an enterprise-grade, compliance-driven web application built on ASP.NET Core 5.0 MVC. The platform is purposefully architected to orchestrate, track, and evaluate multi-sector humanitarian interventions, protection cases, field vulnerability assessments, and medical response pipelines.

Designed specifically for Non-Governmental Organizations (NGOs) and humanitarian actors, the system securely manages detailed beneficiary demographics, structures educational and community implementations into programmatic cycles, handles cross-departmental referrals, ensures donor accountability, and processes real-time crisis diagnostic surveys.

________________________________________
🏗️ Architectural Core & Design Patterns

The platform implements a highly decoupled Service-Oriented Architecture (SOA) combined with domain separation principles:

[ Presentation Layer (ASP.NET Core MVC / Razor Views) ]

                           │
                           
                           ▼
                           
 [ Business Logic Layer (Contracts & Bus Implementations) ] (e.g., IAgentBus, ICycleBus)
 
                           │
                           
                           ▼
                           
 [ Infrastructure / Data Access Layer (EF Core + SQL Server) ]
 
 
•	Separation of Concerns: Controllers act strictly as thin entry-point orchestrators. All underlying business rules, validation loops, and data flow decisions are delegated through constructor Dependency Injection to a dedicated service layer utilizing a Bus naming convention (e.g., IAgentBus, ICycleBus, IFormQuestionBus, IUserBus, IRoleBus).
•	Advanced URL Cryptography Security: To protect highly sensitive field records and prevent horizontal privilege escalation or enumeration attacks, public route query strings (such as ProjectId) are fully encrypted via an AesCryptoServiceProvider implementing custom 32-byte secret key matrices.
•	Granular Access Control (RBAC & CBAC): Built on Microsoft Identity infrastructure. Administrative, financial, and policy tools are structurally isolated using custom claims and role-based filters (e.g., [Authorize(Roles = "SuperAdmin")] or [Authorize(Roles = "Admin,Finance")]).
•	Dynamic Linq Expressions: Integrates runtime dynamic expression parsing (System.Linq.Dynamic.Core) across heavy reporting views to enable fluid, asynchronous server-side sorting, pagination, and multi-variable table filtering.

________________________________________

🛠️ System Modules & Domain Capabilities

1. Advanced Beneficiary & Household Lifecycle Management
•	Socio-Demographic Profiling: Tracks comprehensive attributes of individuals, including legal documentation status, military/civil registry standing, housing/shelter classifications, and educational backgrounds.
•	Family Unit Framework: Maps individuals into structural households, programmatically distinguishing a primary head of household ("Agent") from dependents or children.
•	Conflict of Interest Auditing: Enforces strict compliance checks by logging and auditing potential relationship overlaps between prospective aid applicants and active internal organization staff.
2. Multi-Tier Regional Hierarchy & Geo-Siloing
•	Operates on a tightly nested, 5-tier regional taxonomy database:
$$\text{Governorate (Gov)} \longrightarrow \text{District} \longrightarrow \text{Sub-District} \longrightarrow \text{Community} \longrightarrow \text{Neighbourhood}$$
•	Filters active data grids, workspaces, and lookups based on the logged-in user's assigned GovernorateId, maintaining regional data sovereignty and strict field isolation.
3. Programmatic Service Cycles & Cohorts
•	Cycles & Grades: Groups long-term humanitarian interventions into sequential "Cycles," further segmented into granular curriculum milestones or performance assessment levels called "Grades."
•	Cycle Groups: Coordinates delivery cohorts by pinning target beneficiary lists to specific regional project branches and timeframes to continuously evaluate progress metrics.
4. Dynamic Forms Engine & Crisis Diagnostics
•	Runtime Survey Builder: Utilizes an extensible question schema configuration allowing administrators to dynamically inject custom field questions, valid response options, and scoring definitions without modifying backend code.
•	Protection Frameworks: Integrates workflows aligned with international protection standards (e.g., UNHCR Protection Risk Classifications) along with tailored follow-up steps for dedicated protection casework.
•	Rapid Field Diagnostics: Features high-performance analytical modules optimized for emergency crisis assessments (such as immediate market and basic needs evaluations following natural disasters), outputting data counts directly to dashboard metrics.
5. Inter-Departmental Referrals & Alert Hub
•	Referral Lifecycle Management: Safely transfers sensitive cases (e.g., specialized medical referrals or emergency shelter placement requests) between external provider nodes or internal teams, tracking states through strict workflows (Pending, Closed, Deleted).
•	Centralized Alert Board: Uses an integrated notification subsystem (NotifiyController) to instantly brief caseworkers when emergency feedback is submitted, steps are delayed, or case actions require attention.
6. Financial Controls & Medical Provider Disbursements
•	Restricts access to sensitive project financing, allocation matrices, and itemized billing logs entirely to authorized accounting roles.
•	Validates provider invoices and links financial disbursements to authorized networks of external clinics or suppliers matching the caseworker's regional security scope.
7. Asynchronous Mass Ingestion Pipeline
•	Leverages high-performance Excel parsing via EPPlus integrations. The ingestion pipeline reads heavy tabular worksheets, validates layout headers, and maps row arrays asynchronously to process bulk imports directly into the database, mitigating manual user data entry.

________________________________________

💻 Tech Stack

•	Backend Framework: ASP.NET Core 5.0 (Model-View-Controller Architecture)
•	Identity & Security: Microsoft ASP.NET Core Identity, AES-256 Symmetric Cryptography Engine
•	Data Access Layer: Entity Framework Core (EF Core) via ApplicationDbContext, LINQ Dynamic Query Execution
•	Task Automation: Hangfire Service Pipelines (Background Processing Engine)
•	Reporting Services: SQL Server Reporting Services (SSRS) Client integrations, EPPlus Excel Management Hub
•	Frontend Layer: Razor Views, Bootstrap Dashboard Shells, jQuery, JSON Grid Components.

