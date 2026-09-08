# repository

## Description

Provisions a Git repository for a Nephio cluster. Supports multiple git providers:
- **Gitea** (default) - Self-hosted git server
- **GitHub** - GitHub.com or GitHub Enterprise
- **GitLab** - GitLab.com or self-hosted GitLab

The repository will be named after the cluster name.

## Configuration

Configure the git provider in `git-context.yaml`:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: git-context
  annotations:
    config.kubernetes.io/local-config: "true"
    kpt.dev/config-injection: "required"
data:
  provider: gitea      # Options: gitea, github, gitlab
  url: "http://172.18.0.200:3000"  # Required for Gitea, optional for custom GitHub/GitLab URLs
  org: nephio  # Organization/owner name for the repository
```

### Provider-Specific Configuration

#### Gitea (Default)
```yaml
provider: gitea
url: "http://172.18.0.200:3000"
org: nephio
```
Generates: `http://172.18.0.200:3000/nephio/{cluster-name}.git`

#### GitHub
```yaml
provider: github
org: your-org-name
```
Generates: `https://github.com/your-org-name/{cluster-name}.git`

#### GitLab
```yaml
provider: gitlab
org: your-org-or-group
```
Generates: `https://gitlab.com/your-org-or-group/{cluster-name}.git`

For self-hosted GitHub/GitLab, specify `url`:
```yaml
provider: gitlab
url: "https://gitlab.mycompany.com"
org: myteam
```
