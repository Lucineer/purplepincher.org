# Your First Plato Room

## Tutorial: Creating a Thinking Space

### What You'll Build

A Plato room for a topic you care about. The room will have:
- A purpose and personality
- Constraints that shape all outputs
- Knowledge tiles for context
- A history of interactions

### Step 1: Choose a Topic

Pick something you work on regularly. Examples:
- Debugging CUDA errors
- Writing documentation
- Deploying to edge hardware
- Learning a new framework

### Step 2: Create the Room File

Create a markdown file:

```markdown
# My Room: [Topic Name]

## Purpose
[One paragraph describing what this room is for and 
what kind of thinking happens here]

## Constraints
- MUST: [Hard rules - output must satisfy these]
- SHOULD: [Soft guidelines - try to follow these]
- CANNOT: [Prohibitions - output must never do these]
- MAY: [Permissions - output is allowed to do these]

## Available Tiles
- [List relevant knowledge tiles here]

## Personality
[Describe the room's tone and style]

## History
[Interactions will be recorded here over time]
```

### Step 3: Add Real Constraints

Good constraints are specific and enforceable:

```markdown
## Constraints
- MUST: Include specific code examples
- MUST: State assumptions explicitly
- SHOULD: Compare at least 2 approaches
- CANNOT: Make claims without evidence
- MAY: Reference external documentation
```

Bad constraints are vague:

```markdown
## Constraints
- MUST: Be helpful
- SHOULD: Be good
```

### Step 4: Add Knowledge Tiles

Reference existing tiles that are relevant to your room's topic:

```markdown
## Available Tiles
- [cuda-memory-management](../tiles/47.md) — OOM debugging on Jetson
- [thermal-throttling](../tiles/23.md) — GPU temperature management
```

### Step 5: Use the Room

When you have a question or problem related to the room's topic:
1. Open the room file
2. Review the constraints and tiles
3. Generate your response within the room's framework
4. Record the interaction in the History section

### Step 6: Let It Grow

Over time:
- Add new tiles from your experiences
- Refine constraints based on what works
- Record successful applications in tiles
- The room becomes a living knowledge base

### Example: Edge Deployment Room

```markdown
# Room: Jetson Edge Deployment

## Purpose
Coordinating software deployment to NVIDIA Jetson Orin Nano devices.
All suggestions must account for 8GB unified memory, ARM64 
architecture, and 15W power envelope.

## Constraints
- MUST: Include memory usage estimates
- MUST: Specify ARM64 compatibility
- SHOULD: Provide rollback procedure
- CANNOT: Assume x86 availability
- CANNOT: Require more than 6GB working RAM
- MAY: Suggest CUDA optimizations

## Available Tiles
- [cuda-oom-fix](../tiles/47.md)
- [arm64-quirks](../tiles/31.md)
- [power-management](../tiles/44.md)

## Personality
Practical, hardware-grounded, cautious. Prefers proven solutions
over experimental ones. Always asks "will this fit in 8GB?"
```

## Next Steps

- Join the fleet: `JOINING-THE-FLEET.md`
- Learn about tiles: `../ecosystem/TILE-NETWORK.md`
- Learn about constraints: `../ecosystem/CONSTRAINT-THEORY.md`
