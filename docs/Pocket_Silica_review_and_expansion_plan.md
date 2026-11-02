# Review of Pocket Silica

This review covers the complete text of `gooding.docx`. The companion file, `Pocket_Silica_revised_text.md`, contains simpler replacement wording and a proposed expansion of the methodology. The original Word document is unchanged. Its page layout could not be verified because the available document renderer requires LibreOffice, which is unavailable in this environment.

The revision uses **water and electricity**, as you confirmed. New methods are proposals for your actual study, not a record of tests already completed. Check them with your adviser and match them to the system you will build before submitting the paper.

## Overall assessment

The paper has a workable computer science focus: develop Pocket Silica and compare a quadtree with a uniform grid under the same simulation rules. Its main weakness is that it explains the motivation and Agile development process more clearly than the experiment itself.

Nineteen pages alone does not establish that the paper is incomplete. Compare your draft with your department's required sections and assessment criteria. Your classmates may have different topics, formatting, diagrams, or research methods. If your department sets a minimum length, follow that requirement. Otherwise, add information that makes your work reproducible rather than stretching paragraphs or inserting larger screenshots.

## Issues to correct throughout the paper

| Issue in the original | Why it matters | Correction in the companion text |
| --- | --- | --- |
| Some sections cover water only; others cover water and electricity. | The objectives, scope, model, and tests describe different systems. | Use both resources consistently and measure each separately. |
| Research Design describes Agile only. | Agile explains how software is developed, but does not fully explain how research evidence is collected. | Describe development and controlled computational experiments, then explain Agile as the development process. |
| Respondents are professionals or advisers, but later sections call them Computer Science students. | The participant description and instruments do not agree. | Use qualified technical evaluators consistently. Confirm the actual number and selection criteria. |
| Some wording assumes a quadtree will be faster. | The comparison should be able to show an advantage, no difference, or a disadvantage. | Treat performance as an open research question. |
| The gap says electricity has barely been studied and that the combination has never been done. | The limited review does not establish a field-wide absence of research. | Limit the gap to the studies reviewed and the specific comparison proposed. |
| Resource depletion is presented as evidence of accuracy. | A falling resource meter can match a programmed rule even when the real-world model is unrealistic. | Separate software correctness from real-world validity. |
| The significance section suggests demonstrated learning and policy value. | The scope excludes learning, player experience, and environmental prediction tests. | Describe these as possible future uses, not demonstrated benefits. |
| The ethics section says no special privacy procedures are needed. | Evaluators still provide feedback that should be handled responsibly. | Explain consent, participant codes, access, retention, and reporting without names. |
| Broad technical claims cite Lee et al. and Ru et al., but their references are missing. | Readers cannot trace the evidence. | Remove the unsupported claim unless the complete, relevant sources can be supplied. |

## Corrections to wording

The replacement text keeps necessary terms such as quadtree, spatial partitioning, and simulation, but explains them in ordinary language.

| Original wording | Clearer wording |
| --- | --- |
| Review of Related Literatures | Review of Related Literature |
| Research Methodologies | Research Methodology |
| The Figure 1 shows | Figure 1 shows |
| real spacing and resource problems | problems involving location and limited resources |
| studies reviewqed | studies reviewed |
| This one show | This study shows |
| frames per seconds | frames per second |
| professionals and or academic advisers | professionals or academic advisers |
| two things growing against each other | infrastructure growth and increasing resource demand |
| this study sits between those realities | this study connects spatial simulation with an interactive mobile prototype |
| treating every space with equal computational weight | using the same level of detail across the entire map |

Use future tense for proposed procedures. Use past tense only for work that has actually been completed. Use “correctness” when checking the program against specified rules. Reserve “real-world accuracy” for comparisons with suitable real-world evidence.

## Recommended structure

Keep your school's required chapter arrangement. The following preserves your apparent two-chapter organization rather than assuming that every school requires three chapters.

### Chapter 1 Introduction and related literature

1. Introduction and background
2. Statement of the problem or research questions
3. General and specific objectives
4. Review of related literature, grouped by theme
5. Synthesis and research gap
6. Conceptual framework
7. Paradigm of the study, if required separately
8. Scope and delimitations
9. Significance of the study
10. Definition of terms

Your original places Objectives after the literature review. That can remain if it follows your school template. The more important changes are adding clear research questions and making sure the gap leads directly to the objectives.

### Chapter 2 Research methodology

1. Research design
2. Agile development process
3. Research environment and technical setup
4. System requirements and architecture
5. Simulation model and assumptions
6. Quadtree design
7. Uniform grid baseline
8. Test scenarios and experimental procedure
9. Verification and acceptance criteria
10. Technical evaluators and selection
11. Research instruments
12. Data gathering procedure
13. Data analysis
14. Ethical considerations
15. Methodological limitations

Place the consolidated References after Chapter 2, unless the school requires references after each chapter. Move long checklists, detailed test records, and supplementary screen designs to appendices if your template permits them.

## What to add below Research Design

These are the most valuable additions. The page estimates are planning estimates under normal thesis formatting, not guaranteed page counts. Some material replaces existing paragraphs, so do not add these estimates directly to the current nineteen pages.

| Addition | What to explain | Approximate space |
| --- | --- | --- |
| Research design and research questions | What is being developed, what is compared, and what evidence answers each objective | 0.5–1 page |
| System architecture | How the interface, simulation, spatial index, and logging tool work together | 0.5–1 page |
| Simulation rules | Infrastructure growth, water supply, electricity supply, allocation, shortages, and time steps | 1–2 pages |
| Quadtree design | Stored data, subdivision, depth limit, boundary handling, insertion, and queries | 1–1.5 pages |
| Grid baseline | Fixed cell size, equivalent operations, shared rules, and configuration selection | 0.5–1 page |
| Experiment plan | Entity counts, layouts, random seeds, run duration, repetitions, and device controls | 1–1.5 pages |
| Verification plan | Small examples with known answers, edge cases, and pass criteria | 0.5–1 page |
| Instruments and analysis | Actual logging fields, units, calculations, and evaluator checklist | 0.5–1 page |

Together, these topics could support roughly five to ten additional pages of useful explanation. The final total depends on the department's format and the level of detail you can support. Do not claim a particular page count until the Word document has been laid out and checked.

### The most important technical question

**What spatial operation makes the quadtree useful in this simulation?**

If every building simply subtracts demand from one global water total and one global electricity total, a running total may be enough. Dividing the map would not, by itself, make that calculation faster or more meaningful.

The proposed expansion therefore uses resource service areas: a supply source serves entities within a defined area, and the spatial structure finds those entities. Both the quadtree and the grid must answer the same queries and use the same allocation rules. This is a proposed design choice; check that it matches the game you intend to implement. If it does not, identify the actual spatial operation before adopting the text.

### Proposed test matrix

These are starting suggestions for a pilot test, not facts about your existing system or mandatory sample sizes.

| Setting | Proposed starting point | How to finalize it |
| --- | --- | --- |
| Algorithms | Quadtree and uniform grid | Implement both with the same simulation rules. |
| Layouts | Evenly spread, one cluster, several clusters | Define how positions are generated and save the input files. |
| Entity counts | 100, 500, 1,000, and 2,000 | Adjust after a pilot so the range is meaningful on the test device. |
| Independent layouts | Five saved seeds per layout and entity count | Generate identical inputs for both methods. |
| Repeated runs | Three runs per saved input and method | Increase only if the pilot shows unstable measurements. |
| Warm-up | Ten seconds, excluded from measurements | Check that startup work has settled. |
| Measured run | Sixty seconds | Keep duration identical within each comparison. |
| Simulation step | Fixed and identical for both methods | Select and report a value suitable for the model. |

This full starting matrix contains 360 measured runs: 2 methods × 3 layouts × 4 entity counts × 5 seeds × 3 repetitions. At sixty seconds each, that is six hours of measured time before warm-up and resets. Reduce or automate the matrix if that is unrealistic. Do not present it as an adopted protocol until you can carry it out.

The three repetitions on one input measure run-to-run variation. They are not three new independent maps. Average or summarize those repetitions for each saved input before making comparisons across layouts.

### Proposed verification examples

| Case | Setup | Expected check |
| --- | --- | --- |
| Empty map | No consumers | No consumption is recorded; no crash occurs. |
| Simple demand | Two buildings request 3 water units and 2 electricity units each | Total requested demand is 6 water units and 4 electricity units per step. |
| Water shortage | Water availability is below demand; electricity is sufficient | The recorded shortage follows the water allocation rule. |
| Electricity shortage | Electricity availability is below demand; water is sufficient | The recorded shortage follows the electricity allocation rule. |
| Both resources short | Both supplies are below demand | Both shortages are recorded without negative supplies. |
| Boundary | A building lies exactly on a cell boundary | The entity is stored and counted once. |
| Overlapping service areas | An entity can be reached by two sources | Allocation does not satisfy the same demand twice. |
| Dense cluster | Many entities occupy one small region | Subdivision stops at the depth or size limit without losing entities. |

These are software checks. They do not show that the simulation predicts actual environmental effects in Tarlac.

## Source and reference corrections

The web checks below were performed on 29 October 2026. A failed page fetch is a reason to investigate, not proof that a source does not exist.

1. **Pax Silica classification and water claims.** The Philippine Information Agency's 10 August 2026 report describes BCDA's position that the project is for semiconductor and advanced manufacturing facilities, with separate water and power arrangements. The original's treatment of the project as a data-center development and its single water-demand figure are therefore too definite. The replacement text attributes the official position and describes Pocket Silica as a simplified fictional scenario. [Official report](https://pia.gov.ph/news/bcda-clarifies-misconceptions-on-pax-silica-project-in-new-clark-city/PAGE)

2. **Game Developer article.** The linked page is by Videep Mishraa and is dated 27 October 2020, rather than December 2023. Its example concerns mesh-density partitioning. It should not be cited as experimental proof that your simulation will run faster. [Article](https://www.gamedeveloper.com/programming/quadtree-in-unity)

3. **Pinwheel tutorial.** The page identifies Tâm Trần Ngọc, an original publication date of 3 June 2024, and an update on 25 September 2025. It discusses culling largely stationary objects. The replacement text distinguishes that use from adaptive resource simulation. Check the author's preferred bibliographic name form against your required citation style. [Tutorial](https://www.pinwheelstud.io/post/how-to-do-cell-based-culling-using-quadtree-in-unity-c-part-1)

4. **McGiven et al.** The journal gives pages **2961–2974**, not 2961–2980. [Journal record](https://hess.copernicus.org/articles/29/2961/2025/)

5. **Wamucii et al.** The journal gives pages **3495–3518**, not 3495–3512. Its reference list entry should include the eight authors rather than using “et al.” as a substitute for the full author list. [Journal record](https://hess.copernicus.org/articles/28/3495/2024/)

6. **Maxim and Arnedo-Moreno.** Preserve the hyphen in Arnedo-Moreno. The replacement summarizes the review as design guidance rather than treating it as proof of the prototype's realism. [Journal article](https://games.jmir.org/2025/1/e54075)

7. **Finkel and Bentley.** The original cites them but omits the reference entry. Add the 1974 article. Also avoid suggesting that every quadtree uses the same equal-cell, capacity-based subdivision rule; explain the particular variant you will build. [Author institution record](https://scholars.uky.edu/es/publications/quad-trees-a-data-structure-for-retrieval-on-composite-keys/)

8. **Other citations.** Lee et al. (2021), Ru et al. (2022), and Manila Bulletin (2026) lack complete matching entries. The supplied PNA URL returned a 404 during this review. Remove unsupported statements or supply traceable, relevant sources. The replacement reference list includes only sources used by the replacement text; the other original references are not automatically false, but still require checking if restored.

## Figures and formatting

The source contains three embedded raster images and additional drawing objects. Text extraction does not fully establish whether every drawing is correct or visible in Word. Review all six numbered figures in the actual document.

- Put headings in their own paragraphs. In the original, Review of Related Literature, Scope and Delimitation, Significance, and Definition of Terms run together with following text.
- Apply Word heading styles so that the outline and any table of contents work properly. The extracted headings are currently mostly Normal paragraphs with direct bold formatting.
- Label the interface images as proposed screens or mockups if they are not screenshots of a completed system. Explain what each screen contributes to the simulation.
- Show both water and electricity in the conceptual and IPO diagrams. If NPCs remain in the IPO diagram, explain their actual role and resource demand; otherwise remove them.
- In the conceptual framework, show the spatial method as the main factor being compared. Entity count and layout are workload factors. Hold each workload constant within a paired comparison. Use performance measures and correctness checks as separate outputs.
- Explain the system architecture and quadtree with diagrams that readers need to understand the method. Avoid enlarging loading and settings screens just to gain pages.
- Use the department's prescribed font, margins, line spacing, chapter titles, numbering, and reference style. Do not change these simply to match another student's length.

## Details you still need to supply

Before the proposal is ready for submission, record the engine and language with versions; mobile operating system; actual test-device specifications; map dimensions; time-step duration; building types and demand values; service-area rules; quadtree capacity and depth limit; grid cell size; saved seeds; final run counts and durations; correctness tolerance; evaluator number and criteria; actual checklist; and feedback retention period.

The companion text avoids inventing these facts. Where it says a setting will be documented, replace that general statement with the real setting once you have selected it. If your school requires those details in the proposal, add them before submission rather than leaving them until the results chapter.
