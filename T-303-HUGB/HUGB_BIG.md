

Engineering
- the practice of using natural science, mathematics, and the engineering design process to 
	- solve technical problems
	- increase efficiency 
	- increase productivity
	- improve systems
- make things work by applying theories, methods, and tools where these are appropriate
- get results of the required quality within the schedule and budget (organizational and financial constraints).


Software engineering
- what?
	- an engineering discipline concerned with all aspects of software production (the practical problems of producing software.)
		- software project management
		- the development of tools, methods, and theories to support software production.
	- use of software processes for
		- software specification
		- development
		- validation
		- evolution
	- fix problems like 
		- excessive schedule pressure
		- changing needs (end-users, lawyers, bosses, etc.)
		- lack of technical specifications
		- lack of documented project plan
		- excessive and secondary innovations
		- requirements creep
		- lack of scientific methods
		- ignoring the obvious
		- unethical behavior
	- 4 fundamental activities
		- software specification
			- functionality and constraints on operation are defined
		- software design and implementation
			- the specified software is produced
		- software validation
			- software is validated in accordance with specifications
		- software evolution
			- evolve to meet changing customer needs
- Benefits
	- produce reliable and trustworthy systems economically and quickly
- When 
	- whenever you're developing software applications
- Evaluation 


software process
- what 
	- A systematic approach used in software engineering
	- Activities common across all software processes
		- specification
		- design (architecture)
		- implementation
		- quality assurance (testing)
		- validation
		- evolution
	- Attributes
		- product / artefacts (outcomes of process activities)
		- roles
			- responsibilities of people
		- pre- and postconditions
			- true before and after a process activity has been enacted or product produced
	- Categories
		- plan-driven
		- agile
- Benefits
	- having some structure in the development of software makes the work better, faster and more efficient
- Considerations
	- Organization structure
	- size of software
	- type of software
	- context of software
	- time and budget
	- programmer competence
	- access to stakeholders


Three general issues that affect software
- heterogeneity
	- flexibility to run in different environments (mobile phone, laptop, etc.)
- business and social change
	- building software takes time, software needs to adapt to changes over that time
- security and trust
	- cannot be attacked and personal information security is maintained.


Requirements engineering
- what?
	- finding, documenting and managing what the stakeholder needs are for the product to be developed
		- for understanding end-users and stakeholders (and maintaining that knowledge)
		- for understanding how the system should work, and how to build it
			- Build the right system!
	- composed of 4 activities
		- requirements elicitation
		- requirement specification
		- requirement validation
		- requirement management
- Benefits?
	- produce documents to communicate and maintain information
	- fully understand what an application does so that it can perform as expected by stakeholders.
- Issues?
	- overengineering is never good. Producing a lot of documents makes no sense if said documents are never used.
- When / when not?
	- Depends on software process
		- Agile requires less documentation, but understanding user needs is of vital importance, so RE still applies there
- Evaluation
	- Requirements validation, one of the four activities of RE


Requirement elicitation
- what
	- Discovering requirements
	- Prioritizing requirements based on importantce
	- Negotiation 
	- employ requirement elicitation techniques
		- Interviews -->  
		- Survey (questionnaire based or not) -->
		- observation -->
		- study of existing system --> 
		- scenarios -->
- Issues
	- needs not wants
		- recording customer wants is an error, make sure that everything is a "need"
	- domain
	- conflicts
		- different stakeholders will often tell you different things
	- politics of organization
		- might have to adhere to rules or processes that are set in stone
- Benefits
	- the right way of learning about the user, and what is expected of the system
- When
	- In plan-driven development this is often a first step
	- in agile like processes this is often done continuously, but you must almost always do this step at the beginning so you have some clue of what you're building.
- Evaluation
	- requirement validation
	- Over time


Requirement specification
- what
	- The process of writing down the user and system requirements in a requirement document
		- clear unambiguous
		- complete
		- consistent
		- testable
	- user requirement
		- functional requirement
		- what does the user need to do
	- system requirements
		- technical level, what components are needed
		- hardware and software needed to run the application
		- used for system design
		- add detail and explain how the user requirements should be provided by the system
		- what does the system need to do
	- In plan driven, use software requirements document


Requirement validation
- What
	- Validating that the elicited requirements and specifications are appropriate
	- they are 
		- correct
			- represent stakeholder needs
		- complete
			- all important and relevant stakeholder needs are represented
		- unambiguous
			- Everything is clearly understandable in one way (this is very hard)
		- consistent
			- same format throughout specifications
		- ranked for importance
			- what is needed first, and what might be skippable
		- modifiable
			- easy to change (evolve)
		- verifiable
			- you can write tests for them
		- traceable
			- A requirement depends on another requirement
			- To show that we're following regulatinos
			- show where requirements come from
- Issues 
- Benefits
	- Validating your requirements means fewer change requests and hopefully less conflict with stakeholders, although these can never be perfectly avoided
		- less cost
		- less time
- When
	- right after or even while eliciting requirements
	- in plan-driven processes you validate at the beginning and mostly hope / expect that you're correct
	- in agile this should be done regularly, although it isn't as hard to step back so there is less emphasis on validation there (maybe just before the requirements are chosen for implementation in a sprint)
- Evaluation
	- comes to light with time


Requirement validation techniques
- Prototypes
	- observe how users use the system and chat about what they would like to be different
	- common in agile
- reviews
	- code review
	- review with users
- checklist
	- content check  -> the following sections are present
	- correctness check  -> the requirements are relevant stakeholder needs
	- consistency check  -> conflicts in requirements
	- CRUD check  -> requirements for all CRUD included
		- data can be manipulated according to user needs


Requirement management
- what
	- Requirements management is the process of understanding and controlling changes to system requirements
		- change
			- handling new requirements
			- updating requirements
		- tracking while in development
		- traceability policy
	- 3 principal stages to change management process
		- problem analysis and change specification
			- analyze whether change proposal is valid
				- send back for further detail, then continue
				- deny
			- change analysis and costing (effect and cost of making change)
			- change implementation (requirement document, system design and implementation)
	- decide on
		- Requirements identification -> unique identifiers for requirements
		- a change management process -> assess impact and cost of changes
		- traceability policies 
			- define relationships between requirements, amongst themselves and to the system design
			- how to maintain relationship records
		- tool support -> for requirement management
- Benefits
	- Requirements have a specific format and are usable
	- requirements evolve in a structured and formal way (managable way)


Change management
- what
	- 3 principal stages
		- problem analysis and change specification
		- change analysis and costing
		- change implementation
	- change proposals
	- typical change process
		- clients can register a change process
		- analyze the change (is this a)
			- missing requirement
			- bug
			- wrong implementation
		- Analyze feasability and necessity of change


System requirement specification
- the key document is the system requirements document, which tells the software engineer what the system is supposed to do. 
- Without such knowledge, it is difficult to assess the impact of proposed system changes. 


User story
- what
	- express wants of users, the why behind the requirements (not needs)
	- used for something very specific
- how 
	- as a {persona} I'd like to {functionality} so that I can {benefit}
	- who , what , why
- Benefits
	- understand the system from the perspective of a stakeholder
	- Understand the goals of stakeholders
- Issues
	- not being specific enough in the user story
	- creating user stories that do not apply to real users
- Evaluation
	- get an expert and/or user to look over the user stories and validate them


Process paradigms
- the waterfall model
- incremental development
- reuse-oriented software engineering


the waterfall model
- what
	- Takes fundamental process activities of specification, development, validation and evolution and represents them as strictly separate process phases
	- Cascade from one phase to another
	- all process activities must be planned and scheduled before starting work on them
		- requirement analysis and definition -> system specification
		- system and software design
		- implementation and unit testing
		- integration and system testing
		- operation and maintenance
			- correct errors not found earlier
			- improve implementation of system units and enhance the system's services as new requirements are discovered
	- Result of one phase is an input to another
		- documents that are approved
- Benefits
	- A very traditional engineering method
	- Very structured, what you plan is what you get
		- whether it is what you need is not our issue
- Issues
	- If there is a need to wait in any part of the process, the whole project is delayed
	- producing and approving documents can be expensive
	- commitments must be made at an early stage in the process, which makes it difficult to respond to changing customer requirements
- when
	- parts of the system are well understood and can be specified and developed in advance using a waterfall-based process


Incremental development
- what
	- Interleaves the activities of specification, development and validation
	- system developed as a series of versions with each version adding functionality to the previous version
	- specification, development and validation activities are interleaved, with rapid feedback across activities
	- types
		- plan-driven
			- iterations are identified in advance
		- agile
			- early increments identified
			- later depends on progress and customer priorities
- Benefits
	- reflects the way we solve problems
	- easier to make changes
	- faster delivery and deployment of useful software to customers
- Issues
	- not fit for all contexts
	- system structure tends to degrade as new increments are added
- when
	- when parts of the system are difficult to specify in advance


Reuse-oriented software engineering
- what
	- based on the existence of a significant number of reusable components
	- integrating components into a system rather than developing them from scratch
	- stages
		- component analysis
		- requirement modification
		- system design with reuse
		- development and integration
			- anything that could not be bought is created
		- COTS -- components off the shelf
- Benefits
	- reduced costs and risks
	- faster delivery of software
- Issues
	- requirement compromise
	- less control over system evolution


the v-model
- what
	- plan-driven software process 
	- build, then validate
	- an adaptation of the waterfall process that is still commonly used in systems engineering
		- one module at a time
	- v-shaped structure
		- left (sequential down)
			- specification
			- design
			- implementation / coding
		- Right (testing) (go up)
			- unit testing
			- integration testing
			- system testing
			- acceptance testing
	- plan for other side of v starts as soon as the left side is complete
- Benefits
	- plan-driven
- Issues
	- plan-driven


When a plan-driven software process is used (e.g., for critical systems development), testing is driven by a set of test plans. An independent team of testers works from these pre-formulated test plans, which have been developed from the system specification and design. Figure 2.7 illustrates how test plans are the link between testing and development activities. This is sometimes called the V-model of development (turn it on its side to see the V).

xtreme programming XP
- what
	- Users define and prioritize requirements
	- For each sprint
		- select number of user stories
		- break the user stories into tasks
		- plan release (what to release this increment)
		- development and integration testing
		- release the software
		- evaluate with stakeholders
			- repeat <-
	- Incremental planning with small releases
		- new version up to several times per day
		- delivered to customers every 2 weeks
	- Practices
		- TDD
		- pair programming
		- simple desing
			- solve problem now, make generic later
		- sustainable pace
			- reasonable working conditions and hours
		- continuous refactoring
		- collective ownership
		- continuous integration
			- All automated tests have to pass for every build
		- sustainable pace
		- on-site customer (representative)
	- System requirements
		- customers are intimately involved in specifying and prioritizing 
			- developers cannot change prioritization
		- not specified as lists of required system functions. 
			- Rather, the system customer is part of the development team and discusses scenarios with other team members. 
	- story cards
		- used instead of a formal document to collect user requirements incrementally
		- developed by system customers and developers
		- the main inputs to the XP planning process (the planning game)
		- when implementing
			- break into tasks
			- estimate (per task)
				- effort
				- resources
	- Evolution of requirements
		- unimplemented stories change or may be discarded
		- new story cards are created (following same process with customer)
	- Spike
		- an increment where no programming is done 
			- do testing / prototyping
			- design system achitecture
			- develop system documentation
	- Deadlines are every two weeks, strictly!
		- if there are development problems, the customer is consulted and functionality is removed from the planned release
	- designing for change is often wasted effort
		- No generality
		- reorganize the software when these changes actually occur.
	- software should always be easy to understand and change as new stories are implemented.
	- most companies who have adopted an XP variant use small releases, test-first development, and continuous integration. 
- Benefits
	- Working with directly with users
	- Working with less overhead
- Issues
	- Sometimes development pressure means that refactoring is delayed because the time is devoted to the implementation of new functionality
	- Degrading software structure
		- Because architecture is not planned, new features and changes cannot readily be accommodated by code-level refactoring and require the architecture of the system to be modified.
		- changes to software become harder to implement
		- fixed by constant refactoring
			- programmers look for possible improvements to the software and implement them immediately
- When -> see agile


pair programming
- what
	- two people programming together on 1 computer
		- 1 person programs and explains what they're doing
		- 1 person comments on and asks about the code
- benefits
	- more people know how the system is being developed
	- sharing knowledge
- when
	- on-boarding
	- AVOID when experienced developers



extreme programming practices
- incremental development
	- small frequent releases of the system
	- requirements are based on simple customer stories or scenarios
		- used as a basis for deciding what functionality should be included in a system increment
- customer involvement 
	- through continuous engagement of the customer in the devlopment team
	- customer representative takes part in the development and is responsible for defining acceptance tests for the system
- People, not process
	- pair programming
	- collective ownership of the system code
	- sustainable development process that does not involve excessively long working hours
- change
	- regular system releases to customers
	- test-first development
	- refactoring to avoid code degeneration
	- continuous integration of new functionality
- maintaining simplicity 
	- constant refactoring 
		- improves code quality
	- use simple designs that do not unnecessarily anticipate future changes to the system


Scrum
- what
	- Agile specifically designed for the software world
		- management of iterative software development
	- No prescribed technical practices
		- made to tailor to the needs of your specific team / company
	- the process
		- Specification / planning
			- product backlog
				- a flexible collection of user stories populated at the beginning of the process
			- sprint backlog
		- Increments / sprints
			- each sprint is 2 - 4 weeks
				- populate sprint backlog, and break chosen user stories down into tasks
				- team-members choose their tasks
			- Daily scrum (standup meetings)
				- what was done the day before
				- where are you stuck
				- what is your plan for the current day
			- Sprint review (end of sprint)
				- deliverable is reviewed with customer
					- Something that can be run and shown to customer
					- discuss changes in product backlog
				- retrospective
					- What went well, what didn't, what should we change in the future?
			- repeat (even into maintenance)
		- Roles
			- Scrum team 7 +- 2 people
			- cross-functional 
				- self-organized, everyone with same responsibilities, collective ownership of code
			- Scrum master
			- product owner
				- a customer representative
				- has authority to make decisions about what is acceptable and what should be changed / added
				- prioritizes the product backlog
				- should be able to give constant feedback (part of the team)
- Benefits
	- Simple and modular
	- The idea behind Scrum is that the whole team should be empowered to make decisions
	- The product is broken down into a set of manageable and understandable chunks.
	- Unstable requirements do not hold up progress.
	- The whole team has visibility of everything and consequently team communication is improved.
	- Customers see on-time delivery of increments and gain feedback on how the product works.
	- Trust between customers and developers is established and a positive culture is created in which everyone expects the project to succeed.
- Issues
	- Agile team must be mature
	- scrum is created for co-located teams, distributed teams may not work as well.
	- Architecture tends to get neglected as it is not part of the process
	- lack of documentation
	- Maybe a little bit too modular -> sometimes no longer scrum / agile
	- Some issues cannot be defined in a user story format
	- Some contexts don't allow for agile development
	- bad at fixing bugs


Scrum vs. xtreme programming
- Unlike XP, Scrum does not make specific suggestions on how to write requirements, test-first development, etc.
- **Scrum focuses on project management and teamwork, while XP focuses on code quality and individual programmers' work**.
- Scrum the team can choose the sequence in which to build the product, while in xp they have to follow a strict prioritization scheme


Scrum master
- what
	- ensures that the scrum process is followed
	- protects team from external distractions
	- interfaces with the rest of the organization / customers
	- a facilitator
		- arranges daily standup meetings
		- tracks backlogs
		- records decisions
		- measures progress
		- communicates with customers and management
	- There is no top-down direction from the scrum master
	- should have experience from a succesful scrum team
- Issues
	- A scrum master is not the boss of a scrum team. A scrum team is a TEAM of independent identities that self-organize.
- Benefits
	- The rest of the team can focus on what matters for finishing the sprint
	- Less stress on others
	- Someone to make sure the team is working like it's supposed to


Definition of done
- what
	- the goal/-s of a sprint
		- when do we consider the work for this sprint to be done
		- i.e. what do we want to achieve in this sprint
- Issues
	- this is not a concrete list. You should not do more than is defined, but you don't have to do everything perfectly.
- Benefits
	- Understand what work needs to be done
	- thing about the tasks before you do them
- evaluation
	- should be something that is achievable within the time limit of the sprint
	- should be something that "fills" the sprint


Decision protocol
- what
	- Documents the what and why of the system
	- a diary for the developers to document decisions they've made so that later on aspects of the system can be analyzed, and we remember errors that may have occurred
- benefits
	- a great repository of knowledge about the system
	- a very easy, informal way to document the system


task breakdown/ownership
- what
	- breaking down user stories, or other higher level requirements into tasks
		- for implementation
	- chosen not assigned (scrum)
- benefits
	- seeing what work needs to be done to create functionality
	- makes it easier to estimate the work required and see what truly needs to be done
- when
	- at the start of a sprint in agile


Agile
- what?
	- Prioritize development of higher value customer features and validate them frequently
	- The rundown
		- increments called sprints
			- new, working releases of the system (increments) are created and made available to customers every two or three weeks. 
		- Constant stakeholder involvement
			- customers then propose new and changed requirements to be included in later iterations of the system
		- frequent delivery of updates
		- automation -> automated testing f.x.
		- minimal documentation (NOT no documentation)
	- Agile teams
		- a team member clearly understands his goals and priorities
		- Kaizen - continous improvement
		- Self-organized teams -- no direct management
		- develop methods to work efficiently as a team
			- formalize / standardize methods to develop software and become better at using those methods with time
			- automate as much as possible
	- specification, design, and implementation are intertwined
		- minimize documentation using informal communications rather than formal meetings with written documents.
			- avoid work that has dubious long-term value
			- eliminate documentation that will never be used
		- Activities
			- Main focus on design and implementation
			- requirement elicitation and testing also
		- emphasis on
			- importance of writing well-structured code
			- investing effort in code improvement
			- lack of documentation should not be a problem in maintaining systems developed using an agile approach. (in a perfect world)
	- We plan iteratively in short sprints
		- Continuous communication is needed between dependent teams (at least when planning sprints)
		• Outputs decided before an iteration (or during)
		- Iteration planning
			- a shorter-term outlook
			- focuses on planning the next increment of a system
				- typically 2 to 4 weeks of work for the team.
			- iteration occurs across activities (activities intertwined)
				- requirements and design are developed together
	- documentation ‘spike’
		- team produces system documentation instead of producing a new version of a system
	- two-stage approach to planning in agile
		- Release planning
			- look ahead for several months and decide on the features that should be included in a release of a system.
- Considerations (issues and when good)
	- real issues
		- maintaining continuity of the development team
			- team members should understand aspects of the system without having to consult documentation (implicit knowledge)
		- Losing customer representative once development is over and maintenance starts
			- requirements gathered through alternative mechanisms such as change proposals
		- collect requirements informally and incrementally 
			- Many do not create a coherent requirements document
			- likely to make system maintenance more difficult and expensive
		- cascade (no longer working in agile)
			- separate teams for requirements, development, and testing
		- Too little documentation
			- we still need to have some knowledge about the application
		- People must have a suitable personality for agile
		- prioritizing changes can be extremely difficult
			- especially when many stakeholders
		- maintaining simplicity requires extra work
		- changing company cultures is difficult and takes time. Adapting to agile may take some time -- changing to informal processes is diiificult
		- Architecture
			- tends to get fucked -> agile doesn't really discuss architecture it just has to happen
	- agile teams
		- requires a team that is very mature
		- needs to self-organize without direct management
		- hard to start straight away
	- Environments
		- Successful when
			- Application development where the system requirements usually change rapidly during the development process
			- Product development where a software company is developing a small or medium-sized product for sale.
			- Custom system development within an organization, where there is a clear commitment from the customer to become involved in the development process and where there are not a lot of external rules and regulations that affect the software.
		- bad when
			- critical systems
				- because of the need for security, safety, and dependability analysis 
	- customer representatives
		- not representative enough of the user base
		- has other responsibility
	- top challenges
		- define what a customer value is
		- customer collaboration
		- agile team maturity
	- Top value metrics
		- number of defects per period
		- amount of work in progress
		- cycle time


Agile contracts
- Software requirements document is usually part of the contract between the customer and the supplier.
	- incremental specification is inherent in agile methods
		- writing contracts may be difficult
- contracts
	- the customer pays for the time required for system development rather than the development of a specific set of requirements
	- benefits developer and customer if all goes well
	- otherwise dispute over who is to blame, and who should pay for extra time and resources to solve the problems
This contrasts with agile development, where many decisions affecting the development are delayed and made later, as required, during the development process.


The agile manifesto
- Individuals and interactions over processes and tools
- working software over comprehensive documentation
- customer collaboration over contract negotiation
- responding to change over following a plan


Rapid software development processes
- what
	- produce useful software quickly
		- software is developed in series of increments (rather than a single unit)
		- each increment includes a new system functionality
	- The processes of specification, design, and implementation are interleaved.
	- no detailed system specification, and design documentation is minimized
	- user requirements document only defines the most important characteristics of the system.
	- system is developed in a series of versions. 
		- End-users and other system stakeholders are involved in specifying and evaluating each version
			- They may propose changes to the software and new requirements that should be implemented in a later version of the system.
		- heavy use of prototyping
- when 
	- in business environments where quick and efficient work is key
		- quickly take advantage of new opportunities and respond to competitive pressure by developing faster
- When not
	- critical applications


plan-driven processes
- what
	- the development process is planned in detail - then following it exactly
	- the ‘traditional’ way of managing large software development projects. 
	- the focus is on making plans and having milestones
	- project plan 
		- process activities
			- the resources available to the project
			- the work breakdown
				- work to be done
				- who will do it
			- development schedule
			- work products
			- progress is measured against this plan
		- identify
			- risks to the project and the software under development
			- the approach that is taken to risk management
		- specific details of project plans vary depending on the type of project and organization
		- Used by managers to support project decision making and as a way of measuring progress.
	- Iterative approach
		- iterations identified in advance
			- outputs planned and associated with each stage / iteration
		- iteration occurs within activities with formal documents used to communicate between stages of the process. 
			- outputs from one stage are used as a basis for planning the following process activity
		- the requirements will evolve 
			- a requirements specification will be produced
				- an input to the design and implementation process
		- Iterations / development stages are SEPARATE
			- make plans, then freeze them
	- Not much communication needed between teams during development
		- Interfaces are discussed and fixed when we develop
	- can be incremental
	- testing driven by a set of test plans
- when
	- required by some regulations projects
	- --> agile vs. plan-driven
issues
- many early decisions have to be revised because of changes to the environment in which the software is to be developed and used. 
	- Delaying such decisions is sensible because it avoids unnecessary rework.
Benefits
- early planning allows organizational issues (availability of staff, other projects, etc.) to be closely taken into account
- potential problems and dependencies are discovered before the project starts, rather than once the project is under way.


Agile vs. plan driven
- plan driven when
	- important to have a very detailed specification and design before moving to implementation
		large systems that require larger development teams
	- Systems that require a lot of analysis before implementation (e.g., real-time system with complex timing requirements) usually need a fairly detailed design to carry out this analysis
	- Long-lifetime systems may require more design documentation to communicate the original intentions of the system developers to the support team
		- plan driven preferred, but not necessarily better than agile
	- Agile methods often rely on good tools to keep track of an evolving design. if not have good tools for program visualization and analysis, then more design documentation may be required. - plan driven
	- If the development team is distributed 
	- part of the development is being outsourced
	- If you have a team with relatively low skill levels, you may need to use the best people to develop the design, with others responsible for programming.
	- if the system subject to external regulation 
- agile when
	- incremental delivery strategy, where you deliver the software to customers and get rapid feedback from them, realistic
	- the system can be developed with a small co-located team who can communicate informally. 
- Considerations
	- size of system
	- type of system
	- available tools (for developers) and experience
	- organization culture, structure and communication
		- developing the system
		- being developed for
	- competence of designers and programmers
- Differences
	- agile has intertwined stages of development while plan-driven has clearly separated stages with defined outputs and inputs, and freezes of previous stages.
	- plan driven requires a lot of documentation and planning while agile tries to figure things out intuitively as the product evolves.
	- Plan-driven tends to follow a very defined structure while agile is quite fluid and unstructured (compared to plan-driven)


Estimation
- what
	- estimating the time that a task will take (in the context of agile)
	- some games can be played
	- use 
		- planning poker
			- parallel estimation
				- Everyone estimates on their own
			- independently estimate tasks and simultaneously reveal their estimates
			- improve communication, avoid anchoring bias
		- burndown-chart
			- a way of visualizing how long tasks are taking
		- Story points
			- talk about deadlines
			- evaluate difficulty based on story points, then fit them into a budget
			- velocity - how much can you do in one sprint?
			- difficulty, not time spent
- Benefits
	- Forces you to think about the work to be done
		- what needs to be done
		- how much work it will take
- Issues
	- When we don't think about the work to be done




Software architecture
- what
	- a system organization that will satisfy the functional and non-functional requirements of a system
		- describes how the system is organized as a set of communicating components.
		- identify main structural components and relationships between them.
	- the link between design and requirements engineering
	- descriptive or prescriptive
	- two levels of abstraction
		- in the small 
			- the architecture of individual programs
			- how an individual program is decomposed into components
		- in the large 
			- architecture of complex enterprise systems that include other systems, programs, and program components
			- often distributed over different computers, owned and managed by different companies
	- non-functional requirements depend on the system architecture 
		- performance
		- robustness 
		- distributability
		- maintainability 
		- individual components implement the functional system requirements
	- may use different architectural patterns or styles for different parts of the system.
	- why
		- Stakeholder communication
			- a design plan for the negotiation of system requirements
		- System analysis 
			- can the system meet critical requirements 
			- a means of structuring discussions with clients, developers, and managers. 
			- an essential tool for complexity management
				- hides details, focus on key system abstractions.
		- Large-scale reuse
			 - system architecture is often the same for systems with similar requirements 
	- complete architectural documentation may be required when
		- developing critical systems
		- need to make a detailed dependability analysis of the system
		- need to convince external regulators that your system conforms to their regulations and so 
- considerations
	- generic application architecture exists?
	- multi-threaded?
	- architectural patterns or styles?
	- how to approach the structure of the system
	- how to decompose into subcomponents
	- strategy to control operation of components
	- non-functional requirements
	- how to evaluate the design
	- how to document the architecture
	- large components 
		- improves performance
	- small, fine-grain components 
		- improves maintainability. 
- Issues
	- Incremental development of architectures is not usually successful.


Architecture emphasis
- Performance 
	- localize critical operations within a small number of components, all deployed on the same computer 
	- few relatively large components rather than small, fine-grain components
	- reduce the number of component communications
- Security
	- use layered structure for architecture
	- critical assets protected in innermost layers
	- high level of security validation applied to these layers.
- Safety 
	- safety-related operations are all located in either a single component or in a small number of components
		- Reduce costs and problems of safety validation
		- provide related protection systems that can safely shut down the system in the event of failure.
- Availability
	- include redundant components 
	- possible to replace and update components without stopping the system. 
- Maintainability
	- use fine-grain, self-contained components that may readily be changed
	- Producers of data should be separated from consumers and shared data structures should be avoided.
- Evaluating 
	- how well the system meets its functional and non-functional requirements when it is in use
	- compare against reference architectures or generic architectural patterns


Architectural views
- process view
	- shows how, at run-time, the system is composed of interacting processes. This view is useful for making judgments about nonfunctional system characteristics such as performance and availability.
- development view
	- shows how the software is decomposed for development, that is, it shows the breakdown of the software into components that are implemented by a single developer or development team. This view is useful for software managers and programmers.
- physical view
	- shows the system hardware and how software components are distributed across the processors in the system. This view is useful for systems engineers planning a system deployment.
- logical view
	- shows the key abstractions in the system as objects or object classes. It should be possible to relate the system requirements to entities in this logical view.


Architecture and RE in practice
- overlap between requirements engineering and architectural design.
 - Ideally, a system specification should not include any design information.
- Architectural decomposition 
	- necessary to structure and organize the specification
	- might propose an abstract system architecture as part of RE
		- associate groups of system functions or features with large-scale components or sub-systems. 
	- use this decomposition to discuss the requirements and features of the system with stakeholders.


Architecture patterns / styles
- what
	- a stylized, abstract description of good practice, which has been tried and tested in different systems and environments
		- describes system organization that has been successful in previous systems
		- includes information on
			- when appropriate to use that pattern
			- strengths and weaknesses.
	- Styles 
		- guidance and analysis for building a broad class of architectures in a specific domain
	- patterns
		- solve smaller, more speciﬁc problems within a given style
- considerations
	- size of applicaiton
	- context of application (where)
	- legacy (what do we have)
	- demands
		- to security
		- to performance
	- company structure (conway's law)
	- mode of deployment
	- scalability
		- in terms of use
		- in terms of people working on it


Layered architecture
- what
	- separation and independence allow changes to be localized.
	- system functionality is organized into separate layers
		- each layer only relies on the facilities and services offered by the layer immediately beneath it.
	- Organizes the system into layers with related functionality associated with each layer. 
		- A layer provides services to the layer above it
		- the lowest-level layers represent core services that are likely to be used throughout the system.
- when
	- building new facilities on top of existing systems
	- development is spread across several teams with each team responsibility for a layer of functionality
	- multi-level security is required
- Benefits
	- Allows replacement of entire layers so long as the interface is maintained. 
	- Redundant facilities (e.g., authentication) can be provided in each layer to increase the dependability of the system.
- Issues
	- providing a clean separation between layers is often difficult
		- direct communication may be impossible
	- Performance can be a problem because of multiple levels of interpretation of a service request as it is processed at each layer.


The layered approach to software architecture
- what 
	- Examples
		- layered architecture
		- MVC
	- changeable and portable
		- A layer can be replaced by another, equivalent layer with same interface
	- layered systems localize machine dependencies in inner layers
		- only the adjacent layer is affected when layer interfaces change or new facilities are added to a layer
		- easier to provide multi-platform implementations of an application 
	- supports the incremental development of systems
	- the view presented is the conceptual organization of a system


Model view controller MVC
- What
	- Separates presentation and interaction from the system data
		- changes are localized
	- system structured into three logical components that interact
		- The Model component 
			- manages the system data and associated operations on that data. 
		- The View component 
			- defines and manages how the data is presented to the user.
		- The Controller component
			- manages user interaction (e.g., key presses, mouse clicks, etc.)
			- passes these interactions to the View and the Model
- When 
	- multiple ways to view and interact with data
	- future requirements for interaction and presentation of data are unknown
- Benefits
	- data can change independently of its representation and vice versa
	- Supports presentation of the same data in different ways 
		- changes made in one representation are shown in all of them.
- Issues
	- additional code and code complexity when the data model and interactions are simple.


repository architecture
- what
	- Describes how a set of interacting components can share data.
	- concerned with the static structure of a system 
		- does not show its run-time organization
	- All data in a system is managed in a central repository that is accessible to all system components
		- Components do not interact only through the repository, never directly
	- The majority of systems that use large amounts of data are organized around a shared database or repository.
	- an efficient way to share large amounts of data
		- no need to transmit data explicitly from one component to another
- When
	- large volumes of information are generated that has to be stored for a long time
	- data-driven systems 
		- inclusion of data in the repository triggers an action or tool
	- data is generated by one component and used by another
- Benefits
	- Components can be independent 
		- they do not need to know of the existence of other components
		- Changes made by one component can be propagated to all components
	- All data can be managed consistently (e.g., backups done at the same time) everything in one place.
- Issues
	- Single point of failure (the repo)
		- problems in the repository affect the whole system
	- inefficiencies in organizing all communication through the repository
		- components must operate around an agreed repository data model 
		- compromise between the specific needs of each tool 
		- difficult or impossible to integrate new components 
			- f.x. data models do not fit the agreed schema
	- Distributing the repository may be difficult.
		- problems with data redundancy and inconsistency.


service oriented architecture (SOA)
- what
	- precursor to microservices
	- services
		- should be loosely coupled
		- should be combinable in new and innovative ways
		- are platform independent
		- follow standardized commmunication protocols
	- localized concepts
		- Service registry
			- where services are published
		- service provider
			- implements, runs and publishes the service
		- service user
			- binds to provider (SOAP)
			- finds a service through registry
	- Vision
		- find and re-use services through global service registries
- Issues
	- tightly coupled with technology standards (SOAP)


Service
- what
	- loosely coupled
	- implementation and platform independent
	- Pay for service use -> i.e. not built or maintained by you 



microservices
- what
	- building applications as suites of services (breaking them down into)
	- an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API
		- services
			- splitting up and organized around business capability
			- independently deployable by fully automated deployment machinery
			- independently scalable
			- provides a firm module boundary
				- different services, different languages and or different teams
	- Componentization via Services
	- teams are cross-functional and owns a product over its full lifetime
		- including the full range of skills required for the development
		- a development team takes full responsibility for the software in production. 
		- take on some support burden
		- Teams are responsible for all aspects of the software they build including operating the software 24/7.
	- Smart endpoints and dumb pipes
		- aim to be as decoupled and as cohesive as possible
		- act more as filters in the classical Unix sense
			- receiving a request, applying logic as appropriate and producing a response.
	- Decentralized Governance
		- teams own their own domain logic (not same rules everywhere)
		- choice of tools when building service
		- producing useful tools that other developers can use to solve similar problems to the ones they are facing
	- Decentralized Data Management
		- decentralize decisions about conceptual models and data storage decisions
			- conceptual model of the world will differ between systems
				- common issue when integrating across a large enterprise 
			- each service manages its own database
				- either different instances of the same database technology, or entirely different database systems - polyglot persistence
	- continuous delivery
		- must design for failure
			- tolerate failure of other services
			- emphasis on real-time monitoring of the application
	- Evolutionary Design
		- new features by new services 
		- We can avoid a lot of versioning by designing services to be as tolerant as possible to changes in their suppliers.
- Benefits
	- Strong Module Boundaries
		- reinforce modular structure (good for large teams)
	- Independent deployment
		- Simple services are easier to deploy, and since they are autonomous, are less likely to cause system failures when they go wrong.
		- Minimize redeployment through cohesive service boundaries and evolution mechanisms in the service contracts.
		- scaling easy
	- technology diversity
		- you can mix multiple languages, development frameworks and data-storage technologies.
- Issues
	- distribution
		- Distributed systems are harder to program
		- remote calls are slow and are always at risk of failure.
	- Eventual consistency
		- Maintaining strong consistency is difficult for a distributed system
			- everyone has to manage eventual consistency.
	- Operational complexity
		- You need a mature operations team to manage lots of services, which are being redeployed regularly.


difference between SoA and microservice
- SoA
	- Services are shared and used enterprise wide
	- all services share a common data repo
	- every service has a broad scope, if one fails, then everything fails
- microservice
	- individual services that function independently
	- smaller services


client-server style
- what 
	- commonly used run-time organization for distributed systems
	- usually implemented as distributed systems, connected using Internet protocols.
		- but can be implemented on one computer
	- services
		- functionality of the system
		- delivered from a separate server
	- components
		- servers
			- offer services to other components
			- do not need to know the identity of clients or how many clients are accessing their services
		- clients 
			- call on the services offered by servers (users of services)
				- through remote procedure calls 
					- request-reply protocol such as the http protocol used in the WWW.
					- make a request to a server and waits until reply
			- normally several instances of a client program executing concurrently on different computers.
			- may have to know the names of the available servers and the services that they provide.
		- network 
			- allows the clients to access services
- When
	- data in a shared database has to be accessed from a range of locations
	- load on a system is variable -> servers can be replicated
- Benefits
	- separation and independence
		- servers can be distributed across a network
		- Services and servers can be changed without affecting other parts of the system.
		- upgrade servers transparently without affecting other parts of the system
	- General functionality can be available to all clients without being implemented by all services.
- Issues
	- services are single points of failure 
		- susceptible to denial of service attacks or server failure
	- Performance may be unpredictable 
		- depends on the network as well as the system
	- management problems if servers are owned by different organizations


pipe-and filter style
- What
	- Data flows from one filter to another and is transformed as it moves through the sequence.
		- Each processing step (filter)
			- implemented as a transform.
			- is discrete and carries out one type of data transformation
		- Input data flows through these transforms until converted to output
		- data can be processed by each transform item by item or in a single batch.
	- a model of the run-time organization of a system where functional transformations process their inputs and produce outputs.
- When
	- data processing applications (both batch- and transaction-based) 
		- inputs are processed in separate stages to generate related outputs.
	- The architecture of an embedded systems where each process is executed concurrently.
	- batch sequential model
		- When transformations are sequential with data processed in batches 
			- a common architecture for data processing systems (e.g., a billing system)
- Benefits
	- Easy to understand
		- Workflow style matches the structure of many business processes
	- supports transformation reuse
	- Evolution by adding transformations is straightforward
	- Can be implemented as either a sequential or concurrent system.
- Issues
	- The format for data transfer has to be agreed upon between communicating transformations
		- Each transformation must parse its input and unparse its output to the agreed form
		- increased system overhead and may mean that it is impossible to reuse functional transformations that use incompatible data structures.
	- Interactive systems are difficult to write using the pipe and filter 
		- need for a stream of data to be processed



Generic application architecture
- what
	- describe the structure and organization of particular types of software systems.
		- often application reuse without reimplementation
	- common software architectures that work as long as your business is similar
		- create design checklists
		- steal ideas or buy them
		- do less work
	- F.x.
		- ERP systems
			- large systems that are easy to tailor to specific contexts
		- data processing applications
		- transaction processing
		- event processing applications
		- language processing
		- COTS


Conway's law
- what
	- An organization developing a product sooner or later starts resembling the product (architecture)
		- teams structured like the software structure
		- communication within the organization
	- Architecture is a blueprint for development of the organization
- Considerations
	- the structure of your organization matters when choosing an architecture


System modelling
- what
	- System modeling is the process of developing abstract models of a system, with each model presenting a different view or perspective of that system.
	- types
		- UML
		- mathematical models


Model
- what
	- an abstract view of a system 
		- not an alternative represenation of the system
			- a representation of a system should maintain all the information bout the entity being represented
		- ignores some system details
		- Complementary system models can be developed to show 
			- context 
			- interactions
			- structure 
			- behavior
	- 3 common uses
		- facilitating discussion about an existing or proposed system.
		- documenting an existing system.
			- requires correct notation, but not necessarily complete
		- a detailed system description that can be used to generate a system implementation
			- generate a complete or partial system implementation from the system model
			- required to be complete and correct
- when
	- requirements engineering process to help derive the requirements for a system
	- design process to describe the system to engineers implementing the system 
	- after implementation to document the system’s structure and operation. 
- Issues
	- creating models for the wrong audience
	- inaccuracies in models may have consequences
	- may lack purpose


Model
- what?
	- representation of something in the real world
	- types
		- descriptive
		- prescriptive - planning
- Benefits / why
	- communication
	- analysis
	- certification
	- simulation
	- generation


Diagram
- what
	- a view on a model

Diagrams vs. models
- Diagram
	- picture of something, a view on a model
	- A lot of diagrams can work on one model
	- A view, shows part of (the system then) the model


UML diagram types
- context of system
	- relatinship to outside world an other systems
	- describe human and automated processes in which particular software systems are used.
	- use
		- domain model (1) 
		- class diagrams
		- component diagrams
- interaction
	- how components communicate with each other
		- user interaction, which involves user inputs and outputs, 
			- helps to identify user requirements.
		- interaction between the system being developed and other systems 
			- highlights the communication problems that may arise
		- interaction between the components of the system
			- helps us understand if a proposed system structure is likely to deliver the required system performance and dependability.
	- use
		- sequence diagram
- structure
	- the organization of a system in terms of the components that make up that system and their relationships.
		- static models
			- show the structure of the system design
		- dynamic models
			- show the organization of the system when it is executing.
	- For discussing and designing the system architecture
	- use
		- class diagram
		- component diagram
- beheavior
	- behavior within unit / component
	- the dynamic behavior of the system as it is executing
		- what is supposed to happen when a system responds to a stimulus from its environment
		- two types of stimuli
			- Data -> which has to be processed
			- Events -> that triggers processing
	- use
		- state machine diagram

Diagram type overview
- Activity diagrams, show the activities involved in a process or in data processing.
- Use case diagrams, show the interactions between a system and its environment.
- Sequence diagrams, show interactions between actors and the system and between system components.
- Class diagrams, show the object classes in the system and the associations between these classes.
- State diagrams, show how the system reacts to internal and external events


domain model
- what
	- context model -> what is in the system and what is not
	- the domain vocabulary
	- purpose
		- define the domain of your system
		- understand the system of elements and interactions between them
	- Identify
		- important (domain) concepts
		- relevant entities for the problem under study (the target system)
		- relations between concepts
	- Draw with no technical detail (informal UML)
	- kind of drawn like class diagram, but not really


component diagram
- what
	- simliar to class diagrams
		- but components not classes
	- important for architecture
- defines what is going in (required to make the component work) and what's coming out (what the component provides)
- drawings
	- lollipops provide public interface
	- lego hands use interface
	- can also go into more class diagram, defining attributes and methods with arrows and such


Sequence diagram
- what
	- interaction, not what components do
	- timeline with sync and async message
	- common for networks
	- Sequence diagrams in the UML are primarily used to model the interactions between the actors and the objects in a system and the interactions between the objects themselves.


Component
- what
	- A unit of composition (made up of something else)
	- an application that can
		- run independently (independently deployable)
		- communicate in a network
	- has specified dependencies (interfaces)


Module
- **Modules are collections of methods and constants.** They cannot generate instances.


V & V
- what
	- verification & validation
		- Verification -> building the product right (conforms to specification)
		- validation   -> building the right product (conforms to user needs)
	- Establish confidence that the system is fit for purpose


Software inspection
- what
	- Analysis of static system -> no execution
	- analyze and check the system requirements, design models, the program source code, and even proposed system tests
	- static V&V methods -> don't execute the code
	- focus on the source code of a system but any readable representation of the software, such as its requirements or a design model, can be inspected
	- considers broader quality attributes of a program
		- compliance with standards
		- portability
		- maintainability
		- You can look for inefficiencies
		- inappropriate algorithms
		- poor programming style
- Benefits
	- Improved understanding of codebase
	- everybody is kept in check regarding readability and documentation
	- some things are easier to see than to test
- Issues
	- can't cover everything, f.x. performance


Inspection methods
- manual review
	- code review
		- improve communication and shared understanding of code
- Automatic
	- linters
	- natuaral language processing (for inspection)
	- automated program analysis and repair
		- bugs found via automated testing


Software testing
- what
	- excercising and observing actual behavior
		- Execute program using artifical inputs / data
		- results are then checked for anomalies or errors
	- Goals
		- Validation testing 
			- the software meets its requirements (operates as intended)
		- defect testing
			- Discover undesirable bugs
			- root out undesirable system behavior such as system crashes, unwanted interactions with other systems, incorrect computations, and data corruption.
			- if successful, system is running incorrectly
	- Stages
		1. Implementation and unit testing
		2. Integration and system testing
		3. Operation and maintenance testing
- Benefits
	- notice errors before deployment
- Issues
	- errors can mask other errors
	- positive testing
		- testing only positive cases (how you think people will use the application)
	- Cannot show the absence of bugs

Quality assurance
- what
	- assuring the quality of a product
	- an assortment of management activities
		- change management
		- security management
		- risk management
		- testing
		- etc.


What to test
- custom software
	- at least one test for every requirement in the requirements document. 
- For generic software products
	- there should be tests for all of the system features, plus combinations of these features, that will be incorporated in the product release.


3 stages of testing for commercial software products
- Development testing
	- testing in development to discover bugs and defects
- Release testing
	- a separate testing team tests a complete version of the system before it is released to users
	- check that the system meets the requirements of system stakeholders.
- User testing
	- users or potential users of a system test the system in their own environment
	- Acceptance testing is one type of user testing where the customer formally tests a system to decide if it should be accepted from the system supplier or if further development is required.

Manual vs. automated testing
- manual
	- tester follows a script and runs the program with some test data
	- note down anything interesting
- Auomatated
	- Tests are encoded in a program that senses anomalous results
	- Confined to testing what a program is supposed to do
		- not GUI or unwanted side effects


Development testing
- testing activities carried out by the team developing the system
- primarily a defect testing process
- 3 levels of granularity:
	- Unit testing
		- individual program units or object classes are tested
		- focus on testing the functionality of objects or methods.
		- Mainly defect testing
	- Component testing
		- several individual units are integrated to create composite components
		- focus on testing component interfaces
			- interface misuse -> incorrect assumptions about use (call)
			- interface misunderstanding -> incorrect assumptions about behavior
			- timing error -> components in different time (async)
	- System testing
		- some or all of the components in a system are integrated and the system is tested as a whole
		- focus on testing component interactions
		- integrating components to create a version of the system and then testing the integrated system
		- System testing checks that 
			- components are compatible
			- interact correctly 
			- transfer the right data at the right time across their interfaces
		- what to test
			- All system functions that are accessed through menus should be tested.
			- Combinations of functions (e.g., text formatting) that are accessed through the same menu must be tested.
			- Where user input is provided, all functions must be tested with both correct and incorrect input.


Component vs. system testing
- During system testing, reusable components that have been separately developed and off-the-shelf systems may be integrated with newly developed components. The complete system is then tested.
- Components developed by different team members or groups may be integrated in system testing. System testing is a collective rather than an individual process. 
- Sometimes a separate testing team with no involvement from designers and programmers.


Unit testing 
- the process of testing program components, such as methods or object classes. Individual functions or methods are the simplest type of component.
	- test all operations associated with the object;
	- set and check the value of all attributes associated with the object;
	- put the object into all possible states


black box testing
- use the specification of a system to identify equivalence partitions, this is called 


white box testing
- look at the code of the program to find other possible test


release testing vs. system testing
- release testing
	- check that the system meets its requirements and is good enough for external use (validation testing).
	- A separate team that has not been involved in the system development should be responsible for release testing.
- System testing 
	- focus on discovering bugs in the system (defect testing)


Release testing 'functional testing'
- convince the supplier of the system that it is good enough for use. If so, it can be released as a product or delivered to the customer
- black box with tests derived from system specification
- functionality, not implementation


scenario testing
- make up scenario
- follow scenario manually, making deliberate mistakes along the way
- also checks performance


Performance tests
- ensure that the system can process its intended load
- run a series of tests where you increase the load until the system performance becomes unacceptable.
	- try to be realistic about what processes are running
- tests the failure behavior of the system. 
- Avoid
	- data corruption 
	- unexpected loss of user services
- the system should ‘fail-soft’ rather than collapse under its load.
- particularly relevant to distributed systems based on a network of processors
	- Stress testing helps you discover when the degradation begins so that you can add checks to the system to reject transactions beyond this point.


User or customer testing 
- a stage in the testing process in which users or customers provide input and advice on system testing.
- 3 different types of user testing:
	- Alpha testing
		- users of the software work with the development team to test the software at the developer’s site.
	- Beta testing
		- a release of the software is made available to users to allow them to experiment and to raise problems that they discover with the system developers.
		- aform of marketing, customers learn about their system and what it can do for them.
	- Acceptance testing
		- customers test a system to decide whether or not it is ready to be accepted from the system developers and deployed in the customer environment.

contracts
- outcome of negotiations may be conditional acceptance of the system
- The customer may accept the system so that deployment can begin
	- system provider agrees to repair urgent problems and deliver a new version to the customer as quickly as possible


Inspection vs. testing
- testing requires runnable software
- inspection can look for things that are hard to test
	- compliance with standards
	- readability
	- coding / documenting conventions


Types of testing 
- development testing (mirror waterfall process) (all testing done by developers)
	- system testing --> requirements
		- the whole system is tested
		- focus on defect testing
	- integration / component testing --> Design
		- Assume that unit testing has been done competently
		- test that interfaces behave as desired / specified
		- also stress test the system
	- unit testing --> Implementation
- release testing
	- Is the system ready for release? (acceptable for stakeholders)
	- checked by the user / stakeholder
	- validation testing
	- factory acceptance test
		- let user, client or stakeholder test the system and see whether they can accept it or not
	- blackbox testing
		- Looking only at the interactions between user and the system (none of the internals, like the code itself)
- User testing
	- users test the systems in real environments and report back
	- alpha and beta testing
- regression testing
	- re-test the system to check that newly introduced code has not broken what was already there
- partition testing
	- Identify groups of inputs with common characteristics
	- test each group with at least one test case
	- input and output are in different partitions
- Implementation testing
- operation testing


Automated testing
- what
	- running tests automatically
	- use some libraries like the unit test library for python
		- set up testing environments and run your tests
		- get a comprehensive review of the results of your tests
			- sometimes also coverage reports
- benefits
	- makes the process way easier


Unit testing
- test individual components in isolation
- unit - individual function or method


test coverage
- what
	- types
		- function coverage
			- each function is called at least once in testing
		- statement coverage 
			- each statement is tested at least once
		- edge coverage
			- each edge in graphical representation traveled at least once
		- condition coverage
			- Every condition evaluated to true at least once and false at least once
			- atomic condition coverage
				- every condition in the program has been tested


Architecture vs. design
- Architecture
	- the macro, high level structure and system quality tradeoffs
	- what components and how they interact
- Design
	- the micro, classes, functions, design patterns and more
	- How components actually operate


Software design
- what
	- identify and describe the fundamental software system abstractions and relationships
	- a description of the structure of the software to be implemented
		- data models
		- structures
		- interfaces between system components
		- algorithms
	- developed iteratively
	- design outputs
		- system architecture
		- database specification
		- interface specification
		- component specification


configuration management
- the general process of managing a changing software system
- support the system integration process so that all developers can access the project code and documents in a controlled way, find out what changes have been made, and compile and link components to create a system
- 3 fundamental activities
	- Version management
		- facilities to coordinate development by several programmers
		- stop one developer overwriting code that has been submitted to the system by someone else.
	- System integration
		- define what versions of components are used to create each version of a system
		- used to build a system automatically by compiling and linking the required components.
	- Problem tracking
		- allow users to report bugs and other problems
		 - allow all developers to see who is working on problems and when they are fixed.


SOLID
	- 5 principles of OO design
- single responsibility
	- system does one thing and one thing only
	- Changes affect less of system, easier to understand
- open-closeness
	- a class is open to extensions (building on top of the class)
	- closed for modifications -> never change internals that are already in use
- Liskov substitution
	- If a class depends on another class implementation, it should work with all subtypes
	- A depends on B, C inherits from B, A can use C instead of B
- interface segregation
	- Have multiple interfaces instead of just one for different use cases of a component
	- segregate interfaces based on specialization
- dependency inversion
	- If dependency, depend on something in abstraction, not in concrete class
	- f.x. depends on sorting algorithm, use abstract sorting algorithm


Design patterns
- what
	- good practices / proven solutions for designing classes and their relationships
	- support high-level, concept reuse
	- pattern
		- timeless entity that can be reused in different contexts
		- a description of the problem and the essence of its solution
		- a well-tried solution to a common problem, not a detailed specification
		- a vocabulary for talking about a design
		- a way of reusing the knowledge and experience of other designers
	- anti-pattern
		- solutions that are proved to not work well
	- The four essential elements of design patterns
		- A name
		- A description of the problem area, explain when to apply
		- A solution description
			- parts of the design solution
			- relationships
			- responsibilities
			- not a concrete design description
			- a template for a design solution that can be instantiated in different ways.
		- the consequences—the results and trade-offs—of applying the pattern.
- Issues
	- over-reliance on design patterns is never a good thing
		- not everything is a pattern
	- application of patterns changes over time
- Evaluation
	- often use SOLID or previous knowledge / experience


Gang-of-four patterns
- what
	- 23 patterns that became very influential
	- the original design pattern book
	- categories
		- creational
		- structural
		- beheavioral
- Issues
	- some patterns have not proved to be timeless

Abstract objects
- include general operations applicable in all situations

Concrete objects
- instance of class


Singleton pattern (creational)
- what
	- Ensure that a class has only one instance and provide global access to that instance
	- The singleton object is initialized only when it’s requested for the first time
	- getInstance() method to get singleton
	- how
		- Make the default constructor private
		- Create a static creation method that acts as a constructor
			- this method calls the private constructor to create an object and saves it in a static field
			- following calls return the cached object.
- Issues
	- violates single responsibility
		- make sure single instance
		- provides global access to controller
- when 
	- a class in your program should have just a single instance available to all clients
	- The Singleton pattern can mask bad design, for instance, when the components of the program know too much about each other.


factory pattern  (creational)
- what
	- Decouple creator from product
		- creator creates product
		- interface is a controller
	- subclasses may return different types of products only if these products have a common base class or interface
	- creator class
		- declares the factory method to return the product
	- products should have the same interface
- When
	- discover new product type (that can use the same interface) and want to implement it without breaking existing client code
- Issues
	- a lot of subclasses required, may become a mess
- Benefits
	- you can introduce new types of products into the program without breaking existing client code


adapter pattern (structural)
- what
	- Allow objects with incompatible interfaces to collaborate
	- adapt data in order to use a specific interface
		- realizes an interface, and connects it to a service
	- how
		- client
			- a class that contains existing business logic
			- has client interface
		- Service
			- some useful class with an incompatible interface to client
		- Adapter
			- wraps the service object 
			- defines an interface to the service object that is compatible with the client object
	- Adapter
		- special object that converts interface of some object so that another object can understand it
		- wraps the other object to hide its complexity
	- two-way adapters also exist
	- class adapter
		- when multiple inheritance is allowed
		- inherit from client and service, and combine their functionalities in one class
	- SOLID
		- open-closed
		- single-responsibility
- Benefits
	- Client doesn't get coupled to the adapter class (like it would if it were translating the service on its own)
- when
	- f.x. XML to JSON
- Issues
	- if the service class can be modified, do that instead of introducing extra complexity


facade pattern  (structural)
- what
	- Tidy up the interfaces to a number of related objects that have often been developed incrementally
	- a class that provides a simple interface to a complex subsystem which contains lots of moving parts
	- includes only those features that clients really care about.
		- limited functionality in comparison to working with the subsystem directly. 
	- SOLID
		- interface segregation -> can have multiple facades
		- single responsibility
- example
	- API
- Issues
	- limits the use of what lies behind it


decorator pattern (structural)
- what
	- Allow for the possibility of extending the functionality of an existing class at run-time.
		- take something that exists and put something on top of it
		- attach new behaviors to objects by placing object inside special wrapper objects that contain the behaviors.
			- define same interface + something new
	- The problem : Inheritance is static
		- can’t alter the behavior of an existing object at runtime
	- SOLID
		- interface segregation
		- open-closeness
- example
	- Need to add functionality to class, but cannot modify class directly
	- Subclasses can have just one parent class. In most languages, inheritance doesn’t let a class inherit behaviors of multiple classes at the same time.
- issues
	- can result in many layers of wrappers


observer pattern  (behavioral)
- what
	- Tell several objects that the state of some other object has changed
	- Separate the display of the state of an object from the object itself and allows alternative displays to be provided. 
		- When the object state changes, all displays are automatically notified and updated to reflect the change.
	- two abstract objects
		- subject
		- observer (corresponding to a display)
	- two concrete objects inerhiting from the abstract objects
		- contreteSubject
			- contains state to be displayed
			- can add and remove observers
			- can notify when state is changed
		- conreteObject
			- maintains a copy of the state of its subject
			- implements update() interface of observer
			- displays state and reflects changes when state is updated
	- Minimal coupling -> observer knows only the abstract observer
	- All alternative presentations should support interaction and, when the state is changed, all displays must be updated.
	- SOLID
		- open-close -> oberver and subject classes are always the same
		- liskov -> concrete can be swapped out
- Example
	- button
- Issues
	- optimizatinos that enhance display performance are impractical
	- changes to subject may cause a set of linked updates to observer to be generated, some of which unnecessary
- when
	- provide multiple displays of state information
	- when not necessary for the object that maintains the state information to know about the specific display formats used.


strategy pattern (behavioral)
- what
	- take a class that does something specific in a lot of different ways and extract all of these algorithms into separate classes called _strategies_.
	- client selects strategy
	- how
		- context
			- delegates work to a linked strategy object
			- setStrategy
			- runStrategy
			- Only aware of strategy interface
		- strategy interface
			- common to all concrete strategies
			- execute()
		- concrete strategy
			- implements strategy
			- execute()
		- client
			- creates strategies and feeds to context
			- asks context to run strategy
- Benefits
	- context becomes independent of concrete strategies
		- you can add new algorithms or modify existing ones without changing the code of the context or other strategies.
		- You can swap algorithms used inside an object at runtime.
	- You can isolate the implementation details of an algorithm from the code that uses it.
- Issues
	- If you only have a couple of algorithms and they rarely change, no reason to overcomplicate the program
	- Clients must be aware of the differences between strategies to be able to select a proper one.


Iterator pattern
- what 
	- Provide a standard way of accessing the elements in a collection, irrespective of how that collection is implemented (Iterator pattern).


Safety
- ability of a system to operate without catastrophic failure
	- injury, loss of life, environmental, financial, economic impact


Dependability
- what
	- a property of the system that reflects its trustworthiness
	- covers the related systems attributes of availability, reliability, safety, and security.
	- the degree of confidence a user has that the system will operate as they expect
		- the system will not ‘fail’ in normal use.
	- Types of failure
		- hardware failure
		- software failure
		- operational failure
	- Trustworthiness and usefulness are not the same
		- if very useful, you might tolerate some failure
	- fault tolerance
- Issues
	- more important than their detailed functionality because:
		- System failures affect a large number of people
			- Failure may mean that normal business is impossible.
		- Users often reject systems that are unreliable, unsafe, or insecure
			- tarnish reputation of producer
		- System failure costs may be enormous
		- Undependable systems may cause information loss
			- Data is expensive to collect and maintain
				- sometimes worth much more than the computer system (recovery and the like)
	- dependable systems have to include redundant code to 
		- help them monitor themselves
		- detect erroneous states
		- recover from faults before failures occur
	- affects the performance of systems -> overhead
		- trade off performance and dependability
	- Because of extra design, implementation, and validation costs, increasing the dependability of a system significantly increases development costs.
		- validate that system meets requirements
		- prove to external regulators that the system is safe
- evaluation
	- non-numeric


dimensions of dependability
- Availability
	- the probability that it will be up and running and able to deliver useful services to users at any given time
	- The probability that a system, at a point in time, will be operational and able to deliver the requested services.
- Reliability 
	- the probability, over a given period of time, that the system will correctly deliver services as expected by the user.
	- the probability that the system’s services will be delivered as defined in the system specification.
- Safety Informally
	- how likely it is that the system will cause damage to people or its environment.
- Security Informally
	- how likely it is that the system can resist accidental or deliberate intrusions.


system properties as dependability properties:
- Repairability 
	- diagnose problems
	- access components
	- fix system failures quickly
- Maintainability 
	- how easy to introduce new requirements without failure
- Survivability
	- the ability of a system to continue to deliver service whilst under attack and, potentially, whilst part of the system is disabled.
	- identify key system components and ensure that they can deliver a minimal service. 
		- resistance to attack
		- attack recognition
		- recovery from damage caused by attack
- Error tolerance
	- the extent to which the system has been designed so that user input errors are avoided and tolerated
	- system should detect user errors and fix them or request user to reinput data


Safety-critical systems
- systems where it is essential that system operation is always safe
	- the system should never damage people or the system’s environment even if the system fails
- types
	- Primary safety-critical software 
		- software that is embedded as a controller in a system
		- may cause a hardware malfunction, which results in human injury or environmental damage.
	- Secondary safety-critical software
		- can indirectly result in an injury.
- The key to assuring safety 
	- ensure that accidents do not occur 
	- or that the consequences of an accident are minimal


Security 
- a system attribute
	- reflects the ability of the system to protect itself from external attacks, which may be accidental or deliberate
	- most general-purpose computers are now networked and are therefore accessible by outsiders


Security vs. safety
- security is a prerequisite for safety
- a system can operate and protect itself from intrusion


Attacks and threats
- what
	- External actors threatening the dependability of our software
	- The majority of external attacks focus on system infrastructures 
		- infrastructure components (e.g., web browsers) are well known and widely available.
	- In networked systems there are 3 main types of security threats: (threats to)
		- confidentiality of the system and its data 
			- unauthorized access to information
			- interaction threat
		- integrity of the system and its data 
			- damage or corrupt the software or its data
			- modification and fabrication threats
		- availability of the system and its data
			- restrict access to the software or its data for authorized users.
			- interruption thrat
	- In practice, most vulnerabilities in sociotechnical systems result from human failings rather than technical problems.
- evaluate
	- probability
	- control
	- feasible


Security engineering 
- what 
	- development and evolution of systems that can resist malicious attacks, intended to damage the system or its data
	- Security activites (often by system managers)
		- User and permission management 
		- System software deployment and maintenance 
		- Attack monitoring, detection and recovery 
	- Security risk assessment and management 
		- Risk management
			- balance losses against costs of security procedures that may reduce these losses
		- organizational security policy. 
			- applies to all systems and should set out what should and should not be allowed.
				- helps to identify risks and threats that might arise
	- Risk assessment 
		- starts before the decision to acquire the system has been made 
		- A staged process
			- Preliminary risk assessment (requierment elicitation stage)
				- decide if an adequate level of security can be achieved at a reasonable cost
					- derive specific security requirements for the system
			- Life-cycle risk assessment (system development life cycle)
				- informed by the technical system design and implementation decisions
				- changes to the security requirements 
				- identify known and potential vulnerabilities 
					- used to inform decisions about the system functionality, implementation testing and deployment
			- Operational risk assessment (after deployment)
				- Fix incorrect security assumptions from earlier stages
				- Organizational changes may mean that the system is used in different ways from those originally planned


application security vs infrastructure security:
- Application security 
	- Software Engineers ensure that the system is designed to resist attacks.
- Infrastructure security
	- a management problem where system managers configure the infrastructure to resist attacks.
	- System managers
		- set up the infrastructure to make the most effective use of available infrastructure security features
		- repair infrastructure security vulnerabilities that come to light as the software is used.
- Operation security
	- while running, ensure safe, and keep running


Misuse cases 
- scenarios that represent malicious interactions with a system
- use 
	- to discuss and identify possible threats 
	- determine the system’s security requirements
- can be used alongside use cases when deriving the system requirements


designing for security
- Planning stage
	- know what needs to be protected
	- be aware of vulnerabilities inherent in the design decisions that you've made
	- find steps to reduce the associated risks.
	- you need to take security issues into account during the systems design process.
- Architectural design
	- how do architectural design decisions affect the security of a system?
	- Fundamental issues
		- Protection
			- how should the system be organized so that critical assets can be protected against external attack?
		- Distribution
			- how should system assets be distributed so that the effects of a successful attack are minimized?
		- potentially conflicting
			- Everything in one place with a looot of protection vs. single point of failure and performance
			- Everything decoupled vs. protecting each and every end-point
	- Architecture and security
		- client-server when protection of data is a critical requirement
			- protection mechanisms built into the server
			- associated losses and cost of recovery if protection compromised is high
			- vulnerable to denial of service attacks
		- distributed object architecture
			- if denial of service attack are a major risk
			- system assets are distributed across a number of different platforms, with separate protection mechanisms used for each of these
		- in many cases, the architectural style that is most suitable for meeting the security requirements may not be the best one for meeting the performance requirements
- Good practice
	- what is accepted good practice when designing secure systems?
- Design for deployment
	- what support should be designed into systems to avoid the introduction of vulnerabilities when a system is deployed for use?
- Designing a system to be secure inevitably involves compromises
	- security measures often require a lot of additional computation and so affect the overall performance of a system.
	- tensions between security and usability
		- additional security means that they can’t use the system
		- have to find a balance between security, performance, and usability


Levels of protection
- Platform-level protection 
	- platform on which the system runs (infractructure / computer)
- Application-level protection
	- access to the applicaiton (authentication and authorization)
- Record-level protection 
	- access to specific records (encryption)


General design guidelines for security
- what 
	- two principal uses:
		- raise awareness of security issues in a software engineering team.
		- used as a review checklist that can be used in the system validation process. 

general security design guidelines
- Base security decisions on an explicit security policy
	- a high-level statement that sets out fundamental security conditions for an organization
	- defines the ‘what’ of security rather than the ‘how’, so the policy should not define the mechanisms to be used to provide and enforce security.
- Avoid a single point of failure
	- never rely on a single mechanism to ensure security
	- ‘defense in depth’ -> employ several different techniques
- Fail securely
	- System failures are inevitable in all systems 
	- When the system fails, you should not use fallback procedures that are less secure than the system itself
- Balance security and usability
	- demands of security and usability are often contradictory
	- As you add security features to a system, it is inevitable that it will become less usable.
- Log user actions
	- always maintain a log of user actions
	- This log should record 
		- who did what
		- the assets used
		- time and date of the action
	- if you maintain this as a list of executable commands, you have the option of replaying the log to recover from failures. 
	- tools allow you to analyze the log and detect potentially anomalous actions
- Use redundancy and diversity to reduce risk
	- Redundancy
		- maintain more than one version of software or data in a system 
	- Diversity
		- the different versions should not rely on the same platform or be implemented using the same technologies
		- platform or technology vulnerabilities will not affect all versions
- Validate all inputs
	- never accept any input without applying some checks to it
	- define the checks that should be applied as part of the requirements
- Compartmentalize your assets
	- organize the information in a system into compartments. 
		- Users should only have access to the information that they need, rather than to all of the information in a system.
	- effects of an attack may be contained
		- not all information affected at once
- Design for deployment
	- Common issue is that the system is not configured correctly when it is deployed in its operational environment
	- design your system to simplify deployment in the customer’s environment 
	- check for potential configuration errors and omissions in the deployed system
- Design for recoverability
	- always design your system with the assumption that a security failure could occur. 
	- think about how to
		- recover from possible failures and restore the system to a secure operational state.
		- make the system resilient so that it survives to deliver essential services to users.


Survivability or resilience 
- what
	- property of a system as a whole
	- reflects its ability to continue to deliver essential business or mission-critical services to legitimate users 
		- while it is under attack 
		- after part of the system has been damaged (system failure or attack)
	- achieving survivability depends on three complementary strategies:
		- Resistance 
			- Build capabilities into the system to repel attacks
		- Recognition 
			- Build capabilities into the system to detect attacks and failures and assess the resultant damage
		- Recovery
			- capability to deliver essential services while under attack
			- capability to recover full functionality after an attack


8 principles of ethics in software engineering
- PUBLIC 
	- Software engineers shall act consistently with the public interest.
- CLIENT AND EMPLOYER 
	- Software engineers shall act in a manner that is in the best interests of their client and employer consistent with the public interest.
- PRODUCT 
	- Software engineers shall ensure that their products and related modifications meet the highest professional standards possible.
- JUDGMENT
	- Software engineers shall maintain integrity and independence in their professional judgment.
- MANAGEMENT 
	- Software engineering managers and leaders shall subscribe to and promote an ethical approach to the management of software development and maintenance.
- PROFESSION 
	- Software engineers shall advance the integrity and reputation of the profession consistent with the public interest.
- COLLEAGUES 
	- Software engineers shall be fair to and supportive of their colleagues.
- SELF 
	- Software engineers shall participate in lifelong learning regarding the practice of their profession and shall promote an ethical approach to the practice of the profession.



Biases
- Confimation bias -> pay more attention to stuff that confirms our thoughts
	- traceability
	- TDD
- Optimism bias -> produce overly optimistic estimates, judgements, predictions
- framing effect -> focus disproportionately on one thing (frame question in specific manner)
	- adressing by both individuals
- hyperbolic discoutning -> prefer less reward now, to big reward later
- anchoring /adjustment bias -> sticking to what has been proposed
	- adress with parallel estimation
	- estimates based on expert opinion or model-based estimates
- Availability bias -> sticking to what is known / familiar (but not necessarily correct)
	- participatory decisions
	- traceability
	- retrospectives
- Bandwagon -> adjusting to majority opinion


Debiasing
- what
	- reducing biases in processes
	- It is easier to
		- debias task rather than person
	- Examples of debiasing techniques
		- Planning poker to prevent anchoring bias in effort estimation [P38].
		- Reference class forecasting or model-based forecasting to mitigate optimism in effort estimation
		- Ontology-based documentation to mitigate availability bias
		- Directly asking for disconfirmatory evidence to reduce confirmation bias
		- Generating multiple, diverse problem formulations and solution candidates to mitigate framing effects
		- Using confirmation bias metrics to select less-biased testers
		- For security, employing independent penetration testing specialists to reduce confirmation bias [83].
		- ﻿﻿﻿Designating a devil's advocate in retrospective meetings to avoid groupthink
		- retrospectives where you explicitly exchange / share information between team members
- Benefits
	- more efficient, and more correct work


Security properties
- Confidentiality
- integrity
- availability


tradeoffs in security
- risk 
- value
- performance
- user acceptance


Policies
- what
	- a way of evaluating for security applications
	- assets
		- what kind of data do we have of value
		- how exposed are these assets
	- procedures
		- what are we doing to protect assets
	- responsibilities
		- who is responsible for asserting the security of assets
	- existing policies
		- procedures or responsibilities that are already in place


Programming principles in context of security
- limit visibility of data in components
	- encapsulate as much as you need
- Always check inputs
	- f.x. sql injection
- Handle all exceptions
	- when something goes wrong, the application doesn't just crash
- Provide restart
	- if crash, then it should be able to work again
- Check boundaries of data
	- overflow attacks (or errors)
	- check if correct type


Host-target development
- what 
	- host-target model
		- Software is developed on one computer (the host), but runs on a separate machine (the target). 
		- host -> development platform 
		- execution platform -> target
	- platform 
		- hardware
		- installed operating system
		- supporting software
			- database management system
			- development platforms
			- interactive development environments
- Issues
	- cannot run tests in the same environment as the system is built -> needs to be simulated
 
test driven development  TDD
- what
	- Writing executable tests before the code
		- automated testing
			- ideally the tests run automatically after every change of the program (continuous integration)
	- Requirements have to be clarified directly
	- focus on requirements, rather than implementation
	- an approach to program development in which you interleave testing and code development
	- code developed incrementally, along with a test for that increment
		- don’t move on to the next increment until the code that you have developed passes its test.
	- works in plan-driven and agile
- Benefits
	- Fewer large integration problems Issues with test-driven development
	- everything (should be) tested.
		- defects discovered early in the development process
		- Regression testing 
			- can always check that changes to the program have not introduced new bugs.
			- reduced cost of regression testing
				- whether new code has introduced new bugs
	- helps programmers clarify their ideas of what a code segment is actually supposed to do (problem understanding)
	- code coverage
		- every code segment you write should have at least one test
	- has been shown to lead to improved code quality; in others, the results have been inconclusive.
	- The tests themselves act as a form of documentation that describe what the code should be doing
- Issues
	- Few people use it consistently
	- Not always possible (E.g., graphical toolkits)
	- Feels unnatural to many
	- testing needs to be very good
		- if you have incomplete knowledge or understanding, then test-driven development won’t help. 
		- If you forget to write a test for this, then the code to check will never be included in the program.
	- Simplified debugging When a test fails
		- it should be obvious where the problem lies. 
	- you still need a system testing process to validate the system
		- requirements are appropriate to stakeholders
		- performance, reliability, and checks that the system does not do things that it shouldn’t do, 
- when
	- new software development where the functionality is either implemented in new code or by using well-tested standard libraries.
	- small and medium-sized projects.



Model based engineering MBE
- what
	- MBE process is a process in which software models play an important role although they are not necessarily the key artifacts of the development.
	- used more in specific areas
	- types
		- simulations of environments
			- automotive, avionic, railway, etc.
		- model based testing
			- generating tests from models or requirements (very nice)
		- domain-specific languages (DSL)
			- languages made for non-programming people
	- Process
		- source model <- input
			- UML model f.i.
		- transformation (compiler)
			- reads source model and creates a target model
			- uses a source language, and writes code in target language 
		- target model <- output
			- code
	- Modelling languages
		- grammar    -> textual, mathematical or natural language
		- meta model -> a model
- Benefits
	- code is generic
	- Higher quality code
	- More focus on engineering
	- platform independent
	- quickly try out new things
	- faster development
		- skip writing repetitive code that is easy to generate anyway
		- software product lines (almost the same software many times)
			- don't have to build similar applications from scratch every time
- When
	- complex / large systems
	- safety critical systems (that haave to be correct)
- issues
	- individual and very specific code may be hard to generate
	- performance and maintainability may be a case
	- version control cannot be done
	- acceptance -> proud programmers
	- resistance -> new tech, new workflow
	- tooling    -> graphical modeling hard to build and use


model driven engineering MDE
- what
	- concerned with all aspects of the software engineering process
	- models rather than programs are the principal outputs of the development process
		- programs that execute on a hardware/software platform are generated automatically from the models
	- allows engineers to think about systems at a high level of abstraction
		- no concern for the details of their implementation. 
- Benefits
	- reduces the likelihood of errors
	- speeds up the design and implementation process
	- allows for the creation of reusable, platform-independent application models
	- system implementations can be generated for different platforms from the same model
	- rapid rehosting
- Issues 
	- abstractions that are supported by the model are not always the right abstractions for implementation
	- the arguments for platform independence are only valid for large long-lifetime systems where the platforms become obsolete during a system’s lifetime
	- requirements engineering, security and dependability, integration with legacy systems, and testing.


Model driven architecture
- a model-focused approach to software design and implementation 
	- uses a sub-set of UML models to describe a system.
- 3 types of abstract system models should be produced
	- Computation independent model (CIM) / domain models
		- may develop several different CIMs
			- different views of the system
			- identify important security abstractions per field, such as security
	- platform independent model (PIM) 
		- models operation of the system without reference to its implementation
		- UML models that show the static system structure and how it responds to external and internal events.
	- Platform specific models (PSM) 
		- transformations of the PIM model 
		- separate PSM for each application platform
		- layers of PSM
			- each layer adding some PIM detail


Three key model types to create an executable sub-set of UML
- Domain models
	- identify the principal concerns in the system
	- defined using UML class diagrams that include objects, attributes, and associations.
- Class models 
	- classes are defined, along with their attributes and operations.
- State models 
	- state diagram is associated with each class and is used to describe the lifecycle of the class


model automation
- generating code
- generating tests


modeling languages
- grammar model
- meta model


law of demeter -> unit has limited knowledge of other units (only talk to friends, never strangers)

development lifecycle
- plan
- code
- build
- test
- release
- deploy
- -- maintenance ->
- operate
- monitor
- plan -> cycle



measurement theory in software engineering
- what
	- ISO / IEC 2502n - measuring software quality


measurements
- base measurement
- derived measures
- indicator
- information product



infrastructure for complex applications may include:
- an operating system platform, such as Linux or Windows
- other generic applications that run on that system, such as web browsers and e-mail clients
- a database management system
- middleware that supports distributed computing and database access
- libraries of reusable components that are used by the application software



design for failure
- what
	- design with the expectation of something failing, so that the system can handle it.
- Benefits
	- stuff can go wrong (potentially) without the user noticing
- Issues
	- may introduce overhead


Why diversity and inclusion (in software engineering)
- Ethical
	- reflect society (like the customer base you are building for)
	- value diversity -- because it's the right thing to do
	- Recognize talents -- a diverse population brings diverse skills and talents.
- Economic / social
	- Diversity leads to
		- Innovation 
		- creativity
	- Productivity -- tends to increase with diversity
	- Recruitment -- a larger pool to pick workers from / talent you can attract and hire
	- turnover -- more people will stay if they feel included
	- Direct economic impact
		- Having multiple talents
		- reflecting society
		- more diverse products / projects
			- Accessibility is considered earlier, and the needs of the user base in general

Equality
- people are treated the same
- everyone stands on equal ground


Equity
- fair and impartial
	- you being in a wheelchair doesn't take any opportunities from you

Diversity
- what
	- Diversity is of vital importance in software engineering
		- diverse perspectives
		- diverse toolsets
		- better understanding
		- increased productivity
		- Ethical and economic benefits
	- Inclusion is not the same as diversity
		- Inclusion is accepting diverse kinds of people
		- Everyone on the team feels welcome, included, safe
	- gender diversity has a positive effect on productivity
		- the Socio-emotional behavior and non-aggressive strategies attributed to women in teams could imply a more positive attitude towards teamwork and collaboration in gender diverse projects
		- all male groups tend to be overly competititve
	- Gender diversity has a negative effect on turnover (less turnover)
		- welcoming communities should exhibit less turnover
	- The higher the median tenure in the project, the less likely it is there will be people joining or leaving the project
		- more experienced teams will neither persist, nor will the attrition be lower.
	- When forming or recruiting a software team, increased gender and tenure diversity are associated with greater productivity (consistent with IP)
	- brings different perspectives together
	- Higher tenure diversity may increase attrition
		- mitigated when more experienced people are present (?)
- Issues
	- Non-diverse teams
		- build non-diverse products
			- less relevant issues are raised (because the developers aren't aware of them)
		- may lead to discrimination, often accidentally
		- Less consideration of diverse populations and circumstances
			- accessibility
			- less of a filter for something that may be insensitive
			- lack of people havign the human experience to notice certain issues
	- Why non-diverse teams exist
		- Bad interviewing practices and unconscious biases
		- lack of minorities joining the software engineering workforce


DevOps
- what
	- the team developing the software also runs operates and runs it so that it continuously evolves
		- one team building and maintaining the system
	- Use of continuous practices
		- embrace a lot of automation
	- Agile
		- a lot of monitoring for gathering feedback on newest release
- Considerations
	- must use compatible architecture
		- how to design product that you can deploy regularly
		- how to roll back changes
		- how to monitor the system
	- configuration management, testing and infrastructure must all be gooood
	- teams need to handle a lot of stuff
		- Including coordination of teams
- When
	- Likes microservice architectures very much


continuous deployment
- what
	- CI + building and deploying automatically on a regular basis
		- can have deploy button
	- Requires
		- a very good test suite
			- tests sufficient to tell whether you can push this to live
			- regression, unit, and system testing
- When 
	- environments like XP or microservice architecture
- Issues
	- When releases are confined to some rules
		- regulations -> certificiations may require audit of application
		- android / istore -> require audit of application


continuous integration  CI
- what 
	- As soon as work on a task is complete (once pushed), it is integrated into the whole system after any such integration, all the unit tests in the system must pass
	- originates from xtreme programming
	- Requires CI solution
	- cannot commit unless the build runs without error in automated test suite
- Benefits
	- allows problems caused by the interactions between different developers to be discovered and repaired as soon as possible
- When 
	- Automated testing needs to be sufficient
- Issues
	- If the system is very large, it may take a long time to build and test. It is therefore impractical to build that system several times per day.
	- If the development platform is different from the target platform
		- may not be possible to run system tests in the developer’s private workspace. There may be differences in hardware, operating system, or installed software. Therefore more time is required for testing the system
	- daily build systems are better for large systems
- evaluation
	- evaluating tests


continuous experimentation
- what
	- run experiments by comparing divverent versions of software in production environment
	- Continuously run experiments in live deployment
	- Uses some methods to collect data
		- The data is then analyzed to see the results of changes
			- base measurement -> raw measurement
			- derived measures -> function to combine base measurements
			- indicator        -> categorical criteria from derived measures
			- information product -> dashboard to visualize information
- Benefits
	- This is high level user testing (essentially beta testing without report back)
	- get feedback straight from real-world use of system
- Issues
	- you are running sometimes untested software on live servers
		- customer dissatisfaction
		- other issues


Continuous experimentation methods
- A/B testing
	- two versions, 50/50 split who gets which version
- canary release
	- two or more version, random who gets what, but with some distribution
		- 95 / 5 f.x.
- dark launch
	- new release tested with input from user
	- user is not actually served the new release, nor is he aware of the side effects of him using the old release


product quality 
- Dependability
product quality-in-use
- usability


coupling
- the degree of interdependence between software modules
	- the strength of relationships between modules
	- probability that code unit B will break after unknown change to code in unit A
- Well-structured and designed 
- systems have low coupling


Scenario
- what
	- real-life examples
		- interaction sessions
		- one or small number of possible interactions
		- Should have a lot of detail
	- Nice for validation
	- A description of flow of events


personas
- a way of imagining different individuals using our product


low-code
- What
	- Alternative method of building software, using models instead
	- application development platforms that enable rapid application delivery with minimmal hand-coding, and quick setup and deployment
	- How does it work
		- interactive visual programming environments
		- model-driven
		- templates and flows
	- Automate repetititve software development tasks
	- speeding up the production of solutions that serve business needs by abstracting the coding for the common reusable software components and allocating developer effort to tasks closer to business outcomes
- Benefits
	- Increased productivity and security (lessen human errors)
	- shorten development, deployment, and maintenance cycle
	- fewer resources to complete a solution means decreased costs
- Issues
	- can be constrained
	- the best tools are very expensive
	- hard for programmers to transition


Low-code application platform -- LCAP
- OutSystems
- SalesForce


Open source
- Benefits
- Issues


Traceability policy
- what
	- define the relationships between each requirement and the system design
	- define how these records should be maintained
	- identify requirements to be able to talk about and connect them
		- tests
		- dependencies
		- change request


Non-functional requirements vs. functional requirements
- non-functional requirements
	- qualities of the system
		- quick
		- maintainable
		- secure
- functional requirements
	- what the system should do
		- ..Actor.. should be able to do X


Productivity considerations
- programming languages
	- how complicated is it
	- garbage collection etc
- documentation
	- how much, how well, and how
	- how well does this fit our needs
- Tools
	- syntax completion
	- error highlighting
	- linting
	- help the speed of finding errors and developing the applicaiton
- practices
	- stuff we do
	- automated testing and more
- agile
	- associated with higher productivity
	- just-in-time planning
- Completeness of design
	- if architecture is fixed, then we're faster / more productive
- Process maturity
	- are people used to all the steps
- Requirements stabitlity
	- how much are the requirements changing
	- how much are we changing
- Time fragmentation
	- doing something for a long uninterrupted time
- office layout
	- own office or home office, more productive
- Personality
	- and mix of personalities
	- diverse sets of personalities improve productivity
- happiness
	- if happy, happiiii
- Communication
	- the better it is, the more productive people become
- Cameraderie
	- how well does the team work together
	- is everyone happy together
- Psychological safety
	- an atmosphere that allows for you to make mistakes
	- Productivity up
- Respect
	- among individuals in team


Group development model (stub)
- forming
- storming
- norming
- performing
- adjourning


Testing in agile
- acceptance testing every 2-4 weeks with customer representative


Scalability
- what
	- the ability to scale systems
		- can handle more data
		- can handle more traffic
		- can handle more developers working on the system
	- Practices that help scalability
		- distribution
- Considerations
	- architecture
	- context of use


Stakeholder
- what
	- someone with a stake in the project
	- A person or role that is affected by the system in some way
	- Anyone who should have direct or indirect influence on the system requirements
	- example stakeholders
		- end-users
		- customers
		- clients
		- management
		- store-clerks
		- developers
		- project-owner
		- regulatory certification authority
		- trade-union representatives
		- other systems
- Benefits
	- knowing who will use your system helps you develop a more appropriate system
		- this means that less changes are required and less erorrs
			- less development
			- less cost
			- less maintenance
			- less work
- When
	- ALWAYS

