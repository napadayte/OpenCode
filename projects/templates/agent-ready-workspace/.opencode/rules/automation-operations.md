# Automation Operations Rules

------------------------------------------------------------

## Purpose

This workspace may document and manage automations, especially n8n workflows.

Automation must be boring, explicit, and recoverable.

------------------------------------------------------------

## Automation Types

Common automation types:

- n8n workflows
- scheduled scripts
- data export jobs
- data cleanup jobs
- notification workflows
- stock scanner workflows
- backup workflows
- reporting workflows

------------------------------------------------------------

## Required Documentation

Every automation should document:

- purpose
- owner
- trigger
- schedule
- inputs
- outputs
- credentials used
- external services
- failure behavior
- retry behavior
- logs
- rollback
- disable procedure
- last verified date

------------------------------------------------------------

## n8n Rules

For n8n:

- treat n8n data as sensitive
- document workflows in automations/n8n/
- document Docker volume name
- document backup procedure
- document restore procedure
- never delete workflow data without approval
- never rotate credentials without approval
- never expose webhook secrets
- never commit exported credentials

------------------------------------------------------------

## Ask Before

Ask before:

- running workflows
- changing triggers
- changing schedules
- changing credentials
- changing webhook URLs
- changing Docker containers
- changing Docker volumes
- deleting executions
- pruning logs
- importing workflows
- restoring n8n data

------------------------------------------------------------

## Automation Change Report

Every automation change report must include:

- changed automation
- reason
- affected files
- affected data
- credentials touched or not touched
- verification
- rollback
- remaining risks

------------------------------------------------------------

## Failure Rule

If an automation touches data or money-related information, failure handling must be documented before execution.

------------------------------------------------------------
