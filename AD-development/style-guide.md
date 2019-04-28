# Documentation Style

- ```Code Artifact/ any file in the source code```. Can be combined with a link to the source code on GitHub.

- *Citing*  

- *italic* and ***bold + italic*** can be showed to show something that is important. However, the use of bold and italic should be minimized.
  - *Something fundamentally important*  

  - ***Something fundamentally important***  

- Model diagram, tables, list with occasionally a small note in *italics* to indicate anything major, the legend, etc.


- Description of the model elements, as a list, with the name of each element in **bold**, followed by a small text (3-4 lines).

- Table with links to the implementation of the elements.

- Max 2-3 sentence for model introduction. This should be self-evident from the headers and the model themselves.

- Use First Capital Letter for component/ entity name. Do not use **bold**/ *italic*.

  Exception: according to rule 2, you can use **bold** in the model description, but just for the component being described/ introduced, do not use **bold** for component that is just mentioned in a random paragraph or description for an another component.

  Only use **bold** when the component is first defined.

  E.g.
  >- **User Interface:** The User Interface is controlled by the Android Framework, based on XML files to indicate what to display to the user. It sends the user events to the Conversation Controller, and updates the information displayed to the user.
  >- **Conversation Controller:** The Conversation Controller indicates to the Key Generator to prepare keys when a new conversation is selected, prepares the message that needs to be sent (formatting it and wrapping it with metadata), and saves it to the local database. It updates the User Interface with the status information of the message.


- Links to other resources.
  - Add a link for:
    - Code elements
    - Concepts not defined, e.g., E2EE, Forward secrecy, etc.
    - References to support a point
  - When choosing the target for a link, select either:
    - a link to the current version of a Signal Android file/folder in GitHub
    - a link to an official reference (e.g., Android API)
    - a link to a Wikipedia page (for general concepts being referenced)
    - a link to a file/section in our background folder
    - (try not to use this one too much) a link to another view
    - In particular, avoid links to blogs or other informal resources.
    - Also, avoid links that serve no real purpose (e.g., for a concept already defined, or already linked).

  - Try to be concise, avoid meaningless sentence like "It's important that ...", "We have to keep in mind that ...". To the best of your capacity, avoid (in order of importance)
    - Sentence clauses that capture no information ("It's important that ..."). If you can cut a part of the sentence, and it's still logically valid, do it.
    - Passive voice
    - 1st person pronouns ("we did ..."). When doing so, don't just replace it with a passive voice! Try to describe the factual information, rather than the process.

  - Try to avoid casual language and being narrative. This includes abbreviations ("app", ...) and niche jargon words.

  - No use of colors.
