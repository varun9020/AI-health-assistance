🐙 OctaMind
Multi-Agent Reasoning Framework for Parallel AI Intelligence
Build modular AI systems using isolated reasoning chains, collaborative aggregation, and developer-first architecture.

Python License Status AI

Overview
OctaMind is a lightweight Python framework built for collaborative AI reasoning.

Traditional AI workflows often depend on a single reasoning path. OctaMind approaches problems differently.

Instead of relying on one model response, the framework enables multiple isolated reasoning agents to analyze a problem independently and combine their outputs into a stronger final conclusion.

This design works especially well for:

Analytical reasoning
Multi-perspective decision systems
Complex decomposable tasks
High-confidence AI workflows
Why OctaMind?
Single-agent systems often suffer from early reasoning lock-in.

Typical flow:

Input
 ↓
Single Model
 ↓
Answer
OctaMind introduces isolated parallel reasoning:

Input
 ↓
Independent Expert Agents
 ↓
Consensus + Verification
 ↓
Final Response
Benefits:

Parallel reasoning
Reduced bias from single-path logic
Modular agent workflows
Better explainability
Traceable outputs
Flexible system design
Core Features
⚡ Parallel Execution
Run multiple reasoning agents simultaneously.

🧠 Independent Analysis
Agents operate in isolation to avoid reasoning contamination.

🤝 Consensus Aggregation
Final outputs are synthesized through dedicated aggregation logic.

🔍 Audit-Friendly Design
Reasoning trails remain transparent and reviewable.

🪶 Lightweight Framework
Minimal core dependencies and clean architecture.

🔧 Bring Your Own Model
Compatible with any LLM provider using callable interfaces.

Architecture
                    User Problem
                          │
                          ▼

               ┌────────────────────┐
               │      Engine        │
               └────────────────────┘
                    │     │     │

            ┌───────┘     │     └───────┐
            ▼             ▼             ▼

      ┌──────────┐  ┌──────────┐  ┌──────────┐
      │ Agent A  │  │ Agent B  │  │ Agent C  │
      └──────────┘  └──────────┘  └──────────┘

            ▼             ▼             ▼
                    Consensus Layer
                          │
                          ▼
                    Final Decision
Installation
Install directly:

pip install octamind
Or clone locally:

git clone YOUR_REPO_LINK
cd octamind
Create environment:

python -m venv venv
Activate:

Windows

venv\Scripts\activate
Linux / Mac

source venv/bin/activate
Install dependencies:

pip install -r requirements.txt
Bring Your Own LLM
OctaMind follows a provider-agnostic approach.

Any callable model function can be used.

Example:

import openai

client = openai.Client(api_key="YOUR_KEY")

def my_llm(prompt: str) -> str:
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[
            {
                "role": "user",
                "content": prompt
            }
        ]
    )

    return response.choices[0].message.content
Creating an Agent
Agents inherit from the base Agent class.

Example:

from octamind import Agent, tool

class LegalAgent(Agent):

    def __init__(self):

        super().__init__(
            role="Legal Analyst",
            goal="Identify contractual and liability risks",
            input_description="Business agreement",
            llm_callable=my_llm
        )

    @tool
    def compliance_check(self, text: str):

        """
        Analyze regulatory compliance.
        """

        return "Compliant"

    def execute(self, data: str):

        prompt = self._build_prompt(data)

        return self.llm_callable(prompt)
Creating an Aggregator
Aggregators combine independent reasoning outputs.

Example:

from octamind import Aggregator
from typing import Any

class ConsensusAggregator(Aggregator):

    def __init__(self):

        super().__init__(
            role="Consensus Builder",
            goal="Merge expert findings",
            llm_callable=my_llm
        )

    def execute(
        self,
        reports: dict[str, str]
    ) -> Any:

        formatted = self._format_reports(
            reports
        )

        prompt = f"""
        Reports:
        {formatted}

        Final conclusion:
        """

        return self.llm_callable(prompt)
Running the Engine
Launch collaborative reasoning:

from octamind import Engine

legal = LegalAgent()

engine = Engine(
    agents=[legal],
    aggregator=ConsensusAggregator()
)

result = engine.run(
    "Project investment analysis"
)

print(result.consensus)
print(result.traces)
Example Applications
OctaMind works especially well for:

⚖️ Legal Review
Risk and compliance analysis.

🩺 Medical Reasoning
Independent diagnostic perspectives.

💼 Business Strategy
Structured planning and evaluation.

📈 Financial Analysis
Multi-perspective investment reasoning.

🔬 Research Systems
Collaborative evidence synthesis.

Repository Structure
src/
├── engine/
├── agents/
├── aggregators/
├── demos/
├── tests/
└── docs/
Main modules:

Engine → Parallel execution
Agents → Domain specialists
Aggregators → Consensus logic
Demos → Examples
Docs → Documentation
Roadmap
Planned development:

 Agent marketplace
 Memory systems
 Tool ecosystem
 Visual workflow debugger
 Distributed execution
 Dashboard UI
License
OctaMind follows a Fair-Code model using:

Business Source License 1.1

Usage:

✅ Personal use
✅ Research
✅ Internal workflows

Restricted:

❌ Commercial hosted wrappers without license

Future transition:

This project is designed to transition toward Apache 2.0 according to licensing terms.

Contact
Questions, feedback, or collaboration:

📩 ganisettivarun8@gmail.com

Open an Issue for:

Bugs
Features
Technical discussions
⭐ Support the Project
If OctaMind helps your work, consider starring the repository.

Build smarter collaborative AI systems 🚀
