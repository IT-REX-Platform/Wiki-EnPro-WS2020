# Deployment View

This page describes general thoughts and design decisions that were used to create the [Deployment Diagram](https://miro.com/app/board/o9J_ldsCOKg=/?moveToWidget=3074457352127621741&cot=12) (concept on Miro).

The [Component Model](./Application-Architecture--Implementation-View) was already designed with the thoughts of smaller scalable entities as components. These components are reused in the Deployment diagram. Because of that most components and especially databases are just deployed on their own logical node. Only the gamification services are deployed together on one node for now. This is subject to change because we haven't finally decided on how to split up these services (or if we want to split them up at all).
