# Setting up Multi-Agent / Claude Process

## Workflow Architecture 

### Parts
#### Orchestrator
- CLAUDE.md defines Orchestrator behavior
- Coordinage work
- Delegate tasks to subagents
- Enforce quality
- Report progress

#### Specialized Agents
- Completes specific types of tasks
- Given a clear protocol defining how they should think and operate

#### Skills 
- Reference library
- Structured knowledge documents
- Loaded by agents on demand
- Gives agents the knowledge they need to complete their tasks

### Practices
- Agents specify behavior
    - Process, approach, standards
- Skills specify knowledge
    - Reference material, technical details
- Skills are loaded by agents
    - Keeps orchestrator's context clean


#### Pipelines
- Design pipelines for certain types of tasks
- Define pipeline specifications in CLAUDE.md
    - Define how to decide which pipeline to use
    - Define steps for each pipeline
    - Define available agents and skills for each pipeline
    - Define when to require human interaction


## Artifact Files
Create and update files to record task progress

### State File
Captures where work stopped
- Current Step
- What's been done
- What's next

### Plan Document
- Full methodology and task sequence
- Everything that was done and why
- Exact ordered list of tasks
- What could go wrong and how to handle it
- Key decisions log
- Final review log

### Intermediate Outputs
- Outputs of intermediate steps

### Report
- Stakeholder-facing summary
- Contains:
    - Executive summary
    - Detailed methodology
    - Limitations

### Learnings File
- Insights accumulated during the task


## Context Window Management
- Don't fill up the entire context window - the model gets confused when it's close to 100%

### 40% - 60%
    - Delegate more to subagents, work more to keep the orchestrator clean

### 60% - 75%
    - Finish current task
    - Save state
    - Warn about restarting soon

### >75%
    - Save state
    - Recommend restarting the session

## Validation
### Quick Check
- Catch obvious errors
- Run after every data fetch / data transformation
- Make sure the data is what you expect

### Adversarial Check
- Separate agent for independent review
- Catch complex errors
    - Wrong approach
    - Interpretation wrong
- Classify findings into:
    - INFO
        - Worth noting, but not a problem
    - WARNING
        - Potential issue that doesn't block progress
    - BLOCKER
        - Must be fixed before proceeding
        - Trigger a revision cycle
            - Attempt to auto-fix
            - If that doesn't work, stop for human review

### Revision Mode
- Change an existing analysis
- Read the existing plan, then create a __new version__ of the artificats
    - Don't modify the originals