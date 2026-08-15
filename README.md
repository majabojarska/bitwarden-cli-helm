# bitwarden-cli-helm

[![Status](https://github.com/majabojarska/bitwarden-cli-helm/actions/workflows/status.yaml/badge.svg)](https://github.com/majabojarska/bitwarden-cli-helm/actions/workflows/status.yaml)
[![Dependabot Updates](https://github.com/majabojarska/bitwarden-cli-helm/actions/workflows/dependabot/dependabot-updates/badge.svg)](https://github.com/majabojarska/bitwarden-cli-helm/actions/workflows/dependabot/dependabot-updates)

Helm chart for [majabojarska/bitwarden-cli-docker](https://github.com/majabojarska/bitwarden-cli-docker).

## Installing

```sh
kubectl create secret generic bitwarden-cli-auth \
  --from-literal=BW_CLIENTID='your_clientid' \
  --from-literal=BW_CLIENTSECRET='your_clientsecret' \
  --from-literal=BW_PASSWORD='your_vault_password'

helm upgrade --install bitwarden-cli ./helm-charts/bitwarden-cli
```

## Required configuration

The chart requires Bitwarden credentials provided either as:

1. `auth.existingSecret` (default: `bitwarden-cli-auth`) pointing to a Secret containing `BW_CLIENTID`, `BW_CLIENTSECRET`, `BW_PASSWORD`
2. `auth.existingSecret=""` and `auth.clientId`, `auth.clientSecret`, `auth.password` values (the chart then creates the Secret)

## Defaults aligned with the image

- `config.bwHost=vault.bitwarden.eu`
- `service.port=8087` and `container.port=8087`
- `persistence.enabled=true` with mounted appdata at `/home/bitwarden/appdata`
