# AGENTS.md — Awesome NVIDIA Licensing

## Purpose

This repository is a curated reference for NVIDIA software and GPU licensing. It is intended for both human operators and automated agents that need to answer licensing questions, validate compliance posture, or generate deployment guidance.

## Scope

Cover the following topics when adding or editing content:

- NVIDIA Software License Agreements (SLAs) and EULAs.
- CUDA Toolkit licensing.
- Deep-learning SDK licensing (cuDNN, TensorRT, TensorRT-LLM).
- NVIDIA AI Enterprise (NVAIE) entitlements and pricing models.
- NVIDIA vGPU, Virtual PC, RTX Virtual Workstation, and Virtual Applications licensing.
- NVIDIA NIM deployment modes and licensing boundaries.
- NVIDIA NGC Catalog access levels and container EULAs.
- NVIDIA License System (NLS): Cloud License Service (CLS) vs. Delegated License Service (DLS).
- Cloud and marketplace licensing (PAYG, BYOL).
- Hardware-specific restrictions (GeForce/Titan data-center prohibition, bundled NVAIE GPUs).
- Open-source software (OSS) compliance and SBOM/VEX retrieval.
- Compliance checklists for pre-deployment, operations, and audits.

## Style

- Use the same format as the other `awesome-*` repositories in this workspace.
- Keep entries factual; label official NVIDIA resources as `Official` and third-party resources as `Community`.
- Always include the disclaimer that this is reference material, not legal advice.
- Prefer official NVIDIA documentation links.

## Maintenance

- Run `./scripts/validate-links.sh` before finishing any edit.
- Update the [Quick Reference](#quick-reference) table when a new licensing rule is added.
- Update the [Glossary](#glossary) for any new abbreviations.

## Important reminders

- Do not provide legal advice or interpret EULAs as an attorney.
- When in doubt, direct users to NVIDIA Enterprise Support or their own legal/procurement teams.
- Verify dates and version-specific terms; NVIDIA license terms change over time.
