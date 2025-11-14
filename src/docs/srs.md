# Software Requirements Specification

<!--Use the template and make it into a markup file (or copy an existing one from another project). (Do not change table of content)-->
<!--Proof of version control (GIT, or by hand on second page)-->
<!--Blue text has been replaced with actual information regarding project.-->
<!--Items that are not relevant have been maintained but contain the comment: not applicable (n/a)-->
<!--Items that you don’t know yet have been marked with: to be determined (tbd)-->
<!--SRS contains the overall Use Case Diagram (UCD) – which should be correct (ie. system boundary, associations ... etc.) (( If you embed the diagram from a cloud document, any changes to the original picture will propagate automatically to the md file without you having to make sure  the documentation is up to date! This is how you should do it))-->

For the game jAilbreak

---

## Table of Contents

- [1. Introduction](#1-introduction)
  - [1.1 Purpose](#11-purpose)
  - [1.2 Scope](#12-scope)
  - [1.3 Definitions, Acronyms and Abbreviations](#13-definitions-acronyms-and-abbreviations)
  - [1.4 References](#14-references)
  - [1.5 Overview](#15-overview)
- [2. Overall Description](#2-overall-description)
- [3. Specific Requirements](#3-specific-requirements)
  - [3.1 Functionality](#31-functionality)
  - [3.2 Usability](#32-usability)
  - [3.3 Reliability](#33-reliability)
  - [3.4 Performance](#34-performance)
  - [3.5 Supportability](#35-supportability)
  - [3.6 Design Constraints](#36-design-constraints)
  - [3.7 Online User Documentation and Help System Requirements](#37-online-user-documentation-and-help-system-requirements)
  - [3.8 Purchased Components](#38-purchased-components)
  - [3.9 Interfaces](#39-interfaces)
    - [3.9.1 User Interfaces](#391-user-interfaces)
    - [3.9.2 Hardware Interfaces](#392-hardware-interfaces)
    - [3.9.3 Software Interfaces](#393-software-interfaces)
    - [3.9.4 Communications Interfaces](#394-communications-interfaces)
  - [3.10 Licensing Requirements](#310-licensing-requirements)
  - [3.11 Legal, Copyright, and Other Notices](#311-legal-copyright-and-other-notices)
  - [3.12 Applicable Standards](#312-applicable-standards)
- [4. Supporting Information](#4-supporting-information)

---

# 1. Introduction

<!--The introduction of the Software Requirements Specification (SRS) should provide an overview of the entire SRS. It should include the purpose, scope, definitions, acronyms, abbreviations, references, and overview of the SRS._-->

<!--Note: The SRS captures the complete software requirements for the system, or a portion of the system. Following is a typical SRS outline for a project using only traditional natural-language style requirements - with no use-case modeling. It captures all requirements in a single document, with applicable sections inserted from the Supplementary Specifications (which would no longer be needed). For a template of an SRS using use-case modeling, which consists of a package containing Use-Cases of the use-case model and applicable supplementary specifications and other supporting information, see rup_SRS-uc.dot._-->

<!--Many different arrangements of an SRS are possible. Refer to [IEEE830-1998] for further elaboration of these explanations, as well as other options for SRS organization._-->

## 1.1 Purpose

<!--Specify the purpose of this SRS. The SRS should fully describe the external behavior of the application or subsystem identified. It also describes nonfunctional requirements, design constraints and other factors necessary to provide a complete and comprehensive description of the requirements for the software._-->

{{#include project-description.md:desc}}

## 1.2 Scope

<!--A brief description of the software application that the SRS applies to; the feature or other subsystem grouping; what Use-Case model(s) it is associated with; and anything else that is affected or influenced by this document._-->

This specification defines the entirety of the jAilbreak project, in particular the features listed under the "*Use cases*" chapter
[![Use case diagram](./../assets/use-case-diagram.svg)](./use-cases/)

## 1.3 Definitions, Acronyms and Abbreviations

<!--This subsection should provide the definitions of all terms, acronyms, and abbreviations required to properly interpret the SRS. This information may be provided by reference to the project Glossary._-->


|Word|Meaning|
|-|-|
|AWS|Amazon Web Services|
|LLM|Large Language Model|


## 1.4 References

[UC-Overview]: ./use-cases/
[UC-AI-Chat]: ./use-cases/ai-chat.md
[UC-Level-Progression]: ./use-cases/level-progression.md
[UC-Level-Selection]: ./use-cases/level-selection.md

- [UC-Overview]
- [UC-AI-Chat]
- [UC-Level-Progression]
- [UC-Level-Selection]

## 1.5 Overview

<!--This subsection should describe what the rest of the SRS contains and explain how the document is organized._-->

The following chapters elaborate on project considerations and requirements

---

# 2. Overall Description

<!--This section of the SRS should describe the general factors that affect the product and its requirements. This section does not state specific requirements. Instead, it provides a background for those requirements, which are defined in detail in Section 3, and makes them easier to understand. Include such items as:_-->
<!--- product perspective-->
<!--- product functions-->
<!--- user characteristics-->
<!--- constraints-->
<!--- assumptions and dependencies-->
<!--- requirements subsets-->

## Product perspective
We aim to sharpen the prompt engineering skills of players, in a puzzle-like fun manner.
It is to be percieved as a game, and thereby should by enjoyable.

## Product functions
The product shall fulfill the use cases displayed in [UC-Overview], which are specified under the "*Use cases*" chapter

## User characteristics
Our players are people, that are enthusiastic about AI, Technology and hacking of systems in a safe environment.

## Constraints
The cost of running the project shall remain low,
especially costs involving AI model usage,
since players will send lots of prompt to the AI models in order to obtain the password.

---

# 3. Specific Requirements

<!--This section of the SRS should contain all the software requirements to a level of detail sufficient to enable designers to design a system to satisfy those requirements, and testers to test that the system satisfies those requirements. When using use-case modeling, these requirements are captured in the Use-Cases and the applicable supplementary specifications. If use-case modeling is not used, the outline for supplementary specifications may be inserted directly into this section, as shown below._-->

## 3.1 Functionality

<!--This section describes the functional requirements of the system for those requirements which are expressed in the natural language style. For many applications, this may constitute the bulk of the SRS Package and thought should be given to the organization of this section. This section is typically organized by feature, but alternative organization methods may also be appropriate, for example, organization by user or organization by subsystem. Functional requirements may include feature sets, capabilities, and security._-->

<!--Where application development tools, such as requirements tools, modeling tools, etc., are employed to capture the functionality, this section document will refer to the availability of that data, indicating the location and name of the tool that is used to capture the data._-->

<!--The requirement description._-->

### AI gatekeeper conversations
See [UC-AI-Chat] for specifics

### Level progression
See [UC-Level-Progression] for specifics

### Level selection
See [UC-Level-Selection] for specifics

## 3.2 Usability

<!--This section should include all of those requirements that affect usability. For example, specify the required training time for a normal users and a power user to become productive at particular operations; specify measurable task times for typical tasks or base the new system's usability requirements on other systems that the users know and like; specify requirement to conform to common usability standards, such as IBM's CUA standards or Microsoft's GUI standards._-->

### Web frontend
The game shall be playable from a publicly accessible website.
This approach does not require players to download an application to their computer,
improving the overall convenience of obtaining and playing the game.

### Ease of registration
While creation of an account is necessary to prevent abuse of the game,
this process shall be made as easy as possible.
A user should only have to provide a valid e-mail address, a name and password.
Phone number or credit card verification is not desired.

## 3.3 Reliability

<!--Requirements for reliability of the system should be specified here. Some suggestions follow:_-->
<!--- Availability — specify the percentage of time available (xx.xx%), hours of use, maintenance access, degraded mode operations, etc.-->
<!--- Mean Time Between Failures (MTBF) — usually specified in hours, but could be in days, months or years.-->
<!--- Mean Time To Repair (MTTR) — how long is the system allowed to be out of operation after it has failed?-->
<!--- Accuracy — specify precision (resolution) and accuracy that is required in the system's output.-->
<!--- Maximum Bugs or Defect Rate — usually expressed in terms of bugs per thousand lines of code (bugs/KLOC) or bugs per function-point.-->
<!--- Bugs or Defect Rate — categorized by severity: minor, significant, critical. The requirements must define what is meant by "critical" (e.g., complete loss of data or complete inability to use part of the system).-->

### Availability
To ensure a 99.99% availability of the game at all times,
a cloud provider shall be used for deploying the application.
Manually achieving close to perfect uptime across geographic regions is very difficult.

### Response speed
For the enjoyability of the game, it is essential to keep time waiting for AI responses to a minimum.
Responses to player prompts shall be generated and displayed in less than two seconds on average.

### Absence of bugs
To minimize critical issues,
the backend shall be written in a language,
which by design reduces the attack surface for mishaps.

## 3.4 Performance

<!--The system's performance characteristics should be outlined in this section. Include specific response times. Where applicable, reference related Use Cases by name._-->
<!--- Response time for a transaction (average, maximum)-->
<!--- Throughput (e.g., transactions per second)-->
<!--- Capacity (e.g., number of customers or transactions the system can accommodate)-->
<!--- Degradation modes (acceptable operation mode when system is degraded)-->
<!--- Resource utilization (memory, disk, communications, etc.)-->

### Compute time
Since the game is to be deployed using a cloud provider,
reducing compute time per request is essential to keep costs low.
This shall be achieved by using a fast programming language with low overhead for the backend.

### Scalability
To account for playerbase growth,
the application shall be developed in a scalable manner right from the beginning.
It shall, however, be able to scale to zero, to avoid large costs during the early launch phase.

## 3.5 Supportability

<!--This section indicates any requirements that will enhance the supportability or maintainability of the system being built, including coding standards, naming conventions, class libraries, maintenance access, maintenance utilities._-->
The application shall be built in a modular and maintainable manner.

## 3.6 Design Constraints

<!--This section should indicate any design constraints on the system being built. Design constraints represent design decisions that have been mandated and must be adhered to. Examples include software languages, software process requirements, prescribed use of development tools, architectural and design constraints, purchased components, class libraries, etc._-->

### Backend
The backend shall be written in the Rust programming language, using popular, industry-standard libraries.

### Frontend
The frontend shall be written in Javascript, using the React web framework.

### Deployment
Deployment shall take place on AWS due to economical considerations.
<!--its free, fuck yeah-->

## 3.7 On-line User Documentation and Help System Requirements

<!--Describes the requirements, if any, for on-line user documentation, help systems, help about notices, etc._-->
### API documentation
Documentation for backend API routes shall be easily accessible for members of the project development team.

## 3.8 Purchased Components

<!--This section describes any purchased components to be used with the system, any applicable licensing or usage restrictions, and any associated compatibility and interoperability or interface standards._-->

n/a, only on-demand cloud computing costs shall be incurred.

## 3.9 Interfaces

<!--This section defines the interfaces that must be supported by the application. It should contain adequate specificity, protocols, ports and logical addresses, etc. so that the software can be developed and verified against the interface requirements._-->

### 3.9.1 User Interfaces

<!--Describe the user interfaces that are to be implemented by the software._-->

The game shall be playable using a single, interactive, publicly accessible internet website.

### 3.9.2 Hardware Interfaces

<!--This section defines any hardware interfaces that are to be supported by the software, including logical structure, physical addresses, expected behavior, etc._-->

n/a

### 3.9.3 Software Interfaces

<!--This section describes software interfaces to other components of the software system. These may be purchased components, components reused from another application or components being developed for subsystems outside of the scope of this SRS but with which this software application must interact._-->

n/a

### 3.9.4 Communications Interfaces

<!--Describe any communications interfaces to other systems or devices such as local area networks, remote serial devices, etc._-->

The frontend and backend are to be connected using a HTTP REST API.

## 3.10 Licensing Requirements

<!--Defines any licensing enforcement requirements or other usage restriction requirements that are to be exhibited by the software._-->

Only AI models for which a license can be legally obtained are to be used.

## 3.11 Legal, Copyright, and Other Notices

<!--This section describes any necessary legal disclaimers, warranties, copyright notices, patent notice, wordmark, trademark, or logo compliance issues for the software._-->

n/a

## 3.12 Applicable Standards

<!--This section describes by reference any applicable standard and the specific sections of any such standards which apply to the system being described. For example, legal, quality and regulatory standards, industry standards for usability, interoperability, internationalization, operating system compliance, etc._-->

n/a
