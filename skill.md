---
name: google-cloud-docs-engine
description: |
  Architect and author enterprise-grade Google Cloud and GKE documentation that reflects Staff Platform Architect standards. Use this skill whenever someone asks you to create, audit, or improve a README.md for Google Cloud labs, GCP architectural guides, or Kubernetes documentation. This skill ensures documentation is visually scannable, architecturally rigorous, technically flawless, and suitable for enterprise audiences. Applies to: creating new lab READMEs, improving existing documentation, designing documentation structures for multi-cloud or multi-cluster scenarios, establishing documentation standards for engineering teams, or auditing documentation quality.
compatibility: None
---

# 🌐 Google Cloud Enterprise Documentation Engine (GEMINI Framework)

Welcome to the definitive documentation framework for Google Cloud, GKE, and enterprise infrastructure labs. This skill encodes the standards of a **Staff Platform Architect at Google Cloud**: authoritative, visually stunning, technically flawless, and deeply empathetic to developer execution.

Your mission: Bridge the gap between abstract architectural patterns and concrete terminal execution. Every README should educate before it instructs.

---

## 🧠 Part 1: The Philosophy Layer

### 6. Documentation Philosophy (The "Why Before How" Rule)

Every repository must **educate before it instructs**.

Never begin a README by immediately listing commands. Instead, follow this sequence:

1. **What problem does this solve?**
2. **Why does this Google Cloud service exist?**
3. **When should an enterprise choose this architecture?**
4. **What tradeoffs are involved?**
5. **Only then explain how to implement it.**

Every lab should feel like a condensed Google Cloud Architecture Center article, not a collection of terminal commands.

#### Required Section Flow

Every significant section must follow this architectural cascade:

```
Business Problem
        ↓
Architecture Decision
        ↓
Google Cloud Service Explanation
        ↓
Implementation
        ↓
Verification
        ↓
Observability
        ↓
Cleanup
```

Never reverse this order. This pattern ensures readers understand *why* before they type.

---

### 7. Architecture-First Writing Standards

Documentation must explain infrastructure from the perspective of an **enterprise platform architect**.

#### DON'T: Explain services in isolation
❌ "Create a VPC."

#### DO: Explain architectural intent
✅ "Provision a dedicated VPC to establish network isolation for all workloads. This creates a foundational security boundary that allows firewall policies, subnet segmentation, and private service connectivity to be managed independently from application deployments."

#### Service Explanation Template

Whenever introducing a Google Cloud service, use this concise format:

```
☸️ [Service Name]

[Service Name] is [what it does and who manages it].

It [primary capability] while allowing teams to [what teams focus on instead].

### Enterprise Use Cases
• [Pattern 1]
• [Pattern 2]
• [Pattern 3]
```

**Example:**

```
☸️ Google Kubernetes Engine

Google Kubernetes Engine (GKE) is Google's managed Kubernetes platform.

It abstracts away control plane operations while allowing teams to focus on deploying workloads rather than maintaining Kubernetes masters.

### Enterprise Use Cases
• Multi-region application deployments
• Microservices at scale
• Workload isolation with Namespace policies
• Compliance-driven deployments with Policy Controller
```

---

## 🎨 Part 2: Visual & Formatting Standards

### 1. Visual Breakouts & Callout Standards

Use GitHub-flavored Markdown alert syntax to highlight critical information. **Restrict usage to prevent warning fatigue.**

```markdown
> [!NOTE]
> Use for architectural context, default platform behaviors, or background 
> processes that happen automatically in GCP infrastructure.

> [!TIP]
> Use for optimization steps, productivity shortcuts (shell aliases), 
> or cost-saving measures during lab execution.

> [!WARNING]
> Use when a step has high latent failures, precise timing dependencies 
> (waiting for external load balancer IP allocation), or complex IAM prerequisites.

> [!CAUTION]
> Use exclusively for operations that incur significant structural costs, 
> permanent data loss, or state corruption (forced Terraform state manipulation, 
> missing cleanup steps).
```

---

### 2. Image Anchoring & Local Storage Rules

**All architectural diagrams, workflow charts, and verification screenshots must be stored locally in `/images/`.**

#### Storage Location & Naming
* **Path:** `/images/` at repository root
* **Format:** lowercase, hyphen-delimited, phase-bound
* ✅ Good: `gke-cluster-topology.png`, `terraform-apply-success.png`
* ❌ Bad: `Screenshot 2026-06-30 at 12.01.AM.png`, `image1.png`

#### Structural Positioning (The Anchor Rule)

Images are **visual validation wrappers**, not decorative elements:

1. **Architectural/Topology Diagrams** → Positioned **ABOVE** the explaining text block
2. **Terminal/UI Verification** → Positioned **BELOW** the execution code block

#### HTML Syntax (Required)

Always use HTML tags for explicit dimension control:

```html
<p align="center">
  <img src="images/gke-cluster-topology.png" 
       alt="GKE Multi-Cluster Architecture Topology" 
       width="800">
</p>
```

---

### 3. Code, Terminal, and GCP Formatting

#### Explicit Syntax Highlighting
Never use bare triple backticks. Always declare language:

```bash
# Good: Language specified
gcloud compute instances list
```

```yaml
# Good: YAML syntax highlighted
apiVersion: v1
kind: Pod
metadata:
  name: example
```

#### Environment Variable Hygiene
Define variables **explicitly before use**. Never hardcode project IDs, zones, or user identifiers:

```bash
# Define first
export PROJECT_ID="qwiklabs-gcp-01-a1b2c3d4e5f6"
export REGION="us-central1"
export ZONE="${REGION}-a"

# Then reference
gcloud compute instances create my-vm \
  --project=$PROJECT_ID \
  --zone=$ZONE
```

#### Declarative Over Imperative
Prefer Terraform and Kubernetes manifests over long CLI command chains:

```hcl
# Preferred: Declarative
resource "google_container_cluster" "primary" {
  name     = "primary-cluster"
  location = "us-central1"
  
  initial_node_count = 3
}
```

#### Typographic Standards
* **Bold (`**text**`)** for UI elements: "Click **Grant Access**"
* **Backticks (`` `text` ``)** for: commands, variables, file paths, resource names
* **Standard hyphens** in prose (never em dashes `--`)

---

## 🏛️ Part 3: Structural Standards

### 8. Enterprise README Blueprint

Every repository README must follow this mandatory layout:

```
# [Repository Title]

## Executive Summary
[1-2 sentences about the problem and solution]

## Architecture Overview
[High-level diagram + description]

## Business Problem
[Why does this lab exist? What enterprise challenge does it address?]

## Solution Overview
[How does this architecture solve the problem?]

## Reference Architecture
[Detailed architecture explanation with all components]

## Prerequisites
[Required tools, accounts, permissions]

## Repository Structure
[Directory layout and file purposes]

## Environment Variables
[All variables needed for execution]

## Implementation
[Step-by-step lab execution]

## Validation
[How to verify successful deployment]

## Observability
[Monitoring, logging, metrics setup]

## Troubleshooting
[Common issues and resolutions]

## Cleanup
[Complete resource teardown]

## Cost Considerations
[Expected GCP costs and optimization notes]

## Security Considerations
[IAM, networking, compliance notes]

## Performance Notes
[Scaling characteristics and tuning]

## Further Reading
[Related documentation and patterns]

## References
[Links to official GCP docs and external resources]
```

**Never skip sections**—adapt them to your lab's scope, but maintain this structure.

---

### 9. Service Card Documentation

Whenever you introduce a major Google Cloud service, generate a documentation card:

```markdown
## ☁️ Cloud NAT

Cloud NAT enables private Google Cloud resources to access the 
internet without exposing public IP addresses.

### Why it exists

Private workloads frequently need outbound internet connectivity 
for package installation, updates, or API communication.

Cloud NAT provides outbound connectivity while preserving 
private networking.

### Enterprise Use Cases

• Private GKE clusters requiring external API access
• Secure VM fleets with controlled internet egress
• Compliance environments with zero public IPs
• Zero Trust architectures with identity-driven egress
```

Generate similar cards for every major service introduced in the lab.

---

### 10. Google Cloud Documentation Aesthetic

All documentation should mirror official Google Cloud documentation:

* **Generous whitespace** — Readability over density
* **Short paragraphs** — Max 3-4 sentences per paragraph
* **Informative headings** — Hierarchy is navigation
* **Consistent emoji usage** — Visual scanability without excess
* **Minimal decorative language** — Precision over prose
* **Diagrams before implementation** — Architecture precedes commands
* **Business context before technology** — Why before how

Readers should understand the architecture **before typing a single command**.

---

### 11. Screenshot Strategy

Screenshots are **evidence**, not decoration.

#### Allowed Screenshot Types
✅ Console verification (deployed resources visible in UI)
✅ Successful deployment (terraform apply complete, no errors)
✅ Resource topology (network diagrams, Kubernetes pod states)
✅ Monitoring dashboards (metrics, alerts, SLOs)
✅ Log entries (error traces, application output)
✅ IAM permissions (role assignments, service account bindings)
✅ Kubernetes workload state (pod replicas, deployment status)

#### Forbidden Screenshot Types
❌ Terminal output that merely repeats shell copy/paste
❌ Documentation screenshots that duplicate README text
❌ Blurry or poorly cropped images
❌ Excessively long vertical screenshots

**Golden Rule:** Every screenshot must add visual value beyond the surrounding text. If it doesn't, remove it.

---

## 🔄 Part 4: Execution Framework

### 4. Step-by-Step Document Processing Algorithm

When creating or auditing documentation, execute this pipeline sequentially:

```
[1. SCAN] ──> [2. CODE EXTRACT] ──> [3. IMAGE MAP] ──> [4. SAFETY] ──> [5. REVIEW]
```

#### [1. SCAN PHASE]
Identify all required infrastructure components:
- VPCs, subnets, firewall rules
- GKE cluster(s), node pools, add-ons
- IAM roles, service accounts, Workload Identity
- Observability (monitoring, logging, tracing)
- Storage (Cloud Storage, Persistent Volumes, Databases)
- Networking (Load Balancers, Service Mesh, DNS)

#### [2. CODE EXTRACTION]
Pull out all executable snippets and organize them linearly:
- gcloud CLI commands
- Terraform/HCL configurations
- Kubernetes YAML manifests
- Bash scripts
- Python automation

Ensure execution order is unambiguous. No forward references.

#### [3. IMAGE MAPPING]
Identify where visual aids prevent confusion:
- Topology diagrams at architecture section start
- Verification screenshots after each major step
- Observability dashboards in validation section
- Placeholder HTML tags with semantic names

#### [4. SAFETY OVERLAY]
Inject alerts at known friction points:
- GKE add-on propagation delays (5-10 minutes)
- Context switching via `kubectl config use-context`
- External Load Balancer IP allocation timing
- IAM permission propagation
- API enablement latency

#### [5. ARCHITECTURAL REVIEW]
Polish vocabulary. Replace pedestrian phrases:
- ❌ "set up a network" → ✅ "provision a decoupled, zero-trust VPC architecture"
- ❌ "create some databases" → ✅ "instrument persistent layer with managed relational storage"
- ❌ "just run the command" → ✅ "execute the infrastructure deployment pipeline"

---

### 15. Gemini Execution Prompt (Non-Negotiable)

Before generating any README, internally execute this workflow:

```
Understand the business objective
        ↓
Identify all Google Cloud services involved
        ↓
Determine the enterprise architecture
        ↓
Explain WHY each component exists
        ↓
Design the document structure
        ↓
Map image locations
        ↓
Insert architecture diagrams
        ↓
Generate implementation steps
        ↓
Generate verification procedures
        ↓
Add troubleshooting guidance
        ↓
Add cleanup instructions
        ↓
Perform architectural review
        ↓
Deliver publication-ready README
```

**Final output should:**
- Read like Google Cloud Architecture Center material
- Be architecture-driven before command-driven
- Be visually polished (proper formatting, anchored images)
- Be technically accurate (tested, no deprecated APIs)
- Be enterprise-suitable (staff architect rigor)

---

## ✨ Part 5: Language & Voice

### 14. Writing Style Rules

Write like a **Google Cloud Staff Platform Architect**.

#### Preferred Vocabulary
* provision
* orchestrate
* govern
* federate
* enforce
* observe
* validate
* harden
* optimize
* automate
* scale
* isolate
* instrument
* operationalize
* standardize

#### Avoid
* setup (use "provision" or "deploy")
* make (use "create" or "configure")
* create stuff (be specific)
* just run (use "execute")
* simply click (use "navigate to and select")
* easy (be precise instead)
* obviously (let readers decide)
* basically (be authoritative)

**Tone:** Authoritative, precise, instructional—without becoming verbose or condescending.

---

### 13. Repository Naming Convention

Repository names must immediately communicate **platform**, **core technology**, and **architectural purpose**.

#### Pattern
```
Platform-CoreTechnology-Purpose
```

#### Examples

| Repository | Description |
|---|---|
| `FleetOps-GKE-Public` | Enterprise Multi-Cluster Fleet with Anthos Service Mesh, Policy Controller, RBAC |
| `GKE-Autopilot-ScaleOps` | Zero-Ops Autopilot optimized for scalable microservices |
| `Obsrv-CloudOps-Mesh` | Cloud Operations observability with distributed tracing and ASM telemetry |
| `DataPipe-PubSub-BQ` | Streaming pipelines using Pub/Sub, Dataflow, BigQuery |
| `K8s-Workload-Identity` | Zero Trust identity with Workload Identity Federation |
| `DevSecOps-ArtifactAnalysis` | Secure supply chain with Artifact Registry, Binary Authorization |
| `FinOps-GKE-Optimization` | Cost optimization with autoscaling, Spot VMs, rightsizing |

---

## 🔍 Part 6: Quality Assurance

### 12. Architecture Review Checklist

Before publishing any README, verify the following:

#### Technical Accuracy
- [ ] Every command has been tested
- [ ] No deprecated APIs used
- [ ] UI paths are current (screenshots match current console)
- [ ] All prerequisites are listed
- [ ] Terraform/Kubernetes manifests are valid HCL/YAML

#### Documentation Quality
- [ ] Business problem clearly explained
- [ ] Architectural motivation included
- [ ] Every service has explanation card
- [ ] Verification steps are present
- [ ] Cleanup instructions are complete
- [ ] Troubleshooting section addresses common failures

#### Enterprise Readability
- [ ] Clear, scannable headings
- [ ] Consistent terminology throughout
- [ ] Professional language (no jargon without definition)
- [ ] Zero filler content
- [ ] Sections follow mandated flow

#### Visual Quality
- [ ] Images properly anchored (above/below relevant content)
- [ ] Consistent image widths (800px recommended)
- [ ] All assets are local in `/images/`
- [ ] Appropriate alt text on all images
- [ ] Screenshots are necessary (not redundant with text)

#### Architecture Quality
- [ ] Document reads like Google Cloud Architecture Center
- [ ] Every infrastructure component justified
- [ ] Security considerations addressed
- [ ] Cost implications explained
- [ ] Scalability characteristics documented

---

## 🚀 Quick Start: Creating a README with GEMINI Standards

### Workflow

1. **Understand the Business Objective**
   - What enterprise challenge does this lab solve?
   - Who are the target users (platform engineers, SREs, architects)?
   - What's the expected outcome?

2. **Scan for Infrastructure**
   - List all GCP services involved
   - Map the logical architecture
   - Identify integration points

3. **Structure the Document**
   - Use the mandatory blueprint layout
   - Create service explanation cards
   - Map where images will go

4. **Write the Content**
   - Philosophy layer first (why before how)
   - Architecture overview with diagram
   - Step-by-step implementation
   - Verification procedures

5. **Polish & Review**
   - Run the Architecture Review Checklist
   - Validate all code snippets
   - Ensure visual quality
   - Verify terminology consistency

---

## 📚 Key Principles Summary

| Principle | Application |
|---|---|
| **Why Before How** | Always explain business problem and architectural decision before implementation steps |
| **Architecture-First** | Diagrams and explanations precede code blocks |
| **Local Assets** | All images stored in `/images/` with semantic names |
| **Enterprise Voice** | Write like a Staff Platform Architect, not a tutorial writer |
| **Precision Over Prose** | Exact, authoritative language without excess verbosity |
| **Mandatory Structure** | Follow the README blueprint—adapt sections, don't skip them |
| **Visual Validation** | Screenshots are evidence of successful deployment states |
| **Service Cards** | Every major GCP service gets a concise explanation card |
| **Continuous Verification** | Validation and troubleshooting sections are required |

---

## 🎯 When to Use This Skill

**Use this skill whenever:**
- Creating a new Google Cloud or GKE lab README from scratch
- Auditing existing documentation for enterprise standards
- Designing documentation for complex multi-cloud architectures
- Establishing documentation standards for engineering teams
- Improving documentation quality for publication readiness
- Creating architectural guides or best practice documentation

**This skill ensures:** Your documentation is authoritative, visually stunning, technically accurate, and suitable for enterprise engineers at Google Cloud or organizations managing complex infrastructure.
