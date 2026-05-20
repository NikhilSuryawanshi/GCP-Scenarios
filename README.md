# GCP-Scenarios

This repository contains reproducible Google Cloud (GCP) issue reproduction scenarios implemented with Terraform. Each scenario bundles the Terraform code, explicit repro steps, expected behavior, and cleanup instructions so engineers can reproduce, diagnose, and test cloud issues in a repeatable way.

**Purpose:** Provide a collection of self-contained, documented GCP scenarios that demonstrate specific issues, misconfigurations, or edge cases. Useful for debugging, automated testing, knowledge sharing, and postmortems.

**Repository layout**
- Organize scenarios by product, then scenario name. Example path:
	`product/scenario-name/files` (for example `cloud-run/sidecar-packet-capture/files`).
- `product/` — top-level folders named for a GCP product or service (e.g. `cloud-run`, `compute`, `networking`).
- `modules/` — optional shared Terraform modules used across scenarios.
- `scripts/` — helper utilities (optional).

Scenario folder structure (recommended):
- `product/scenario-name/files/`
	- `README.md` — human-readable repro steps, expected outcome, and cleanup instructions
	- `main.tf`, `variables.tf`, `outputs.tf` — Terraform config
	- `vars.tfvars` (optional) — example variable values
	- `cleanup.sh` (optional) — helper to remove resources

**Prerequisites**
- Install `terraform` (recommended >= 1.5)
- Install and authenticate `gcloud` CLI
- A GCP project with billing enabled and appropriate IAM permissions to create resources

**How to run a scenario**
1. Configure your environment (set `GOOGLE_CLOUD_PROJECT`, authenticate with `gcloud auth application-default login`, or export required service account credentials).
2. Change into the scenario directory: `cd product/01-short-name`.
3. Initialize and apply Terraform:

```bash
terraform init
terraform apply -var="project=YOUR_PROJECT_ID"
```

4. Follow the scenario `README.md` for additional manual steps or verification commands.
5. When finished, run `terraform destroy -var="project=YOUR_PROJECT_ID"` (or the scenario's `cleanup.sh`) to remove resources.

**Adding a new scenario**
- Create a new folder under `product/` with a leading numeric prefix to preserve order.
- Include a `README.md` describing: title, short description, GCP services used, Terraform version, step-by-step repro, expected behavior, and cleanup steps.
- Ensure Terraform state is not committed (use remote state or .gitignore local state files).

**Contributing & Support**
- Open an issue to propose a new scenario or ask for help.
- Submit a pull request with the scenario folder and documentation.

---
