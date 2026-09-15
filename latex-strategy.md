# LaTeX / TikZ-Beamer Visual Strategy
## "Case File: Graph Neural Networks" — Static Translation

---

## 1. The Core Challenge

The HTML deck uses JavaScript animations, fragment reveals, CSS transitions, film-grain effects, and SVG canvas elements. In LaTeX we have **zero animation**, so every visual must work as a **complete, self-contained static composition**. The strategy is to *freeze the most revealing moment* of each scene — the frame that carries the most narrative weight — and build that as a TikZ drawing.

---

## 2. Design Token Mapping

| HTML Variable | LaTeX Color Definition | Usage |
|---|---|---|
| `--board` `#241C17` | `boardbg` | Slide background |
| `--board2` `#31251B` | `boardmid` | Secondary BG, panels |
| `--paper` `#E8DCC4` | `papercream` | Card fill |
| `--paper2` `#C6B08A` | `paperdark` | Card gradient bottom |
| `--string` `#C1272D` | `crimson` | Edges, red X, strike |
| `--brass` `#C9A66B` | `brass` | Kicker text, borders |
| `--gold` `#F0C46A` | `gold` | Active nodes, callouts |
| `--chalk` `#F2EBDD` | `chalk` | Body text |
| `--dim` `#93826C` | `dimtext` | Metadata, labels |
| `--ink` `#14100E` | `ink` | Deep shadow |

### Fonts
- **Big Shoulders Display** → Use `\fontfamily{phv}\bfseries` (Helvetica Bold condensed) with manual letter-spacing via `\textls` (microtype) or hand-kern with `\kern`.  
  *Alternative*: Use `fontspec` with the actual Google Font if compiling with XeLaTeX/LuaLaTeX (recommended).
- **Courier Prime** → `\ttfamily` or `\fontfamily{pcr}` (Courier).
- **Spline Sans** → `\sffamily` body text.

### Compilation Target
> **Use XeLaTeX + fontspec** to load the exact Google Fonts (Big Shoulders Display, Spline Sans, Courier Prime) for pixel-perfect font matching.

---

## 3. Slide Layout Architecture

### Beamer Theme
- `\usetheme{default}` with all navigation stripped.
- Full-bleed `boardbg` background on every frame using `\setbeamercolor{background canvas}`.
- No header/footer/navigation symbols.
- Aspect ratio: `16:9` (`\documentclass[aspectratio=169]{beamer}`).

### Compositional Grid
Every slide uses one of three layout templates:

| Template | Usage | TikZ approach |
|---|---|---|
| **Centered Hero** | Single concept, typographic moment | `node` anchored at `(0,0)` with relative children |
| **Left + Right Panel** | Side-by-side comparisons | `\begin{columns}` or two `scope` regions split at `x=0` |
| **Canvas** | Full-slide graph/diagram | One large `tikzpicture` filling the entire frame |

### TikZ Coordinate System
Set the tikzpicture to span the full 16×9 frame:
```latex
\begin{tikzpicture}[remember picture, overlay]
  % Full frame: (-8,-4.5) to (8,4.5) in cm when origin=center
```

---

## 4. Scene-by-Scene Visual Translation

### Scene 1 · Cold Open: Trust the Person or Trust the Network?
**HTML moment**: Corkboard dark background. Central parchment card pinned with strings radiating to three badges (VERIFIED BANK in gold, two SCAM ACCOUNTS in crimson).  
**LaTeX approach**:
- Background `boardbg` fill.
- Central `papercream` rectangle with rounded corners as the profile card.
- Three outer `papercream`/`crimson` badge rectangles with `boardmid` fill.
- TikZ `\draw[crimson, line width=1.2pt]` straight lines (strings) from card center to each badge.
- Red pin: small filled circle `crimson` at top-center of card.
- Typography: Kicker in `brass` typewriter font, card name in display font.

### Scene 2 · The CNN Example
**HTML moment**: Image decomposed into a 3×3 patch grid, hierarchy label strip (Pixels → Edges → Patterns → Shapes → Object).  
**LaTeX approach**:
- Left half: a 5×5 grid of small squares (TikZ `\foreach` loop) with one 3×3 sub-block highlighted in `gold` fill.
- Right half: a vertical arrow chain with five node labels: `Pixels → Edges → Patterns → Shapes → Object`, each in a small rounded box.
- Use `\draw[->, gold, line width=1.5pt]` arrows connecting the boxes.

### Scene 3 · Name the CNN
**HTML moment**: Typographic stamp — large display text centered.  
**LaTeX approach**:
- Pure typographic slide. Large centered `\textbf{Convolutional Neural Network}` in display font at huge size.
- Below: `(CNN)` in `brass`.
- Below: subtitle in `chalk` Spline Sans.
- Subtle horizontal `brass` rule above/below the name.

### Scene 4 · Break the Assumption: Grid vs. Graph
**HTML moment**: Two-panel side-by-side. Left: 5×5 pixel grid with cell #37 highlighted. Right: irregular graph with 6 nodes.  
**LaTeX approach**:
- Left panel (scope): `\foreach` 5×5 grid; cell at row 3, col 2 filled `gold` with "37" label.
- Right panel (scope): 6 nodes placed at hand-picked `(x,y)` coordinates with `\draw[crimson]` edges. No labels on nodes.
- Vertical `brass` rule dividing the two panels.
- Caption labels below each panel.

### Scene 5 · Obvious Solutions 1 & 2
**HTML moment**: Left: 4 isolated dots. Right: 4×4 adjacency matrix table.  
**LaTeX approach**:
- Left half: four large `fill=dimtext` circles with `\node[circle, fill=dimtext]`.
- Right half: a `tabular` or TikZ matrix of zeros and ones, styled like the HTML's `table.mx`, inside a `papercream` card background rectangle.
- `brass` heading "SOLUTION 2" above the matrix card.

### Scene 6 · The Failure: Permutation Sensitivity
**HTML moment**: Two caffeine molecules side by side with different numberings → two matrices → two predictions → Red X.  
**LaTeX approach**:
- Two "molecule graphs" (6-node hexagonal caffeine approximation) drawn with TikZ nodes and edges, numbered differently (1-6 vs shuffled).
- Below each molecule: small `papercream` card showing matrix excerpt and prediction score (`0.83` vs `0.11`).
- Large red `\times` symbol (or TikZ drawn X) stamped over the right molecule/matrix pair.
- `crimson` punchline text below.

### Scene 7 · The Pivotal Question
**HTML moment**: One glowing node, large text "What is this node?" with "is" struck through and replaced by gold "Who influences this node?"  
**LaTeX approach**:
- Single large `gold`-outlined circle node centered.
- Above: `chalk` body text "What is this node?" with `\sout{is}` from `ulem` package.
- Below (or replacing): gold-colored `\textbf{Who influences this node?}`.
- Subtle `gold` glow effect: concentric circles with decreasing opacity using `fill opacity`.

### Scene 8 · GNN Idea: Gather · Aggregate · Update
**HTML moment**: Central node with 3 neighbours; envelope glyphs on edges; three-step label strip.  
**LaTeX approach**:
- Central node in `gold` fill. Three neighbour nodes in `brass` fill at 120° positions.
- `\draw[crimson, ->, line width=1.5pt]` arrows pointing inward from each neighbour.
- Small envelope glyphs: TikZ `\draw` rectangle with flap triangle on each arrow midpoint.
- Three horizontal label boxes below the graph: `[GATHER]`, `[AGGREGATE]`, `[UPDATE]` in `chip`-style rectangular outlines.

### Scene 9 · Alice's Graph Demo (Step 4: Final State)
**HTML moment**: Named 5-node graph with Alice updated to "LIKELY: 89%", all nodes having updated cards.  
**LaTeX approach**:
- Five named nodes placed manually:
  - Alice: center, `gold`-filled card.
  - Bob (top-left), Carol (top-right): `brass`-outlined.
  - David (far left), Eve (far right): `dimtext`-outlined.
- Each node is a `papercream` rectangle with name and status field.
- `\draw[crimson, line width=1.2pt]` edges.
- Alice's card highlighted with `gold` border and "LIKELY: 89%" status label.
- Small "message arrows" frozen mid-travel from Bob and Carol toward Alice.

### Scene 10 · The Intuitive Equation
**HTML moment**: Large equation centered, with curved callout lines connecting terms to plain-English labels.  
**LaTeX approach**:
- Use `amsmath` for the equation. Display it in a centered `equation*` environment with `\sigma\Bigl(W \cdot \text{AGG}\bigl(\{h_u^{(k)}\}_{ u\in\mathcal{N}(v)}\bigr)\Bigr)`.
- TikZ overlay: place named `coordinate` marks inside the equation using `\tikzmark`, then draw curved `\draw[->, brass, bend right=30]` arrows from each term to its label (typewriter text in `dimtext`).

### Scene 11 · Depth = Reach & Over-Smoothing
**HTML moment**: Fixed graph with all nodes faded to uniform gray (Layer 6 over-smoothing state).  
**LaTeX approach**:
- Graph of ~8 nodes, all filled with a flat mid-gray (`\definecolor{smgray}{HTML}{4A4642}`).
- All edges drawn in `dimtext` at low opacity `draw opacity=0.35`.
- All nodes identical in color, size, and no labels.
- "LAYER 6" counter label top-right in `gold` typewriter font.
- "OVER-SMOOTHING" stamp text in `crimson` large display font below.

### Scene 12 · Attention: Not All Informants Are Equal
**HTML moment**: Central node with one thick gold edge (high attention) and one thin dim edge (low attention). Three chip labels.  
**LaTeX approach**:
- Central `gold` node.
- Left neighbour: `\draw[gold, line width=4pt]` thick edge with `gold` fill node (expert/trusted).
- Right neighbour: `\draw[dimtext, line width=0.8pt, draw opacity=0.4]` thin dim edge.
- Three bottom chips: TikZ `\node[draw=gold!40, rounded corners=2pt, text=gold]` boxes: GCN / GraphSAGE / GAT.

### Scene 13 · Case Study 1: Halicin
**HTML moment**: Dark bacterium micrograph background. Case card with MIT 2020 data and halicin molecule.  
**LaTeX approach**:
- Background: `boardbg` with a subtle TikZ noise-like texture using a random dots pattern (or just the dark bg with vignette).
- Large `papercream` card (left or center) with:
  - `brass` kicker: "CASE STUDY 01 · DRUG DISCOVERY"
  - Display headline: "Halicin"
  - Body facts: MIT 2020, 100M compounds, pan-resistant bacteria.
- Right: TikZ hexagonal ring structure approximating caffeine/halicin (6 C atoms, connecting single/double bond lines).

### Scene 14 · Case Study 2: GraphCast
**HTML moment**: Earth globe with icosahedral mesh overlay. Key facts card.  
**LaTeX approach**:
- Large circle (Earth) with `fill=boardmid` and crosshatch/mesh overlay using TikZ `\foreach` to draw icosahedral edges radiating from center.
- `papercream` card (right side) with DeepMind GraphCast facts.
- `brass` mesh edge lines inside the circle at various angles.

### Scene 15 · Case Study 3: CERN LHC
**HTML moment**: Dense particle hit cloud → candidate graph → pruned tracks.  
**LaTeX approach**:
- Background: `boardbg`.
- Left region: many small dots (random-ish scatter) using `\foreach` with fixed coordinates.
- Right region: a reduced set of dots connected by `crimson` edge lines (the "pruned" graph).
- TikZ `\draw[->, brass, line width=1pt]` arrow between the two regions labeled "GNN PRUNES".

### Scene 16 · The Unifying Picture
**HTML moment**: Three side-by-side cards (molecule, planet, collider) fading, leaving the word "GRAPH".  
**LaTeX approach**:
- Three `papercream` cards side by side, each with a label: `[MOLECULE]`, `[ATMOSPHERE]`, `[COLLIDER]`.
- A large `gold` arrow or transition annotation pointing downward to the word **GRAPH** in `gold` huge display font below.
- `chalk` subtitle: "Different problems. Same structure."

### Scene 17 · Final Close
**HTML moment**: Return to Scene 1's Dhaka node and network.  
**LaTeX approach**:
- Re-use the Scene 1 corkboard layout but with a key visual difference: the strings now pulse with a `gold` glow (simulate with `gold` line color).
- Closing quote in `chalk` italic serif, centered below the corkboard network.
- Footer: small `brass` typewriter text: "A Graph Neural Network is simply how we teach neural networks to look at the things and the connections at the same time."

---

## 5. Reusable TikZ Macros

Define these once in the preamble:

```latex
% Rounded paper card
\newcommand{\papercard}[3]{% (x,y), width, height
  \fill[papercream, rounded corners=3pt] (#1) rectangle +(#2, #3);
}

% Graph node
\newcommand{\gnode}[3]{% (x,y), label, color
  \node[circle, draw=#3, fill=#3!20, line width=1.5pt,
        minimum size=22pt, font=\tiny\ttfamily] at (#1) {#2};
}

% Chip label
\newcommand{\chip}[2]{% (x,y), text
  \node[draw=gold!50, text=gold, font=\bfseries\small,
        inner sep=5pt, rounded corners=2pt] at (#1) {#2};
}

% Red pin
\newcommand{\redpin}[1]{% (x,y)
  \fill[crimson] (#1) circle (4pt);
}

% Vignette overlay
\newcommand{\vignette}{
  \fill[black, opacity=0.5, path fading=radial out fading]
    (-8,-4.5) rectangle (8,4.5);
}
```

---

## 6. Section Divider Strategy

Use a **kicker line** at the top-left of each slide: `SCENE XX / 17` in `brass` typewriter font. This mirrors the HTML's `#footR` progress indicator.

---

## 7. Compile Pipeline

```bash
xelatex gnn-deck.tex
xelatex gnn-deck.tex   # second pass for TikZ overlays
```

Required packages:
- `beamer`, `tikz`, `pgf`
- `fontspec` (XeLaTeX)
- `xcolor`, `amsmath`, `amssymb`
- `ulem` (strikethrough)
- `microtype`
- TikZ libraries: `arrows.meta`, `calc`, `positioning`, `shapes.geometric`, `fadings`

---

## 8. What We Gain vs. Lose in Translation

| HTML Feature | LaTeX Equivalent | Notes |
|---|---|---|
| JS fragment reveals | Static: show the final/peak state | One slide = one frozen moment |
| CSS animations | None | Composition must imply motion |
| Film grain texture | None (too heavy) | Omit; dark bg alone is sufficient |
| Google Fonts | fontspec loading | Requires fonts installed on system |
| Responsive scaling | Fixed 16:9 beamer | Identical to HTML's 1600×900px |
| Presenter notes | `\note{}` in beamer | Works with `pdfpc` or beamer notes mode |
| Progress bar | Manual `brass` rule + scene counter | Simple and clean |
