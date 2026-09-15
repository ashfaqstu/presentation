# Case File: Graph Neural Networks — Master Slide-by-Slide Speaker Script

**Deck Target**: [gnn-deck.tex](file:///c:/Users/user/Desktop/presentation/gnn-deck.tex) / [gnn-deck.pdf](file:///c:/Users/user/Desktop/presentation/gnn-deck.pdf)
**Total Slides**: 33 Slides (111 PDF Pages)
**Target Duration**: 10:00 – 11:30 Total Runtime
**Delivery Style**: Conversational, investigative, Veritasium-style causal progression (*Puzzle → Failure → Mathematical Discovery → Real-World Consequence*).

---

## Quick Navigation & Presentation Outline

| Act | Scene | Slides | Topic | Target Time |
|---|---|---|---|---|
| **Act I: The Gap** | Scene 01 | **Slide 01 – 02** | Cold Open: Mbappé and His Connections | `0:00 - 0:45` |
| | Scene 02 | **Slide 03 – 04** | The CNN Example: Exploiting Spatial Grids | `0:45 - 1:20` |
| | Scene 03 | **Slide 05** | Name the CNN: Convolutional Neural Networks | `1:20 - 1:40` |
| | Scene 04 | **Slide 06** | Grid vs. Graph: Breaking the Spatial Assumption | `1:40 - 2:05` |
| | Scene 05 | **Slide 07** | Obvious Solutions 1 & 2: Discard Edges vs. Adjacency Matrix | `2:05 - 2:25` |
| | Scene 06 | **Slide 08 – 09** | The Failure: Permutation Sensitivity & The Red X | `2:25 - 3:00` |
| **Act II: The Mechanism** | Scene 07 | **Slide 10** | The Pivotal Question: "Who influences this node?" | `3:00 - 3:25` |
| | Scene 08 | **Slide 11** | The GNN Idea: Gather → Aggregate → Update | `3:25 - 4:00` |
| | Scene 09 | **Slide 12 – 17** | Run It By Hand: Alice's Graph (Real Numbers Worked Demo) | `4:00 - 6:30` |
| | Scene 10 | **Slide 18** | The Formal Equation: Mathematical Summary | `6:30 - 7:10` |
| | Architecture | **Slide 19 – 21** | Predictions, Fraud Detection & The 3 Graph Tasks | `7:10 - 7:50` |
| **Act III: Nuance & Impact**| Scene 11 | **Slide 22 – 23** | Depth = Reach & Over-Smoothing at Layer 6 | `7:50 - 8:30` |
| | Scene 12 | **Slide 24 – 25** | Attention (GAT) & The Architecture Zoo (GCN, GraphSAGE) | `8:30 - 9:05` |
| | Scene 13 | **Slide 26** | Case Study 1: Halicin & Antibiotic Discovery (MIT) | `9:05 - 9:45` |
| | Scene 14 | **Slide 27 – 28** | Case Study 2: GraphCast & Planetary Weather (DeepMind) | `9:45 - 10:20` |
| | Scene 15 | **Slide 29 – 30** | Case Study 3: CERN LHC Particle Trajectory Tracking | `10:20 - 10:55` |
| | Scene 16 | **Slide 31 – 32** | The Unifying Picture: Molecules, Planet, Particles → GRAPH | `10:55 - 11:15` |
| | Scene 17 | **Slide 33** | Final Close: Thank You | `11:15 - 11:30` |

---

# ACT I: THE GAP
*Why ordinary neural networks break when the world has no grid.*

---

### Slide 01–02 [Pages 1–9] · Scene 01: Cold Open — Mbappé and His Connections
**Visuals**: One slide that builds click by click on a warm cream background. Mbappé is the central node. Three photos arrive as neighbouring nodes, each joined to him by an edge with the relationship written on it in orange: `PITCH STAFF — ordered to mop the pitch`, `THE REFEREE — told how to referee`, `YOU, THE VIEWER — stared down through the screen`. An arrow then leads from Mbappé down to a red `DICTATOR?` (of the penalty box). Finally the title becomes the two questions, and every edge turns orange.

- **[Page 1 / Initial]** *(Mbappé alone: KYLIAN MBAPPÉ · FORWARD · WORLD CUP WINNER)*
  > "Can we trust this person?
  > Kylian Mbappé. Forward. World Cup winner."

- **[Page 2 / Click 1]** *(On his own, nothing looks suspicious.)*
  > "Look at him on his own. Nothing suspicious. Completely normal footballer."

- **[Page 3 / Click 2]** *(Pitch staff photo + edge: ordered to mop the pitch)*
  > "But let's look at how he interacts with the people around him.
  > Here he is with the pitch staff... ordering them to mop the pitch."

- **[Page 4 / Click 3]** *(Referee photo + edge: told how to referee)*
  > "Here he is with the referee. Telling the referee how to referee."

- **[Page 5 / Click 4]** *(Viewer photo + edge: stared down through the screen)*
  > "And here he is with... you. Staring you down, straight through the TV."

- **[Page 6 / Click 5]** *(Wait... why is everyone taking orders from this guy?)*
  *(Pause. Let the audience connect it themselves.)*
  > "Wait. Why is everyone taking orders from this guy?"

- **[Page 7 / Click 6]** *(Arrow: INFERRED FROM HIS CONNECTIONS → DICTATOR? (of the penalty box))*
  *(Deadpan. Wait for the laugh.)*
  > "Dictator. Of the penalty box.
  >
  > Notice we never learned a single new fact about Mbappé himself. Everything we concluded came from the edges: how he treats other people."

- **[Page 8 / Click 7]** *(Title becomes: What if the person itself isn't the information?)*
  *(Drop the comedy. Slow down.)*
  > "So what if the person itself isn't the information?"

- **[Page 9 / Click 8]** *(What if the connections are? · every edge turns orange)*
  > "What if the **connections** are?
  >
  > So how do we normally make machines understand structured information?
  > Let's start with something neural networks are really good at."

---

### Slide 03 [Pages 10–12] · Scene 02: The CNN Example — The Grid Assumption
**Visuals**: A crisp 5x5 regular pixel grid appears. At Click 1, a golden 3x3 convolution patch highlights.

- **[Page 10 / Initial]**
  > "Imagine this is an image. Each square is one pixel.
  > Deep learning is famously good at images, so let's see why."

- **[Page 11 / Click 1]** *(Golden 3x3 convolution window highlights on the grid)*
  > "Suppose I give this image to a neural network. It succeeds because this image has rigid, predictable structure. Every pixel has an obvious neighbourhood: a pixel above it, below it, left, and right."

- **[Page 12 / Click 2]** *(Subtitle: A neural network doesn't need to swallow the whole canvas at once.)*
  > "A network doesn't need to swallow the entire image all at once. It can slide a local 3-by-3 window across predictable coordinates."

---

### Slide 04 [Pages 13–18] · Scene 02: The CNN Example — The Hierarchy
**Visuals**: Left: 5x5 pixel grid. Right: Vertical pipeline revealing Pixels → Edges → Patterns → Shapes → Object Recognized.

- **[Page 13 / Initial]** *(Pixels chip appears)*
  > "Because of that spatial regularity, we can think of a CNN as building increasingly complex features out of local patterns. Conceptually, pixels combine..."
- **[Page 14 / Click 1]** *(Edges)*
  > "...into edges."
- **[Page 15 / Click 2]** *(Patterns)*
  > "Edges combine into patterns."
- **[Page 16 / Click 3]** *(Shapes)*
  > "Patterns combine into shapes."
- **[Page 17 / Click 4]** *(Object Recognized in gold)*
  > "And shapes combine into an object recognized."
- **[Page 18 / Click 5]** *(Bottom takeaway: Why does this work? Rigid geometric order)*
  *(Firm, authoritative tone)*
  > "Why does this work so brilliantly? Because an image possesses an obvious, rigid geometric order."

---

### Slide 05 [Pages 19–21] · Scene 03: Name the CNN
**Visuals**: High-impact editorial title: *Convolutional Neural Network*, followed by *CNN* badge.

- **[Page 19 / Initial]**
  > "This architecture has a name you already know:"
- **[Page 20 / Click 1]** *(CNN badge pops)*
  > "A Convolutional Neural Network. A CNN."
- **[Page 21 / Click 2]** *(Subtitle: A network designed for data with an obvious spatial arrangement.)*
  > "CNNs are brilliant, but they come with a hidden contract: they only work because the world we handed them was neatly laid out on a grid."

---

### Slide 06 [Pages 22–25] · Scene 04: Grid vs. Graph — Breaking the Assumption
**Visuals**: Left panel: 5x5 pixel grid with cell #37 in amber. Right panel: An irregular, asymmetric graph with 6 nodes connected by crimson edges.

- **[Page 22 / Initial]** *(Pixel 37 on left grid)*
  > "In an image, pixel number 37 has predictable neighbours. Left, right, top, bottom. Its geometry is fixed."
- **[Page 23 / Click 1]** *(Right panel prompt: What happens when the data has no grid?)*
  *(Shift gaze to the right side of the screen.)*
  > "CNNs work because images have a grid.
  > But what happens when our data doesn't?"
- **[Page 24 / Click 2]** *(Irregular graph appears)*
  > "Look over here. What is pixel 37 in this graph?"
- **[Page 25 / Click 3]** *(Bottom punchline: There is no pixel 37. Only things and relationships.)*
  *(Slow down. Emphasize every word.)*
  > "There is no pixel 37. There are no rows. No columns. No left-to-right scanning order.
  >
  > There are only things... and relationships between those things."

---

### Slide 07 [Pages 26–30] · Scene 05: Obvious Solutions 1 & 2
**Visuals**: Left: Solution 1 (Discard the edges → isolated dots). Right: Solution 2 (Flatten the adjacency matrix: $A \rightarrow$ [0,1,0,1, 1,0,1,0, …]).

- **[Page 26 / Initial]** *(Solution 1: Discard the edges)*
  > "So how do we feed a graph into deep learning? There are two obvious ideas that everyone tries first.
  >
  > Idea number one: throw away the edges. Treat every node as an isolated dot."
- **[Page 27 / Click 1]** *(LOSES GRAPH STRUCTURE · What if we keep them?)*
  > "That throws away the very information we care about. The cold open already showed us the edges hold the secret."
- **[Page 28 / Click 2]** *(Solution 2: Flatten the adjacency matrix)*
  > "Fine. Let's preserve those connections in a form a conventional model can process.
  > Write the graph as an adjacency matrix of ones and zeros, flatten it into one long row, and feed that row into a standard neural network."
- **[Page 29 / Click 3]** *(SENSITIVE TO NODE ORDERING)*
  > "The matrix itself is perfectly good graph data. The problem is what a standard network does with it: it treats position 1 of that row as meaning something specific. And position 1 depends on how we numbered the nodes."
- **[Page 30 / Click 4]** *(Why do naive approaches fail?)*
  *(Lean in slightly; deliver as a cliffhanger)*
  > "Why would that matter? Watch."

---

### Slide 08 [Pages 31–36] · Scene 06: The Failure — Permutation Sensitivity
**Visuals**: Left: Caffeine molecule (Numbering A: 1-6) with Toxicity: 0.83. Right: Exact same molecule renumbered (Numbering B: 4,1,6,2,5,3) with Toxicity: 0.11. Top line: `TASK: PREDICT WHETHER THIS MOLECULE IS TOXIC`. Both numbers are tagged `ILLUSTRATIVE PREDICTION`.

- **[Page 31 / Initial]** *(Header: Same molecule. Same atoms. Same bonds.)*
  > "Now imagine the graph isn't just anonymous dots. Imagine the nodes are atoms, and the edges are chemical bonds.
  > Suppose we're trying to predict whether this molecule is toxic.
  >
  > Six atoms, seven bonds. We number the atoms 1, 2, 3, 4, 5, 6."
- **[Page 32 / Click 1]** *(Green toxicity card: 0.83)*
  > "We flatten its adjacency matrix and feed it to the network. Suppose the model predicts toxicity 0.83. *(These numbers are an illustration, not a real model's output.)*"
- **[Page 33 / Click 2]** *(Center question: What if we simply renumber the atoms?)*
  > "Now, what if another scientist writes down the exact same molecule, but numbers the atoms in a different order?"
- **[Page 34 / Click 3]** *(Numbering B appears with identical bonds)*
  > "Same atoms. Same bonds. Nothing in the physical universe changed."
- **[Page 35 / Click 4]** *(Red toxicity card: 0.11)*
  > "We feed the new matrix in. Now suppose the same model says 0.11. Non-toxic."
- **[Page 36 / Click 5]** *(Bottom takeaway)*
  > "The rows and columns swapped places, and the neural network gave a completely contradictory answer."

---

### Slide 09 [Pages 37–40] · Scene 06: The Failure — The Red X
**Visuals**: Numbering A vs. Numbering B, each with its 6×6 adjacency matrix drawn above its toxicity number (filled square = bond). The two matrices have visibly different filling patterns, with `SAME BONDS · DIFFERENT FILLING` between them. Toxicity 0.83 vs. 0.11. A bold crimson X lands across Numbering B's matrix and prediction.

- **[Page 37 / Initial]**
  > "Here are the two adjacency matrices the network actually saw. Same seven bonds, but because we numbered the atoms differently, the ones land in completely different cells.
  > Toxicity 0.83. Toxicity 0.11. Same molecule. Two opposite predictions."
- **[Page 38 / Click 1]** *(Massive crimson X slams onto screen)*
  *(Pause for one full second. Let the visual strike home.)*
  > "This is a catastrophic failure."
- **[Page 39 / Click 2]** *(Amber text: The network learned our filing system.)*
  > "The network didn't learn chemistry."
- **[Page 40 / Click 3]** *(Bold dark text: It never learned the chemistry.)*
  *(Speak with absolute conviction)*
  > "The network learned our **filing system**. It memorized which row we wrote first.
  >
  > The model saw the atoms. It saw the numbers. But it never understood the relationships.
  > So what information were we actually missing?"

---

# ACT II: THE MECHANISM
*Inventing the GNN: Gather, Aggregate, Update.*

---

### Slide 10 [Pages 41–44] · Scene 07: The Pivotal Question
**Visuals**: Left: three questions stack up, each earlier one fading as the next appears. Right: a single node → its neighbours appear → gold arrows show influence flowing in.

- **[Page 41 / Initial]** *(What is this node?)*
  > "The relationships. So let's change the question we ask.
  > Classical machine learning asks: *What is this node?* What are its own features?"
- **[Page 42 / Click 1]** *(What is connected to it? · neighbours appear)*
  > "But that's exactly what failed. So ask instead: *What is connected to it?*
  > Remember Mbappé: his own card looked clean. His neighbours didn't."
- **[Page 43 / Click 2]** *(Who influences this node? · arrows flow inward)*
  *(Pause. Emphasize the word 'influences'.)*
  > "And then the real question: **Who influences this node?**"
- **[Page 44 / Click 3]** *(RELATIONAL REASONING)*
  > "That's relational reasoning, and it's the question ordinary neural networks were never designed to ask."

---

### Slide 11 [Pages 45–50] · Scene 08: The GNN Idea
**Visuals**: A target node with 3 neighbours. Three plain sentences come first; the step chips only appear once the steps are named.

- **[Page 45 / Initial]** *(We need to use the neighbourhood.)*
  > "So if the answer lives in the connections, we need to use the neighbourhood."
- **[Page 46 / Click 1]** *(That is the idea behind a Graph Neural Network.)*
  > "That is the whole idea behind a Graph Neural Network."
- **[Page 47 / Click 2]** *(It passes messages between connected nodes. · MESSAGE PASSING)*
  *(Pause here. Let the idea land before naming any steps.)*
  > "It works by passing messages between connected nodes."
- **[Page 48 / Click 3]** *(Envelopes fly in. Chips appear; 1. GATHER lights)*
  > "One round of that has three steps. **Gather**: every neighbour hands over a copy of what it knows."
- **[Page 49 / Click 4]** *(Sum box. 2. AGGREGATE lights)*
  > "**Aggregate**: blend those messages into one summary, without caring who spoke first."
- **[Page 50 / Click 5]** *(Node turns amber. 3. UPDATE lights)*
  > "**Update**: the node mixes that summary into its own description of itself.
  > That sounds abstract, so let's run one by hand with real numbers."

---

### Slide 12 [Page 51] · Scene 09: Run It By Hand — Setup
**Visuals**: Five people on screen: Alice in the center, connected to Bob and Carol; David connected to Bob, Eve connected to Carol. Right panel: Dossier worksheet with two vector slots: Activity and Topic X.

- *(Point to: Graph appears)*
  > "Here is our test case. Five people in a social graph.
  > Our question: **Is Alice likely to be interested in Topic X?**"
- *(Point to: Slot definitions on worksheet)*
  > "Every person carries a card with just two numbers.
  > Slot 1 is **Activity**: how active they are, from 0 to 1.
  > Slot 2 is **Topic X**: how much they engage with Topic X, from 0 to 1."
- *(Point to: The five cards listed)*
  > "Bob and Carol love Topic X: they are at 1.00.
  > David and Eve are at 0.00."
- *(Point to: Alice's Topic X is marked UNKNOWN)*
  > "Look at Alice: her Topic X slot is blank --- stored as 0.00.
  > Her own card cannot answer the question."
- *(Point to: Progress strip: = ONE LAYER)*
  > "One layer of a GNN consists of three steps. Let's run all three by hand."

---

### Slide 13 [Page 52] · Scene 09: Run It By Hand — Step 1: Gather
**Visuals**: Amber arrows run from Bob and Carol into Alice, with their messages on the edges. David and Eve are dimmed.

- *(Point to: Header: Step 1 of 3 --- GATHER)*
  > "Step 1: Gather.
  > We ask: who is exactly one hop away from Alice?"
- *(Point to: Bob and Carol light up in amber)*
  > "Bob and Carol. That is her 1-hop neighbourhood."
- *(Point to: David and Eve dim to gray)*
  > "David and Eve are two hops away. In this round, they sit out."
- *(Point to: Bob's card vector [0.60, 1.00] copies onto the edge)*
  > "What is a message? Bob simply makes a copy of his card and sends it along the edge: 0.60, 1.00."
- *(Point to: Carol's card vector [0.40, 1.00] copies onto the edge)*
  > "Carol sends a copy of hers: 0.40, 1.00."
- *(Point to: Worksheet summary: Gathering is copying, not deciding)*
  > "Alice's inbox now holds two vectors. Notice: nothing has been merged yet, and Alice's own card hasn't changed. Gathering is copying, not deciding."

---

### Slide 14 [Page 53] · Scene 09: Run It By Hand — Step 2: Aggregate
**Visuals**: Worksheet calculates the slot-by-slot average. Neighbourhood badge under Alice: [0.50, 1.00]. An order-invariance line shows mean(Bob, Carol) = mean(Carol, Bob).

- *(Point to: Header: Step 2 of 3 --- AGGREGATE)*
  > "Step 2: Aggregate. Two vectors arrived in Alice's inbox. We need one summary vector out."
- *(Point to: Bob and Carol's vectors displayed)*
  > "Bob sent [0.60, 1.00]. Carol sent [0.40, 1.00]."
- *(Point to: Rule: average them slot by slot)*
  > "Our aggregation rule: take the mean, slot by slot."
- *(Point to: Activity: (0.60 + 0.40) / 2 = 0.50)*
  > "Slot 1 Activity: 0.60 plus 0.40 divided by 2 gives 0.50."
- *(Point to: Topic X: (1.00 + 1.00) / 2 = 1.00)*
  > "Slot 2 Topic X: 1.00 plus 1.00 divided by 2 gives 1.00."
- *(Point to: Neighbourhood vector m(Alice) = [0.50, 1.00])*
  > "So her neighbourhood summary vector is [0.50, 1.00]."
- *(Point to: The Shuffle Test)*
  *(Gesture firmly)*
  > "Why an average? Try the shuffle test. Put Carol first and Bob second: 0.40 plus 0.60 divided by 2 is STILL 0.50. Identical."
- *(Point to: Bottom takeaway)*
  > "This directly solves the molecule failure! The answer can never depend on the arbitrary order we list neighbours in."

---

### Slide 15 [Page 54] · Scene 09: Run It By Hand — Step 3: Update
**Visuals**: Worksheet shows linear combination of Alice's own card + neighbourhood summary. Alice's card is shown already rewritten in amber: [0.65, 0.50].

- *(Point to: Header: Step 3 of 3 --- UPDATE)*
  > "Now Step 3: Update. Alice doesn't throw her own identity away. She mixes herself with her neighbours."
- *(Point to: Mine: [0.80, 0.00], Theirs: [0.50, 1.00])*
  > "Her own card was [0.80, 0.00]. Her neighbourhood summary is [0.50, 1.00]."
- *(Point to: Formula: new = 0.5 x mine + 0.5 x theirs)*
  > "The update rule: 50% of her own card, plus 50% of her neighbours. Those percentages are the trainable neural network weights $W$."
- *(Point to: Activity: 0.5(0.80) + 0.5(0.50) = 0.65)*
  > "Activity: half of 0.80 is 0.40. Half of 0.50 is 0.25. Sum: 0.65."
- *(Point to: Topic X: 0.5(0.00) + 0.5(1.00) = 0.50)*
  > "Topic X: half of zero is zero. Half of 1.00 is 0.50. Sum: 0.50!"
- *(Point to: Activation function $\sigma$)*
  > "A non-linear activation like ReLU or sigmoid squashes it, keeping it in range."
- *(Point to: Alice's card turns amber: [0.65, 0.50] with CARD REWRITTEN)*
  *(Smile, tone of breakthrough)*
  > "Look at Alice's card now: [0.65, 0.50]. Her card has been rewritten!"

---

### Slide 16 [Page 55] · Scene 09: Run It By Hand — The Answer
**Visuals**: Before vs. After side-by-side comparison. Classification readout calculates $p = \sigma(2.10) = 89\%$. LIKELY INTERESTED badge.

- *(Point to: Before: Alice [0.80, 0.00])*
  > "Look at what just happened. Before round 1, Alice had a zero on Topic X."
- *(Point to: After: Alice [0.65, 0.50])*
  > "After round 1, Alice sits at 0.50."
- *(Point to: Text: Nothing about Alice changed)*
  > "Nothing about Alice herself changed. Not her age, not her location, not her posts."
- *(Point to: Classification equation: $p = \sigma(6 \times 0.50 - 0.9) = \sigma(2.10)$)*
  > "Now, a simple one-layer classifier takes that 0.50 and computes: sigmoid of 2.1..."
- *(Point to: Green badge: LIKELY INTERESTED: 89%)*
  > "...giving 0.89. An 89% probability that Alice is interested in Topic X!"
- *(Point to: Bottom takeaway)*
  > "It's the cold open all over again --- but this time, it isn't a human gut feeling. It is pure, rigorous arithmetic."

---

### Slide 17 [Page 56] · Scene 09: Run It By Hand — All At Once
**Visuals**: The full 5-node graph with every card already updated after round 1. All Topic X slots read 0.50.

- *(Opening line)*
  > "And remember: Alice wasn't special."
- *(Point to: All cards flip at once! ROUND 1 COMPLETE)*
  > "Every node on the board ran the exact same three steps at the exact same moment."
- *(Point to: David and Eve highlighted)*
  > "David and Eve updated too. Because David is connected to Bob, David absorbed Topic X signal as well."
- *(Point to: All Topic X slots read 0.50)*
  > "Look at the Topic X slot across all five people: 0.50, 0.50, 0.50, 0.50, 0.50. The signal diffused across the network."
- *(Point to: Cliffhanger: Hold that thought --- it is about to become a problem.)*
  *(Wry smile, dramatic pause)*
  > "Hold that thought... because in three slides, that is going to become a serious problem."

---

### Slide 18 [Pages 57–58] · Scene 10: The Formal Equation (two static slides)
**Visuals**: The full GNN equation $h_v^{(k+1)} = \sigma(W_{\text{self}} h_v^{(k)} + W_{\text{nbr}} \text{AGG}(\{h_u^{(k)} : u \in \mathcal{N}(v)\}))$ on both slides. Part 1 highlights the neighbours' side and dims Alice's own terms; Part 2 does the reverse. Every callout carries a number from Alice's run.

**Page 57 · Part 1 — What the neighbours contribute**
- *(Opening line)*
  > "Here is the master equation of Graph Neural Networks. Don't let the notation intimidate you --- you have already calculated every single symbol by hand. Start with the bright half: the neighbours."
- *(Point to: my neighbours {Bob, Carol})*
  > "$\mathcal{N}(v)$ is Alice's neighbours: Bob and Carol."
- *(Point to: each neighbour's current card)*
  > "$h_u$ is each neighbour's current card --- Bob's is [0.60, 1.00]."
- *(Point to: the shuffle-proof combiner)*
  > "$\text{AGG}$ is the permutation-invariant aggregator --- our average, [0.50, 1.00]."
- *(Point to: how much of them)*
  > "$W_{\text{nbr}}$ is the learned weight: how much to trust the neighbours. We used 0.5. That half of the equation is Gather and Aggregate."

**Page 58 · Part 2 — What Alice keeps, and the new card**
- *(Point to: how much of me)*
  > "Now the other half. $W_{\text{self}}$ is how much Alice keeps of her own previous card: 0.5 times [0.80, 0.00]."
- *(Point to: squash it back into range)*
  > "$\sigma$ is the activation function squashing it into range."
- *(Point to: Alice's new card [0.65, 0.50])*
  > "And on the left: $h_v^{(k+1)}$ --- Alice's updated card."
- *(Point to: Gather · Aggregate · Update)*
  > "Whenever you read a research paper with this equation, don't get lost in tensor indices. Just remember: **Gather. Aggregate. Update.**"

---

### Slide 19 [Page 59] · Architecture: From Embeddings to Decisions
**Visuals**: 3-stage pipeline: Raw Input $x_v$ → $K$-Layer GNN → Final Vector $h_v^{(K)}$.

- *(Point to: Raw Input box)*
  > "Now, how does this solve real-world problems in production? We start with raw tabular features: age, location, timestamp."
- *(Point to: K-Layer GNN box lights up in gold)*
  > "We pass them through $K$ layers of Gather, Aggregate, Update."
- *(Point to: Final Vector $h_v^{(K)}$ lights up in green)*
  > "Out comes a rich mathematical embedding vector $h_v^{(K)}$."
- *(Point to: Takeaway text)*
  > "After $K$ layers, that vector no longer represents just the isolated node. It encodes the entire relational story of its $K$-hop neighbourhood."

---

### Slide 20 [Pages 60–64] · Solving the Crime: Fraud Detection
**Visuals**: Left: Target #4091 embedding card containing Bank and Scam ring connections. Right: Softmax head fires → Crimson box: FRAUDULENT 94.2%.

- **[Page 60 / Initial]** *(Suspect embedding card)*
  > "Let's return to our opening crime scene in Dhaka. Target #4091."
- **[Page 61 / Click 1]** *(Embedding contents revealed)*
  > "The GNN compressed their network into their final embedding: 1 verified bank, 2 flagged scam rings."
- **[Page 62 / Click 2]** *(Gold arrow & Softmax Head)*
  > "We pass that embedding into a simple softmax classifier head."
- **[Page 63 / Click 3]** *(Red banner: FRAUDULENT 94.2%)*
  *(Punchy delivery)*
  > "Output: Fraudulent with 94.2% confidence."
- **[Page 64 / Click 4]** *(Bottom takeaway)*
  > "The GNN closed the cold open. Guilt by association, proven mathematically."

---

### Slide 21 [Pages 65–68] · The Three Graph Prediction Tasks
**Visuals**: Three dossier cards side-by-side: Node Level (Classification), Edge Level (Link Prediction), Graph Level (Property Test).

- **[Page 65 / Initial]** *(Node Level card)*
  > "And that same mechanism solves every graph problem in computer science across three distinct levels:
  > First, **Node Level**: Is this individual account a scammer? Will this customer churn?"
- **[Page 66 / Click 1]** *(Edge Level card)*
  > "Second, **Edge Level**: Will an edge form between these two nodes? This powers recommendation engines and friend suggestions on LinkedIn or Instagram."
- **[Page 67 / Click 2]** *(Graph Level card)*
  > "Third, **Graph Level**: Pool all node vectors together to predict a property of the whole graph: Is this entire molecule toxic? Is this financial network experiencing systemic risk?"
- **[Page 68 / Click 3]** *(Bottom takeaway)*
  > "One unified engine powers all three levels of prediction."

---

# ACT III: NUANCE & REAL-WORLD IMPACT
*Layer limits, attention mechanisms, and world-changing applications.*

---

### Slide 22 [Pages 69–72] · Scene 11: Depth = Reach
**Visuals**: Central node with concentric dashed circular reach boundaries: Layer 1 (1 hop) → Layer 2 (2 hops).

- **[Page 69 / Initial]**
  > "Now, an intuitive question arises: if one layer let Alice hear from her direct neighbours..."
- **[Page 70 / Click 1]** *(LAYER 1 badge in gold, 1.8cm dashed circle)*
  > "...what happens if we stack a second layer?"
- **[Page 71 / Click 2]** *(LAYER 2 badge, circle expands to 2.8cm, outer nodes illuminate)*
  > "In Layer 2, Alice's neighbours have already gathered from *their* neighbours. So Alice now hears from David and Eve --- two hops out!"
- **[Page 72 / Click 3]** *(Takeaway: Depth is reach)*
  > "In a GNN, **depth is reach**. Each extra layer widens the horizon of who a node can hear."

---

### Slide 23 [Pages 73–74] · Scene 11: Over-Smoothing — Disaster at Layer 6
**Visuals**: Top corner: LAYER 6 in crimson. All nodes wash out to identical, faint gray circles. Crimson title: OVER-SMOOTHING.

- **[Page 73 / Initial]** *(Layer 6 counter, washed out gray nodes, OVER-SMOOTHING title)*
  > "So in deep learning, we always want more layers, right? In CNNs we use 50 or 100 layers. What happens if we stack 6 layers in a GNN?"
  *(Pause. Point to the faded, washed-out nodes.)*
  > "Disaster."
- **[Page 74 / Click 1]** *(Both explanation bullets appear together)*
  *(Slow, deliberate delivery)*
  > "Remember Alice's demo: after just one round, every single person's Topic X slot already read 0.50.
  >
  > If you interrogate everyone in a graph long enough, eventually everybody repeats the exact same consensus story. All node vectors collapse to identical gray mush.
  >
  > This is called **over-smoothing**.
  > And that is why almost all production GNNs stop at just 2 or 3 layers."

---

### Slide 24 [Pages 75–78] · Scene 12: Attention — Not All Informants Are Equal
**Visuals**: Alice between Bob and Carol. At Click 2, the edge to Bob thickens into glowing gold ($\alpha = 0.88$), while the edge to Carol fades to a thin hairline ($\alpha = 0.12$).

- **[Page 75 / Initial]** *(We averaged Bob and Carol equally. Should we have?)*
  > "Here is another flaw in our hand demo. We averaged Bob and Carol 50/50.
  >
  > But should we have?"
- **[Page 76 / Click 1]** *(Red strings between nodes)*
  > "What if Bob is a verified world expert on Topic X, and Carol is a casual observer?"
- **[Page 77 / Click 2]** *(Bob's edge turns into a 4pt golden beam ($\alpha = 0.88$); Carol's turns into a faint line ($\alpha = 0.12$))*
  *(Point with enthusiasm)*
  > "Why should Alice listen to them equally? She shouldn't!
  > The network should learn attention weights $\alpha$."
- **[Page 78 / Click 3]** *(Bob node glows in gold, Carol dims)*
  > "Give 88% of your attention to the expert, and only 12% to the stranger."

---

### Slide 25 [Pages 79–83] · Scene 12: The Architecture Zoo
**Visuals**: Three architecture cards: GCN (Average everyone), GraphSAGE (Sample a few), GAT (Learn who to trust).

- **[Page 79 / Initial]** *(GCN card)*
  > "That single realization gives rise to the entire family of modern GNN architectures:
  > Average everyone equally: that's **GCN** (Graph Convolutional Network)."
- **[Page 80 / Click 1]** *(GraphSAGE card)*
  > "When the graph has billions of nodes and you can't listen to everyone: sample a random subset. That's **GraphSAGE**."
- **[Page 81 / Click 2]** *(GAT card highlighted in amber)*
  > "Learn dynamically who to trust using attention: that's **GAT** (Graph Attention Network)."
- **[Page 82 / Click 3]** *(Header: Not every relationship is equally useful)*
  > "Not every relationship is equally useful."
- **[Page 83 / Click 4]** *(Bottom takeaway)*
  > "Every modern GNN variant in the literature is simply a refined answer to one of three questions: how to gather, how to aggregate, or who to listen to."

---

### Slide 26 [Pages 84–89] · Scene 13: Case Study 1 — Halicin (Drug Discovery)
**Visuals**: Parchment dossier on left: *MIT · 2020 Halicin*. Right: Chemical ring graph with Carbon (C) and Nitrogen (N) nodes connected by crimson bonds. Green badge: *Killed Pan-Resistant Bacteria*.

- **[Page 84 / Initial]** *(Halicin card & molecular graph)*
  > "Up to this point, this might sound like an elegant academic theory.
  >
  > Let me show you what happens when this technology meets the real physical world.
  >
  > In 2020, researchers at MIT represented molecules as graphs. Atoms as nodes. Chemical bonds as edges."
- **[Page 85 / Click 1]** *(Bullet 1: Screened 100 million molecules)*
  > "They screened a digital library of over **100 million** molecules."
- **[Page 86 / Click 2]** *(Bullet 2: Learned chemical bond topologies)*
  > "The GNN learned chemical bond topology --- completely immune to atom numbering."
- **[Page 87 / Click 3]** *(Bullet 3: Flagged a molecule humans had overlooked)*
  > "It flagged a candidate molecule that human chemists had completely overlooked because it looked nothing like any known antibiotic."
- **[Page 88 / Click 4]** *(Green badge: Killed Pan-Resistant Bacteria)*
  > "They tested it in the lab. It wiped out *Acinetobacter baumannii* --- a deadly superbug resistant to every conventional antibiotic in medicine. They named it **Halicin**."
- **[Page 89 / Click 5]** *(Bottom takeaway)*
  *(Warm, inspiring tone)*
  > "A neural network read chemistry as a graph... and found a life-saving drug."

---

### Slide 27 [Pages 90–92] · Scene 14: Case Study 2 — Global Weather (The Entire Atmosphere)
**Visuals**: A clean spherical Earth outline. Radial airflow rays and latitude circles reveal a planetary mesh graph.

- **[Page 90 / Initial]** *(Case File 02: The Entire Atmosphere)*
  > "Now let's expand our scale from nanometer molecules to an entire planet."
- **[Page 91 / Click 1]** *(Mesh lines illuminate around the globe)*
  > "What if every coordinate on Earth is a node? Adjacent atmospheric airflows are edges."
- **[Page 92 / Click 2]** *(Subtitle)*
  > "The entire atmosphere of planet Earth becomes a single continuous spherical graph."

---

### Slide 28 [Pages 93–97] · Scene 14: Case Study 2 — GraphCast (Planetary Scale)
**Visuals**: Left: Planetary mesh. Right: DeepMind 2023 GraphCast dossier card with bullet reveals.

- **[Page 93 / Initial]** *(GraphCast card)*
  > "In 2023, Google DeepMind published **GraphCast**."
- **[Page 94 / Click 1]** *(Bullet 1: 10-day global forecast in under 1 minute)*
  > "It produces a 10-day global weather forecast in **under 1 minute** on a single machine."
- **[Page 95 / Click 2]** *(Bullet 2: Beat European supercomputers on >90% of variables)*
  > "It outperformed the European gold-standard supercomputers that take hours on massive server clusters on over 90% of test variables."
- **[Page 96 / Click 3]** *(Bullet 3: Predicted Hurricane Lee days earlier)*
  > "It accurately predicted the landfall trajectory of Hurricane Lee days ahead of official forecasters."
- **[Page 97 / Click 4]** *(Card badge: Same Principle. Planetary Scale.)*
  > "The exact same three steps you ran on Alice --- Gather, Aggregate, Update --- executed across the entire planet at once."

---

### Slide 29 [Pages 98–98] · Scene 15: Case Study 3 — CERN Particle Physics (The Question)
**Visuals**: A spray of particle sensor hit dots scattered in space. Full text revealed cleanly in one view.

- **[Page 98 / Full Slide]**
  *(Curious, dramatic tone)*
  > "And finally, let's journey to CERN's Large Hadron Collider.
  >
  > When two protons collide at 99.999% the speed of light, they spray thousands of detector sensor hits in every direction.
  >
  > The million-dollar question for physicists is:
  > **Which of these thousands of scattered hits belong to the same subatomic particle?**"

---

### Slide 30 [Pages 99–103] · Scene 15: Case Study 3 — CERN Particle Trajectory Tracking
**Visuals**: Left: CERN LHC · CMS / ATLAS card. Right: Candidate sensor dots connect into a solid golden particle trajectory line! Red badge: Discovering New Physics.

- **[Page 99 / Initial]** *(Connect Dots card)*
  > "It is the ultimate connect-the-dots challenge."
- **[Page 100 / Click 1]** *(Bullet 1: Builds a graph of candidate hits)*
  > "Physicists build a graph connecting candidate sensor hits."
- **[Page 101 / Click 2]** *(Bullet 2 & Trajectory line lights up in bold gold)*
  *(Point to the glowing gold curved trajectory)*
  > "A GNN evaluates edge probabilities and prunes away the false connections in **milliseconds**, tracking the true particle path in real time."
- **[Page 102 / Click 3]** *(Bullet 3: Reconstructs particle trajectories)*
  > "Filtering millions of collisions per second."
- **[Page 103 / Click 4]** *(Crimson badge: Discovering New Physics)*
  > "Graph Neural Networks are actively helping physicists discover new fundamental laws of nature."

---

### Slide 31 [Pages 104–107] · Scene 16: The Unifying Picture — Three Fields
**Visuals**: Three paper cards side-by-side: MOLECULES (Chemistry), PLANET (Atmosphere), PARTICLES (Physics).

- **[Page 104 / Initial]** *(Card 1: Molecules & Atoms)*
  > "Think about what we have just seen:
  > A molecule in biology."
- **[Page 105 / Click 1]** *(Card 2: Planet & Airflow)*
  > "A planet in meteorology."
- **[Page 106 / Click 2]** *(Card 3: Particles & Detectors)*
  > "A subatomic particle in quantum physics."
- **[Page 107 / Click 3]** *(Bottom takeaway)*
  > "To a traditional scientist, these three disciplines have absolutely nothing in common."

---

### Slide 32 [Pages 108–110] · Scene 16: The Unifying Picture — GRAPH
**Visuals**: The screen clears to a massive, commanding gold word centered on the white canvas: G R A P H.

- **[Page 108 / Initial]** *(Massive gold title: G R A P H)*
  *(Pause for two seconds. Let the single word anchor the entire talk.)*
  > "Except underneath... they share the exact same mathematical soul."
- **[Page 109 / Click 1]** *(Subtitle: Different problems. Same underlying structure.)*
  > "Different problems. Same underlying structure."
- **[Page 110 / Click 2]** *(Takeaway: Whenever relationships are part of the information...)*
  *(Speak with quiet authority)*
  > "Whenever the relationships are part of the information... ignoring those relationships is throwing information away."

---

### Slide 33 [Page 111] · Scene 17: Final Close — Thank You
**Visuals**: Large gold *Thank you.* with *QUESTIONS & DISCUSSION* underneath.

- *(Stand tall, look directly at the audience / evaluators)*
  > "And that is the core truth to take away today:
  >
  > A Graph Neural Network is simply the way we teach neural networks...
  > to look at the things... and the connections...
  > at the exact same time.
  >
  > Thank you."

---

## Speaker Delivery Cheatsheet: The 5 Golden Rules

1. **Never rush Slide 09 (The Red X)**: Hold silence after saying *"The network learned our filing system. It never learned the chemistry."* That is your intellectual climax in Act I.
2. **Anchor the Math to Physical Action (Slide 11 & 18)**: When explaining $\text{AGG}$ and $W$, use your hands: *Gather* (pulling inward), *Aggregate* (compressing together), *Update* (flipping your hand).
3. **Keep the Numbers Physical (Slides 13–15)**: Don't read equations as algebra. Say: *"Bob sent a 1.00 on Topic X. Alice had zero. They split the difference: now Alice is at 0.50."*
4. **Deliver the Over-Smoothing Punchline (Slide 23)**: Contrast the 100-layer CNN with GNNs. *"Why do GNNs stop at 2 or 3 layers? Because depth is reach, and if you talk to everyone, all originality washes away."*
5. **The Closing Frame (Slide 33)**: Deliver the final sentence slowly and deliberately with eye contact before clicking to *"Thank you."*
