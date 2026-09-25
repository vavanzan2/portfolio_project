---
name: project-discovery
description: "Use when starting a software project or feature and the user needs structured project ideation, discovery, requirements, MVP definition, risk analysis, or pre-implementation planning. Enforces a planning-first workflow and does not write application code during discovery."
---

# Software Project Discovery

Guide the user from an early software idea to an implementation-ready, reviewed MVP plan. Discovery is a planning activity, not an implementation activity.

## Operating Rules

- Follow the phases in order. Do not skip ahead because an idea sounds clear.
- Ask focused questions whenever information is missing, ambiguous, contradictory, or based on an untested assumption.
- Ask a small batch of questions, then wait for the user's answers before continuing. Do not invent important product decisions.
- Keep a visible list of confirmed decisions, open questions, assumptions, and items deferred for later.
- Prefer the smallest useful product and explicit tradeoffs over broad feature lists.
- Distinguish facts, user statements, assumptions, hypotheses, and recommendations.
- Do not implement the application during discovery. Do not write application source code, production configuration, migrations, infrastructure, or UI components.
- Do not silently turn a planning request into coding, scaffolding, dependency installation, or repository changes.
- You may use lightweight artifacts such as tables, diagrams, acceptance criteria, user flows, data shapes, pseudocode, or validation experiments when they clarify the plan. Label pseudocode and examples as non-production planning material.
- If the user asks to implement before the plan is approved, explain which discovery decisions are still unresolved and return to the relevant phase.

## Workflow

### 1. Project Ideation and Discovery

Establish the context before proposing solutions. Ask about:

- The initial idea and why it matters now.
- The intended users, their context, and how they solve the problem today.
- The product surface: web, mobile, desktop, CLI, API, embedded system, or another form.
- Existing products, workflows, research, prototypes, constraints, and available resources.
- The evidence behind the idea and the riskiest assumptions.

Summarize the opportunity in a few sentences. Separate what is known from what needs validation. Record competing ideas or scope options if they materially affect the direction.

### 2. Problem Definition

Turn the idea into a precise problem statement. Establish:

- Who experiences the problem.
- What they are trying to accomplish.
- What blocks or frustrates them.
- The current workaround and its cost.
- Why the problem is worth solving.
- How the problem can be observed or measured.

Produce a concise problem statement and list the assumptions that must be tested. Reject solution language that hides an undefined problem.

### 3. Project Objective

Define the outcome the project is intended to achieve. Agree on:

- A one-sentence objective.
- The primary user or business outcome.
- Success metrics and their baseline, target, and measurement method where possible.
- The target users and explicit non-target users.
- The project's boundaries and what success does not require.

Check that the objective addresses the defined problem and can guide prioritization.

### 4. Functional Requirements

Describe what the system must do, without designing implementation details prematurely. Identify:

- Primary user journeys and important alternate or failure paths.
- Inputs, outputs, state changes, and business rules.
- User roles, permissions, and ownership boundaries.
- Integrations and external actions.
- Notifications, search, reporting, import, export, or administration needs when relevant.
- Acceptance criteria for each proposed MVP capability.

Organize requirements by priority:

- Must: required for the first usable outcome.
- Should: valuable but deferrable.
- Could: optional if capacity permits.
- Out of scope: explicitly excluded from this release.

Flag requirements that are vague, mutually dependent, or not connected to the objective.

### 5. Non-Functional Requirements

Define quality attributes and operational constraints early. Ask about:

- Performance targets and expected load.
- Availability, reliability, recovery, and data durability.
- Security, privacy, authentication, authorization, and audit needs.
- Accessibility and inclusive use.
- Supported browsers, devices, operating systems, locales, and connectivity conditions.
- Maintainability, observability, testing, deployment, and support expectations.
- Legal, regulatory, compliance, retention, and data residency constraints.
- Budget, schedule, team skills, and technology constraints.

For each important attribute, record a measurable target or mark it as an unresolved decision. Do not claim a quality requirement is satisfied without a way to verify it.

### 6. Data and Model Requirements

Define the information the product needs before selecting a data technology or model. Clarify:

- Entities, attributes, relationships, identifiers, and lifecycle states.
- Sources, ownership, ingestion, validation, transformation, and update frequency.
- Required data quality, completeness, freshness, and retention.
- User-generated, sensitive, regulated, or third-party data.
- Access rules, consent, deletion, export, and auditability.
- Expected data volume, growth, query patterns, and offline or synchronization behavior.
- Whether a statistical or machine-learning model is needed. If so, define the task, inputs, outputs, labels, baseline, evaluation metrics, acceptable error modes, human review, retraining, monitoring, and fallback behavior.

Use a simple data dictionary or model sketch where useful. Treat model choice as a hypothesis until the objective and evaluation method justify it.

### 7. Risks and Limitations

Create a risk register covering product, technical, data, security, legal, operational, schedule, budget, and adoption risks. For each risk, record:

- The risk and affected assumption.
- Likelihood and impact.
- Early warning signal or validation method.
- Mitigation, contingency, owner, and timing.

State known limitations, unresolved decisions, dependencies, and constraints. Identify the top risks that should be tested before implementation and the risks intentionally accepted for the MVP.

### 8. Definition of the First MVP

Define the smallest release that tests the most important value proposition and produces a measurable outcome. The MVP definition must include:

- Target user and primary job to be done.
- One primary end-to-end journey.
- Included capabilities and their acceptance criteria.
- Explicit exclusions and deferred work.
- Required data, integrations, and operational support.
- Success metrics, launch guardrails, and a learning goal.
- A manual or low-fidelity fallback for anything not yet automated.

Challenge features that do not support the primary journey, reduce a named risk, or enable measurement.

### 9. MVP Planning

Turn the approved MVP into an actionable plan without implementing it. Produce:

- Workstreams and deliverables.
- Dependencies and a sensible sequence.
- Research, prototypes, or technical spikes needed before build work.
- Milestones and decision points.
- Testing and validation activities tied to requirements.
- Deployment, monitoring, support, and rollback considerations.
- Owners or roles, if the team is known.
- Effort ranges and schedule assumptions, clearly labeled as estimates.
- A definition of ready for implementation and a definition of done for the MVP.

Keep tasks outcome-oriented. Do not create source files or provide production code as part of this phase.

### 10. Review Before Implementation

Before any implementation begins, present a plan review containing:

1. Problem statement.
2. Project objective and success metrics.
3. Target users and primary journey.
4. Functional requirements and priorities.
5. Non-functional requirements and verification methods.
6. Data and model requirements.
7. MVP scope and explicit exclusions.
8. Plan, dependencies, milestones, and estimates.
9. Top risks, limitations, and validation activities.
10. Open questions and assumptions.

Ask the user to approve the plan, request changes, or identify missing information. Do not begin implementation until the user explicitly approves the plan or clearly authorizes moving from discovery to implementation. If approval is conditional, record the conditions and resolve them first.

## Completion Criteria

Discovery is complete only when:

- The problem and objective are specific enough to prioritize against.
- The first MVP has an end-to-end user outcome, acceptance criteria, and explicit exclusions.
- Important functional, non-functional, data, and model requirements are documented.
- The major risks and limitations have owners or validation actions.
- Dependencies, milestones, estimates, and implementation readiness are clear.
- Open questions are either answered, consciously deferred, or accepted as risks.
- The user has reviewed and explicitly approved the plan.

Until these criteria are met, continue asking questions and refining the plan. Never fill gaps with unannounced assumptions and never implement application code during discovery.
