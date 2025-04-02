# Supabase Helm Chart

This Helm chart deploys Supabase on Kubernetes. It includes all the core Supabase services:
- Supabase Studio (Dashboard)
- PostgreSQL Database
- REST API
- Auth Service
- Realtime Service

## Prerequisites

- Kubernetes 1.19+
- Helm 3.0+
- Ingress Controller (optional, for external access)

## Installation

1. Add the Helm repository:
```bash
helm repo add supabase https://your-repo-url
helm repo update
```

2. Install the chart:
```bash
helm install supabase supabase/supabase
```

## Configuration

The following table lists the configurable parameters of the Supabase chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `nameOverride` | Override the name of the chart | `""` |
| `fullnameOverride` | Override the full name of the chart | `""` |
| `global.postgresql.auth.database` | Database name | `postgres` |
| `global.postgresql.auth.username` | Database username | `postgres` |
| `global.postgresql.auth.password` | Database password | `postgres` |
| `supabase.studio.image.repository` | Supabase Studio image repository | `supabase/studio` |
| `supabase.studio.image.tag` | Supabase Studio image tag | `20240205-0b7a0c1` |
| `supabase.studio.ingress.enabled` | Enable ingress for Supabase Studio | `true` |
| `supabase.studio.ingress.hosts` | Ingress hosts configuration | `[{"host": "supabase.local", "paths": [{"path": "/", "pathType": "Prefix"}]}]` |

For more configuration options, see the `values.yaml` file.

## Usage

1. Access Supabase Studio:
   - If ingress is enabled, access the Studio at `http://supabase.local`
   - Otherwise, use port-forwarding:
     ```bash
     kubectl port-forward svc/supabase-studio 3000:3000
     ```

2. Get database credentials:
   ```bash
   kubectl get secret supabase-db-credentials -o jsonpath='{.data.DATABASE_URL}' | base64 -d
   ```

3. Access REST API:
   ```bash
   kubectl port-forward svc/supabase-rest 3000:3000
   ```

## Uninstallation

To uninstall/delete the Supabase deployment:

```bash
helm delete supabase
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details. 