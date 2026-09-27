# Kubernetes Secret Decoder

A simple, browser-based tool for decoding [Kubernetes Secret](https://kubernetes.io/docs/concepts/configuration/secret/) manifests into human-readable values.

**Live site:** [pilotkid.github.io/kube-secret-decoder](https://pilotkid.github.io/kube-secret-decoder/kubernetes-secret-decoder.html)

## What it does

Kubernetes Secrets store sensitive data (passwords, tokens, keys) as base64-encoded strings. This tool lets you paste a Secret manifest in YAML or JSON format and instantly see the decoded values — no server, no network requests, everything runs entirely in your browser.

## Features

- **Accepts YAML or JSON** – paste a raw `kubectl get secret -o yaml` or `kubectl get secret -o json` output directly.
- **Supports `data` and `stringData`** – decodes base64-encoded `data` entries and passes through `stringData` values as-is.
- **Multiple output formats:**
  - **JSON** – key/value object, easy to copy into config files.
  - **.env** – `KEY="value"` pairs for use with dotenv tooling.
  - **Plain text** – human-readable key + value listing.
- **Copy or download** – grab the output to your clipboard or save it as a file.
- **100% private** – no data ever leaves your browser.

## Usage

1. Open the [live page](https://pilotkid.github.io/kube-secret-decoder/kubernetes-secret-decoder.html) (or open `kubernetes-secret-decoder.html` locally in any browser).
2. Paste your Kubernetes Secret manifest into the top text area.
3. Click **Decode**.
4. Choose an output format and use **Copy output** or **Download output** as needed.

### Example input

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
data:
  USERNAME: YWRtaW4=
  PASSWORD: c2VjcmV0
```

### Example output (JSON)

```json
{
  "USERNAME": "admin",
  "PASSWORD": "secret"
}
```

## Running locally

No build step is needed. Just open the HTML file directly:

```bash
open kubernetes-secret-decoder.html   # macOS
xdg-open kubernetes-secret-decoder.html  # Linux
start kubernetes-secret-decoder.html  # Windows
```

## Deployment

The live site is automatically published to GitHub Pages whenever changes are pushed to the `main` branch via the workflow at [`.github/workflows/deploy-pages.yml`](.github/workflows/deploy-pages.yml).
