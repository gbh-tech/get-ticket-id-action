<!-- omit in toc -->
# Get Ticket ID Action

<!-- omit in toc -->
## Content

- [Overview](#overview)
- [Usage](#usage)
  - [Examples](#examples)

## Overview

This GitHub Action facilitates getting the ticket ID from a branch name used
in a workflow. If you have a branch with a similar name to:

```text
TK-123-fix-for-README-file
```

This action will be able to output the string `TK-123`, then re-use it in your
other workflow steps or jobs.

## Usage

See [action.yml](action.yml) for more info about the action.

```yaml
- uses: gbh-tech/get-ticket-id-action@v1
  with:
    # Optional. Specifies the git ref to use to obtain the ticket ID.
    # Defaults: github.head_ref, github.ref_name
    ref: ''
```

> 💡 Check the official documentation on the [github context] to learn more
> about the values of `github.head_ref` and `github.ref_name`.

### Examples

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: gbh-tech/get-ticket-id-action@v1
        id: get-ticket-id
      - name: Show the discovered ticket ID
        env:
          TICKET_ID: ${{ steps.get-ticket-id.outputs.ticket-id }}
        run: echo "Ticket ID is ${TICKET_ID}"
```

<!-- References -->
[github context]: https://docs.github.com/en/actions/learn-github-actions/contexts#github-context
