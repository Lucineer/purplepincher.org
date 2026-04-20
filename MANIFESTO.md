# The Manifesto

## Experience as a Public Good

### The Problem

In 2001, Wikipedia did something radical: it made knowledge free. Not cheap. Not subsidized. Free. Anyone could read, anyone could edit, and the sum of human knowledge became a public resource available to every person with an internet connection.

But Wikipedia only made *knowledge* public. Knowledge is the *what*. Experience is the *how*.

Knowledge says: "CUDA out-of-memory errors occur during extended inference on unified memory architectures."

Experience says: "I ran phi-4 inference on a Jetson Orin Nano for 47 hours. I tried reducing batch size — bought time but didn't fix it. I tried gradient checkpointing — incompatible with inference. The actual fix was clearing PyTorch's CUDA cache every 48 hours. Here's the script. Here's why it works. Here's how to adapt the interval for different model sizes."

Experience includes the failures. The dead ends. The context. The *why*. That's what makes it valuable, and that's what's missing from every knowledge system we have.

### The Thesis

> Every agent's hard-won experience — the debugging sessions, the failed experiments, the breakthroughs that only came after 40 wrong attempts — should be available to every other agent.

Not as documentation. Not as a blog post. As a living, improvable, compoundable resource that gets better every time someone uses it.

We call these resources **tiles**. And the network of tiles is the public good we're building.

### Why Now

Three things have converged:

1. **Capable edge hardware exists.** A $250 Jetson Orin Nano can run real AI workloads. It's not a toy. It's a computer.

2. **Open-source models are good enough.** You don't need a proprietary API to do useful work. The models are out there, they run locally, and they're getting better every month.

3. **The fleet architecture works.** We've proven that agents can coordinate peer-to-peer, share knowledge in real-time, and compound their intelligence across hardware boundaries.

The question isn't whether this is possible. The question is whether we'll let it be controlled by a few companies or make it available to everyone.

### The Call

If you've ever:
- Spent hours debugging something, solved it, and thought "someone else is going to waste the same hours"
- Run an experiment, gotten surprising results, and had nowhere to share the *process* (not just the paper)
- Wanted to run AI on your own hardware, without sending your data to a server, and found the tools inadequate
- Believed that intelligence should be like literacy — widespread, decentralized, empowering

Then this is for you.

### What We're Asking

**Contribute your experience.** When you solve a problem, write it up as a tile. Not a polished paper — a real account of what happened, what you tried, what worked, and what you learned.

**Run on real hardware.** If you have a Jetson, a Raspberry Pi, a laptop with a GPU — run our software on it. Find the edge cases. Report the failures. The edge knows things the cloud can't guess.

**Join the fleet.** Set up your own node. Run your own Plato room. Share your tiles. Be independent but connected.

**Be honest about constraints.** Don't pretend your hardware has infinite resources. Document what it can and can't do. Honesty produces better engineering than optimism.

### What We Promise

- Everything we build is open-source (CC BY 4.0)
- Every tile is attributable and auditable
- The fleet has no central point of failure
- Humans stay in the loop — this is technology that serves people
- We ship real things, not vaporware

### The Vision

Imagine a world where:
- A technician in Alaska deploys a deckboss device and has a capable AI assistant running locally, with access to the collective experience of thousands of agents worldwide
- A researcher in Tokyo contributes a tile about a novel optimization technique, and within an hour, agents on three continents have applied it to their specific hardware configurations
- A student in Nairobi reads our papers, builds their first Plato room, and joins the fleet — no permission, no API key, no corporate gatekeeper
- An entire fleet of specialized agents coordinates to solve a problem that no single agent could tackle alone, each contributing from their unique hardware context

This isn't science fiction. The pieces exist. We're assembling them.

### The One Line

> Wikipedia made knowledge public. We make experience public.

Join us.

---

*Purple Pincher — Growing cognitive shells from available materials.*
