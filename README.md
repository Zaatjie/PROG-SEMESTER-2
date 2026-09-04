# RaceDay

## Description

RaceDay is a web-based system for organising and taking part in running
events. Organisers can create events (e.g. a city marathon or a trail run),
split each event into categories such as a 5km Fun Run or a Half Marathon,
and capture finish times once the event has taken place. Participants can
browse upcoming events, enrol in the categories they want to run, and view
their results once they're published.

The system is built around six core entities — **Users**, **Events**,
**Categories**, **Enrolments**, **Results**, and **Payments** — documented in
full in [`/docs/erd.png`](docs/erd.png). The planned API surface is
documented in [`/docs/api-endpoint-plan.md`](docs/api-endpoint-plan.md) (also
available as [`/docs/api-endpoint-plan.docx`](docs/api-endpoint-plan.docx)),
and the database schema with seed data is in
[`/docs/schema.sql`](docs/schema.sql).

## Roles

The system supports two user roles, both stored in the same `Users` table
and distinguished by a `Role` field.

### Organiser

An Organiser creates and manages events. They can:
- Create, update, and delete their own events
- Add, update, and remove categories within their events
- View who has enrolled in each category
- Capture and update race results once an event has taken place

An Organiser can only manage the events and categories they created — they
cannot edit another Organiser's event.

### Participant

A Participant takes part in events. They can:
- Browse and search all published events and categories
- Enrol in a category for an event they want to run
- View and cancel their own enrolments
- View their own results once an Organiser has published them

A Participant cannot create events or capture results — those actions are
restricted to the Organiser who owns the event.

## Repository Structure

```
/docs
  erd.png                    - Entity Relationship Diagram
  api-endpoint-plan.md       - API endpoint plan (Markdown)
  api-endpoint-plan.docx     - API endpoint plan (Word)
  schema.sql                 - Database schema + seed data (SQL Server)
/.github/workflows
  validate-docs.yml          - CI check that /docs contains the required files
```

## CI/CD

A GitHub Actions workflow ([`validate-docs.yml`](.github/workflows/validate-docs.yml))
runs on every push and pull request to `main`. It checks that the `/docs`
folder exists and that it contains `erd.png`, `api-endpoint-plan.md`, and
`schema.sql`.

**Successful build:**

_Screenshot pending — add `docs/ci-success.png` once you have pushed this
repository and the workflow has run successfully, then replace this note
with `![CI/CD successful build](docs/ci-success.png)`._
