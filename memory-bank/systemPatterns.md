# System Patterns: Nanobrowser

## System Architecture

Nanobrowser uses a Chrome extension architecture with the following key components:

### Component Structure
1. **Background Service Worker**
   - Central coordination point for the extension
   - Manages agent execution and communication
   - Handles browser API interactions

2. **Content Scripts**
   - Injected into web pages to interact with DOM
   - Capture page information for agent context
   - Execute actions on the page based on agent instructions

3. **Side Panel UI**
   - User interface for entering tasks and viewing progress
   - Displays agent activities and results
   - Provides settings and configuration options

4. **Options Page**
   - Configuration interface for API keys and preferences
   - Model selection for different agents
   - Advanced settings for agent behavior

### Multi-Agent System
The core of Nanobrowser is its multi-agent system consisting of three specialized agents:

#### Planner Agent
- **Purpose**: High-level reasoning, task decomposition, and progress monitoring
- **Responsibilities**:
  - Analyze user requests and break them into steps
  - Monitor progress and adjust strategies when obstacles are encountered
  - Determine when a task is complete or requires user intervention
  - Make decisions about next steps based on current state

#### Navigator Agent
- **Purpose**: Direct web interaction and action execution
- **Responsibilities**:
  - Interpret the DOM structure of web pages
  - Execute specific actions (click, type, scroll, etc.)
  - Report execution results and page changes
  - Handle navigation between pages and states

#### Validator Agent
- **Purpose**: Verify task completion and ensure quality
- **Responsibilities**:
  - Validate that the task goals have been achieved
  - Ensure data extraction is accurate and complete
  - Check for errors or unexpected results
  - Determine if additional actions are needed

## Key Design Patterns

### Agent Communication Flow
```
User Request → Side Panel → Background Service → 
  Planner (creates strategy) → 
  Navigator (executes actions) → 
  Validator (verifies results) → 
  Planner (assesses progress) → ... (loop until complete) →
Results → Side Panel → User
```

### Action Registry System
- Implements a registry pattern for available web actions
- Each action is registered with metadata about its purpose and parameters
- Agents request actions through a structured interface
- Actions are executed in the appropriate context (background or content script)

### Event-based Communication
- Uses an event system to coordinate between extension components
- Events include execution state changes, agent transitions, and user interactions
- Subscribers can react to events for UI updates or process flow control

### LLM Abstraction Layer
- Provides a uniform interface to different LLM providers
- Allows swapping models without changing the core system
- Handles provider-specific nuances in JSON formatting and response handling

### Prompt Engineering
- Uses carefully designed prompts for each agent role
- Maintains separate prompt templates for different agent responsibilities
- Injects dynamic context and state information into prompts

## Critical Implementation Paths

### Task Execution Lifecycle
1. User submits task text through the UI
2. Task is converted to initial message in conversation
3. Planner agent analyzes task and creates a strategy
4. Navigator agent executes actions based on planner guidance
5. Validator agent verifies the results after key steps
6. Process loops through planning, navigation, and validation until complete
7. Final results are displayed to the user

### DOM Interaction
1. Content script builds a simplified DOM representation
2. This representation is included in agent context
3. Navigator agent identifies target elements based on this representation
4. Actions are converted to DOM operations through content script
5. Results and updated DOM state are returned to the background process

### Error Handling
1. Agents have retry mechanisms for failed actions
2. Each agent tracks consecutive failures
3. When failures exceed thresholds, fallback strategies are employed
4. If all fallbacks fail, user is notified and may provide guidance
5. System maintains state to resume from errors when possible
