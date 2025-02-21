## SSL Orchestrator Policies

${\large{\textbf{\textsf{\color{red}Definition}}}}$

A **Policy** is a set of rules that match traffic patterns. When a rule condition is matched, it assigns a set of actions to the matching flow. A single SSL Orchestrator policy applied to an application can contain multiple "rulesets", including a traffic ruleset, logging ruleset, and potentially other types. All of the different rulesets will have similar traffic condition options, but take different actions. For example, the traffic ruleset can take the following actions:

* Allowing or resetting the traffic
* Intercepting (decrypting) or bypassing decryption
* Assigning the flow to a service chain of inspection services
