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

[Notes on setting up your local development environment - challenges you faced, how you solved them]

### Steps to Reproduce

1. [Step 1]
2. [Step 2]
3. [Observed result]

### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]

**Match:** [What similar patterns/solutions exist in the codebase?]

**Plan:** [Step-by-step implementation plan]
1. [Modify file X to do Y]
2. [Add function Z]
3. [Update tests]

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
