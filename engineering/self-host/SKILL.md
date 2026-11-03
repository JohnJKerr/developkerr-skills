---
name: self-host
description: Prepare a repository for Coolify hosting with Dockerfiles or Compose where appropriate, external-service configuration, concise setup notes and secret-leakage checks. Validate locally where practical. Does not deploy, change live infrastructure or rotate credentials.
---

# Self-Host

Prepare the repository for hosting in Coolify. Deliver the required build/runtime files and succinct setup instructions; do not deploy or change live infrastructure.

## Inspect the project

Read the existing build, runtime and hosting configuration. Identify the deployable applications, build context, runtime entrypoints, ports, configuration and external dependencies. Reuse working conventions rather than replacing them incidentally. Resolve material uncertainty about what deploys together before choosing the packaging.

Consult current official documentation when the project's Coolify, framework or container behaviour needs verification. Follow the versions and runtime actually used; do not invent configuration or force a dependency upgrade merely to prepare hosting.

## Prepare the deployment files

- Prefer a Dockerfile for a single deployable application. Use Compose when multiple projects need to deploy together, rather than scaffolding it by default.
- Keep MongoDB, Logto and similar dependencies as separate services. Configure their addresses and required connections instead of bundling them into the application deployment.
- Follow the project's stack and build process, including appropriate build and runtime stages. Keep the runtime image focused on what the application needs.
- Account for the runtime entrypoint, listening address and port, health checks and persistent storage where relevant. Keep environment-specific values configurable.
- Distinguish build-time configuration from runtime configuration, especially for front-end assets. A value compiled into browser code is public, even if supplied through a private build environment.
- Review the build context and `.dockerignore` so credentials, local environment files, unrelated output and other unnecessary files do not enter the build.

Do not change application architecture or production authentication policies merely to make container startup easier.

## Check for secret leakage

Scan relevant repository files, tracked configuration, environment examples and the actual build context for secrets. Review Dockerfiles, Compose files, build scripts and logging paths for ways credentials could enter committed files, image layers, build arguments or logs. Use an available secret scanner where useful, with redacted output; otherwise perform focused checks and state their limits.

Prevent the inspection itself from disclosing values: do not dump environment files or print raw matching lines that may contain secrets. Report file locations and credential types without reproducing secret values.

- Keep real secrets out of committed files and images. Use placeholders in examples and external configuration for runtime secrets.
- Do not pass secrets through ordinary Docker build arguments or bake them into image environment values. Where a build genuinely needs a credential, use a supported secret mechanism and ensure outputs and logs do not persist it.
- Deleting a secret in a later image layer does not remove it from an earlier layer. Exclude it from the build context and avoid copying it in the first place.
- A `.gitignore` entry does not remove an already tracked secret. Check what is tracked as well as what could be copied into an image.
- Flag confirmed exposure for revocation or rotation; do not imply deleting the current value remedies previous exposure. Do not rotate credentials or rewrite repository history as part of this skill.

Correct leakage paths in the repository within the requested scope, without displaying secret values. Report unresolved exposure or configuration needs plainly. A scan with no findings is not proof that no secrets exist; identify material coverage limits.

## Validate locally

Build the container and smoke-test startup locally where practical. Use safe placeholder or local-test configuration and avoid contacting production services or running production migrations. Check relevant port, health and static-asset behaviour for the application rather than treating a successful image build as proof of runtime readiness.

Keep validation proportionate to the repository changes. If required tools or dependencies are unavailable, state what could not be checked and why. Do not claim deployment success: no deployment is performed.

## Document and finish

Add or update succinct Coolify setup notes, normally in the project's `/docs` folder. Cover the build file and context, expected ports and health checks, required configuration names with placeholders, external services and relevant storage requirements. Include a configuration step only when it is needed by this project.

Explain what repository files changed, the checks actually performed and what remains for the user to configure in Coolify. Highlight any secret exposure requiring user action without revealing the secret. Do not deploy, create hosting resources, change live service settings or rotate credentials.
