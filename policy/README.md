# Policy files

This directory holds the example Tailscale App Connector policy artifacts used by the
toolkit.

## `default-ai-domains.json` — example domain policy (`common` pack)

`default-ai-domains.json` is the built-in `common` domain pack: the default
selective-routing policy the installer applies when you do not pass your own
`--domains-file`.

> **Example only.** This list is provided as an **example of selective domain routing using
> common AI services**. It is **not authoritative, exhaustive, or guaranteed to remain
> current**. Review and maintain domain policies for your own environment before use.

Selective domain routing is domain-agnostic — the toolkit is not AI-specific. AI-service
domains are simply the bundled example. To use your own policy, pass
`--domains-file /path/to/your-domains.txt` (a newline-delimited list, with `#` comments
allowed) or `--domains-file /path/to/your-domains.json` (a JSON string array). See the
[README](../README.md#example-domain-policy-ai-services).

**Format.** This file is a strict JSON string array (no comments) because tooling and tests
read it with a JSON parser. To print the exact, normalized entries:

```bash
python3 scripts/policy_tool.py domains --domains-file policy/default-ai-domains.json
```

## `app-connector.example.json`

A complete example tailnet-policy snippet for a single App Connector, used by the smoke
test and by the local `validate` / `merge` / `diff` examples. Its `domains` array is kept a
superset of `default-ai-domains.json` (a unit test enforces this).

## Historical identifiers (compatibility)

The public-facing project name is being updated to **Tailscale Network Control**, but this
file's name (`default-ai-domains.json`) and related identifiers — the
`AI_EGRESS_DOMAINS_FILE` environment variable, the `tag:ai-egress-*` connector tags, the
`AI-Egress-*` connector name, and the `tailscale-ai-egress` repository URL — intentionally
keep the historical `tailscale-ai-egress` name. They are load-bearing for existing installs,
scripts, tests, and upgrade paths and are **not** renamed for cosmetic consistency. See
[docs/Stability.md](../docs/Stability.md).
