# Awesome NVIDIA Licensing

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](http://creativecommons.org/publicdomain/zero/1.0/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)

A curated, practical guide to understanding, deploying, and staying compliant with **NVIDIA software and GPU licensing**. This repo is designed for both humans (operators, architects, procurement) and coding agents (automated compliance checks, deployment scripts, and policy enforcement).

> ⚖️ **Disclaimer:** This is community-curated reference material, **not legal advice**. NVIDIA license terms change over time and may vary by country, product version, and purchase channel. Always read the current EULA/SLA for the exact product you deploy and consult your legal/procurement teams for binding decisions.

---

## Contents

- [Quick Reference](#quick-reference)
- [Core NVIDIA License Agreements](#core-nvidia-license-agreements)
  - [NVIDIA Software License Agreement (SLA)](#nvidia-software-license-agreement-sla)
  - [CUDA Toolkit End User License Agreement (EULA)](#cuda-toolkit-end-user-license-agreement-eula)
  - [cuDNN, TensorRT, and Deep Learning SDKs](#cudnn-tensorrt-and-deep-learning-sdks)
- [NVIDIA AI Enterprise (NVAIE)](#nvidia-ai-enterprise-nvaie)
- [NVIDIA vGPU / Virtual Workstation](#nvidia-vgpu--virtual-workstation)
- [NVIDIA NIM](#nvidia-nim)
- [NVIDIA NGC and Container Licensing](#nvidia-ngc-and-container-licensing)
- [NVIDIA License System (NLS)](#nvidia-license-system-nls)
- [Cloud and Marketplace Licensing](#cloud-and-marketplace-licensing)
- [Hardware-Specific Restrictions](#hardware-specific-restrictions)
- [Open Source Software (OSS) Compliance](#open-source-software-oss-compliance)
- [Kubernetes and GPU Operator Licensing](#kubernetes-and-gpu-operator-licensing)
- [Common Licensing Mistakes](#common-licensing-mistakes)
- [Compliance Checklists](#compliance-checklists)
- [Tools and Official Resources](#tools-and-official-resources)
- [Glossary](#glossary)
- [Contributing](#contributing)
- [License](#license)

---

## Quick Reference

| Situation | License Requirement | Enforcement | Key Source |
|---|---|---|---|
| Bare-metal CUDA compute on a data-center GPU | Generally no license for CUDA driver/runtime itself | EULA only | [CUDA EULA](https://docs.nvidia.com/cuda/eula/index.html) |
| Access NGC-gated enterprise containers (NIM, Riva, etc.) | **NVIDIA AI Enterprise** required for production | NGC entitlement check | [NVAIE Licensing](https://docs.nvidia.com/ai-enterprise/planning-resource/licensing-guide/latest/licensing.html) |
| vGPU for Compute (time-sliced / MIG-backed) | **NVAIE** license per vGPU instance | Software enforced; performance degrades without license | [vGPU FAQ](https://docs.nvidia.com/vgpu/faq/latest/nls.html) |
| RTX Virtual Workstation (vWS) / high-end 3D VDI | **vWS** license per concurrent user (CCU) | Software enforced | [vGPU Client Licensing](https://docs.nvidia.com/vgpu/latest/grid-licensing-user-guide/index.html) |
| Virtual PC (vPC) / multimedia VDI | **vPC** license per concurrent user | Software enforced | [vGPU Client Licensing](https://docs.nvidia.com/vgpu/latest/grid-licensing-user-guide/index.html) |
| Virtual Applications (vApps) / RDSH app streaming | **vApps** license per concurrent user | EULA mostly; software for one user per vGPU | [vGPU Client Licensing](https://docs.nvidia.com/vgpu/latest/grid-licensing-user-guide/index.html) |
| Self-hosted NVIDIA NIM in production | **NVAIE** license per GPU | NGC entitlement / EULA | [NIM docs](https://docs.nvidia.com/nim/) |
| GeForce/Titan driver in a data center | **Prohibited** (except blockchain processing) | EULA | [GeForce EULA](https://www.nvidia.com/en-us/drivers/geforce-license/) |
| NVIDIA Omniverse Enterprise | NVAIE or Omniverse Enterprise entitlement | License server token (CLS/DLS) | [Omniverse Licensing](https://docs.omniverse.nvidia.com/enterprise/latest/ov_license_server/license_services.html) |
| NGC free public containers | NGC account / API key for some; no license for many public images | Authenticated access for private/entitled content | [NGC Catalog Guide](https://docs.nvidia.com/ngc/latest/ngc-catalog-user-guide.html) |

---

## Core NVIDIA License Agreements

### NVIDIA Software License Agreement (SLA)

Most NVIDIA SDKs, libraries, and enterprise software are governed by the **NVIDIA Software License Agreement**. It is a click-through agreement you accept when downloading the software.

Key concepts:

- **Licensed, not sold.** NVIDIA grants a limited, non-exclusive, non-transferable, non-sublicensable (unless stated) license.
- **Authorized users.** Employees, contractors, and (for academic institutions) enrolled/employed users on your secure network.
- **Distribution rights.** Only portions explicitly marked as "distributable" may be redistributed, typically as incorporated object code into an application with material additional functionality.
- **Prohibited uses.** Reverse engineering, decompilation, stand-alone redistribution, and use beyond the licensed scope.
- **Updates.** Maintenance and updates are governed by the same agreement unless superseded.

> **Agent note:** Always locate the exact SLA version embedded with the downloaded artifact (`/opt/nvidia/.../LicenseAgreement.pdf` or `EULA.html`).

- **[NVIDIA Software License Agreement](https://www.nvidia.com/en-us/agreements/software-license-agreement/)** `Official`
- **[NVIDIA Trustworthy AI Terms](https://www.nvidia.com/en-us/agreements/trustworthy-ai/terms/)** `Official` — applies to AI offerings.

### CUDA Toolkit End User License Agreement (EULA)

The CUDA Toolkit EULA covers the CUDA Toolkit, CUDA Samples, the NVIDIA Display Driver, and NVIDIA Nsight tools.

- **Free to use** for development and deployment on NVIDIA GPUs.
- **No per-GPU license fee** for the CUDA runtime/driver itself.
- **Export controls** apply; confirm you are not in an embargoed jurisdiction.
- **GeForce data-center prohibition** is enforced through the driver EULA, not the CUDA EULA per se.

- **[CUDA EULA](https://docs.nvidia.com/cuda/eula/index.html)** `Official`

### cuDNN, TensorRT, and Deep Learning SDKs

Deep-learning SDKs (cuDNN, TensorRT, TensorRT-LLM, etc.) each have product-specific license supplements.

- **cuDNN** is governed by the NVIDIA cuDNN Software License Agreement.
- **TensorRT** has its own SLA; newer **TensorRT for RTX** has a separate EULA.
- Redistribution is permitted only for portions identified as distributable and only when embedded into an application with material additional functionality.
- Include the notice: `This software contains source code provided by NVIDIA Corporation.` when distributing sample-derivative source code.

- **[cuDNN SLA](https://docs.nvidia.com/deeplearning/cudnn/sla/index.html)** `Official`
- **[TensorRT SLA](https://docs.nvidia.com/deeplearning/tensorrt-rtx/latest/reference/sla.html)** `Official`
- **[TensorRT for RTX License](https://developer.download.nvidia.com/licenses/NVIDIA_TensorRT_RTX_License_(21Apr2025).pdf)** `Official`

---

## NVIDIA AI Enterprise (NVAIE)

NVIDIA AI Enterprise is the umbrella production license and support subscription for NVIDIA's AI software stack.

### What it unlocks

- Production rights for NIM microservices, Riva, NeMo, Triton Inference Server, TensorRT, cuDNN, and many NGC enterprise containers.
- Enterprise support (Business Standard or Business Critical).
- Maintenance, security patches, and long-term branches for selected components.
- Access to gated NGC content and Helm charts.

### Licensing model

- **Per GPU.** One license is required for every GPU installed in the server or workstation running NVAIE software.
- **Per server/instance** for CPU-only compute environments.
- **Subscription or perpetual.** Subscriptions are 1, 3, or 5 years. Perpetual licenses include 5 years of Business Standard Support.
- **Cloud consumption** via cloud marketplaces (pay per GPU-hour).

### Bundled NVAIE

- **H100 PCIe / NVL and H200 NVL** include a 5-year NVAIE subscription (activation required with GPU serial number).
- **A800 40GB Active** includes a 3-year NVAIE subscription.
- **DGX Hopper** systems include NVAIE in the DGX software bundle.
- **DGX Blackwell (B200/B300)** and **Blackwell DGX systems** do **not** bundle NVAIE; licenses must be purchased separately.

- **[NVIDIA AI Enterprise Licensing Guide](https://docs.nvidia.com/ai-enterprise/planning-resource/licensing-guide/latest/licensing.html)** `Official`
- **[NVAIE Packaging & Pricing Guide (PDF)](https://www.nvidia.com/en-us/data-center/products/ai-enterprise-suite/)** `Official`

---

## NVIDIA vGPU / Virtual Workstation

NVIDIA vGPU software enables multiple VMs to share a physical GPU. Licensing depends on the vGPU type and use case.

### License editions

| Edition | Target Users | Typical Workload |
|---|---|---|
| **NVIDIA Virtual Applications (vApps)** | App streaming / RDSH users | PC-level apps delivered via Citrix, VMware Horizon, RDSH |
| **NVIDIA Virtual PC (vPC)** | VDI knowledge workers | Full Windows VDI with multimedia and browser video |
| **NVIDIA RTX Virtual Workstation (vWS)** | Power users | High-end CAD, CAE, 3D rendering, professional graphics |

### Licensing model

- **Per Concurrent User (CCU).** One license per active user/session.
- **Annual subscription** or **perpetual + SUMS** (Support, Upgrade, and Maintenance Subscription).
- vPC and vWS include a vApps entitlement.

### Enforcement

| Deployment | Required License | Enforcement |
|---|---|---|
| A-series vGPU | vApps | Software (one user per vGPU) + EULA |
| B-series vGPU | vPC or vWS | Software |
| Q-series vGPU | vWS | Software |
| GPU passthrough — workstation/3D | vWS | Software |
| GPU passthrough — PC apps | vApps | EULA only |
| Bare metal — workstation/3D | vWS | Software |
| Bare metal — PC apps | vApps | EULA only |

- **[Virtual GPU Client Licensing User Guide](https://docs.nvidia.com/vgpu/latest/grid-licensing-user-guide/index.html)** `Official`
- **[vGPU Licensing FAQ](https://docs.nvidia.com/vgpu/faq/latest/nls.html)** `Official`

---

## NVIDIA NIM

NVIDIA NIM provides optimized, containerized inference microservices.

### Three usage modes

1. **Hosted API catalog** (`build.nvidia.com`)
   - Free tier for prototyping via the NVIDIA Developer Program.
   - Rate-limited; not intended for production traffic.
2. **Downloadable NIM containers**
   - Free for development, testing, and research on up to 16 GPUs (Developer Program).
   - Requires NVAIE for production use.
3. **NVAIE production deployment**
   - Self-hosted on your own GPUs with full enterprise support.
   - Priced per GPU per year.

> **Compliance rule of thumb:** If real end users or business transactions depend on the output, you are in production and need NVAIE.

- **[NVIDIA NIM Documentation](https://docs.nvidia.com/nim/)** `Official`
- **[NIM API Catalog](https://build.nvidia.com/explore/discover)** `Official`
- **[NVIDIA NIM FAQ / Pricing](https://www.nvidia.com/en-us/ai/nim/)** `Official`

---

## NVIDIA NGC and Container Licensing

The [NVIDIA NGC Catalog](https://catalog.ngc.nvidia.com/) hosts containers, models, Helm charts, and SDK resources.

### Access levels

| Level | View Public | Download Public | View Entitled | Download Entitled | Notes |
|---|---|---|---|---|---|
| **Guest** | Yes | Yes | Yes | No | No account required for many public assets |
| **Authenticated** | Yes | Yes | Yes | No | Requires NGC account + API key |
| **Subscriber** | Yes | Yes | Yes | Yes | Requires NVAIE or product entitlement |

### Container EULA acceptance

Pulling an NGC container typically constitutes acceptance of the product-specific EULA. Many containers include the EULA at a known path inside the image, e.g. `/opt/nvidia/<product>/LicenseAgreement.pdf`.

### OSS components

NGC containers bundle open-source software. License notices and source-code offers (e.g. for GPL/LGPL components) are usually documented in the container or on the NGC page.

- **[NGC Catalog User Guide](https://docs.nvidia.com/ngc/latest/ngc-catalog-user-guide.html)** `Official`
- **[NGC Container Registry](https://catalog.ngc.nvidia.com/)** `Official`

---

## NVIDIA License System (NLS)

NLS is the modern entitlement-delivery platform for NVAIE, vGPU, and Omniverse Enterprise.

### Service instance types

| Type | Hosting | Use case | Internet required? |
|---|---|---|---|
| **Cloud License Service (CLS)** | NVIDIA-managed in the cloud | Internet-connected clients; easiest setup | Yes (egress 80/443) |
| **Delegated License Service (DLS)** | On-premises virtual appliance | Air-gapped / sovereign / restricted networks | No, for clients |

### High-level workflow

1. Purchase entitlements through NVIDIA or a reseller; receive a **PAK ID** (30-character entitlement key).
2. In the **NVIDIA Licensing Portal** (`nvid.nvidia.com`), create a **License Server**.
3. Create or register a **Service Instance** (CLS or DLS).
4. Bind the License Server to the Service Instance.
5. Install the license on the service instance.
6. Generate a **Client Configuration Token** and deploy it to licensed clients.
7. Clients lease licenses from the service instance at boot and return them at shutdown.

### Legacy license server

Older vGPU releases used the **NVIDIA vGPU Software License Server** (FlexNet-based). New deployments should use NLS (CLS/DLS).

- **[NVIDIA License System User Guide](https://docs.nvidia.com/license-system/latest/pdf/nvidia-license-system-user-guide.pdf)** `Official`
- **[Delegated License Service User Guide](https://docs.nvidia.com/license-system/dls/latest/)** `Official`
- **[Legacy vGPU License Server User Guide](https://docs.nvidia.com/vgpu/ls/latest/grid-license-server-user-guide/index.html)** `Official`

---

## Cloud and Marketplace Licensing

### Public cloud options

| Model | License handling | When to use |
|---|---|---|
| **Pay-as-you-go (PAYG)** | License included in hourly per-GPU price | Burst, experimentation, no existing NVAIE |
| **Bring Your Own License (BYOL)** | Use existing NVAIE subscription on certified cloud instances | Already own NVAIE, need consistent entitlements |
| **Cloud marketplace subscription** | Billed through CSP marketplace | Align licensing with cloud procurement |

### Important notes

- H100/H200 NVL cloud instances may include NVAIE depending on the provider offering.
- B200/B300 cloud instances typically require separate NVAIE purchase.
- GPU passthrough VMs in the cloud follow the same rules as on-prem: NVAIE is required only for NVAIE-gated software, not for basic CUDA.
- vGPU for Compute in the cloud is software-enforced and requires NVAIE per vGPU instance.

---

## Hardware-Specific Restrictions

### GeForce and Titan in data centers

NVIDIA's GeForce/Titan driver EULA includes the clause:

> **No Datacenter Deployment.** The SOFTWARE is not licensed for datacenter deployment, except that blockchain processing in a datacenter is permitted.

Practical implications:

- Consumer-grade GPUs (GeForce/Titan) are **not authorized** for data-center software deployments.
- This restriction applies to the **software/driver**, not ownership of the hardware.
- Non-commercial, small-scale research/LAN use that does not operate at data-center scale is generally not the target of enforcement, per NVIDIA public statements.
- Datacenter/colocation providers often reject consumer GPUs for this reason.

### H100 / H200 / A800 bundled NVAIE

Selected GPUs include NVAIE subscriptions activated by serial number. Track serial numbers and activation dates for compliance audits.

### DGX systems

- DGX Hopper includes NVAIE in the DGX software bundle.
- DGX Blackwell requires separately purchased NVAIE licenses.

---

## Open Source Software (OSS) Compliance

NVIDIA products frequently incorporate open-source components (Linux kernel modules, drivers, libraries, etc.).

### What to track

- **Component inventory:** Name, version, origin URL, license name.
- **Linking/dynamic vs. static:** Static linking of copyleft libraries can affect your obligations.
- **Modifications:** Any changes to OSS components must be recorded.
- **Distribution terms:** Permissive licenses (MIT, Apache-2.0, BSD) usually require attribution; copyleft licenses (GPL, LGPL, AGPL) may require source publication.

### NVIDIA open-source resources

- NVIDIA GPU kernel modules are open-source (`nvidia/open-gpu-kernel-modules`).
- CUDA and driver packages include OSS notices and source-code offers.
- Container SBOMs and VEX documents are available from NGC for vulnerability and license review.

### Practical compliance steps

1. Generate or retrieve SBOMs for every NVIDIA container you ship.
2. Review licenses of bundled components before redistribution.
3. Preserve copyright notices and license texts.
4. For GPL/LGPL components, honor source-code offer requirements.
5. Use license-scanning tools (FOSSology, ScanCode, ORAS) in CI/CD.

- **[NVIDIA Open GPU Kernel Modules](https://github.com/NVIDIA/open-gpu-kernel-modules)** `Official`
- **[NGC SBOM / VEX Retrieval](https://docs.nvidia.com/ngc/latest/ngc-catalog-user-guide.html)** `Official`

---

## Kubernetes and GPU Operator Licensing

The [NVIDIA GPU Operator](https://github.com/NVIDIA/gpu-operator) automates driver, container runtime, and device-plugin deployment on Kubernetes. Licensing considerations:

| Node type | NVAIE required? | Notes |
|---|---|---|
| **Bare-metal worker nodes** | Only for NVAIE-gated NGC software | Basic CUDA workloads do not need NVAIE |
| **vGPU-backed VM worker nodes** | Yes, per vGPU instance | GPU Operator can distribute NLS client tokens automatically |
| **GPU passthrough VM worker nodes** | Same as bare metal inside the VM | |
| **CPU-only nodes running NVAIE software** | One NVAIE subscription/license per server/instance | |

### NLS client configuration token paths

Licenses are obtained via a **Client Configuration Token** (`.tok` file) that identifies the client to CLS/DLS.

| OS | Default token directory |
|---|---|
| Linux | `/etc/nvidia/ClientConfigToken/` |
| Windows | `%SystemDrive%:\Program Files\NVIDIA Corporation\vGPU Licensing\ClientConfigToken\` |

Ensure:

- The directory contains only the token intended for the client.
- File permissions are `744` (Linux) or equivalent restricted access.
- The `nvidia-gridd` service (Linux) or `NVIDIA Display Container LS` service (Windows) is restarted after token deployment.

## Common Licensing Mistakes

1. **Assuming CUDA requires a license.** The CUDA toolkit/driver does not require a separate license fee; compliance is EULA-based.
2. **Using free NIM endpoints for production.** The hosted `build.nvidia.com` endpoints are rate-limited and intended for prototyping.
3. **Forgetting vGPU licensing scales by concurrent user.** A vPC/vWS/vApps license is needed per active session, not per physical GPU.
4. **Deploying GeForce/Titan in data centers.** The driver EULA explicitly prohibits data-center deployment except for blockchain processing.
5. **Not tracking bundled NVAIE activation.** H100/H200/A800 GPUs include NVAIE subscriptions tied to serial numbers and ship dates.
6. **Mixing CLS and DLS in HA.** High-availability clusters must be composed entirely of DLS instances; CLS and DLS cannot be mixed in the same HA cluster.
7. **Ignoring OSS obligations in NGC containers.** Containers include GPL/LGPL and other components; retain SBOMs and honor source-code offers.

## Compliance Checklists

### Pre-deployment

- [ ] Identify every NVIDIA software component in the stack (driver, CUDA, cuDNN, TensorRT, NIM, vGPU, GPU Operator, etc.).
- [ ] Download and read the exact EULA/SLA version bundled with each component.
- [ ] Confirm GPU model and deployment mode (bare metal, passthrough, vGPU, cloud PAYG/BYOL).
- [ ] Determine whether NVAIE is required and how many GPU licenses are needed.
- [ ] Verify GeForce/Titan hardware is not deployed in a data-center driver scenario.
- [ ] Choose CLS vs. DLS based on network topology and security requirements.

### Operational

- [ ] Register all GPU serial numbers that include bundled NVAIE.
- [ ] Keep license-server uptime and HA monitoring in place (especially DLS).
- [ ] Monitor license usage vs. purchased entitlements.
- [ ] Renew subscriptions before expiration to avoid service degradation.
- [ ] Document user access and authorized-user policies.

### Audit / review

- [ ] Maintain an inventory of NVIDIA entitlements, PAK IDs, and license servers.
- [ ] Retain SBOMs and OSS notices for redistributed containers.
- [ ] Review rate-limit and production-use clauses for hosted NIM endpoints.
- [ ] Validate that vGPU workloads match purchased CCU counts.
- [ ] Run `./scripts/validate-links.sh` before publishing doc updates.

---

## Tools and Official Resources

### NVIDIA portals and docs

- **[NVIDIA Licensing Portal](https://nvid.nvidia.com/)** `Official`
- **[NVIDIA Enterprise Support](https://www.nvidia.com/en-us/support/enterprise/)** `Official`
- **[NVIDIA EULA / Agreements Hub](https://www.nvidia.com/en-us/agreements/)** `Official`
- **[NVIDIA AI Enterprise Documentation](https://docs.nvidia.com/ai-enterprise/)** `Official`
- **[NVIDIA vGPU Documentation](https://docs.nvidia.com/vgpu/)** `Official`
- **[NVIDIA NIM Documentation](https://docs.nvidia.com/nim/)** `Official`
- **[NVIDIA NGC Catalog](https://catalog.ngc.nvidia.com/)** `Official`
- **[NVIDIA GPU Operator Documentation](https://docs.nvidia.com/gpu-operator/latest/index.html)** `Official`

### Compliance / SBOM tools

- **[ORAS CLI](https://oras.land/)** `Community` — fetch NGC SBOM and VEX artifacts.
- **[FOSSology](https://www.fossology.org/)** `Community` — open-source license and copyright scanner.
- **[ScanCode Toolkit](https://github.com/nexB/scancode-toolkit)** `Community` — license and origin scanner.
- **[SPDX](https://spdx.org/)** `Community` — standard format for license data exchange.

### License-server utilities

- **`nvidialsadmin`** `Official` — CLI for managing DLS/CLS service instances.
- **NVIDIA License System User Guide** `Official` — referenced above.

---

## Glossary

| Term | Meaning |
|---|---|
| **CCU** | Concurrent User — a vGPU license metric. |
| **CLS** | Cloud License Service — NVIDIA-hosted license delivery. |
| **DLS** | Delegated License Service — on-premises license delivery. |
| **EULA** | End User License Agreement. |
| **NVAIE** | NVIDIA AI Enterprise. |
| **NLS** | NVIDIA License System. |
| **NGC** | NVIDIA GPU Cloud / NVIDIA NGC Catalog. |
| **NIM** | NVIDIA Inference Microservices. |
| **PAK ID** | Product Activation Key — 30-character entitlement identifier. |
| **SBOM** | Software Bill of Materials. |
| **SLA** | Software License Agreement. |
| **SUMS** | Support, Upgrade, and Maintenance Subscription. |
| **VEX** | Vulnerability Exploitability eXchange document. |
| **vGPU** | NVIDIA Virtual GPU technology. |
| **vPC / vWS / vApps** | Virtual PC, RTX Virtual Workstation, Virtual Applications. |

---

## Contributing

Read [CONTRIBUTING.md](./CONTRIBUTING.md) for the quality bar, entry format, and PR process.

---

## License

This list is released into the public domain under [CC0-1.0](./LICENSE).
