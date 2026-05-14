# Deployment Guide

This guide covers how to redeploy the jAilbreak project from scratch.

## Prerequisites

- [Nix](https://nixos.org/download/) with flakes enabled
- AWS account with SSO configured
- Git

## Steps

### 1. Clone the Repository

```bash
git clone https://github.com/Tam-DHBW/jAilbreak
cd jAilbreak
```

### 2. Enter the Development Environment

```bash
nix develop
```

This provides all required tooling via the Nix flake, including:
- AWS CLI & SAM CLI
- Terraform
- Rust toolchain (rustc, cargo, cargo-lambda)
- Node.js & TypeScript

### 3. Authenticate with AWS

```bash
aws sso login
```

Make sure your SSO session is configured and you have the necessary permissions for the target account.

### 4. Deploy Infrastructure

```bash
terraform -chdir=terraform apply
```

Review the plan and confirm. This provisions all AWS resources (Lambda, S3, Cognito, API Gateway, etc.).

### 5. Deploy Backend

```bash
just b_deploy
```

This builds the Rust Lambda functions with `cargo lambda build` and deploys them in parallel:
- `jb_authorizer` — custom API Gateway authorizer
- `jb_api_regular` — standard API handler
- `jb_api_chat` — chat/streaming handler

### 6. Deploy Frontend

```bash
just f_deploy
```

This builds the Vite frontend and uploads the `dist/` folder to the S3 hosting bucket. You will be prompted to confirm before the upload proceeds.

## Quick Reference (Full Redeploy)

```bash
git clone https://github.com/Tam-DHBW/jAilbreak
cd jAilbreak
nix develop
aws sso login
terraform -chdir=terraform apply
just b_deploy
just f_deploy
```
