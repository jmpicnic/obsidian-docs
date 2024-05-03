---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: true
title: Is my Supply Chain System Project Healthy?
---

{{ draftMark }}

As a manager or executive responsible for any non trivial Supply Chain system development or implementation project you are guaranteed to go through at least one *doom* episode where the project feels out of control, impossible to understand and hopelessly out of track. Rest assured that if the project could talk, it would tell you *It is not you, it is me*. Large projects are always challenging, and Supply Chain Systems projects are among the most challenging as they sit at the intersection of information, people and physical processes. A combination that very few other projects exhibit.

## What do Supply Chain Systems Projects Look like?

There are many definitions of system like the one in [Wikipedia](https://en.wikipedia.org/wiki/System)[@SystemWiki2024], my preference is to use the one from W. E. Deming[@demingNewEconomicsIndustry1997]. Slightly paraphrased it is:

> A system is a network of interdependent components that act together to accomplish a well defined outcome.

The outcome is what Deming calls *the aim of the system*. The *aim* is not part of the system, it is given externally and drives the design of the system itself.

The aim of Supply Chain Systems is to support the operations, people and assets that drive the movement of materials and goods both within facilities (warehouses, distribution centers, factories, ...) and between those and the final consumers. They also play a role in managing the commercial, legal and financial activities associated with those movements, including changes of custody, ownership and jurisdiction.

Originally, supply chain systems could be neatly classified into *Material Handling* and *Management Systems* projects. These two disciplines have since converged into systems that combine both. Traditional *Management Systems* [don't handle well the real-world, real time data feeds of Supply Chains](../erps-cannot-handle-supply-chains.md) and *Material Handling* systems are [incorporating logic that once belonged to management systems](../scac-system-fragmentation/article.md).

Sitting at the intersection of the worlds of information, people and the physical processes require integrating mechanical, hardware and software technologies, people, organizations and operational processes. The projects to design, implement and deploy these systems frequently require a much broader set of disciplines that other comparable systems with the associated risks of failure and difficulty to manage, control and oversee. Successfully executing these projects require a set of skills that is only available to very large companies or organizations specialized in these projects.

Most Operations Managers and Executives usually don't have access to the complete set of skills, either in themselves or in their staff to understand and evaluate all the aspects of these projects. It is little surprise that when these projects run into difficulties they feel under-equipped to respond to those difficulties effectively.

## What we mean by a Supply Chain System Project

### Project as a System itself

A project can itself be considered a *System* by the definition above with its components being its activities, resources and people and its aim the creation and deployment of a specific Supply Chain System.

Looking at these projects as systems, we quickly can identify four *interdependent components* for it:

Goal Definition
: Activities, documents and knowledge that define what the *aim* of the target Supply System will be and how to know when it is ready.

People
: The staff, with their motivations, skills and interactions, that will execute the project together with the organizational structure that organizes them. People must include not only the technical staff designing and implementing the system, but also stakeholders, intended users and maintainers of the system, business sponsors, etc...

Process
: The set of practices and rules that govern the interaction of people and define deliverables, oversight and decision criteria to be used in the project.

Technology
: Tools and pre-existing capabilities that will be used in the execution of the project. The word *Technology* is sometimes associated exclusively with *Information Technology* or software. Supply Chain systems involve physical systems and people. *Technology* in this context is meant to include mechanical and electrical components in addition to the common elements of databases, networks, user interfaces, etc...

Although given in the definition of *System*, it is worth emphasizing that these *Components* of the project are **interdependent** and although distinct from each other, they cannot be considered in isolation from one another.

There is plenty of books and articles that provide guidance for how to deal with each of these components including requirements management, high performance teams/organizations, project management and specific technologies, etc... When applying them to a particular project, they need to be adapted and tuned to work together. No two projects are the same. Like any other system, the project itself needs to be designed, operated and monitored. It is the responsibility of the project leadership to ensure that it is done in an integrated way and with the highest possible professional standards.

### And then everything changes

It would be an error to think that a project as a system can be defined and implemented at the beginning and expect that it will remain unchanged during its lifetime. Staff changes, requirements evolve due to business changes or learning by the team, technology changes with ever increasing pace and processes need to adapt and follow a *continuous improvement* discipline.

Part of the project design itself must be to choose how these changes will be identified and how the project will adapt to them. As an example, at this time it is a truism that any technology chosen for a project is obsolete the moment the project starts. At the same time a project that constantly tried to keep up with any new applicable technology would never make any progress towards its goal. A well designed project will have a clear way to evaluate technology changes and make decisions on whether and how to incorporate them. Similarly, a well designed project will have defined succession plans for key staff positions and skills to minimize the impact of the inevitable personnel changes.

Without getting into specifics of how change management needs to be incorporated in a project, it is still important to note it is an essential part of a well designed project.

## Identifying Project Failures

The practices, tools and mechanisms to monitor a project are often not given enough attention. Similarly to how it would be unthinkable to deploy a complex industrial system without robust, well design sensors, monitors and alert systems, a project design needs to include equivalent monitoring capabilities to detect potential failures and deviations from expected operation as early as possible.

Too frequently these elements are considered mostly an *accountability* mechanism for project management. Nobody would think of blaming a boiler if the pressure gauge shows unexpected changes. Instead, it is read as information to make decisions on how to change the operation of the boiler, reduce the power applied, vent pressure, etc. Similarly project monitoring should focus on identifying and reporting signals for decision making and to be reviewed in a *safe* environment to ensure that information is transparently available across the project and diligently acted on.

A definition of *failure* useful in many fields is a variation of *[...] when a system does not do what it is supposed to do [...]*[@SystemsSystemsFailure2009;@berkSystemsFailureAnalysis2009]. Hidden in this definition is the assumption that what a system *is supposed to do* is well defined and can be measured in a reliable way.

Treating projects as systems themselves helps bring them close to fulfill that assumption by requiring that an *aim* or goal of the target system is defined, yet it is usually not enough.

The goals of the system to be developed may (even unconsciously) incorrectly substitute for the goals of the project, leading to a mis-identification of real failures of the project and fatal delays in detection because the behavior of the system can only be assessed once it is at least partially built. To avoid this problem, the best practice is to  have explicit statements of goals for the project itself and define associated monitors and reports.

The traditional definition also assumes that the system itself and the environment in which it operates do not change much. This is a reasonable assumption for systems that are *built* and then *operated*. For Projects, both themselves and the environment in which they operate are much more variable and uncertain. The definition of Failure needs to include how the system, in this case the project, copes with this uncertainty and change. A deviation of the initial parameters of the project like time or budget may or may not represent a real failure of the project depending on what changes have taken place since the reference parameters were defined. The definition of failure conditions need to:

1. Be revised at a defined frequency or when certain changes happen in the project.
2. Incorporate logic about how long a condition is present (e.g. a projected delay) before it is considered a failure, giving the project regular operation an opportunity to *self-correct*

Finally, following the emphasis that Dr. Deming makes on *Method* vs *Results*[@demingNewEconomicsIndustry1997], monitoring and detection of failures need to include deviations of prescribed processes, even above deviations of expected results. The action to take when a deviation is detected can be changes to the project operations (add resources, change the order of activities, re-balance workloads, ...) and may also require to changes to the design of the project itself (People, Process, Technology) including its monitoring mechanisms and failure criteria.

This last statement is the foundation of building a *learning* culture in the project and the best tool to deal with the high uncertainty and variability that these projects encounter.

## How Failures Happen

Viewing Projects as systems themselves helps in identifying how failures can happen in a project and what kinds of failures to look for.

Failures in systems may arise in three ways:

1. A mismatch between the capabilities of the system and the environment, including the definition of its *aim* or goal. This mismatch may appear if the environment changes or it presents conditions that were not originally foreseen in the design of the system. This is the common occurrence of *edge cases*. Conditions that are rare, difficult to predict or specify that are frequently missed in the initial specification of a system.
2. Issues in the interaction between the components of the system. Even in the case that each component operates within its design parameters, the interaction between them may lead to system failures. Similar to the first point, these failures occur at the boundaries of the specification of the components involved, maybe in how they react to an exceptional condition or configurations that appear after a long sequence of complex state changes.
3. Internal Component Failures when a component starts behaving outside of its expected operation.

Projects experience these kinds of failures. As an example of the first type, a project may rely on the availability of certain number of engineers or skilled installers, which may not be possible if the labor market is very tight in the area or the hiring process cannot scale to make them available in the right time frame. A technology may be a good match for a project, and staffing may be adequate. A mismatch in the training or expertise on that particular technology will appear as an inter-component failure.

This classification helps project leadership be systematic in defining and designing the project and also provides guidelines for how to handle them. For the first kind of failure, the reaction may be a change to the project goals to incorporate a changing environment or previously missed details, or it can be exerting more control over the environment itself, e.g. implementing a triage process to review any changes to requirements from stakeholders.

### Inter-Component Failures

In a project, mismatched choices among its components are the source of failures that are difficult to identify and diagnose when they appear, and doubly difficult to correct because of the large number and scope of changes that fixing them require.

The most obvious coupling is that of Technology choices to the Goal of the project. After all, this is one of the main outcomes of the design of the target system. Despite this, many projects don't make that connection explicit. Not tying them explicitly effectively discards design information that is later needed when evaluating changes to the target system, as it is not clear why a technology may have been chosen and what capabilities are important to preserve vs. which ones are ancillary. Even more harmful is the effect of adopting a technology that afterwards is used in an unintended way introducing couplings and constraints in the system that make its maintenance more difficult and expensive. As an example, the choice of a relational database as an storage technology for the operational system, if unconstrained may open the door to create custom reports from it, which make it very hard to upgrade the database or change its schema later.

Technology choices are also heavily influenced by the People component in the project. The skills, training and experience of the available staff may be the overriding factor in these decisions to the point that they may not even be considered as decision points at all. In many cases this is justified. Even in these cases the responsible approach is to document the decision. By documenting it, the decision becomes explicit and therefore subject to review later which again enables learning in the project and organization. It also helps separate the cases where it is justified from others that may be less clear. The interaction between choice of technologies and people can be expressed as a tradeoff between choosing the best fit technology and the cost, time and disruption that upgrading the team would require through a combination of hiring, training and replacements.

Project leadership needs to ensure and maintain close alignment of the *People* to the *Goal* of the project. Clearly this needs to start with a clear vision and communication of the goal, but it also works the other way around. The goal needs to be influenced by the skills, availability and motivations of the people in the project. In some cases, these considerations may be unavoidable as when union contracts are involved, in other cases they may be more subtle but not less important. It would be unwise to try to staff a national defense project with pacifists and vice-versa, accept such a project if your workforce is already composed of pacifists. This may feel *fluffy* when compared to hard engineering choices, but we have seen in the news repeated cases of employee activism tying projects to political positions in areas like privacy, animal rights, etc. Without judging the merits of these positions, responsible project leadership needs to ensure strong and sincere alignment of the people to the goals of the project for it to be successful. Alignment and engagement must also be continuously monitored and reinforced in the presence of changes in the staffing of the project, their internal motivations and attitudes or the goals themselves.

Processes and People interactions are determined by the culture of the team and how the processes leverage that culture. The processes that are effective in a military organization where chain-of-command is central to the culture of the group are very different than those that will work in an academic setting where each professor is their own boss.

The processes that a project can adopt are also influenced by the technologies that will be used. Technologies may impose constraints on the sequence of tasks or activities effectively precluding some forms of agile methodologies that rely on an assumption of mostly independent small *stories* that can be performed in almost any order. Technology choices may also introduce hidden couplings of activities that require specific reviews or communication between teams in ways that are easy to miss. The design of the layout of a warehouse may depend on the fire suppression technology chosen, requiring or not communication with the rack layout design.

Finally the interaction between the choice of processes for a project and the project's goal is determined by the balance of uncertainty and risk that the project can tolerate. As indicated in the figure below, for low risk, low uncertainty projects, traditional project management processes work well and usually deliver the most predictable and efficient outcomes, unfortunately these situations rarely occur in non trivial projects. When uncertainty grows, but the impact of failures can be easily absorbed or corrected, agile or iterative processes are effective at the cost of potential need for re-work (refactoring in software) or backtrack of partial results. If the uncertainty stays moderate but the risks are higher, a *Thin-Thread* approach where one or several *thin-threads* of the system that span the goal end-to-end  the system is built around a core that spans the project end-to-end and act as the guides to build the rest of the system around it. The name is taken from the technique of spinning the main cables of suspension bridges in-place over a pilot wire[@SpinningMainCables]. When both Risk and Uncertainty are high the project needs to foresee building multiple prototypes and test models as it is done in space programs for new vehicle or mission designs.

![Risk-Uncertainty Processes](assets/risk-uncertainty-matrix.drawio.png){: width=70%}

### Component Failures

Each of the components of the project can also experience its own specific failures

#### Goal Definition Failures

Failures in the definition fo the Goal (Requirements) of the target system have the highest impact on the result of the project. It is well known that somewhere around 80% of costs and risks of engineering projects are baked in during the definition and early conceptual design steps, when a full project organization may not even be in place. Failures in requirements definition arise when the scope of the project is vague or does not have a clear boundary. This can be because the full extent of the operations that the target system needs to support is not well known to the requirements team or because it is so well known that it is part of the background knowledge and not documented. In either case the result is ambiguity on what the target system needs to perform resulting in scope creep, cost overruns and delays. Well structured and clearly documented requirements reflect the Supply Chain processes and activities that the target system must support. Goal definition will fail if these processes and activities themselves are not mature and change frequently no matter how thoroughly requirements are collected and documented at a point in time. Attempting to mechanize or automate processes that themselves are not mature increases the risk to the project enormously. The project can still mitigate this risk by explicitly adding goals and requirements on flexibility and adaptability of the target system, but these requirements usually require very high project effort to incorporate configurability, extensibility, etc. which are difficult to estimate and frequently ignored.

Requirements Capture and management are very difficult activities that require highly sophisticated skills in both the domain (Supply Chain processes) and all components of development projects as described in this article. On top of this, documenting these requirements in an articulate and clear way requires strong communication skills. When an organization does not have individuals or teams that have this synthesis of skills, the result is incomplete or ambiguous requirements, particularly specifying the expected behaviors of the system in edge cases or in the presence of errors or anomalous conditions. Given the difficulty of this task and the scarcity of talent that can perform at the level of integration required, projects need to ensure that the requirements process is not a *one and done* effort at the beginning of the project but rather embedded along its whole lifetime and that those responsible for requirements are in constant interaction with stakeholders and the technical team as catalysts of learning and to ensure that the project reacts quickly to any changes.

The requirements that capture the goal of the target system are frequently described in terms of functionality or behavior at a reasonably high level to be able to cover the scope of the system. This leaves room for ambiguity about how to determine whether a particular requirement is met or not by the system. Defining the Goal of the target system is not complete unless there are clear *acceptance criteria* for all requirements that can be verified objectively with a minimum of interpretation. In the ideal case, acceptance criteria map directly to tests that can be performed on the target system with a clear yes/no result and possibly using automated test harnesses and drivers.

#### People & Organization Failures

Despite the label, People failures are rarely attributable to individuals but rather to the difficulty of finding the right match of talent to the needs of the project or to divergent motivations with respect to the goal of the project. They may arise when the staff contributing to the project either don't have the skills needed or their motivation does not support the effort the project requires. From the point of view of the project, skills can be hired or they can be trained. A project failure is to gloss over gaps of skills and *hope* that staff will pick them up *on-the-job*. Motivation is the result of a sense of shared ownership of the project and an alignment of the goals of the project with the incentives offered to staff members (from compensation to career progress or other intrinsic motivations) and values. A strong *mission alignment* results when all three point in the same direction. While it is very difficult to have perfect alignment, project leadership can make a significant difference by simply considering these aspects and being open in their communication with the staff.

At an organizational level, it goes without saying that not providing adequate resources invites failure. Beyond that an organization structure that promotes short and open lines of communication and reporting and has clear sponsorship from senior management will minimize chances of failure and recover faster when they happen.

A critical aspect of People and Organization that needs to be given as much attention as any critical activity is implementing a comprehensive change management plan to educate staff and stakeholders and minimize the negative impacts that the project will have even if completely successful. All projects are undertaken with the goal to effect change in some aspect of an operation. These changes will inevitably result in some changes that are negative to stakeholders. They may result in loss of specific jobs, geographic displacements, obsolescence of certain skills and requirements to acquire new skills. If the project does not address these negative impacts effectively it will face active and passive resistance that could lead to failure with extreme cases resulting even in active sabotage of equipment or willful neglect of maintenance or operating procedures that may result in down time, or damage to equipment or data.

#### Process Failures

A lot of attention has been devoted to project management methodologies, processes and practices with different recommendations to improve the chances of success. Trying to summarize the process aspects, in our view, fall in four distinct areas, strongly influenced by the CMM model[@CapabilityMaturityModel2023]:

- Requirements Management which is addressed extensively as part of the [Goal Definition Component](#goal-definition-failures).
- Task Execution that includes all aspects of managing the specific tasks that need to be performed as part of the project.
- Quality Assurance dealing with the verification of both the results of the project as well as the adherence of the tasks to best practices and project standards.
- Release Management to clearly identify and manage the deliverables for the project, including labeling, versioning and inventorizing them.



#### Technology Failures

## Avoiding Surprises

### Nuts-to-Bolts Project Evaluation

### Continuous Project Oversight

## Wrapping up

## References

\bibliography