# Data Workflow Portfolio

Selected independent projects by **Manuel Romero III**, focused on data ingestion, record identity, relational modeling, and validation.

These case studies explain the problem, the decisions I contributed, the implementation team's role, and the current limits of each project.

## Projects

| Case study | Main problem | Project technologies | Status |
| --- | --- | --- | --- |
| [Field-service CRM](CRM-DATA.md) | Turn external parcel records into dependable business data and protect live records during changes | MariaDB, SQL, TypeScript service | Production use; source private |
| [Scripture-to-music workflow](MUSIC-WORKFLOW.md) | Preserve published source structure while planning passages and organizing recordings | Python, CSV, PostgreSQL | Working components; audio-review prototype |
| [AI correction monitor](CORRECTION-MONITOR.md) | Define what should trigger a correction monitor and evaluate its detection behavior | Python, labeled conversation data | Research prototype; public research branch |
| [Sermon-editing prototype](SERMON-EDITING.md) | Reuse unchanged footage while encoding the transitions that need editing | Python, FFmpeg, structured transcripts | Prototype |

## Contributions and implementation

My contribution to the modern projects was workflow and data-model design, requirements, review, and project coordination. AI tools and paid contractors wrote the modern implementation code. Each case identifies the particular decisions I made and the work supplied by others.

The technologies above describe the projects' implementations. My current goal is an entry-level data engineering role in which I can develop hands-on SQL and pipeline implementation skills with an experienced team.

## Earlier hands-on programming

The [Unity movement prototype](https://github.com/Zenoctra/mdr180004_p03) preserves university-era C# source from 2022: custom acceleration and drag, directional calculations, camera movement, and wall-movement experiments built around Unity's `CharacterController`.

## Reading and source access

The CRM's production repositories and the local music/media working folders remain private. These are newly written case studies, not exports of those repositories. Diagrams and examples are explanatory; they contain no production records or private transcripts.

The correction-monitor study links to the relevant existing public source. The historical Unity project also has public source. Project statuses and limitations are stated on each case page.
