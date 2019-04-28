# Summary of the Formal Feedback

This document synthesizes the formal feedback received from:

- [Evaluation of Milestone 1](feedback-v1.txt)
- [Presentation of February 27](feedback-presentation2019-02-27.txt)
- [Evaluation Workshop following Milestone 2](feedback-evaluationworkshop.md)
- [Evaluation of Milestone 2](feedback-v2.md)

## General

- **Issue**: Non unique formatting

  **Mitigation**: Create a style guide for the whole AD

- **Issue**: References to other milestones

  **Mitigation**: Reference artifacts rather than milestones

- **Issue**: Broken links
  
  **Mitigation**: Check and fix. Be careful when restructuring the folders.

- **Issue**: Views are not concise enough

  **Mitigation**: Use a less narrative style. Remove any phrases that do not contribute hard facts. Try to apply "less is more" when refactoring text. Bring things to the point fast, say thing explicitly instead of giving examples. Avoid sayings like "It is very important to know that XYZ", just mention "XYZ". Reduce discussions of the process or AD decisions to a minimum, or remove.

## Context View

- **Issue**: Context could be explored more in details

  **Mitigation**: Expand the context view, and discuss more the role of external entities.

- **Issue**: The concern isn't clearly measurable.

  **Mitigation**: Discuss how to measure the concern.

- **Additional Information**: 
  - How to find which user to send a message to?
  - How good is the video quality?
  - How much data gets stored?

## Functional View

- **Issue**: Data streaming (e.g., calls) is hinted but not explained by the view

  **Mitigation**: Clearly indicate that streaming is outside the scope of this view, and why?

- **Issue**: Imprecise terminology ("component" vs "module", "layer" vs "interface", "UI" component in the system layer, etc.)

  **Mitigation**: Use consistent terms to refer to the same elements, and make sure the definition is correct.

- **Issue**: PAC style is covered too briefly, and doesn't include the responsibilities and constraints of the style.

  **Mitigation**: Decouple the discussion of Android Framework from the discussion of the style, and expand on the latter.

- **Issue**: Background knowledge should be extracted away from the view.

  **Mitigation**: Create new file for background concepts.

- **Issue**: Scenario is hard to fully grasp.

  **Mitigation**: Add a sequence diagram.

- **Issue**: The key exchange is referred to, but not described.

  **Mitigation**: Add a section to describe the key exchange.

- **Issue**: Sub-optimal structure (the main model comes too late, is intimidating, etc.)

  **Mitigation**: Restructure the view, minimizing to forward references and always introducing a concept before referring to it.

- **Issue:**  Colors in models is extraneous information.

  **Mitigation:** Find other ways to convey the same information.

- **Additional Information**:
  - How do activities integrate with the rest of the system?
  - How does the handshake protocol work?
  - What are some examples of jobs?
  - How does streaming work?

## Information View

- **Issue**: Background knowledge should be extracted away from the view.

  **Mitigation**: Create new file for background concepts.

- **Issue**: Symmetric and asymmetric keys are not explained enough to understand their purpose.

  **Mitigation**: Make a section to explain the different kind of keys and their purpose.

- **Issue:** ER diagram is not clear enough

  **Mitigation**: Explain it in more details, and rework the abstractions.

- **Issue**: Mapping to existing code artifacts should not be a bullet list

  **Mitigation**: Convert to a table, and map to their functional components.

- **Issue**: Information view only discusses encryption/decryption.

  **Mitigation**: Include other relevant handling of data, if any.

- **Issue**: Sub-optimal structure (hidden design decisions/architecture principles, etc.)

  **Mitigation**: Restructure the view, outlining the design decisions and principles behind them.

- **Issue**: Unclear definition of a session.

  **Mitigation**: Clarify what a session is.

- **Additional Information**:
  - How does the disappearing message feature work?
