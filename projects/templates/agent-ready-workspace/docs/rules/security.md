# Security Rules

------------------------------------------------------------

## Purpose

The workspace must prevent secret leaks, destructive actions, and unsafe agent behavior.

------------------------------------------------------------

## Secrets

Never commit:

- API keys
- tokens
- passwords
- private keys
- OAuth credentials
- browser cookies
- auth.json
- oauth_creds.json
- google_accounts.json
- .env files
- exported n8n credentials
- database dumps containing credentials

------------------------------------------------------------

## Secret Handling

If a secret file is discovered:

1. Stop.
2. Report the path.
3. Do not print contents.
4. Check git status.
5. Confirm whether it is ignored.
6. Ask user what to do.

------------------------------------------------------------

## Dangerous Commands

Never run automatically:

- rm -rf
- git reset --hard
- git clean -fd
- git push --force
- docker volume rm
- docker system prune
- database drop commands
- destructive migration commands
- format commands
- recursive forced deletion commands

------------------------------------------------------------

## Ask Before

Ask before:

- installing tools
- changing auth
- changing credentials
- exposing webhooks
- opening firewall ports
- modifying Docker volumes
- deleting files
- moving important folders
- changing global config
- touching OneDrive backup folders

------------------------------------------------------------

## Output Safety

Do not print secrets into chat, logs, reports, or markdown files.

When referencing secrets, use placeholders:

    <API_KEY>
    <TOKEN>
    <PASSWORD>
    <SECRET_PATH>

------------------------------------------------------------

## Financial Safety

For market or stock scanner work:

- state limitations
- avoid investment advice
- separate data from decisions
- document assumptions
- do not automate trading inside this workspace

------------------------------------------------------------

## Recovery Safety

Before risky work, confirm:

- backup exists
- restore path is known
- current git status is clean or understood
- target path is correct
- environment is correct

------------------------------------------------------------
