# Kubernetes Resources

## Namespace

A **Namespace** is a logical separation mechanism in Kubernetes.  
It allows you to group resources within the same cluster and apply
policies, access control, and resource limits per group.

Namespaces are *logical* because:
- All resources still run on the same physical cluster
- Kubernetes enforces isolation using rules, scope, and metadata
- Namespaces help organize environments such as `dev`, `test`, and `prod`

### Example: Create a Namespace

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```