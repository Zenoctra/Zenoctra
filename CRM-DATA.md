# Field-Service CRM: Data Integrity in a Live Application

[Portfolio](PORTFOLIO.md) / Field-service CRM

**Context:** A CRM used by a lawn-care business for customer records, quotes based on lot size, and call routing. The application uses MariaDB and a supporting service. The production source remains private.

**My role:** Requirements, technical direction, behavior review, and project coordination. AI tools and a contractor supplied the implementation code and detailed database/deployment mechanisms.

## 1. Import real records and keep them current

A quote form needs dependable parcel information, not plausible-looking sample data. I required real county parcel records, continuing monthly updates, and coverage of the business's service communities. I also raised cases involving community aliases and growing subdivisions.

The implemented import maps external fields into a common record, normalizes addresses, validates usable identifiers and lot sizes, and updates records without creating another copy on each run.

```mermaid
flowchart LR
    A[County parcel records] --> B[Map, normalize, validate]
    B --> C[Identify and upsert]
    C --> D[Application records and quoting]
```

I specified the data source, update requirements, and business edge cases. The AI/contractor chose and wrote the pagination, field mapping, batching, and upsert implementation. MariaDB was an accepted technology choice.

## 2. Separate property identity from service eligibility

The same street line can exist in different ZIP codes. Matching by an incomplete address can associate a quote with the wrong lot size. A provider can also return a nearby property rather than the one requested.

I directed the repair and challenged a proposed scope reduction that would have discarded useful, already-paid property information. The requirement was to retain that information safely while checking service eligibility separately.

The AI identified the specific key and matching defects; the contractor implemented the repair. The resulting identity includes the normalized street and ZIP, and matching checks the requested property more strictly.

An abstract illustration:

| Street line | ZIP | Expected identity |
| --- | --- | --- |
| SAME STREET LINE | ZIP-A | Property A |
| SAME STREET LINE | ZIP-B | Property B |

These are symbolic examples, not customer addresses. A shared street line alone must not cause the two records to overwrite each other.

## 3. Preserve live data during database changes

When a supporting database/update step did not travel with a deployment, I challenged a repair aimed only at that one database. I required an approach that would also handle later features.

The failure scenario I raised was concrete: a customer signs up, or a parcel import adds a property, after a local database copy is made. Deploying that copy must not erase the newer live record or introduce development-only rows.

I specified live-data preservation, exclusion of development-only data, and backup/recovery requirements. The AI and contractor supplied the deployment and recovery mechanics. Code rollback, schema changes, and restoring database rows are different operations; this work does not establish that every database change can be reversed automatically.

The release workflow also needed to let a contractor deliver updates without production-server access or deployment credentials held in GitHub. I specified those constraints and required the pull-based approach to be retained during later changes. AI developed the mechanism and the contractor wrote most of the current deployment/restore implementation.

## 4. Measure the effect of cost controls

Paid address lookups need spending controls, but a legitimate property manager might search several properties. I asked whether the system could show how often limits were encountered and whether useful customer inquiries were being blocked.

The AI acknowledged that its earlier plan did not capture that information and added event tracking and a daily SQL aggregation. The report distinguishes paid requests, cache hits, blocked requests, and related outcomes.

My contribution was identifying the measurement gap and requiring information to assess the business tradeoff. The AI supplied the event/schema/query implementation. Event counts do not by themselves establish measured dollar savings or reduced customer loss.

## Status and boundaries

The CRM has production use. This case describes an application database with batch imports and operational reporting. It does not claim warehouse experience, personal authorship of the SQL/TypeScript implementation, a zero-data-loss guarantee, or independently measured business improvements.

This page contains no production code, customer data, deployment configuration, server details, or credentials.
