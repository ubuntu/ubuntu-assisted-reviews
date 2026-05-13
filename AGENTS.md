# Project Overview

This project is a set of agent skills used to assist in the review of
Ubuntu Stable Release Updates (SRUs) and packages added to the NEW
queue.

# Skills

Each skill is located in a top-level directory and contains a `SKILL.md`
file with detailed instructions and workflow guidance.

For example, `./sru-review` contains instructions for reviewing SRUs.

## Available Skills

- `skills/sru-review` - Review Ubuntu Stable Release Updates
- `skills/new-review` - Review packages in the NEW queue

# Safeguards

- Never force-push to main.
- Never commit anything without explicit user request.
- Never log or commit secrets/keys.

# Available tools

The following tools should be available when using these skills. The user should be alerted if any of these tools are unavailable.

- `git-ubuntu`: Used to get packages from Launchpad. Can be installed through the `git-ubuntu` snap.
- `lrc`: Used for copyright review. Traverses the source package tree, figures out the license/copyright of all files, and compares them to `debian/copyright`, flagging any discrepancies. Can be installed by the `licenserecon` package.
- `rmadison`: Used to check for the versions of a particular package in the Debian/Ubuntu archive. Can be installed by the `devscripts` package.
