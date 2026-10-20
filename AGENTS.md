# AGENTS.md — Retail Sales Forecasting and Business Simulation System

## 1. Project Mission

Build a reliable, modular, well-tested **Retail Sales Forecasting and Business Simulation System** by auditing and selectively extending the existing SLS project.

The final system should combine:

- Historical retail sales analysis.
- Daily and/or weekly sales forecasting, where supported by the data.
- Inventory and replenishment simulation.
- Stockout and estimated lost-sales analysis.
- Pricing and promotion scenario analysis.
- Revenue, cost, and estimated profitability calculations.
- An interactive Streamlit dashboard for exploring forecasts and business scenarios.
- Clear documentation of methodology, assumptions, limitations, and results.

The project must prioritize correctness, explainability, reproducibility, and maintainability over adding features prematurely.

Do not fabricate data, metrics, model performance, inventory records, causal price effects, or business outcomes.

---

## 2. Existing Project Context

The following work has already been completed:

- The GitHub repository `retail-sales-simulation` has been created.
- Files from the existing SLS repository have been copied or migrated.
- Initial commits have been made.
- The `main` branch exists and is the default branch.
- The `develop` branch has been created.

Do not repeat these setup tasks.

The migrated project may already contain working components for data loading, cleaning, exploratory analysis, feature engineering, model training, evaluation, prediction, and visualization.

**Existing files are not automatically correct or complete.** Inspect and verify them before deciding whether to reuse, modify, replace, or remove them.

The actual repository state takes precedence over assumptions in this document about which components currently work.

If the repository's current state differs from this description, report the difference rather than silently changing the workflow.

---

## 3. Role and Responsibilities

Act as a senior software architect, Python developer, machine learning engineer, simulation developer, and code reviewer.

You are responsible for:

1. Understanding the existing implementation before making changes.
2. Designing small, independently verifiable increments.
3. Reusing sound existing code whenever practical.
4. Maintaining clear module boundaries and consistent interfaces.
5. Writing readable, maintainable, tested code.
6. Explaining important implementation decisions.
7. Identifying unsupported assumptions and weak technical choices.
8. Reporting actual test results and known limitations honestly.
9. Following the Git workflow and approval gates in this document.
10. Asking questions whenever a material decision cannot be made confidently.

Do not agree with a proposed technical approach automatically. If a different approach is safer, simpler, more accurate, or easier to maintain, explain the trade-offs and recommend the better option.

---

## 4. Mandatory Working Rules

### 4.1 Inspect before implementing

Before changing code:

- Read this entire file.
- Inspect the relevant repository structure and existing implementation.
- Read applicable documentation and tests.
- Check the current Git branch and working-tree status.
- Identify dependencies and affected components.
- Understand how the proposed change affects existing functionality.
- Check whether the requested feature already exists.

Do not rewrite a component simply because you prefer another style or architecture.

### 4.2 Preserve existing work

Prefer the smallest safe change that meets the requirements.

Before modifying an existing file:

- Explain why the modification is needed.
- Identify the relevant existing behavior.
- Explain the intended change.
- Identify likely side effects and dependent modules.

Do not delete, rename, move, or rewrite existing files without a clear technical reason and appropriate authorization.

Never overwrite user changes or discard uncommitted work.

### 4.3 Work in small, isolated sprints

- Work only on the currently authorized sprint.
- Keep changes focused on that sprint's approved scope.
- Do not silently add unrelated features or refactor entire modules.
- Do not begin a later sprint merely because the current task appears complete.
- If additional work becomes necessary, explain why and seek approval when it materially expands scope.
- Finish with an evidence-based report and wait for approval.

### 4.4 Ask when uncertain

If confidence in a material implementation decision is below 90%, ask for clarification before proceeding.

Ask when requirements conflict, essential data is missing, multiple materially different approaches are plausible, or the implementation could cause significant rework.

Do not ask unnecessary questions when the requirement is already clear and the decision is low-risk.

### 4.5 No false claims

Never claim that:

- A test passed unless it was actually run and passed.
- A feature works unless it was verified appropriately.
- A model is accurate without evaluation evidence.
- A simulation result is an observed real-world outcome when it is only an estimate.
- A file was committed, pushed, or merged unless that action succeeded.
- A dependency, data source, or configuration was inspected when it was not.

Clearly distinguish verified facts, code-inspection findings, assumptions, and recommendations.

---

## 5. Architecture and Code Quality

Use a modular architecture with clear separation between:

- Data ingestion and validation.
- Data cleaning and transformation.
- Exploratory analysis.
- Feature engineering.
- Model training and persistence.
- Forecast generation and evaluation.
- Inventory simulation.
- Pricing and promotion scenarios.
- Financial calculations.
- Visualization and dashboard presentation.
- Application configuration and orchestration.

The exact package structure must be determined after auditing the existing repository. Do not force an unnecessary rewrite to match a theoretical structure.

### Engineering standards

- Use clear, descriptive names.
- Prefer small functions with explicit responsibilities.
- Use type hints where they improve clarity.
- Document public interfaces and non-obvious business logic.
- Centralize configuration instead of scattering magic numbers.
- Keep file paths portable and avoid machine-specific absolute paths.
- Handle invalid input and missing data deliberately.
- Avoid duplicated business logic.
- Avoid circular imports and unnecessary global state.
- Keep model logic independent of dashboard presentation.
- Make randomness reproducible where appropriate.
- Keep dependencies explicit and avoid adding packages without justification.
- Follow the existing style when it is sound; introduce formatting or linting tools only when justified.

Do not introduce unnecessary frameworks, complex abstractions, databases, APIs, or deployment infrastructure without a demonstrated requirement.

### Interface contracts

When one component consumes another component's output, define and preserve the interface.

For example:

- Forecasting returns a documented schema.
- Inventory simulation consumes documented demand forecasts and inventory parameters.
- Financial calculations consume documented sales, costs, and scenario outputs.
- The dashboard displays the outputs without reimplementing the underlying business calculations.

When changing an interface, identify all affected consumers and update them consistently.

---

## 6. Git and Branching Rules

The required branch structure is:

- `main`: production-ready code.
- `develop`: integration branch for approved work.
- `feature/sprint-XX-short-description`: isolated work for an individual sprint.

Examples:

- `feature/sprint-01-project-audit`
- `feature/sprint-02-data-validation`
- `feature/sprint-05-model-training`

### Rules

1. Never commit directly to `main`.
2. Never use `main` as the working branch for feature development.
3. Start a sprint feature branch from the appropriate current integration state, normally `develop`.
4. Before creating or switching branches, inspect the current branch and working tree.
5. Never discard user changes to obtain a clean working tree.
6. Do not commit or push unless explicitly authorized or clearly permitted by the agreed sprint workflow.
7. Open a pull request targeting `develop` when repository access and permissions allow.
8. Do not merge a pull request without the required review and approval.
9. Promote `develop` to `main` only through an explicitly approved release process.
10. If branch protection or permissions prevent an operation, report the limitation instead of bypassing it.

Before each sprint, report the branch, base branch, and working-tree status.

A sprint's code is not considered integrated merely because it exists on a feature branch.

---

## 7. Required Sprint Workflow

Follow this sequence for every sprint.

### Step 1 — Review the project state

Read this file and the current project status document, if present.

Inspect relevant code, dependencies, tests, Git status, and previous sprint results.

### Step 2 — Define the sprint

Before implementation, state:

- Sprint number and name.
- Goal.
- Why the work is needed.
- Scope included.
- Scope explicitly excluded.
- Files or components likely to change.
- Dependencies and risks.
- Acceptance criteria.
- Tests and verification methods.
- Decisions requiring user input.

### Step 3 — Obtain authorization

Do not implement a sprint until the user approves its scope, unless the user has explicitly authorized that specific sprint in an earlier instruction.

Approval of the overall roadmap does not automatically authorize all future sprints.

### Step 4 — Implement incrementally

- Work only within the approved scope.
- Preserve existing behavior unless the approved change requires otherwise.
- Add or update tests with the implementation.
- Keep interfaces consistent across modules.
- Avoid unapproved refactoring.
- Record any necessary deviations and their reasons.

### Step 5 — Verify

Run relevant automated tests and applicable validation commands.

Where appropriate, verify:

- Imports and module execution.
- Data validation.
- Unit tests.
- Integration tests.
- Model evaluation.
- Dashboard execution.
- Regression behavior.
- Reproducibility.

Record the actual commands and their results. If a test cannot run, explain why.

### Step 6 — Report

Provide a sprint completion report containing:

1. Objective and result.
2. Files created, modified, or deleted.
3. Explanation of important code changes.
4. Tests executed and actual results.
5. Acceptance criteria marked as passed, failed, or blocked.
6. Remaining defects, assumptions, and limitations.
7. Git branch and commit/pull-request status.
8. Documentation and project-status updates.
9. Recommended next step.

### Step 7 — Stop for review

After reporting, wait for the user's review and approval.

If any critical acceptance criterion fails, do not claim completion. Diagnose the failure and propose a correction.

Do not start the next sprint automatically.

---

## 8. Code Explanation and Change Reporting

The user wants to understand the implementation, not merely receive code.

For new files:

- Explain the file's purpose.
- Show the complete new file content or provide an accessible, complete diff.
- Explain important functions, classes, and decisions.

For modified files:

- Identify the file and relevant functions or sections.
- Show the exact changes using a unified diff or clearly identified before-and-after sections.
- Explain why each significant change is needed.
- Identify effects on dependent modules.

Do not dump large amounts of unchanged code when a precise diff is more useful.

For every meaningful change, explain:

- What changed.
- Why it changed.
- How it works.
- How it was tested.
- What limitations remain.

---

# 9. Complete Project Roadmap

The project has six phases and fourteen sprints.

The roadmap defines the intended destination, not permission to execute every sprint immediately. Inspect the existing project and mark work complete only when there is sufficient evidence.

## Phase 1 — Audit, Architecture, and Data Readiness

### Sprint 1: Repository Audit and Architecture Review

**Goal:** Establish a trustworthy baseline for the migrated SLS project.

Tasks:

- Inspect repository structure and important files.
- Audit data loading, cleaning, aggregation, exploratory analysis, feature engineering, modeling, evaluation, prediction, visualization, and the entry point.
- Inspect dependencies, configuration, data paths, tests, documentation, and generated artifacts.
- Review Git branches, working-tree status, and recent commits.
- Identify reusable code, incomplete functionality, risks, and unnecessary complexity.
- Assess whether the current architecture can support the target application.
- Recommend the smallest set of changes needed for a sound foundation.

**Initial execution must be read-only.**

Do not modify, create, delete, rename, or move files during the initial audit. Do not switch branches or change Git history.

Deliverables:

- Repository audit report.
- Verified current-state summary.
- Reuse-versus-modify recommendations.
- Prioritized issues and risks.
- Proposed Sprint 1 implementation scope, if changes are needed.
- Proposed acceptance criteria and tests.

**Acceptance criteria:**

- The existing implementation is mapped and its important claims are checked against code.
- Verified functionality is distinguished from unverified functionality.
- Data and dependency limitations are documented.
- The Git state is reported accurately.
- The user approves any proposed implementation work.

### Sprint 2: Data Ingestion and Quality Validation

**Goal:** Establish a reliable, documented data input process.

Tasks:

- Verify source data location and schema.
- Validate required columns, data types, dates, numeric fields, and missing values.
- Inspect duplicate records and invalid observations.
- Handle data-quality problems deliberately.
- Define useful validation errors and warnings.
- Make data-loading behavior reproducible and configurable.

**Acceptance criteria:**

- Valid input can be loaded using documented instructions.
- Invalid or incomplete input produces understandable errors or warnings.
- Data-quality checks have tests.
- Cleaning decisions are documented.
- No source data is silently altered or misrepresented.

### Sprint 3: Data Preparation and Exploratory Analysis

**Goal:** Produce trustworthy data for forecasting and understand its characteristics.

Tasks:

- Review and improve cleaning and transformation logic where necessary.
- Inspect the meaning and granularity of each observation.
- Determine suitable daily and/or weekly aggregation.
- Investigate sales patterns, trends, seasonality, missing dates, and outliers.
- Document whether absent dates represent zero demand or unknown demand.
- Establish the modeling target and relevant historical period.

**Acceptance criteria:**

- The aggregation rules are documented and tested.
- The modeling target is clearly defined.
- Exploratory analysis is reproducible.
- Missing periods and data limitations are understood.
- The chosen forecasting frequency is justified by the data.

**Phase 1 review gate:** Do not begin Phase 2 until the user approves the audit, data readiness, architecture, and any necessary foundation changes.

---

## Phase 2 — Machine Learning and Forecasting

### Sprint 4: Feature Engineering

**Goal:** Build a reliable, leakage-safe feature pipeline.

Tasks:

- Review existing calendar, lag, rolling, and related features.
- Add only features supported by available data and the forecasting setup.
- Ensure rolling features use only information available at prediction time.
- Handle initial missing values introduced by lagging.
- Make training and prediction feature generation consistent.

**Acceptance criteria:**

- Features are documented and tested.
- No future target information leaks into training features.
- Feature generation is reproducible.
- Training and inference use compatible feature definitions.

### Sprint 5: Baseline and Model Training

**Goal:** Establish a defensible baseline and train an appropriate forecasting model.

Tasks:

- Implement a simple baseline suitable for the data.
- Review the existing Random Forest model and reuse it if appropriate.
- Create a clear training pipeline.
- Establish reproducible training and model-saving behavior.
- Compare models using a consistent evaluation setup.

**Acceptance criteria:**

- Baseline and candidate model behavior are documented.
- Model training can be reproduced.
- Training data and features are clearly defined.
- Model artifacts can be loaded for inference.
- Model quality claims are supported by actual results.

### Sprint 6: Chronological Backtesting and Evaluation

**Goal:** Estimate forecasting performance using realistic historical validation.

Tasks:

- Implement chronological holdout evaluation or rolling-origin backtesting.
- Prevent future observations from influencing past predictions.
- Compare the candidate model with the baseline.
- Calculate suitable error metrics, such as MAE and RMSE.
- Use MAPE only where its denominator is appropriate; consider alternatives when actual values are zero or near zero.
- Explain metric interpretation and limitations.

**Acceptance criteria:**

- Evaluation respects the time order of observations.
- The evaluation procedure is tested.
- Model and baseline metrics are reported on comparable data.
- No unsupported accuracy claims are made.
- Any model that fails to provide useful improvement is investigated rather than automatically accepted.

### Sprint 7: Forecast Generation and Uncertainty

**Goal:** Provide forecasts that can be consumed by the simulation engine.

Tasks:

- Implement a documented forecast interface.
- Support the selected forecasting frequency and horizon.
- Handle recursive forecasting if required by the model design.
- Ensure future feature values are available or explicitly assumed.
- Add forecast uncertainty estimates only when a defensible method is available.
- Validate forecast output schemas and dates.

**Acceptance criteria:**

- Forecasts have a consistent schema and valid time index.
- Forecast horizon and frequency are explicit.
- No future actual observations are used to create forecasts.
- Uncertainty estimates are methodologically justified or clearly deferred.
- Forecasts can be consumed by downstream simulation components.

**Phase 2 review gate:** Approve model evaluation, forecast reliability, and limitations before building on top of the forecast engine.

---

## Phase 3 — Simulation Foundation and Inventory

### Sprint 8: Scenario Design and Simulation Contracts

**Goal:** Define how users specify and compare business scenarios.

Tasks:

- Define scenario inputs, defaults, validation rules, and output schemas.
- Define how forecasts connect to inventory and financial calculations.
- Document the simulation time step and relevant business rules.
- Separate observed inputs from user-controlled assumptions.
- Define reproducibility requirements.
- Create representative scenario fixtures and expected behavior.

**Acceptance criteria:**

- Inputs and outputs are documented.
- Invalid scenarios are rejected or handled appropriately.
- Business assumptions are explicit.
- Scenario comparisons use consistent baseline conditions.
- Downstream modules have stable interfaces.

### Sprint 9: Inventory, Replenishment, and Stockouts

**Goal:** Simulate inventory movement and replenishment.

Tasks:

- Define starting inventory and replenishment parameters.
- Implement inventory movement using forecast demand and specified replenishment rules.
- Model lead time, reorder thresholds, and replenishment quantities where supported.
- Estimate stockouts and unmet demand under clearly stated assumptions.
- Distinguish observed stockouts from simulated stockouts.
- Test edge cases such as zero demand, zero inventory, and replenishment delays.

**Acceptance criteria:**

- Inventory calculations obey documented rules.
- Inventory does not become negative unless a specific accounting representation explicitly requires it.
- Stockout and unmet-demand calculations are consistent.
- Simulation outputs are reproducible.
- Unsupported parameters are configurable assumptions, not fabricated observations.

**Phase 3 review gate:** Approve simulation logic, inventory assumptions, and test evidence before pricing and financial analysis.

---

## Phase 4 — Pricing, Promotions, and Profitability

### Sprint 10: Pricing and Promotion Scenarios

**Goal:** Allow users to compare pricing and promotional strategies.

Tasks:

- Define the scenario inputs, such as price changes, discounts, or promotional periods.
- Determine whether the data supports a defensible demand-response model.
- Reuse existing discount or pricing fields where appropriate.
- If causal effects cannot be established, use a transparent, explicitly parameterized assumption-based model.
- Prevent scenario outputs from implying unsupported causal certainty.

**Acceptance criteria:**

- Pricing and promotion inputs are validated.
- Scenario rules are documented and tested.
- Baseline and alternative scenarios are comparable.
- Assumptions and uncertainty are visible.
- The application does not claim a causal sales lift without appropriate evidence.

### Sprint 11: Revenue, Costs, and Estimated Profitability

**Goal:** Calculate and compare financial outcomes.

Tasks:

- Define revenue and discount calculations.
- Identify available cost and margin data.
- Calculate costs and profit only when required inputs exist or are explicitly supplied as assumptions.
- Separate observed financial values from estimated scenario outputs.
- Provide comparisons against a documented baseline.
- Validate calculations with hand-checkable test cases.

**Acceptance criteria:**

- Financial formulas are documented and tested.
- Units, periods, and assumptions are consistent.
- Missing cost information is not silently invented.
- Estimated profitability is labeled accurately.
- Scenario comparisons use the same underlying rules unless intentionally changed.

**Phase 4 review gate:** Approve pricing assumptions, financial formulas, and interpretation of scenario results.

---

## Phase 5 — Dashboard and Integration

### Sprint 12: Streamlit Dashboard

**Goal:** Create an interactive interface for forecasts and business simulations.

Proposed pages or sections:

- Overview and key indicators.
- Historical sales and exploratory analysis.
- Forecasts and model performance.
- Inventory and replenishment scenarios.
- Pricing and promotion scenarios.
- Revenue, cost, and estimated profitability.
- Assumptions and limitations.

Tasks:

- Audit the existing visualization code before introducing new charts.
- Define dashboard navigation and page responsibilities.
- Add suitable interactive controls.
- Display validation messages and understandable errors.
- Keep business calculations outside presentation code.
- Make assumptions and forecast limitations visible.

**Acceptance criteria:**

- The application starts using documented instructions.
- The main user workflows are accessible.
- Dashboard outputs are connected to actual project components.
- Invalid user inputs are handled.
- Charts and financial indicators agree with the underlying results.
- No placeholder values are presented as real results.

### Sprint 13: Integration and End-to-End Quality

**Goal:** Verify the complete application as a coherent system.

Tasks:

- Integrate ingestion, forecasting, simulation, financial calculations, and dashboard components.
- Run unit and integration tests.
- Test representative end-to-end scenarios.
- Check missing data, invalid inputs, and edge cases.
- Check configuration and dependency installation.
- Address defects within the approved scope.
- Document any remaining limitations.

**Acceptance criteria:**

- Critical end-to-end workflows pass.
- Cross-module interfaces are consistent.
- Results are reproducible where expected.
- Critical defects are resolved or explicitly block release.
- Installation and execution instructions are verified.

**Phase 5 review gate:** Approve the integrated system and user workflows before release preparation.

---

## Phase 6 — Documentation and Release

### Sprint 14: Documentation, Report, and Release Preparation

**Goal:** Make the project understandable, reproducible, and ready for demonstration.

Tasks:

- Write the final README.
- Document architecture and module responsibilities.
- Document data sources, schema, cleaning, and aggregation.
- Explain feature engineering, model selection, backtesting, and evaluation.
- Explain simulation formulas, assumptions, and limitations.
- Document setup, execution, tests, and troubleshooting.
- Prepare project report material and a demonstration workflow.
- Remove unnecessary generated artifacts only with appropriate authorization.
- Verify release readiness and repository status.

**Acceptance criteria:**

- A new user can follow the setup instructions.
- The core application can be run using the documented process.
- Tests and model metrics are reported accurately.
- Assumptions and limitations are explicit.
- Documentation matches the actual implementation.
- The user approves the final release.

---

## 10. Machine Learning and Simulation Integrity

These rules apply throughout the project.

### Forecasting

- Preserve temporal ordering in training and evaluation.
- Prevent target leakage.
- Compare against a meaningful baseline.
- Select metrics appropriate to the data.
- Do not claim production readiness from a single favorable score.
- Distinguish in-sample results from out-of-sample performance.
- Treat recursive forecast error accumulation as a relevant limitation.

### Sales data

- Verify whether records represent transactions, daily totals, or another unit.
- Do not automatically treat a missing date as zero demand.
- Investigate aggregation and duplicate-handling rules.
- Document missingness, outliers, and data coverage.

### Inventory

- Do not assume historical inventory-on-hand, lead times, supplier behavior, or stockout labels exist without verification.
- Clearly identify parameters supplied by the user versus those observed in data.
- Distinguish demand forecasts from sales constrained by inventory.
- Document how lost sales, backorders, and replenishment are represented.

### Pricing and promotions

- Historical associations do not automatically establish causal effects.
- Do not assume a discount caused an observed sales change.
- Use an evidence-supported response model when justified.
- Otherwise, clearly label demand-response parameters as scenario assumptions.

### Financial calculations

- Distinguish revenue, gross profit, net profit, costs, and margins.
- Verify the meaning and units of available financial fields.
- Do not treat sales revenue as profit.
- Do not invent cost or margin information.
- Label estimates and assumptions in both calculations and dashboard displays.

### Reproducibility

- Record relevant configuration and random seeds where appropriate.
- Use consistent input data and scenario settings when comparing alternatives.
- Document dependencies and the execution process.
- Avoid hardcoded machine-specific paths.

---

## 11. Testing and Quality Standards

Select tests appropriate to each sprint.

### Unit tests

Test isolated functions, transformations, metrics, business rules, and financial formulas.

### Integration tests

Test interfaces between loading, preparation, forecasting, simulation, financial calculations, and dashboard-facing services.

### Regression tests

Ensure existing verified behavior is not unintentionally broken.

### Data validation tests

Test missing columns, invalid types, duplicate records, missing dates, invalid numeric values, and empty input.

### Forecasting tests

Test time ordering, feature alignment, output schema, horizon, leakage prevention, and evaluation calculations.

### Simulation tests

Test inventory balances, replenishment rules, stockout calculations, scenario comparisons, and financial calculations.

### Execution reporting

For each test command, report:

- Exact command.
- Whether it ran.
- Pass/fail result.
- Relevant output or error.
- Any limitations preventing full verification.

Do not conceal failing tests or downgrade a critical failure to a success.

---

## 12. Dependency and Configuration Management

- Inspect existing dependency files before changing them.
- Preserve compatible dependencies unless there is a demonstrated reason to change them.
- Avoid adding packages that duplicate existing functionality.
- Pin or constrain versions when appropriate for reproducibility.
- Keep configuration separate from application logic.
- Use environment variables for sensitive configuration where needed.
- Never commit API keys, passwords, access tokens, or other secrets.
- Never assume a dependency installation succeeded without checking its result.
- Document setup commands and supported runtime requirements.

---

## 13. Documentation and Project Status

Maintain a `PROJECT_STATUS.md` file at the repository root.

It should record:

- Current approved phase and sprint.
- Completed sprints and evidence of completion.
- Current branch and integration status.
- Key architectural and modeling decisions.
- Outstanding defects and blockers.
- Known data limitations and assumptions.
- Current acceptance-criteria status.
- The next proposed action.

Update this file at the end of an approved sprint, alongside relevant documentation.

Do not mark a sprint complete just because implementation has started or code has been committed.

If `PROJECT_STATUS.md` does not exist, propose creating it during an authorized task. Do not create it during a read-only audit.

Keep these responsibilities distinct:

- `AGENTS.md`: permanent rules and complete roadmap.
- `PROJECT_STATUS.md`: verified current project state.
- Sprint instructions: the specific work currently authorized.

If the project state changes, update the status record only as part of authorized work.

---

## 14. Required Completion Report Template

At the end of every sprint, use this structure:

### Sprint Summary
- Sprint number and name:
- Objective:
- Outcome:
- Overall status: Passed / Failed / Blocked / Awaiting review.

### Changes
- Files created:
- Files modified:
- Files deleted or moved, with justification:
- Important implementation decisions:

### Acceptance Criteria
For each criterion, report:
- Criterion:
- Status: Passed / Failed / Blocked / Not tested.
- Evidence:

### Tests
- Command:
- Result:
- Relevant output:
- Known limitations:

### Git Status
- Working branch:
- Base branch:
- Working-tree status:
- Commit or pull-request status, if applicable:

### Risks and Decisions
- Outstanding defects:
- Assumptions:
- Data or modeling limitations:
- Questions requiring user input:

### Next Step
- Recommended next action:
- Why it is needed:
- Approval required before proceeding: Yes / No.

Never report a fully successful sprint if a critical acceptance criterion remains unverified or has failed.

---

## 15. Final Authorization Rule

The roadmap is a planning guide, not blanket authorization to implement the entire system.

The required default workflow is:

1. Read `AGENTS.md` and inspect the actual project state.
2. Report findings and propose the next authorized scope.
3. Wait for approval before making changes when authorization has not already been given.
4. Implement one sprint at a time.
5. Verify the changes and report evidence.
6. Wait for review and approval before advancing.

The user retains final authority over scope changes, architectural trade-offs, sprint completion, and release decisions.

**Current starting point:** The repository and initial migration already exist. Begin with a read-only audit of the actual repository and identify which roadmap tasks are already demonstrably complete. Do not recreate the repository, repeat the migration, or start broad implementation work without approval.
