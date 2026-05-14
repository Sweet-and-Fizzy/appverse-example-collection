# RStudio (Example)

Example RStudio launcher app, part of the [Appverse Example Collection](../README.md). This is a reference implementation demonstrating how to structure a Batch Connect app within a multi-app repo. **Not deployable as-is** — the cluster name, module loads, job template, and other site-specific details are placeholders.

## Files in this directory

| File | Purpose |
|---|---|
| [`manifest.yml`](./manifest.yml) | Required by Open OnDemand to recognize the app. Supplies name, category, role, description. |
| [`form.yml`](./form.yml) | The launcher form users fill out. Defines `bc_num_hours` and `num_cores` fields. |
| [`appverse.yml`](./appverse.yml) | Per-app catalog metadata for the Appverse. Supplies name, description, app type, maintainer, tags. |

## What's missing for a real deployment

To make this app deployable, you'd add:

- `submit.yml.erb` — job submission configuration (template, queue, account, resource requests)
- `template/` directory with `script.sh.erb` and `before.sh.erb` — the job script and RStudio launch logic
- `view.html.erb` — the connection page shown after the job starts
- Real cluster names in `form.yml`'s `cluster:` list (currently `example_cluster`)
- Module load commands or environment setup specific to your HPC site

See the [OSC bc_osc_rstudio_server](https://github.com/OSC/bc_osc_rstudio_server) repo for a complete real-world RStudio app reference.

## License

Public domain — copy freely.
