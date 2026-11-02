# Pocket Silica complete change list

Reviewed on 30 October 2026 against the latest saved `gooding.docx`, including its embedded conceptual framework and updated IPO diagram. This checklist consolidates the remaining changes. The Word file has not been edited. Full Word pagination and page layout have not been rendered; the formatting observations below concern document structure and the embedded images.

Your confirmed focus is water and electricity. NPCs protest when resource supply is low; you specifically confirmed that reaching a specified electricity level triggers a reaction. Exact thresholds and recovery conditions have not yet been supplied. The quadtree's specific game operation is also still undecided.

## Keep the changes that are already correct

Keep the revised introduction paragraphs 3 and 6, general objective, specific objectives 1–3, research gap, synthesis, water-and-electricity scope wording, and government/player significance paragraphs. Keep the NPC protest sentence now added to Scope and the reference to protests in the Design phase. References are now after the methodology; keep that placement unless your school requires a different arrangement.

The updated IPO diagram correctly includes NPC population, water and electricity settings, protest thresholds, and visible protest behavior. Keep those additions. Restore the missing technical inputs described in item 10 below.

## First resolve what the quadtree actually does

### 1. Correct the understanding of subdivision

A quadtree is a way to organize positions in a map or other two-dimensional space. In the capacity-based version described in your paper, a cell divides into four when its object count exceeds a selected capacity, subject to a stopping limit. The division is a data structure operation; it need not appear as four panels on the player's screen. Low FPS is a performance measurement, not this version's subdivision condition.

For illustration only, if a leaf has a capacity of four objects, adding a fifth object can trigger subdivision. Four is an example, not a selected thesis setting. Other quadtree variants use other subdivision rules. Do not copy the fixed-depth Pinwheel culling method as if it used the same capacity-based rule. [Capacity-based example](https://www.gamedeveloper.com/programming/quadtree-in-unity), [fixed-depth culling example](https://www.pinwheelstud.io/post/how-to-do-cell-based-culling-using-quadtree-in-unity-c-part-1)

### 2. Choose and describe the real spatial operation

The paper must identify an operation that uses object positions. Possible uses include finding nearby objects or selecting objects visible to a camera. These are examples to consider, not features confirmed for Pocket Silica. Select an operation you will actually implement and explain how both the quadtree and grid perform it.

If the game only subtracts demand from global resource totals and triggers all NPCs from one global threshold, those calculations alone do not explain why the game needs a quadtree. Do not invent local resource networks or NPC movement rules just to justify the algorithm. A quadtree can support a spatial operation while the resource calculations remain a separate part of the game.

The final description in the introduction, Objective 1, frameworks, Scope, and methodology must all agree with the operation selected. Performance improvement remains something to test; subdivision alone does not establish higher FPS.

## Chapter 1 changes

### 3. Introduction paragraph 2 — distinguish proposed plans from established effects

Keep this paragraph's purpose as the local background. Remove the definite irrigation-effect conclusion. Retain the 130-million-liter estimate, partnership description, and project-component list only if their exact sources and attribution can be verified.

A shorter replacement for the paragraph is:

> This global trend provides a background for discussing the proposed Pax Silica development in New Clark City, Capas, Tarlac. According to the Philippine Information Agency, the Bases Conversion and Development Authority describes the development as a location for semiconductor and advanced manufacturing facilities and states that separate water and electricity supply arrangements are planned (Reparejo, 2026). These statements describe proposed arrangements rather than measured results from an operating project.

If retaining public concerns, name and cite the source raising them. Do not present a concern as an observed impact. [Official report](https://pia.gov.ph/news/bcda-clarifies-misconceptions-on-pax-silica-project-in-new-clark-city/)

### 4. Introduction paragraph 4 — explain the selected variant and remove unsupported comparison

Replace the sentence beginning “The quadtree, a hierarchical spatial data structure first introduced…” with:

> An early form of the quadtree was described by Finkel and Bentley (1974). This study proposes a capacity-based variant that divides a cell into four smaller cells when its object count exceeds a set limit, subject to a stopping condition.

Remove the last sentence citing Lee et al. (2021) and Ru et al. (2022), unless you supply complete sources that actually support it. Replace it with:

> This study will compare the quadtree with a uniform grid to determine how each performs under the selected test conditions.

Once the actual spatial operation is decided, identify that operation here. Keep the rest of the introduction's sequence. Mentioning land as background in paragraph 1 is acceptable. [Finkel and Bentley record](https://scholars.uky.edu/en/publications/quad-trees-a-data-structure-for-retrieval-on-composite-keys/)

### 5. Introduction paragraph 5 — support the serious-game discussion

The current statements about learning, city planning, emergency response, and realism need sources. A focused replacement that uses literature already in the paper is:

> Simulation games provide an interactive way to represent decisions and their consequences. Huang et al. (2025) provide an example involving a drinking-water emergency, while Maxim and Arnedo-Moreno (2025) discuss principles for planning and evaluating serious games. In Pocket Silica, the evaluation will focus on computational performance and whether the prototype follows its defined rules. Learning outcomes will require a separate evaluation.

This preserves the paragraph's connection to games while matching your evaluation scope. [Huang et al.](https://doi.org/10.1371/journal.pone.0321210), [Maxim and Arnedo-Moreno](https://games.jmir.org/2025/1/e54075)

### 6. Review of Related Literature — correct source descriptions

Make these specific changes:

- In **Quadtree as a Spatial Data Structure**, change the last phrase “infrastructure and water” to “infrastructure and demand for water and electricity.” Describe Zhou et al. as an example of adaptive spatial sampling, rather than proof of game performance.
- Replace the **Quadtree Applications in Game Development** paragraph with the paragraph below. The current one treats visibility culling as if it proves that resource demand can be calculated once per cell.
- Rename **Serious Games for Water and Energy Resource Management** to **Serious Games for Water Resource Management**, because the three cited games concern water. Alternatively, retain the broader heading only after adding and discussing an actual electricity-management source.
- In the Huang summary, use “Initial findings suggested…” rather than a universal claim about communication and crisis resolution.
- Remove the claim that the water-game findings apply “just as easily to electricity.” Explain that your study proposes an electricity model with its own rules.
- Replace the **Realism in Serious Game Design** paragraph with the paragraph below. A detailed prototype is not automatically a validated model of the real world.

Replacement for **Quadtree Applications in Game Development**:

> Mishraa (2020) presents a Unity implementation that divides space according to mesh density. Tâm Trần Ngọc (2025) demonstrates quadtree-based cell culling, in which groups of objects can share visibility results. These examples show practical uses of spatial grouping in games. However, they do not establish how well a quadtree will perform in Pocket Silica. That question will be examined through the planned comparison with a uniform grid.

Replacement ending for **Serious Games for Water Resource Management**:

> These studies provide examples of how games represent water-related decisions and conflicts. Pocket Silica will apply the broader idea of resource management to water and electricity, using separate rules for each resource. The cited studies do not directly evaluate Pocket Silica's electricity model or its learning outcomes.

Replacement for **Realism in Serious Game Design**:

> Maxim and Arnedo-Moreno (2025) reviewed digital game design frameworks and identified common elements such as clear objectives, game mechanics, prototyping, testing, and repeated improvement. Their review supports planning and evaluating a game according to its stated purpose. In Pocket Silica, the technical evaluation will check whether the prototype follows its defined simulation rules. This does not establish that it predicts real-world resource conditions or improves learning.

Use the linked sources in items 1 and 5, and the corrected references in items 22–24.

### 7. Objective 4 — include the confirmed NPC behavior

Replace Objective 4 with:

> To verify that the simulation correctly applies the intended rules for infrastructure growth, water consumption, electricity supply and demand, and NPC protest responses.

Objectives 1–3 can stay for now. Refine Objective 1 when the actual spatial operation in item 2 has been selected. Do not add NPCs to the quadtree merely because they are present in the game; include them in its entity model only if the implementation actually stores them there.

### 8. Conceptual Framework — align Figure 1 with the comparison

Figure 1 is still the original diagram. It labels the quadtree as both an independent variable and a moderating variable. No separate moderation or mediation analysis is described in the methodology.

Use these labels:

| Part | Content |
| --- | --- |
| Independent variable | Spatial partitioning method: quadtree versus uniform grid |
| Dependent measures | Processing time, FPS, memory use, and simulation correctness |
| Control conditions | Same map, infrastructure data, NPC settings and input events, water and electricity rules, build settings, and test device within each comparison |
| Algorithm behavior | Cell subdivision and cell count; label these as descriptive measures rather than a demonstrated mediating variable |
| Moderating-variable box | Remove the duplicated quadtree box for the current research design |

A workload such as entity count may vary between scenarios; it must remain the same for both methods within each paired comparison. It is not globally constant if you deliberately vary it in the experiment.

Replacement for the explanation below Figure 1:

> Figure 1 shows the planned comparison between the quadtree and uniform grid. The spatial partitioning method is the independent variable. Processing time, FPS, memory use, and correctness-test results are the measured outputs. Cell subdivision and cell count will describe how the structures behave. Both implementations will use identical conditions within each comparison, including the map, infrastructure data, NPC settings, resource rules, input events, and test device.

### 9. Paradigm heading — restore the full title

The document paragraph currently reads **Paradigm of the S**. Change it to **Paradigm of the Study**. The title inside the inserted diagram is already complete.

### 10. IPO diagram and explanation — restore the missing inputs

The new diagram correctly includes protests. In replacing it, the old map, infrastructure, and capacity inputs were lost. Add them back.

Use this complete content:

| Input | Process | Output |
| --- | --- | --- |
| Map dimensions and simulation parameters | Quadtree and uniform grid implementation | Pocket Silica prototype with visible protest behavior |
| Infrastructure positions, types, and growth data | Infrastructure growth and the selected spatial operation | Performance results: processing time, FPS, and memory use |
| NPC population and behavior settings | Water and electricity calculations and NPC protest responses | Correctness-test results |
| Water and electricity supply/demand settings and protest thresholds | Identical-scenario performance comparison and correctness testing | |
| Cell capacity and stopping settings for the quadtree; cell size for the grid | | |

Replacement for the explanation below Figure 2:

> Figure 2 follows the Input, Process, and Output model. The inputs include map dimensions, infrastructure data, NPC population and behavior settings, water and electricity settings, protest thresholds, and the configuration of each spatial structure. The process includes implementing the quadtree and uniform grid, running the same growth and resource simulation, updating NPC protest responses, comparing performance, and checking expected results. The outputs are the Pocket Silica prototype, processing-time, FPS, and memory-use results, and simulation correctness-test results.

### 11. Scope and significance — keep the scope, clarify the evaluation boundary

Keep the NPC protest sentence already added to Scope. Add **learning outcomes** to the existing exclusion of player enjoyment and engagement:

> Player enjoyment, engagement, and learning outcomes will not be evaluated because the study focuses on computational performance and simulation correctness.

Replace the **Academic Community** significance paragraph with:

> To the academic community, this study provides an example of applying a quadtree to a mobile simulation involving infrastructure growth, water, electricity, and NPC responses. It also provides a comparison with a uniform grid under the same test conditions.

This removes the unsupported claims about most quadtree research and avoids overstating novelty. Retain the possibility language already used for players and planning agencies.

### 12. Definition of Terms — correct Resource Conflict and define NPC

Resource Conflict is still water-only. Replace it with:

> **Resource Conflict** — A simulated condition in which demand for water or electricity exceeds the available supply, leaving some demand unmet.

Add:

> **Non-Player Character (NPC)** — A character controlled by the simulation that reacts through protests when a resource reaches its defined protest-triggering level.

Keep Resource Demand and Resource Shortage. Once selected, also define the specific spatial operation, simulation step, cell capacity, and stopping limit clearly enough to match the implementation. Make “reaches capacity” versus “exceeds capacity” consistent everywhere; the final rule must match the code.

## Chapter 2 changes

### 13. Research Design — split the opening and include protest checks

Keep the controlled-experiment introduction. Start a new paragraph at **This study follows the Agile development methodology** so that research evaluation and software development are distinct.

In Requirements, add NPC protest behavior to the feature list. In Testing, add:

> The correctness tests will also check whether NPC protests begin at the specified resource thresholds and follow the defined conditions for ending.

The present Design sentence includes NPC reactions correctly. Clarify the spatial operation there after item 2 is decided. Use future tense consistently for procedures that have not happened yet.

### 14. Add the missing method sections after the Agile discussion

Place these after the paragraph beginning **Agile fits this study well** and before **Research Environment**:

1. **Simulation Rules** — infrastructure growth, water, electricity, and NPC behavior.
2. **Spatial Data Structure Design** — actual spatial operation, quadtree, and uniform grid.
3. **Experimental Test Plan** — scenarios, known-answer checks, and measurement procedure.

Under **Simulation Rules**, a provisional NPC paragraph based on the confirmed mechanic is:

> NPCs will react through protests when resource supply reaches the specified protest-triggering level. The simulation will check the relevant water or electricity condition during its updates and display the corresponding NPC response. The resource thresholds and conditions for ending protests will be defined as part of the simulation rules.

Before submission, state the real thresholds and recovery rules instead of leaving the last sentence as a promise. Do not insert guessed percentages, local-supply mechanics, protest movement, or consequences that are not part of the game.

### 15. Research Environment — identify where measurements are made

List the actual game engine and version, language, development operating system, and test device specifications. State whether the benchmark uses a desktop build, emulator, or installed mobile build. Do not present desktop measurements as measurements of a mobile device.

Use **processing time, frames per second (FPS), and memory use** consistently. These three appear in Objective 3; all relevant methods sections need to cover them. Do not fabricate device specifications if the test setup has not been selected.

### 16. Respondents — use one evaluator group

The current group is IT/CS professionals or advisers. Keep that description unless you actually decide to recruit students instead. Change **professionals and or academic advisers** to **professionals or academic advisers**.

Supply the planned evaluator number, selection criteria, and actual checklist. Their feedback concerns required functions; it does not replace performance measurements or known-answer tests.

### 17. Research Instrument — replace the paragraph

> The study will use a performance testing tool, a correctness-test record, and a technical evaluation checklist. The performance testing tool will measure processing time, frames per second (FPS), and memory use for both implementations under identical conditions. The correctness-test record will document each scenario, its expected output, its actual output, and whether it passes or fails. The evaluation checklist will be given to the technical evaluators described in the Respondents of the Study section to assess the prototype's required functions.

Also identify the actual measurement tool and what each metric measures. Processing time needs a defined timed operation; memory needs a stated profiler definition; FPS needs a sampling procedure. A frame-rate cap or drawing workload can hide differences in algorithm time, so interpret the measures separately.

### 18. Data Gathering Procedure — replace the paragraph

> Data will be gathered through automated tests and technical evaluation. The researcher will run both implementations using the same initial conditions, saved input events, and simulation rules, recording processing time, FPS, and memory use. Correctness tests will record expected and actual results for spatial operations, water and electricity calculations, and NPC protest responses. The finished prototype will then be presented to the technical evaluators, who will complete the evaluation checklist and may provide written comments.

The final procedure must specify the actual run plan described in item 25 below.

### 19. Data Treatment — replace the paragraph

> Performance results will be grouped by implementation and test scenario. Repeated runs will be summarized using clearly stated measures of typical performance and variation. Correctness results will report passed and failed cases and explain differences between expected and actual outputs. Evaluation checklist responses will be summarized according to the checklist's response scale, and written comments will be grouped by recurring issue.

Specify the selected summary statistics once the run plan and checklist scale are chosen. Do not average ratings unless you actually use a defined numerical scale. Do not claim statistical significance from an average alone. Keep repeated measurements of one saved input distinct from different independent inputs.

### 20. Ethical Considerations — replace the paragraph

> Participation in the technical evaluation will be voluntary. Evaluators will be informed of the purpose of the study, the review tasks, and how their responses will be used. Only information needed for the evaluation will be collected, and identifying details will be excluded from reported results. Evaluation records will be handled according to the institution's requirements. Public sources used for the simulation background will be cited properly.

State the actual access and retention arrangements where your institution requires them. Public project information does not remove responsibilities for evaluator feedback and consent records.

## Wording, formatting, and references

### 21. Apply these direct wording and structure corrections

| Current text | Replacement or action |
| --- | --- |
| Review of Related Literatures | Review of Related Literature |
| Research Methodologies | Research Methodology, unless the school prescribes otherwise |
| Paradigm of the S | Paradigm of the Study |
| The Figure 1 / The Figure 2 | Figure 1 / Figure 2 |
| This one show | This study shows, or use the replacement in item 11 |
| frames per seconds | frames per second |
| Computer Science students in Instrument/Treatment | technical evaluators, matching Respondents |
| space capacity limit | cell capacity limit |
| simulation accuracy, when testing programmed rules | simulation correctness |
| basic grid-based method / grid-based baseline | use uniform grid-based approach consistently |
| Figure 4 Loading Screen | Figure 4: Loading Screen, matching the other captions |
| Arnedo Moreno | Arnedo-Moreno |

Put headings in separate paragraphs from body text. This applies to Review of Related Literature, Scope and Delimitation, Significance, and Definition of Terms. Apply your school's heading hierarchy and Word heading styles. Separate figures from heading paragraphs where they currently share one paragraph. The source has many empty paragraphs; inspect their actual page effect before deleting them so that figure placement is not damaged.

Keep the school's font, margins, spacing, and caption requirements. Do not change them to inflate the page count. Identify screen designs as proposed mockups unless they are screenshots of the working prototype. Keep each caption next to its figure and explain the main screen's resource indicators and protest display if those features are shown.

### 22. Correct these verified reference details

| Entry | Correction |
| --- | --- |
| Game Developer article | Author Videep Mishraa; 27 October 2020. Cite Mishraa (2020) in text. |
| Pinwheel tutorial | Credit the displayed author Tâm Trần Ngọc. The page was published 3 June 2024 and updated 25 September 2025; identify the version consistently. |
| Zhou et al. | Include article number 1365366 after volume 11. |
| McGiven et al. | Pages 2961–2974. Preserve the spelling Müller. |
| Wamucii et al. | Pages 3495–3518; include the eight authors in the reference entry. |
| Maxim and Arnedo-Moreno | Preserve the hyphen in the second surname. |
| Linked IEA news article | Publication date is 16 April 2026; 2025 in its title is the year being discussed. |

Source links: [Mishraa](https://www.gamedeveloper.com/programming/quadtree-in-unity), [Pinwheel](https://www.pinwheelstud.io/post/how-to-do-cell-based-culling-using-quadtree-in-unity-c-part-1), [Zhou](https://doi.org/10.3389/fmars.2024.1365366), [McGiven](https://hess.copernicus.org/articles/29/2961/2025/), [Wamucii](https://hess.copernicus.org/articles/28/3495/2024/), [Maxim](https://games.jmir.org/2025/1/e54075), [IEA](https://www.iea.org/news/data-centre-electricity-use-surged-in-2025-even-with-tightening-bottlenecks-driving-a-scramble-for-solutions).

### 23. Add or reconcile missing references

Add:

> Finkel, R. A., & Bentley, J. L. (1974). Quad trees: A data structure for retrieval on composite keys. *Acta Informatica, 4*(1), 1–9. https://doi.org/10.1007/BF00288933

If using the replacement local-background paragraph, add:

> Reparejo, A. J. R. (2026, August 10). BCDA clarifies misconceptions on Pax Silica project in New Clark City. *Philippine Information Agency*. https://pia.gov.ph/news/bcda-clarifies-misconceptions-on-pax-silica-project-in-new-clark-city/

The existing Lee et al., Ru et al., and Manila Bulletin citations do not have complete matching reference entries. Supply and verify them, or remove the associated citations and unsupported statements. Do not choose a different paper merely because its author and year happen to match.

The Bloomberg reference is listed under Nicoletti, Ma, and Bass, so use Nicoletti et al. (2025) in text if retaining it. Its direct page fetch was restricted during checking; this is not a finding that the article is false. If retaining the Philstar story, its byline is Josiah Antonio, so match its reference and in-text author accordingly. The supplied PNA URL returned 404 and needs repairing or replacement; that does not prove the article never existed.

### 24. Make the reference list consistent

Use your department's required citation style. If it is APA, alphabetize the final references, use hanging indents, and keep each complete reference together rather than splitting author, title, and URL into unrelated paragraphs. Use et al. in text for three or more authors, while listing the required authors in the reference entry. Replace Wamucii's reference-list et al. with:

> Wamucii, C. N., van Oel, P. R., Teuling, A. J., Ligtenberg, A., Gathenya, J. M., Hofstede, G. J., van Noordwijk, M., & Speelman, E. N.

Each in-text citation must have a matching reference, and each item in the cited reference list must be used in the text. If the school requires separate local/foreign or thematic groups, follow that template rather than imposing a different structure.

## Settings that must come from your actual design

### 25. Specify the simulation and algorithm settings

These are missing details, not values that should be guessed:

- The actual spatial operation, entities indexed, and reason it is needed.
- Infrastructure growth rule and what buildings demand.
- Water starting amount, units, replenishment if any, shortage and allocation rules, and prevention of negative quantities.
- Electricity meaning and units: capacity, energy available per time interval, or stored energy. Use compatible demand units.
- Whether protest thresholds use remaining supply, a percentage, or demand satisfaction; whether equality triggers a protest; which resources trigger it; and when it stops.
- Whether protests are a visible reaction only or have other implemented consequences. NPC demand, movement, and effects on growth have not been confirmed.
- Simulation time step and update order.
- Quadtree capacity, subdivision condition, stopping limit, boundary handling, and update policy.
- Uniform grid cell size and equivalent operations.

### 26. Specify the experiment and evaluator settings

- Actual map sizes, entity counts, layouts, event sequences, and saved seeds if randomness is used.
- Identical input data for both methods and a fair method of choosing their configurations.
- Warm-up, measured duration, number of repetitions, reset procedure, and run order.
- Actual measurement tools, timed operation, memory definition, FPS sampling, graphics settings, and frame-rate cap.
- Known-answer tests for spatial queries, resource calculations, protest triggers and recovery, subdivision limits, and boundaries.
- Expected answers and numeric tolerances where relevant.
- Actual development and test platform, evaluator number, selection criteria, checklist items, and response scale.

These details provide useful methodological content. Finalize them to make the study reproducible; do not add invented values or repeated background paragraphs simply to increase the page count.
