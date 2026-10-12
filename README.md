# Lautaro Plugins

A collection of tools, plugins, and reusable skills created and maintained by [LautaroO](https://github.com/LautaroO). The marketplace identifier is `lautaro-plugins`.

The collection will grow as new tools are added. Initially, it includes only `maf-dotnet`, a plugin for working with Microsoft Agent Framework in .NET.

## Available plugins

| Plugin | Version | Source |
| --- | --- | --- |
| `maf-dotnet` | `0.1.1` | [maf-dotnet-template](https://github.com/LautaroO/maf-dotnet-template) |

The `maf-dotnet` catalog entry references the plugin repository root and selects the published release tag `v0.1.1` (commit `8da562313289bbea0e7bca6d85e99942fc5e8aa6`). Plugin versions are independent of Microsoft Agent Framework NuGet versions. This repository contains no plugin skill copies; applications such as `maf-playground` consume the catalog.

## Installation

Add the marketplace and install its first available plugin, `maf-dotnet`:

```sh
codex plugin marketplace add https://github.com/LautaroO/lautaro-plugins.git --sparse .agents/plugins
codex plugin marketplace list
codex plugin add maf-dotnet@lautaro-plugins --json
codex plugin list --json
```

Merge [the consumer configuration](examples/maf-playground.config.toml) into the application's existing `.codex/config.toml`. Open the application project in Codex and approve project trust through the client: project configuration is loaded only for trusted projects. Trust is a per-machine decision; do not commit personal authentication state or machine-specific trust paths.

Start a fresh session after installation and verify that Codex exposes all fourteen `maf-dotnet` skills, including `maf-adoption`, from its installed cache. A source-file count alone does not prove client discovery.

## Using maf-dotnet in an existing application

Explicitly select the installed plugin's `maf-adoption` skill and request inspection of the application. Preserve root and scoped instructions. Compare existing `.agents/skills/maf-*` copies with the installed plugin and move project-specific adaptations into scoped instructions or project references before removing redundant copies. Keep application behavior and NuGet versions unchanged; run the application's existing checks.

## Updating maf-dotnet

Review the next published plugin release and change the catalog's `source.ref` to its version tag after checking manifest version, skills and fresh-session evidence. Never move a published plugin tag; publish a new version for later changes. Do not track `main` in the plugin source selector. Publish the catalog update, then refresh and install:

```sh
codex plugin marketplace upgrade lautaro-plugins
codex plugin add maf-dotnet@lautaro-plugins --json
codex plugin list --json
```

Start a fresh session and verify the installed version and fourteen discovered skills. Retain the previous catalog commit for rollback.

## Initial maf-dotnet verification status

The initial catalog format was accepted by Codex CLI `0.162.1` using an isolated temporary `CODEX_HOME`. The source plugin checkout passed structural validation (14 skills, 17 playbooks) and its 18 unit tests. Installation from its Git source was attempted, but terminal DNS could not resolve `github.com`; remote installation and native-client discovery remain unverified. The application's adoption and checks are separate follow-up work.

Official references: [plugin packaging and marketplace format](https://developers.openai.com/plugins/build/plugins), [configuration reference](https://learn.chatgpt.com/docs/config-file/config-reference).

## maf-dotnet 0.1.1 release verification

The published `v0.1.1` plugin tag resolves to commit `8da562313289bbea0e7bca6d85e99942fc5e8aa6`. Its repository CI passed, including Markdown links. Native Codex CLI `0.162.1` installed the candidate through an isolated test marketplace and seven fresh sessions covered fourteen discovered skills, both adoption profiles, ordinary .NET negative routing, maturity and checkpoint review. See the [release evidence](https://github.com/LautaroO/maf-dotnet-template/blob/v0.1.1/docs/releases/v0.1.1.md).

Plugin version `0.1.1` carries guidance verified against MAF `dotnet-1.24.0`; it does not install or upgrade MAF packages in consuming applications. Desktop GUI behavior and application runtime/provider behavior were not tested.

Native CLI also installed the published tag through the updated catalog Git source and reported version `0.1.1`. All 52 package files (manifest, version, license, skills and resources) matched the verified release content; installed-resource validation passed.
