# Appverse Example Collection

This repository is a reference example for the [OOD Appverse catalog](https://openondemand.connectci.org/the-appverse). It demonstrates the structure of an `appverse.yml` file at the root of a multi-app repository.

The catalog uses the root `appverse.yml` to build a **Collection** page: one source repo that produces one or more Appverse apps grouped together.

## What this repo demonstrates

The root [`appverse.yml`](./appverse.yml) shows every key the catalog parses today:

| Key | Purpose |
|---|---|
| `appverse.min_version` | Schema version the file targets. The catalog supports up to `1.0`; newer files are rejected with a clear error. |
| `title` | Display title for the Collection (shown on the Collections grid and detail page). |
| `description` | Short description (one or two sentences). |
| `website` | URL to the project's homepage or landing page. Renders as a `WWW` link in the Collection sidebar. |
| `docs` | URL to the project's documentation. Renders as a `DOCS` link in the Collection sidebar. |
| `maintainer.name` | Person or group maintaining the repo. |
| `maintainer.support_url` | Where users go with questions or bug reports — typically the repo's issue tracker. |
| `tags` | List of Collection-level tags. Match-only against the catalog's existing tag vocabulary (case-insensitive). Unknown tags are silently skipped. |
| `shared_paths` | Repo-relative paths to shared infrastructure (templates, job scripts) that the apps in this Collection depend on. |
| `apps` | List of subpaths, each containing an Appverse app. Each entry has a `path:` key pointing at the subdirectory. |

## Real-world structure

In a real multi-app repo, each `apps[].path` would be a directory containing:

- `manifest.yml` — required by OOD to deploy the app
- `form.yml` — required by OOD for the launcher form
- `appverse.yml` (optional) — per-app catalog metadata (description, app type, tags)

This example repo does not include those subdirectories — it's documentation-by-example for the Collection-level schema. See the [App Contributor Guide](https://openondemand.connectci.org/appverse-contributor-documentation) for per-app file requirements.

## Validation behavior

When the catalog syncs a repo:

- If `appverse.yml` is well-formed and `appverse.min_version` is `1.0` or below: the Collection is created or updated with the declared metadata. Tags that match the existing vocabulary are attached.
- If `appverse.yml` is malformed (YAML parse error, top-level is a list, or `min_version` is too new): the Collection is flagged `stale_invalid` with a plain-language error message pointing at the file and field to fix.
- If the repo has no `appverse.yml` at all: the catalog still creates a Collection, deriving minimal metadata (title, description, organization) from the GitHub repo itself.

Unknown optional keys are ignored with a warning so newer-schema files don't break older catalog pipelines.

## License

Public domain — copy freely.
