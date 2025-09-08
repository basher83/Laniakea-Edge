# Quality Assessment Framework

## Overview

The quality assessment framework provides a comprehensive, objective evaluation of Infrastructure-as-Code repositories. It uses multi-dimensional scoring with weighted metrics tailored to each IaC technology.

## Quality Dimensions

### 1. Testing Quality (30% weight)

**Purpose**: Evaluate the presence and comprehensiveness of testing practices

#### Ansible Metrics
- **Molecule Tests** (40%): Presence and coverage of Molecule test scenarios
- **Ansible Lint** (20%): Configuration and rule compliance
- **CI/CD Pipeline** (20%): Automated testing on commits/PRs
- **Test Coverage** (20%): Percentage of code tested

#### Scoring Algorithm
```python
def calculate_testing_score(repo_data):
    scores = {
        'molecule': detect_molecule_score(repo_data),  # 0-10
        'lint': detect_ansible_lint_score(repo_data),   # 0-10
        'ci': detect_ci_pipeline_score(repo_data),      # 0-10
        'coverage': calculate_coverage_score(repo_data)  # 0-10
    }
    
    weights = {
        'molecule': 0.4,
        'lint': 0.2,
        'ci': 0.2,
        'coverage': 0.2
    }
    
    return sum(scores[k] * weights[k] for k in scores)
```

### 2. Documentation Quality (25% weight)

**Purpose**: Assess the completeness and clarity of documentation

#### Documentation Metrics
- **README Completeness** (30%): Presence of key sections
- **Usage Examples** (30%): Code examples and tutorials
- **API Documentation** (20%): Parameter descriptions
- **Changelog** (20%): Version history and updates

#### Evaluation Criteria
```yaml
readme_sections:
  required:
    - description
    - requirements
    - installation
    - usage
  recommended:
    - examples
    - configuration
    - troubleshooting
    - contributing
    - license
```

### 3. Maintenance Activity (25% weight)

**Purpose**: Measure the health and activity of the project

#### Activity Metrics
- **Commit Frequency** (25%): Recent commit activity
- **Issue Response** (25%): Time to first response
- **Pull Request Activity** (25%): PR merge rate and time
- **Release Cadence** (25%): Frequency of releases

#### Time Decay Function
```python
def calculate_activity_score(last_activity_date):
    days_since = (datetime.now() - last_activity_date).days
    
    if days_since <= 30:
        return 10.0
    elif days_since <= 90:
        return 8.0
    elif days_since <= 180:
        return 6.0
    elif days_since <= 365:
        return 4.0
    elif days_since <= 730:
        return 2.0
    else:
        return 0.0
```

### 4. Community Health (20% weight)

**Purpose**: Evaluate community engagement and support

#### Community Metrics
- **Contributors** (30%): Number of unique contributors
- **Stars** (20%): GitHub star count
- **Forks** (20%): Number of forks
- **Issue Resolution** (30%): Closed vs open issues ratio

## Scoring Methodology

### Composite Score Calculation

```python
def calculate_overall_score(metrics):
    weights = {
        'testing': 0.30,
        'documentation': 0.25,
        'maintenance': 0.25,
        'community': 0.20
    }
    
    overall = sum(
        metrics[category] * weights[category] 
        for category in weights
    )
    
    return round(overall, 1)
```

### Score Normalization

All metrics are normalized to a 0-10 scale:

```python
def normalize_score(value, min_val, max_val, target_min=0, target_max=10):
    """Normalize a value to target scale"""
    if value <= min_val:
        return target_min
    elif value >= max_val:
        return target_max
    else:
        ratio = (value - min_val) / (max_val - min_val)
        return target_min + (ratio * (target_max - target_min))
```

### Score Bands

| Score Range | Classification | Description |
|------------|----------------|-------------|
| 9.0 - 10.0 | Excellent | Production-ready, best practices |
| 7.0 - 8.9 | Good | Solid choice, minor improvements needed |
| 5.0 - 6.9 | Fair | Usable but needs significant work |
| 3.0 - 4.9 | Poor | Major issues, use with caution |
| 0.0 - 2.9 | Critical | Abandoned or severely flawed |

## Technology-Specific Adaptations

### Ansible-Specific Metrics

```yaml
ansible_specific:
  testing:
    - molecule_scenarios: Check .molecule/ directory
    - ansible_lint: Check .ansible-lint file
    - galaxy_tests: Check tests/ directory
    
  structure:
    - meta_main: Check meta/main.yml
    - tasks_main: Check tasks/main.yml
    - defaults: Check defaults/main.yml
    - handlers: Check handlers/main.yml
    
  best_practices:
    - idempotency: Check for changed_when usage
    - tags: Check for task tags
    - variables: Check for proper variable naming
```

### Terraform-Specific Metrics (Future)

```yaml
terraform_specific:
  testing:
    - terratest: Check for Go test files
    - checkov: Security scanning configuration
    - tflint: Linting configuration
    
  structure:
    - main_tf: Check main.tf
    - variables_tf: Check variables.tf
    - outputs_tf: Check outputs.tf
    - versions_tf: Check versions.tf
    
  best_practices:
    - state_management: Remote state configuration
    - modules: Module structure and reusability
    - providers: Provider version constraints
```

## Quality Indicators

### Positive Indicators (Boost Score)

```python
positive_indicators = {
    'has_ci_badge': +0.5,
    'has_security_policy': +0.5,
    'has_code_of_conduct': +0.3,
    'has_contributing_guide': +0.3,
    'uses_semantic_versioning': +0.4,
    'has_automated_releases': +0.5,
    'includes_examples_directory': +0.5,
    'has_issue_templates': +0.3,
    'uses_branch_protection': +0.4,
    'signed_commits': +0.3
}
```

### Negative Indicators (Reduce Score)

```python
negative_indicators = {
    'has_security_vulnerabilities': -2.0,
    'uses_deprecated_syntax': -1.0,
    'no_license': -1.5,
    'broken_ci_builds': -1.0,
    'high_complexity': -0.5,
    'no_tests': -2.0,
    'abandoned_repo': -3.0,
    'many_open_issues': -0.5,
    'no_documentation': -2.0,
    'hardcoded_secrets': -3.0
}
```

## Recommendation Engine

### Recommendation Generation

```python
def generate_recommendations(analysis_result):
    recommendations = []
    
    # Testing recommendations
    if analysis_result['testing']['score'] < 7:
        if not analysis_result['testing']['has_molecule']:
            recommendations.append({
                'priority': 'high',
                'category': 'testing',
                'action': 'Add Molecule tests for role validation',
                'impact': '+2.0 testing score'
            })
    
    # Documentation recommendations
    if analysis_result['documentation']['score'] < 7:
        if not analysis_result['documentation']['has_examples']:
            recommendations.append({
                'priority': 'medium',
                'category': 'documentation',
                'action': 'Add usage examples to README',
                'impact': '+1.5 documentation score'
            })
    
    # Sort by priority and impact
    return sorted(recommendations, 
                  key=lambda x: (x['priority'], x['impact']), 
                  reverse=True)
```

### Priority Levels

| Priority | Score Impact | Implementation Effort | Example |
|----------|-------------|----------------------|---------|
| Critical | >2.0 points | Variable | Add license file |
| High | 1.0-2.0 points | Medium | Add test suite |
| Medium | 0.5-1.0 points | Low-Medium | Improve documentation |
| Low | <0.5 points | Low | Add badges to README |

## Caching Strategy

### Cache Layers

```yaml
cache_layers:
  L1_memory:
    ttl: 300  # 5 minutes
    size: 100 # repositories
    
  L2_redis:
    ttl: 3600  # 1 hour
    size: 10000
    
  L3_database:
    ttl: 86400  # 24 hours
    size: unlimited
```

### Cache Invalidation

```python
def should_invalidate_cache(repo_data, cached_data):
    """Determine if cache should be invalidated"""
    
    # Check if repository was updated
    if repo_data['pushed_at'] > cached_data['analyzed_at']:
        return True
    
    # Check if cache is too old
    cache_age = datetime.now() - cached_data['analyzed_at']
    if cache_age.days > 7:
        return True
    
    # Check if scoring algorithm changed
    if cached_data['algorithm_version'] != CURRENT_VERSION:
        return True
    
    return False
```

## Performance Optimization

### Parallel Analysis

```python
async def analyze_repository_parallel(repo_url):
    """Analyze repository with parallel metric collection"""
    
    tasks = [
        analyze_testing_async(repo_url),
        analyze_documentation_async(repo_url),
        analyze_maintenance_async(repo_url),
        analyze_community_async(repo_url)
    ]
    
    results = await asyncio.gather(*tasks)
    
    return aggregate_results(results)
```

### Batch Processing

```python
def batch_analyze_repositories(repo_list, batch_size=10):
    """Process repositories in batches"""
    
    results = []
    
    for i in range(0, len(repo_list), batch_size):
        batch = repo_list[i:i + batch_size]
        batch_results = process_batch_parallel(batch)
        results.extend(batch_results)
        
        # Rate limit protection
        time.sleep(1)
    
    return results
```

## Validation & Testing

### Score Validation

```python
def validate_score(score_data):
    """Validate score calculation"""
    
    assertions = [
        0 <= score_data['overall'] <= 10,
        sum(score_data['weights'].values()) == 1.0,
        all(0 <= v <= 10 for v in score_data['metrics'].values()),
        score_data['algorithm_version'] == CURRENT_VERSION
    ]
    
    if not all(assertions):
        raise ValueError("Invalid score calculation")
    
    return True
```

### Regression Testing

```yaml
test_repositories:
  excellent:
    - ansible/ansible  # Expected: 9.0-10.0
    - geerlingguy/ansible-role-docker  # Expected: 8.5-9.5
    
  good:
    - community/general  # Expected: 7.0-8.5
    
  poor:
    - abandoned/old-role  # Expected: 0.0-3.0
```

---

*This quality framework ensures consistent, objective assessment of IaC repositories across different technologies.*