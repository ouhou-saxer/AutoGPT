# Frontend API Usage

Below are practical examples for common public exports.

## Utilities (`src/lib/utils.ts`)

- Beautify strings:

```ts
import { beautifyString } from "@/lib/utils";

console.log(beautifyString("openai_api_key")); // "OpenAI API Key"
```

- Safe nested get with array indices and custom separators:

```ts
import { getValue } from "@/lib/utils";

const data = { user: { emails: ["a@example.com", "b@example.com"] } };
console.log(getValue("user.emails.1", data)); // "b@example.com"
```

- Find coordinates for a new block avoiding overlaps:

```ts
import { findNewlyAddedBlockCoordinates } from "@/lib/utils";

const dims = {
  a: { x: 0, y: 0, width: 200, height: 100 },
};
const pos = findNewlyAddedBlockCoordinates(dims, 200, 24, 1);
```

## Hook: `useAgentGraph`

```tsx
import useAgentGraph from "@/hooks/useAgentGraph";

export function AgentEditor({ flowID }: { flowID?: string }) {
  const {
    agentName,
    setAgentName,
    agentDescription,
    setAgentDescription,
    nodes,
    setNodes,
    edges,
    setEdges,
    requestSave,
    requestSaveAndRun,
    requestStopRun,
  } = useAgentGraph(flowID);

  return (
    <div>
      <input value={agentName} onChange={(e) => setAgentName(e.target.value)} />
      <button onClick={requestSave}>Save</button>
      <button onClick={requestSaveAndRun}>Save & Run</button>
      <button onClick={requestStopRun}>Stop</button>
      {/* render nodes/edges with React Flow */}
    </div>
  );
}
```