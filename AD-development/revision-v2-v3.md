# Revision from v2 to v3

This document describes the revision of this architectural description between versions 2 and 3.

## Issues to Address

A list of issues can be found in the [Summary of the Formal Feedback](feedback/evaluation-v2.md). These issues are further synthesized and sorted here in the following categories: Critical, Major, Minor, If time permits.

### Critical (C)

*Issues compromising the validity of the architectural description.*

1. **Structure of the AD:** The AD should have a clean and effective structure, which is not an artifact of its development into several milestones.
2. **Conciseness of the AD:** The current AD is too verbose and too narrative. This adds clutter to the text, and makes the relevant information more sparse.
3. **Terminology:** The terminology used in the AD is, in some places, inconsistent. Make sure the correct terms are used consistently across different documents.
4. **Keys and key exchange:** The discussion of keys is not self-contained, and hard to understand. It also misses relevant information on the key exchange, and how it relates to the functional components. We need to add a new section (with models) on the types of keys and the key exchange protocol.

### Major (MA)

*Issues for which the solution affects a large portion of the AD, and involves a large amount of time and effort to fix.*

1. **Apply the Evolution perspective:** Retrospectively use the Evolution perspective to improve the Information and Functional views.
2. **Consistent formatting:** Make the format of the views more consistent by using commonly agreed rules.
3. **Improve Context view:** Expand the Context view by exploring more in details the relevant external entities and their relationships with Signal Android.
4. **Data streaming concerns:** The Context and Functional views hint at data streaming (e.g., video calls) as a major feature of the application, but the Functional view does not allow the reader to understand it.
5. **Incomplete discussion of PAC style:** Improve the discussion of how the PAC style is used to organize activities, by describing the constraints and responsibilities of activities.
6. **Missing details in the functional scenario:** Improve the functional scenario by adding supporting models (e.g., a sequence diagram) and explaining how it relates to the information from the Information view.
7. **Definition of a session:** The term "session" is used for the keys, but it is unclear what it refers to: a message, a series of messages, etc. Clarify this definition and how keys are used.

### Minor (MI)

*Issues that are quick to solve, and don't affect a large portion of the AD.*

1. **Broken links:** Make sure there are no broken links in the documents.
2. **Measurability of the concern:** Describe how the concern can be measured, or rephrase it to be measurable.
3. **Colors in models:** Remove unnecessary use of colors in the models.
4. **Examples of jobs:** Add concrete example of jobs to improve the description of this concept.

### If Time Permits (ITP)

*Less important issues that probably will not get fixed.*

1. **Additional scenarios:** Streaming scenarios, expiring messages
2. **Additional details:** Unique identification of Signal users by (hashed) phone number

## Revision Plan

**Goal:** Solve all Critical (high priority) and Minor (low investment) issues, and most of the Major issues. If possible, solve some of the If Time Permits issues.

**Steps:**

1. [C1] Restructure the AD at surface level: organize the views into meaningful folders.
2. [C2, MA2] Establish a style guide to agree on common formatting and style rules to use across all documents.
3. [C2, C3] Review and rewrite the text of the existing files to (a) improve the conciseness of the text and (b) export all non-essential parts into a background file. Make sure to communicate with other members to agree on the correct terminology to use.
4. [MI1, MI2, MI3, MI4] Correct the minor issues of the views, and otherwise ensure the correctness of all other information presented in the views.
5. [C4] Work on a new Key Exchange section that will be tied to both the Information and Functional views. Make sure to correctly split the new information in their most relevant views, and keep the views self-contained, but keep the information consistent across views.
6. [MA3-7] Separately work on addressing the Major issues on each assigned part. Make sure to communicate with others for any change that may break consistency.
7. [MA1] Select a few major changes in the history of Signal Android, and apply the Evolution perspective from these changes. Keep track of the insights gained by the application of this perspective.

**Parts Assignment:**

- Mathieu: AD structure and first part of Functional view
- Duan: Context view and Evolution perspective
- Dong: second part of Functional view and key exchange
- Max: Information view, Key-exchange in Functional-view, Crypto-background in appendix
- Maksim: Information view and Evolution perspective

**Additional Notes:**

- To ensure consistency across views, discuss any decision that would apply to many parts with the GitHub issues.
