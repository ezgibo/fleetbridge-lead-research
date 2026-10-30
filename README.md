# FleetBridge Lead Research

FleetBridge explores how structured company data and source evidence can support B2B lead research for a fictional fleet software vendor. It addresses the work of turning carrier records and scattered public information into reviewable company briefs. The notebook combines SQLite lookups, Gemini-generated JSON, deterministic validation, and human source review to keep reported facts, sourced observations, and sales hypotheses separate.

## Key features

- Retrieve company records by USDOT identifier using a parameterized, read-only SQLite lookup.
- Generate structured research briefs from supplied evidence excerpts with URLs, exact quotes, confidence labels, missing information, and uncertainty flags.
- Check brief structure, company identity, URL formatting, evidence matches, and consistency with database values.
- Compare power units, driver counts, and mileage year against an FMCSA SAFER company snapshot, preserving source evidence and flagging discrepancies.
- Configure Google ADK tools with guards that require database lookup before government-source research.
- Define bounded agent tests and save JSON research records, validation reports, source snapshots, and execution traces locally.
- Include synthetic validation and error-handling examples, plus sections for reviewing saved evaluation artifacts.

## Technologies

Python, Google Colab, SQLite, Google Gen AI SDK, Google ADK, Requests, Beautiful Soup, and Python's standard library. Later experimental sections also reference Ollama, Qwen, LiteLLM, and DuckDuckGo search through `ddgs`.

## Repository contents

```text
notebooks/fleetbridge_research.ipynb   Research workflow and experimental extensions
README.md                            Project scope, setup, and usage
.gitignore                           Secrets, datasets, and generated-file exclusions
repository-description.txt           Short GitHub repository description
```

The notebook preserves every original cell source. Saved outputs, execution counts, and session metadata have been removed for sharing. The supplied presentation was reviewed as context and excluded because it contains personal names. It also describes a broader system whose complete implementation is not included here.

## Installation

This is a Colab-oriented project snapshot. It requires external project assets and is not a self-contained application.

1. Download or clone this repository and open `notebooks/fleetbridge_research.ipynb` in Google Colab.
2. Supply an authorized local copy of `fleetbridge.db` through Google Drive. The notebook expects a `companies` table with fields including `DOT_NUMBER`, `LEGAL_NAME`, `DBA_NAME`, `PHY_CITY`, `PHY_STATE`, `POWER_UNITS`, `TOTAL_DRIVERS`, `MCS150_MILEAGE_YEAR`, and `score`. Pilot cells also expect the specific USDOT records referenced in the code.
3. Review the Drive paths before execution. The original notebook repeats project-specific paths in `DB_PATH`, `LOOKUP_DB_PATH`, and other cells. Point those paths to your own project assets in your working copy.
4. Add `GOOGLE_API_KEY` to Colab Secrets and allow notebook access. Never paste credentials into notebook cells or outputs.
5. Review the package checks and installation cells before running them. The notebook specifies `google-adk==2.7.1`, `google-genai==2.12.1`, and `google-auth==2.49.0` for the agent setup. These are recorded notebook versions, not a newly verified compatibility guarantee.

The notebook's model identifier is `gemini-3.8-flash`. Confirm that the identifier and quota are available to your account before making requests. No model requests were made while preparing this repository.

### External assets required by later sections

Several later cells import project files that were not supplied with this repository:

- `fleetbridge_validator_v1.py`, `test_fleetbridge_validator_v1.py`, and `signal-definitions-v1.md`
- `fleetbridge_storage_v1.py`, `fleetbridge_local_database_v1.py`, `fleetbridge_discovery_agent_v1.py`, and `fleetbridge_evaluation_v1.py`
- The evaluation handoff archive, its result files, and `finalize_phase3.py`

Provide those original assets separately to use the corresponding sections. Their implementations and test suites are not included here. Database and evaluation files are intentionally excluded from version control.

## Usage

1. Read the notebook headings and status notes before executing cells. This is a development record with separate experiments, not a single validated “Run all” workflow.
2. Mount Drive and inspect the database. Review the selected records and paths before generation.
3. For source-assisted briefs, review the evidence pack, configure Gemini through Colab Secrets, generate the JSON brief, and run the validation cells.
4. Inspect each URL and quote manually. Structural validation cannot prove that an evidence quote supports a claim. Keep source conflicts and potential fleet needs explicitly marked for review.
5. For the government comparison, load the read-only lookup and SAFER helper definitions. Run the synthetic tests before the single direct lookup. Review the saved JSON and HTML snapshot.
6. Run live ADK tests only after reviewing their prerequisites, request limits, and output locations. Treat source errors, quota errors, incomplete research, and “no signal found” as distinct outcomes.

Generated files generally go to `phase3_outputs` beside the database. Some later sections back up the database and write findings to SQLite. Review these cells and use a disposable database copy before executing them. Other experimental cells install packages, download local models, or start an Ollama process.

## Scope and limitations

- The main brief-generation evaluation uses supplied excerpts. It does not establish autonomous discovery, verified buying intent, business impact, or time savings.
- The government tool checks three reported fields from one source. A lack of differences does not establish the absence of signals elsewhere.
- The notebook records failed combined-agent attempts and unresolved end-to-end validation. It also references experimental local-agent modules that are absent from this repository.
- Saved evaluation artifacts and the database were not supplied. This repository makes no new performance or accuracy claims and does not reproduce the presentation's broader system results.
- API calls, remote websites, Drive assets, and model availability affect execution. The notebook was inspected statically rather than executed during repository preparation.

## Data handling and source attribution

Credentials are read through Colab Secrets. Database files, raw datasets, source snapshots, model files, and generated research records should remain outside Git. Public company identifiers and short attributed source excerpts remain in the original code as research examples.

The original notebook retains its source URLs, Google ADK documentation links, and AI-use disclosure. Referenced material includes the [FMCSA SAFER Company Snapshot](https://safer.fmcsa.dot.gov/CompanySnapshot.aspx) and the company pages cited directly in the evidence packs. Company statements and government records retain their respective source limitations.

No explicit project license was present in the supplied files. No new license or permission to redistribute third-party data is asserted.
