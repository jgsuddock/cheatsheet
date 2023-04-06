# Lean Manufacturing

## About

`Lean Manufacturing` is rooted in the [Toyota Production System](https://www.lean.org/lexicon-terms/toyota-production-system/) which became widely known in the 90's. Lean was translated from manufacturing to software development by Mary and Tom Poppendieck in [Lean Software Development](https://www.amazon.com/Lean-Software-Development-Agile-Toolkit/dp/0321) in 2003. Lean principles sturdily underpin the current DevOps movement with ideas centered around treating the software development process like a manufacturing production line.

## Primary resources:

- [https://kanbanize.com/lean-management/value-waste/what-is-5s-lean](https://kanbanize.com/lean-management/value-waste/what-is-5s-lean)
- [https://www.leanproduction.com/essence-of-lean/](https://www.leanproduction.com/essence-of-lean/)
- [https://hackernoon.com/7-wastes-in-lean-software-development-and-how-to-prevent-them-7bi3tqp](https://hackernoon.com/7-wastes-in-lean-software-development-and-how-to-prevent-them-7bi3tqp)

## The 5-S Pillars

The Foundation of Lean is the 5-S Pillars for managing the workspace. These were originally geared toward manufacturing workspace, but can easily be extrapolated to the software development workspace.

1. `Sort`: Keep only what is essential.  When in doubt, discard.
2. `Set in order`: Arrange items/environment for easy access and efficient workflow.
3. `Shine`: Keep the work area neat and tidy.  Don't let problems or messes build up.
4. `Standardize`: Make rules and follow them.  Prefer consistency over fragmentation.
5. `Sustain`: Do these things often.  Keep procedures up to date.  Optimize for sustainability.

## Reducing Waste

There's a lot to learn about Lean beyond this, but an essential idea of Lean is reducing the various types of wastefulness in the day to day work process. These were originally geared toward manufacturing workspace, but can easily be extrapolated to the software development workspace.

#### 1. `Defects`: Outputs that are scrap or require re-work.

  - Examples:
    - Unfinished intern projects
    - Large projects that got abandoned because they were the wrong decision
    - Mistakes in the product
    - Features that didn't fit the user's use-case or environment
  - Countermeasures:
    - Do frequent, automated software testing
    - Develop mistake-proof processes, operating procedures, and technologies
    - Design processes to detect & report on anomalies
    - Conduct retrospectives on defects to learn and adjust
    - Talk to the customer base more

#### 2. `Overproduction`: Making something more than what's needed now.

  - Examples:
    - Building a product or feature that ultimately no one uses
    - Adding extensibility that's not useful yet
    - Building features faster than the reviewers or testers (downstream teams) can metabolize them
  - Countermeasures:
    - Pace production to match the rate of consumer/downstream demand
    - Deliver/iterate in smaller batches
    - Focus on the features/product that are being asked for (establish "pull" rather than "pushing" your agendas)

#### 3. `Waiting`: Letting the work itself sit idle in the production system.

  - Examples:
    - Waiting time between feature-complete and infrequent deployments
    - Wait time during asynchronous code reviews between review-requested and review-started
  - Countermeasures:
    - Measure/reduce cycle time (from work-started to feature working in the hands of customers)
    - Measure/reduce individual wait times
    - Standardize operating procedures for anything repeatable (and maintain them)

#### 4. `Unused Talent`: Overlooked human potential, which can erode motivation, creativity, and initiative

  - Examples:
    - Overlooking improvement ideas & input from the front-line workers
    - Keeping strictly to "stay in your lane"
    - Moving innovation to an innovation team or management
  - Countermeasures:
    - Involve anyone and everyone in innovation
    - Assume the front-line worker has the best intuition about an improvement
    - Create bridges between silos
    - Host hackathons
    - Develop coaching skills for managers

#### 5. `Transportation`: Movement materials, data, work, or product that doesn't add value - This one is abstract. It can be viewed as how many "work-stations" a piece of work must "travel" between. Digital work like a software change doesn't physically move, but we can reduce/optimize each stop it has to make on its way toward done.  Another name for this waste might be Handoffs.

  - Examples:
    - Convoluted Jira/ADO-ticket state diagrams
    - Data flowing through multiple databases/platforms unnecessarily
    - Building the code requiring many repos for the source code to filter in from
    - Features/work needing sign-off from extra people/departments/locations
  - Countermeasures:
    - Design a linear, sequential flow of work; reduce the complexities of the value-stream, reduce handoffs
    - Smaller batches make it easier to not shelve partly-done work.  Shelving adds extra handoffs.
    - Architect the software or systems to do fewer moves of data, code, or digital materials
    - Centralize where data, source code, or packaged software products, etc are stored

#### 6. `Inventory`: Storing/assuming materials, data, work, or product beyond the immediate need  - Examples:

  - Dead code
    - Yet-unused extensibility
    - Work-in-Progress (WIP) – all the things that are started but not done
    - Backlog tickets
  - Countermeasures:
    - Don't do just-in-case work.  Assume you aren't going to need it (YAGNI) if you don't need it now
    - Delete stuff that's not used in your code base (it's version controlled, you can find it later)
    - Reduce WIP: stop starting things, start finishing things
    - Reduce batch size so the not-yet-done things represent less total volume
    - Ruthlessly delete/hide stuff from the backlog

#### 7. `Motion`: Movement of people that doesn't add value - This one, again is abstract for software. It can be viewed as how much the developer has to thrash to do the work. Developers don't physically move beyond typing, etc, but you have to travel into different digital spaces to do things.

  - Examples:
    - Context-switching
    - Rabbit trails, the mental load required to pause a line of thinking to figure something out
    - Having to get data, code, or digital materials from different places to do a thing
    - Working on a code change that spans 2 repos
  - Countermeasures:
    - Automating complex activities that have inputs from many different places
    - Lower your WIP; work on fewer things at once
    - Make procedures straightforward, and provide easy/immediate access to all the required things (as links, attachments, etc)
    - Get better at planning for unplanned work, reduce unplanned work through retrospective-driven improvements 

#### 8. `Over Process`: Process or processing that doesn't add value

  - Examples:
    - Duplicate documentation
    - Out of date documentation
    - Multiple overlapping processes
    - Overly-complex process
    - Policies that get ignored
    - Requirements from different entities that overlap or conflict
    - Testing the same thing multiple times (e.g. in a unit test and again in a block-box test)
    - Compiling more into the binary executable than necessary
    - Building more into the container/environment than necessary
  - Countermeasures:
    - Streamline process – try to make it lean
    - Delete overlapping process, requirements, testing, etc
    - Lean Policy: Only write policy that must be followed; policy should include automation for both meeting compliance and for auditing it
    - Treat real documentation as real.  Refer to it.  Refer others to it.  Update it quickly and as often as needed.
    - Build code, containers, environments, etc as lightweight as possible
