# Graph Neural Networks — Presentation Plan

## The Overarching Story

> **"Normal neural networks are very good at understanding things that have an obvious order or grid.**
> **But what happens when the meaning of something depends on its relationships?"**

GNN is never introduced as an abstract mechanism or a taxonomy lecture. It is presented as the **inevitable mathematical solution** to a real limitation in classical neural networks.

---

## The 17-Block Narrative Structure (10:00 / 600s Total)

| Block | Timing | What the audience sees | Purpose | Why it exists |
|---|---|---|---|---|
| **1. Cold open / activity** | `0:00–0:45` (45s) | Single profile node (Dhaka, 24, 17 posts) &rarr; reveal connections to Bank and Scammers | Create curiosity / break assumption | Nobody should know yet that this is a GNN presentation. Preloads relational intuition. |
| **2. The CNN example** | `0:45–1:20` (35s) | Image &rarr; local patches &rarr; edges &rarr; shapes &rarr; object | Establish what NNs already do well | Gives the audience a familiar mental model of spatial locality. |
| **3. Name the CNN** | `1:20–1:40` (20s) | "Convolutional Neural Network (CNN)" | Give a name to what they just experienced | The name has meaning because the behavior was already demonstrated. |
| **4. Break the assumption** | `1:40–2:05` (25s) | Rigid 5&times;5 pixel grid vs. irregular graph side-by-side | Establish the structural limitation | "Pixel 37 has a neighbor. What is pixel 37 in a graph? There is no pixel 37." |
| **5. Obvious solutions 1 & 2** | `2:05–2:25` (20s) | 1. Disconnected nodes (lose bonds). 2. Store graph in adjacency matrix. | Show the natural first attempts | Makes the audience participate in the invention. |
| **6. The failure** | `2:25–3:00` (35s) | Same molecule, two atom numberings &rarr; predictions flip (0.83 vs 0.11) &rarr; Red X | Destroy the matrix solution | **Core reveal**: "The network learned our filing system, not the chemistry." |
| **7. The key question** | `3:00–3:25` (25s) | Text: "What is this node?" &rarr; strike through "is" &rarr; **"Who influences this node?"** | Create the exact question GNN solves | The conceptual birth of GNN. |
| **8. The GNN idea** | `3:25–4:00` (35s) | One node asks its neighbors &rarr; Gather &rarr; Aggregate &rarr; Update | Intuition before terminology | The audience understands message passing naturally before seeing formal math. |
| **9. Step-by-step GNN demo** | `4:00–5:35` (95s) | Alice, Bob, Carol, David, Eve &rarr; cards fly inward &rarr; combine &rarr; Alice updates &rarr; graph ripples | Concrete demonstration | Anchors representation learning in an intuitive, physical process. |
| **10. Intuitive equation** | `5:35–6:00` (25s) | Formal equation mapped with curved callout lines directly to the demo steps | Formal notation as a summary | Equation becomes a celebration of what they already know, not a speed bump. |
| **11. Depth = reach & over-smoothing** | `6:00–6:40` (40s) | 1 hop &rarr; 2 hops &rarr; 3 hops &rarr; Layer 6: all nodes fade to identical gray | Explain layer limits | "Interrogate everyone long enough and they all tell the same story." |
| **12. Attention & variants** | `6:40–7:10` (30s) | "What if every neighbor isn't equally important?" Variable edge thicknesses | Justify GAT / GraphSAGE / GCN | Audience now has a reason for architecture variants. |
| **13. Case study 1: Halicin** | `7:10–8:00` (50s) | Molecule as graph &rarr; 100M compound search &rarr; antibiotic killing *A. baumannii* | Real-world consequence | GNN understands relationships that matter chemically. |
| **14. Case study 2: GraphCast** | `8:00–8:40` (40s) | Planetary mesh graph &rarr; 10-day global forecast in <1 min on one machine | Demonstrate scale | Proves graphs aren't just molecules; atmosphere itself is a graph. |
| **15. Case study 3: CERN LHC** | `8:40–9:20` (40s) | Particle detector hits &rarr; candidate graph &rarr; GNN cuts wrong strings to track particles | Demonstrate breadth | Completely different field, identical underlying structure. |
| **16. The unifying picture** | `9:20–9:45` (25s) | Molecule + Planet + Detector cards side-by-side &rarr; dissolve into **GRAPH** | Intellectual payoff | "Different problems. Same structure. Whenever relationships are information, ignoring them throws data away." |
| **17. Final close** | `9:45–10:00` (15s) | Return to opening Dhaka profile and network | Close the narrative loop | "A GNN is simply a way to look at the things and the connections at the same time." |

---

## Slide-by-Slide Detailed Specification

### Scene 1 · Cold Open: Trust the Person or Trust the Network? `45s`
- **Visuals**: Dark corkboard. A single pinned suspect card:
  - `Location: Dhaka`, `Age: 24`, `Posts: 17`.
  - Question: *"Can you decide if this person is trustworthy?"*
  - First overlay: Strings snap outward to connected nodes:
    - `VERIFIED BANK` (top)
    - `SCAM ACCOUNT` (bottom left)
    - `SCAM ACCOUNT` (bottom right)
  - Second overlay: *"What if the person itself isn't the information? What if the connections are?"*
- **Takeaway**: Relational context holds the crucial signal.

### Scene 2 · The CNN Example: Exploiting Grid Structure `35s`
- **Visuals**: A high-resolution image decomposes into local 3&times;3 pixel patches.
  - Animated brackets highlight: Pixels &rarr; Edges &rarr; Patterns &rarr; Shapes &rarr; Object.
  - Highlight regular spatial grid: every pixel has predictable neighbors (top, bottom, left, right).
- **Takeaway**: Classical deep learning succeeds by exploiting rigid geometric structure.

### Scene 3 · Name the CNN `20s`
- **Visuals**: Clean, authoritative typographic stamp:
  - **Convolutional Neural Network (CNN)**
  - Subtitle: *"A network designed for data with an obvious spatial arrangement."*
- **Takeaway**: Name comes *after* the audience has experienced the mechanism.

### Scene 4 · Break the Assumption: Grid vs. Graph `25s`
- **Visuals**: Two side-by-side panels:
  - Left panel: Rigid 5&times;5 pixel grid with pixel #37 highlighted. *"Pixel 37 has predictable neighbors."*
  - Right panel: Irregular graph with arbitrary node connections. *"What is pixel 37 here? There is no pixel 37. Just things and relationships."*
- **Takeaway**: Natural and relational data does not fit into an image grid.

### Scene 5 · Obvious Solutions 1 & 2 `20s`
- **Visuals**:
  - Solution 1: Break all the strings. Isolated points: $\bullet \quad \bullet \quad \bullet \quad \bullet$. *"Throw away the relationships &rarr; throw away the answer."*
  - Solution 2: Write the graph into an adjacency matrix table $A$. *"Looks perfectly reasonable..."*
- **Takeaway**: Leads the audience directly into the trap of using traditional matrices.

### Scene 6 · The Failure: Permutation Sensitivity `35s`
- **Visuals**:
  - Two caffeine molecules shown side-by-side with identical bonds and atoms.
  - Only change: Node indexing (Atom 1 vs Atom 5).
  - Two adjacency matrices displayed:
    - Matrix 1 &rarr; Toxicity prediction: **0.83**
    - Matrix 2 &rarr; Toxicity prediction: **0.11**
  - Pulsing Red X stamp slams onto screen.
  - Killer punchline: *"The network learned our filing system, not the chemistry."*
- **Takeaway**: Relabeling nodes breaks standard neural networks; graphs require permutation invariance.

### Scene 7 · The Pivotal Question: "Invent GNN" `25s`
- **Visuals**: Single node floating in space. Large typography:
  - Display: **"What is this node?"**
  - Animation: Red string strikes through "is", replaced by glowing gold text:
  - Display: **"Who influences this node?"**
  - Subtitle: *"And that is the question ordinary neural networks weren't designed to ask."*
- **Takeaway**: Switches the paradigm from intrinsic node features to relational message passing.

### Scene 8 · The GNN Idea: Gather · Aggregate · Update `35s`
- **Visuals**: Central target node lights up in gold.
  - Three distinct conceptual steps revealed:
    1. **Gather**: Envelope glyphs travel along incident edges inward.
    2. **Aggregate**: Envelopes collapse into one order-independent container (`mean`/`sum`/`max`).
    3. **Update**: Combined message + target's previous state pass through shared weight matrix $W$.
  - All nodes on the board flip cards simultaneously.
- **Takeaway**: GNN is fundamentally three operations repeated everywhere.

### Scene 9 · Step-by-Step GNN Demo: The Alice Graph `95s`
- **Visuals**: Dedicated named graph layout:
  - **Alice** connected to **Bob** and **Carol**.
  - **David** connected to Bob; **Eve** connected to Carol.
  - Target question: *"Is Alice likely to be interested in Topic X?"*
  - **Step 1**: Alice inspects her card: `[Interest: Unknown, Activity: High]`.
  - **Step 2**: Bob and Carol send their feature cards along edges to Alice.
  - **Step 3**: Cards arrive and merge in an aggregation box.
  - **Step 4**: Alice updates her representation card: `[Interest: LIKELY (0.89)]`.
  - **Step 5**: The camera zooms out as Bob, Carol, David, and Eve execute the same step simultaneously.
- **Takeaway**: "The whole graph learns through conversations."

### Scene 10 · The Intuitive Equation `25s`
- **Visuals**: Single clean equation displayed in center:
  $$h_v^{(k+1)} = \sigma\Big( W \cdot \text{AGG}\big(\{h_u^{(k)} : u \in \mathcal{N}(v)\}\big) \Big)$$
  - Runtime SVG callout wires connect terms to plain-English labels:
    - $h_v^{(k+1)}$ &rarr; *"the new card"*
    - $\text{AGG}$ &rarr; *"the shuffle-proof combiner"*
    - $\mathcal{N}(v)$ &rarr; *"my neighbours"*
    - $\sigma$ &rarr; *"squish it"*
- **Takeaway**: "You already understood this slide. It is just the demo written down."

### Scene 11 · Depth = Reach & Over-smoothing `40s`
- **Visuals**: Fixed graph with layer counter:
  - Layer 1: 1-hop ring glows gold. *"I know my neighbours."*
  - Layer 2: 2-hop ring glows. *"I know my neighbours' neighbours."*
  - Layer 3: 3-hop ring glows. *"Three steps away."*
  - Layer 6: Warp pulse. Every node fades into an identical dull gray.
  - Caption: **Over-smoothing.** *"Interrogate everyone long enough and they all tell the same story."*
- **Takeaway**: Most production GNNs stay at 2–3 layers; deep learning instincts must be tempered.

### Scene 12 · Attention: Not All Informants Are Equal `30s`
- **Visuals**: Central node with edges of dynamically varying thickness and glow:
  - Thick glowing edge &rarr; High attention weight (expert/close friend).
  - Thin dim edge &rarr; Low weight (stranger/noise).
  - Bottom taxonomy chips:
    - **GCN**: Average everyone
    - **GraphSAGE**: Sample a few
    - **GAT**: Learn who to trust
- **Takeaway**: Explains why variants exist in one unified sentence.

### Scene 13 · Case Study 1: Halicin (Drug Discovery) `50s`
- **Visuals**: Full-screen electron micrograph of *Acinetobacter baumannii*.
  - Molecule card overlays.
  - Key facts: MIT, 2020. 100 million molecules screened as graphs.
  - Found **halicin**: killed pan-resistant pathogens humans had overlooked.
- **Takeaway**: GNN extracts functional biochemical meaning from relational graph topology.

### Scene 14 · Case Study 2: GraphCast (Global Weather) `40s`
- **Visuals**: Satellite imagery of Earth overlaid with an icosahedral mesh graph.
  - Atmospheric grid points as nodes; physical adjacency as edges.
  - DeepMind's **GraphCast**: 10-day global weather forecast in **< 1 minute on one machine**.
  - Outperformed European ECMWF gold-standard supercomputers on >90% of variables.
- **Takeaway**: Proves GNN scales from micro-scale chemistry to planetary-scale physics.

### Scene 15 · Case Study 3: CERN LHC (Particle Tracking) `40s`
- **Visuals**: High-energy collision visual inside CERN's CMS/ATLAS detector.
  - Thousands of sensor hits form a dense cloud.
  - GNN builds candidate hit graph and cuts false edges to isolate true particle tracks.
  - Caption: *"A connect-the-dots problem at absurd physical scale."*
- **Takeaway**: Proves GNN is a general-purpose relational engine across all scientific disciplines.

### Scene 16 · The Unifying Picture `25s`
- **Visuals**: Three cards side-by-side:
  - `[MOLECULE: Atoms + Bonds]`
  - `[ATMOSPHERE: Grid points + Air flow]`
  - `[COLLIDER: Detector hits + Trajectories]`
  - All three images fade away, leaving behind one bold, glowing word:
  - **G R A P H**
  - Caption: *"Different problems. Same underlying structure."*
- **Takeaway**: The ultimate intellectual payoff of the talk.

### Scene 17 · Final Question & Close `15s`
- **Visuals**: Returns to the opening Dhaka suspect node and its network.
  - Closing line:
    > *"Whenever relationships are part of the information, throwing those relationships away is throwing information away.*
    > *A Graph Neural Network is simply how we teach neural networks to look at the things and the connections at the same time."*
- **Takeaway**: Complete, elegant narrative closure.

---

## Technical & Visual Design Guidelines

1. **Palette**:
   - Background: Dark investigative corkboard (`#0A0806` to `#241C17`)
   - Accent String: Crimson Red (`#C1272D` exclusively for connections and critical stamps)
   - Accents: Brass (`#C9A66B`) and Warm Gold (`#F0C46A` for active message passing)
   - Paper Cards: Warm parchment (`#E8DCC4` to `#C6B08A`) with tactile drop shadows
2. **Typography**:
   - Headlines: `Big Shoulders Display` (800 weight, impactful and editorial)
   - Body: `Spline Sans` (clean, readable, 24px+ for live stage viewing)
   - Metadata / Tags: `Courier Prime` (typewriter/casefile aesthetic)
3. **Pacing Discipline**:
   - Max 15 words per slide on concept moments; zero clutter.
   - Pause points at Scenes 1, 6, 7, 10, and 17: deliver the punchline and pause for 2 beats.
