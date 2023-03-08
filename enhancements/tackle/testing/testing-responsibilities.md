---
title: testing-responsibilities
authors:
  - "@aufi"
reviewers:
  - TBD
approvers:
  - TBD
creation-date: "2023-03-07"
last-updated: "2023-03-07"
status: provisional|implementable|implemented|deferred|rejected|withdrawn|replaced
see-also:
  - "/enhancements/testing/high-level-summary.md"
  - https://github.com/konveyor/enhancements/pull/98
---

# Konveyor testing responsibilities

## Release Signoff Checklist

- [ ] Enhancement is `implementable`
- [ ] Design details are appropriately documented from clear requirements
- [ ] Test plan is defined
- [ ] User-facing documentation is created

## Summary

Testing of Konveyor is critical to keep its quality, release stability and happyness of community. In order to accomplish that, it is needed to create, execute and maintain several kinds of tests like end-to-end and components-specific test suites.

This enhancement should provide an introduction to Konveyor project testing strategy and define basic responsibilities for community members including developers as well as QE.

## Motivation

As we build an upstream community project that consists of multiple components, it is needed to ensure quality and stability of the project. One of important parts to achieve this is to have a test suite.

There are multiple level of tests like unit, integration or end-to-end, those could be executed on several levels from a single component unit tests to the Konveyor end-to-end UI test suite executed by automated CI.

The motivation for this enhancement is to do it in the most effective and engineers-friendly way.

### Goals

The main goal is to have a consistent test suite covering most of Konveyor application features that can be executed automatically and together with component tests, results will be reported to Konveyor CI.

An important part of this effort is to set expectations and basic responsibilities for Konveyor upstream community members regarding to test creation, execution and maintenance.

### Non-Goals

Cover downstream testing.

## Proposal

Let's start with kinds of tests relevant for us:
- Component/repository specific **unit tests**
  - Tests **logic** of a single Konveyor component (hub, UI, …), doesn’t require running whole Konveyor installation or other components (like Keycloak) to be executed, but either doesn’t need it or mocking it.
  - Test technology/framework depends on technology used in a given component.
- Component/repository specific **integration tests**
  - Tests **logic** of a single Konveyor component (hub, UI, …), but requires other Konveyor components to be running in order to pass the test (e.g. testing addon via requests to Hub to trigger analysis).
- Konveyor suite **end-to-end tests** (with UI or API)
  - Tests basic **use-cases** of the Konveyor tool (scenarios which real users would expect to be working).
  - Requires running Konveyor installation and covers functions of multiple components.

These tests should be executed and maintained as described in following section.

### Responsibilities

#### Overview matrix

| Kind of test | Primary Responsible | Presence | Executed on | Executed from | Source code in |
|---|---|---|---|---|---|
| **unit** | Developers | optional | Component | PRs&push | Component repo |
| **integration** | Developers | required | Component+Konveyor | PRs&push | Component repo |
| **E2E** | QE | required | Running Konveyor | time-based schedule | E2E test suite repos |

#### More specific matrix as a starting point for Konveyor Hub and E2E tests

| Kind of test | Primary Responsible | Description | Source code | Triggered by |
|---|---|---|---|---|
| **integration** Hub | Hub developers | REST API coverage tests, maybe addons, [more](https://github.com/konveyor/tackle2-hub/discussions/241) | https://github.com/konveyor/tackle2-hub/... | PR&push |
| **integration** addon-windup | Addon developers | Bash-scripted windup analysis | https://github.com/konveyor/tackle2-addon-windup/blob/main/hack/test-e2e.sh | PR&push |
| **E2E** API | Developers&QE | Golang API test suite (WIP) | https://github.com/konveyor/go-konveyor-tests | time-based schedule |
| **E2E** UI | QE | Existing QE-maintained UI test suite using cypress framework | https://github.com/konveyor/tackle-ui-tests | time-based schedule |



### What Konveyor org expects from its components
- Decide if unit tests are relevant for given component, if so, write it and maintain it.
- Be primarily responsible for maintaining component integration tests.
- Setup test actions on their components repositories and report it to Konveyor CI repo.

### What Konveyor components should expect from Konveyor org
- Provide tools for automated Konveyor installation setup (locally as well as with github actions) ready for running their integration tests on PRs (use Konveyor CI repo as a starting point).
- Provide working&stable Konveyor builds (partially ensured by e2e tests).

### Execution and project status

Konveyor CI repository is at https://github.com/konveyor/ci, it doesn't execute test suites itself, it just display status of E2E or components tests runs.

Overall CI status is:
- GREEN if all E2E test suites and all reporting components tests are passing.
- YELLOW if all E2E test suites are passing, but some of components reporting tests are failing.
- RED if some of E2E test suites is failing.

### Implementation Details/Notes/Constraints [optional]

TBD technologies&resources to for re-use

### Security, Risks, and Mitigations

Upstream test suite must not contain any company internal information not customer data (not even as sample data).

## Design Details

### Test Plan

Open Konveyor upstream CI at https://github.com/konveyor/ci and see its status (green hopefully).

### Upgrade / Downgrade Strategy

Tests are dependent on Konveyor application, so might need to be branched/tagged and executed together and specifically for given Konveyor version.

No upgrade/downgrade actions for upstream test suite are expected.

## Implementation History

This is a follow-up on Dylan's Testing overview enhancement https://github.com/konveyor/enhancements/pull/98. 

## Drawbacks and Alternatives

Since testing could be considered as QE's responsibility, developers and Konveyor component maintainers don't need to care, so we might:
- not run upstream tests, leave it for downstream product builders OR
- not formalize upstream testing responsibilities too much to not make it over-engineered. 

## Infrastructure Needed

Github actions with Minikube should be enough for upstream tests executions.