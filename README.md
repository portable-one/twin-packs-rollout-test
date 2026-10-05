# Portable account catalog rollout test

This repository is a throwaway rehearsal, not the production catalog or publisher. Its packages use isolated test names. Existing production repositories, histories, package versions and Worlds remain unchanged.

# Independent twin publisher

This repository publishes immutable Protocol 3 packages using released World and twin-standard tooling. It does not clone platform source or require a platform account. Package-specific API behavior, spec and journeys live with each package.

Install from the committed lock using Bun 1.3.11: `bun install --frozen-lockfile --ignore-scripts`. Build through an owned World with `bun scripts/run-world.ts build`. Build outputs and compiled pack facts are generated, never maintained by hand. Local synthetic state uses throwaway credentials.

Release is an explicit `release.yml` dispatch, disabled until `PACK_PUBLISH_ENABLED=true`. Set `CATALOG_PACKAGE_VERSION` to the exact catalog bootstrap version; it must include this repository's approved source registration. The workflow installs that CLI with scripts disabled, retains its dependency lock, builds through a fresh World, and publishes one exact version with npm provenance. It confirms registry integrity and retains immutable submission JSON for a fork PR. This publisher has no catalog App key or proposal token. It never approves or merges. Qualification is performed explicitly before release; this workflow adds no test trigger.

The publisher App has contents/pull-request write access only to `volter-ai/twin-catalog-rollout-test`. Put its client ID in `CATALOG_PR_APP_CLIENT_ID` and its key in `CATALOG_PR_APP_PRIVATE_KEY`. `NPM_TOKEN` is a scoped publication credential when npm trusted publishing is unavailable. No private platform read token is needed. Job tokens are revoked automatically.

The [catalog process](https://github.com/volter-ai/twin-catalog-rollout-test/blob/main/docs/process.md) owns registration, independent assessment, moderator admission, recommendation and revocation. Outside publishers register their own repositories, scopes and release workflows, and submit from forks using their own credentials.

A successful upload is never repeated. Workflow reruns only confirm an exact version by registry reads; they cannot upload. For an accepted upload whose confirmation failed, use the retained tarball and `node scripts/publish.mjs --confirm-only` with the recorded catalog CLI. Do not dispatch a new publication run for that version while confirmation is unresolved. If submission preparation fails after upload, retrieve the retained package and submission artifacts, confirm the exact registry version, and retry preparation. Open the catalog PR from `portable-one/twin-catalog-rollout-test` using the retained submission JSON; no GitHub proposal credential is stored in this publisher. Code changes require a new version. An outside submission requires current-head non-author human moderator approval; eligible internal submissions can use the named maintainer merge path.
