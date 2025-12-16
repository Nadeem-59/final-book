# Voice-to-Text and NLP

The perception layer of the agent is responsible for converting human speech into structured, machine-readable commands. This process involves two primary stages: transcription and interpretation.

## Voice-to-Text (VTT) Transcription

The first stage is the conversion of raw audio input into text. This is a well-established problem domain, and the system is designed to be agnostic to the specific VTT provider. Any service that can provide a reasonably accurate text transcription is suitable.

**Key Requirements:**
-   **Low Latency:** For real-time interaction, the transcription service must return results promptly.
-   **High Accuracy:** While the NLP module can handle some ambiguity, higher transcription accuracy leads to more reliable intent extraction.

## Natural Language Processing (NLP) for Intent Extraction

Once a text transcription is available, the NLP module interprets its meaning. This is a critical step that bridges the gap between ambiguous human language and the precise logic required by the planner.

**Process:**
1.  **Entity Recognition:** The model identifies key nouns and objects in the text (e.g., "cube," "sphere," "red circle").
2.  **Intent Classification:** The model determines the primary verb or action the user wants to perform (e.g., "move," "pick up," "go to").
3.  **Parameter Association:** The model links the recognized entities to the classified intent, forming a structured command.

**Example:**
-   **Input Text:** "Could you please move the blue block onto the goal area?"
-   **Structured Output:**
    ```json
    {
      "intent": "MOVE",
      "parameters": {
        "object": { "type": "block", "color": "blue" },
        "destination": { "type": "area", "name": "goal" }
      }
    }
    ```

This structured data is the final output of the perception subsystem and serves as the input to the Planning Subsystem.
