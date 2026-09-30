# Contributing to fitness-apps

Thanks for your interest in contributing! This monorepo holds open-source fitness apps built on the [exercises-dataset](https://github.com/rarhs/exercises-dataset), plus the shared data package they use.

By participating, you agree to follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## Ways to contribute

- **Report a bug** — open an issue with steps to reproduce, what you expected, and what happened (browser/OS if it's a UI bug).
- **Suggest a feature** — open an issue describing the problem it solves before writing code, so we can agree on the approach.
- **Improve docs** — typo fixes and clarifications are always welcome.
- **Send code** — pick an open issue (or open one first for anything non-trivial) and submit a pull request.

## Project layout

```
packages/exercise-data/   shared data layer: types, slim exercise index, media URL helpers
apps/vault/               exercise library, routine builder and session logger (Vite + React)
```

## Development setup

Requires Node.js 18.17 or newer.

```bash
npm install        # once, at the repo root (npm workspaces)
npm run sync-data  # regenerate the slim exercise index from the dataset
npm run check      # type-check all workspaces
npm test           # run tests across all workspaces
```

Run the Vault app locally:

```bash
npm run dev --workspace @fitness-apps/vault
```

## Pull request workflow

1. Fork the repo and create a branch from `main` (e.g. `fix-routine-sort`).
2. Make your change. Keep PRs focused — one fix or feature per PR.
3. Make sure `npm run check` and `npm test` pass locally.
4. Open a pull request describing **what** changed and **why**. Link the related issue if there is one.

`main` is protected: every change lands through a pull request, and the `check` (type-check, tests, bundle-size gate) and `smoke` (end-to-end) checks must pass before merging.

## Ground rules

- **Never bundle the full dataset.** Instruction text is fetched at runtime; only the slim index in `packages/exercise-data/src/generated/` is bundled. CI enforces a bundle-size budget.
- **Don't edit `exercise-index.json` by hand** — regenerate it with `npm run sync-data`.
- **Respect the media license.** Exercise images and GIFs are © Gym Visual, redistributed with permission at 180×180 only. Any UI that shows them must display the attribution (`DATASET_ATTRIBUTION`), and media must never be upscaled, re-hosted at a higher resolution, or stripped of attribution.

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE) that covers this project's code.
