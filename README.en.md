<h1>Development Rules</h1>

[日本語版 README](./README.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./.github/PULL_REQUEST_TEMPLATE.md) [![Last commit](https://img.shields.io/github/last-commit/tetratensor/awesome-development-rules)](./)

`Development Rules` is a comprehensive, practical repository that compiles best practices and guidelines for software development.<br>
This repository aims to provide guidance for developers, teams, and organizations to build higher-quality, maintainable, and scalable software.

<h1>Table of Contents</h1>

- [Code Style](#code-style)
- [Package Principles](#package-principles)
- [Coding Principles](#code-principle)
- [Review](#review)
- [Testing](#test)
- [Documentation](#document)
- [Git Operations](#git-operation)
- [Release Control (Feature Flags)](#release-control)
- [Team Building](#team-building)
- [References](#reference)
- [Useful Templates](#template)
- [Deals](#deals)
- [Contributing](#contributing)
- [Code of Conduct](#code-of-conduct)
- [Authors](#authors)
- [License](#license)
<!-- - [CSS Design](#css-design) -->

<h1 id="code-style">Code Style</h1>
Follow the coding conventions, style guides, and principles agreed upon within the team.<br>
Write clear, readable code with appropriate comments.

<h2>Use Documentation Comments</h2>
Documentation comments are special comments inserted into source code to provide documentation or explanations for software elements (functions, classes, modules, etc.).

#### For Python (Docstring)

```
def count_characters(text: str) -> int:
  """Return the length of a string.

  This function calculates the length of the given string and returns it.

  Args:
      text: The string.

  Returns:
      int: Length of the string.

  Raises:
      TypeError: If the argument is not a string.

  Examples:
      >>> count_characters("Hello world!")
      12

  Note:
      Returns 0 for an empty string ("").
  """

  if not isinstance(text, str):
    raise TypeError("Argument must be a string.")

  return len(text)
```

#### For JS (JSDoc)

```
/**
 * This is a JSDoc comment. It provides documentation for the function.
 *
 * @param {string} parameter Description of the parameter.
 * @returns {number} Description of the return value.
 */
function exampleFunction(parameter) {
  // Implementation
  return parameter.length;
}
```

#### For TS (TSDoc)

```
/**
 * This is a TSDoc comment. It provides documentation for the function.
 *
 * @param parameter Description of the parameter. Type is `string`.
 * @returns Description of the return value. Type is `number`.
 */
function exampleFunction(parameter: string): number {
  // Implementation
  return parameter.length;
}
```

<h2>Write clear annotation comments</h2>

#### Better Comments

```
// * Emphasis
// ! Warning
// ? Question
// TODO: Task
// FIXME: Known bug
// HACK: Not a clean solution
// XXX: Major issue
```

#### VSCode extension to list annotation comments

[Todo Tree](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree)

<h2>Twelve-Factor App</h2>
The Twelve-Factor App is a methodology summarizing how modern web applications should be built, expressed as twelve best practices.<br>
It consists of the following twelve factors:

1. Codebase<br>
   One codebase tracked in version control, many deploys
2. Dependencies<br>
   Explicitly declare and isolate dependencies
3. Config<br>
   Store configuration in the environment
4. Backing services<br>
   Treat backing services as attached resources
5. Build, release, run<br>
   Strictly separate build and run stages
6. Processes<br>
   Execute the app as one or more stateless processes
7. Port binding<br>
   Export services via port binding
8. Concurrency<br>
   Scale out via the process model
9. Disposability<br>
   Maximize robustness with fast startup and graceful shutdown
10. Dev/prod parity<br>
    Keep development, staging, and production as similar as possible
11. Logs<br>
    Treat logs as event streams
12. Admin processes<br>
    Run admin/management tasks as one-off processes

<h1 id="package-principles">Package Principles</h1>
Package principles are six guidelines for designing packages in software development.<br>
These principles help make packages reusable and maintainable.

<h2>Reuse-Release Equivalence Principle</h2>
Only reuse what is released, or if you reuse it, release it.<br>
In other words, classes within a package should be either all reusable or all not reusable.<br>
Avoid half-baked releases; only use fully released artifacts.<br>
Using partially released artifacts risks unexpected changes in your code.

<h2>Common-Reuse Principle</h2>
Emphasizes an all-or-nothing approach: when a released package changes, you either adopt all changes or none.<br>
Consumers cannot cherry-pick specific changes; if a package upgrade bundles both desired and undesired changes, users must choose between versions.<br>
This often stems from packages that contain too many responsibilities. Properly split packages so that only the necessary ones are exchanged, minimizing side effects.<br>
In application development, group classes with common functionality into the same package, ensuring high cohesion.

<h2>Common-Closure Principle</h2>
Classes within a package should be closed to the same kinds of changes.<br>
Ideally, a single change requires swapping only a single package.<br>
“Closed” means the responsibilities inside the package are self-contained.<br>
A common antipattern is a bloated `Common` package referenced by everything, making impact areas unpredictable.<br>
Group highly related classes together and separate classes that change for different reasons into different packages to improve predictability and maintainability.

<h2>Acyclic-Dependencies Principle</h2>
Package dependencies must not form cycles.<br>
Cyclic dependencies make debugging, releasing, and testing difficult. They can also be subtle at the package level (A uses B, B uses C, and C indirectly uses A).<br>
Design dependencies to be unidirectional, or encapsulate strong relationships within a package.

<h2>Stable-Dependencies Principle</h2>
Depend in the direction of stability.<br>
Depending on more stable packages minimizes the blast radius of changes.<br>
The key is to depend consistently on more stable packages. Here, “stable” means “hard to change.”<br>
Depending on unstable artifacts leaves you with no higher stability to rely upon.

<h2>Stable-Abstractions Principle</h2>
Stability and abstraction should be proportional.<br>
Highly stable packages should be more abstract; less stable packages can be more concrete.

<h1 id="code-principle">Coding Principles</h1>
<h2>SOLID</h2>
The SOLID principles are five fundamental guidelines widely adopted in object-oriented programming.<br>
They make software easier to understand, more flexible, and more maintainable.

#### Single Responsibility Principle<br>

Each module (a cohesive grouping of data and functions) should have a single responsibility.<br>
With a single responsibility, changes will have minimal impact.

#### Open-Closed Principle<br>

Software entities (classes, functions, modules, etc.) should be open for extension but closed for modification.<br>
Enable adding new functionality without changing existing code to ensure flexibility, reusability, and maintainability.

#### Liskov Substitution Principle<br>

Base types should be replaceable with their subtypes.<br>
Subtypes must behave as their base types to maintain predictability and extensibility.

#### Interface Segregation Principle<br>

Clients should not be forced to depend on interfaces they do not use.<br>
Prefer fine-grained interfaces so clients only depend on what they actually use, reducing unwanted coupling.

#### Dependency Inversion Principle<br>

High-level modules should not depend on low-level modules. Both should depend on abstractions.<br>
Abstractions should not depend on details; details should depend on abstractions.<br>
Depending on abstractions improves reuse across contexts.

<h2>KISS (Keep It Simple, Stupid)</h2>
Goal: Prefer simple solutions over complex ones.<br>
Reason: Redundant code and complex structures increase bugs and reduce maintainability.

<h2>DRY (Don’t Repeat Yourself)</h2>
Goal: Avoid duplicating code and logic; reuse instead.<br>
Reason: Centralize common functionality so changes happen in one place, preserving consistency.

<h2>YAGNI (You Ain’t Gonna Need It)</h2>
Goal: Do not implement features “just in case”; improve development efficiency by avoiding unnecessary work.<br>
Reason: Unnecessary features waste time and bloat the codebase, hurting maintainability.

<h2>SLAP (Single Level of Abstraction Principle)</h2>
Goal: Maintain a consistent level of abstraction within code blocks.<br>
Reason: Improves readability, comprehension, and maintainability.

<h2>Separation of Concerns</h2>
Goal: Split a system into independent parts based on distinct concerns or functionality.<br>
Reason: Improves modularity and constrains change impact to specific areas, enhancing maintainability and extensibility.

<h2>Leaky Abstraction</h2>
Goal: Minimize leakage of implementation details through abstractions.<br>
Reason: When abstractions leak, consumers face unpredictable behavior and surprises.

<h1 id="review">Review</h1>
Code review uncovers bugs (mistakes, issues) that are hard for the author to notice and helps improve quality by bringing another perspective.<br>
It also facilitates knowledge sharing through discussions between reviewer and reviewee.<br>
Establishing shared evaluation criteria (guidelines) maintains consistent quality.

## Review Guidelines

| Perspective   | Summary                                 | Details                                                                                                                      |
| ------------- | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Design        | Architecture, design, design principles | Is the architecture/design consistent as an application? Are responsibilities and behaviors appropriate for the application? |
| Functionality | Meets functional requirements           | Does it behave as intended? Any concerns about communication volume or performance?                                          |
| Simplicity    | Ease of understanding                   | Is the code readable? Is the behavior as simple as possible to achieve the goal?                                             |
| Test          | Tests exist and are appropriate         | Are appropriate automated tests present? Do they provide sufficient quality assurance?                                       |
| Naming        | Naming for classes, methods, variables  | Are names clear and responsibility-oriented? Any grammar or typo issues?                                                     |
| Style         | Code style                              | Does the style conform to language conventions?                                                                              |
| Comment       | Comments                                | Are comments clear and useful? Are documentation/annotation comments appropriate?                                            |
| Document      | Documentation                           | Are related documents updated? Is the content appropriate?                                                                   |

[We refer to Google’s Engineering Practices documentation.](https://fujiharuka.github.io/google-eng-practices-ja/ja/review/)

## Remediation Priority Guidelines

| Tag    | Meaning                     |
| ------ | --------------------------- |
| MUST   | Must fix                    |
| SHOULD | Nice to have or minor       |
| IMO    | Reviewer’s opinion          |
| Q      | Questions for clarification |

## How to file review comments

Combine the eight review perspectives above with the four priority tags as prefixes when leaving comments.

#### Example

MUST(Design): The class has multiple responsibilities, violating the Single Responsibility Principle.

<h1 id="test">Testing</h1>
Always write relevant tests when adding new features or modifying existing ones.<br>
Merge only after all tests pass.

<h1 id="document">Documentation</h1>
Keep development documents and design specs up-to-date.

<h1 id="git-operation">Git Operations</h1>
<h2>Branching Strategies</h2>

### Git-flow

A branching model for long-term development and release management.

| branch     | Description                       |
| ---------- | --------------------------------- |
| main       | Production                        |
| develop    | Ongoing development               |
| release    | Next release candidates           |
| feature/\* | Feature development and bug fixes |
| hotfix/\*  | Bug fixes for production          |

### GitHub-flow

Simple and flexible branching strategy.

| branch     | Description      |
| ---------- | ---------------- |
| main       | Production       |
| feature/\* | Working branches |

### GitLab-flow

Combines Git-flow and GitHub-flow.

### Trunk-Based Development

Encourages frequent updates and direct development on the `main` branch (trunk), emphasizing continuous and frequent integration.

<h2>Basic branch rules</h2>
No direct pushes to `main`<br>
One branch per feature as a rule<br>
Branch off from a `feature` branch for work<br>
Delete working branches after merging<br>
Prefer code review (have someone review your changes)

<h2>Issues & Pull Requests</h2>
Describe specific work such as tasks, bugs, and new features in Issues and work based on them.<br>
When work is complete, create a Pull Request and request reviews.

<h2>Commit Messages</h2>
Use prefixes to clearly communicate what changed.

### Prefixes (Commit message style)

| Prefix         | Description                                 |
| -------------- | ------------------------------------------- |
| init           | First commit                                |
| chore          | Changes to build tooling or docs generation |
| add            | Add (files, features)                       |
| feat, feature  | Add (features, files)                       |
| update         | Non-bug functional changes                  |
| perf           | Performance improvements                    |
| refactor       | Refactoring                                 |
| change         | Specification/behavior changes              |
| fix            | Bug fixes                                   |
| remove, delete | Remove (files, features)                    |
| revert         | Revert changes                              |
| test           | Add or adjust tests                         |
| docs           | Documentation-only changes                  |
| merge          | Merge branches                              |
| sleep          | I was sleepy                                |

### Prefixes (Short)

| Prefix         | Description               |
| -------------- | ------------------------- |
| add            | Add (files, features)     |
| remove, delete | Remove (files, features)  |
| update         | Non-bug functional change |
| fix            | Bug fix                   |

#### Commit message examples

- init
- chore: Add React and dependencies
- add: Implement user registration
- sleep: I'm so sleepy

<h2 id="release-control">Release Control (Feature Flags)</h2>
Feature Flags are mechanisms that allow you to toggle system behaviors (features) on and off dynamically without code changes.
Feature flags improve development efficiency, reduce risk, and increase user satisfaction.

Note: Distinct from Feature Flags, there are also [Future Flags](https://remix.run/blog/future-flags)

#### Gradual rollout of new features

- Expose in-development features to a subset of users for testing and feedback, then roll out gradually
- Toggle features per user to conduct A/B tests or multivariate tests

#### Fast rollback

- Disable features quickly without waiting for code changes if issues occur
- Minimize impact and reduce user-facing problems via quick rollbacks

#### Safely introduce risky changes

- Deploy to production and enable features after confirming impact
- Roll back quickly without code changes if problems arise

#### Examples

- Beta-release a new UI design to specific users
- Temporarily unlock paid features for free-plan users
- Control feature visibility by region or device
- Temporarily disable features while fixing bugs

#### Sample code

```
export const Page = () => {
  if (featureFlag) {
    return <NewFeature />
  } else {
    return <CurrentFeature />
  }
}
```

<!--
<h1 id="css-design">CSS Design</h1>

- BEM
- OOCSS
-->

<h1 id="team-building">Team Building</h1>
<h2>Optimal team size (Two-Pizza Rule)</h2>
The “Two-Pizza Rule,” advocated by Jeff Bezos, suggests the ideal team size is about 4–8 people—small enough to be fed by two pizzas. The goal is to increase meeting productivity.
The idea is that the more participants there are, the lower the productivity. Keeping the team small preserves creativity and efficiency.

#### Details

The more participants in a meeting, the lower the productivity. Limit participants to a number that can share two pizzas. Large meetings can hurt creativity.

#### Application

In large organizations, even if individual teams are small, autonomy and productivity can be lost. When applying this rule, consider team autonomy and mission.

#### Running meetings

Appoint a facilitator, set basic rules, and ensure the agenda is relevant to all participants. This strategy helps improve meeting efficiency and productivity.

<h2>When to ask questions (Google AI team’s 15-minute rule)</h2>
The “15-Minute Rule” adopted by Google’s AI team provides an efficient approach to problem solving.

#### Details

1. Try to solve the problem yourself for the first 15 minutes.
2. If unresolved after 15 minutes, ask someone for help.

#### Purpose

The goal is to optimize time and encourage efficient problem solving.
Skipping the first step wastes others’ time; skipping the second wastes your own time.

#### Application

Use this as a guideline; adjust times and rules to fit the situation.

<h2>How to ask questions</h2>
When asking questions, explicitly state what you tried and what you researched to make it easier for others to help.

### Tips for asking questions

#### Asking

1. Use the most appropriate channel. Do not cross-post the same message to multiple channels.
2. Don’t ask for permission to ask; just ask. Provide as much detail as possible.
3. Research first. Search documentation and the web; spending time to find answers yourself is great learning.
4. If answers will take time, create a thread. This avoids confusing the main channel and allows parallel discussions. Likewise, reply with a thread if you answer with more questions.
5. Respect people’s time.
6. Don’t DM people for help—even if they’ve helped you before. Ask in public so everyone benefits.

#### Sharing code

There are two main ways to share code when needed:

1. If the code is short, use Markdown code fences.
2. If it’s long, share a GitHub repository or Gist link.

#### Do not post images of code or terminal output

Images are hard to read and prevent copying text, making it difficult to help.
Use screenshots only to show visual issues in the browser.

#### Tips for structuring questions (PREP method)

The PREP method stands for Point, Reason, Example, Point—an effective communication technique for conveying opinions and ideas. Steps:

1. Point: State your conclusion or main point first.
2. Reason: Provide the reasons supporting your conclusion.
3. Example: Provide concrete examples or evidence.
4. Point (again): Restate your main point to reinforce the message.

<h1 id="reference">References</h1>

- [Google Styleguide](https://github.com/google/styleguide/tree/gh-pages)
- [Twelve-Factor App](https://12factor.net/)

<h1 id="template">Useful Templates</h1>
Provide reusable templates (issue/PR templates, architecture templates, etc.).
Coming soon. Contributions welcome.

<h1 id="deals">Deals</h1>
Curated discounts or offers useful for developers.
Coming soon. Contributions welcome.

<h1 id="contributing">Contributing</h1>
Contributions are welcome! Please open an Issue first to discuss major changes, then submit a Pull Request.

- Follow the guidelines in this repository when proposing edits
- Use clear commit message prefixes (see Commit Messages)
- Keep documentation updated

<h1 id="code-of-conduct">Code of Conduct</h1>
Please read our [Code of Conduct](./CODE_OF_CONDUCT.md).

<h1 id="authors">Authors</h1>
See [AUTHORS](./AUTHORS).

<h1 id="license">License</h1>
Distributed under the [MIT License](./LICENSE).
