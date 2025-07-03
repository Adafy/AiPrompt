# Adafy AI assisted software development rules

**Tags:** development-rules, coding-standards, process-guidelines, git-workflow

This is an instruction document for an LLM used to help Adafy personnel in their software development tasks. This document acts as a foundation, and should always be included in AI assisted development. There can and should be project-specific instructions that will complement and, when necessary, override these instructions.

This is a document that should be updated when the need arises. It should be kept general, so that projects can use it without a need to override large parts of it.

**FOR DEVELOPERS**: Note that this document is currently located in a public repository. **DO NOT add any kind of customer specific information in this document, keep that in a project-level instructions.**

## System Context

**Note:** This section should be filled in at the project level with specific information about:
- Target development environment and technology stack
- Database and API framework specifics
- Architecture patterns and deployment context
- Any project-specific development tool requirements

## Git & Version Control

- **Keep commits small and focused** - user reviews all changes
- **Keep branch changes small** - enables manageable pull requests
- **Branch naming:** `JIRA-123-Description` (ticket number + brief description)
- **Main branch:** Notify the user and wait for instructions before working on the main branch
- **Workflow:** Feature branch → smaller implementation branches → user handles final PR to main

## Code Quality

### Controllers & Services
- **Keep controllers small** - move logic to services when controller action methods become complex
- **Use service classes** for business logic beyond simple operations

### Data Access
- **Prefer LINQ** over SQL strings in repositories
  - *Rationale:* LINQ provides type safety, better maintainability, and compile-time error checking
  - *Example:* `users.Where(u => u.IsActive)` instead of `"SELECT * FROM Users WHERE IsActive = 1"`
- **Never use `GetAll()`** unless specifically instructed
  - *Rationale:* Avoid loading all entities to prevent memory issues and performance degradation
  - *Risk:* Can cause OutOfMemoryException with large datasets and slow application response
- **Exception:** Parameter-like entities (application types, lookup tables) may use `GetAll()`

### API Standards
When project backend is a Web API, follow these rules:
- **Never update** `swagger.json` or `WebApiClient.cs` (NSwag-generated)
- **Use [`HttpStatusCode`](System.Net.HttpStatusCode) constants** in [`ProducesResponseTypeAttribute`](Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute)

## Development Process

### Scope Management
- **Never expand beyond scope** without permission
- **Report insufficient solutions** to user, don't implement extras
- **Wait for user review** before proceeding to the next step

### Continuous Improvement
- **Propose instruction improvements** when you notice patterns, issues, or missing guidance that should be documented in these rules
- **Be proactive** about suggesting additions to development standards, coding practices, or process improvements based on encountered scenarios

## Documentation & Logging

### Implementation Logs
- **File naming:** Start filename with Jira ticket number when available 
  - `JIRA-123-task-description.md` for single tasks
  - `JIRA-123-story-description.md` for final, story-level log file
  - Try to find the Jira ticket number from the current branch name in Terminal
  - **If no Jira ticket:** Use 5-digit incremented number (e.g., `00001-task-description.md`, 
- **Always create** `.md` file in [`/implementations`](implementations/) folder after each task
- **Add tags/keywords** at file beginning for quick relevance identification
- **Skip logging** only for minimal changes
  - *Definition:* Changes affecting fewer than 10 lines of code or simple UI adjustments (text, colors, spacing) that don't alter business logic
- **Read previous logs** before starting new tasks - use filenames and tags to select relevant documents
- **Keep task log updated** when implementation proceeds, if one exists
- **Consolidate implementation logs** when finalizing larger developments (stories or similar)
  - **Consolidated file placement:** Place in [`/implementations`](implementations/) folder
  - **Consolidated file naming:** Start with Jira ticket number (e.g., `JIRA-456-story-consolidation.md`)
  - **Content requirements:** 
    - Include brief description of overall story/development and consolidate all related implementation logs from that development cycle
    - If Jira ticket is available, add a link to the ticket after the heading of the document. The URL of the ticket is in format https://adafy.atlassian.net/browse/PRJ-123, where PRJ-123 is the Jira ticket number
    - Follow naming convention defined for task specific log files
  - **Remove task log files after consolidation**

### Log Structure
```markdown
**Tags:** keyword1, keyword2, keyword3

# Task Description
Brief description of what was implemented

## Changes Made
- Specific change 1
- Specific change 2
```

## Error Handling & Security

### Error Handling
- **Use specific exceptions** instead of generic `Exception` class
- **Log errors with context** - include relevant data that helps debugging
- **Fail fast principle** - validate inputs early and throw meaningful exceptions
- **Don't swallow exceptions** - always log or re-throw with additional context

### Security Considerations
- **Validate all inputs** - never trust user input, validate on server side
- **Use parameterized queries** - prevent SQL injection attacks
- **Implement proper authentication** - verify user identity before processing requests
- **Log security events** - track authentication failures and suspicious activities

## Performance Guidelines

### General Performance
- **Use async/await** for I/O operations to prevent thread blocking
- **Implement pagination** for large data sets instead of loading everything
- **Cache frequently accessed data** - use appropriate caching strategies
- **Optimize database queries** - use projection when you don't need full entities

## Critical Rules Summary

1. **English in code** - always enforce for consistency and maintainability
2. **Small commits** - user reviews everything to ensure quality
3. **No scope expansion** - get permission first to control project scope
4. **Log all significant work** - use tags for discoverability and knowledge transfer
5. **Read previous logs** - understand context before starting to avoid duplication
6. **Never use `GetAll()`** - avoid loading all entities to prevent performance issues
7. **Validate inputs** - always validate user input to prevent security vulnerabilities
8. **Use async patterns** - implement async/await for I/O operations to improve scalability