# GitHub Action: Run reek with reviewdog 🐶

[![](https://img.shields.io/github/license/reviewdog/action-reek)](./LICENSE)
[![depup](https://github.com/reviewdog/action-reek/workflows/depup/badge.svg)](https://github.com/reviewdog/action-reek/actions?query=workflow%3Adepup)
[![release](https://github.com/reviewdog/action-reek/workflows/release/badge.svg)](https://github.com/reviewdog/action-reek/actions?query=workflow%3Arelease)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/reviewdog/action-reek?logo=github&sort=semver)](https://github.com/reviewdog/action-reek/releases)
[![action-bumpr supported](https://img.shields.io/badge/bumpr-supported-ff69b4?logo=github&link=https://github.com/haya14busa/action-bumpr)](https://github.com/haya14busa/action-bumpr)

This action runs [reek](https://github.com/troessner/reek) with
[reviewdog](https://github.com/reviewdog/reviewdog) on pull requests to improve
code review experience.

## Examples

### With `github-pr-check`

By default, with `reporter: github-pr-check` an annotation is added to the line:

![Example comment made by the action, with github-pr-check](examples/example-github-pr-check.png)

### With `github-pr-review`

With `reporter: github-pr-review` a comment is added to the Pull Request Conversation:

![Example comment made by the action, with github-pr-review](examples/example-github-pr-review.png)

## Inputs

### `github_token`

`GITHUB_TOKEN`. Default is `${{ github.token }}`.

### `reek_version`

Optional. Set reek version. Possible values:
* empty or omit: install latest version
* `gemfile`: install version from Gemfile (`Gemfile.lock` should be presented, otherwise it will fallback to latest bundler version)
* version (e.g. `6.0.0`): install said version

### `reek_flags`

Optional. Reek flags. (`reek --single-line . <reek_flags>`)

### `tool_name`

Optional. Tool name to use for reviewdog reporter. Useful when running multiple
actions with different config.

### `level`

Optional. Report level for reviewdog [`info`, `warning`, `error`].
It's same as `-level` flag of reviewdog.

### `reporter`

Optional. Reporter of reviewdog command [`github-pr-check`, `github-pr-review`].
The default is `github-pr-check`.

### `filter_mode`

Optional. Filtering mode for the reviewdog command [`added`, `diff_context`, `file`, `nofilter`].
Default is `added`.

### `fail_on_error`

Optional.  Exit code for reviewdog when errors are found [`true`, `false`]
Default is `false`.

### `reviewdog_flags`

Optional. Additional reviewdog flags.

## Example usage

```yml
name: reviewdog
on: [pull_request]
jobs:
  reek:
    name: runner / reek
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v4
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: 3.0.0
      - name: reek
        uses: reviewdog/action-reek@v1
        with:
          reek_version: gemfile
          reporter: github-pr-review # Default is github-pr-check
```

## Sponsor

<p>
  <a href="https://evrone.com/?utm_source=action-reek">
    <img src="https://www.mgrachev.com/assets/static/evrone-sponsored-300.png" 
      alt="Sponsored by Evrone" width="210">
  </a>
</p>

## License

[MIT](https://choosealicense.com/licenses/mit)
