# pr-agent-settings

Qodo Merge compliance rules and codebase standards for **kodflow** organization.

## Structure

```
pr-agent-settings/
├── metadata.yaml                              # Repo → compliance path mapping
└── codebase_standards/
    ├── global/                                # Applied to ALL repos
    │   └── pr_compliance_checklist.yaml
    └── devcontainer-template/                 # Repo-specific rules
        └── pr_compliance_checklist.yaml
```

## How It Works

1. Qodo Merge reads `metadata.yaml` to find which compliance paths apply to each repo
2. Global rules are applied first, then repo-specific rules
3. Each PR is checked against the combined ruleset

## Adding a New Repository

1. Add entry to `metadata.yaml`:

```yaml
my-new-repo:
  pr_compliance_checklist_paths:
    - "global"  # Always include global
    - "my-new-repo"  # Repo-specific rules
```

2. Create `codebase_standards/my-new-repo/pr_compliance_checklist.yaml`

## Compliance Rule Format

```yaml
pr_compliances:
  - title: "Rule Name"
    compliance_label: true
    objective: "What this rule ensures"
    success_criteria: "Conditions that pass the check"
    failure_criteria: "Conditions that fail the check"
```

## Documentation

- [Qodo Merge Compliance Docs](https://qodo-merge-docs.qodo.ai/tools/compliance/)
- [Configuration Options](https://qodo-merge-docs.qodo.ai/usage-guide/configuration_options/)

## Activation

Add to your `.qodo-merge.toml` or `.pr_agent.toml`:

```toml
[pr_compliance]
enable_global_pr_compliance = true
enable_generic_custom_compliance_checklist = true
```
