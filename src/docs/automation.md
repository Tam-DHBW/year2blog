# Automation

Overview of the CI/CD and infrastructure automation used in this project.

---

## Terraform

All AWS infrastructure is managed declaratively in the `terraform/` directory using the AWS provider (v6.x). State is stored remotely in an S3 bucket (`jailbreak-terraform-state`, `eu-central-1`) with native lock file support.

### Managed Resources

| Resource | Purpose |
|----------|---------|
| API Gateway | REST API with routes auto-generated from backend code |
| Lambda | `jb_api_regular`, `jb_api_chat`, `jb_authorizer` |
| CloudFront | CDN with SPA routing and `/api` path rewriting |
| S3 | Frontend static hosting + Lambda code archives |
| DynamoDB | `jb_counters`, `jb_prompt_templates`, `jb_levels` |
| Cognito | Moderator authentication (OAuth2/OIDC) |
| CloudWatch | Lambda log groups |

The API Gateway spec is auto-generated from the Rust backend at plan/apply time, keeping routes in sync with code.

---

## GitHub Actions

A workflow (`.github/workflows/sonarqube.yml`) runs on every push to `main` and on pull requests.

**Steps:**

1. Checkout with full history
2. Setup Node.js 24 and Rust toolchain
3. Generate code coverage via `cargo-llvm-cov`
4. Run SonarQube scan and upload results

---

## SonarQube

[SonarCloud](https://sonarcloud.io) performs continuous code quality inspection, configured in `sonar-project.properties`.

- **Project:** `Tam-DHBW_jAilbreak`
- **Coverage:** Rust LCOV reports (`backend/lcov.info`)
- **Exclusions:** `node_modules`, `dist`, `target`, `reports`
- **Checks:** Code smells, bugs, security vulnerabilities, duplicates
