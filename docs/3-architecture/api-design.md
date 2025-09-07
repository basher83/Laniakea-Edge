# API Design Specification

## API Overview

The Laniakea-Edge API follows RESTful principles and implements the Model Context Protocol for AI agent integration. All endpoints return JSON and use standard HTTP status codes.

## Base URL

```
Production: https://api.laniakea-edge.io/v1
Staging:    https://staging-api.laniakea-edge.io/v1
Local:      http://localhost:8000/v1
```

## Authentication

### API Key Authentication
```http
GET /analyze HTTP/1.1
Host: api.laniakea-edge.io
X-API-Key: lek_live_1234567890abcdef
```

### OAuth2 Bearer Token
```http
GET /analyze HTTP/1.1
Host: api.laniakea-edge.io
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

## Core Endpoints

### Repository Analysis

#### Analyze Single Repository
```http
POST /v1/analyze
Content-Type: application/json

{
  "repository_url": "https://github.com/ansible/ansible",
  "technology": "ansible",
  "options": {
    "include_recommendations": true,
    "depth": "comprehensive"
  }
}
```

**Response:**
```json
{
  "repository": {
    "url": "https://github.com/ansible/ansible",
    "name": "ansible",
    "technology": "ansible"
  },
  "overall_score": 9.5,
  "metrics": {
    "testing": {
      "score": 10.0,
      "details": {
        "framework": "pytest",
        "coverage": 89.5,
        "ci_configured": true
      }
    },
    "documentation": {
      "score": 9.5,
      "details": {
        "readme_quality": "excellent",
        "api_docs": true,
        "examples": true
      }
    },
    "maintenance": {
      "score": 9.0,
      "details": {
        "last_commit_days": 1,
        "open_issues": 245,
        "response_time_hours": 12
      }
    },
    "community": {
      "score": 9.5,
      "details": {
        "contributors": 500,
        "stars": 58000,
        "forks": 23000
      }
    }
  },
  "recommendations": [
    "Consider adding more integration tests",
    "Improve issue triage process"
  ],
  "analysis_timestamp": "2024-01-15T10:30:00Z",
  "analysis_duration_ms": 15230
}
```

#### Batch Analysis
```http
POST /v1/analyze/batch
Content-Type: application/json

{
  "repositories": [
    "https://github.com/ansible/ansible",
    "https://github.com/geerlingguy/ansible-role-docker"
  ],
  "technology": "ansible",
  "callback_url": "https://webhook.site/unique-id"
}
```

**Response:**
```json
{
  "job_id": "job_550e8400-e29b-41d4-a716-446655440000",
  "status": "queued",
  "estimated_completion": "2024-01-15T10:35:00Z",
  "repositories_count": 2,
  "callback_url": "https://webhook.site/unique-id"
}
```

### Repository Discovery

#### Search Repositories
```http
GET /v1/discover?query=mysql&technology=ansible&limit=10
```

**Response:**
```json
{
  "results": [
    {
      "repository": {
        "url": "https://github.com/geerlingguy/ansible-role-mysql",
        "name": "ansible-role-mysql",
        "owner": "geerlingguy"
      },
      "relevance_score": 0.95,
      "quality_score": 8.5,
      "description": "Ansible Role - MySQL",
      "last_updated": "2024-01-10T00:00:00Z"
    }
  ],
  "total_count": 156,
  "next_page": "/v1/discover?query=mysql&technology=ansible&limit=10&page=2"
}
```

#### Advanced Search
```http
POST /v1/discover/advanced
Content-Type: application/json

{
  "query": {
    "keywords": ["mysql", "mariadb"],
    "technology": "ansible",
    "filters": {
      "min_stars": 50,
      "max_days_since_update": 180,
      "license": ["MIT", "Apache-2.0"],
      "has_tests": true
    }
  },
  "sort_by": "quality_score",
  "limit": 20
}
```

### Quality Metrics

#### Get Scoring Criteria
```http
GET /v1/metrics/criteria?technology=ansible
```

**Response:**
```json
{
  "technology": "ansible",
  "criteria": {
    "testing": {
      "weight": 0.3,
      "factors": [
        {"name": "molecule_tests", "weight": 0.4},
        {"name": "ansible_lint", "weight": 0.2},
        {"name": "ci_pipeline", "weight": 0.2},
        {"name": "test_coverage", "weight": 0.2}
      ]
    },
    "documentation": {
      "weight": 0.25,
      "factors": [
        {"name": "readme_completeness", "weight": 0.3},
        {"name": "usage_examples", "weight": 0.3},
        {"name": "api_documentation", "weight": 0.2},
        {"name": "changelog", "weight": 0.2}
      ]
    }
  }
}
```

## Model Context Protocol (MCP) Integration

### Tool Discovery Endpoint
```http
GET /v1/mcp/tools
```

**Response:**
```json
{
  "tools": [
    {
      "name": "analyze_repository",
      "description": "Analyze an Infrastructure-as-Code repository for quality",
      "parameters": {
        "type": "object",
        "properties": {
          "repository_url": {
            "type": "string",
            "description": "GitHub repository URL"
          },
          "technology": {
            "type": "string",
            "enum": ["ansible", "terraform", "kubernetes"],
            "description": "IaC technology type"
          }
        },
        "required": ["repository_url"]
      }
    },
    {
      "name": "discover_repositories",
      "description": "Search for IaC repositories matching criteria",
      "parameters": {
        "type": "object",
        "properties": {
          "query": {
            "type": "string",
            "description": "Search query"
          },
          "technology": {
            "type": "string",
            "enum": ["ansible", "terraform", "kubernetes"]
          },
          "limit": {
            "type": "integer",
            "default": 10
          }
        },
        "required": ["query"]
      }
    }
  ]
}
```

### Tool Execution Endpoint
```http
POST /v1/mcp/execute
Content-Type: application/json

{
  "tool": "analyze_repository",
  "parameters": {
    "repository_url": "https://github.com/ansible/ansible",
    "technology": "ansible"
  },
  "context": {
    "conversation_id": "conv_123",
    "user_id": "user_456"
  }
}
```

## Async Operations

### Job Status
```http
GET /v1/jobs/job_550e8400-e29b-41d4-a716-446655440000
```

**Response:**
```json
{
  "job_id": "job_550e8400-e29b-41d4-a716-446655440000",
  "status": "in_progress",
  "progress": {
    "completed": 1,
    "total": 2,
    "current": "analyzing geerlingguy/ansible-role-docker"
  },
  "created_at": "2024-01-15T10:30:00Z",
  "updated_at": "2024-01-15T10:31:30Z"
}
```

### Job Results
```http
GET /v1/jobs/job_550e8400-e29b-41d4-a716-446655440000/results
```

## Webhooks

### Webhook Registration
```http
POST /v1/webhooks
Content-Type: application/json

{
  "url": "https://your-app.com/webhook",
  "events": ["analysis.completed", "job.failed"],
  "secret": "webhook_secret_123"
}
```

### Webhook Payload
```json
{
  "event": "analysis.completed",
  "timestamp": "2024-01-15T10:35:00Z",
  "data": {
    "job_id": "job_550e8400-e29b-41d4-a716-446655440000",
    "repository": "https://github.com/ansible/ansible",
    "overall_score": 9.5
  },
  "signature": "sha256=..."
}
```

## Error Responses

### Standard Error Format
```json
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "API rate limit exceeded. Please retry after 3600 seconds.",
    "details": {
      "limit": 1000,
      "remaining": 0,
      "reset_at": "2024-01-15T11:00:00Z"
    }
  },
  "request_id": "req_abc123"
}
```

### Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| INVALID_REQUEST | 400 | Malformed request |
| AUTHENTICATION_REQUIRED | 401 | Missing authentication |
| PERMISSION_DENIED | 403 | Insufficient permissions |
| NOT_FOUND | 404 | Resource not found |
| RATE_LIMIT_EXCEEDED | 429 | Rate limit hit |
| INTERNAL_ERROR | 500 | Server error |
| SERVICE_UNAVAILABLE | 503 | Service temporarily down |

## Rate Limiting

### Rate Limit Headers
```http
HTTP/1.1 200 OK
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1642248000
X-RateLimit-Reset-After: 3600
```

### Rate Limit Tiers

| Tier | Requests/Hour | Burst | Concurrent |
|------|--------------|-------|------------|
| Free | 100 | 10 | 1 |
| Basic | 1000 | 50 | 5 |
| Pro | 10000 | 200 | 20 |
| Enterprise | Unlimited | 1000 | 100 |

## Pagination

### Cursor-Based Pagination
```http
GET /v1/discover?query=mysql&cursor=eyJvZmZzZXQiOjEwfQ==&limit=10
```

**Response:**
```json
{
  "results": [...],
  "pagination": {
    "cursor": "eyJvZmZzZXQiOjIwfQ==",
    "has_more": true,
    "total_count": 156
  }
}
```

## Versioning

### Version Header
```http
GET /analyze HTTP/1.1
Host: api.laniakea-edge.io
Accept-Version: v1
```

### Version in URL
```
https://api.laniakea-edge.io/v1/analyze
https://api.laniakea-edge.io/v2/analyze
```

### Deprecation Notice
```http
HTTP/1.1 200 OK
Sunset: Sat, 1 Jul 2024 00:00:00 GMT
Deprecation: true
Link: <https://api.laniakea-edge.io/v2/analyze>; rel="successor-version"
```

## OpenAPI Specification

### Swagger UI
```
https://api.laniakea-edge.io/docs
```

### OpenAPI JSON
```
https://api.laniakea-edge.io/openapi.json
```

### Example OpenAPI Definition
```yaml
openapi: 3.0.0
info:
  title: Laniakea-Edge API
  version: 1.0.0
  description: AI-powered quality analysis for IaC repositories
  
servers:
  - url: https://api.laniakea-edge.io/v1
    description: Production
    
paths:
  /analyze:
    post:
      summary: Analyze a repository
      operationId: analyzeRepository
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/AnalyzeRequest'
      responses:
        '200':
          description: Analysis complete
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AnalysisResult'
```

## Client SDKs

### Python Example
```python
from laniakea_edge import Client

client = Client(api_key="lek_live_xxx")

# Analyze repository
result = client.analyze_repository(
    repository_url="https://github.com/ansible/ansible",
    technology="ansible"
)

print(f"Quality Score: {result.overall_score}")
```

### JavaScript Example
```javascript
const LaniakeaEdge = require('laniakea-edge');

const client = new LaniakeaEdge.Client({
  apiKey: 'lek_live_xxx'
});

// Analyze repository
const result = await client.analyzeRepository({
  repositoryUrl: 'https://github.com/ansible/ansible',
  technology: 'ansible'
});

console.log(`Quality Score: ${result.overallScore}`);
```

## Health & Status

### Health Check
```http
GET /v1/health
```

**Response:**
```json
{
  "status": "healthy",
  "version": "1.0.0",
  "uptime_seconds": 86400,
  "services": {
    "api_gateway": "healthy",
    "orchestrator": "healthy",
    "discovery": "healthy",
    "analyzer_ansible": "healthy",
    "cache": "healthy"
  }
}
```

### API Status Page
```
https://status.laniakea-edge.io
```

---

*This API design provides a comprehensive interface for AI agents and developers to integrate with Laniakea-Edge.*