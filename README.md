# Task Runner Project Configurations

This repository contains example project family configurations for the task runner orchestrator.

## What is a Project Family?

A project family groups related repositories that should be cloned together when running tasks. For example:

- **healthtrac**: web + api + mobile repos
- **neptune**: web + api + mobile repos
- **pythia**: frontend + api repos

## Configuration Structure

```
projects/
  healthtrac.sh      # Defines healthtrac family
  neptune.sh         # Defines neptune family
  pythia.sh          # Defines pythia family
```

## Example Configuration

```bash
#!/bin/bash
# Project: healthtrac
# Repositories that belong to this family

REPOS="healthtrac360-web healthtrac360-api healthtrac360-mobile"
PRIMARY_REPO="healthtrac360-web"
```

## Usage

```bash
# Source a project config
source projects/healthtrac.sh

# Now $REPOS and $PRIMARY_REPO are set
./task-run.sh --project healthtrac --task my-task --desc "Description" --script script.sh
```

## Available Project Families

### healthtrac
- healthtrac360-web (primary)
- healthtrac360-api
- healthtrac360-mobile

### neptune
- neptune (primary)
- neptune-api
- neptune-mobile

### pythia
- pythia-frontend (primary)
- pythia-api

## Creating Your Own Project Family

1. Create a new file in `projects/`
2. Define `REPOS` (space-separated list)
3. Define `PRIMARY_REPO` (where PRs will be created)
4. Source it before running tasks

```bash
# projects/my-project.sh
REPOS="my-web my-api"
PRIMARY_REPO="my-web"
```

## Integration with Task Runner

The task runner orchestrator reads these configurations to:
- Discover which repos to clone
- Determine the primary repo for PR creation
- Set up isolated Docker containers with all related code

See: https://github.com/dominiquemb/dev-workflow for the main orchestrator
