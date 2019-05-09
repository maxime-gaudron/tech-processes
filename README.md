# tech-processes

Gathering all the processes I'm used to for tech.

## Development processes

### Definition of done

__Developer:__ _It's done._     
__PM:__ _I don't see it live._  
__Developer:__ _Ah, development is done, it's not deployed._  
__QA:__ _And what about testing ?._  

Every step of the development process should have it's own definition of done attached to it to ensure clear communication and to manage expectations.

- Todo
  - Is there any third party dependencies
  - Is the outcome clear
  - Is there any deadline
  - Who are the stakeholders
- Ongoing
  - Is the issue assigned
- Code review
  - Was the CR need communicated by the assignee
  - Does it pass the CR checklist
  - Was it moved to "QA" or moved back to "Ongoing"
  - Is the assignee aware of the outcome
- QA
  - Was the QA need communicated by the assignee/reviewer
  - Does it pass the CR checklist
  - Was it moved to "Ready for release" or moved back to "Ongoing"
  - Is the assignee aware of the outcome
- Ready for release
  - Shall it be deployed with the next release
  - Is it assigned with a release number
  - Is the stakeholder aware of the status
- Done
  - Issue is closed with the proper resolution
  - It is part of the corresponding release
  - The stakeholder is aware of the status

Note: Above are the base status for a small tech team, CR and QA can each be subdivided in "Awaiting for X" and "In X" to avoid duplicate work by multiple persons.

### DCVS processes

#### Branching model

- [Git flow](https://nvie.com/posts/a-successful-git-branching-model/)
- [Github flow](https://guides.github.com/introduction/flow/)

The branching model decision should be based on the complexity and advancement of the project, team size, environments available and testing plan.

#### Commit messages

- [Git commit messages](https://chris.beams.io/posts/git-commit/)

Commit messages should always contain a reference to the ticket number or email describing the reason of the change. Moreover tools such as Jira have DCVS integration allowing automatic linking of commit/branches/pull requests to the correct ticket.

#### Commit size

- Each commit should be meaningful by itself
- Small commits simplify reviews
- Rebasing & Squashing before merging simplify the history of the code

Thought: Technical debts is created due to the shortcuts taken given the environment at that time. The code itself is in the DCVS and the story around is in the issue tracking software. A bi-directionnal link between them and proper description is necessary, not for us today but for the next developer trying to understand the code.


### Code review checklist

What is the purpose of a code review ? 

- Ensure quality
- Have discussions
- Share information
- Share understanding
- Create a baseline
- Grow as a team

Who should do a code review ?  

- Developers of the same level or more senior
- Junior developers should review their peers code and be reviewed by their senior

What should be reviewed ?

#### First pass - Context
- Check the context in the issue tracking software
- Type of code - feature, bugfix, one time task
- How long will it stay - the longer, the most attention

#### Second pass - Cosmetic
- Indentation
- Naming consistency ( snake_case, CamelCase, ... )
- Naming intent ( is it meaningful ? )
- Coding standards ( PSR for PHP ? Standard for JS )
 
#### Third pass - Logic
- Good software practices - SOLID, KISS, DRY, SRP & SLA, ...
- Usage of design patterns - DiC, Strategy, Factory, ...
- Good architecture - Separation of business logic vs software architecture
- Logging & error handling - Does it degrade gracefully, meaningul logs & errors messages ?
- Scaling - How will it perform under load ?
- Tests - Is there any tests ? Shall we test ? 
     

Thoughts on testing: 

- [Testing pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)
- Good coding practices over tests

### Release process

#### Versioning

[Semantic versioning](https://semver.org) 

#### Before the release

- __Request per minutes__ check  
Will the current traffic impact the deployment ?
- __JIRA/Github release__  
Linked to jira/github release through release notes  
Are all the tickets "__Ready for release__" ?  
Are PR squashed, up to date, merged and branches removed
- __Communication__  
If any downtime, is it clearly communicated to the teams ?  
Is the customer service aware of the deployment ?

#### After the release
- __Infrastructure/APM__ checks overall and per server  
APM Web & CLI error rate   
CPU/RAM/Disk/Network usage  
Response time per transaction   
- __Customer feedback__ check  
Is there any issue discovered by the users ?   
- __Release on Jira__  
Move the tickets to "__Done__" with the proper resolution  
Set the release as "__Released__"  
- __Communication__  
Announce the release either on slack/email  

## Infrastructure

### Backup

#### First step - Backup strategy

First step is to recognize the sensible systems and data they contain. From there what is the backup strategy that should be applied :

- __What ?__  
Which systems have sensible ?  
- __Frequency__  
Which backup frequency should we use ?  
- __Encryption__  
Backups are sensible, which encryption should be used ?  
- __Encryption key storage__  
Where should the encryption key be saved ?  
- __Location__  
Once created, where should the backup be saved ?   
Multiple location ?

#### Second step - Backup usability

Having backup is the first step, integrating them in the development/testing process guarantees their usability. Backup can be 

- __Anonymisation__  
Is there any sensible customer data ? Phone number, email, address, name, CC, ... ?  
Is there any configuration value stored in the backup ?  
- __Staging export__  
Automated scheduled importation in the staging system  
- __Development export__  
Is all the data necessary ?  
Can we reduce the size ?

#### Third step - Disaster recovery

- __Communication__  
Customer service, Ops, ...  
General communication  
- __Incident report__

### Daily monitoring

Daily monitoring could be a role shared across the engineering team. Ideally a weekly rotation, every morning one of the team member checks the systems and create or follow up on issues.

- APM error rate, frontend & CLI, Infrastructure, Domain expiration, SSL certificate expiration
- GA, CVR across device/browser
- Issue creation for any anormalitity

### Adding new service

Third parties have different renewal and termination policies, two situations to avoid:  
 - Automatic renewal for lengthy contract.  
 - System shutdown due to termination of contract or payment failure.  

   - Signup with shared email
   - Which credit card ? Expiration date ?
   - Invoice details
   - Accounting email copy
   - Communication
   - Credentials sharing
   - Tax information
   - Documentation

### Staging system

   - How to reset / import / export data
   - Importance of up/down SQL migrations
   - How to reserve a staging environment
 
## Hiring processes

 - ATS
 - Hiring funnel
 - Scheduling tool
 - Score cards
 - Sanity code test
 - HR tech questions
 - Interview coding tests
 - Interview agenda
 - Code review test
 
## Team processes

Team processes should be kept to the bare minimum until the team encounter the need to add one.

Bare minimum :  

 - __Monthly Team retrospective__
     - __General team feeling__  
     Trace a line from sad to happy smiley on the whiteboard, ask the team members to quickly draw a face on a post-it, go to the board, stick it on the line and say a couple of words.
     - __Everybody's perspective__  
      - __Part one__ - Gather perspectives  
     Split the whiteboard in three areas, good, bad and ideas. Give each person 3-5 post-its and ask them to write their thoughts. After 10 minutes or so, ask everybody to stick the post-its in the right area and say a few words about it.   
      - __Part two__ - Cluster feedback  
       Remove the "good" and group the leftover post-its per cluster of ideas.
      - __Part three__ - Open perspectives  
     Once done,  give a marker and assign three "dots" to each person to be distributed between the cluster of ideas.  
      - __Part four__ - Discuss the topics, write down actionable tasks and assign them  
 - __Daily standup__  
     - __Part one__ - Announcements  
     - __Part two__ - Business as usual  
     Keep it short, 30-60 second per person   
     - __Part three__ - Discuss new processes.  
     Something didn't work, it's time to get a consensus, let one team member propose a change and the team to react on it. 
     
     
Tools:

 - [Retrospective generator](https://retromat.org/en/)

 
## Project processes

 - Ticketing system configuration

 Open all the transitions between states.  
 Remove sub-tasks.  
 Create "__Spike__" type.  
  
 - Statuses & Definition of Done
   - Backlog
   - Frozen
   - Todo
   - Ongoing
   - Review
   - QA
   - Ready for Release
   - Done 

   Note: Naming isn't tech specific.
    
 - Normal lane / Fast lane
 - Kanban / Scrum.  
 To be decided by the team, I would suggest to start with a Kanban process as a startup is unpredictable, given longer, larger projects scrum would fit too. it depends mainly on how much uncertainty you have
 - Issue
   - Types
     - Epic
     - Spike
     - Task
     - Bug  
   Note the lack of "sub-tasks" Ideally the project would be structured with epics and tasks attached to them to avoid many level of sub-sub-sub-tasks.
   - Template in the description field.  
   Issue tracking software allow adding a placeholder in the description field. This would act as a "code review checklist" reminding the people writing the issue to add as much details as possible.
     - Status quo
     - Acceptance criteria
     - QA todo
     - Notes
     - Dependencies
       - Translation keys
       - Credentials
       - Third party tools
       - Release date
 - Estimations
   - Tee-shirt vs Story point
   - [Cone of uncertainty](http://www.agilenutshell.com/cone_of_uncertainty)
 
## Inhouse

 - Issue tracking system
 - Service desk
 - Knowledge base  
 - Inventory management  
   Centralising suppliers details, overseeing hardward depreciation, warranties contracts and expiration dates, streamline procurement, ideally integrates with the Issue Tracking system.
 - On & off boarding
 - __Security__
   - Two factor authentication
   - Mobile device management
 - Password management
   - __Password manager__  
   Source of truth, all the sensible password, keys, certificates, ...
   - __GPG__  
   Per_fect for one time share or communication of sensible data to third parties.
 
 __Tools:__
 
  - [Gnu Privacy Guard](https://www.gnupg.org)
  - [Mailenvelope](https://www.mailvelope.com/en) - Plugs in browser and integrate to Gmail
  - [Passbolt](http://passbolt.com) - Cloud/On-premised open-source password manager
  - [Snipe-IT](http://snipeitapp.com) - Open-source inventory management
 
## Incident report

### Template

```
Post-mortem of incident on <DATE>

Timeline

22:30 CET: Incident begins
22:41 CET: A CC Agent reports an error in our Slack channel.

Time to response: 
22:50 CET: First engineer on the case

Time to mitigation:
23:05 CET: Systems stable

Description

Impact

Best possible description using any measure of impact.

Learnings

A bullet pointed list of things we learned from the incident.

Next Steps

A checklist of actionable items as outcomes of this issue.
```

__Notes:__  
The report should be accurate, factual and complete. Ideally involve multiple persons with different perspectives on the incident, Dev, QA, PM, Stakeholders ...  
The most important information you need to gather is __root cause__, __root cause__, __root cause__

## QA process

 - Testing tool
 - Manual / Automated
 - Test plans
 - X-tests / Regression tests / Feature tests / Exploratory tests
 - Device / Browser matrix
 - Payment tests
 - Test Credit Card
 
## Documentation

 - Confluence
 - Google docs
 
## Tools

 - Jira
 - Github
 - Slack
 - GPG
 - Static code analysis
 - Password manager
 - Inventory manager
 - AWS
 - Google organisation
 - ATS
 - Scheduling tool
