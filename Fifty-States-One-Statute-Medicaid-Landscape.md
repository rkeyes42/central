# Fifty States, One Statute

## How American Medicaid Programs Resemble One Another, How They Differ, and How Health Plans and State Agencies Actually Work Together

*A companion document to the Central series of healthcare data demonstration applications.*

---

## Introduction: One Statute, Fifty-Some Programs

Medicaid is a single federal statute — Title XIX of the Social Security Act — implemented as more than fifty distinct programs: fifty states, the District of Columbia, and five territories, each running its own eligibility rules, benefit package, delivery system, payment methods, data systems, and vocabulary, inside a federal frame that guarantees certain things everywhere and leaves an astonishing amount to state choice.

This is why a Medicaid data professional can move between states and find the 834 transaction, the coverage-group concept, and the eligibility span waiting in every one of them — and simultaneously find that the words mean different things, the delivery architecture is unrecognizable, and a record shape that was routine in one state is impossible in the next. Texas has no expansion group at all; Vermont has almost no health plans at all; in Utah the word "ACO" means a capitated MCO; in Colorado nobody is "enrolled" in the regional entities so much as attributed to them. Same statute. Different worlds.

This document maps that terrain in four parts: what is the same everywhere (the federal chassis); the axes along which states diverge; how health plans and state Medicaid agencies actually work together, end to end; and a fifty-state gazetteer. A closing section indexes the Central series applications against the map.

Program facts reflect the public record of the mid-2020s. Medicaid changes constantly — expansion status, plan rosters, waiver terms, and procurement outcomes all move year to year — so verify anything load-bearing against current CMS and state agency publications before relying on it.

---

## Part I — The Federal Chassis: What Is the Same Everywhere

Beneath fifty different paint jobs sits one chassis. These elements are federal requirements or near-universal conventions, and they are the reason Medicaid experience transfers between states at all.

**An individual entitlement with matched financing.** Medicaid is an entitlement: every person who meets a state's eligibility rules must be covered, with no enrollment cap and no waiting list for the state plan itself (waiver services can have waiting lists — an important asterisk covered later). The federal government matches state spending at the FMAP — the Federal Medical Assistance Percentage — which floats by state per-capita income from 50% to the high 70s, with a fixed 90% match for the ACA expansion group everywhere. The match structure explains an enormous amount of state behavior: every eligibility decision, benefit decision, and payment decision is a shared-dollar decision.

**A mandatory eligibility floor.** Every state must cover certain groups: poverty-related children (with federal minimum income thresholds by age band), pregnant women to at least 138% FPL, parents at the state's (often very low) historical welfare-linked level, SSI recipients in most states, and certain Medicare Savings Program populations. Every state must also cover former foster youth to age 26. Above the floor, everything is state option — which is where Part II begins.

**MAGI methodology for most of the program.** Since 2014, financial eligibility for children, pregnant women, parents, and expansion adults uses Modified Adjusted Gross Income — a single national income methodology with no asset test — determined against uniform household-composition rules. The aged, blind, and disabled pathways ("non-MAGI") still use the older SSI-derived budgeting, with asset tests in almost every state (California's elimination of the non-MAGI asset test is the famous exception). Every state therefore runs two determination worlds side by side, and every state's data model carries the MAGI/non-MAGI distinction somewhere.

**A mandatory benefit floor, and EPSDT above everything.** Inpatient and outpatient hospital care, physician services, lab and X-ray, home health, nursing facility care for adults, family planning, FQHC/RHC services, and transportation to care are mandatory everywhere. For children, EPSDT — Early and Periodic Screening, Diagnostic and Treatment — overrides state benefit limits entirely: any medically necessary service coverable under federal Medicaid law must be provided to a child, whether or not the state covers it for adults. EPSDT makes every state's child benefit package effectively identical in legal scope, however different the adult packages are.

**Single state agency, due process, and statewideness (with waiver exceptions).** Federal law requires one designated single state agency, fair-hearing rights before adverse action, comparability of benefits within groups, and statewide operation — each of which can be, and constantly is, waived under Section 1115 or 1915 authority. Nevada's two-county managed care map and California's county-by-county delivery models both exist inside waived statewideness.

**Retroactive eligibility, by default.** The statute's default grants eligibility up to three months before the application month if the person would have qualified — the "two clocks" phenomenon every eligibility system must model, since eligibility runs backward while plan enrollment only runs forward. A growing set of states has waived retro down to the application month for some or all adults (Utah, Iowa, Florida for some groups, New Hampshire's expansion population, and others), which is a difference catalogued in Part II — but the default, and the data shape it creates, is universal.

**Third-party liability: Medicaid pays last.** Everywhere, Medicaid is the payer of last resort. Employer coverage, Medicare, casualty settlements, and union trust funds all pay first, and every state runs cost-avoidance and pay-and-chase machinery to enforce it. The TPL segment — the data that changes no dates and no eligibility, only who pays first — exists in every state's files.

**The dual-eligible architecture.** In every state, Medicare is primary for people who have both programs; Medicaid wraps. Every state operates the Medicare Savings Programs (QMB, SLMB, QI) and the buy-in exchange with CMS — the accretion/deletion premium file that is, for MSP-only members, the entire substance of their coverage. What differs (Part II) is how aggressively the state integrates the two programs above that floor.

**Data and transaction standards.** HIPAA's adopted X12N transactions are national: the 834 for enrollment, the 820 for capitation premium payment, the 837 for claims and encounters, the 270/271 for eligibility inquiry, the 835 for remittance. Every state operates a CMS-certified MMIS (Medicaid Management Information System), reports person-level data to T-MSIS, and assigns a permanent member identifier that survives gaps, moves, and category changes. The identifiers differ in format and name — CIN in both New York and California (different formats, same acronym, a collision the Central series enjoys), RID, Medicaid ID — but the concept is universal: the person, permanently, through everything.

**The eligibility span itself.** Finally, and most fundamentally for data work: every state expresses coverage as spans — a coverage group held over a date range, opened by a determination, closed for a reason. The span is the atom of Medicaid data in all fifty states. Everything in Part II is a statement about what the spans can contain and what runs alongside them.

---

## Part II — The Axes of Difference

State programs do not differ randomly; they differ along a manageable set of axes. Any state can be located by its position on each.

### Axis 1: Expansion status — the existence of the adult group

The single largest eligibility difference is whether the ACA adult expansion group (19–64, to 138% FPL, at the 90% federal match) exists at all. As of mid-2025, forty states plus DC have adopted it; ten have not: Alabama, Florida, Georgia, Kansas, Mississippi, South Carolina, Tennessee, Texas, Wisconsin, and Wyoming. In non-expansion states, a non-disabled childless adult generally cannot qualify regardless of income, and parent thresholds sit brutally low — roughly 15–20% FPL in Texas and Alabama — creating the coverage gap: people over the Medicaid line but under the marketplace subsidy floor.

The expansion axis has texture beyond yes/no. Wisconsin is non-expansion but has no gap, covering all adults to 100% FPL under waiver at the regular match — the only state in that position. Georgia runs Pathways to Coverage, a limited expansion to 100% FPL conditioned on qualifying work or engagement activities. Several states expanded only after ballot initiatives forced the question (Maine, Idaho, Nebraska, Utah, Oklahoma, Missouri, South Dakota), and Utah's version came with the full saga — voter initiative, legislative rewrite, CMS repricing, statutory fallback — legible in its group codes to this day. Arkansas expanded through premium assistance, buying marketplace qualified health plans for its expansion adults rather than enrolling them in Medicaid MCOs. Montana attached premiums and launched through a commercial third-party administrator. Indiana built POWER accounts — consumer-directed contribution accounts — into its expansion. The expansion group is one federal object with a dozen state personalities.

### Axis 2: Delivery architecture — the spectrum from all-FFS to all-in capitation

This is the axis the Central series works hardest, because it determines what the delivery span table can even contain. The spectrum, roughly:

**All fee-for-service.** The state pays every claim directly; there are no comprehensive plans. Alabama (with the ACHN care-coordination overlay), Alaska, Wyoming, Maine, Montana, South Dakota, and Connecticut (which famously terminated its MCO contracts in 2012 and returned to self-insured managed FFS with administrative services organizations — the state that fired its plans). Vermont belongs here in effect but by an entirely different route: the Global Commitment waiver makes the state itself operate as the public managed care entity — the state is the plan.

**PCCM and attribution overlays.** Fee-for-service claims with a coordination structure on top: primary care case management entities or regional accountable entities earning per-member-month fees without claim risk. Idaho's Healthy Connections, Alabama's ACHN, and — in a more evolved form — Colorado's Accountable Care Collaborative, whose Regional Accountable Entities carry attribution for everyone and a behavioral capitation, while physical claims stay largely FFS. Oklahoma ran this model (SoonerCare Choice) for twenty-five years before its 2024 big-bang conversion to capitation.

**Partial or geographic MCO.** Comprehensive plans for some populations or some places. Nevada's city limit (MCOs in Clark and Washoe only); Mississippi's MississippiCAN (managed care for some groups, FFS for others); Georgia's CMOs (families and children in plans, ABD largely FFS); North Dakota (one plan for the expansion population, FFS for traditional).

**Statewide comprehensive MCO.** The modal American arrangement: most or all populations in full-risk plans statewide. Most expansion states with mature programs live here — Ohio, Michigan, Illinois, Louisiana, Kentucky, Washington, Virginia, New Jersey, Pennsylvania, Maryland, New Hampshire, Nebraska, West Virginia, and many more.

**All-in capitation including LTSS.** The far pole: essentially everything, including long-term services and supports, inside capitation. Arizona — born capitated in 1982, the last state in and the only one that never built a legacy FFS system, with ALTCS covering nursing facilities and HCBS under capitation since 1989. Tennessee — the first state to move everyone into MCOs at once (1994) and home of CHOICES MLTSS. Kansas (KanCare), Hawaii (QUEST Integration), New Mexico (Turquoise Care), Florida (SMMC, comprehensive plus long-term care), Delaware, New Jersey, and Texas's STAR+PLUS all put LTSS at risk.

**Sui generis models.** Oregon's Coordinated Care Organizations: regional, community-governed entities under global budgets with sustainable-rate-of-growth targets and health-related-services flexibility — capitation with a public-utility temperament. Vermont's state-as-plan. North Carolina's 2021 transformation, notable for building Tailored Plans — specialty managed care for serious behavioral health and I/DD populations — beside its Standard Plans. Massachusetts's 2018 restructuring around MCO-administered and provider-led ACO partnerships.

Two structural notes cut across the spectrum. First, provider-integrated plans — insurers owned by health systems — are a recurring species: Intermountain's SelectHealth in Utah, UnitedHealth's Health Plan of Nevada (which owns the valley's largest medical group), University of Utah's Healthy U, county-created public plans like L.A. Care and IEHP in California (the Two-Plan model's Local Initiatives, the largest publicly operated plans in the nation), CalOptima and the other California COHS plans, Denver Health's plan in Colorado, Presbyterian in New Mexico, CareSource's Ohio roots, Parkland and Cook Children's plans in Texas. Second, no state's architecture is finished: Oklahoma converted in 2024, Florida re-procured into SMMC 3.0 in 2025, North Carolina transformed in 2021–2024, and Nevada's statewide expansion has been on the policy calendar — the map is a snapshot, always.

### Axis 3: Geography inside the state

Even settled architectures vary by county line. California is the extreme case: three concurrent models assigned by county — COHS counties (one public plan, everyone, automatically, zero choice), Two-Plan counties (a public Local Initiative versus one commercial), GMC counties (a genuine menu) — so the same program offers zero options in San Mateo, two in Los Angeles, and four in Sacramento. Nevada's urban/rural split turns capitation on and off at a county line. Texas and Florida run plan competition by service region; New York's plan rosters differ borough by borough and county by county; Wisconsin's and Minnesota's rural counties have seen single-plan and county-based-purchasing arrangements. The data lesson is constant: in Medicaid, the address is frequently the single most consequential field in the file.

### Axis 4: Carve-outs — what the capitation does not contain

A "comprehensive" plan almost never covers everything; states carve benefits out of the capitation and run them separately, and the carve map differs everywhere.

**Behavioral health** is the great carve-out story. Some states carve it to county government: Utah's PMHPs (the county mental health authorities as capitated payers — the state that kept the split on purpose), Pennsylvania's Behavioral HealthChoices (counties hold right of first opportunity and typically contract a BH-MCO), California's county mental health plans for specialty behavioral health, Michigan's regional PIHPs. Others carve it to a statewide vendor (Idaho's behavioral plan), or to specialty plans for defined populations (Ohio's OhioRISE for children with complex needs; North Carolina's Tailored Plans; Arkansas's PASSEs for BH and I/DD). And a whole cohort spent the last decade carving behavioral health back in: Washington's 2016–2020 integrated purchasing is the canonical example, Colorado's RAEs and New York's HARPs are cousins. Whether the seam between physical and behavioral payment runs through a member's record — and who sits on the far side of it — is one of the fastest ways to characterize a state.

**Pharmacy** has been moving the other direction: several states have carved pharmacy out of managed care into a single state-run or single-PBM arrangement — California's Medi-Cal Rx (2022), New York's NYRx (2023), West Virginia, Missouri, Wisconsin's long-standing FFS pharmacy, and Ohio's single PBM operating inside its managed care program. **Dental** is frequently delegated to specialized administrators. **Non-emergency medical transportation** commonly runs through statewide brokers. Every carve-out multiplies the enrollment streams, the coordination protocols, and the reconciliation work — the two-roster problem generalizes to an N-roster problem.

### Axis 5: LTSS strategy

Long-term services and supports is where state philosophies diverge most expensively. The poles: Arizona, where even the nursing homes have never billed state fee-for-service, versus Alabama, where even the nursing homes are gray. Between them: MLTSS states (managed LTSS — Tennessee CHOICES, Texas STAR+PLUS, Florida LTC, Kansas, New Jersey, Delaware, New Mexico, Hawaii, New York's MLTC partial-capitation model where the plan is at risk for LTSS only while Medicare stays primary); FFS-waiver states running 1915(c) home-and-community-based waivers with capped slots and waiting lists (the one place the entitlement genuinely queues — Washington's and Florida's waitlist registers in the Central series); self-direction programs where the member is the employer of record (Wisconsin's IRIS, New Mexico's Mini Community Benefit, most states in some form); and transition machinery (Money Follows the Person everywhere, under local names like Alabama's ACT). New Hampshire adds the county wrinkle: county governments share the non-federal cost of nursing home care and operate county homes.

### Axis 6: Eligibility generosity and the non-MAGI rules

Above the federal floor, states choose: children's upper limits (from near-minimum to 300%+ FPL counting CHIP), pregnancy limits, twelve-month postpartum (now adopted nearly everywhere), whether a medically-needy spend-down pathway exists (New York's is central; many states have none), 217-like special income rules for institutional care, and — the quiet revolution — asset-test policy, where California abolished the non-MAGI asset test outright. Family-planning-only programs (Alabama's Plan First is among the oldest and largest) create the sliver-benefit record: spans that look like coverage and pay for one service line. Continuous-eligibility policy is a new frontier: multi-year continuous eligibility for young children (Oregon to age six, with Washington and others following) and Oregon's two-year adult continuous eligibility change what churn even looks like in the data. And the states waiving retroactive eligibility down to the application month (Utah broadly; several others for expansion or waiver populations) shrink the classic reach-back to nearly nothing.

### Axis 7: The 1115 waiver personality

Nearly every ambitious state feature lives inside a Section 1115 demonstration, and the waiver portfolio is a fingerprint: Vermont's Global Commitment (the state as plan), Oregon's CCO waiver (global budgets, health-related services, continuous eligibility), Rhode Island's global compact, Tennessee's aggregate-cap financing demonstration, Arizona's original statewide capitation waiver, California's CalAIM (Community Supports — housing deposits, medically tailored meals, asthma remediation as plan-paid services with no CPT ancestry), Massachusetts's and North Carolina's delivery-reform waivers, Arkansas's premium assistance, Indiana's HIP, Georgia's Pathways, Montana's HELP. Reading a state's 1115 special terms and conditions is the fastest way to learn what makes its data strange.

### Axis 8: Who determines eligibility, and on what

The single state agency requirement conceals real administrative diversity. About ten states are county-administered — California (58 county welfare departments on CalSAWS), New York (local districts), Colorado, Minnesota, New Jersey, North Carolina, Ohio, Pennsylvania, Virginia, Wisconsin — meaning the determination workforce belongs to county government. Some states put eligibility in the human-services or workforce agency rather than the health agency: Utah's Department of Workforce Services, Nevada's Division of Welfare and Supportive Services. Agency mergers and renames are their own data event — Utah's DHHS (2022), New Mexico's Health Care Authority (2024), the perennial lesson that identifiers need effective dates. Each state runs one integrated eligibility system (and their consolidations — three legacy systems into CalSAWS — are decade-scale projects), plus the CMS-certified MMIS, increasingly built as modules run by different vendors.

### Axis 9: Branding and vocabulary

Not trivial, because the words are the interface: Medi-Cal, MassHealth, TennCare, SoonerCare, BadgerCare, Husky Health, Apple Health, MaineCare, KanCare, Health First Colorado, Med-QUEST, Turquoise Care, Cardinal Care, Green Mountain Care. Plans are called MCOs, ACOs (Utah — full-risk plans, not Medicare's attribution animal), CCOs (Oregon), CMOs (Georgia), PASSEs (Arkansas), RAEs (Colorado), PIHPs (Michigan). The same three letters mean different things across programs; the same concept wears five names. A concept crosswalk is not a nicety in this field — it is infrastructure.

### Axis 10: The duals strategy

Above the universal wrap-and-buy-in floor, states choose how hard to integrate Medicare and Medicaid: aligned D-SNP policies (California's matching rule — the D-SNP must share the Medi-Cal plan's parent, alignment by statute; exclusively aligned arrangements in COHS counties), FIDE-SNPs (Minnesota's MSHO is the elder statesman, running since the 1990s; Massachusetts, New Jersey), the financial-alignment MMP demonstrations (concluded at the end of 2025, transitioning members to integrated D-SNPs in Ohio, Michigan, Illinois, Texas, and others), default enrollment, or simply letting the FFS wrap and the D-SNP market coexist. The Central series' running catalog of "what happens in the data when Medicare arrives" — sixteen different answers across sixteen states, from the loud unwind to the perfect stillness to the answer that depends on which county you are standing in — is really this axis, observed from the member record.

---

## Part III — How Plans and State Medicaid Work Together

Where managed care exists, the state–plan relationship is a long, structured, deeply data-mediated partnership. It has a lifecycle, a money flow, a data flow, and an accountability apparatus, and they look remarkably similar across states even when everything else differs.

### The lifecycle: procure, contract, ready, operate, re-procure

It begins with **procurement**: the state issues an RFP for a defined program, population, and region set; plans bid; awards land; protests frequently follow (procurement litigation is a genre of its own); and contracts run roughly three to five years with renewals. Re-procurement is the periodic earthquake — plans exit, plans enter, and hundreds of thousands of members transition on a single effective date. New Mexico's 2019 and 2024 cycles, Ohio's Next Generation awards, and Florida's SMMC 3.0 (with plan exits, successor mappings, and a region renumbering, all visible in member data) are the pattern. A canceled procurement leaves ghosts: Alabama's RCOs were legislated, certified, funded, and canceled in 2017 before a single member-month was paid, and probationary assignment codes still sit in archives — schemas outlive policies.

Before go-live, plans pass **readiness review**: systems testing (can the plan consume the 834 and return encounters), network adequacy demonstration, staffing, and call-center capacity. Then operations begin, and the relationship becomes a set of recurring files and meetings for years at a stretch.

### The money: capitation, rate cells, and the actuarial frame

The state pays each plan a **capitation** — a per-member-per-month amount — in exchange for the plan bearing the cost of covered services. Rates are set in **rate cells**: the cross of eligibility category, age band, sex, region, and sometimes institutional or waiver status, each cell separately priced (Hawaii's island-by-island cells are the geography made explicit). Federal rules require rates to be **actuarially sound** — certified as reasonable, appropriate, and attainable — and modern rules add a **medical loss ratio** expectation around 85%, with remittances when plans underspend. Rates are frequently **risk-adjusted** by member health status using diagnosis-based models, so the encounter data plans submit literally prices their future revenue — one of several reasons encounter completeness is a perpetual battleground.

Layered on the base capitation: **withholds** tied to quality performance; **risk corridors** sharing gain and loss in bands around the target; **state directed payments** through which states require plans to pay certain providers in certain ways (minimum fee schedules, uniform increases, value-based arrangements) — an increasingly large share of the dollars; **maternity kick payments** and similar event-based supplements; and **reinsurance or stop-loss** for catastrophic cases. In partial-capitation models the deal is explicitly narrower: New York's MLTC plans are at risk for long-term services only. In PCCM and attribution models there is no claim risk at all — the ACHN or RAE earns a coordination fee over an FFS spine, the same 834 grammar carrying a categorically smaller promise.

The payment itself moves on the **820** transaction — the premium payment order that must reconcile, member by member and month by month, against the enrollment file. Retroactive enrollment changes generate capitation adjustments and recoupments; a member disenrolled back three months is three months of capitation clawed back, which is why plans read the 834's date segments with such attention.

### The data: the enrollment stream, the encounter stream, and everything between

**Enrollment (834).** The state is the source of truth for who is enrolled; plans hold a copy. States send daily or weekly change files and periodic full audit files; plans reconcile and dispute. The maintenance codes are a tiny vocabulary (additions, terminations, changes) carrying enormous variety: auto-assignment when a choice window closes unanswered; the county-line termination cut for a member who lost nothing and chose nothing; the conversion wave where hundreds of thousands of members already known to the state arrive at plans as "new" enrollees and stress every duplicate-matching routine; the Medicare-entitlement termination that fires in one stream while a county behavioral stream stays silent. Enrollment runs prospectively from the first of a month, while eligibility can run backward — the two clocks — so FFS tails precede plan pickup in most states, except where retro has been waived nearly away.

**Choice and assignment.** Where members have a choice, the state runs the choice window and an **auto-assignment algorithm** for non-responders — typically weighted by prior plan relationships, family alignment, provider relationships, plan quality, and market-share balancing. Where members have no choice — COHS counties, single-plan regions — enrollment is automatic and the packet never exists. Plan-change rights (an initial switch period, annual open enrollment, for-cause changes anytime) generate the routine plan-to-plan transitions that dominate register D of nearly every Central app.

**Encounters (837).** Plans must report every service they pay as an encounter — a claim-shaped record with no payment obligation attached — and states validate volume, completeness, and quality against contractual thresholds with financial penalties behind them. Encounters feed rate setting, risk adjustment, quality measurement, program integrity, and T-MSIS: the state's visibility into a capitated program is exactly as good as its encounter data, which is why encounter quality clauses have real teeth.

**Coordination files.** TPL and coordination-of-benefits data flow both directions (the state's data matches discover employer coverage; plans discover it at the point of service; pay-and-chase recoveries run backward). Carve-out coordination requires crossover protocols — the crisis episode where the emergency department bills the physical payer while the mobile crisis team bills the county authority. Duals generate the buy-in exchange with CMS and, in aligned models, enrollment coordination with the D-SNP side of the same parent company.

### The accountability apparatus

States oversee plans through **network adequacy** standards (time/distance, appointment availability, secret-shopper surveys); **quality measurement** (HEDIS submissions, CAHPS surveys, state dashboards, withhold scoring); an annual **External Quality Review** by an independent EQRO; **grievance and appeal** systems with state fair hearings above plan-level appeals; **program integrity** obligations mirrored down into plan SIUs; and a sanctions ladder from corrective action plans through liquidated damages, enrollment freezes, and (rarely) termination. Plans, in turn, manage networks and utilization, run care management, and — in the modern era — administer in-lieu-of services and value-added benefits that move the boundary of what a capitation can pay for (California's Community Supports paying rent deposits and medically tailored meals is the frontier case).

### What the state always keeps

However much is delegated, the state retains eligibility determination (always — plans never decide who is eligible), the master enrollment record, rate setting, FFS payment for carve-outs and non-enrolled populations, the buy-in relationship with CMS, fair hearings, T-MSIS reporting, and policy itself. The cleanest way to describe the division of labor: **the state decides who is covered and what the promise is; the plan operates the promise for its enrolled slice; and the 834, 820, and 837 are the three-file conversation through which the two sides agree, month after month, about exactly what happened.**

---

## Part IV — The Fifty-State Gazetteer

One row per state: expansion status as of mid-2025, the delivery architecture in a phrase, and the distinctive marks a data professional should know walking in. Program names are the public brands. Everything here is a simplification and everything here changes; verify before load-bearing use.

| State | Program / brand | Expansion | Delivery architecture | Distinctive marks |
|---|---|---|---|---|
| Alabama | Alabama Medicaid | No | All FFS + ACHN regional care-coordination networks (PCCM) | The last major all-FFS state; RCO reform canceled 2017 pre-launch; Plan First family-planning-only program; ~18% FPL parent line |
| Alaska | Alaska Medicaid / DenaliCare | Yes (2015) | All FFS — no comprehensive managed care | Tribal health system central; 100% FMAP for IHS/tribal-referred care; travel as a covered logistics problem; vast-geography program |
| Arizona | AHCCCS | Yes | All-in capitation statewide, including LTSS (ALTCS) | Born capitated 1982 — never built legacy FFS; ALTCS since 1989; AIHP tribal FFS option with fluid plan switching; integrated D-SNP alignment |
| Arkansas | Arkansas Medicaid / ARHOME | Yes (2014) | Premium assistance: expansion adults in marketplace QHPs; PASSEs (provider-led risk entities) for BH/IDD; FFS core | The "private option" original; PASSE model is nationally unique |
| California | Medi-Cal | Yes | Three concurrent county models: COHS / Two-Plan / GMC (+ regional); county specialty BH carve; Medi-Cal Rx pharmacy carve | Largest program on earth; full-scope coverage regardless of immigration status (completed Jan 2024); CalAIM Community Supports; no non-MAGI asset test; Kaiser gated contract; D-SNP matching rule |
| Colorado | Health First Colorado | Yes | ACC: Regional Accountable Entities — attribution + BH capitation over largely FFS physical | The attribution model at scale; RAE phases as recurring re-procurement; Denver Health plan as provider-integrated pocket |
| Connecticut | HUSKY Health | Yes | Managed FFS with ASOs — terminated MCO contracts in 2012 | The state that fired its plans and went back; PCMH program on an FFS spine |
| Delaware | Diamond State Health Plan (Plus) | Yes | Statewide comprehensive MCO including MLTSS | Small-state all-in model; DSHP-Plus MLTSS |
| Florida | Statewide Medicaid Managed Care (SMMC) | No | Statewide mandatory MCO by region, incl. Long-Term Care program | SMMC 3.0 re-procurement (2025) with plan exits and region renumbering; share-of-cost medically needy month-by-month spans; LTC waitlist by priority score; largest non-expansion program after Texas |
| Georgia | Georgia Families / Pathways | Partial (Pathways, 2023) | CMOs for families/children; ABD largely FFS | Pathways: work/engagement-conditioned coverage to 100% FPL — nationally unique; expansion politics ongoing |
| Hawaii | Med-QUEST (QUEST Integration) | Yes | All-in statewide MCO incl. LTSS | Island-by-island rate cells; early all-population managed care; plan-keeps-you dual transitions |
| Idaho | Idaho Medicaid | Yes (2020, ballot 2018) | FFS + Healthy Connections PCCM; behavioral plan carve; duals plans in some counties | Ballot-forced expansion; benefit-lane structure; PCCM persistence |
| Illinois | HealthChoice Illinois | Yes | Statewide comprehensive MCO | Consolidated from county-era patchwork; large D-SNP transition from the MMP demo |
| Indiana | Healthy Indiana Plan (HIP) / Hoosier Healthwise | Yes (HIP 2.0) | Statewide MCO | POWER accounts — consumer contribution accounts inside Medicaid; Basic/Plus benefit tiers; the consumer-directed expansion archetype |
| Iowa | IA Health Link | Yes | Statewide comprehensive MCO incl. LTSS | The abrupt 2016 full privatization — a case study in big-bang transitions; retro waived for many adults |
| Kansas | KanCare | No | All-in statewide MCO incl. LTSS | Non-expansion all-in capitation — the unusual pairing; three-plan market |
| Kentucky | Kentucky Medicaid (kynect) | Yes (2014) | Statewide comprehensive MCO | Crowded plan market (six MCOs); kynect exchange integration heritage |
| Louisiana | Healthy Louisiana | Yes (2016) | Statewide comprehensive MCO | Fast, clean 2016 expansion launch as the modern template |
| Maine | MaineCare | Yes (2019, ballot 2017) | All FFS — no comprehensive MCO | Ballot-forced expansion delayed then implemented; FFS with PCCM heritage |
| Maryland | HealthChoice | Yes | Statewide comprehensive MCO | Coexists with the all-payer/Total Cost of Care hospital model — plans inside a rate-regulated hospital world |
| Massachusetts | MassHealth | Yes (pre-ACA heritage) | MCOs + Accountable Care Partnership Plans + PCC plan | RomneyCare precursor state; 2018 ACO restructuring; FIDE-SNP duals (Senior Care Options); the eligibility ladder inverted by generosity |
| Michigan | Healthy Michigan Plan | Yes | Statewide MCO; regional PIHPs hold the behavioral carve | Public regional behavioral entities (PIHPs) — the big-state county-flavored carve-out; MI Health Link MMP transitioned to D-SNPs |
| Minnesota | Medical Assistance | Yes | Statewide MCO with county-based purchasing pockets | MSHO — the nation's senior integrated-duals program, running since the 1990s; county-administered eligibility |
| Mississippi | Mississippi Medicaid / MississippiCAN | No | MCO for portions of the population; FFS remainder | The missing-rung eligibility ladder; among the lowest thresholds in the nation |
| Missouri | MO HealthNet | Yes (2021, ballot 2020 + litigation) | MCO for families/kids statewide; ABD largely FFS | The expansion the courts enforced; managed care/FFS population split |
| Montana | Montana Medicaid (HELP) | Yes (2016) | FFS — no comprehensive MCO | HELP Act premiums and the commercial TPA launch (since unwound); premium-clock data shapes; frontier delivery |
| Nebraska | Heritage Health | Yes (2020, ballot 2018) | Statewide comprehensive MCO | Ballot-forced expansion; unified physical/BH/pharmacy procurement |
| Nevada | Nevada Medicaid | Yes | MCO in Clark & Washoe counties only; FFS in 14 rural counties | The city limit — capitation switches on/off at county lines; Culinary Health Fund TPL texture; public-option law tied to Medicaid procurement; statewide MC expansion on the policy calendar |
| New Hampshire | NH Medicaid / Granite Advantage | Yes | Statewide comprehensive MCO | Expansion with a statutory FMAP trigger (ends if the match drops); expansion retro waived; county share of nursing home costs |
| New Jersey | NJ FamilyCare | Yes | Statewide comprehensive MCO incl. MLTSS | Early MLTSS adopter (2014); FIDE-SNP duals integration |
| New Mexico | Turquoise Care | Yes | All-in statewide MCO incl. LTSS | Double rename 2024 (program and agency — identifiers need effective dates); Western Sky exit as the plan-departure case; Community Benefit self-direction |
| New York | New York Medicaid | Yes | Mainstream MCO + HARP behavioral product line + MLTC partial-cap LTSS; NYRx pharmacy carve | The product-line state; MLTC partial capitation; medically needy spend-down at scale; county/local-district administration; the original CIN |
| North Carolina | NC Medicaid | Yes (Dec 2023) | Standard Plans + Tailored Plans (specialty BH/IDD MCOs), transformed 2021–2024 | The newest expansion; the great FFS-to-managed-care transformation; Tailored Plans as specialty-population managed care |
| North Dakota | ND Medicaid Expansion | Yes (2014) | Expansion population via a single contracted MCO; traditional FFS | One-plan expansion arrangement — a structure all its own |
| Ohio | Ohio Medicaid Next Generation | Yes | Statewide MCO; OhioRISE specialty child BH plan; single PBM | The 2022 Next Gen re-procurement; centralized pharmacy inside managed care; provider-sponsored plan heritage (CareSource) |
| Oklahoma | SoonerCare / SoonerSelect | Yes (2021, ballot 2020) | Statewide MCO since April 2024 | The big bang: 25 years of PCCM converted to capitation on one date — every member record carries the birthmark |
| Oregon | Oregon Health Plan | Yes | CCOs — regional, community-governed coordinated care organizations under global budgets | The global-budget model; health-related services flexibility; continuous eligibility pioneer (children to six, two-year adult) |
| Pennsylvania | Medical Assistance / HealthChoices | Yes | Physical HealthChoices MCOs; behavioral carve to counties (right of first opportunity); CHC MLTSS | The county behavioral carve at the largest scale; Community HealthChoices MLTSS rollout |
| Rhode Island | RIte Care | Yes | Statewide comprehensive MCO | The 2009 global waiver — first statewide global-budget compact; small-state laboratory heritage |
| South Carolina | Healthy Connections | No | Statewide comprehensive MCO | Non-expansion with mature managed care |
| South Dakota | South Dakota Medicaid | Yes (2023, constitutional ballot 2022) | Predominantly FFS — no comprehensive MCO | Expansion by constitutional amendment; FFS delivery persists post-expansion |
| Tennessee | TennCare | No | All-in statewide MCO incl. CHOICES MLTSS | First all-managed-care state (1994); aggregate-cap financing demonstration with shared savings; single pharmacy benefit manager |
| Texas | STAR / STAR+PLUS / STAR Kids / STAR Health | No | Program constellation: population-specific capitated programs statewide | Largest non-expansion program; the constellation model — the program, not just the plan, encodes the population; 1115 uncompensated-care pool |
| Utah | Utah Medicaid | Yes (2020, the fallback) | ACOs (full-risk plans) on the Wasatch Front; county PMHP behavioral carve statewide | Proposition 3 → legislative rewrite → CMS denial → statutory fallback; TAM/Bridge/full sediment in the group codes; "ACO" vocabulary collision; retro shrunk to the application month; Workforce Services determines eligibility |
| Vermont | Green Mountain Care / Global Commitment | Yes | The state operates as the public managed care entity — no commercial comprehensive MCOs | The state-is-the-plan waiver; OneCare all-payer ACO era concluded; single-payer-adjacent temperament |
| Virginia | Cardinal Care | Yes (2019) | Statewide comprehensive MCO incl. MLTSS | 2023 consolidation of Medallion and CCC Plus into one program — the merge as a data event |
| Washington | Apple Health | Yes | Statewide integrated MCO (physical + behavioral purchased together) | The integration decade (2016–2020) that ended the BH carve-out; Health Care Authority as purchaser; continuous eligibility for young children; HCBS waitlist realities |
| West Virginia | Mountain Health Trust | Yes | Statewide comprehensive MCO | Among the highest Medicaid-coverage shares in the nation; pharmacy carved to FFS |
| Wisconsin | BadgerCare Plus / ForwardHealth | No (waiver to 100% FPL) | HMO model for families; Family Care & IRIS for LTSS | The only non-expansion state with no coverage gap; IRIS self-direction; county human-services fabric |
| Wyoming | Wyoming Medicaid | No | All FFS — no managed care | The smallest program; non-expansion frontier FFS; eligibility reconciliation against daily state files as the operational heartbeat |

The District of Columbia (expanded, statewide MCO) and the five territories (block-grant-style capped federal financing — a fundamentally different fiscal deal) sit outside this table but inside the same statute.

---

## Part V — Reading the Central Series Against This Map

The Central series builds one demonstration application per state on a deliberately constant chassis — same synthetic population size, same register structure, same 834 rendering — so that everything that differs between apps is the state itself. Against the axes above, the built states index like this:

| Axis illustrated | Central series applications |
|---|---|
| The federal chassis itself (baseline mechanics) | Maryland, New York — the reference implementations: spans, groups, the two clocks, the 834 |
| Expansion presence, absence, and personality | Mississippi (the missing rung), Texas and Florida and Alabama (non-expansion negative space), Montana (HELP premiums), Utah (the ballot-rewrite-denial-fallback sediment), Oklahoma and Idaho (ballot states) |
| The delivery spectrum, pole to pole | Alabama (all gray — the control group) ↔ Arizona (born capitated — never gray); Vermont (the state is the plan); Connecticut's story is told in the landscape, not yet an app |
| Attribution and PCCM overlays | Colorado (RAEs), Alabama (ACHN), Oklahoma (the PCCM era as birthmark) |
| Geography as architecture | Nevada (the city limit), California (three models by county), Hawaii (island rate cells) |
| Carve-outs and integration | Utah (the county PMHP carve kept on purpose) ↔ Washington (the integration that ended it); New York (HARP as carve-in product line) |
| LTSS strategies | Arizona (ALTCS), New York (MLTC partial cap), Texas (STAR+PLUS constellation), Washington and Florida (waitlists), New Mexico (self-direction), Alabama (FFS nursing homes, ACT transitions), New Hampshire (county homes) |
| Eligibility exotica | Florida (share-of-cost flicker), Alabama (Plan First sliver; MSP-only spans), Massachusetts (the inverted ladder), Nevada (hospital presumptive eligibility), Utah (the short reach-back), California (the scope conversion) |
| Procurement and program change as data events | Florida (SMMC 3.0 in-window), New Mexico (the Western Sky exit), Oklahoma (the big bang), Alabama (the RCO ghost), Virginia-style merges (told via New Mexico's double rename) |
| The Medicare catalog (duals, one answer per state) | Sixteen answers and counting, from Massachusetts (loud) to Alabama (perfectly still) to Nevada (two answers, chosen by geography) to Utah (split down the middle of one member) to California (aligned by law) |
| TPL | Nevada (the Culinary Health Fund register — the series' first) |

The series currently covers twenty-plus states in this format, with Alaska in an earlier format, and the remaining states — Oregon's CCOs, Pennsylvania's county behavioral carve, North Carolina's transformation, Tennessee's TennCare, Connecticut's return to FFS, Minnesota's MSHO, Indiana's POWER accounts, Arkansas's PASSEs among the most teachable — as the natural continuation.

---

## Closing: The Portable Skill

The practical takeaway of all of this for anyone who works in Medicaid data: the statute gives you a portable core — the span, the group, the permanent identifier, the two clocks, the 834/820/837 conversation, payer-of-last-resort, the buy-in — and each state wraps that core in a local architecture you must learn on arrival: what the delivery column can contain, where the carve-out seams run, what the county line does, which words collide, and what the waiver made strange. Learn the chassis once; learn each state's paint job with respect. The states are not fifty variations on a theme. They are fifty serious answers to the same set of hard questions, and the differences between them are, in nearly every case, somebody's deliberate decision with a story behind it — usually legible, if you know how to read it, in the member data itself.

---

*All program facts reflect the public record of the mid-2020s and change continuously; expansion status, plan rosters, waiver terms, delivery architectures, and procurement outcomes should be verified against current CMS and state agency publications before any non-demonstration use. This document simplifies deliberately in the service of teaching. Prepared as a companion to the Central series of single-file healthcare data demonstration applications.*

*© Robert Thomas Keyes*
