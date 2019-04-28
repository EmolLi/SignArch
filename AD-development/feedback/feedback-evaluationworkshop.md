# Feedback Received during the Evaluation Workshop (workshop 7)

**Evaluators:**

- Will
- Bao
- Howie

## Overview

**Points for Improvement:**

- There is some redundancy between the views.

## Context View

**Questions:**

- How to find which user to send to?
  - A: Each user is identified with its phone number.
- How good is the quality of the video? Is there a way to measure it?
- How much data gets stored?

## Functional View

**Questions:**

- Why is the job layer excluded from the scenario?
- What does it mean to have nested components inside the Activity component?
- How does data flow up from the bottom layers to the activities (e.g., to show the content of a message)?

**Points for Improvement:**

- You can give some concrete examples of jobs.
- You can include another scenario for video calls.
- At first, it's not obvious what GUI/Hardware means (GUI and file system together is weird).
- You can split the overview functional diagram, to make it less intimidating.

## Information View

**Questions:**

- How is the session key used? Is there one session key per message sent?
- How does the disappearing messages feature work? How is it handled by Signal? Is it different from other applications like Snapchat?

**Points for Improvement:**

- The Information view should not just focus on how data is encrypted. It should include other elements as well.
- You can improve the explanation of what is a session.