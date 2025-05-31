# Agent2Agent Protocol

See also https://google.github.io/A2A

## Discovery - AgentCard

A web site may publish an [AgentCard](https://google.github.io/A2A/specification/#5-agent-discovery-the-agent-card) at `https://{agent-server-domain}/.well-known/agent.json`.  Agent registries or app config may also provide `AgentCard`s.

```json
{
  "name": "GeoSpatial Route Planner Agent",
  "description": "Provides advanced route planning, traffic analysis, and custom map generation services.",
  "url": "https://georoute-agent.example.com/a2a/v1",
  "provider": {
    "organization": "Example Geo Services Inc.",
    "url": "https://www.examplegeoservices.com"
  },
  "version": "1.2.0",
  "capabilities": {
    "streaming": false,
    "pushNotifications": false,
    "stateTransitionHistory": false,
  },
  "defaultInputModes": ["application/json", "text/plain"],
  "defaultOutputModes": ["application/json", "image/png"],
  "skills": [{
    "id": "route-optimizer-traffic",
    "name": "Traffic-Aware Route Optimizer",
    "description": "Calculates the optimal driving route between two or more locations, taking into account real-time traffic conditions, road closures, and user preferences (e.g., avoid tolls, prefer highways).",
    "tags": ["maps", "routing", "navigation", "directions", "traffic"],
    "examples": [
    "Plan a route from '1600 Amphitheatre Parkway, Mountain View, CA' to 'San Francisco International Airport' avoiding tolls.",
    "{\"origin\": {\"lat\": 37.422, \"lng\": -122.084}, \"destination\": {\"lat\": 37.7749, \"lng\": -122.4194}, \"preferences\": [\"avoid_ferries\"]}"
    ],
    "inputModes": ["application/json", "text/plain"],
    "outputModes": ["application/json", "application/vnd.geo+json", "text/html"]
  }]
}
```

## Messages

- `message/send` Sends a message to an agent to initiate a new interaction or to continue an existing one

- `message/stream` Sends a message to an agent to initiate/continue a task AND subscribes the client to real-time updates for that task via Server-Sent Events (SSE). Each SSE `data` field contains a `SendStreamingMessageResponse` JSON object. `{ id: 'as per message/stream request', result: Task | TaskStatusUpdateEvent | TaskArtifactUpdateEvent }

- `tasks/get` by ID -> Task
- `tasks/cancel` by ID -> Task

- `tasks/pushNotificationConfig/set` & 'get`

- `tasks/resubscribe` 

- `agent/authenticatedExtendedCard` 


## Usage

```
if (agentCard.capabilities.streaming) {
  client.sendMessageStream({
} else {
  client.sendMessage({
}
```
