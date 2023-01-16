# ADR-Achieving-Eventual-Consistency

This technical document is primarily an investigation into how we can achieve eventual consistency between the FE and BE within the Ada platform given the CQRS + Event Sourcing architecture of the BE.

Additionally to address architectural/technical issues within the FE that exist as a consequence of the current design patterns around data fetching, storage and sharing.

<br />

## Table of Content

1. [Assumptions](#Assumptions)
2. [Additional Reading](#Additional_Reading)
3. [Overview](./Overview/1.Background.md)
   - [Background](./Overview/1.Background.md)
   - [Problem Statements](./Overview/2.Problems.md)
   - [Solution Aims](./Overview/3.Aims.md)
4. [Data Synchronisation](./DataSynchronisation/1.CurrentProblem.md)
   - [Current Problem](./DataSynchronisation/1.CurrentSolution.md)
   - [Possible Solutions](./DataSynchronisation/2.PossibleSolutions.md)
     1. [Server Wait ❌](./Solutions/1.ServerWait.md)
     2. [Read from Primary after Write ❌](./Solutions/2.PrimaryRead.md)
     3. [Client Polling (After Write) ❌](./Solutions/3.PollAfterWrite.md)
     4. [Push to Client (Webhooks) ✅❓](./Solutions/4.PushToClient.md)
     5. [Continuous Polling (Pseudo Webhooks) 🤔❓](./Solutions/5.ContinuousPolling.md)
   - [Webhooks & AWS](./DataSynchronisation/3.WebhooksAndAWS.md)
5. [Proposed Solution](./ProposedSolution/1.Overview.md)
   - [Overview](./ProposedSolution/1.Overview.md)
   - [Client Architecture](./ProposedSolution/2.ClientArchitecture.md)
   - [Server Architecture](./ProposedSolution/3.ServerArchitecture.md)
   - [Outstanding Questions](./ProposedSolution/4.OutstandingQuestions.md)
   - [Rollout Plan](./ProposedSolution/5.RolloutPlan.md)
6. [But what about the other stuff?](./OtherStuff/index.md)

<br />

## Assumptions

I have assumed that anyone reading this document

- is familiar with the current architecture of the Ada platform
- has a reasonable understanding of the CQRS / Event Sourcing patterns
- understands the resultant issue of eventual consistency when using a decoupled Read Projection as the primary data source for driving the UI within a CQRS / Event Sourcing architecture.

<br />

## Additional Reading

If you are unfamiliar with any of the above, here are some useful articles to help better understand the problem domain:

- CQRS Pattern - https://learn.microsoft.com/en-us/azure/architecture/patterns/cqrs
- Event Sourcing Pattern - https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing
- More on Event Sourcing - https://martinfowler.com/eaaDev/EventSourcing.html
- The problem of Eventual Consistency - https://codeopinion.com/eventual-consistency-is-a-ux-nightmare

<br />

[Next - "Overview: Background" ->](./Overview//1.Background.md)
