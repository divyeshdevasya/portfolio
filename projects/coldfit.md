# Coldfit

**Configurator / Personal concept**

A configurator for refrigerated vehicles that checks a choice against the load and the rules before it asks for a quotation.

![Conceptual workflow](../assets/coldfit.svg)

*Illustrative diagram, not a product screenshot or implementation blueprint.*

## Problem

Buyers of refrigerated vehicles usually pick a body size first and find out later that the pallets do not fit, the payload is too low, the chassis is not offered in that weight class or a different licence applies. A configurator that only lists options leaves that checking to a sales conversation.

## Project scope

A bilingual web configurator. The user states the load (pallets and payload), then chooses temperature class, body size, chassis, powertrain and equipment. A fit check updates live: pallet positions, a likely payload band, external width and height against legal limits, licence and tachograph notes, ATP class and chassis compatibility. Failed checks offer a one-click fix. The user can save and share a configuration, print a specification or send a quotation request; a token-protected page lists the requests.

**Technical areas:** Next.js / React / TypeScript / Cloudflare D1 / Drizzle

## Engineering decisions

- Keep the rules engine a set of pure functions over a typed catalog, so every check is unit-tested without a browser or a database.
- Label every fact as published (law or standard), typical (public manufacturer information) or estimate, and show payload and dimensions as ranges, never as single exact numbers.
- Combine independent component-mass uncertainties as a root of summed squares to give a likely band rather than a worst case.
- Pack pallets with a two-block guillotine search and test it against hand-counted layouts and monotonicity.
- Version the configuration schema and upgrade old saved links on read, so earlier shared configurations keep working.
- Protect the quotation form with a hidden field, a timing check, per-address rate limiting on a salted hash that is cleared after 24 hours, explicit consent and no third-party scripts.
- Disable the admin interface until a long secret is set, and compare it in constant time.

## Outcome

A working application with 22 unit tests for the rules engine and schema, 74 API checks and a 27-check browser flow, verified in German and English from 360 to 1440 px. A hosted deployment has not been run.

## Limits and context

The catalog is a planning model, not supplier data: chassis weight classes are rounded from public information and payload and dimensions are estimates. Nothing in it is an offer, an approval or a certification. The legal text describes what the application does and has not been reviewed by a lawyer. Implementation and any manufacturer reference remain private.

[Back to portfolio](../README.md)
