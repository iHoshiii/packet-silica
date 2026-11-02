# Pocket Silica Game Design Document

## 1 Title Page

**Game name:** Pocket Silica

**Tag line:** Grow technology while sustaining communities

**Document version:** 0.1

**Last updated:** 2 November 2026

**Institution:** Nueva Vizcaya State University, College of Information Technology Education

**Research title:** Pocket Silica: A Quadtree-Based Spatial Simulation for Modeling Data Center Growth and Water Resources Conflict in a Mobile Game

**Degree program:** Bachelor of Science in Computer Science, Major in Game Development

| Team member | Confirmed role |
| --- | --- |
| Aldwin Bernard V. Loreto | Research team member |
| Daniel John A. Dela Cruz | Research team member |
| Dustin A. Oliganga | Research team member |
| Ramonsito B. Adducul | Research adviser |

The full names and adviser are recorded on the supplied thesis presentation's title slide. Individual design, programming, art, testing, and documentation assignments remain to be allocated. No separate external client is designated; academic review involves the adviser and thesis panel.

This document specifies a proposed Android resource-management game and its research controls. Water-resource conflict is the main simulation focus, with electricity as a supporting mechanic. Technology, currency, farms, employment, community satisfaction, and four expansion zones provide the player's decisions and progression.

Version 0.1 defines the intended thesis prototype. Numeric settings are initial balancing defaults for pilot testing. A delivered software build and completed evaluation are not asserted by this specification. Future features are identified separately in Section 11.

## 2 Revision History

| Version | Date | Change | Responsibility |
| --- | --- | --- | --- |
| 0.1 | 2 November 2026 | Initial GDD covering the research scope, proposed game rules, campaign, endgame, interface, implementation, presentation details, and recommended statistical treatment. | Research team |

The structure follows the Serious Game Design Document Outline linked in Section 15. Changes to gameplay rules, balance profiles, experiment settings, and saved-data formats require a new document or configuration version. Each evaluated build must identify the versions it implements.

## 3 Game Overview

### 3.1 Purpose of the game

Pocket Silica is a single-player mobile management simulation set in a fictional developing region. The player establishes data centers and farms, supports communities, and expands utility capacity. Every new development changes demand for shared water and electricity. The central challenge is deciding how much growth existing sources can support while maintaining agriculture, a viable economy, and community services.

The game also provides a research environment for comparing a capacity-based quadtree with a uniform grid. Both methods organize the same entities and answer the same service-area queries. The study measures computational performance and checks the correctness of spatial queries, resource allocation, and protest responses. A quadtree advantage is an experimental question, not a victory condition or guaranteed result.

### 3.2 Intended use

The prototype is intended for standalone play, supervised thesis demonstrations, technical evaluator sessions, and repeatable benchmark runs. It can illustrate resource tradeoffs for discussion. The present study does not establish educational effectiveness, changes in public attitudes, enjoyment, engagement, or real environmental outcomes.

The fictional region uses simplified game units. Its results do not predict the effects of Pax Silica or represent a validated model of a real community, river, electrical network, or data center.

### 3.3 Justification for the design

Service areas make location relevant to resource access. Farms, households, and data centers create competing demands, while dense and sparse districts create different spatial workloads. This connects player decisions to the thesis's spatial-data-management problem. Four expansion zones provide a bounded campaign that can be completed within the thesis prototype's development scope.

The original thesis establishes infrastructure growth, water scarcity, supporting electricity mechanics, NPC protests, and the algorithm comparison. This GDD proposes the detailed economy, agriculture, employment, local supply rules, progression, and ending needed to turn that research setting into a playable game.

### 3.4 Target audience and genre

The proposed primary players are university students and adult players comfortable with basic touch controls. Technical evaluators, advisers, and researchers form a separate evaluation audience. The demographic and tutorial assumptions require pilot confirmation.

The genre is a single-player resource-management and spatial strategy simulation. It uses a top-down two-dimensional map, real-time simulation steps, and pause controls. Multiplayer, combat, in-app purchases, and competitive leaderboards are outside the prototype.

### 3.5 Central twist

The development that earns progress also increases pressure on resources. A profitable data center can meet a technology target while reducing the water available to households or farms. Expansion adds obligations because previously unlocked districts continue operating. Success requires sustained development that the region can support.

## 4 Gameplay

### 4.1 Player objectives

The player must unlock all four zones, reach the final technology target, and maintain adequate resources, agriculture, finances, and community satisfaction across the active region. Building the largest number of data centers is not an independent objective. A developed region must still support its households and agricultural activity.

### 4.2 Progression and play flow

The player starts in the northwest zone with a community, a farm, basic utility facilities, and a construction reserve. The other three zones are covered by fog. The player inspects local demand, places or upgrades facilities, runs the simulation, and responds to shortages. A milestone panel explains the conditions for the next expansion.

The core loop is to inspect supply and demand, plan a construction or operating decision, observe its effect, and correct shortages before adding further demand. Build mode pauses the campaign while a placement preview is open. Confirmed actions take effect at the next simulation-step boundary.

When a milestone remains satisfied for the configured stability period, the next adjacent zone unlocks permanently. The expansion sequence is northwest, northeast, southeast, then southwest. Every unlocked zone remains active. Unlocking a zone adds its configured community and reveals resource sites and buildable terrain.

### 4.3 Challenges and mission structure

The campaign combines increasing demand with different building layouts. Early play teaches coverage and capacity. Later districts increase the number of consumers sharing sources and introduce cross-border service areas. The player resolves these challenges using the same limited set of construction, upgrade, pause, and resume actions.

A tutorial introduces one action at a time. Each expansion begins with a short briefing explaining the new area's needs. Tutorial completion is based on performing actions and reading indicators; it is not a research measure of learning.

### 4.4 Victory and failure

The final objective is to develop all four districts into a region that sustains its technology, economy, communities, and agriculture within available water and electricity capacity. The final stability conditions must remain true for 20 consecutive simulation steps in the initial balance profile. Section 5 defines the exact checks.

Victory pauses simulation and presents a regional summary, resource history, technology total, and number of protests. The player may inspect the final map or restart. An endless sandbox is a future extension.

Persistent bankruptcy produces a recoverable scenario failure. In the initial profile, a negative currency balance for 20 consecutive steps opens a failure panel and pauses play. Shortages and protests provide warnings and economic consequences but do not instantly destroy the region. The player may load a checkpoint or restart; emergency grants and automatic debt forgiveness are excluded from the baseline.

### 4.5 Scoring

The campaign reports milestone completion and final stability rather than a combined score that allows money to cancel out severe shortages. Completion time, peak technology production, shortage steps, and protest events are descriptive summary values. These are gameplay indicators, separate from the thesis's processing-time, frame-performance, and memory measurements.

## 5 Mechanics

### 5.1 Simulation model and time

The world contains stationary infrastructure and community entities on a bounded two-dimensional map. Resource transfers use quantities per logical simulation step. The initial pacing default is one step per real second at normal speed; a second speed setting advances two steps per real second. Pause advances no logical steps. Pacing is configurable and must be frozen for formal experiments.

The simulation clock is independent of rendering. Resource demand, production, finances, satisfaction, and milestones update once per logical step. Touch input and animation may update between steps. Sources do not gain resources while the application is suspended, and there is no offline economy.

Every step follows this order:

1. Apply queued construction, upgrade, pause, and resume commands in recorded order, revalidating each against the current state.
2. Read the previous step's protest state and determine available workers and staffing fractions.
3. Calculate active entities' water and electricity requests from their configured building levels.
4. Replenish water sources, establish electricity generation, and allocate the two resources independently.
5. Calculate operating fractions, technology production, food production, income, and upkeep.
6. Determine food adequacy, update household satisfaction, and calculate the next protest state.
7. Update milestone and debt counters, save required state, and emit research records when enabled.

Requests are not recalculated after observing another resource's shortfall. A protest state calculated in this step affects workforce in the next step. This ordering prevents circular calculations and makes replays reproducible.

### 5.2 Entities and indicators

| Type | Main contribution | Main requirements | Important state |
| --- | --- | --- | --- |
| Community group | Residents, available workers, and household income | Water, electricity, and food | Population, satisfaction, shortage counters, protest state |
| Data center | Cumulative technology and operating income | Water, electricity, workers, and upkeep | Building level, operating fraction, output |
| Farm | Food and agricultural income | Water, supporting electricity, workers, and upkeep | Building level, operating fraction, food output |
| Water facility | Stored water and replenishment | Construction and upkeep | Storage, replenishment, service radius |
| Power plant | Electricity generation per step | Construction and upkeep | Generation cap and service radius |
| Dam facility | Both water and electricity outputs | Approved site, construction, and upkeep | Separate water storage and generation caps |

Currency, technology, food adequacy, employment, and satisfaction are indicators rather than collectible objects. Residents are represented by community groups with visual NPC markers. The prototype does not simulate individual journeys, births, deaths, migration, or inventories.

### 5.3 Initial balance profile

The following settings define a testable starting profile called `campaign_v0_1`. They are proposed design defaults, not calibrated real-world quantities or final balance findings. Water, electricity, food, technology, and currency use explicitly labeled game units.

| Entity at level one | Build cost | Water demand per step | Electricity demand per step | Job slots | Maximum food or technology per step | Income per step | Upkeep per step |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Community group | Scenario placed | 10 | 6 | Supplies 20 workers | Requires 6 food | 4 | 0 |
| Farm | 40 | 6 | 2 | 4 | 8 food | 3 | 1 |
| Data center | 80 | 12 | 8 | 8 | 1 technology | 9 | 3 |
| Water facility | 70 | 0 | 0 | 0 | 20 water replenishment | 0 | 2 |
| Power plant | 70 | 0 | 0 | 0 | 20 electricity generation | 0 | 2 |
| Dam facility | 150 | 0 | 0 | 0 | 20 water and 15 electricity | 0 | 4 |

Each community group represents 30 residents, including the 20 available workers. The workforce is part of that population, not an additional population count. Food demand and income are per community group. The starting currency reserve is 300, technology is zero, and household satisfaction is 80 out of 100.

Water facilities start with 80 stored units and have a capacity of 160. Dams start with 120 and have a capacity of 240. Water facilities and power plants have a service radius of 240 map units; dams have a radius of 280. The initial water facility is scenario configured to replenish 30 units per step, and the initial power plant supplies 25 electricity units per step. Those starter advantages must be declared in the scenario data.

### 5.4 Placement and construction

The player selects a building from the construction menu and moves a preview over visible terrain. The preview shows build cost, new demand, coverage, and placement validity. Confirmation requires an unlocked zone, a free build site, a valid terrain tag, and enough currency to pay the full construction cost.

Sites use a 32-unit placement grid. Each occupied site belongs to one entity. Its center is the point used for spatial queries. Water facilities require a tagged intake site, dams require a tagged dam site, and other buildings require ordinary buildable terrain. Rivers are visual and scenario-defined resource features; detailed river flow is not simulated.

Confirmation queues the command without deducting money. At the next step boundary, the simulation rechecks placement, occupancy, and available currency, then deducts the cost and creates the entity as one transaction. An invalid or unaffordable queued command is rejected with a message and no charge. Commands later in the queue see the funds and occupancy left by earlier accepted commands. Upgrades use the same transaction rule. New buildings have no additional construction delay. Cancellation before confirmation costs nothing. Relocation, demolition, resale, and roads or pipe-network routing are future extensions.

### 5.5 Spatial service areas and allocation

A consumer is eligible for a source when its center is inside or exactly on that source's circular service radius. Sources can serve consumers across unlocked-zone borders. Sources and consumers inside locked zones remain inactive until the zone is unlocked. A large regional stockpile cannot supply a consumer outside every relevant service area.

Both spatial methods perform a service-area query, return candidate identifiers, and apply the same exact distance test. Results contain no duplicates. Sources are processed by immutable source identifier, and consumer identifiers are sorted before resource summation. This prevents tree traversal order from changing gameplay.

For each resource, maintain every consumer's remaining unmet request. At a source, total the remaining requests of eligible consumers. If that total is zero, allocate nothing. Otherwise divide available supply by total remaining demand and cap the resulting fraction at one. Give each eligible consumer its remaining request multiplied by that fraction. Reduce its unmet request and the source's supply by the actual allocation before processing the next source.

Overlapping sources therefore cannot supply more than a consumer requests. Fixed source ordering is a declared simplification and may affect allocation; the order must remain identical across algorithm modes. The baseline uses proportional allocation and has no player-controlled priority policy.

### 5.6 Water and electricity rules

At the start of a step, a water source adds its replenishment to its previous stored balance, up to storage capacity. Allocation subtracts only the water actually supplied. The next balance cannot be negative. A source with no consumers can accumulate water up to its capacity.

A power source provides its configured electricity quantity for the current step. Allocation uses the same eligibility and remaining-demand procedure as water. Unused electricity is discarded at step end. Batteries, electricity trading, electrical faults, and transmission losses are excluded.

A dam has separate configured water and electricity outputs. Drawing household water does not automatically change its generation in this version. Electricity-dependent pumping and water-dependent generation are excluded to avoid introducing an undefined circular resource model. Any later coupling requires its own rules and verification cases.

### 5.7 Workforce and operating performance

Workers form one abstract regional pool; travel distances and commuting are not modeled. A non-protesting community supplies all its configured workers. A protesting community supplies 50 percent in the initial profile. Essential water and electricity facilities do not require workers in this version so that basic supply can recover during a protest.

Active farms and data centers request their configured job slots. Available workers are distributed proportionally when the total requested jobs exceed the worker pool. All active workplaces receive the same staffing fraction in that case. Report filled jobs and unemployment separately from technology progress.

For each active farm or data center, calculate the fraction of water demand met, electricity demand met, and job slots filled. Its operating fraction is the smallest of those three fractions, clamped between zero and one. A resource that the entity does not require has a fulfillment fraction of one.

For example, a data center with water fulfillment of 0.75, electricity fulfillment of 1.0, and staffing of 1.0 operates at 75 percent. It produces 0.75 technology and 6.75 currency units before its full active upkeep is deducted. Its allocated resource consumption is recorded as supplied; the prototype does not refund water after finding a different bottleneck.

### 5.8 Agriculture and food

A farm's current-step food and income equal its configured maximum outputs multiplied by its operating fraction. Food is a current-step output, with no warehouse, spoilage, or trading system. Regional food adequacy is total food production divided by total household food demand, capped at one. If there are no households, food adequacy is one.

The food supply is shared regionally in this baseline. Each zone still reports local agricultural production, and milestones require enough local production for its community. This makes agriculture relevant to each district without adding delivery networks. Unmet food need reduces satisfaction and household income but does not independently trigger a protest in this version.

### 5.9 Economy and technology

Currency increases through operating farm and data-center income and household income. Household income is its base income multiplied by the smallest of its water, electricity, and regional food-adequacy fractions. Currency decreases through confirmed construction, upgrades, and upkeep. There is no borrowing interface, interest, taxation policy, currency pickup, or market speculation system.

The account updates once per step using actual income minus actual upkeep. Negative balances remain visible; they are not silently clamped to zero. Construction and upgrades require enough existing cash. A negative balance increments the debt counter, while a nonnegative balance resets it. Twenty consecutive negative steps cause the failure state described in Section 4.

Technology accumulates from operating data centers and never decreases due to a shortage. Current technology production is displayed separately. Low technology alone does not cause a protest. Milestones require currently operating facilities so that historical technology cannot substitute for an active economy.

### 5.10 Upgrades and operating controls

Each constructed facility supports one upgrade. The upgrade costs its original base construction cost and multiplies its level-one resource demands, job slots, maximum outputs, and active upkeep by 1.5, as applicable. A source upgrade increases replenishment or generation and storage capacity by 1.5 but leaves its service radius unchanged. An upgrade does not refill water storage for free. It preserves the entity's identifier and position.

The player may pause or resume farms and data centers. A paused workplace requests no workers or resources and produces no food, income, or technology. It pays 25 percent of its level-adjusted upkeep and does not count toward an active-development milestone. Households and essential supply facilities cannot be paused. Pause commands change operating state, not entity membership in the spatial index.

### 5.11 Satisfaction and protests

Each community has a satisfaction score from zero to 100. Its current target is 50 times its water-fulfillment fraction, plus 25 times its electricity-fulfillment fraction, plus 25 times regional food adequacy. Each step the score moves toward that target by at most five points. This is an abstract game rule, not a prediction of real public behavior.

A non-protesting community increments its shortage counter when either water or electricity fulfillment is below 80 percent. Otherwise that counter resets. Three consecutive shortage steps cause it to enter the protesting state at the end of the step. Low technology and low currency are not direct protest triggers.

A protesting community increments a separate recovery counter only when both water and electricity fulfillment reach at least 90 percent. Otherwise the recovery counter resets. After three consecutive qualifying steps, the community returns to normal at step end. While protesting, it remains protesting in the intermediate 80 to 90 percent band. Food affects satisfaction, income, and victory conditions but not this protest transition.

On entry to or recovery from protest, reset both the shortage and recovery counters to zero. Protests reduce the following step's available workers. Visual NPC groups display peaceful protest markers and their cause; there is no combat, policing, or suppression mechanic. Restoring services is the player's response. The original thesis's water-only protest objective must be aligned with its broader water-or-electricity scope before this combined rule is evaluated.

### 5.12 Expansion milestones and final stability

The initial cumulative technology targets are 20 for the first expansion, 60 for the second, 120 for the third, and 200 for final victory. Earlier targets do not reset when a new zone opens.

For an expansion, every currently occupied zone must have household water and electricity fulfillment of at least 90 percent, satisfaction of at least 70, no active protest, and local farm production sufficient for its household food demand. Each occupied zone must also contain at least one operating farm and one operating data center with an operating fraction of at least 0.90. Regional currency and current net income must both be nonnegative, and the technology target must be reached.

All conditions must hold for ten consecutive steps to reveal the next zone. Any failed condition resets the stability counter to zero. Unlocking occurs automatically at the end of that completed step: create the next zone's community, reset the stability counter, and save the post-unlock checkpoint. Newly activated entities first participate in the next step. Zones never relock. All four occupied zones must meet the same conditions for 20 consecutive steps at technology 200 to win.

### 5.13 Options and screen flow

The main menu opens New Campaign, Continue, Tutorial, Settings, Help, and Credits. New Campaign opens a briefing and then the map. Continue loads the last valid save. The map opens building inspection, construction, district status, milestone, and pause panels. A paused game can save, resume, return to menu, or restart after confirmation. Victory and failure panels link to map inspection or recovery choices.

Campaign settings include sound and music volume, reduced motion, resource icon labels, and simulation speed. Speed changes only the wall-clock pace. Research mode locks speed and other experiment settings to its run configuration. There are no campaign cheats or Easter eggs in the prototype; developer controls are separate from campaign progression.

### 5.14 Saving and replaying

Maintain one manual save and one automatic checkpoint. Create the initial checkpoint before the first campaign step, then replace it after each zone unlock. Manual saves occur at completed step boundaries. On application suspension, attempt to save the last completed step to the manual slot and pause the simulation. An incomplete step is never committed to the save.

Save the configuration version, scenario, random seed, tick, entity identifiers and states, next entity-ID allocator, water balances, currency, technology, zone unlocks, debt counter, stability counter, both community shortage and recovery counters, and pending action sequence. Rebuild the spatial index from canonical entities during loading. Do not store the quadtree as authoritative game state. Invalid or incompatible saves display a recovery message and must not be silently overwritten.

Restart uses the scenario's original data and seed. Research replays use saved input actions rather than live touch input. Their exact action sequence, event timing, and configuration remain constant across spatial methods.

## 6 Story and Narrative

### 6.1 Backstory and player role

Pocket Silica takes place in a fictional region seeking technological and economic development while maintaining household services and farming. The player acts as its infrastructure coordinator. No named political official, real company, or real community is simulated. The data center is a fictional game entity and does not assert what any actual development contains.

### 6.2 Story progression

The narrative follows four development episodes. The starting district establishes basic services. The second introduces pressure from denser technology growth. The third exposes the difficulty of maintaining multiple service areas. The fourth requires the whole region to remain stable together.

Short text briefings introduce each district. Contextual messages explain shortages, agricultural losses, milestones, and recovery. The campaign ends with a summary of the player's region. There are no branching dialogue trees, voiced characters, cinematic cutscenes, or moral-alignment system in the baseline.

## 7 Game World

### 7.1 Map and visual setting

The proposed map is a 1024 by 1024 unit square. The logical origin is the top-left corner, positive x points east, and positive y points south; rendering coordinates must map consistently to this convention. Its four 512 by 512 zones form a two-by-two arrangement. The northwest zone opens first, followed clockwise by northeast, southeast, and southwest. The placement grid has 32-unit cells with sites at their centers. Terrain tags identify buildable ground, intake sites, dam sites, and protected decorative river tiles.

The map is authored and saved as scenario data rather than generated during campaign play. Buildings, rivers, farms, and community groups use a readable top-down style. The camera pans and zooms over the same map without loading separate scenes between districts.

### 7.2 Initial conditions and expansion content

The first zone contains a community at (272, 240), a farm at (240, 272), a starter water facility at (240, 240), and a starter power plant at (272, 272). Its configured intake and dam sites appear in the scenario. No data center exists initially; the player constructs it on a free buildable site. The campaign configuration must prevent terrain tags from conflicting with these starting entities.

Each newly unlocked zone creates one community and exposes at least two water-intake sites and one dam site. Suggested community anchors are (784, 240), (784, 752), and (272, 752), following the expansion sequence. Utility facilities and farms in those zones must be constructed by the player. Candidate resource sites must allow all communities to receive both utilities within the chosen radii. Final terrain coordinates and protected tiles are an authored-map deliverable that must pass a solvability playtest before release.

### 7.3 Fog and regional responsibility

Fog hides locked-zone buildings and controls placement eligibility. Locked communities do not request resources, generate income, or protest. Inactive sources do not accumulate stored water before their zone opens. Unlocking initializes the new entities using scenario values. Previous zones continue consuming and producing resources.

The four campaign zones are independent of the quadtree. The spatial root covers the whole map from the beginning. A quadtree leaf divides when its configured entity capacity is exceeded, subject to its maximum depth or minimum-size limit. Subdivision may happen anywhere and repeatedly; it is not triggered by a level unlock, shortage, or frame-rate threshold.

## 8 Characters and Opponents

### 8.1 Player and communities

The player has no walking avatar. The map interface represents the infrastructure-coordinator role. Communities are non-playable groups that provide labor and household demand. Their visual appearance distinguishes ordinary residents, workers, and peaceful protest groups without requiring individually simulated agents.

Each community uses the same Normal and Protesting states defined in Section 5. The game displays its satisfaction, fulfilled needs, available workers, and protest reason. Workers do not have separate personalities, inventories, skills, or pathfinding. Facilities remain stationary after placement.

### 8.2 Opposition and artificial intelligence

The opposing pressures are insufficient supply, operating costs, limited coverage, and the demands introduced by expansion. There is no hostile faction or armed enemy. Protesters are residents expressing unmet service needs, not enemies to defeat.

NPC behavior is a deterministic state machine driven by recorded resource fulfillment and counters. Cosmetic animation cannot change resource allocation, workforce, or protest timing. Both spatial methods use identical NPC settings and state transitions.

## 9 Levels

### 9.1 Campaign structure

The campaign uses one persistent map with four stages. A stage is complete when the active region satisfies its milestone. Each later stage retains previous obligations and adds a community and development area. The same rules apply throughout; scenario layouts change the challenge.

| Stage | Area introduced | Gameplay emphasis | Initial technology target | Sustained condition |
| --- | --- | --- | --- | --- |
| 1 | Northwest | Read coverage and demand, establish the first data center, and protect starter agriculture. | 20 | Ten qualifying steps to unlock stage 2 |
| 2 | Northeast | Support another community and manage a denser development cluster. | 60 | Ten qualifying steps to unlock stage 3 |
| 3 | Southeast | Coordinate several sources and cross-border service areas. | 120 | Ten qualifying steps to unlock stage 4 |
| 4 | Southwest | Sustain all districts and complete the regional stability challenge. | 200 | Twenty qualifying steps for final victory |

The milestone conditions in Section 5 apply in addition to the technology targets. The campaign map should include meaningful density differences, but it must not be presented as the only research benchmark.

### 9.2 Tutorial and assessment

The tutorial teaches selection, coverage inspection, valid placement, time controls, resource warnings, workplace pausing, and the milestone panel. Hints explain the difference between lack of coverage and inadequate source capacity. Players can replay the tutorial from the main menu.

A stage summary reports its achieved conditions and opens the next briefing. Progress is assessed through recorded simulation values, not an external quiz. Players replay earlier stages by loading a checkpoint or restarting the campaign; there is no independent level-selection system in the baseline.

### 9.3 Research scenarios

Separate benchmark scenarios use evenly distributed entities, one dense cluster, and several clusters. They vary entity counts and query workloads without depending on a player's skill or campaign success. The researcher fixes layouts, seeds, source placements, build settings, and action lists before the main comparison. These scenarios do not unlock campaign rewards.

## 10 User Interface

### 10.1 Visual system and camera

The proposed presentation is landscape with a top-down orthographic camera. World panning and zooming are bounded to the map. The placement grid is a player aid and does not reveal which spatial index is active. Quadtree-cell visualization is a developer overlay, excluded from measured builds unless specifically part of a logged diagnostic run.

The HUD displays currency and net income, cumulative technology and current production, population and filled jobs, food adequacy, and satisfaction. Water and electricity show demand fulfillment and shortages, with district-level details available by selection. A regional water total is supplementary; it cannot imply that every district has access to that water.

### 10.2 Touch and desktop controls

| Action | Android control | Development equivalent |
| --- | --- | --- |
| Select a building or community | Tap | Left click |
| Pan the world | Drag on empty terrain | Drag on empty terrain |
| Zoom | Pinch | Mouse wheel |
| Choose a construction site | Tap a site while the preview is active | Left click a site |
| Confirm or cancel | Labeled panel buttons | Same buttons or Escape to cancel |
| Pause or change speed | HUD buttons | Same buttons |
| Open details or milestones | Labeled HUD or inspector buttons | Same buttons |

Do not assign essential commands exclusively to gestures. Placing a building requires an explicit confirmation button so a pan gesture cannot spend currency accidentally. Modal settings, construction previews, and confirmation panels pause campaign time.

### 10.3 Building panels and alerts

The inspector shows identifier, type, level, state, cost or upkeep, requested and supplied resources, staffing, output, and supplying facilities. Resource overlays show coverage boundaries and differentiate covered-but-short consumers from uncovered consumers. The construction preview displays added demand before confirmation.

Alerts identify the affected community, reason, duration, and available response. A protest alert explains the service deficit. A milestone panel lists each condition and the current consecutive-step counter. The debt panel shows actual balance, net income, and remaining grace steps.

### 10.4 Art and accessibility

Use consistent top-down building silhouettes and distinguish water, electricity, agriculture, and technology with icons and text as well as color. Selection outlines, clear type labels, readable numeric text, scalable interface elements, and large touch targets are required. Reduced motion disables nonessential pulsing and camera movement. Small labels should remain readable at the target device's normal display settings.

Art should portray a fictional region rather than imply a geographic reconstruction. Use original or appropriately licensed assets and record their licenses. Institution logos, if used in credits, require approved source files and appropriate institutional usage.

### 10.5 Audio and help

Optional background music and short sound cues support placement, warnings, milestones, and recovery. Audio is never the only signal. Music and effects have separate volume controls. The help panel explains resource units, operating fractions, shortage allocation, protest recovery, and milestone requirements. A glossary distinguishes technology, employment, capacity, coverage, and satisfaction.

## 11 Content Additions

Developers add buildings, balance profiles, and scenarios through version-controlled data files and asset references. The baseline has no in-game administrator editor, downloadable content store, or remote configuration service. Data validation rejects negative demands, duplicate identifiers, invalid coordinates, missing assets, impossible radii, and inconsistent version fields.

| Content | Thesis prototype baseline | Future extension |
| --- | --- | --- |
| Infrastructure growth | Player placement, one upgrade, and four permanent land expansions | Automatic urban growth, redevelopment, demolition, or relocation |
| Water and electricity | Fixed source capacities, water storage, local service areas | Pumping dependencies, transmission networks, water-quality or flow models |
| Population and agriculture | Community groups, shared workers, farms, and simple food adequacy | Individual mobility, migration, multiple crops, storage, or markets |
| Environmental factors | Fixed scenario conditions | Weather, climate change, natural calamities |
| Government projects | Excluded from the baseline | Flood-control and other public-project systems |
| Post-campaign play | Final summary and restart | Endless sandbox or additional scenarios |

Future environmental and government-project systems need explicit effects, units, geographic operations, and tests before inclusion. They must not change the frozen benchmark configuration midway through the research comparison.

## 12 Feedback for the Player

Every important consequence should be traceable to a visible rule. The game distinguishes out-of-range service, insufficient capacity, insufficient staffing, low agricultural output, and debt. A player should be able to identify which condition prevents a milestone without guessing.

Feedback follows three stages: a forecast before a construction decision, a warning when a deficit appears, and a recorded consequence if it persists. The source inspector explains connected demand and storage. The community inspector shows shortage and recovery counters. The final summary reports sustained performance, not a moral judgment of the player.

Example messages are: "Water coverage does not reach this farm," "Connected water demand exceeds current supply," "This community has had inadequate electricity for two steps," and "Services restored: two of three recovery steps completed." Messages use the same units and thresholds as the simulation.

## 13 Data Collection for the Administrator

### 13.1 Research mode and records

The administrator is the researcher operating a separate local test interface. Research mode selects a saved scenario, algorithm, configuration, seed, warm-up procedure, and recorded action sequence. It can start runs and export records. Research controls are hidden from ordinary campaign play and cannot unlock land or alter campaign saves.

| Record group | Minimum fields |
| --- | --- |
| Run identity | Run ID, build ID, configuration version, scenario ID, seed, action-file checksum, algorithm, run order |
| Environment | Device model, operating system, graphics settings, frame cap, timing method, profiler configuration |
| Workload | Logical step, entity count, source and query counts, entity layout, index settings, action sequence |
| Performance | Spatial-query time, simulation-update time, measured frame performance, supported memory measure |
| Index diagnostics | Build or insertion time when available, quadtree node or leaf counts and depth, grid-cell settings |
| Correctness | Expected and returned IDs, allocations, resource balances, protest transitions, pass or fail and tolerance |
| Run validity | Loading or warm-up exclusion, interruptions, crash status, excluded interval and reason |

Save logs locally in a structured format such as CSV, with configuration and scenario manifests in JSON. Export must identify units. Processing time is in milliseconds; frame measures distinguish FPS from frame duration. Memory records must name the profiler measure instead of presenting an unspecified total.

### 13.2 Fair comparison and correctness

The quadtree and uniform grid must receive identical entity records, source service areas, resource rules, NPC logic, event timing, seeds, and actions. Rendering, device settings, build type, and measurement procedures remain constant within each paired comparison. Shared simulation code calls the chosen spatial interface; changing the index must not change intended outcomes.

Check query results against an independent direct scan for small cases. Check water, electricity, food, finances, and protest transitions against known expected values. Agreement between the two indices alone is insufficient because both could share a defect. Compare identifiers exactly and use a declared numeric tolerance for fractional outputs.

Required cases include an empty map, one consumer, repeated positions, map and service boundaries, overlapping sources, insufficient resources, inactive buildings, source upgrades, zone unlocking, protest entry and recovery, and save/load replay. A small allocation example with requests of 6 and 4 against 5 available units must allocate 3 and 2 under the proportional rule.

The original thesis specifies 20 runs of 60 measured seconds per implementation and scenario, excluding loading, and a technical review by 50 qualified evaluators. These are the paper's planned settings. The adviser-approved final protocol must confirm feasibility, warm-up, scenario counts, device controls, and any amendments before collection. Alternate or randomize algorithm run order and preserve interruptions and rerun reasons.

### 13.3 Evaluator information and privacy

Technical evaluators use a checklist tied to required functions and can provide comments. Use participant codes in analysis and keep consent records separately. Do not require player names, account registration, location tracking, or online telemetry for campaign play. Store research files and evaluator feedback locally under researcher-controlled access and follow the institution's agreed retention policy.

This design collects evidence about performance and specified functions. It does not add a learning-outcome, public-opinion, or enjoyment study. Any additional human-subject evaluation requires a matching protocol and consent process.

### 13.4 Statistical treatment of data

The recommended primary analysis is descriptive, organized by spatial method, entity count, and layout. Predeclare complete simulation-update time per logical step in milliseconds as the primary performance measure, including spatial-index maintenance and queries. Query-only time, frame performance, and a clearly named memory measure are secondary outcomes. These measures are reported separately rather than combined into a weighted score.

Each 60-second benchmark run supplies one summary for each measure. Calculate the mean update time within a run, then report the mean and sample standard deviation of those run summaries. Also report median and interquartile range to describe skewness or long tails. Average FPS for a run is the number of rendered frames divided by the measured elapsed time; do not substitute the average of instantaneous FPS readings. A 95th-percentile frame duration can describe occasional slow frames. Select the memory measure and units before collection, such as peak managed-memory use in MB, and use the same definition for both methods.

| Evidence | Recommended treatment | Interpretation |
| --- | --- | --- |
| Update and query times, frame performance, and memory | Per-run summaries followed by mean and sample standard deviation; median and interquartile range as supporting summaries | Typical performance and measured variability for each workload condition |
| Quadtree versus grid performance | Matched absolute differences and percentage change, with confidence intervals when the experimental design supports them | Magnitude and uncertainty of the performance difference |
| Correctness cases | Passed and failed counts, attempted-case denominator, pass percentage, unexecuted cases, and failure descriptions | Compliance with predefined expected answers |
| Technical evaluation checklist | Item-level frequencies and percentages for Met, Partly met, Not met, and Not observed | Which required functions evaluators could verify |
| Written evaluator comments | Group comments by recurring issue and retain important disagreements | Specific defects or improvement needs |

For runtime, calculate a pair's percentage improvement as grid time minus quadtree time, divided by grid time, multiplied by 100. Positive values indicate a time reduction; negative values indicate a slowdown. State whether the report summarizes pair-level percentages or calculates a percentage from aggregated times. Do not report a percentage where the baseline is zero. Relate the difference to the application's update and frame budget so that a small p-value is not mistaken for a useful improvement.

Frame and tick observations inside a run are not separate independent experiments. Twenty repetitions of one saved map characterize execution variation for that map, device, and build; they do not create twenty independently sampled maps. To support comparisons across maps, generate and save several independent layout instances within each layout-by-entity-count condition. Run both methods on every input, balance or randomize order, and summarize repeated executions within each input before comparing the paired input-level summaries. If only one map per condition is used, keep conclusions conditional on those fixed cases.

Inferential testing is optional and must be specified before the main comparison. With independent paired inputs and suitably behaved paired differences, a two-sided paired t-test at the 0.05 level can assess the mean difference, accompanied by a 95 percent confidence interval. Assess the distribution of the paired differences, not just each method's raw values. A Wilcoxon signed-rank test is an alternative only when its assumptions, including approximate symmetry and independence of the paired differences, are reasonable. If these conditions are unsupported, report the descriptive results and obtain an appropriate revised analysis plan rather than automatically switching tests. Predefine any family of confirmatory comparisons and its multiple-testing adjustment before examining results.

For correctness, compare exact identifiers and declared numeric tolerances against independent expected answers. Report unexecuted cases separately and resolve failed required cases before accepting the benchmark build. A high average pass percentage does not excuse a failure in a required rule. Invalid, interrupted, or crashed benchmark runs are documented with their reasons and rerun policy; inconvenient results are not silently removed.

For evaluator responses, state invited and participating counts and each item's valid-response denominator. Keep Not observed and missing responses visible. If reporting the proportion rated Met among observed responses, identify that denominator explicitly. Do not automatically assign equally spaced numerical weights or compute a mean for these categorical judgments. Purposively selected technical evaluators support a functional review of the prototype, not population-wide claims about all players.

The presentation's Slide 11 mentions GUESS, while its Slide 8 and the thesis scope exclude enjoyment and UX assessment. The baseline therefore retains the technical checklist. Adding a satisfaction instrument would require consistent objectives, scope, instruments, consent, and a separate scoring and analysis plan; its results should not be merged with benchmark timings.

This recommendation draws on the NIST guidance on paired observations, measures of scale, and signed-rank assumptions, and on Kalibera and Jones's work on benchmark uncertainty. Their links are provided in Section 15.6. The study must select and record its final plan before collecting confirmatory data.

## 14 Deployment

### 14.1 Target and installation

The planned delivery is an offline Android application supplied as an installable APK for thesis demonstrations and technical evaluation. Public app-store publication is outside this prototype. A release package should include the APK, build identifier, installation instructions, configuration manifest, and known-device record. No user account or server is required for ordinary play.

The thesis identifies a Xiaomi POCO X7 Pro with Android 16, a Dimensity 8400 processor, and 8 GB RAM as its evaluation environment. These are thesis-declared test-device details, not validated minimum requirements. Minimum supported Android version, screen sizes, storage footprint, and supported devices must be established through actual builds and recorded testing.

### 14.2 Rebuilding and configuration

Obtain the project revision from the project repository, install the recorded Unity editor and Android build modules, restore the package versions in the project manifests, open the project, select the documented startup scene, and build the Android target using the release instructions. Exact scene names, editor patch version, scripting backend, graphics API, and package versions belong in the verified build record before handover.

Campaign and benchmark configuration files are packaged with the build. Research exports use the application's local persistent-data area and an explicit export action. Save failures, low storage, missing configuration, and incompatible files produce a readable error without deleting the last valid save. Signing credentials, access tokens, and passwords must not be placed in this GDD or the public repository.

## 15 Development

### 15.1 Platform and project source

The thesis names Unity 6.6 and C# for development. This GDD preserves that declared choice; the exact installed editor release and its availability have not been independently verified here. Confirm the full editor identifier and record it in the project build manifest before implementation and handover. Record Android SDK and JDK versions, render pipeline, input system, profiler tools, and all third-party dependencies from the actual project.

The current project repository is [packet-silica](https://github.com/iHoshiii/packet-silica). The repository location is known, but a complete game codebase or verified implementation is not asserted. Documentation is stored under `docs/`. A Unity implementation should use a documented project root and a checked-in folder guide so the next developer can locate scenes, scripts, assets, configurations, tests, and research tools.

### 15.2 Software structure

Separate the interface, simulation state and rules, spatial index, persistence, and research logger. The canonical entity registry owns identifiers and state. An interchangeable spatial interface supports construction, insertion, and service-area queries. Pausing and upgrading preserve position and identifiers. Save/load reconstructs the index from canonical entities.

The quadtree and uniform grid use the same map bounds and point-in-service-area test. Quadtree capacity, maximum depth, and minimum cell size, along with grid cell size, are configurable experiment parameters selected during the pilot. Do not choose different settings for individual scenarios after inspecting which method wins. Boundary ownership and maximum-depth behavior require explicit tests.

Use stable identifiers, deterministic event order, and consistent numeric operations. Keep animation and visual NPC groups separate from authoritative simulation. If moving agents, deletion, or relocation are added later, both indices must implement equivalent updates and their costs must be included in the experiment.

### 15.3 Implementation and acceptance sequence

First implement the canonical entities, step order, independent resource calculations, and known-answer tests. Next add one playable zone, placement, pausing, and resource feedback. Then add economy, farms, staffing, protests, progression, persistence, and the remaining zones. Add the alternative index and replay tools through the shared spatial interface, then verify equivalence and profile representative workloads.

Before formal evaluation, fix correctness failures, complete a pilot, freeze the configuration and build, and preserve scenario files and actions. A performance comparison cannot compensate for incorrect allocation or protest logic. The delivered prototype is accepted when it supports the four-zone campaign, the stated win and failure states, save/load, correct resource and NPC responses, and repeatable quadtree/grid runs with usable exports.

### 15.4 Development schedule

| Period | Planned work |
| --- | --- |
| July to August 2026 | Research and literature review |
| August to October 2026 | Proposal preparation and methodology |
| November 2026 | Proposal defense, revisions, and approval |
| December 2026 | System and algorithm design after proposal approval |
| December 2026 to March 2027 | Game development and refinement, targeting feature completion in early March |
| January to March 2027 | Internal testing and bug fixing during development |
| Early March 2027 | Pilot testing and benchmark setup |
| Mid to late March 2027 | Benchmarking and technical evaluation |
| Late March to early April 2027 | Analysis and results writing |
| April 2027 | Manuscript completion, final defense, corrections, and submission |

Documentation and adviser consultations continue throughout. March testing activities proceed in sequence after a stable build is ready. Exact defense dates remain subject to institutional scheduling.

### 15.5 Decisions and implementation status

| Decision | Version 0.1 position | Required confirmation |
| --- | --- | --- |
| Research emphasis | Water conflict, supporting electricity, and quadtree/grid evaluation | Align objectives, scope, instruments, and tests |
| Protest cause | Persistent water or electricity shortage | Resolve the original objective's water-only wording |
| Balance profile | Initial defaults in Section 5 | Playtest costs, production, thresholds, and recovery |
| World map | Four authored zones and a placement grid | Complete terrain/site coordinates and demonstrate solvability |
| Team and adviser | Full team and adviser names supplied by the presentation | Assign individual production roles and confirm review responsibilities |
| Engine and device | Thesis-declared Unity and Android environment | Record actual editor, dependencies, device, and minimum support |
| Delivered build | Planned prototype specification | Add release ID, date, implemented features, and known limitations after verification |
| Research settings | Original planned run and evaluator counts retained | Confirm the final adviser-approved protocol before data collection |
| Evaluation scope | Technical correctness and performance retained | Resolve the presentation's GUESS reference against the stated exclusion of UX and enjoyment |

### 15.6 Sources and design basis

The section order follows the University of North Carolina's [Serious Game Design Document Outline](https://wwwx.cs.unc.edu/~pozefsky/seriousgames/NewDesignDocTemplate.pdf). The game-specific specification is original to this project.

Project sources are `gooding.docx` (objectives, scope, environment, methods, and testing) and `Thesis Presentation_ Pocket Silica.pptx` (team and adviser on Slide 1; tools and protocol on Slides 10 to 12). Slide 13 contains only a statistical-treatment heading. The companion `Pocket_Silica_revised_text.md` proposes service-area, allocation, and reproducibility details; it does not replace the original manuscript.

Design discussions establish the campaign, economy, agriculture, technology, workforce, satisfaction goal, future factors, and schedule. Detailed formulas, balance values, persistence, milestones, and endgame rules remain proposed specifications for review and pilot testing. Implementation status is recorded in Section 15.5.

Statistical references are [NIST Analysis of paired observations](https://www.itl.nist.gov/div898/handbook/prc/section3/prc311.htm), [NIST Measures of Scale](https://www.itl.nist.gov/div898/handbook/eda/section3/eda356.htm), [NIST Signed Rank Test](https://www.itl.nist.gov/div898/software/dataplot/refman1/auxillar/signrank.htm), and Kalibera and Jones (2013), [Rigorous Benchmarking in Reasonable Time](https://kar.kent.ac.uk/33611/).
