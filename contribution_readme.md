# Contribution 1: Persist Local Development Database Across Docker Restarts

**Contribution Number:** 1
**Student:** Vanesa Aguay Guerra
**Issue:** #2198
**Status:** Phase I - In Progress

---

## Why I Chose This Issue

I chose this issue because it is a concrete systems problem with a clear definition of success. I was looking for an issue where I could understand the problem in plain language, identify the affected components, and trace how a fix would impact the overall developer experience.

The issue also aligns well with my interests in systems engineering, infrastructure, and reliability. Through coursework in data structures and systems programming, research work involving distributed measurement systems, and projects involving deployment pipelines and APIs, I have become interested in understanding how technical systems behave across environments and where failures occur. This issue sits at the intersection of software infrastructure and developer tooling, which makes it both practical and a strong opportunity to learn more about Docker, PostgreSQL persistence, and application startup workflows.

Beyond solving the issue itself, I hope to gain experience contributing to a larger open source codebase, understanding how maintainers think about developer experience, and improving my ability to debug system-level problems.

---

## Understanding the Issue

### Problem Description

The local development database does not persist across Docker restarts. Every time developers restart the Docker environment, locally created database data is erased and replaced with a fresh database.

### Expected Behavior

The PostgreSQL database should persist data across Docker restarts.

If a developer creates or modifies data locally, that data should still exist after running Docker again. Developers should also have a simple way to intentionally reset the database when they want a clean environment.

### Current Behavior

Currently, running `docker compose up` wipes locally created database data because the PostgreSQL container does not use a persistent volume. In addition, the backend startup process automatically clears and reseeds the database every time it starts.

As a result, developers lose local data whenever the Docker environment is restarted, making testing and development workflows more difficult.

### Affected Components

Based on my initial review, the issue appears to involve:

- Docker configuration files, particularly `docker-compose.yml`
- PostgreSQL container configuration
- Backend startup scripts
- The `populate_db` process responsible for clearing and reseeding the database
- Development environment setup and database initialization logic 

---

## Reproduction Process

### Environment Setup

I reviewed the issue discussion and linked pull request to understand the current development workflow. The issue affects Activist's Docker-based local development environment and specifically the PostgreSQL database setup. Based on the maintainer discussion, the problem occurs because database state is not persisted across container restarts and the startup process reseeds the database on launch.

### Steps to Reproduce

1. Clone the Activist repository and complete the local Docker setup.
2. Start the development environment using `docker compose up`.
3. Create or modify data in the local PostgreSQL database.
4. Verify that the data exists in the application or database.
5. Stop the Docker containers.
6. Restart the development environment using `docker compose up`.
7. Reopen the application and inspect the database contents.
8. Observe that previously created local data has been removed and replaced with a fresh seeded database.

### Reproduction Evidence

Issue Link: https://github.com/activist-org/activist/issues/2198

Related Pull Request: https://github.com/activist-org/activist/pull/2199

Branch Link: https://github.com/[YOUR_USERNAME]/activist/tree/fix-local-db-persistence

My Findings:

The PostgreSQL container currently does not maintain local development data across Docker restarts. Additionally, the backend startup process runs database initialization logic that clears and reseeds data, resulting in loss of locally created records. This creates friction for contributors who need persistent test data during development.

---

## Implementation Plan

### Understand

The goal is to ensure local PostgreSQL data persists across Docker restarts while still giving developers a simple way to intentionally reset and reseed their database when needed.

### Match

The issue discussion and related pull request suggest two common infrastructure patterns:

* Using Docker volumes to persist database state.
* Separating initial database seeding from normal application startup.

These patterns are widely used in containerized development environments to improve reliability and developer experience.

### Plan

* Review the current `docker-compose.yml` configuration.
* Identify how the PostgreSQL container is currently storing data.
* Add a persistent Docker volume for database storage.
* Review the backend startup process and locate where `populate_db` is executed.
* Modify initialization behavior so the database is not automatically cleared on every startup.
* Preserve a separate workflow for developers who want a fresh seeded database.
* Test persistence by creating local data, restarting Docker, and confirming the data remains available.
* Verify that the manual reset workflow continues to function correctly.

### Implement

Working Branch:

https://github.com/[YOUR_USERNAME]/activist/tree/fix-local-db-persistence

### Review

Before submitting a solution I will verify that:

* The change follows Activist contribution guidelines.
* Database persistence works across multiple Docker restarts.
* Existing development workflows are not broken.
* Documentation accurately reflects any workflow changes.

### Evaluate

Success will be measured by:
* Local data remaining available after Docker restarts.
* No automatic database wipe during normal startup.
* Ability to intentionally reset and reseed the database when desired.
* Successful execution of existing project tests and development workflows.



**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
