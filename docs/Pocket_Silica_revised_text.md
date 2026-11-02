# Pocket Silica revised text

This is a text companion to the original Word document. It provides clearer wording for the existing sections and proposed additions to the methodology. It uses water and electricity throughout. The expanded methods are a proposed research plan and must match the system and protocol adopted with the adviser. Keep the original figures in Word and update their labels as described in the separate review.

## Chapter 1 Introduction and related literature

### Introduction

Large technology projects raise questions about land use and the supply of water and electricity. These questions also provide a setting for a computer science problem: how can a simulation manage many objects when some parts of a map are crowded and others are almost empty?

The proposed Pax Silica development in New Clark City, Capas, Tarlac, provides the local background for this study. A Philippine Information Agency report describes BCDA's position that the development will host semiconductor and advanced manufacturing facilities. The same report states that BCDA plans separate water and power arrangements for the development (Reparejo, 2026). These are reported plans, not measured outcomes.

Pocket Silica uses this background to create a fictional infrastructure and resource-management scenario. It does not treat Pax Silica as a confirmed data-center project or assume that it will draw water and electricity from existing community supplies. Instead, it uses simplified rules to explore what happens inside a simulation when infrastructure demand increases while available resources are limited.

The technical focus is spatial data management. A simulation may need to find which buildings are inside a service area, identify nearby consumers, or update selected parts of a map. A uniform grid divides the map into cells of the same size. A quadtree divides space into four parts at each subdivision, allowing some areas to have smaller cells than others. Finkel and Bentley (1974) described an early quadtree structure. This study will use a capacity-based variant that divides a cell when it contains too many entities, subject to a depth or size limit.

A quadtree may reduce the work needed for some spatial queries, but it also requires memory and time to maintain its cells. Its value depends on the distribution of entities and the operations performed. The study will therefore compare it with a uniform grid rather than assume that it is always the better choice.

The simulation will be presented through a mobile game prototype called Pocket Silica. The game will provide an interface for infrastructure growth and resource demand. The research will evaluate the algorithm's performance and whether the program follows its specified rules. It will not measure learning outcomes or predict the actual environmental effects of Pax Silica.

### Statement of the problem

The study will examine whether a quadtree is a suitable spatial data structure for a mobile simulation of infrastructure growth and competition for water and electricity. It will address the following questions:

1. How can a quadtree organize infrastructure entities and support the spatial operations required by the simulation?
2. How can the algorithm be integrated into a working mobile game prototype?
3. How do the quadtree and uniform grid compare in processing time, memory use, and frame performance as entity counts and spatial layouts change?
4. Do both implementations produce the expected spatial-query and resource-allocation results under predefined test conditions?

### Objectives

The general objective is to design, develop, and evaluate a quadtree-based spatial simulation in a mobile game prototype that models infrastructure growth and demand for limited water and electricity.

The specific objectives are:

1. To design a quadtree that organizes infrastructure entities and supports the simulation's spatial queries as the map becomes more crowded.
2. To implement the quadtree and the rules for infrastructure growth, water demand, and electricity demand in Pocket Silica.
3. To compare the quadtree with a uniform grid using the same workloads, simulation rules, and test conditions, measuring processing time, memory use, and frame performance.
4. To verify spatial-query results and resource calculations using test cases with known expected answers.

### Review of related literature

#### Quadtrees as spatial data structures

A quadtree organizes two-dimensional space through repeated subdivision into four parts. The rules for subdivision depend on the variant used. In this study, an entity will represent an object such as a building, and a cell will divide when its entity count exceeds a set capacity, unless a stopping limit has been reached.

Zhou et al. (2024) applied quadtree-based methods to ocean sampling. Their work uses spatial variation to help select sampling locations under a limited sampling budget. It supports the use of adaptive spatial subdivision for uneven information, although its sampling methods differ from the capacity-based structure proposed for Pocket Silica. It does not directly establish how the proposed game will perform.

#### Quadtrees in game development

Mishraa (2020) presents a Unity example that divides space according to mesh-vertex density. The example illustrates bounds checking, insertion, capacity limits, and subdivision. It provides a practical reference for implementation rather than an experimental comparison of resource simulations.

The Pinwheel Studio tutorial by Tâm Trần Ngọc (2025) describes quadtree-based cell culling for largely stationary objects. Objects are grouped spatially so that visibility tests can sometimes be applied to a group. This is useful background for grouping nearby objects, but deciding whether objects are visible is different from calculating their resource demand. Pocket Silica must test its own queries and update rules.

#### Serious games for water resource management

Huang et al. (2025) developed a game about a drinking-water contamination emergency. Initial sessions with 41 participants suggested that frequent, proactive, and transparent communication could improve crisis decisions. The study provides an example of using game rules to represent a resource-related problem, although its main focus is communication rather than spatial-index performance.

McGiven et al. (2025) developed Thirsty Earth, in which players make farming and irrigation decisions under uncertain conditions. The game includes cooperation and shared water resources. It provides a reference for representing competing demands through playable rules, rather than evidence about the speed of a quadtree implementation.

Wamucii et al. (2024) used the ENGAGE game to support discussion of water challenges in Kenya's upper Ewaso Ngiro basin. Their game sessions examined decisions, participation, and communication. The work shows how a game can support discussion about resource allocation. Pocket Silica will have a different evaluation focus: computational performance and software correctness.

#### Design and evaluation of serious games

Maxim and Arnedo-Moreno (2025) reviewed digital serious-game design frameworks and identified shared design principles. Their review supports a planned development process with clear objectives and evaluation. For Pocket Silica, the evaluation must match the intended contribution. A working prototype and correct calculations can support technical claims, but educational benefits would require a separate study of users and learning.

### Synthesis and research gap

The reviewed sources address adaptive spatial structures, practical quadtree implementations, and games about water-related decisions. Their purposes and evaluation methods differ. The reviewed game studies do not provide the particular quadtree-versus-grid benchmark proposed for Pocket Silica, while the reviewed quadtree examples do not evaluate this mobile infrastructure and resource scenario.

The research gap is therefore a specific implementation and evaluation question: how will a capacity-based quadtree compare with a uniform grid when both perform the same spatial operations in a mobile simulation involving water and electricity? This statement is limited to the literature reviewed. It does not claim that electricity games or similar combinations have never been studied.

Pocket Silica will address this question through a working prototype, a controlled comparison, and test cases with known answers. The contribution will be evidence about the selected implementation and workloads, including conditions where the quadtree helps and conditions where its maintenance cost may outweigh its benefits.

### Conceptual framework

Figure 1 will show the relationship between the spatial data structure and the measured results. The main factor being compared is the spatial partitioning method: a quadtree or a uniform grid. Entity count and spatial layout will be varied to create different workloads. Within each paired comparison, both methods will receive the same map, entity positions, resource settings, and sequence of events.

The performance measures will include simulation-update time, spatial-query time, memory use, and frame performance. Correctness will be assessed separately by comparing query results and resource values with expected answers. Quadtree depth, node count, and leaf count will describe how the structure behaves; these measures will not, by themselves, establish that it performs better.

The comparison will hold the device, build settings, graphics settings, time-step duration, and logging procedure constant wherever possible. This will help distinguish changes caused by the spatial method from changes caused by other parts of the system.

### Paradigm of the study

Figure 2 will follow an Input, Process, and Output model. Inputs will include map dimensions, entity positions and types, water and electricity supply settings, demand values, service areas, and the configuration of each spatial structure.

The process will include implementing the two spatial methods, applying the same simulation rules, running predefined workloads, checking expected results, and recording performance. The outputs will be the Pocket Silica prototype, benchmark records, correctness-test results, and an analysis of the two methods under the tested conditions.

### Scope and delimitations

The study will cover the design, development, and evaluation of a capacity-based quadtree within Pocket Silica, a mobile game prototype. The simulation will represent infrastructure growth and demand for two resources: water and electricity. A uniform grid will provide the baseline for comparison.

The study will examine the quadtree's insertion, subdivision, and spatial-query operations. It will compare performance across selected entity counts and layouts and will check calculations using predefined scenarios with known expected results. A small group of qualified technical evaluators will review the prototype's required functions.

The map and resource rules will be simplified. Public information about Pax Silica will provide context, while test inputs will be selected for simulation and benchmarking. The study will not collect field measurements of water, electricity, land use, or community conditions in Tarlac. It will not treat the simulation as a forecast of actual resource demand or environmental effects.

The prototype will not include multiplayer features or in-app purchases. Player enjoyment, learning outcomes, and public attitudes will not be measured. The study will not assess whether Pax Silica should proceed. Performance conclusions will apply to the devices, software versions, configurations, and workloads actually tested.

### Significance of the study

For computer science students and researchers, the study will provide a documented example of implementing and evaluating spatial data structures in a mobile simulation. Its benchmark procedure and test cases may help later projects make comparable measurements.

For game developers, the prototype may provide a reference for organizing entities and carrying out resource-related spatial queries. The results will help explain when the tested quadtree configuration is useful and when a uniform grid may be sufficient.

For educators and interested players, the prototype may provide a visual example of how increasing demand can interact with limited supplies under stated rules. Any improvement in understanding would need to be tested separately.

For planning agencies and community organizations, the prototype may serve as a simplified discussion aid. It will not replace environmental assessments, engineering models, or local consultation.

For future researchers, the study will provide a starting point for adding better data, refining allocation rules, testing other spatial structures, or evaluating learning and usability.

### Definition of terms

**Quadtree.** A spatial data structure in which a cell can have four child cells. This study will use capacity-based subdivision with a stopping limit.

**Spatial simulation.** A computer model that represents objects, locations, and changes over time.

**Entity.** An object represented in the simulation, such as an infrastructure building or resource consumer.

**Cell capacity.** The maximum number of entities allowed in a quadtree leaf before subdivision is considered.

**Leaf cell.** A cell that has no child cells and stores entities directly.

**Uniform grid.** A spatial structure that divides the map into cells of the same size, used as the comparison method in this study.

**Service area.** A defined part of the map within which a resource source can serve consumers.

**Resource demand.** The quantity of water or electricity an entity requests during a simulation step.

**Resource shortage.** The portion of requested demand that cannot be supplied under the model's allocation rules.

**Simulation step.** One fixed interval during which the model applies growth, demand, and allocation rules.

**Correctness.** Agreement between a program's output and the expected output under its specified rules.

**Frames per second.** The number of displayed frames produced in one second, abbreviated as FPS.

**Random seed.** A saved starting value used to reproduce the same generated input sequence.

## Chapter 2 Research methodology

### Research design

The study will develop a mobile simulation prototype and evaluate it through controlled computational experiments. The development work will produce Pocket Silica and two implementations of its spatial operations: one using a quadtree and one using a uniform grid. The experiments will compare these implementations under the same input conditions.

Each comparison will use the same map, entities, resource settings, event sequence, and simulation duration. The spatial data structure will be the main difference between the two versions. This will allow the researcher to examine how the selected method affects processing time, memory use, and frame performance.

The study will also verify correctness through small test cases with known answers. These checks will cover entity storage, spatial queries, and the allocation of water and electricity. Technical evaluators will provide a supplementary review of required functions. Their opinions will not replace measured benchmark results or automated correctness checks.

Agile will guide software development. It will allow the algorithm, resource rules, and interface to be built and improved in short cycles. The experimental procedure will remain a separate part of the research design so that development progress and research evidence are clearly distinguished.

### Agile development process

Figure 3 will show the repeated development cycle. Each cycle will include requirements, design, implementation, testing, and review. A working build will be prepared for evaluation after the required functions and correctness checks have been completed.

#### Requirements

The researcher will identify the prototype's required functions. These will include creating a map, placing infrastructure entities, tracking water and electricity, running spatial queries, displaying shortages, and exporting test records. The requirements will also specify which operations must be identical in the quadtree and grid versions.

Each requirement will have an observable check. For example, a requirement to prevent duplicate counting will be checked using an entity placed exactly on a cell boundary. These checks will connect the implementation work to the research objectives.

#### Design

The researcher will design the entity records, resource rules, spatial structures, interface, and logging format. The design will separate the simulation logic from screen drawing so that graphics work does not become confused with algorithm work.

The proposed loading screen will introduce the prototype while required assets are prepared. The main screen will show the map, infrastructure, and water and electricity indicators. The settings screen will contain the controls actually supported by the prototype. Figures 4, 5, and 6 will illustrate these screens and should be identified as mockups until they show a working implementation.

#### Implementation in sprints

Initial sprints will implement entity storage and the spatial structures. Later sprints will add resource demand, allocation, growth events, the interface, and automated measurements. A sprint will be considered complete when its required functions and related checks pass.

The same simulation logic will be reused by both spatial methods. This will reduce the risk that a difference in resource calculations is mistaken for a difference in algorithm performance.

#### Testing and review

The researcher will test new functions after each sprint and record defects. Failed correctness cases will be corrected before the benchmark build is finalized. Adviser feedback may guide revisions to the design and required features.

After the benchmark configuration is fixed, changes that affect performance or calculations will require the relevant tests to be repeated. The build used for each recorded experiment will be identified in the results.

### Research environment and technical setup

Development will take place on a computer capable of running the selected game engine and its development tools. The final methodology will identify the engine, programming language, operating system, and their versions. It will also identify the actual mobile device used to evaluate the mobile build, including its processor, memory, operating-system version, and relevant display settings.

Desktop development measurements and mobile measurements will be reported separately. Editor performance will not be presented as mobile-device performance. If only one mobile device is available, conclusions will be limited to that device.

The test record will include the build type, graphics settings, frame-rate limit, and measurement tools. Tests will use consistent device settings. Background activity and thermal conditions will be controlled as far as practical, and interruptions or unusual conditions will be recorded.

### System requirements and architecture

Pocket Silica will contain four connected parts: the interface, the simulation model, the spatial data structure, and the measurement tool. The interface will show the game state and accept permitted player actions. The simulation model will update buildings, demand, supplies, and shortages. The spatial structure will organize entities and answer location-based queries. The measurement tool will save test settings, performance records, and correctness results.

The simulation model will call a shared set of spatial operations. The quadtree and grid will each implement these operations so that the simulation can switch methods without changing the meaning of a query or the resource-allocation rules.

Automated benchmark runs will use saved actions rather than live player input. This will allow both methods to receive the same events at the same simulation steps. Interactive play will demonstrate the prototype, while saved scenarios will provide repeatable research measurements.

### Simulation model and assumptions

The proposed model will represent infrastructure entities as points on a two-dimensional map. Each record will contain an identifier, position, type, operating state, water demand, and electricity demand. If the implementation requires building footprints instead of points, the overlap and ownership rules will be specified before testing.

Resource sources will have defined service areas. A spatial query will identify the consumers inside each area. This operation gives the spatial data structure a direct role in the simulation. A single global resource total, without location-based operations, would not by itself justify the quadtree comparison.

The simulation will advance in fixed time steps. The model will state how long a step represents and use the same duration for both methods. Growth events will add entities or change demand at saved steps. The same event list will be replayed in both implementations.

#### Water model

Water will be represented as a stored quantity. During each step, the model will add any defined replenishment, subject to storage capacity. It will then allocate water to eligible consumers without allowing supply to become negative.

For a source, available water will equal the smaller of its storage capacity and its previous balance plus replenishment. Its next balance will equal available water minus the quantity actually supplied. If eligible demand exceeds available water, the difference will be recorded as a water shortage.

#### Electricity model

Electricity will be represented as the energy available during a simulation step. The model will distinguish energy from power: water may be measured in liters, energy in kilowatt-hours, and power in kilowatts. If abstract game units are used, they will be labeled as game units and used consistently.

The proposed model will not carry unused electricity into the next step unless storage is explicitly included. Available energy for each step will be compared with eligible demand, and unmet demand will be recorded as an electricity shortage.

#### Allocation rules

Each resource will use a stated allocation rule. A simple proposed rule is proportional allocation: when supply is insufficient, eligible consumers receive the same fraction of their requested quantity. The rule will be applied identically by both spatial methods.

If a consumer can be reached by several sources, the model will use a fixed source order and track remaining unmet demand. A consumer will not receive more than it requested. Candidate entities will be processed in a stable order when necessary so that tree traversal order does not change allocations.

The prototype will define how shortages affect building activity. In the proposed minimal model, water and electricity requests are calculated first, and the fulfilled fractions determine the displayed operating state for that step. Unused or unmet quantities will not silently change another resource's calculation. Any more detailed coupling between the resources will need its own rules and tests.

The model will omit detailed hydrology, electrical-network behavior, and actual industrial production. These assumptions will keep the study focused on the stated computational problem.

### Quadtree design

The quadtree root will cover the complete map. A leaf will store the identifiers of entities located within its bounds. When insertion causes its count to exceed the selected capacity, the cell will divide into four equal child cells if the depth and minimum-size limits allow it.

Existing entities will be redistributed to their child cells after subdivision. Every point entity will belong to exactly one leaf. The implementation will define a consistent boundary rule so that an entity on a dividing line is neither lost nor counted twice. The map's outer boundary will have an explicit inclusion rule.

Subdivision will stop at the maximum depth or minimum cell size even if a leaf remains over capacity. The remaining entities will stay in that leaf. This will prevent repeated subdivision when many entities have the same or nearly the same position.

A service-area query will first test whether a cell overlaps the query region. Cells outside the region will be skipped. For overlapping cells, the algorithm will visit child cells or examine leaf entities. An exact position check will determine whether each candidate is inside the service area. The query will return the matching entity identifiers without duplicates.

The design will state whether entities remain stationary, whether deletion is supported, and whether empty cells can merge. The initial proposed workload will emphasize insertion and queries for stationary infrastructure. If movement or deletion is added, both methods will implement equivalent updates and the experiment will include their cost.

Tree construction, insertion, subdivision, and query time will be recorded separately where the measurement tool permits. The study will also record node count, leaf count, and maximum depth. These will help explain performance changes as entity layouts become more crowded.

### Uniform grid baseline

The baseline will divide the same map into cells of a fixed size. An entity's position will determine its cell. A service-area query will examine the grid cells that overlap the area and apply the same exact position check used by the quadtree.

The baseline will use the same entity records, service areas, event list, resource calculations, and result format. It will use a reasonable implementation rather than checking every entity unnecessarily. This will make the comparison useful to developers deciding between practical alternatives.

Cell size affects a grid's query cost and memory use, just as capacity and depth affect a quadtree. Candidate settings will therefore be examined in a pilot test. The selected settings and the reason for choosing them will be recorded before the main benchmark. Configuration choices will not be changed separately for individual results after seeing which method wins.

### Test scenarios and experimental procedure

The experiments will vary entity count and spatial layout. Layouts will include an evenly spread arrangement, a single dense cluster, and several clusters. These cases will test different distributions rather than favoring only the condition in which a quadtree is expected to perform well.

The final protocol will specify map size, entity counts, service-area locations and sizes, resource settings, growth schedules, and random seeds. Exact generated inputs will be saved so that both methods can receive identical data even if random-number generation changes later.

An initial pilot will check whether the selected workloads run successfully and whether the measurements are stable. It will help set the final entity counts, warm-up interval, measured duration, and number of repetitions. Those settings will be fixed and documented before the main experiment.

For each saved input, both methods will start from the same initial state. The researcher will reset the simulation, complete the warm-up interval, run the measured interval, and save the results. Run order will be alternated or randomized to reduce the effect of one method always being tested first.

Repeated runs of the same input will show measurement variation. Several saved layouts will provide variation across generated maps. These two sources of variation will be kept separate in the analysis. A crash or interrupted run will be recorded rather than silently removed, and any rerun will be identified.

### Verification and acceptance criteria

Correctness will be checked before interpreting performance results. For small test cases, a simple reference routine will examine every entity directly. Its matching identifiers will be compared with the identifiers returned by both spatial structures. Resource calculations will also be checked against hand-calculated examples.

Tests will include an empty map, one entity, several entities in one cell, entities on boundaries, repeated positions, overlapping service areas, sufficient supply, water shortage, electricity shortage, and simultaneous shortages. Growth tests will check that inserted entities contribute demand at the intended step.

For example, if two eligible buildings each request three water units and two electricity units per step, total requested demand must be six water units and four electricity units. If supplies are lower, the result must match the selected allocation rule and must not produce negative balances or duplicate allocations.

Entity identifiers and counts will require exact agreement. Numeric outputs will use a predefined tolerance appropriate to their units and representation. The tolerance and its reason will be recorded before the main tests. A case will pass only if the required conditions are met; failures will be corrected and retested.

Agreement between the two methods alone will not prove correctness because both may contain the same error. The independent reference routine and known-answer examples will provide additional checks. Passing these checks will show compliance with the model's rules, not accuracy in predicting real-world conditions.

### Technical evaluators and selection

The study will invite evaluators with relevant experience in computer science, information technology, software development, algorithms, or game development. Selection will be purposive: evaluators will be chosen for their ability to review the required technical functions.

The final methodology will state the number invited, the number who participate, and the inclusion criteria. Evaluators will review the prototype and its checklist. They will not be treated as a representative sample of players or the public.

### Research instruments

The first instrument will be an automated benchmark and logging tool. Each record will identify the algorithm, build, device, scenario, saved input, configuration, and run. It will record the selected timing and memory measures using stated units and measurement procedures.

Simulation-update time and spatial-query time will be measured in milliseconds. Memory will be reported using the definition provided by the selected profiler, such as total application memory or a clearly identified allocation measure. FPS and frame time will describe the visible application. These measures will be interpreted separately because screen rendering can limit FPS even when algorithm processing becomes faster.

The second instrument will be a correctness-test record containing the setup, expected output, actual output, and pass or fail result. It will include a place to record the defect and the outcome of a repeated test.

The third instrument will be a technical evaluation checklist. Items will be linked to the objectives and required functions, including correct entity placement, resource displays, shortage behavior, test execution, and result export. Response options will be met, partly met, not met, and not observed, with space for evidence and comments.

The adviser or another qualified reviewer will examine the checklist before use to identify unclear, repeated, or unrelated items. The researcher will revise the instrument based on that review and retain the final version with the study records.

### Data gathering procedure

1. Finalize the simulation rules, configurations, instruments, and test protocol with the adviser.
2. Complete the required functions and correct defects found in the known-answer tests.
3. Run a pilot to finalize the workload range and measurement procedure.
4. Save the benchmark build, settings, scenario files, seeds, and event lists.
5. Execute both methods on each saved input using the same device and procedure.
6. Check logs for missing values, interruptions, and crashes, and document any reruns.
7. Present the working prototype and checklist to the technical evaluators after obtaining their consent.
8. Organize benchmark records, correctness results, and evaluator feedback for analysis.

### Data analysis

Results will be grouped by algorithm, entity count, layout, and configuration. Repeated runs on the same saved input will be summarized before comparisons are made across inputs. The analysis will report the number of inputs and repetitions so that readers can identify what each summary represents.

Timing summaries will include a typical value, such as the mean or median, together with a measure of variation. Frame-time results may include a high percentile to show slower frames, provided the sampling procedure and sample count are reported. Startup measurements will be separated from the measured steady-running interval.

For a paired timing comparison, the percentage change relative to the grid will be calculated as the grid time minus the quadtree time, divided by the grid time, multiplied by 100. A positive value will indicate lower time for the quadtree; a negative value will indicate higher time. This calculation will be used only when the baseline value is nonzero and both measurements represent the same operation.

Memory results will be compared separately using the stated profiler definition. A method may be faster while using more memory, so the discussion will consider both measures. Quadtree node counts and grid configuration will help explain these differences.

Correctness results will report passed and failed cases, the kinds of errors found, and the outcomes after correction. Checklist responses will be summarized using counts for each response option. Written comments will be grouped by recurring issue, while preserving any important difference in evaluator views.

The study will not assume that repeated timing samples are independent maps or claim statistical significance from an average alone. If an inferential test is required, the analysis plan will identify an appropriate independent unit, check its assumptions, and select the test before interpreting the benchmark results.

### Ethical considerations

Evaluators will receive a clear explanation of the study and the purpose of the checklist. Participation will be voluntary. The consent process will explain the tasks, the expected time, how feedback will be used, and the point until which a participant can withdraw their feedback.

Feedback will use participant codes instead of names in the analysis. The researcher will limit access to consent records and evaluation files and state a retention and deletion schedule consistent with institutional requirements. Any required institutional review will be completed before evaluation begins.

Sources will be cited accurately. Reported project plans, simulation assumptions, and measured findings will be distinguished. The game and paper will not present fictional resource shortages as observed effects of Pax Silica or use real community identities without a justified research need.

### Methodological limitations

The experiment will test selected implementations and configurations. Results may differ with other devices, programming approaches, grid sizes, tree settings, or spatial operations. This will limit claims about which structure is best in general.

The resource model will simplify water storage and electricity supply. Technical evaluator feedback will concern required functions and will not establish environmental realism, usability for a wider population, or educational effectiveness. These areas may be addressed in later research.

## References

Finkel, R. A., & Bentley, J. L. (1974). Quad trees a data structure for retrieval on composite keys. *Acta Informatica, 4*, 1–9. https://doi.org/10.1007/BF00288933

Huang, J., Ashcraft, C. M., & Mo, W. (2025). Gamifying water crisis management: A serious game for drinking water contamination emergency response. *PLOS ONE, 20*(4), e0321210. https://doi.org/10.1371/journal.pone.0321210

Maxim, R. I., & Arnedo-Moreno, J. (2025). Identifying key principles and commonalities in digital serious game design frameworks: Scoping review. *JMIR Serious Games, 13*, e54075. https://doi.org/10.2196/54075

McGiven, L., Poland, K., Reinking, C., & Müller, M. F. (2025). Thirsty Earth: A game-based approach to interdisciplinary water resource education. *Hydrology and Earth System Sciences, 29*, 2961–2974. https://doi.org/10.5194/hess-29-2961-2025

Mishraa, V. (2020, October 27). QuadTree in Unity. *Game Developer*. https://www.gamedeveloper.com/programming/quadtree-in-unity

Reparejo, A. J. R. (2026, August 10). BCDA clarifies misconceptions on Pax Silica project in New Clark City. *Philippine Information Agency*. https://pia.gov.ph/news/bcda-clarifies-misconceptions-on-pax-silica-project-in-new-clark-city/PAGE

Tâm Trần Ngọc. (2025, September 25). How to do cell based culling using quadtree in Unity C#—Part 1. *Pinwheel Studio*. https://www.pinwheelstud.io/post/how-to-do-cell-based-culling-using-quadtree-in-unity-c-part-1

Wamucii, C. N., van Oel, P. R., Teuling, A. J., Ligtenberg, A., Gathenya, J. M., Hofstede, G. J., van Noordwijk, M., & Speelman, E. N. (2024). Guiding community discussions on human–water challenges by serious gaming in the upper Ewaso Ngiro River basin, Kenya. *Hydrology and Earth System Sciences, 28*, 3495–3518. https://doi.org/10.5194/hess-28-3495-2024

Zhou, Y., Lin, P., Liu, H., Zheng, W., Li, X., & Zhang, W. (2024). Fast and flexible spatial sampling methods based on the Quadtree algorithm for ocean monitoring. *Frontiers in Marine Science, 11*, 1365366. https://doi.org/10.3389/fmars.2024.1365366
