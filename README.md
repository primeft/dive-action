# Dive GitHub Action

[![Release][release-badge]][release]
[![GitHub Marketplace][marketplace-badge]][marketplace]

Analyze container image efficiency using [Dive](https://github.com/wagoodman/dive).

## Usage

<!--doc_begin-->
### Inputs

| Name       | Type   | Required | Default                             | Description                                                                  |
| ---------- | ------ | -------- | ----------------------------------- | ---------------------------------------------------------------------------- |
| image      | String | true     |                                     | Container image to analyze                                                   |
| config     | String | false    | `${{ github.workspace }}/.dive-ci`  | Path to [dive config file](https://github.com/wagoodman/dive#ci-integration) |
| exit-zero  | String | false    | `false`                             | Whether to force exit with zero even when scan fails ("true"/"false")        |

### Outputs

| Name                | Description                 |
| ------------------- | --------------------------- |
| efficiency          | Efficiency of the image     |
| wasted-bytes        | Number of wasted bytes      |
| user-wasted-percent | Percentage of space waster  |
<!--doc_end-->

### Example

<!-- x-release-please-start-version -->
```yaml
name: "Example Workflow with Dive"
on: [push]

jobs:
  sample-workflow:
    runs-on: ubuntu-latest
    name: Analyze image efficiency using Dive
    steps:
      - name: Checkout repo
        uses: actions/checkout@de0fac2e4500dabe0009e67214ff5f5447ce83dd # v6.0.2

      - name: Analyze image efficiency
        uses: primeft/dive-action@v0.2.1
        with:
          image: "node:alpine"
          config: ${{ github.workspace }}/.dive-ci
          exit-zero: "false"
```
<!-- x-release-please-end -->

## Development

**Build output:** The canonical build output is **`dist/`**. The action entry point is `dist/index.js` (see `action.yml`). The `lib/` directory is TypeScript compiler output and is gitignored; do not commit it.

Install and build:

```bash
npm install
npm run build
```

Release (CI runs `npm run build` and commits `dist/` on release PRs):

```bash
npm run build
git add dist/
git commit -m "chore: Build dist for release"
# Tag and push as needed, or use release-please
```

[release]: https://github.com/primeft/dive-action/releases/latest
[release-badge]: https://img.shields.io/github/release/primeft/dive-action.svg?logo=github&color=green
[marketplace]: https://github.com/marketplace/actions/dive-container-image-analysis
[marketplace-badge]: https://img.shields.io/badge/marketplace-dive--container--image--analysis-green?logo=github
