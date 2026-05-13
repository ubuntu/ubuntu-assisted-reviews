# ubuntu-assisted-reviews
Hackathon repo for AI-assisted review for SRU uploads.

## Running with `workshop`

Setup the workspace:

```bash
workshop launch
workshop exec -- claude login
workshop exec -- git config --global gitubuntu.lpuser "$LP_USER"
```

Run the SRU review action:

```bash
workshop run --env CLAUDE_MODEL=$CLAUDE_MODEL -- claude $UBUNTU_SERIES $SOURCE_PACKAGE
```

For example:

```bash
workshop run -i --env CLAUDE_MODEL=claude-sonnet-4-6 -- claude-sru-review noble openssl
```
