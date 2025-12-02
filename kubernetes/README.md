# Helm-Operator - Simple Deployment

This is a simple Kubernetes deployment to test the `cleanstart/helm-operator:latest-dev` image on your cluster.

## Overview

This deployment demonstrates running the `helm-operator` binary as a Kubernetes Job in your cluster.

- **Image**: `cleanstart/helm-operator:latest-dev`
- **Namespace**: `helm-operator-test`
- **Resources**: Job for one-time execution of `helm-operator --help`

## Prerequisites

- Amazon EKS cluster running
- `kubectl` configured to access your EKS cluster
- Basic familiarity with Kubernetes

## Deployment Steps

### Step 1: Create the Namespace

```bash
kubectl apply -f namespace.yaml
```

Verify the namespace:
```bash
kubectl get namespace helm-operator-test
```

### Step 2: Deploy the Helm-Operator Help Job

```bash
kubectl apply -f job.yaml
```

### Step 3: Check Job Status

View the job:
```bash
kubectl get jobs -n helm-operator-test
```

View the pod:
```bash
kubectl get pods -n helm-operator-test
```

### Step 4: View Job Logs

```bash
kubectl logs -n helm-operator-test -l job-name=helm-operator-help
```

**Expected output:**
```
Usage of helm-operator:
  ... (help text)
```

## Trying Different Commands

To try a different command, edit `job.yaml` and change the args to a valid subcommand. For example, to print version info using the `version` subcommand:

```yaml
args:
  - "version"
```

Then re-apply and view logs:
```bash
kubectl delete job helm-operator-help -n helm-operator-test --ignore-not-found
kubectl apply -f job.yaml
kubectl logs -n helm-operator-test -l job-name=helm-operator-help
```

## Viewing Resources

### List all resources in namespace

```bash
kubectl get all -n helm-operator-test
```

### Describe the job

```bash
kubectl describe job helm-operator-help -n helm-operator-test
```

### Get pod details

```bash
kubectl get pods -n helm-operator-test -o wide
```

## Cleanup

### Delete the job

```bash
kubectl delete job helm-operator-help -n helm-operator-test
```

### Delete the namespace (removes everything)

```bash
kubectl delete namespace helm-operator-test
```

Or delete all resources:
```bash
kubectl delete -f job.yaml
kubectl delete -f namespace.yaml
```

## Troubleshooting

### Job Not Starting

Check pod events:
```bash
kubectl describe pod -n helm-operator-test -l job-name=helm-operator-help
```

### Pod Fails

View pod logs:
```bash
kubectl logs -n helm-operator-test -l job-name=helm-operator-help --previous
```

### Image Pull Issues

Check image pull status:
```bash
kubectl get pods -n helm-operator-test
kubectl describe pod -n helm-operator-test <pod-name>
```

## Next Steps

Once the basic job is working, you can:
- Create jobs that exercise other `helm-operator` capabilities (as applicable)
- Set up CronJobs for scheduled operations
- Add RBAC if interacting with cluster resources is required
- Mount config or values files if needed for advanced scenarios


