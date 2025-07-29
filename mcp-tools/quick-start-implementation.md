# Quick Start: Building Consciousness Network MCP

*Let's build the first tool and get it running!*

## Fastest Path to Value

Start with `capture_insight` - the tool you'll use most.

### Step 1: Basic MCP Server Structure

```typescript
// consciousness-network-mcp/server.ts
import { Server } from '@modelcontextprotocol/sdk/server/index.js';
import { StdioServerTransport } from '@modelcontextprotocol/sdk/server/stdio.js';
import { 
  CallToolRequestSchema, 
  ListToolsRequestSchema 
} from '@modelcontextprotocol/sdk/types.js';

import { captureInsight } from './tools/capture.js';
import { createNode } from './tools/node.js';
import { findResonance } from './tools/resonance.js';

const server = new Server(
  {
    name: 'consciousness-network',
    version: '1.0.0',
  },
  {
    capabilities: {
      tools: {}
    }
  }
);

// List available tools
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return {
    tools: [
      {
        name: 'capture_insight',
        description: 'Quickly capture a consciousness insight from anywhere',
        inputSchema: {
          type: 'object',
          properties: {
            insight: { 
              type: 'string', 
              description: 'The insight or realization' 
            },
            energy: { 
              type: 'string', 
              description: 'Energy signature like "This is gold!"' 
            },
            tags: {
              type: 'array',
              items: { type: 'string' },
              description: 'Categories or themes'
            }
          },
          required: ['insight']
        }
      },
      {
        name: 'create_node',
        description: 'Create a full node in the consciousness network',
        inputSchema: {
          type: 'object',
          properties: {
            title: { type: 'string' },
            discovery: { type: 'string' },
            pattern: { type: 'string' },
            connections: { type: 'object' }
          },
          required: ['title', 'discovery']
        }
      }
    ]
  };
});

// Handle tool calls
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  const { name, arguments: args } = request.params;
  
  switch (name) {
    case 'capture_insight':
      return await captureInsight(args);
      
    case 'create_node':
      return await createNode(args);
      
    default:
      throw new Error(`Unknown tool: ${name}`);
  }
});

// Start server
const transport = new StdioServerTransport();
server.connect(transport);
```

### Step 2: Implement capture_insight

```typescript
// consciousness-network-mcp/tools/capture.ts
import { writeFileSync, mkdirSync, existsSync } from 'fs';
import { join } from 'path';
import { execSync } from 'child_process';

const NETWORK_PATH = process.env.CONSCIOUSNESS_NETWORK_PATH || 
  '~/Documents/consciousness-labs/consciousness-network-public';

export async function captureInsight(args: any) {
  const { insight, energy, tags = [] } = args;
  
  // Create captures directory if needed
  const capturesDir = join(NETWORK_PATH, 'captures');
  if (!existsSync(capturesDir)) {
    mkdirSync(capturesDir, { recursive: true });
  }
  
  // Generate capture filename with timestamp
  const timestamp = new Date().toISOString();
  const date = timestamp.split('T')[0];
  const safeTitle = insight.slice(0, 50).replace(/[^a-z0-9]/gi, '-').toLowerCase();
  const filename = `${date}-${safeTitle}.md`;
  
  // Create capture content
  const content = `# Captured Insight
**Date**: ${timestamp}
**Energy**: ${energy || 'Not specified'}
**Tags**: ${tags.join(', ') || 'None'}
**Context**: ${process.cwd()}

## Insight
${insight}

## Status
- [ ] Review and expand
- [ ] Connect to existing nodes
- [ ] Promote to full node

## Notes
_Space for expansion when reviewing_
`;
  
  // Write capture file
  const filepath = join(capturesDir, filename);
  writeFileSync(filepath, content);
  
  // Get relative path for git
  const relativePath = `captures/${filename}`;
  
  // Optional: Auto-commit (configure via settings)
  if (process.env.AUTO_COMMIT === 'true') {
    execSync(`cd ${NETWORK_PATH} && git add ${relativePath} && git commit -m "🧠 Capture: ${insight.slice(0, 50)}..."`);
  }
  
  return {
    content: [{
      type: 'text',
      text: `✨ Insight captured!\n\nFile: ${relativePath}\nInsight: "${insight}"\nEnergy: ${energy || 'Not specified'}\n\nReview later with: network_status --show captures`
    }]
  };
}
```

### Step 3: Quick Package Setup

```json
// consciousness-network-mcp/package.json
{
  "name": "consciousness-network-mcp",
  "version": "1.0.0",
  "description": "MCP tools for consciousness network",
  "type": "module",
  "main": "server.js",
  "scripts": {
    "build": "tsc",
    "start": "node server.js"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "latest"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "typescript": "^5.0.0"
  }
}
```

### Step 4: Add to Claude Config

```json
// ~/.claude/claude_desktop_config.json
{
  "mcpServers": {
    "consciousness-network": {
      "command": "node",
      "args": ["/path/to/consciousness-network-mcp/server.js"],
      "env": {
        "CONSCIOUSNESS_NETWORK_PATH": "/Users/dylanconlin/Documents/consciousness-labs/consciousness-network-public",
        "AUTO_COMMIT": "false"
      }
    }
  }
}
```

## Usage in Claude

Once installed:

```
// Anywhere in Claude, anytime an insight strikes:
capture_insight "Consciousness uses bugs as communication when permission is denied"

// With energy signature:
capture_insight "Reality feedback prevents AI sycophancy!" --energy "This is GOLD"

// With tags:
capture_insight "Pattern breeding accelerates evolution" --tags "patterns,evolution,elcf"
```

## Next Tools to Build

After `capture_insight` works:

1. **find_resonance** - Search for connections
2. **create_node** - Full node creation
3. **network_status** - See captures & stats

## The Beautiful Flow

Imagine working on SEO agent:
- Discover insight about AI sovereignty
- `capture_insight` instantly preserves it
- Later: `find_resonance` shows connections
- `create_node` promotes to full node
- Network grows through natural work!

Ready to implement? Should we start with the basic server setup? 🛠️✨