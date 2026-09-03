# W1D6 - Securing Model Weights and AI Data Centers

This discussion session uses the RAND *Securing AI Model Weights* report and the IAPS *Accelerating AI Data Center Security Research and Implementation* report to examine high-end adversaries, security requirements for highly valuable AI assets, major AI data-center threats, and proposed defensive directions.

## Required Reading Materials

**Before the session, ensure you have access to:**

1. **RAND Corporation Report**: "Securing AI Model Weights" (RRA2849-1)
   - **Link**: https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2800/RRA2849-1/RAND_RRA2849-1.pdf
   - **Focus**: Operational Capability levels (OC1-OC5), Security Levels (SL1-SL5), and attack-vector feasibility

2. **IAPS Research**: "Accelerating AI Data Center Security Research and Implementation"
   - **Link**: https://www.iaps.ai/research/accelerating-ai-data-center-security
   - **Focus**: Important AI data-center attack vectors and recommended security directions

### Quick Reference Guide

**Key Sections for Exercises:**

**RAND Report:**
- Operational Capability levels, especially **OC4 and OC5**
- Security Levels, especially **SL4 and SL5**
- Attack-vector feasibility at different Operational Capability levels
- Security recommendations for protecting highly valuable model weights

**IAPS Research:**
- Side-channel attacks
- Hardware supply-chain attacks
- Model-weight exfiltration
- Security standards
- Security R&D
- Threat and incident information sharing
- Hardware supply-chain security

---

## Discussion Structure

### Part 1: RAND Framework - OC4/OC5 and SL4/SL5 (50 minutes)

#### Exercise 1.1: Understanding OC4 and OC5

> **Difficulty**: 🔴🔴⚪⚪⚪  
> **Importance**: 🔵🔵🔵🔵🔵

**Task**: Open the RAND report and locate the Operational Capability (OC) framework. Focus on **OC4 and OC5**.

**Questions for Group Discussion:**

1. What does RAND mean by an Operational Capability level?
2. What distinguishes an **OC4 operation** from an **OC5 operation**?
3. Why is it more accurate to classify an operation as OC4 or OC5 than to permanently classify an organization as an "OC4 attacker" or "OC5 attacker"?
4. What kinds of attacks become substantially more feasible as an adversary has access to OC5-level resources?

<details>
<summary><b>Answer Key (Operational Capability)</b></summary>

**1. What is an Operational Capability level?**

An OC level describes the **resources and capabilities available to a particular offensive operation**.

The unit being classified is the operation rather than permanently the attacker. A highly capable intelligence service might devote relatively modest resources to one target and extraordinary resources to a small number of top-priority targets.

---

**2. What distinguishes OC4 from OC5?**

**OC4** corresponds roughly to the standard operations of leading cyber-capable institutions.

**OC5** corresponds to the relatively small number of **top-priority operations conducted by the world's most capable institutions**, where substantially more personnel, money, time, intelligence support, specialized expertise, and infrastructure may be available.

| | OC4 | OC5 |
|---|---|---|
| **Type of operation** | Standard high-end operation | Exceptional top-priority operation |
| **Likely operator** | Leading cyber-capable institution | One of the world's most capable institutions |
| **Resources** | Very substantial | Extreme |
| **Planning horizon** | Major sustained operation | Potentially multi-year |
| **Specialized capabilities** | Advanced | The most difficult capabilities may be brought to bear |

A useful shorthand is:

> **OC4 = normal high-end state operation**  
> **OC5 = exceptional, heavily resourced top-priority state operation**

---

**3. Why classify the operation rather than the attacker?**

Because the same institution does not spend the same resources on every target.

An intelligence service might use:

- commodity phishing for one operation
- custom malware and zero-days for another
- years of preparation, supply-chain access, recruited insiders, and specialized hardware for a particularly important target

RAND's framework captures the resources available to the **specific operation**.

---

**4. What changes at the high end?**

RAND treats attack feasibility as graded rather than assigning every attack exclusively to one OC level.

At higher Operational Capability, attacks requiring combinations of the following become more realistic:

- specialized zero-day development
- long-term persistence
- insider recruitment
- software or hardware supply-chain compromise
- attacks against highly isolated systems
- specialized hardware capabilities
- significant intelligence support
- long preparation times

</details>

---

#### Exercise 1.2: Understanding SL4 and SL5

> **Difficulty**: 🔴🔴🔴⚪⚪  
> **Importance**: 🔵🔵🔵🔵🔵

**Task**: Locate RAND's Security Level framework. Focus on **SL4 and SL5**.

**Analysis Questions:**

1. What adversary capability is **SL4** intended to withstand?
2. What adversary capability is **SL5** intended to withstand?
3. What is the relationship between OC4/OC5 and SL4/SL5?
4. If a system is designed to SL4, what kind of attack is it explicitly *not* necessarily designed to withstand?

<details>
<summary><b>RAND Security Level Analysis</b></summary>

| Security Level | Intended Adversary Capability |
|---|---|
| **SL4** | Standard operations by leading cyber-capable institutions — approximately **OC4** |
| **SL5** | Top-priority operations by the world's most capable institutions — approximately **OC5** |

The basic relationship is:

> **OC4 threat → design toward SL4**

> **OC5 threat → design toward SL5**

The Security Level describes what strength of offensive operation the defender is trying to withstand.

---

**What does SL4 not imply?**

SL4 does not claim that the system will withstand every attack available to the world's most capable intelligence services when they devote extraordinary resources to the target.

That is the threat model represented by **OC5 / SL5**.

</details>

---

#### Exercise 1.3: Highly Valuable Models Across Different Environments

> **Difficulty**: 🔴🔴🔴⚪⚪  
> **Importance**: 🔵🔵🔵🔵🔵

Consider a newly trained frontier model whose weights would provide a substantial strategic advantage if stolen.

Copies of the same weights are needed in several environments:

- model training
- research
- internal deployment
- public API deployment

**Questions for Group Discussion:**

1. Should each environment necessarily receive a different target Security Level?
2. If the model is sufficiently valuable that **OC4 operations are worth defending against wherever the weights are accessible**, what target Security Level should those environments have?
3. What if the organization believes the model is important enough to attract an **OC5 top-priority operation**?
4. If several environments have the same target Security Level, what still differs between them?

<details>
<summary><b>Answer Key</b></summary>

**1. Does each environment necessarily receive a different SL?**

No.

RAND discusses several environments because the **security problem and available controls differ between them**. The type of environment does not by itself determine how capable an adversary the organization wants to withstand.

For sufficiently valuable frontier-model weights, the desired level of protection may therefore be similar across several environments.

---

**2. If OC4 is the threat**

If the weights are sufficiently desirable that the organization wants to withstand OC4 operations wherever they are accessible, then the targets might look like:

| Environment | Target Security Level |
|---|---|
| Training | **SL4** |
| Research | **SL4** |
| Internal deployment | **SL4** |
| Public API deployment | **SL4** |

---

**3. If OC5 is the threat**

If the organization intends to withstand a top-priority operation by one of the world's most capable institutions:

| Environment | Target Security Level |
|---|---|
| Training | **SL5** |
| Research | **SL5** |
| Internal deployment | **SL5** |
| Public API deployment | **SL5** |

The same reasoning can produce a mixture of SL4 and SL5 if the organization believes some copies or uses of the asset justify a different threat model.

---

**4. What still differs between environments?**

The controls needed to achieve the target.

For example:

- **Training** requires protecting distributed compute systems, storage, checkpoints, and accelerator interconnects.
- **Research** requires giving researchers useful ways to interact with models without unnecessarily exposing raw weights.
- **Internal deployment** introduces inference services, internal applications, and additional users.
- **Public API deployment** deliberately exposes an interface to untrusted external users.

So:

> **The value of the asset and the adversary determine the desired Security Level.**

> **The environment strongly affects how that Security Level can be implemented.**

</details>

---

### Part 2: IAPS Data Center Security - Major Threats (35 minutes)

#### Exercise 2.1: Attack Vector Analysis

> **Difficulty**: 🔴🔴🔴⚪⚪  
> **Importance**: 🔵🔵🔵🔵🔵

**Task**: Read the IAPS discussion of the following three AI data-center attack areas.

Complete the table for **all three attacks**.

| Attack Area | How does it work? | What does the attacker need? | Why does IAPS think it matters? | What defensive direction does IAPS suggest? |
|---|---|---|---|---|
| **Side-channel attacks** | ? | ? | ? | ? |
| **Hardware supply-chain attacks** | ? | ? | ? | ? |
| **Model-weight exfiltration** | ? | ? | ? | ? |

Groups may divide the initial reading between members, but should complete and discuss the full table together.

<details>
<summary><b>IAPS Attack Vector Analysis</b></summary>

### Side-Channel Attacks

**How does it work?**

An attacker observes unintended physical effects of computation, such as:

- electromagnetic emissions
- power consumption
- acoustic signals
- other physical signals correlated with computation

Those measurements may reveal sensitive information, including cryptographic secrets.

**What does the attacker need?**

Depending on the attack:

- specialized technical expertise
- specialized measurement equipment
- physical proximity or another way to observe the relevant signal
- substantial knowledge of the hardware being attacked

**Why does IAPS think it matters?**

- AI accelerators have received less public side-channel-security scrutiny than mature general-purpose processors.
- Proprietary accelerator designs can make independent security research difficult.
- Sophisticated state adversaries may consider physical attacks that ordinary data-center security programs rarely prioritize.

**Defensive direction:**

- accelerator-specific side-channel defenses
- emissions blocking
- noise injection
- improved confidential-computing support
- dedicated hardware-security research and testbeds

---

### Hardware Supply-Chain Attacks

**How does it work?**

An attacker compromises a component before or during its delivery and installation.

The compromise may involve:

- malicious hardware
- firmware
- programmable components
- networking equipment
- supporting data-center infrastructure

The system can therefore arrive at the data center already compromised.

**What does the attacker need?**

Potential requirements include:

- access to manufacturing
- access to a supplier or integrator
- access during shipping or installation
- hardware and firmware expertise
- significant intelligence or organizational capabilities

**Why does IAPS think it matters?**

- AI data centers rely on complex global supply chains.
- Compromised hardware may operate below the visibility of normal host security controls.
- Responsibility is distributed across chip designers, manufacturers, equipment vendors, integrators, and operators.
- A sufficiently capable adversary may exploit stages of the supply chain that the final data-center operator cannot directly observe.

**Defensive direction:**

- improve supply-chain visibility
- audit security-critical hardware
- improve component verification
- improve supplier assurance
- reduce critical dependencies on high-risk supply chains
- fund additional hardware and supply-chain security research

---

### Model-Weight Exfiltration

**How does it work?**

Once an attacker obtains useful access to model weights, they must transfer the weights out of the protected environment.

IAPS discusses several possible egress paths:

- **In-band** — normal production networking
- **Out-of-band** — management networks and related infrastructure
- **Covert channels** — alternative paths designed to bypass normal egress controls

**What does the attacker need?**

- useful access to the weights or systems processing them
- an egress mechanism
- sufficient channel capacity to transfer a very large amount of information

**Why does IAPS think it matters?**

Frontier-model weights are extremely valuable once stolen.

However, their very large size also gives defenders an unusual advantage. Unlike a password, algorithm, or short research document, a frontier model may require transferring **terabytes** of data.

**Defensive direction:**

- stronger controls on normal production egress
- stronger security for management and out-of-band networks
- reduced covert-channel capacity
- defenses specifically designed around large-volume model-weight exfiltration

</details>

---

### Part 3: IAPS - Comparing Threats and Defensive Gaps (25 minutes)

#### Exercise 3.1: Comparing the Threats

> **Difficulty**: 🔴🔴🔴⚪⚪  
> **Importance**: 🔵🔵🔵🔵🔵

Using your completed table from Exercise 2.1, discuss:

1. Which attack is likely to be cheapest for an adversary under favorable circumstances?
2. Which could be hardest for a data-center operator to detect?
3. Which is most likely to require OC4 or OC5-level resources?
4. Which attacks can themselves provide the attacker with access, and which generally assume that some useful access has already been obtained?
5. Why can the enormous size of model weights be considered a defensive advantage?

<details>
<summary><b>Discussion Guide</b></summary>

**1. Cheapest**

Model-weight exfiltration may be comparatively inexpensive **if the attacker already has sufficient access and a usable egress path**.

This caveat matters:

- a supply-chain compromise can be a way of **obtaining** access
- weight exfiltration generally describes what happens **after** gaining access to the weights

---

**2. Hardest to detect**

A sophisticated **hardware supply-chain compromise** is a strong candidate.

Malicious functionality may:

- arrive before deployment
- reside below normal operating-system monitoring
- survive ordinary software reinstalls
- operate in hardware or firmware that the operator has limited ability to inspect

Other answers are reasonable if the group identifies a specific mechanism and explains why detection would be difficult.

---

**3. Most demanding**

Sophisticated **hardware supply-chain attacks** and advanced **side-channel attacks** are strong candidates for requiring very high-end capabilities.

The exact answer depends on the particular attack. IAPS does not provide a universal ranking.

---

**4. Initial compromise vs. post-compromise**

**Hardware supply-chain compromise** can itself establish attacker access or undermine system integrity.

**Side-channel attacks** may reveal secrets without conventional software compromise.

**Model-weight exfiltration** generally assumes that the attacker has already obtained some ability to access or influence systems containing the weights.

---

**5. Weight size as a defensive advantage**

Stealing a password or algorithm may require transmitting only bytes or kilobytes.

Stealing a frontier model may require transmitting **terabytes**.

That creates opportunities to:

- restrict available bandwidth
- tightly limit egress paths
- detect large transfers
- make low-bandwidth covert channels impractical

</details>

---

#### Exercise 3.2: Where Are the Defensive Gaps?

> **Difficulty**: 🔴🔴🔴🔴⚪  
> **Importance**: 🔵🔵🔵🔵🔵

**Task**: For each attack area, distinguish between defenses that an AI data-center operator can pursue directly and defenses that depend substantially on new research, hardware vendors, suppliers, or government action.

| Attack Area | What can an operator do directly? | What still depends on R&D or vendors? | What requires action outside the individual operator? |
|---|---|---|---|
| **Side-channel attacks** | ? | ? | ? |
| **Hardware supply-chain attacks** | ? | ? | ? |
| **Model-weight exfiltration** | ? | ? | ? |

<details>
<summary><b>Discussion Guide</b></summary>

### Side-Channel Attacks

**Operator actions:**

Depending on the threat and hardware, operators may be able to use:

- stronger physical-access controls
- shielding or emissions-management techniques
- greater physical separation
- confidential-computing features already supported by hardware

**R&D or vendor dependencies:**

More comprehensive defenses may require:

- accelerator-specific side-channel mitigations
- changes to chip or board design
- better confidential-computing support
- improved testing and measurement techniques

**Outside the operator:**

- accelerator vendors
- hardware researchers
- government or other research funders

---

### Hardware Supply-Chain Attacks

**Operator actions:**

Operators can:

- identify security-critical suppliers and components
- improve inventory and provenance tracking
- impose procurement and supplier-security requirements
- audit components and suppliers where feasible
- reduce unnecessary supplier diversity for the most security-critical components

**R&D or vendor dependencies:**

Stronger assurance may require:

- better hardware-verification technologies
- stronger roots of trust
- more inspectable hardware and firmware
- security features designed into components rather than added by the operator

**Outside the operator:**

Supply-chain security necessarily involves:

- component manufacturers
- equipment vendors
- integrators
- logistics providers
- governments

The final data-center operator cannot independently secure every upstream stage of the supply chain.

---

### Model-Weight Exfiltration

**Operator actions:**

Operators can directly strengthen:

- production-network egress controls
- management-network isolation and monitoring
- access controls around weight storage
- bandwidth restrictions
- logging and monitoring of large transfers
- restrictions on unnecessary outbound connectivity

**R&D or vendor dependencies:**

Harder problems include:

- identifying and limiting covert channels
- hardware-enforced egress constraints
- stronger controls in accelerators and management hardware
- mechanisms that remain reliable after partial system compromise

**Outside the operator:**

Some defenses depend on:

- accelerator vendors
- network-hardware vendors
- management-controller vendors
- shared threat intelligence about new exfiltration techniques

</details>

---

### Part 4: IAPS Recommendations and Final Review (10 minutes)

#### Exercise 4.1: IAPS Solution Directions

> **Difficulty**: 🔴🔴⚪⚪⚪  
> **Importance**: 🔵🔵🔵🔵⚪

IAPS also proposes several broader directions for improving AI data-center security.

Complete the following table in one or two sentences per row.

| IAPS Direction | What is it asking for? |
|---|---|
| **AI data-center security standards** | ? |
| **Targeted security R&D** | ? |
| **Threat and incident information sharing** | ? |
| **Hardware supply-chain security** | ? |

<details>
<summary><b>Answer Key</b></summary>

**AI Data-Center Security Standards**

Develop security frameworks specifically for high-value AI data centers, with progressively stronger requirements as the threat level increases.

**Targeted Security R&D**

Fund work on defenses that are currently immature or missing, including accelerator side-channel security, hardware security, supply-chain security, and model-weight exfiltration defenses.

IAPS discusses mechanisms including **DARPA-style programs** for some targeted research areas.

**Threat and Incident Information Sharing**

Improve sharing of:

- attacks and incidents
- indicators of compromise
- lessons learned
- relevant government threat intelligence

between AI labs, data-center operators, vendors, and government.

**Hardware Supply-Chain Security**

Improve:

- supply-chain visibility
- supplier assurance
- component verification
- trusted sourcing
- resilience against especially risky dependencies

for security-critical AI data-center hardware.

</details>

---

#### Exercise 4.2: Final Group Review

Without referring back to the reports, complete the following table.

When your group is finished, open the answer key and correct anything that was missing or substantially different.

| Concept | Explain It in One or Two Sentences |
|---|---|
| **OC4** | ? |
| **OC5** | ? |
| **SL4** | ? |
| **SL5** | ? |
| **Side-channel attacks** | ? |
| **Hardware supply-chain attacks** | ? |
| **Model-weight exfiltration** | ? |
| **IAPS solution directions** | ? |

<details>
<summary><b>Answer Key</b></summary>

**OC4**

Standard high-end operations by leading cyber-capable institutions.

**OC5**

Exceptional top-priority operations by the world's most capable institutions, with much greater resources and specialized capabilities available.

**SL4**

A security posture intended to withstand approximately OC4 operations.

**SL5**

A security posture intended to withstand approximately OC5 top-priority operations.

**Side-channel attacks**

Recover sensitive information from unintended physical effects or signals produced by computation. IAPS calls for more accelerator-specific research and defensive techniques.

**Hardware supply-chain attacks**

Compromise components before they reach or are installed by the data-center operator. IAPS calls for better visibility, verification, supplier assurance, trusted sourcing, and hardware-security R&D.

**Model-weight exfiltration**

Transfer stolen weights through production, management, or covert egress paths. IAPS emphasizes stronger egress defenses and notes that the enormous size of frontier-model weights gives defenders an unusual advantage.

**IAPS solution directions**

Develop stronger AI data-center security standards, fund targeted security R&D, improve threat and incident information sharing, and strengthen critical hardware supply chains.

</details>

---

## Key Takeaways from Document Analysis

### What We Learned from RAND:
- [ ] **OC4** describes standard operations by leading cyber-capable institutions
- [ ] **OC5** describes exceptional top-priority operations by the world's most capable institutions
- [ ] **SL4** is intended to withstand approximately OC4 operations
- [ ] **SL5** is intended to withstand approximately OC5 operations
- [ ] For sufficiently valuable frontier-model weights, several environments may all warrant SL4 or SL5 even though the controls needed in those environments differ

### What We Learned from IAPS:
- [ ] Side-channel attacks are an important and under-researched risk for AI accelerators
- [ ] Hardware supply-chain compromise can undermine assumptions made by conventional software security
- [ ] Model-weight exfiltration must account for production, management, and covert egress paths
- [ ] The enormous size of frontier-model weights gives defenders useful opportunities to constrain exfiltration
- [ ] Some important defenses can be implemented by data-center operators, while others depend on hardware vendors, supply-chain actors, government, or additional R&D
- [ ] IAPS emphasizes AI-specific security standards, targeted security R&D, threat and incident information sharing, and stronger hardware supply-chain security

---

## Further Exploration

### For Deeper Technical Understanding:
- **RAND Report Appendices**: Detailed attack-vector analysis and security-level reasoning
- **IAPS Technical Sections**: Additional discussion of AI data-center attack surfaces and proposed research directions
