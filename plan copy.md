
---

# The Concept

**Framing:** You are a detective. You have a board of suspects connected by red string. GNNs are the technique for answering "what can I learn about this person from the company they keep?"

Every GNN concept maps onto something a detective actually does:

| GNN concept | Detective board |
|---|---|
| Node features | What's written on a suspect's card |
| Edges | Red string between pins |
| Message passing | Each suspect reports what they know to their contacts |
| Aggregation | You combine all the reports you received |
| Update | You rewrite the suspect's card |
| k layers | k rounds of interrogation → info travels k hops |
| Attention (GAT) | Some informants are more reliable than others |
| Over-smoothing | Too many rounds and every suspect tells the same story |

That last row is the payoff — a limitation that usually needs eigenvalue arguments becomes a one-line joke.

---

# Slide-by-Slide Plan (10 min, 13 slides)

**Total budget: 600s.** Times below sum to ~590 with breathing room.

### 1 — Cold open `40s`
Black slide. A single pinned photo, no text. Then a second pin fades in. Then a string snaps between them (TikZ `decorate` path drawn with `\draw[overlay]` across two overlays). Then eight more pins and strings cascade in.

Title resolves: **"Graph Neural Networks — Learning from Who You Know."**

> *Say:* "Every dataset you've trained on so far had a shape. Images are grids. Text is a line. But some of the most important data in the world looks like this — and it has no shape at all."

### 2 — The crime: why normal nets fail `65s`
Three-panel TikZ comparison, revealed with `\onslide<1->`, `<2->`, `<3->`:
- Panel 1: image grid, caption "always 3×3 neighbours" → CNN ✅
- Panel 2: sentence tokens in a row, "always left-to-right" → RNN/Transformer ✅
- Panel 3: a messy graph, "5 neighbours here, 1 there, no order" → ❌ (red X animates in)

Then the killer line appears: **relabel the nodes and an MLP gives you a different answer.** Show it — same graph, permuted node IDs, two different output values flashing.

> *Say:* "This is the whole problem. A neural network that reads the adjacency matrix row by row is reading an arbitrary ordering. It learns the filing system, not the case."

### 3 — Reading the board `40s`
Minimal notation, all visual. A 5-node graph with:
- each node carrying a small feature card (3 coloured boxes = feature vector)
- adjacency matrix drawn beside it, with one cell highlighted and a TikZ arrow linking that cell to the corresponding edge (`remember picture, overlay`)

Two symbols only on screen: $X$ (what we know) and $A$ (who knows whom). Nothing else.

### 4 — The question `20s`
Single line, huge type, centred:

> **"How do I describe this person, if the answer depends on their neighbours?"**

Full stop. Let it sit. This is your pivot slide and it costs you nothing.

### 5–7 — Message passing, the heart of the talk `130s total`

This is a **three-slide animation on one fixed graph layout** — same node positions across all three so the audience tracks continuity. Budget your best TikZ effort here.

**5. Gather `45s`** — one node lights up gold. Its neighbours pulse. Little envelope glyphs travel along the strings inward (`\only<n>` at 4–5 positions along each path creates the motion without needing the `animate` package).

**6. Aggregate `40s`** — the arriving envelopes stack and collapse into one box. Show three options as swappable labels: `mean` / `sum` / `max`. Note in one clause why order-independence matters: **any of these gives the same answer no matter what order the messages arrive in — that's permutation invariance, and it's the fix for slide 2.**

**7. Update `45s`** — aggregated box + the node's own old card feed into a small box labelled $W$, out comes a new card with different colours. Then: **"and now every node has done this, simultaneously."** All ten nodes flip their cards at once.

> *Say (slide 7):* "That's it. That's a GNN layer. Gather, aggregate, update. Everything else in this field is an argument about which of those three steps to change."

### 8 — The one equation `55s`
Show it once, as a **picture with callouts**, not as maths:

$$h_v^{(k+1)} = \sigma\Big( W \cdot \text{AGG}\big(\{h_u^{(k)} : u \in \mathcal{N}(v)\}\big) \Big)$$

Use `tikzmark` to draw curved annotation arrows from each term to a plain-English label: *"the new card"*, *"the shuffle-proof combiner"*, *"my neighbours"*, *"squish it"*. Reveal one callout per overlay so nobody reads ahead.

> *Say:* "You've already understood this slide. This is the previous three slides written down."

### 9 — Depth = reach `45s`
Same graph, centre node fixed. Overlay 1: 1-hop ring glows. Overlay 2: 2-hop ring. Overlay 3: 3-hop. A counter in the corner reads `LAYERS: 1 → 2 → 3`.

Then the punchline overlay — at layer 6 every node fades to the identical grey. Caption: **over-smoothing.** *"Interrogate everyone long enough and they all tell the same story."* Most GNNs are 2–3 layers deep, and now they know why.

### 10 — Not all informants are equal `45s`
Same graph. Edges get variable thickness/opacity. Fat glowing string = high attention weight, thin faded string = low. Caption: **Graph Attention Networks — the model learns who to trust.**

One sentence on GCN vs GraphSAGE vs GAT, as three labels under the same picture: *average everyone / sample a few / weight them.* That's your whole architecture zoo, and it costs 15 seconds.

### 11 — What you can actually ask `40s`
Three mini-boards side by side, each with a different thing circled:
- **Node** — "is this account a fraudster?"
- **Edge** — "will these two become friends?" (link prediction)
- **Graph** — "is this whole molecule toxic?"

### 12 — The extravagant part `105s`
Your impact slide. Do **three**, each as a case file card that flips open. Skip social networks and recommender systems — everyone expects those.

**A. A new antibiotic.** MIT, 2020. They trained a GNN on molecules-as-graphs, pointed it at a library of ~100 million compounds, and it flagged one nobody had considered as an antibiotic. Named **halicin**. It killed strains of bacteria resistant to every existing drug, including *Acinetobacter baumannii*. A neural network read chemistry as a graph and found a drug humans had walked past.

**B. The weather.** DeepMind's **GraphCast** treats the planet as a mesh graph — grid points as nodes, neighbours as edges. It produces a 10-day global forecast in **under a minute on one machine**, against supercomputer models that take hours, and beat the European gold-standard system on the large majority of tested variables. Also flagged hurricane tracks earlier.

**C. The Large Hadron Collider.** Every proton collision sprays thousands of particle hits. Reconstructing which hits belong to the same track is a connect-the-dots problem at absurd scale — so physicists build a graph of candidate hits and let a GNN prune the edges. Graphs are being used to find new physics.

> *Close the slide:* "Molecules, the atmosphere, and subatomic particles. Three fields with nothing in common except that all three are graphs."

### 13 — Close `30s`
Return to the very first board image from slide 1, now with every node glowing and labelled. One line:

> **"If your data is a set of things and the relationships between them, it's a graph. And if it's a graph, a GNN can learn from the relationships — not just the things."**

---

# Technical Execution (this is your 8 marks)

The rubric rewards *tools*, so make the tooling visible.

**Packages:** `tikz` with libraries `calc, positioning, arrows.meta, decorations.pathmorphing, decorations.markings, backgrounds, fadings, shadows.blur, tikzmark, overlay-beamer-styles`.

**The techniques worth deliberately deploying:**
- `overlay-beamer-styles` gives you `visible on=<2->` and `alt=<2>{...}{...}` *inside* TikZ, which is how you animate a diagram without redrawing it four times. This alone will look more advanced than most decks in the room.
- `decorations.pathmorphing` with a `snake`/`random steps` decoration for string wobble — makes the red string look physical, not vector.
- `shadows.blur` on pins and cards for depth.
- `remember picture, overlay` to draw arrows between things on *different parts* of the slide (equation term → diagram element).
- `\only<n>` position stepping for the travelling-envelope animation. Cheaper and more reliable than the `animate` package, and it survives any PDF viewer.
- A custom footline: a thin "CASE PROGRESS" bar that fills across the talk. Section awareness + design polish in one element.

**Design discipline:**
- Corkboard base `#C9A66B` or near-black `#1A1614` with warm paper cards — pick one and never mix.
- Accent red `#C1272D` for string only. Nothing else is red.
- Max ~15 words per slide. Slides 4 and 13 have one sentence each.
- One font family, two weights. Body 20pt+.
- Every node position identical across slides 5–10. Continuity is what makes an audience feel like they're following one idea instead of watching ten pictures.

**Delivery (your 10 marks):** Slides 4, 7, and 13 are deliberate pause points — say the line, then stop talking for a beat. Rehearse the transition from slide 7 to 8 specifically; that's where you tell them they already understand the equation, and it only lands if you sound certain.

---
