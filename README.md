# ubuntu-assisted-reviews
Hackathon repo for AI-assisted review for SRU uploads.

## Examples
The [examples](examples) directory contains two reports generated for the same SRU (openssl). One with the MoonshotAI/Kimi-K2.6 model, and another for Claude Sonnet 4.6. Both were given the same skill:

 * [MoonshotAI/Kimi-K2.6](examples/moonshotAI-Kimi-K2.6-sru-review-openssl-lp2130576.md)
 * [Claude Sonnet 4.6](examples/Claude-Sonnet-4.6-sru-review-openssl-lp2130576.md)

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
