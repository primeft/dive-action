# Dive GitHub Action

[![Release][release-badge]][release]
[![GitHub Marketplace][marketplace-badge]][marketplace]

Analyze container image efficiency using [Dive](https://github.com/wagoodman/dive).

## Usage

<!--doc_begin-->
## Inputs
|Input|Description|Default|Required|
|-----|-----------|-------|:------:|
|`image`|Image to analyze|n/a|yes|
|`exit-zero`|Whether to exit with zero even when scan fails (still fails on error)|`false`|no|
|`config`|Path to dive config file|`${{ github.workspace }}/.dive-ci`|no|
|`dive-version`|Version of dive to use|`v0.13.1`|no|
|`docker-api-version`|Version of the Docker API to use|`1.44`|no|
## Outputs
|Output|Description|
|------|-----------|
|`efficiency`|Efficiency of the image|
|`wasted-bytes`|Number of wasted bytes|
|`user-wasted-percent`|Percentage of space wasted|
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
      - name: Analyze image efficiency
        uses: primeft/dive-action@v0.2.2
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
