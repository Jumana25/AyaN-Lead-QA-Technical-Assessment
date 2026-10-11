# Task 5 — Quality Strategy & Release Judgement

## 5.1 — Go / No-Go Recommendation

**Recommendation: No-go for the current scope until the release risks have been assessed and acceptable quality criteria are met.**

This situation should not have reached this stage without earlier intervention. With two critical defects in a shared service, a regression pass rate of 68%, incomplete UAT, and insufficient testing of the newly deployed FX integration, confirming that QA is green would be misleading.

I would discuss the risks with the development leads and delivery management, review the available unit test results against the team's established benchmarks, and assess the impact of the open defects on the release. I would also propose reducing the release scope by deferring features where feasible rather than compromising quality.

The final decision should follow the established release governance process, involving QA, development, delivery, and the client, with the risks and any accepted exceptions documented.

## 5.2 — Next 72 Hours

I would prioritize activities as follows:

1. **Assess release scope and risks:** Align with stakeholders on business priorities and identify features that can be safely deferred. Involve developers in investigating critical defects and supporting testing.
2. **Investigate regression failures:** Assign the two experienced QA engineers to investigate pipeline failures while guiding the newer engineers through manual execution and test design. Failures must be classified based on evidence rather than dismissed as flaky.
3. **Prioritize API testing:** Run the full API suite, focusing on the transfer journey, transaction correctness, balances, and FX integration. Daily API regression should already be part of the team's routine, assuming a stable testing environment.
4. **Perform targeted end-to-end validation:** Run sanity checks for critical UI journeys and coordinate with the client to complete UAT, prioritizing business-critical scenarios.
5. **Reassess release readiness:** Review the results, outstanding defects, and residual risks with stakeholders before making the final recommendation.

**What I would drop:** Full UI regression for this release, replacing it with targeted end-to-end sanity checks while retaining full API regression. This reallocates limited time toward validating business logic and integration risks.

## 5.3 — Communication

**To the delivery manager:** I would respond in writing that QA is not green, explain the evidence behind that status, and present the proposed mitigation plan, release options, and outstanding risks. I would not confirm a status that the available evidence does not support.

**To the client:** I would communicate the risks transparently, including the incomplete UAT, regression results, FX integration coverage, and relevant shared-service defects. I would propose scope reduction or postponement where necessary and explain what evidence is needed to support release readiness. The level of detail would depend on the client's engagement, but the facts and risk assessment would remain consistent.

Neither audience should receive a misleading assurance or a different assessment of the underlying quality risks.

## 5.4 — Preventive Actions & Metrics

I would introduce the following practices:

* **Daily API regression:** Integrate the suite into the team's routine, with failures investigated and classified rather than repeatedly ignored.
* **Regression failure ownership:** Assign responsibility for investigating flaky tests, tracking their root causes, and preventing known failures from becoming accepted noise.
* **Earlier UAT coordination:** Agree on UAT scope, ownership, and completion milestones with the client well before the release window.
* **Integration testing gates:** Require meaningful positive and negative testing after integration deployments, particularly for financial calculations and shared services.
* **Defined release governance:** Establish explicit quality gates and a documented risk-acceptance process involving QA, development, delivery, and the client.

I would use Jira dashboards to make the following visible to the client:

* **Regression health:** Pass rate and outstanding failures, with flaky tests distinguished from genuine product defects.
* **Defect status:** Open critical/high defects and their assessed release impact.
* **UAT progress:** Execution and pass rates for the agreed business scenarios.

I would not use **the number of test cases executed as a standalone productivity metric**, because it rewards quantity rather than meaningful coverage, risk reduction, or test effectiveness.
