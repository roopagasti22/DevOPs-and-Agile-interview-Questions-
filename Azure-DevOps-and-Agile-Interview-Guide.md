# Azure DevOps, Agile, and GitOps: Interview Guide

A practical guide to Agile work management, Azure DevOps, delivery pipelines, containers, and GitOps. The answers are written to be useful both for interview preparation and as a concise professional reference.

## 1. What is Azure Boards?

**Azure Boards** is the work-planning and tracking service in Azure DevOps. Teams use it to plan, prioritize, assign, and track work throughout an Agile or software-delivery lifecycle.

Common Azure Boards capabilities include:

- **Work items:** Track requirements, user stories, tasks, bugs, and other work.
- **Boards:** Visualize work in columns such as New, Active, and Done.
- **Backlogs:** Prioritize and organize work into product and iteration backlogs.
- **Sprints:** Plan time-boxed iterations, assign work, and monitor sprint progress.
- **Queries and charts:** Filter work items and report on status, ownership, and trends.
- **Dashboards:** Combine charts and widgets to provide a shared view of project health.

Azure Boards supports configurable processes, including Agile, Scrum, and CMMI. The available work-item types and their hierarchy depend on the selected process and project configuration.

## 2. What is Jira?

**Jira** is a work-management and issue-tracking platform from Atlassian. Software teams commonly use Jira to manage product backlogs, user stories, tasks, bugs, sprints, and Kanban workflows. Jira can also be configured for service management and other business workflows.

Typical Jira capabilities include:

- Configurable Scrum and Kanban boards.
- Backlogs, sprint planning, and issue tracking.
- Custom workflows, fields, and issue types.
- Reports and dashboards for team and project progress.
- Integrations with tools such as Confluence, Bitbucket, GitHub, and CI/CD services.

Azure Boards and Jira solve similar planning and tracking problems. The choice often depends on the team's existing ecosystem, integrations, administration preferences, and licensing requirements.

## 3. What is Trello?

**Trello** is a visual work-management tool built around boards, lists, and cards. A board usually represents a project or workflow; lists represent stages or categories; and cards represent work items.

For example, a team might use lists named **Backlog**, **In Progress**, **Review**, and **Done**, moving cards between them as work advances. Trello is often valued for its low setup effort and ease of use. It can support lightweight Agile workflows, but large or complex software-delivery programs may need the richer backlog, reporting, dependency, and development integrations available in Jira or Azure Boards.

## 4. What are Agile work items: Epic, Feature, User Story, Task, Bug, and Issue?

Work items are records used to describe and track work. Their exact names and parent-child relationships vary between products and process templates.

| Work item | Typical purpose | Example |
|---|---|---|
| **Epic** | A large business or product objective that may take multiple releases or teams to deliver. It is usually decomposed into smaller outcomes. | “Improve online purchasing experience” |
| **Feature** | A substantial capability that contributes to an epic and can usually be delivered through multiple stories. | “Allow customers to save payment methods” |
| **User story** | A small, user-focused requirement that describes value and can be completed within an iteration. | “As a returning customer, I want to use a saved card so that checkout is faster.” |
| **Task** | A specific piece of implementation, testing, design, or operational work. Tasks are often associated with a story or another parent item. | “Add saved-card selection to checkout UI” |
| **Bug** | A defect where actual behavior does not meet expected behavior. It should include reproducible details, impact, and relevant environment information. | “Checkout rejects an unexpired saved card” |
| **Issue** | A generic term for a tracked concern or unit of work. In Jira, “issue” is the general record concept and may refer to a story, task, bug, or other configured type. In other tools, “Issue” may be a specific type, so confirm the project's process. | “Investigate intermittent payment timeout” |

A common conceptual hierarchy is:

**Epic → Feature → User Story → Task**

Bugs and issues can be tracked at different levels depending on the team's process. Do not assume every tool uses this exact hierarchy: for example, Azure DevOps process templates differ, and Jira issue types and hierarchy can be configured.

### User-story quality

A useful user story communicates the user, desired capability, and benefit. Teams often add **acceptance criteria** to define the conditions that make the story complete. The INVEST checklist is a common quality aid: stories should be Independent, Negotiable, Valuable, Estimable, Small, and Testable.

## 5. How do you organize work items on an Agile board?

Organize work so that the board reflects the team's actual workflow and makes priorities and blockers visible:

1. **Define the outcome and backlog structure.** Capture larger goals as epics or equivalent items, then break them into deliverable features and stories.
2. **Write actionable stories.** Include user value, acceptance criteria, and links to relevant designs or requirements.
3. **Prioritize the backlog.** Order items by value, urgency, risk, dependencies, and team capacity.
4. **Plan the iteration.** Select ready items for the sprint or iteration, estimate or size them using the team's chosen method, and agree on a sprint goal.
5. **Break stories into tasks where useful.** Tasks should help the team coordinate and track implementation without turning the board into a burdensome checklist.
6. **Use columns that match real states.** For example: Ready, In Progress, Code Review, Testing, and Done. Keep the meaning of each state clear.
7. **Set work-in-progress limits if appropriate.** Limits can expose bottlenecks and encourage finishing work before starting more.
8. **Show ownership, blockers, and dependencies.** Use labels or fields consistently, and avoid relying on color alone to convey important status.
9. **Review and refine regularly.** Reorder the backlog, remove stale work, and check that “Done” follows the team's Definition of Done.

The board should help the team coordinate and improve delivery; it should not replace conversation or become a measure of individual productivity.

## 6. What are Azure DevOps dashboards?

**Azure DevOps dashboards** are configurable pages that bring together project or team information using widgets. They provide a convenient snapshot; they do not replace the underlying work items, pipeline results, or source data.

Dashboards can include widgets for items such as:

- Work-item queries, charts, and sprint status.
- Burndown, velocity, and cumulative-flow views.
- Build or release pipeline status.
- Test results and code-related metrics, depending on available services and configuration.

Teams can create dashboards for different audiences, such as a sprint team, engineering leads, or stakeholders. Good dashboards emphasize a small set of actionable indicators and link back to their source. Permissions determine who can view or edit a dashboard and its underlying data.

## 7. What are Azure Pipelines, and how do you create a pipeline?

**Azure Pipelines** is the Azure DevOps service for automating software build, test, and deployment workflows. A pipeline can run when code is pushed, a pull request is opened, a schedule is reached, or a pipeline is manually started.

Pipelines can use **YAML**, where pipeline configuration is stored as code in the repository, or the **Classic** visual designer. YAML is commonly preferred for new pipelines because it can be reviewed, versioned, and reused with the application code.

### Typical pipeline creation steps

1. **Prepare the repository.** Put the application code and, for YAML, a pipeline file such as `azure-pipelines.yml` in a supported repository.
2. **Create a pipeline.** In Azure DevOps, open **Pipelines**, choose **New pipeline**, select the repository provider, and authorize the required access.
3. **Choose or write a definition.** Select a suitable template or author YAML steps for installing dependencies, building, testing, and publishing outputs.
4. **Configure triggers.** Decide which branches and events should run validation and deployment. Pull-request validation and branch-based triggers are common.
5. **Select an agent.** Use a Microsoft-hosted agent or configure a self-hosted agent when the environment, network, or tooling requires it.
6. **Connect deployment targets securely.** Configure service connections, environments, variable groups, and approvals as needed. Avoid embedding credentials in YAML or source code.
7. **Run and inspect the pipeline.** Review logs and test results, fix failures, and verify published artifacts.
8. **Add deployment controls.** Use stages, environments, checks, and approvals to control promotion to test, staging, and production.

A basic continuous-integration pipeline validates changes and publishes an artifact. A delivery pipeline then deploys that artifact to one or more environments. Exact YAML and tasks depend on the language, build system, hosting target, and security requirements.

## 8. What are service connections, and how do you connect Azure DevOps to external services?

A **service connection** (also called a service endpoint in some contexts) is a configured, permission-controlled connection that lets an Azure DevOps project or pipeline authenticate to an external service. Examples include Azure subscriptions, container registries, Kubernetes clusters, cloud providers, and source-control or package services.

### Typical setup

1. Identify the target service and the minimum permissions the pipeline needs.
2. In Azure DevOps project settings, open **Service connections** and create a connection of the appropriate type.
3. Choose the available authentication method and provide or authorize the required identity and scope.
4. Restrict which pipelines can use the connection; grant access only to the intended projects and pipelines.
5. Reference the connection from the relevant pipeline task or deployment configuration.
6. Test access, monitor use, and rotate or revoke credentials when applicable.

Where supported, prefer **workload identity federation** or another short-lived, secretless authentication method over long-lived client secrets. If a secret is required, store and manage it through the service connection or an approved secret store, not in source control or plain-text pipeline YAML. Use least privilege and periodically review connection permissions.

## 9. What is GitOps?

**GitOps** is an operational approach in which Git repositories hold the desired state of systems, and automated software reconciles the live environment with that declared state.

A typical GitOps workflow is:

1. An engineer proposes a change to application or infrastructure configuration in Git.
2. Review, automated checks, and policy validation run before the change is merged.
3. A GitOps controller or deployment automation detects the approved desired-state change.
4. The controller applies the change to the target environment and continuously compares actual state with desired state.
5. If the environment drifts, the controller reports the difference and may reconcile it according to the configured policy.

GitOps is commonly used with Kubernetes and declarative configuration, but its principles can be applied more broadly. It improves traceability and repeatability, but requires secure repository access, sound change review, secrets management, and careful controls over automated reconciliation.

## 10. What are the advantages and disadvantages of DevOps?

DevOps is a set of practices and a cultural approach that brings development and operations together to deliver and operate software reliably. Its outcomes depend on the organization's implementation; adopting tools alone does not create DevOps.

### Advantages

- **Faster feedback and delivery:** Automated builds, tests, and deployments reduce manual handoffs.
- **More consistent releases:** Repeatable automation reduces environment-specific variation and avoidable errors.
- **Earlier defect detection:** Continuous integration and testing expose issues closer to when changes are made.
- **Shared ownership:** Development and operations collaborate on operability, reliability, and customer outcomes.
- **Improved recovery:** Monitoring, incident practices, and smaller changes can help teams detect and recover from failures faster.
- **Traceability:** Versioned code and pipeline history make changes easier to review and audit.
- **Continuous improvement:** Delivery and operational metrics can help teams identify bottlenecks and improve their process.

### Disadvantages and challenges

- **Up-front investment:** Automation, platform engineering, training, and process changes require time and money.
- **Learning and organizational change:** Teams may need to adopt new skills and work across established role boundaries.
- **Tooling complexity:** Too many disconnected tools or poorly maintained pipelines can increase operational burden.
- **Risk from automation:** A flawed pipeline or overly broad credentials can distribute a mistake quickly.
- **Maintenance requirements:** Tests, build definitions, deployment workflows, and infrastructure configuration need ongoing ownership.
- **Security and compliance demands:** Faster delivery still requires access control, secrets management, auditability, and appropriate approval gates.
- **Cultural pitfalls:** Measuring individuals by activity or enforcing a one-size-fits-all process can undermine collaboration.

DevOps is most effective when automation is paired with clear ownership, secure practices, useful feedback, and a culture of learning.

## 11. What is the role and importance of DevOps in full-stack development?

Full-stack teams work across user interfaces, APIs, services, databases, and deployment environments. DevOps practices help connect those layers into a reliable delivery lifecycle:

- **Continuous integration:** Build and test frontend and backend changes together where appropriate.
- **Quality checks:** Automate unit, integration, API, UI, security, and accessibility checks according to project needs.
- **Environment consistency:** Use containers, infrastructure as code, and configuration management to reduce differences between development, test, and production.
- **Coordinated releases:** Package related client, service, and database changes and deploy them in a controlled sequence.
- **Safe deployment:** Use environments, approvals, feature flags, staged rollouts, and rollback plans when suitable.
- **Observability:** Collect logs, metrics, and traces across browser, API, service, and infrastructure layers to diagnose end-to-end issues.
- **Operational feedback:** Feed production incidents and customer behavior back into planning and engineering decisions.
- **Security throughout delivery:** Apply least-privilege access, dependency checks, secret protection, and appropriate security testing.

This reduces the gap between building a feature and operating it. The goal is not simply to deploy more frequently; it is to deliver useful changes safely and learn quickly from their behavior.

## 12. What is the difference between Azure DevOps, Git, GitHub, and GitOps?

These terms are related but refer to different things:

| Term | What it is | Typical role |
|---|---|---|
| **Azure DevOps** | Microsoft's suite of software-delivery services, including Azure Boards, Repos, Pipelines, Test Plans, and Artifacts. | Plan work, host repositories, build and deploy software, and manage delivery workflows. |
| **Git** | A distributed version-control system. | Track and manage changes to source code and other files. |
| **GitHub** | A platform for hosting Git repositories and collaborating through pull requests, issues, automation, and integrations. | Collaborate on code and automate workflows, including through GitHub Actions. |
| **GitOps** | An operational practice that uses Git-managed desired state and automated reconciliation. | Make infrastructure and application deployment changes reviewable, traceable, and repeatable. |

Git is the version-control technology; GitHub is one platform that hosts Git repositories. Azure DevOps is a broader suite that also offers Git-based repositories. GitOps is a way of operating systems and can use a repository hosted on GitHub, Azure Repos, or another Git service. These tools and approaches can be used together.

## 13. What is the difference between Docker and containers? How do they help in DevOps?

A **container** is an isolated, runnable environment for an application and its dependencies. Containers share the host operating-system kernel, unlike traditional virtual machines, which generally include a separate guest operating system.

**Docker** is a platform and ecosystem for building, packaging, distributing, and running containers. It popularized a common container image workflow and includes tools such as the Docker CLI and Docker Engine. Docker is not synonymous with containers: container images and runtimes are also supported by other tools and standards, such as OCI-compatible tooling and containerd.

### How containers help DevOps

- Package application dependencies in a repeatable image.
- Reduce “works on my machine” differences across development, testing, and production.
- Run isolated services in local development and automated test environments.
- Make build artifacts portable across compatible container environments.
- Support scalable deployments when combined with an orchestrator such as Kubernetes.

Containers do not automatically make an application secure or production-ready. Teams still need to use trusted and maintained base images, scan and update dependencies, avoid embedding secrets, configure resource limits and health checks, and understand the host and runtime security model.

## 14. What is the DevOps process? How does it work, and what are the architectures of Azure DevOps and GitOps?

### The DevOps process

DevOps is a continuous lifecycle rather than a single linear methodology. A common representation is **Plan → Code → Build → Test → Release → Deploy → Operate → Monitor → Plan**:

1. **Plan:** Prioritize customer and business needs as epics, stories, defects, or other work.
2. **Code:** Implement changes in version control and collaborate through reviews.
3. **Build:** Integrate changes and create versioned, reproducible artifacts.
4. **Test:** Run automated and manual checks to assess correctness, performance, security, and other quality needs.
5. **Release:** Decide which validated artifact is ready for a target environment and apply required approvals.
6. **Deploy:** Promote the artifact through development, test, staging, and production environments.
7. **Operate:** Run the service, manage capacity and reliability, and respond to incidents.
8. **Monitor:** Observe service health and user experience using appropriate logs, metrics, traces, and alerts.
9. **Learn and improve:** Use feedback, incidents, and delivery data to refine the product and process.

Continuous integration automates frequent integration and validation of changes. Continuous delivery keeps changes in a deployable state and may require an approval before production. Continuous deployment automatically releases changes to production after they pass the defined controls. These terms describe different levels of automation, and teams should be clear about which one they practice.

### Azure DevOps architecture

Azure DevOps is a hosted or self-managed collection of services organized around an **organization** and **projects**. A project groups work, source, pipelines, and related configuration. The exact service availability and hosting options depend on the Azure DevOps offering and organization setup.

At a high level, a delivery flow may look like this:

```text
People and teams
      |
Azure DevOps organization
      |
Project
  |-- Boards: backlogs, work items, sprints, dashboards
  |-- Repos: Git source control and pull requests
  |-- Pipelines: build, test, publish, and deploy
  |-- Test Plans: test planning and tracking (when used)
  |-- Artifacts: package feeds (when used)
      |
Agents run pipeline jobs
      |
Service connections and environments connect to target systems
      |
Applications and infrastructure are deployed and monitored
```

In practice, a code change can be linked to a work item, reviewed in a pull request, validated by a pipeline running on an agent, published as an artifact, and deployed to an environment using controlled permissions and approvals. Organizations should design identity, permissions, network access, secrets, and audit controls for their specific risk and compliance needs.

### GitOps architecture

GitOps centers on a Git repository as the authoritative record of approved desired state, plus automation that applies and observes that state:

```text
Engineer
   |
   v
Pull request and review
   |
   v
Git repository: application and/or infrastructure desired state
   |                                  ^
   | change notification or polling   | status, drift, and reconciliation results
   v                                  |
GitOps controller or deployment automation
   |
   v
Target environment (for example, a Kubernetes cluster)
   |
   v
Running workloads and infrastructure
```

Depending on the implementation, a controller inside the target environment may pull approved state from Git and reconcile it, or a pipeline may apply changes after repository events and required checks. In the pull-based model, the cluster-side controller retrieves the desired state, which can reduce the need for external deployment systems to hold direct cluster credentials.

Application code and environment configuration may be stored in one repository or separated into multiple repositories. The choice depends on release cadence, ownership, access boundaries, and operational needs. Secrets should not be committed as plain text; use an approved secret-management approach and limit access to both repositories and deployment identities.

### Azure DevOps and GitOps together

Azure DevOps can host Git repositories, run CI pipelines, and provide planning, approvals, and delivery automation. A GitOps controller can then reconcile environment configuration from a Git repository. For example, an Azure Pipeline can build and test an application image, publish it to a registry, and propose a reviewed configuration change that updates the desired image version. A controller applies the approved change to the target environment.

The responsibility split should be explicit: pipelines build and validate artifacts; GitOps automation reconciles declared environment state; and people and policy controls govern what can be changed and promoted.

---

## Quick interview summary

- **Azure Boards, Jira, and Trello** help teams organize work, with different levels of structure and configuration.
- **Epics, features, stories, tasks, bugs, and issues** describe different scopes or categories of work; exact hierarchies vary by tool.
- **Azure Pipelines** automates build, test, and deployment workflows; **service connections** provide controlled access to external systems.
- **Git** is version control, **GitHub** is a collaboration platform, **Azure DevOps** is a delivery suite, and **GitOps** is an operating practice.
- **Docker** provides popular tools for working with containers; containers package applications in isolated, portable environments.
- **DevOps** combines collaboration, automation, and feedback to deliver and operate software reliably.
