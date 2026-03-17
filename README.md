# thomas.github.com

## Kubernetes Debugging

### Checking environment variables in a pod

To inspect environment variables (e.g., database/datasource settings) in a running container, use the correct `kubectl exec` syntax with `--` to separate the pod name from the command:

```bash
kubectl exec -n contentautomation contentautomation-appmanager-557994955f-5x254 -- printenv | grep -E "DB|POSTGRES|JDBC|SPRING_DATASOURCE"
```

**Common mistakes to avoid:**

| Incorrect | Correct |
|-----------|---------|
| `kubectl exec <pod> - <command>` (single dash) | `kubectl exec <pod> -- <command>` (double dash) |
| `Select-String` (PowerShell only) | `grep -E` (Linux/bash) |

The single `-` causes the error `exec: "-": executable file not found in $PATH` because kubectl tries to execute `-` as a command inside the container instead of treating it as the argument separator.
