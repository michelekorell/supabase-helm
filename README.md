# Supabase Helm Chart

This is a lightweight Helm chart for deploying Supabase on Kubernetes, specifically designed for local k3s clusters managed by Rancher.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.0+
- k3s cluster managed by Rancher

## Installation

To install the chart with the release name `supabase`:

```bash
helm repo add supabase https://your-helm-repo-url
helm install supabase supabase/supabase
```

## Configuration

The following table lists the configurable parameters of the Supabase chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `postgresql.enabled` | Enable PostgreSQL deployment | `true` |
| `postgresql.primary.persistence.size` | PostgreSQL PVC size | `10Gi` |
| `api.image.repository` | Supabase API image repository | `supabase/edge-runtime` |
| `api.image.tag` | Supabase API image tag | `latest` |
| `studio.image.repository` | Supabase Studio image repository | `supabase/studio` |
| `studio.image.tag` | Supabase Studio image tag | `latest` |

## Components

This chart deploys the following components:

1. **Supabase API**: The core API service
2. **Supabase Studio**: The web-based management interface
3. **PostgreSQL**: The database backend

## Accessing the Services

By default, the services are exposed as ClusterIP. To access them:

1. **Supabase Studio**: Port 3000
2. **Supabase API**: Port 54321

You can configure ingress by enabling it in the values.yaml file.

## Security Notes

- Change the default PostgreSQL password in production
- Configure proper authentication keys for Supabase Studio
- Consider enabling TLS for ingress in production

## Development

This is a minimal implementation focused on local development. For production use, consider:

1. Adding proper authentication
2. Configuring persistent storage
3. Setting up proper ingress rules
4. Implementing backup solutions
5. Adding monitoring and logging 