# Data Operations Rules

------------------------------------------------------------

## Purpose

Data is more important than code in this workspace.

The agent must treat data, databases, backups, exports, and n8n storage as sensitive assets.

------------------------------------------------------------

## Data First Rule

Before touching data, the agent must identify:

- what data exists
- where it lives
- whether it is original or generated
- whether it contains secrets
- whether it is backed up
- whether it is ignored by git
- how to restore it
- who owns the next decision

------------------------------------------------------------

## Allowed Data Work

Allowed after classification:

- create data inventory notes
- document data locations
- document backup commands
- document restore commands
- inspect filenames
- inspect schemas
- inspect small safe samples
- create placeholder schemas
- create export instructions

------------------------------------------------------------

## Ask Before

Ask before:

- opening large data files
- modifying database files
- modifying exports
- modifying backups
- deleting generated outputs
- running import scripts
- running migration scripts
- changing n8n data
- changing Docker volumes
- changing retention settings
- touching financial datasets

------------------------------------------------------------

## Never Do Automatically

Never automatically:

- delete backups
- delete exports
- delete databases
- overwrite source data
- overwrite n8n storage
- commit database files
- commit backup archives
- commit raw exports
- commit credentials
- commit API responses containing private data

------------------------------------------------------------

## Data Inventory

Every important data asset must be listed in:

    data/inventory.md

Inventory entry format:

- name
- path
- type
- source
- owner
- sensitivity
- git policy
- backup policy
- restore notes
- last verified date

------------------------------------------------------------

## Git Policy

The following should normally stay out of git:

- data/backups/*
- data/exports/*
- *.sqlite
- *.sqlite3
- *.db
- *.duckdb
- *.parquet
- *.csv
- *.xlsx
- *.tar
- *.tar.gz
- *.zip
- auth files
- tokens
- API keys

Exceptions require explicit user approval and explanation.

------------------------------------------------------------

## Financial Data

Financial or market data must include:

- source
- timestamp
- symbol universe
- assumptions
- known gaps
- limitations
- whether it is suitable for decisions

Agents must not present financial scanner output as investment advice.

------------------------------------------------------------

## Restore Rule

A backup is incomplete until restore is documented.

Every backup procedure should include:

- backup command
- verify command
- restore command
- expected location
- risks
- last test date

------------------------------------------------------------
