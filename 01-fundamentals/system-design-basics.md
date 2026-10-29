# System Design Basics

## 1. What is system design?

System design describes the major components of a system, their responsibilities, data ownership, communication paths, operational requirements and failure behavior.

A good design explains not only **what** components exist, but also **why** they exist and which alternatives were considered.

## 2. Begin with requirements

### Functional requirements
What must the product do? Examples:
- Users can register, sign in and manage their profile.
- Users can search a catalogue.
- Users can submit a question to an AI assistant.
- Administrators can manage products and access reports.

### Non-functional requirements
How well must it operate?
- Availability and recovery objectives
- Response-time targets
- Throughput and burst tolerance
- Security, privacy and compliance
- Data durability and consistency
- Maintainability and deployment independence
- Cost ceiling and team capabilities

## 3. Identify system boundaries

Use a context diagram to show:
- Users and external actors
- The system being designed
- External dependencies (payment provider, email service, LLM provider)
- Trust boundaries and data flows

Then create a container diagram for deployable units and a sequence diagram for critical flows.

## 4. Define service-level objectives

Example targets for a hypothetical web application:
- 99.9% monthly availability for core read APIs
- 95th percentile latency under 300 ms for a selected API
- Successful completion of 99% of accepted background jobs within a defined window

These are examples only. Choose targets with product and business stakeholders and define exactly how they are measured.

## 5. List constraints

Record:
- Expected team size and skills
- Existing technology and hosting constraints
- Budget
- Data residency and privacy needs
- Integration dependencies
- Launch deadline
- Recovery and support expectations

## 6. Make trade-offs explicit

Architecture often trades:
- Simplicity vs independent deployment
- Consistency vs availability during network partitions
- Latency vs cost
- Flexibility vs operational burden
- Fast launch vs future migration cost

There is rarely one universally best architecture. The best choice fits the current constraints and has a credible evolution path.

## 7. Deliverables for a design review

- Requirements and assumptions
- Workload model
- Context/container/sequence diagrams
- API and data contracts
- Security and threat model
- Failure-mode analysis
- Deployment and recovery plan
- Cost model
- ADRs for important choices
- Open questions, owners and validation tasks
