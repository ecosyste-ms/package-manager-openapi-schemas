# Contributing to Package Manager OpenAPI Schemas

Thank you for your interest in contributing! This guide will help you add new schemas or improve existing ones.

## Quick Start

1. Fork this repository
2. Create a new branch: `git checkout -b add-ecosystem-name`
3. Add or update a schema in `openapi/`
4. Validate: `swagger-cli validate openapi/your_ecosystem.yaml`
5. Update the README table
6. Submit a pull request

## Adding a New Ecosystem

### 1. Research the API

Find the official API documentation for the package manager:
- Look for API endpoints
- Note authentication requirements
- Check if there's existing OpenAPI documentation

### 2. Create the Schema File

Use an existing schema as a template:

```bash
cp openapi/npm.yaml openapi/your_ecosystem.yaml
```

### 3. Document the API

Update the schema with:

**Info Section:**
```yaml
openapi: 3.0.3
info:
  title: Your Registry API
  description: |
    Description of what the API provides...
  version: 1.0.0
  contact:
    name: Support Team
    url: https://your-registry.org/help
  license:
    name: MIT

servers:
  - url: https://api.your-registry.org
```

**Endpoints:**
```yaml
paths:
  /packages/{name}:
    get:
      summary: Get package metadata
      operationId: getPackage
      tags:
        - Packages
      parameters:
        - name: name
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Package'
        '404':
          description: Not found
```

**Schemas:**
```yaml
components:
  schemas:
    Package:
      type: object
      required:
        - name
        - version
      properties:
        name:
          type: string
          example: express
        version:
          type: string
          example: "4.18.2"
```

### 4. Add Real Examples

Use actual API responses as examples:

```bash
# Test the actual API
curl https://registry.npmjs.org/express | jq . > example.json

# Use that structure in your schema
```

### 5. Validate Your Schema

```bash
# Install validator
npm install -g @apidevtools/swagger-cli

# Validate
swagger-cli validate openapi/your_ecosystem.yaml
```

The schema must pass validation before submitting.

### 6. Update Documentation

Add your ecosystem to README.md:

```markdown
| **Your Ecosystem** | registry.example.com | [`your_ecosystem.yaml`](openapi/your_ecosystem.yaml) | ✅ Complete | XXK |
```

Add ecosystem-specific notes if needed:

```markdown
### Your Ecosystem (Language)
- Package naming format
- Authentication requirements
- Special URL encoding rules
- Version format conventions
```

### 7. Submit Pull Request

Title: `Add [Ecosystem Name] OpenAPI schema`

Description:
```
Adds OpenAPI 3.0 specification for [Ecosystem Name]

Endpoints documented:
- GET /packages/{name} - Package metadata
- GET /packages/{name}/versions - Version list
- etc.

Based on: https://link-to-official-api-docs
```

## Improving Existing Schemas

Found an issue or missing endpoint?

1. Fork and create a branch
2. Make your changes to the schema file
3. Validate with `swagger-cli validate`
4. Submit a PR with clear description of the change

## Schema Quality Guidelines

### Required

- ✅ Valid OpenAPI 3.0.3 format
- ✅ All main endpoints documented
- ✅ Response schemas with types
- ✅ Operation IDs for all endpoints
- ✅ At least one example per endpoint
- ✅ Error responses (404, etc.)

### Recommended

- Parameter descriptions
- Authentication notes
- Rate limiting information
- Links to official documentation
- Multiple examples showing different use cases

## Code Style

### YAML Format

- Use 2 spaces for indentation
- Multi-line descriptions use `|`
- Keep lines under 100 characters
- Sort schemas alphabetically

### Naming

- **operationId:** camelCase (`getPackage`, `listVersions`)
- **Schema names:** PascalCase (`Package`, `Version`)
- **Tags:** lowercase (`packages`, `versions`)

## Testing

GitHub Actions automatically validates all schemas when you submit a PR.

The workflow uses Swagger CLI to validate. If it passes, your PR is ready for review!

## Common Issues

**Schema validation fails:**
- Check all `$ref` paths exist
- Ensure required fields are marked
- Verify examples match schema types

**Not sure about a field:**
- Check existing schemas for similar patterns
- Test against the actual API
- Ask in the PR comments

## Questions?

- Open an issue for questions
- Check existing schemas for examples
- Refer to [OpenAPI 3.0 Spec](https://spec.openapis.org/oas/v3.0.3)

## License

Contributions are accepted under the MIT License.
