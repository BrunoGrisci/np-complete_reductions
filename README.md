# np-complete_reductions

<p align="right">
  <strong>English</strong> |
  <a href="README.pt-BR.md">Português (Brasil)</a>
</p>

**np-complete_reductions** is an interactive, browser-based educational webtool for visualizing classical **polynomial-time reductions** used in proofs of **NP-completeness**.

The tool focuses on reductions from **SAT** and **3SAT** to standard graph and arithmetic problems. It shows how source formulas are transformed into target instances, how solutions correspond in both directions, and why the constructions are computable in polynomial time.

It is designed for classroom use in **Theory of Computation**, especially when teaching reductions after the Cook-Levin theorem and before or alongside the classical catalog of NP-complete problems.

🔗 **GitHub Pages target:** https://brunogrisci.github.io/npcompletereductions

🔗 **GitHub repository:** https://github.com/BrunoGrisci/np-complete_reductions

---

## ✨ Features

### Core functionality
- Interactive visualizations of classical polynomial-time reductions:
  - `SAT ≤P 3SAT`
  - `3SAT ≤P CLIQUE`
  - `3SAT ≤P INDEPENDENT-SET`
  - `3SAT ≤P SUBSET-SUM`
  - `3SAT ≤P VERTEX-COVER`
  - `3SAT ≤P HAMPATH`
- Overview tab explaining the general strategy of NP-completeness proofs:
  - membership in NP,
  - choosing a known NP-complete source problem,
  - building a polynomial-time reduction,
  - proving both correctness directions,
  - bounding the construction size and running time.
- Reduction map showing how the implemented reductions relate to SAT and 3SAT.
- Preset examples for every reduction, including satisfiable and unsatisfiable formulas.
- User-defined formula input with validation for CNF and 3CNF syntax.
- Brute-force satisfiability checking for small examples, used only as a classroom checker.

### Step-by-step construction mode
- Each reduction has a **Step-by-step construction** panel.
- A **Start** button clears the target instance.
- **Next** adds the next object or gadget in the construction.
- **Previous** returns to the preceding construction state.
- **Cancel** exits construction mode and restores the completed target instance.
- Each step includes a focused explanation of the object being created and why it is needed in the proof.

### Reduction visualizations
- **SAT ≤P 3SAT**
  - handles CNF clauses of size 1, 2, 3, and greater than 3,
  - shows auxiliary variables and generated 3-literal clauses,
  - emphasizes equisatisfiability rather than logical equivalence over only the original variables.
- **3SAT ≤P CLIQUE**
  - creates one vertex for each literal occurrence,
  - groups vertices by clause,
  - draws compatibility edges between noncontradictory literals in different clauses,
  - checks candidate cliques of size `k`.
- **3SAT ≤P INDEPENDENT-SET**
  - creates one vertex for each literal occurrence,
  - adds triangle edges inside each clause group,
  - adds contradiction edges between opposite literals in different clauses,
  - checks candidate independent sets of size `k`.
- **3SAT ≤P SUBSET-SUM**
  - builds the digit-table construction with variable columns and clause columns,
  - shows truth-setting rows `yi` and `zi`,
  - shows slack rows `gj` and `hj`,
  - highlights why the target has the form `11...133...3`,
  - explains why no carries occur.
- **3SAT ≤P VERTEX-COVER**
  - builds variable edges and clause triangles,
  - connects clause-literal vertices to matching variable-literal vertices,
  - checks covers of size at most `K`,
  - makes the truth convention explicit.
- **3SAT ≤P HAMPATH**
  - builds directed variable gadgets and clause vertices,
  - shows traversal directions corresponding to truth assignments,
  - adds detour edges for satisfying clauses,
  - lets the user inspect and manually select a path.

### Interactive checking
- Source formulas are checked for satisfiability when small enough.
- Target instances are marked as YES/NO instances according to the reduction.
- The tool can display one corresponding target solution when it exists:
  - satisfying assignment,
  - clique,
  - independent set,
  - subset summing to the target,
  - vertex cover,
  - Hamiltonian path.
- Users can manually select graph vertices, subset rows, or Hamiltonian-path nodes.
- Checkers report whether the manual selection satisfies the target constraints.
- Source and target solutions are shown side by side where appropriate.

### Graph interaction
- Graph-based reductions support draggable nodes:
  - CLIQUE,
  - INDEPENDENT-SET,
  - VERTEX-COVER,
  - HAMPATH.
- Edges remain attached as nodes are dragged.
- Invalid selected edges are highlighted in the relevant checkers.

### Usability and presentation
- Clean single-page interface with tabs.
- Minimalist visual design suitable for lecture projection.
- Clear/dark mode toggle.
- English / Brazilian Portuguese toggle.
- Persistent preferences via `localStorage`:
  - theme,
  - language.
- Fully client-side, with no backend and no external UI framework.

---

## 🧠 Pedagogical goals

This tool was built to help students:

- see reductions as explicit transformations of instances, not just as proof diagrams,
- connect each source formula clause or literal occurrence to an object in the target instance,
- understand the difference between a construction and a brute-force checker,
- inspect why YES instances map to YES instances,
- inspect why target YES instances imply source YES instances,
- understand the role of gadgets, auxiliary variables, slack digits, and graph edges,
- distinguish compatibility edges, conflict edges, and covering edges across different reductions,
- see why the constructed target instance has polynomial size.

It is suitable for:

- undergraduate Theory of Computation courses,
- classroom demonstrations with a projector,
- guided exercises on NP-completeness reductions,
- self-study of classical NP-complete problems,
- comparing multiple reductions from the same source problem.

---

## 📄 Input model

The tool accepts CNF-style formulas in several classroom-friendly formats, for example:

```text
(x1 v !x2 v x3) ^ (!x1 v x2 v x4)
(x1 ∨ ¬x2 ∨ x3) ∧ (¬x1 ∨ x2 ∨ x4)
x1,!x2,x3; !x1,x2,x4
```

For `SAT ≤P 3SAT`, clauses may have arbitrary positive size.

For the reductions from `3SAT`, every clause must have exactly three literal occurrences. Repeated literal occurrences are allowed, as in standard textbook examples such as:

```text
(x1 v x2 v x2) ^ (x1 v !x2 v !x2)
```

For small formulas, the built-in brute-force checker finds a satisfying assignment when one exists. This checker is included for explanation and validation only; it is not part of the polynomial-time reductions.

---

## 🌐 Internationalization (i18n)

- Full support for **English** and **Brazilian Portuguese**.
- Tab names, controls, validation messages, status boxes, construction explanations, proofs, and dynamic labels are bilingual.
- Switching language does **not** reset the current formula, preset, selected tab, construction state, or manual selections.

---

## 🛠️ Tech stack

- Vanilla **HTML / CSS / JavaScript**
- No build step
- No external dependencies
- Fully client-side
- Compatible with static hosting such as **GitHub Pages**

Main files:

- `npcompletereductions.html`
- `assetsNPCompleteReductions/styles.css`
- `assetsNPCompleteReductions/script.js`

To run locally, open `npcompletereductions.html` directly in a browser, or serve the folder with any static file server, for example:

```bash
python3 -m http.server 4173
```

Then open:

```text
http://127.0.0.1:4173/npcompletereductions.html
```

---

## 🧪 Verification

The project is static and does not require a test framework. During development, the implementation was checked with:

```bash
node --check assetsNPCompleteReductions/script.js
```

Browser validation was also used to confirm:

- parser behavior for CNF and 3CNF inputs,
- satisfiable and unsatisfiable presets for each reduction,
- YES/NO preservation in the constructed target instances,
- Start / Next / Previous / Cancel behavior in construction mode,
- display of satisfying assignments and target solutions,
- manual clique and independent-set checking,
- manual subset-sum row selection and target digit checking,
- manual vertex-cover checking and uncovered-edge highlighting,
- manual Hamiltonian-path checking,
- draggable graph nodes with attached edges,
- clear/dark theme switching,
- English/Brazilian Portuguese switching,
- readability on desktop and mobile viewports.

---

## 🚀 Future work (ideas)

- Add a guided lecture mode that automatically advances through each construction.
- Add optional expanded proof annotations beside each constructed object.
- Add export of generated target instances in a machine-readable format.
- Add more textbook and exam-style presets for every reduction.
- Add side-by-side complement view for CLIQUE and INDEPENDENT-SET.
- Add screenshots and short animated examples for the README.

---

## 🎓 Credits

**Developed by**  
**Prof. Bruno Iochins Grisci**  
Departamento de Informática Teórica  
Instituto de Informática – Universidade Federal do Rio Grande do Sul (UFRGS)  
🔗 https://brunogrisci.github.io/  
🔗 https://www.inf.ufrgs.br/site/  
🔗 https://www.ufrgs.br/site/

**Main theoretical reference**
- Michael Sipser, *Introduction to the Theory of Computation*, especially the chapters on NP-completeness and the reductions from SAT/3SAT to classical NP-complete problems.

**Historical context**
- Richard M. Karp, “Reducibility Among Combinatorial Problems,” 1972.
- Karp's work introduced the polynomial-time reduction method as a central tool for showing NP-completeness of many now-classical combinatorial problems.
- The tool uses standard textbook versions of these reductions and prioritizes pedagogical clarity over compact encodings.

**Development note**  
This webtool was created with the assistance of **Codex GPT-5.5**.

---

## 📦 License

This project is licensed under the **MIT License**.

You are free to use, modify, and redistribute it for academic and educational purposes, provided proper attribution is given.

See the `LICENSE` file for details.

---

If you use this tool in teaching or research, a citation or link back to the repository is appreciated.

## 📚 Citation

If you use this tool in academic work (papers, theses, technical reports, or teaching material), please cite it as:

```bibtex
@software{Grisci_NP_complete_reductions,
  author       = {Bruno Iochins Grisci},
  title        = {{np-complete\_reductions}: An Interactive Visualizer for Classical Polynomial-Time Reductions},
  year         = {2026},
  url          = {https://github.com/BrunoGrisci/np-complete_reductions},
  note         = {Educational web-based software},
}
```

---

## 🔄 See also

- **SAT-tableau**  
  Webtool: https://brunogrisci.github.io/sat_tableau  
  Repository: https://github.com/BrunoGrisci/SAT-tableau

- **TM → PCP Domino Generator (tm2pcp)**  
  Webtool: https://brunogrisci.github.io/tm2pcp  
  Repository: https://github.com/BrunoGrisci/tm2pcp-webtool

- **PCP → CFG Ambiguity webtool**  
  Web app: https://brunogrisci.github.io/pcp2cfg  
  Repository: https://github.com/BrunoGrisci/pcp2cfg-webtool

- **Executable computability reductions**  
  Repository: https://github.com/BrunoGrisci/reductions-computability
