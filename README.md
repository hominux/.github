# .github

Organization-wide defaults for [Hominux](https://github.com/hominux). GitHub applies the community-health files below
to every repository that does not define its own. `profile/README.md` renders on the organization page instead.

| Path | Purpose |
| --- | --- |
| [`profile/README.md`](profile/README.md) | Organization profile page |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Contribution guidelines |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Community standards |
| [`SECURITY.md`](SECURITY.md) | Vulnerability reporting |
| [`SUPPORT.md`](SUPPORT.md) | Where to get help |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE) | Default issue forms |
| [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md) | Default pull request template |
| [`.github/FUNDING.yml`](.github/FUNDING.yml) | Sponsor button |

Changes here affect every repository in the organization. Open a pull request; `CODEOWNERS` requests review from
`@hominux/maintainers`.

## Reusable workflows

### `announce-release.yml`

Posts "`<repo> <tag> released.`" with the release link to Mastodon and Bluesky. It skips pre-releases, and skips a
platform whose secrets are unset. Inputs: `tag` (required), `url` (defaults to the tag's release page), `prerelease`.

Call it as a job in the workflow that creates the release, after the publish job. A release created with the default
`GITHUB_TOKEN` does not fire the `release` event, so a separate `on: release` workflow would never run.

```yaml
  announce:
    needs: [plan, publish]
    if: ${{ needs.plan.outputs.dry_run != 'true' }}
    permissions: {}
    uses: hominux/.github/.github/workflows/announce-release.yml@main
    with:
      tag: v${{ needs.plan.outputs.version }}
    secrets:
      MASTODON_INSTANCE_URL: ${{ secrets.MASTODON_INSTANCE_URL }}
      MASTODON_ACCESS_TOKEN: ${{ secrets.MASTODON_ACCESS_TOKEN }}
      BLUESKY_HANDLE: ${{ secrets.BLUESKY_HANDLE }}
      BLUESKY_APP_PASSWORD: ${{ secrets.BLUESKY_APP_PASSWORD }}
```

Set the four secrets at the organization level and grant the calling repositories access.
