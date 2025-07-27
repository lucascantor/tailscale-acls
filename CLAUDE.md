# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository manages Tailscale policy via GitOps following the pattern described at https://tailscale.com/kb/1306/gitops-acls-github. The entire policy configuration is defined in a single file: `policy.hujson`.

## Architecture

- **policy.hujson**: The main policy file containing SSH rules, groups, tag owners, and network grants
- **GitHub Actions Workflow**: Automatically validates policy changes on PRs and deploys them on main branch merges
- **GitOps Pattern**: All policy changes must go through version control and automated testing

## File Structure

- `policy.hujson` - Tailscale policy in HJSON format
- `.github/workflows/tailscale.yml` - GitHub Actions workflow for policy sync
- `.github/README.md` - Basic repository documentation

## Tailnet Policy Structure

The policy.hujson file contains:

- **ssh**: SSH access rules for members
- **groups**: User group definitions (e.g., "group:flatland")
- **tagOwners**: Tags and their ownership assignments for node categorization
- **grants**: Network access rules using the new grant syntax

## Development Workflow

1. Make changes to `policy.hujson`
2. Create a pull request - this triggers policy validation via GitHub Actions
3. Merge to main branch - this automatically deploys the policy to Tailscale

## Important Notes

- All policy rules use the modern "grants" syntax rather than deprecated "ACLs" (docs: https://tailscale.com/kb/1324/grants)
- Exit node access is controlled via tags (e.g., tag:exit-node-member, tag:exit-node-flatland)
- Changes are automatically deployed on merge to main, with no manual intervention required

## Required Practices

- Always adhere to Tailscale's tailnet policy file syntax: https://tailscale.com/kb/1337/policy-syntax
- Always adhere to Tailscale's grants syntax: https://tailscale.com/kb/1538/grants-syntax
