# Healthcare Agentic AI Prompts

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![Healthcare AI](https://img.shields.io/badge/Healthcare-AI%20Safety-blue)](https://github.com/topics/healthcare-ai)
[![Agentic Systems](https://img.shields.io/badge/Agentic-Multi--Agent-purple)](https://github.com/topics/agentic-ai)

A curated collection of production-tested prompt engineering patterns for **healthcare agentic AI systems**, with a focus on **safety, accuracy, and regulatory compliance**. Built from real-world experience deploying AI systems for prior authorization, clinical decision support, and medical document processing.


🎯 What This Repository Offers

| Category | Description |
|----------|-------------|
| **Multi-Agent Orchestration** | Production patterns for coordinating specialized healthcare AI agents |
| **Safety-First Prompts** | Prompts with built-in hallucination detection, confidence scoring, and human escalation |
| **Clinical Extraction** | Templates for extracting structured data from medical records, policies, and clinical notes |
| **Decision Support** | Frameworks for evidence-based clinical reasoning with audit trails |
| **Quality Assurance** | Critic agents, validation patterns, and compliance monitoring |

🏥 Healthcare-Specific Focus

Unlike general-purpose prompt collections, this repository addresses the unique challenges of healthcare AI:

- **Patient Safety**: Conservative bias when evidence is ambiguous
- **Regulatory Compliance**: HIPAA-aware processing, audit trail preservation
- **Clinical Accuracy**: Source citation requirements, hallucination prevention
- **Explainability**: Complete reasoning chains for clinical and legal review
- **Human-in-the-Loop**: Appropriate escalation to clinical reviewers

 📁 Repository Structure

```
healthcare-agentic-prompts/
├── orchestrators/                    # Multi-agent coordination prompts
│   ├── prior-auth-orchestrator/      # PA processing pipeline
│   │   ├── ORCHESTRATOR.md           # Main orchestrator prompt
│   │   ├── agents/                   # Individual agent specifications
│   │   └── schemas/                  # Input/output JSON schemas
│   └── clinical-review-orchestrator/ # Clinical documentation review
│
├── agents/                           # Standalone agent prompts
│   ├── extraction/                   # Data extraction agents
│   │   ├── policy-archivist.md       # Policy criteria extraction
│   │   ├── diagnosis-extractor.md    # ICD-10 mapping and extraction
│   │   ├── treatment-history.md      # Conservative treatment extraction
│   │   └── diagnostic-results.md     # Labs, imaging, assessments
│   │
│   ├── decision/                     # Clinical decision agents
│   │   ├── criteria-matcher.md       # Policy-to-evidence matching
│   │   ├── medical-necessity.md      # Clinical necessity evaluation
│   │   └── gap-analyzer.md           # Documentation gap identification
│   │
│   ├── quality/                      # QA and safety agents
│   │   ├── critic-agent.md           # Decision validation and review
│   │   ├── hallucination-monitor.md  # Factual grounding verification
│   │   └── compliance-auditor.md     # Regulatory compliance checking
│   │
│   └── routing/                      # Workflow routing agents
│       ├── confidence-router.md      # Confidence-based case routing
│       └── escalation-handler.md     # Human review escalation
│
├── patterns/                         # Reusable prompt patterns
│   ├── chain-patterns/               # Prompt chaining strategies
│   │   ├── snowball.md               # Iterative refinement
│   │   ├── parallel-workers.md       # Concurrent execution
│   │   ├── fallback-cascade.md       # Model fallback strategies
│   │   └── self-correction.md        # Error recovery loops
│   │
│   ├── safety-patterns/              # Healthcare safety patterns
│   │   ├── citation-required.md      # Mandatory source citations
│   │   ├── confidence-scoring.md     # Calibrated uncertainty
│   │   └── human-escalation.md       # Escalation triggers
│   │
│   └── output-patterns/              # Structured output patterns
│       ├── clinical-json.md          # Healthcare JSON schemas
│       └── audit-trail.md            # Compliance documentation
│
├── evaluation/                       # Testing and evaluation
│   ├── test-cases/                   # Example inputs and expected outputs
│   ├── benchmarks/                   # Performance benchmarks
│   └── evaluation-framework.md       # How to evaluate agent quality
│
├── docs/                             # Documentation
│   ├── getting-started.md            # Quick start guide
│   ├── architecture.md               # System architecture overview
│   ├── safety-guidelines.md          # Healthcare AI safety principles
│   └── assets/                       # Diagrams and images
│
├── examples/                         # Complete working examples
│   ├── prior-auth-case/              # End-to-end PA processing example
│   └── chart-review-case/            # Clinical chart review example
│
├── CONTRIBUTING.md                   # Contribution guidelines
├── CODE_OF_CONDUCT.md                # Community standards
├── SECURITY.md                       # Security policy
├── CHANGELOG.md                      # Version history
└── LICENSE                           # MIT License
```

🚀 Quick Start

 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/healthcare-agentic-prompts.git
cd healthcare-agentic-prompts
```

 2. Explore the Orchestrator

Start with the Prior Authorization Orchestrator to understand the multi-agent pattern:

```bash
cat orchestrators/prior-auth-orchestrator/ORCHESTRATOR.md
```

 3. Use Individual Agents

Each agent can be used standalone or as part of an orchestrated pipeline:

```python
from anthropic import Anthropic

client = Anthropic()

# Load the policy archivist prompt
with open("agents/extraction/policy-archivist.md") as f:
    system_prompt = f.read()

# Use with Claude
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=4096,
    system=system_prompt,
    messages=[{
        "role": "user",
        "content": f"Extract criteria from this policy: {policy_text}"
    }]
)
```

 4. Implement the Full Pipeline

See the [Getting Started Guide](docs/getting-started.md) for implementing the complete multi-agent system.

 🏗️ Architecture Overview

Multi-Agent Pipeline

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           ORCHESTRATOR AGENT                                │
│                    (Delegation, Coordination, Quality Gates)                │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
        ┌─────────────────────────────┼─────────────────────────────┐
        ▼                             ▼                             ▼
┌───────────────┐           ┌───────────────┐           ┌───────────────┐
│   ZONE 1:     │           │   ZONE 2:     │           │   ZONE 3:     │
│  INGESTION    │    ───►   │  EXTRACTION   │    ───►   │   DECISION    │
│  (Parallel)   │           │  (Parallel)   │           │  (Sequential) │
└───────────────┘           └───────────────┘           └───────────────┘
        │                             │                             │
        │                             │                             │
        └─────────────────────────────┼─────────────────────────────┘
                                      │
                                      ▼
                            ┌───────────────┐
                            │   ZONE 4:     │
                            │   ROUTING     │
                            │ (Conditional) │
                            └───────────────┘
                                      │
        ┌─────────────────────────────┼─────────────────────────────┐
        ▼                             ▼                             ▼
┌───────────────┐           ┌───────────────┐           ┌───────────────┐
│ Auto-Approve  │           │ Human Review  │           │  MD Escalate  │
│ (conf ≥ 0.95) │           │(0.80 ≤ c<0.95)│           │ (conf < 0.80) │
└───────────────┘           └───────────────┘           └───────────────┘
```

 Agent Categories

| Category | Agents | Purpose |
|----------|--------|---------|
| **Ingestion** | ING-1 to ING-4 | Document processing, OCR, classification |
| **Extraction** | EXT-P1, EXT-C1-4, EXT-V1 | Clinical data and policy extraction |
| **Decision** | DEC-1 to DEC-5 | Criteria matching, necessity evaluation, critique |
| **Routing** | RTE-1 to RTE-5 | Confidence-based workflow routing |
| **QA** | QA-1 to QA-4 | Continuous quality monitoring |

🛡️ Safety Principles

This repository embeds healthcare AI safety principles throughout:

 1. No Hallucinations Allowed
```markdown
## Critical Safety Rules
- NEVER fabricate clinical information not present in source documents
- ALWAYS cite specific source documents and page references
- Flag uncertainty explicitly with confidence scores
```

 2. Conservative Escalation
```markdown
## Confidence Routing
- ≥ 0.95: Auto-processing eligible
- 0.80-0.95: Nurse review required
- < 0.80: Physician review required
- Any hallucination: BLOCK auto-processing
```

 3. Complete Audit Trails
```markdown
## Audit Requirements
- Every decision must trace to source evidence
- All agent outputs logged with timestamps
- Document hashes preserved for verification
```

 📊 Evaluation Framework

Each agent includes evaluation criteria:

| Metric | Target | Measurement |
|--------|--------|-------------|
| Extraction Accuracy | ≥ 95% | Compared to gold standard |
| Decision Accuracy | ≥ 90% | Compared to MD review |
| Hallucination Rate | < 0.1% | Critic agent detection |
| Processing Time | < 5 min | End-to-end (95th percentile) |

See [evaluation/evaluation-framework.md](evaluation/evaluation-framework.md) for detailed testing methodology.

 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

 Areas for Contribution

- [ ] Additional specialty-specific extraction agents (oncology, cardiology, etc.)
- [ ] Alternative LLM provider implementations
- [ ] Additional test cases and benchmarks
- [ ] Translations for non-English clinical documentation
- [ ] Integration examples with EHR systems

 📚 Related Resources

 Research Papers
- [AgentClinic: Multimodal Agent Benchmark for Clinical Environments](https://agentclinic.github.io/)
- [MDAgents: Adaptive Collaboration of LLMs for Medical Decision-Making](https://arxiv.org/abs/2404.15155)

 Related Repositories
- [awesome-ai-system-prompts](https://github.com/dontriskit/awesome-ai-system-prompts) - General AI system prompts
- [agentic-system-prompts](https://github.com/tallesborges/agentic-system-prompts) - Coding agent prompts
- [MedLLMsPracticalGuide](https://github.com/AI-in-Health/MedLLMsPracticalGuide) - Medical LLM resources

 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

⚠️ Disclaimer

**This repository is for research and educational purposes only.**

- These prompts are NOT validated for clinical use
- They do NOT constitute medical advice
- They should NOT be used for actual patient care decisions without proper clinical validation and regulatory approval
- Always consult qualified healthcare professionals for medical decisions

 📬 Contact

- **Author**: Alaa Youssef
- **Email**: alaayoussef92@gmail.com
- **LinkedIn**: linkedin.com/in/alaa-youssef-5a610068
- **Twitter**:  @Alaa_Youssef92

---

<p align="center">
  <i>Built with patient safety in mind 🏥</i>
</p>
