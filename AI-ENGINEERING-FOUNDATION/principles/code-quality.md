# Code Quality

High-quality code is correct, easy to read, easy to change safely, and no larger than the problem requires. This is not a style guide: follow the project's existing formatter, linter, and conventions for style.

## Readability

- A reader should understand what a function does from its name and signature, and why from the surrounding context.
- Prefer straightforward control flow. Use early returns to reduce nesting.
- Keep related logic close together.
- Comments explain *why*: a business rule, a constraint, a non-obvious trade-off, a workaround with its cause. Comments that repeat the code are noise and should be removed.

## Cohesion and coupling

- A module groups things that change for the same reason.
- Modules depend on each other through small, explicit interfaces.
- If a change to one feature routinely requires edits in many unrelated files, the boundaries are wrong.

## Separation of concerns

- Business rules do not depend on transport (HTTP, CLI, queue) or storage details.
- Data access is isolated enough to be replaced in tests or changed without rewriting business logic.
- Infrastructure concerns (configuration, logging setup, retries, connection management) do not leak into domain code.
- Proportion matters: a small script does not need three layers. Separate concerns when it reduces real coupling.

## Naming

- Use the domain's terms. `invoice.markOverdue()` beats `processor.handle(item, 3)`.
- Names reveal intent and units: `timeoutSeconds`, `isEligibleForRefund`.
- Avoid vague names: `data`, `info`, `manager`, `helper`, `utils`, `handleStuff`, unless the scope is tiny.
- Be consistent: one concept, one name, across code, database, API, and docs.

## Function and module responsibilities

- A function does one thing at one level of abstraction.
- Long parameter lists, boolean flags that switch behavior, and functions that both compute and perform side effects are signals to restructure.
- Public surface is minimal. Expose what callers need, not everything that exists.

## Testability

- Inject dependencies that cross process boundaries (time, randomness, network, storage) where tests need to control them.
- Pure logic is separated from side effects where practical.
- If a unit cannot be tested without elaborate mocking, reconsider its design before adding mocks.

## Error handling

- Handle errors at the level that has enough context to decide what to do.
- Use the language's idiomatic mechanism (exceptions, result types, error returns) consistently.
- Error messages say what failed and, when safe, why. They do not leak secrets or internals across trust boundaries.
- Do not add defensive checks for situations that cannot occur given validated inputs and types. Validate at the boundary; trust inside it.

## Consistency

- Match the patterns already established in the repository, even if you would choose differently in a new project.
- If an existing pattern is harmful, propose changing it explicitly rather than introducing a second pattern beside it.

## Maintainability

- Small, focused changes are easier to review and revert.
- Delete dead code instead of commenting it out. Version control keeps history.
- Configuration is for values that genuinely vary between environments or deployments, not for every constant.

## Refactoring discipline

- Refactor separately from behavior changes when possible, or at least in clearly separated commits.
- Refactor with tests in place that pin current behavior.
- Have a concrete goal ("make X testable", "remove duplicated pricing logic") and stop when it is reached.
- Do not refactor code unrelated to the current task without approval.

## Avoiding AI-generated filler and unnecessary complexity

Do not produce:

- Generic implementations disconnected from the actual business requirements.
- Layers, interfaces, factories, or base classes with a single implementation and no stated reason.
- Comments that narrate the code ("// increment counter", "// call the API").
- Docstrings that restate the function name.
- Boilerplate copied across files instead of fixing the cause.
- Invented requirements, options, or configuration flags.
- Technology choices without a stated reason.
- Premature optimization: caches, pools, or concurrency added without a measured need.
- Excessive defensive programming: null checks, try/catch blocks, and fallbacks without a credible failure scenario.
- Large rewrites where a focused change would do.
- Placeholder code (`TODO: implement`) presented as complete work.
- Claims of completion without verification.

Every abstraction, dependency, and line of code should have a purpose you can state.

## Duplication

- Remove duplication when the duplicated pieces represent the same knowledge and will change together.
- Leave similar-looking code alone when the pieces represent different concepts that may diverge.
- Do not create an abstraction merely to eliminate a few repeated lines.
