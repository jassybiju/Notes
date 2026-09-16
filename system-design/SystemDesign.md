# System Design

A - Ask Good Question ( What all features needed, How much scalability, )
B - Dont use **Buzzwords**
C - Have **CLEAR** & organized thinking ( dont gamble )
D - Drive discussion

Basic 
1. Understand the Features
2. Define the API
3. Availability ( How long should the project be available. )
4. Latency Performance ( L inverse propotional to P)
5. Scalability 
6. Durability and Consistency ( How consistent in the DB )
7. Class Diagram
8. Security and Privacy
9. Cost efficent

### System Design - 7 steps
1. Requirement Gathering ( features, no.of users, hardware)
2. API - defining
3. Capacity Estimation
4. Define Data model (DB Design)
5. High Level Design
6. Detailed Design of selected component
7. Identify & resolve bottlenecks


## Types of Requirements 

### Functional Requirements

Functional requirements desfine the specific behaviors or functions that a system must perform. They descibe what the system should do in response to various inputs and how it should behave in different situations

Example
- User Registration: Allow users to create new accounts by providing their names, email address and password
- User Profile : Enable users to update their profile information, including their profile picture, bio and contact info

### Non Functional Requirements
Non Functional requirements speciffy the quality attributes or constraints that the system must satisfy. They define how well the system performs certain functions rather than what function its performs

Example
- Performance: The system should be able to handle a minimum of 1000 concurrent users without experiencing significant slowdowns.
- Reliability: The system should have a uptime of at least 99.9% to ensure users can access it whenever they need.
- Security: The system should implement secure authentication mechanisms, such as HTTPS, to protect user data from unauthorized - access.
- Usability: The user interface should be intuitive and easy to navigate, with clear labeling and consistent design elements.
- Scalability: The system should be able to scale horizontally to accommodate an increase in users and data volume without significant changes to the architecture.
- Availability: The system should be available 24/7, with scheduled maintenance windows communicated to users in advance.

### Extended Requirements
Extended Requirements encompass a broader range of considerations that may not fit nearly into the categories of function and non-functional requirements

Examples
- Regulatory Compliance
- Legal Requirements
- Budget Constraints
- Environmental consideration

## Constraints
In system design, contrains define the **limitation and boundaries** within which a system must operate. unlike functional or non-functional requiremetns that describe what a system should do and how well it should perform, constraints impose restrictions on **technology, cost, time, compliance, and other factors.** 

### Gathering Constraints
- Identify key stakeholders
    Constraints often originate from mulitple source, making it essential to engage with relevant stakeholders
    - Business Leaders- Define budgetary and regulatory limitations
    - Product Mangers - Identify feature scope and time constraints
    - Developers & Architect - Evaluate technical constraints
    - Security & Compliance Teams - Ensure regulatory adherence
- Types of Constraints
    - Buisness constraints: These are limitations imposed by business needs, market conditions or corporate policies.
    - Technical Constraints: These include limitations on hardware, software or existing infrastructure.
    - Regulatory & Compliance Constraint: These arise due to laws and industry regulations such as **GDPR, HIPAA or PCI-DSS**.
    - Performance & Scalability Constraints: These defines operational boundaries such as latency, throughput, and resource limits.
    - Time Constraints: Project timelines impact the feasiblity of certain features or architecture
    - Resource Constraints: These relate to the availablilty of skilled personnel, copmuting resources, or infrastructure.

### Documenting Contraints
Constraints should be clearly defined and documented using
- Project requirement documents
- Risk assessment reports.
- Compliance checklist
- Feasibilty studies.

### Challenges in Managing Constraints
- Conflicting Constraints: Different constriants may contradict each other, requiring trade-ffs
- Understanding Future needs: Many constraints evolve overtime. Ignoring scalibilty can lead to expensive redesigns.
- Rigid or Overly Broad Constraints: Overly restrictive constraints may limit innovation, while vague constraints can lead to ambigutiy
- Compliance Complexity: Navigating multiple regulatory frameworks across different regions can be challenging

### Best Pratices for Handling Constraints
- Prioritze Constraints based on impact
- Define Constrainst clearly & Measurably
- Plan for Future Scalabilty
- Regularly Review & Reevalute Constraints
- Use prototyping & testing to validate constraints

## SLA & SLO

**System Level Objectives** are internal, measureable targets set by reliablity engineering teams to define the acceptable operational boundaries of a service, such as **99.9% availability** or **latency under 200ms**. These objectives are desinged to be **SMART**(Specific Measurable, Achievable, Relevant, Time-bound) and typically include an **error budget** to balance relaiablity with development velocity.

**System Level Agreement** are the external, legal contracts between a provider and a customer that specify the consequence, such as **financial penalities** or **service credits**, if the SLOs are not met.

SLAs define the **scope, metrics, and responsibilities** for paid services, ensuring that internal SLOs are set strictly higher thancustomer-facing SLAs to provide a safety buffer against breaches. 

