## Requirement: model right-sizing with safe escalation

The system should route each task to the smallest adequate model by default.

Smaller/cheaper/local models should handle:
- capture
- formatting
- summarization
- classification
- simple transformations

They must not guess beyond their capability.

If a task exceeds capability, the agent must:
- stop
- recommend escalation

Escalation triggers:
- unclear or conflicting instructions
- missing context
- low confidence
- high-risk or irreversible changes
- need for synthesis, planning, or judgment

Escalation output:

Escalation recommended  
Reason:  
Required capability:  
Suggested next step:  

Stronger models handle:
- planning
- synthesis
- architecture
- critical review
- final decisions
