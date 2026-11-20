# YouTrack Autolink Action

A GitHub Action that automatically links YouTrack issue IDs (e.g. `YT-123`) in pull request titles and descriptions.

When a pull request is opened or edited, every issue ID that matches the configured project prefix is converted into a clickable markdown link to the YouTrack issue. Works for repos without GitHub's built-in Autolink references feature (e.g. private repos on a free plan).

## Example

**Before**

> Fix login bug (YT-42)

**After**

> Fix login bug ([YT-42](https://example.youtrack.cloud/issue/YT-42))

## Usage

```yaml
name: YouTrack Autolink
on:
  pull_request:
    types: [opened, edited]

permissions:
  pull-requests: write

jobs:
  autolink:
    runs-on: ubuntu-latest
    steps:
      - uses: tschogge/youtrack-autolink-action@v1
        with:
          youtrack-url: https://example.youtrack.cloud
          youtrack-project: YT
```

## Inputs

| Input | Description | Required |
|---|---|---|
| `youtrack-url` | Base URL of your YouTrack instance, e.g. `https://example.youtrack.cloud` | Yes |
| `youtrack-project` | Project prefix to match, e.g. `YT` (matches `YT-123`) | Yes |

## Notes

- Only the `pull_requests: write` permission is needed.
- IDs that are already linked are not linked twice.
- The workflow trigger (`on:`) must be defined by the consuming workflow; this action only processes the event.