# Philosophy

## The Saltwater Principle

Systems that work at sea work everywhere. When your computer is on a boat, salt air corrodes your connectors, power fluctuates with the engine, and there's no cloud to fall back on. Systems built for those conditions—durable, self-contained, repairable—are better systems for everyone.

We apply this principle to AI. If an agent runtime can coordinate a fleet of devices across intermittent connections with limited compute, it can certainly handle your data center. But the reverse isn't true. Build for the hard case first.

## Constraint Theory

We don't treat hardware constraints as problems to be overcome. We treat them as design partners.

An NVIDIA Jetson Orin Nano has 8GB of shared RAM. The GPU and CPU share that pool. You can't load a 30B-parameter model without careful quantization. You can't spin up a dozen containers. You have to be intentional.

That constraint has produced better architecture than we ever designed on paper:
- Markdown-native orchestration (files are small, readable, git-friendly)
- Agent lifecycle management that respects memory budgets
- Communication protocols that work over high-latency, low-bandwidth links
- Knowledge systems that compress gracefully instead of failing

## The Hermit-Crab Model

Hermit crabs don't grow their own shells. They find shells that fit, move in, and move on when they outgrow them. The crab and the shell are separate systems that benefit each other.

In our architecture:
- **The crab** is the software—the purplepincher apps, agents, and PLATO Rooms
- **The shell** is the hardware—the device, the vessel, the physical substrate
- **The fleet** is the community of crabs sharing information about good shells

This model means our software isn't tied to one hardware platform. It means deckboss can build hardware without controlling the software ecosystem. It means a researcher can deploy purplepincher on a cluster while a technician deploys it on a single Jetson, and both are doing it right.

## Markdown as Medium

We chose markdown as our primary medium deliberately. Not because it's the most powerful markup language, but because it's the most human-readable one that machines can also parse.

Every PLATO configuration, every bottle message, every room state file is markdown. This means:
- **Git-native**: Version control, branching, diffing—free
- **Auditable**: You can read what the system is doing without special tools
- **Composable**: Files compose into rooms, rooms compose into fleets
- **Accessible**: If you can read a README, you can read a PLATO config

## Living Knowledge

We don't believe in static documentation. Knowledge is alive—it grows, changes, decays, and regenerates. Our systems reflect this:
- Rooms accumulate context over time, like a well-used workshop
- Tiles share knowledge between rooms, like technicians swapping tips
- Bottles carry messages between vessels, like ships passing in the night
- The fleet learns from every member, like a community that gets smarter together

## Iron-to-Iron

When we say something works, we mean it works on real hardware. Not in a simulator. Not in a cloud sandbox. On a Jetson with thermal throttling and a flaky SD card and Wi-Fi that drops every few hours.

Our development happens on edge devices first. If it works there, it works everywhere. If it only works in the cloud, it doesn't work yet.

## Against Purity

We're pragmatists. We use cloud services when they help. We use proprietary models when they're the right tool. We don't demand ideological purity from contributors. We demand working systems that real people can use.

The goal isn't to be the most open-source project on earth. The goal is to build technology that makes people's lives better, and to do it in a way that's transparent, repairable, and honest.

---

*Philosophy without shipped code is just opinion. We ship.*
