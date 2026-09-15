# Service Booking: Frontend to API

**Full-stack / React and Python demonstration**

Exploring the boundary between a web interface and the backend that supports a service-booking workflow.

![Conceptual workflow](../assets/barber-fullstack.svg)

*Illustrative diagram, not a product screenshot or implementation blueprint.*

## Problem

User actions in the browser need consistent validation and data handling across the API and storage layer.

## Project scope

The project combines a React interface, a Python API and a relational data store. It provides a concrete example for discussing responsibilities across a full-stack application.

**Technical areas:** React / TypeScript / FastAPI / PostgreSQL

## Engineering decisions

- Keep browser interaction separate from backend business rules.
- Use an explicit API boundary between interface and data handling.
- Treat deployment configuration as a separate concern from application behavior.

## Outcome

A multi-layer web application demonstration with frontend, backend and database components.

## Limits and context

This case study describes the implementation scope. It does not certify a current production deployment or measured adoption.

[Back to portfolio](../README.md)
