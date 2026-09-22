# Agent Identity Infrastructure

**Backend engineering / Reference implementation**

A reference system for treating an AI agent as an accountable actor while keeping a human or legal entity as the contractual principal.

![Conceptual workflow](../assets/agent-identity.svg)

*Illustrative diagram, not a product screenshot or implementation blueprint.*

## Problem

As agents start taking actions on a person's behalf, a merchant or platform needs more than "an API key was used." It needs to know which agent acted, who authorized it, under what delegation and scope, and whether a high-risk action required a human to step back in.

## Project scope

The system issues short-lived, platform-signed access tokens to agents that hold a valid human-to-agent delegation, checks each request against explicit scopes and transaction limits, requires one-time human confirmation for high-risk actions, and keeps an append-only-style audit trail linking every merchant action back to the delegation and human that authorized it. It is deliberately not a browser-fingerprinting or User-Agent detection approach.

**Technical areas:** TypeScript / Fastify / PostgreSQL / Redis / Ed25519 signatures / JWT

## Engineering decisions

- Separate "who signed this request" (the agent's cryptographic identity) from "who authorized this agent" (the human delegation).
- Make delegations versioned and immediately revocable, rather than long-lived static credentials.
- Use short-lived platform-signed tokens plus replay protection instead of trusting a bearer credential indefinitely.
- Require explicit step-up human confirmation for actions above a defined risk threshold.

## Outcome

A runnable reference implementation with unit tests, a full end-to-end demo agent, and Docker Compose setups for local development and a TLS-terminated server deployment. It demonstrates the authorization model rather than integrating with a real merchant.

## Limits and context

This is a reference implementation of the authorization model, not a certified identity or compliance product. Production adoption would need its own threat modeling, key management, and integration work per merchant.

[Back to portfolio](../README.md)
