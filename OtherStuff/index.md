# But what about all the other stuff?

You'll have noticed that there are a number of unanswered questions from our original problem statements. In fact everything other than Eventual Consistency.

It became apparent as I explored solutions for eventual consistency that actually, within that narrow problem domain, the other statements had no bearing, and were independent.

The solution proposed decouples our synchronising mechanism from our data fetching/caching layers, which I think makes sense as it allows us to change patterns, tech and general approach to data fetching/caching in the future without having to rethink how we remain consistent with the server.

However, those things are still issues obviously, and should be addressed as a separate effort. Arguably though, those are much easier problems to solve, and there are many good, and well documented solutions / patterns for these issues within the modern React ecosystem.

<br />

Some useful reading for approaching these solutions:

### **Options for dedicated data fetching / caching**

- Tanstack Query (formerly React Query) - https://tanstack.com/query/v4/docs/react/examples/react/auto-refetching

- SWR - https://swr.vercel.app/
  <br /> Another industry standard lightweight alternative to React Query.

- Redux Toolkit Query - https://redux-toolkit.js.org/rtk-query/overview#motivation
  <br/>An Alternative to React Query, but built on top of Redux.

- Tanstack Router - https://tanstack.com/router/v1
  <br/>An interesting intersection between nested routing (e.g Wouter / React Router) and Data fetching/caching (e.g React Query / SWR).
  <br />It essentially allows you to do route based data fetching (with support for multiple simoultaneous request per route), with built in caching.
  <br />This library is particularly insteresting for us due to the ability to pre-fetch multple endpoints, and have a single loading state for multiple requests, for a given route.
  <br /> Sadly it's still VERY early days in development and not really production ready, but one to watch.

NOTE: All of the solutions would allow us to use a hooks based API for triggering fetches and subscribing to the data cache, allowing us to reduce the dense nesting and eradicate the FaaC pattern from the codebase.

### **Options/alternatives for global state management**

Once we have switched out the over use of Redux for data synchronisation to a dedicated library, then in theory any remaining global state should be relatively light weight. We should be able to potentially completely remove raw redux from our codebase. Options include

- Zustand - https://github.com/pmndrs/zustand
  <br /> Incredibly simple/clean, but powerful state mangement library with a hooks based API

- Easy Peasy - https://easy-peasy.vercel.app/
  <br /> Another great simple/clean, but powerful state management library with a hooks based API, this one is slightly more powerful than Zustand IMO, and is built on top of Redux. Giving you the power of the Redux tooling eco system, without any of the maintenance, boilerplate or code smell.

- Load more great alternatives - https://www.libhunt.com/r/zustand

[Home ->](/README.md)
