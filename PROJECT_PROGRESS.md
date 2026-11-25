# DevSecOps Project Progress

Last updated: 2026-11-25

## Repository

- Fork: `Andersss819/juice-shop`
- Working branch: `devsecops/baseline`
- Final validated pipeline commit: `301ef87bf`
- GitHub Actions run: https://github.com/Andersss819/juice-shop/actions/runs/45689792129
- The `devsecops/baseline` branch is pushed to origin.

## Completed

### Environment

- Ubuntu WSL distribution installed.
- Git, curl, wget, unzip, Python 3, pip and venv installed.
- Docker Desktop 29.9.3 available.
- Docker access from WSL and Windows verified.
- Kind, kubectl and Helm installed locally.
- GitHub CLI authenticated for `Andersss819`.

### Week 1

- OWASP Juice Shop forked and cloned.
- Baseline branch created.
- Gitleaks added to GitHub Actions.
- Semgrep SARIF scan added.
- Application tests integrated.
- Git history scanned for secrets.
- Baseline pipeline errors fixed and validated.

### Week 2

- Docker image built successfully.
- Distroless base image pinned by digest.
- Hadolint Dockerfile linting added.
- Trivy configuration and image scanning added.
- Trivy configuration scope restricted to relevant Dockerfiles.
- Syft CycloneDX SBOM added.
- Container reports and SBOM uploaded as GitHub Actions artifacts.

### Week 3

- Image publishing to GHCR configured for lowercase owner path:
  `ghcr.io/andersss819/juice-shop`.
- Docker Buildx publishes by immutable digest.
- Cosign keyless signing added.
- CycloneDX SBOM attestation added.
- Cosign verification step added.
- Three Kyverno policies added:
  - signed Juice Shop images;
  - reject `:latest`;
  - require `runAsNonRoot`.
- GitHub Actions run #8 completed successfully.
- Tests, source security, container security, GHCR publishing and Cosign signing all passed.

## Final GitHub Actions Result

GitHub Actions run #8:

- Application tests: success
- Secrets and source code: success
- Dockerfile and container: success
- Publish and sign image: success
- Gitleaks, Semgrep, Trivy and container reports: available as artifacts

## Kubernetes Status

- Kind cluster name: `devsecops`
- New control-plane created and ready.
- Kyverno 3.10.0 / v1.20.0 installed with Helm.
- Kyverno policies `prohibit-latest-image-tag` and
  `require-run-as-non-root` were applied successfully.
- The signed-image policy file is ready at `k8s/kyverno-signed-images.yaml`.
- Kubernetes admission demonstration could not be completed because the
  Kind API started returning `TLS handshake timeout` and `context deadline`
  exceeded errors after Helm and Docker operations.

## Remaining Work

1. Restart Windows completely.
2. Start Docker Desktop.
3. Verify:
   ```powershell
   docker info
   kind get clusters
   kubectl get nodes
   kubectl get pods -n kyverno
   ```
4. Reapply the Kyverno policies.
5. Create one compliant Pod.
6. Demonstrate refusal of:
   - an image using `:latest`;
   - a Pod without `runAsNonRoot`;
   - an unsigned image;
7. Save and export the successful and refused `kubectl` output.
8. Pass to week 4: OWASP ZAP baseline, at least five corrections and before/after reports.
