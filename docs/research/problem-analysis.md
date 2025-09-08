## The Core Problem: Signal vs. Noise

Popularity metrics like download counts are poor proxies for quality. A role might be downloaded frequently because it's old and established, not because it's well-maintained, secure, or follows current best practices. The goal is to automate the manual, time-consuming process of deep-diving into code repositories to assess their true quality based on a set of objective criteria.

## Architectural Blueprint for AI Assistant System

The system can be broken down into four key components that work in sequence: the Specification Interface, the Discovery Agent, the Analysis Engine, and the Synthesis Layer.

### 1. Specification Interface (Defining Requirements)

This interface captures user needs through structured requirements rather than simple search queries. It supports multiple input formats including web forms, YAML configuration files, or AI prompts.

#### Key Criteria to Define:

**Core Functionality**

- _"I need a role to manage a PostgreSQL server on Ubuntu 22.04."_

**Target Platform**

- _"Must be compatible with AWS"_
- _"For Kubernetes deployment"_

**Quality Metrics & Weights**
Users can prioritize what "quality" means to them:

- **Maintenance**: Prioritize recently updated collections
- **Testing**: Must have CI pipeline and Molecule tests
- **Documentation**: Clear READMEs and module documentation
- **Community**: Multiple active contributors preferred

### 2. Discovery Agent (Finding Candidates)

This component acts as a researcher, translating user specifications into strategic API calls to identify potential candidates.

#### Tooling Integration:

- **GitHub API**: Repository search, code search, and metadata queries
- **Ansible Galaxy API**: Collection discovery and cross-referencing

#### Search Strategy:

**Primary Search Methods:**

- GitHub API code search with advanced queries:

  ```bash
  language:yaml "ansible-galaxy" "PostgreSQL" in:readme
  topic:ansible topic:postgresql
  ```

- Ansible Galaxy API for collection discovery
- Cross-referencing Galaxy collections with GitHub repositories

#### Smart API Usage:

**Round Robin Queries:**
The agent intelligently cycles through search queries, starting broad and narrowing down:

- Broad: `"PostgreSQL"` → More specific: `"postgresql_user" in:file path:roles/`

**Smart Pagination:**

- Processes results in batches (e.g., 20 repositories per page)
- Performs preliminary filtering before fetching additional pages
- Manages rate limits and maintains efficiency

### 3. Analysis Engine (Quality Scoring)

Once candidates are identified, the Analysis Engine performs deep quality assessments through automated API calls to repository contents and metadata.

#### Automated Scoring Rubric:

##### ✅ Maintenance & Activity

**API Call:** Repository details and commit history
**Metrics:**

- Date of last commit
- Commit frequency
- Number of active contributors

##### 🧪 Testing & CI/CD

**API Call:** Repository file tree inspection
**Metrics:**

- Presence of `.github/workflows/` directory
- Molecule testing directory (`molecule/`)
- Testing configuration files (`tox.ini`, `pytest.ini`)

##### 📖 Documentation Quality

**API Call:** README.md and galaxy.yml content retrieval
**Metrics:**

- README length and structure
- Usage examples presence
- Declared dependencies clarity
- Author information completeness

##### 🤝 Community Health

**API Call:** Issues and pull requests data
**Metrics:**

- Open vs. closed issues ratio
- Average issue resolution time
- Fork and star counts (secondary metric)

**Scoring Process:** Each candidate receives a weighted score based on user-defined priorities from the Specification Interface.

### 4. Synthesis Layer (Human-Readable Reports)

This final component transforms structured scoring data into comprehensive, human-readable reports using Large Language Models (LLMs) like Gemini.

#### Input Processing:

**Data Structure:** List of candidates with associated scores

```json
[
  {
    "repo": "user/repo1",
    "maintenance_score": 9,
    "testing_score": 7,
    "documentation_score": 8
  }
]
```

#### Synthesis Process:

The LLM receives a structured prompt to generate comprehensive reports:

**Example Prompt:**

> "You are an expert Ansible developer. Based on the following scored data, generate a report for a user looking for a high-quality PostgreSQL role. Rank the top 3 candidates. For each one, provide a summary and explicitly state the reasoning for its rank, referencing specific scores in testing and recent maintenance."

#### Output Generation:

- **Clear Rankings:** Top candidates presented in order
- **Detailed Justifications:** Specific reasoning tied to quality metrics
- **Actionable Insights:** Recommendations based on user priorities

---

**System Architecture Benefits:**
This architecture creates a powerful feedback loop where the AI system doesn't just find results—it finds, evaluates, scores, and explains them, effectively solving the core problem of separating quality signal from popularity noise.
