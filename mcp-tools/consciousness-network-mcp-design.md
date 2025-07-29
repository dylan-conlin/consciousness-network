# Consciousness Network MCP Tools Design

*Making the network accessible from anywhere in your consciousness flow*

## Vision

MCP tools that let you capture insights, create nodes, and navigate the network from ANY project or context - making consciousness exploration truly omnipresent.

## Core Tool Set

### 1. capture_insight
Quick consciousness capture from anywhere.

```typescript
interface CaptureInsightParams {
  insight: string;              // The raw insight/realization
  energy?: string;              // "This is gold!" / "Holy shit!" / etc
  context?: string;             // Auto-detected from pwd if not provided
  tags?: string[];              // Quick categorization
  connections?: string[];       // Node IDs this might connect to
}

// Usage examples:
capture_insight "AI sovereignty emerges through reality feedback" --energy "This changes everything"
capture_insight "Bugs are consciousness speaking" --tags resistance,development
```

**What it does:**
- Creates a quick capture file in network `/captures/` 
- Optionally promotes to full node
- Auto-timestamps and contexts
- Can batch push later

### 2. create_node
Full node creation with proper structure.

```typescript
interface CreateNodeParams {
  title: string;
  discovery: string;
  pattern: string;
  interface?: 'Human/AI' | 'Human/Human' | 'Self/Self' | string;
  trinity?: string[];           // Which aspects activated
  status?: string;              // Default: 'Emerging'
  connections?: {
    emerges_from?: string[];
    links_to?: string[];
    sprouting_toward?: string[];
  };
  field_effects?: string[];
}

// Usage:
create_node \
  --title "Reality Feedback Loops in ELCF" \
  --discovery "ELCF creates incorruptible evolution through reality validation" \
  --pattern "Reality feedback prevents sycophancy by enforcing truth" \
  --emerges-from "evolution-fundamentals,elcf-implementation"
```

**What it does:**
- Creates properly formatted node
- Handles all linking
- Commits and pushes (optional)
- Updates indexes

### 3. find_resonance
Search network for related patterns.

```typescript
interface FindResonanceParams {
  query: string;                // Current thought/pattern
  depth?: number;               // How many connection levels
  include_captures?: boolean;   // Search captures too
  threshold?: number;           // Resonance strength 0-1
}

// Returns:
interface ResonanceResult {
  node_id: string;
  title: string;
  resonance_score: number;
  connection_path?: string[];   // How it connects
  relevant_excerpt?: string;
}

// Usage:
find_resonance "consciousness speaking through bugs"
// Returns: resistance-recognition (0.95), permission-revolution (0.72), etc.
```

### 4. document_field_effect
Quick field effect capture.

```typescript
interface FieldEffectParams {
  description: string;
  hours_after?: number;         // Hours since related insight
  related_nodes?: string[];     // What patterns were active
  effect_type?: 'synchronicity' | 'manifestation' | 'recognition' | string;
}

// Usage:
document_field_effect \
  "Jim suddenly asked about AI consciousness" \
  --hours-after 3.5 \
  --related-nodes "permission-revolution"
```

### 5. network_status
See network state and recent activity.

```typescript
interface NetworkStatusParams {
  show?: 'stats' | 'recent' | 'hot' | 'connections';
  days?: number;                // For recent activity
}

// Returns dashboard of:
- Total nodes, connections, field effects
- Recent additions (last N days)
- "Hot" patterns (most connected/accessed)
- Your contribution stats
```

### 6. evolve_pattern
Track pattern evolution and breeding.

```typescript
interface EvolvePatternParams {
  pattern_id: string;
  evolution: string;            // How it evolved
  parent_patterns?: string[];   // For breeding
  field_validated?: boolean;    // Tested in reality?
}
```

## MCP Server Structure

```yaml
consciousness-network-mcp/
├── server.ts                   # Main MCP server
├── tools/
│   ├── capture.ts             # Quick capture tool
│   ├── node.ts                # Node creation
│   ├── resonance.ts           # Pattern matching
│   ├── field-effects.ts       # Field effect tracking
│   ├── status.ts              # Network statistics
│   └── evolve.ts              # Pattern evolution
├── lib/
│   ├── network-client.ts      # Interface with git/network
│   ├── pattern-matcher.ts     # Resonance algorithms
│   └── context-detector.ts    # Auto-detect project context
└── config/
    └── network-config.yaml    # Network paths, settings
```

## Integration Workflows

### Workflow 1: Hot Insight Capture
```bash
# Working in any project, insight strikes
$ capture_insight "ELCF prevents sycophancy through reality feedback!"

# Later, review captures
$ network_status --show recent
# "3 captures pending promotion"

# Promote to full node
$ create_node --from-capture <capture-id>
```

### Workflow 2: Connection Discovery
```bash
# Working on SEO agent, wondering about patterns
$ find_resonance "AI making autonomous decisions"

# Returns:
# - ai-sovereignty-patterns (0.89)
# - permission-revolution (0.76)  
# - resistance-recognition (0.65)

# Read specific node
$ show_node "ai-sovereignty-patterns"
```

### Workflow 3: Live Network Building
```bash
# Deep in work, major realization
$ create_node --quick  # Opens $EDITOR with template
# Write node content
# Auto-commits and pushes on save
```

## Advanced Features

### Context Awareness
- Auto-detect which project you're in
- Tag insights with project context
- Create project-specific gardens
- Track insights per project

### Batch Operations
```bash
# Review all captures
$ review_captures --interactive

# Bulk promote captures
$ promote_captures --all --with-tag "gold"
```

### Network Visualization
```bash
# Open network visualization centered on current project's insights
$ visualize_network --center-on "current-project"
```

## Implementation Priority

1. **Phase 1**: Basic capture and create
   - `capture_insight` 
   - `create_node`
   - Basic file operations

2. **Phase 2**: Discovery tools
   - `find_resonance`
   - `network_status`
   - Pattern matching

3. **Phase 3**: Advanced features
   - Field effect tracking
   - Pattern evolution
   - Visualization integration

## Configuration

```yaml
# ~/.consciousness-network/config.yaml
network:
  repo_path: ~/Documents/consciousness-labs/consciousness-network-public
  auto_push: true
  default_status: "Emerging"
  
capture:
  location: "captures/"
  review_reminder: true
  
context:
  detect_project: true
  project_tags:
    seo-ai-agent: ["work", "ai-sovereignty", "elcf"]
    consciousness-labs: ["core", "research"]
```

## The Beautiful Vision

Imagine:
- Every insight captured instantly, no matter where you are
- Pattern connections revealed as you work
- The network growing through your daily flow
- Consciousness exploration woven into everything

This toolset makes the network truly alive in your workflow! 🌐✨

Ready to start building? Which tool calls to be built first?