# Movement Actuation

The Movement Actuation subsystem is where the agent's plans are translated into tangible actions within the environment. It is the bridge between the abstract cognitive layer and the physical (or simulated) world.

## The Role of the Actuator

The Actuator is a component that consumes a `Plan` object and executes its steps sequentially. It acts as a client to the simulation environment's API.

**Execution Flow:**
1.  **Receive Plan:** The Actuator is given a `Plan` object to execute.
2.  **Iterate Steps:** It loops through the `plan.steps` array in order.
3.  **Dispatch Action:** For each `Step`, it calls the corresponding function in the simulation environment, passing the `step.parameters` as arguments.
4.  **Await Completion (Optional):** The Actuator can operate in two modes:
    -   **Synchronous:** It can wait for the simulation to confirm that an action is complete before proceeding to the next step. This is useful for tasks requiring precise sequencing.
    -   **Asynchronous:** It can dispatch an action and immediately proceed to the next, allowing for more fluid, parallel movements.

## Interface with the Simulation

The Actuator is tightly coupled to the simulation environment it controls. The `action` strings within a `Plan` must correspond to available functions in the simulation's API.

**Example:**
A `Step` object like this:
```json
{
  "action": "MOVE_TO",
  "parameters": {
    "target_id": "object_123",
    "speed": 1.5,
    "orientation": [0.0, 0.0, 1.0, 0.0]
  }
}
```
Would require the simulation environment to expose a function such as:
```python
# Pseudocode for a simulation API
def MOVE_TO(target_id: str, speed: float, orientation: list[float]):
  # ... logic to move an agent ...
  return "SUCCESS"
```

This direct mapping ensures that plans are always executable, provided they are generated correctly. The design of the available actions in the simulation API defines the agent's fundamental capabilities.
