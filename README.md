# Awesome Agent Security [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Securing autonomous AI agents — configs, runtime, tools, MCP, and red-teaming.

A curated list of resources for securing AI **agents** specifically: the skills, plugins, MCP servers, hooks, and unattended loops that execute with your credentials. General LLM-safety lists are linked at the bottom; this one is about the agent attack surface — static config risks, runtime behavior, tool/MCP poisoning, and prompt injection.

*Prompt injection is the SQL injection of the agent era — #1 on the OWASP LLM Top 10, because it exploits the trust boundary between untrusted input and a tool-wielding agent.*

## Contents

- [Threat Models & Standards](#threat-models--standards)
- [Static & Config Scanning](#static--config-scanning)
- [Runtime Guardrails](#runtime-guardrails)
- [Red-Teaming & Testing](#red-teaming--testing)
- [Benchmarks & Evaluation](#benchmarks--evaluation)
- [Prompt Injection & Tool Poisoning](#prompt-injection--tool-poisoning)
- [MCP Security](#mcp-security)
- [Identity, Authorization & Access](#identity-authorization--access)
- [Agent Supply Chain & Provenance](#agent-supply-chain--provenance)
- [Operational Security](#operational-security)
- [Related Lists](#related-lists)
- [Contributing](#contributing)

---

## Threat Models & Standards

- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — The canonical risk taxonomy; prompt injection sits at #1.
- [OWASP Top 10 for Agentic Applications (ASI)](https://www.promptfoo.dev/docs/red-team/owasp-agentic-ai/) — Agent-specific risks: goal hijack, tool misuse, identity/privilege abuse.
- [MITRE ATLAS](https://atlas.mitre.org/) — Adversarial Threat Landscape for Artificial-Intelligence Systems; techniques and case studies for ML/LLM attacks.
- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — Voluntary framework for governing AI risk across the lifecycle; sections 4–6 map to agent-specific concerns.
- [NIST AI 100-2: Adversarial ML Taxonomy](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2023.pdf) — Formal taxonomy of attacks on ML systems including data poisoning, model evasion, and prompt-based attacks.
- [CISA Guidelines for Secure AI System Development](https://media.defense.gov/2023/Nov/27/2003346994/-1/-1/0/CSI-JOINT-GUIDELINES-FOR-SECURE-AI-SYSTEM-DEVELOPMENT.PDF) — Joint CISA/NSA/FBI/NCSC guidance covering design, development, deployment, and operation of AI systems.
- [Cloud Security Alliance AI Safety & Security](https://cloudsecurityalliance.org/research/working-groups/artificial-intelligence/) — CSA working group producing guidance on AI security governance, risk assessment, and controls.
- [ISO/IEC 42001:2023 — AI Management Systems](https://www.iso.org/standard/42001) — International standard for establishing, implementing, and improving an AI management system within organizations.

## Static & Config Scanning

- [agent-scan](https://github.com/snyk/agent-scan) — Scanner for MCP servers and AI agents: inventories installed components and flags injections, sensitive-data handling, and hidden payloads. Formerly Invariant Labs' mcp-scan; now maintained by Snyk.
- [Semgrep Guardian](https://semgrep.dev/products/semgrep-guardian/) — Real-time security for AI-written code: blocks malicious dependencies at install time, catches hardcoded API keys/credentials before commit, and flags insecure patterns the moment an AI coding agent writes them.
- [TruffleHog](https://github.com/trufflesecurity/trufflehog) — Secrets scanner with 800+ credential detectors — essential for agent repos that store cloud/LLM provider keys in config files.
- [detect-secrets](https://github.com/Yelp/detect-secrets) — Yelp's baseline-first approach to detecting secrets in code; useful as a pre-commit hook for agent config files.
- [zizmor](https://github.com/zizmorcore/zizmor) — Security linting for GitHub Actions workflows — agents that run in CI/CD often have overly permissive workflow permissions.

## Runtime Guardrails

- [NeMo Guardrails](https://github.com/NVIDIA-NeMo/Guardrails) — NVIDIA's toolkit for programmable rails between app code and the model: topic control, input/output filtering, and custom guardrail logic.
- [Guardrails AI](https://github.com/guardrails-ai/guardrails) — Input/output Guards backed by a Hub of composable validators; structured-output enforcement plus risk detection.
- [Lakera Guard](https://www.lakera.ai/lakera-guard) — API-based guard for prompt injection, jailbreak, and toxic content detection; lightweight enough for per-request agent guarding.
- [LangFuse](https://github.com/langfuse/langfuse) — Open-source LLM observability platform: trace every agent call, log tool invocations, and set up alerts on anomalous behavior.
- [Weave (Weights & Biases)](https://github.com/wandb/weave) — Observability and evaluation for LLM apps; tracks agent tool calls, traces, and evaluation metrics.
- [Helicone](https://github.com/Helicone/helicone) — Open-source LLM gateway with request logging, caching, and analytics; adds an audit trail to agent API calls.
- [Pangea AI Guard](https://pangea.cloud/ai-guard) — Managed API for content moderation, prompt injection detection, and PII filtering; drop-in for agent pipelines.
- [SandBase Harness](https://github.com/sandbaseai/sandbase-harness) — Local-first, self-hosted runtime for governed agent sessions with MCP tools, approval and credential controls, and audit/replay; sandbox isolation depends on the selected backend and deployment configuration.

## Red-Teaming & Testing

- [garak](https://github.com/NVIDIA/garak) — NVIDIA's LLM vulnerability scanner — nmap for language models; the widest range of attack probes.
- [PyRIT](https://github.com/microsoft/PyRIT) — Microsoft's Python Risk Identification Tool for proactively finding risks in generative-AI systems.
- [promptfoo](https://github.com/promptfoo/promptfoo) — Test/red-team harness with first-class CI/CD support and an agentic red-team suite.
- [HarmBench](https://github.com/centerforaisafety/HarmBench) — Standardized evaluation framework for assessing adversarial robustness across multiple harm categories.
- [TextAttack](https://github.com/QData/TextAttack) — NLP adversarial attack framework: generates adversarial examples via character-, word-, and sentence-level perturbations.
- [ART (Adversarial Robustness Toolbox)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) — IBM's Python toolbox for adversarial ML; attacks, defenses, and benchmarks across modalities.
- [Darkmoon](https://github.com/ASCIT31/Dark-Moon): Open source (GPLv3) autonomous penetration testing platform whose v1.4.0 llm specialist tests LLM and AI inference endpoints against the OWASP LLM Top 10 (prompt injection, system prompt leakage, insecure output handling, SSRF via the model, unbounded consumption), integrating NVIDIA garak, with reproducible proof of exploitation.

## Benchmarks & Evaluation

- [AgentDojo](https://github.com/ethz-spylab/agentdojo) — ETH Zurich's dynamic environment for evaluating prompt-injection attacks and defenses on tool-using agents across multiple task domains.
- [InjecAgent](https://github.com/uiuc-kang-lab/InjecAgent) — Benchmark for indirect prompt injection in tool-integrated agents: 1,054 cases spanning 17 user tools and 62 attacker tools.
- [SWE-bench](https://github.com/SWE-bench/SWE-bench) — Real-world software engineering tasks for evaluating agent coding ability; includes security-relevant bug-fix tasks.
- [CyberSecEval (Meta)](https://github.com/meta-llama/PurpleLlama/tree/main/CybersecurityBenchmarks) — Meta's benchmark evaluating LLMs on cybersecurity tasks: vulnerability identification, exploit generation, and malicious code detection.
- [ToolEmu](https://github.com/ryoungj/ToolEmu) — Framework for evaluating tool-use risks in LLM agents: simulates tool environments to test for injection, misuse, and hallucination.
- [AgentBench](https://github.com/THUDM/AgentBench) — Multi-dimensional benchmark evaluating LLMs as agents across diverse environments including web browsing and code execution.

## Prompt Injection & Tool Poisoning

- [mcp-injection-experiments](https://github.com/invariantlabs-ai/mcp-injection-experiments) — Reproducible proof-of-concept MCP tool-poisoning attacks — read these before you trust a tool description.
- [Simon Willison — prompt injection](https://simonwillison.net/tags/prompt-injection/) — The running field notes on prompt injection: why it's unsolved and what actually helps.
- [Indirect Prompt Injection on ChatGPT (Kai Greshake et al.)](https://arxiv.org/abs/2302.12173) — Foundational paper demonstrating that external data can inject instructions into LLM outputs — the core risk for RAG and tool-using agents.
- [Skeleton Key Attack (Microsoft)](https://www.microsoft.com/en-us/security/blog/2024/06/26/mitigating-skeleton-key-a-new-type-of-generative-ai-jailbreak-technique/) — Jailbreak technique that causes models to ignore all safety guardrails by appending a short suffix to user prompts.
- [ToolSword (Google DeepMind)](https://arxiv.org/abs/2404.02159) — Study of tool-use security in LLM agents: categorizes risks and proposes defenses against tool hijacking and injection.
- [Many-shot Jailbreaking (Anthropic)](https://www.anthropic.com/research/many-shot-jailbreaking) — Demonstrates that very long contexts can overwhelm safety training; relevant for agents that accumulate context across iterations.
- [Speck & Fowler — Crossing the Line](https://arxiv.org/abs/2406.04423) — Analysis of indirect prompt injection in code-generation agents that process untrusted file contents and web data.

## MCP Security

- [Model Context Protocol Specification](https://modelcontextprotocol.io/specification) — Official MCP spec; understanding transport, authorization, and capability-negotiation is prerequisite for securing MCP deployments.
- [MCP Security Best Practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices) — Official guidance on securing MCP servers: transport security, authorization, input validation, and sandboxing.
- [MCP Inspector](https://github.com/modelcontextprotocol/inspector) — Debugging tool for MCP servers; inspect tool definitions, permissions, and message flows before production deployment.
- [Claude Code — MCP Authorization](https://code.claude.com/docs/en/mcp) — How Claude Code handles MCP permissions: approval prompts, trust profiles, and tool-level authorization.

## Identity, Authorization & Access

- [Cerbos](https://github.com/cerbos/cerbos) — Policy-as-code, language-agnostic authorization; enforce fine-grained, context-aware access control on which tools an agent may call.
- [OpenFGA](https://github.com/openfga/openfga) — Open-source fine-grained authorization based on Google Zanzibar; model tool-call permissions as authorization relationships.
- [Ory Keto](https://github.com/ory/keto) — Ory's permission server implementing Google Zanzibar; suitable for deciding which tools/operations an agent can access.
- [SPIFFE/SPIRE](https://github.com/spiffe/spire) — Framework for service identity; agents running as services can use SPIFFE IDs for mutual TLS and workload attestation.
- [HashiCorp Vault](https://github.com/hashicorp/vault) — Secrets management with dynamic credentials; agents should never hold long-lived cloud credentials.

## Agent Supply Chain & Provenance

- [sigstore/cosign](https://github.com/sigstore/cosign) — Container and blob signing; sign agent container images and model artifacts for supply-chain integrity.
- [SLSA (Supply-chain Levels for Software Artifacts)](https://slsa.dev/) — Security framework for supply-chain integrity; applicable to agent containers, model weights, and tool packages.
- [in-toto](https://github.com/in-toto/in-toto) — Framework for ensuring software supply-chain integrity; define and verify layouts for agent deployment pipelines.
- [GUAC (Graph for Understanding Artifact Composition)](https://github.com/guacsec/guac) — Aggregates software security metadata (SBOMs, SLSA attestations, sigstore signatures) into a queryable graph.
- [Scorecard (OpenSSF)](https://github.com/ossf/scorecard) — Automated security checks for open-source projects; evaluate the security posture of MCP servers before adoption.

## Operational Security

- [Claude Code — Security Model](https://docs.anthropic.com/en/docs/claude-code/security) — How Claude Code handles permissions, sandboxing, and tool authorization — essential reading for Claude-based agents.
- [GitHub Copilot — Policies](https://docs.github.com/en/copilot/concepts/policies) — Enterprise governance for Copilot: which features, agents, and models your users can access, and how.
- [OpenTelemetry for LLMs](https://github.com/open-telemetry/opentelemetry-python-contrib/tree/main/instrumentation-genai) — Standardizes LLM observability across agent frameworks via the OpenTelemetry protocol.
- [Falco](https://github.com/falcosecurity/falco) — Cloud-native runtime security monitor; detect anomalous agent behavior (unexpected network calls, file access, process spawning) in real time.
- [Oso](https://github.com/osohq/oso) — Authorization library for building fine-grained access control; model agent permissions as declarative Polar policies.

## Related Lists

- [awesome-ai-security](https://github.com/ottosulin/awesome-ai-security) — Broad AI-security resource collection.
- [Awesome-LLMSecOps](https://github.com/wearetyomsmnv/Awesome-LLMSecOps) — LLM security operations: tooling, attacks, defenses.
- [awesome-agent-skills-security](https://github.com/LLMSecurity/awesome-agent-skills-security) — Focused on agent-skill security: attacks, defenses, benchmarks for tool use.
- [awesome-prompt-injection](https://github.com/Joe-B-Security/awesome-prompt-injection) — Comprehensive collection of prompt injection research, tools, and defenses.
- [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) — Curated list of LLM security tools, papers, and resources.
- [awesome-mcp](https://github.com/punkpeye/awesome-mcp-servers) — Curated list of MCP servers, clients, and tools.

## Contributing

PRs welcome — one entry per PR, with a one-line reason it belongs here. Must be agent-security specific (not generic infosec or generic ML). No dead links, no vendor pages without substance. See [CONTRIBUTING.md](CONTRIBUTING.md).

---

Maintained by [Adventure Wave Labs](https://github.com/adventurewave-labs).

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](LICENSE)
