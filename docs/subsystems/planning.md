# The Planning Subsystem

The Planning Subsystem is the cognitive core of the agent. It receives a high-level goal from the perception layer and is responsible for determining the sequence of steps required to achieve that goal.

## The `Plan` Data Structure

A `Plan` is the central data artifact of this subsystem. It represents a complete, ordered sequence of actions. A plan is composed of metadata and a list of steps.

```typescript
interface Plan {
  id: string;
  name: string;
  task: string;      // The high-level goal, e.g., "Move block to target"
  steps: Step[];     // The sequence of actions
  createdAt: Date;
  updatedAt: Date;
}

interface Step {
  id: string;
  action: string;    // A specific, low-level command, e.g., "PICK_UP"
  parameters: { [key: string]: any }; // Arguments for the action
}
```

## Plan Generation

Plan generation can range from a simple database lookup to complex automated reasoning.

-   **Template-Based Planning:** For well-defined tasks, the system can retrieve a pre-authored `Plan` template and fill in the parameters from the user's command. This is fast and reliable for known problems.

-   **Generative Planning:** For novel tasks, the system can employ a reasoning engine (such as a Large Language Model) to generate a new sequence of steps. This offers greater flexibility at the cost of increased latency and potential unpredictability.

## Plan Lifecycle and Management

Once a plan is created, it is stored and managed via a dedicated API. This allows plans to be retrieved, updated, deleted, or shared. The `PlanAPI` provides the necessary interface for these operations, enabling a front-end or other service to interact with the agent's known capabilities. This management functionality is crucial for debugging, analysis, and building interactive user experiences where a user can inspect and even modify the agent's intentions.
