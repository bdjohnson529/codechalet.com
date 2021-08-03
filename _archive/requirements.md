---
layout: post
title:  "Functional requirements"
parent: Product
parent_path: /tutorials/product/
---
Functional requirements improve communication between the engineering team and the product team. There are numerous ancillary benefits of documenting functional requirements. Below I have laid out a framework for functional requirements which can be used by teams building digital products of any sort. I advocate for the use of functional requirements on both software engineering and data science teams. 


1. **Begin with a user story.**
<br><br>The product exists for the user, and the ultimate motivation for any technical task should be its impact on the user. Any new software engineering features should improve the user experience. Data science projects should also seek to answer questions which will impact the user.
<br><br>It can be difficult to identify the user story for tasks removed from the user interface. While the user impact may not be immediately obvious, the backend infrastructure of your software does have a substantial, and measurable, impact on the user experience. For example, improving the speed of database queries will increase the page load time. Even documenting code will ultimately have a positive impact on the user experience, by empowering the development team to resolve bugs faster.

2. **Document the inputs and outputs, of each step.**
<br><br>Code often starts out as an MVP developed quickly to validate a solution. During the prototyping phase, functions change, files get moved around, and the overall structure is subject to change. Development code is usually messy.
<br><br>Once the solution has been validated, it is important to repackage the solution as a production code set. Production code should have ample documentation, and should be as streamlined as possible. Any steps which can be eliminated, should be eliminated. An effective way to identify, and streamline functionality, is to list the inputs and outputs of each step.

3. **Define acceptance criteria.**
<br><br>Acceptance criteria make the solution *measureable*. Acceptance criteria empower the engineering team to act with autonomy. Using the acceptance criteria rubric, the engineering team can make design decisions about *how* to implement the solution.

The greatest benefit of formalizing technical requirements is the communication which ensues between the product team and the engineering team. I have found the above framework to work on my team, but each team is unique. Simply establishing the habit of documenting technical requirements will yield tremendous benefits for any team.