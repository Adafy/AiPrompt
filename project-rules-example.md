# CustomerXYZ system Development Rules - Project Overrides & Additions
**Tags:** development-rules, coding-standards, process-guidelines, git-workflow, CustomerXYZ-specific

**INHERITANCE:** This file inherits all standards from [Adafy Global Rules](https://github.com/Adafy/AiPrompt/blob/main/rules.md).

**Project-Specific Overrides & Additions:** Only CustomerXYZ-specific deviations and additions are documented below.

## System Context (Global Template Implementation)

**CustomerXYZ** is a Finnish fund granting funding. CustomerXYZ system manages applications and approved projects.

- **Target Environment:** .NET 8 Web API with Entity Framework Core
- **Database:** Cosmos DB. SQL Server is used for localization and identity, but is not directly referenced
- **Architecture:** Clean Architecture with API controllers, services, and repositories
- **Deployment:** Azure App Service
- **System Language:** Finnish (with translation functionality)
- **Application Types:** Private grants (stipendi), organizational grants (määräraha)

## API Standards (Project Addition)

**Additional to Global API Standards:**
- **Inject API clients** instead of using classes directly from other assemblies
- **Exception:** This does not apply to Common assembly, or other assemblies that do not implement a Web API

## Development Process (Global Override)

### Testing (Override - Relaxed Standards)
- **Minimal testing approach** due to system's limited testability constraints
- **Create unit tests** only when simple and easy to review
- **Rationale:** Legacy system architecture and tight coupling make comprehensive testing impractical

## Documentation & Logging (Project Addition)

### CustomerXYZ-Specific Implementation Log Tags
**Additional to Global Tags:** Include these CustomerXYZ-specific tags when relevant:
- `CustomerXYZ` - CustomerXYZ system specific changes
- `stipendi` - Private grant functionality
- `määräraha` - Organizational grant functionality
- `finnish-localization` - Language/localization related changes
