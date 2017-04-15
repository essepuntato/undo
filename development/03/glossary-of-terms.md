# Iteration 3: glossary of terms

## Workflow
A description of a sequence of connected steps, representing a sequence of publishing operations undertaken by agents.

## Workflow execution
A collection of actions that address all the step defined in a workflow.

## Executes
It links a workflow execution to the related workflow description.

## Step
An atomic unit of a workflow that involves some input entity needed to complete the step, and produces some outcomes, such as a document.

## Has step
It links a workflow to a step defined in it.

## Action
An event with at least one agent that is participant in it and that is linked to a workflow execution and to a step of a workflow description.

## Includes action
It links a workflow execution with the related actions. 

## Addresses
It links an action with the step that is addressed (totally or partially) by it.

## Step type
The class of all the particular types for categorising the steps of a workflow description.

## Actor
Some entity taking part actively to a workflow, e.g. by being involved in the actions executing it.

## Involves
It links an action to the entity that are involved.

## Has following step
It links a step of a workflow with the immediate following one.

## Needs
It links a step with a specific entity that is requested for the step completion. 

## Produces
It links a step with the entity that is produced at the end of the execution of that step.