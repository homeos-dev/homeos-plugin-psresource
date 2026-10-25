# homeos-plugin-psresource

![License](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue)

A [homeos](https://github.com/homeos-dev/homeos) plugin for PowerShell modules, backed by [PSResourceGet](https://github.com/PowerShell/PSResourceGet).

## Usage

Add the plugin to your homeos repository:

```sh
homeos plugin add psresource
```

Create a package using this plugin:

```sh
homeos package add psscriptanalyzer --plugin psresource --param name=PSScriptAnalyzer
```

Modules are installed for the current user from the PowerShell Gallery.

## Requirements

These scripts run PSResourceGet, so [PowerShell](https://github.com/PowerShell/PowerShell) 7.4 or later must already be installed.

If you manage PowerShell itself with homeos, for example as a package named `powershell`, point this package at it with `--depends-on powershell` so homeos installs PowerShell before the module that needs it:

```sh
homeos package add psscriptanalyzer --plugin psresource --depends-on powershell --param name=PSScriptAnalyzer
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `name` | Module name on the PowerShell Gallery (e.g. `PSScriptAnalyzer`) |

## Actions

| Action | Command |
|--------|---------|
| install | `Install-PSResource -Name {{name}} -Scope CurrentUser -Repository PSGallery -TrustRepository -Reinstall` |
| update | `Update-PSResource -Name {{name}} -Scope CurrentUser -Repository PSGallery -TrustRepository` |
| uninstall | `Uninstall-PSResource -Name {{name}} -Scope CurrentUser` |

`update` installs the newer version alongside the current one; `uninstall` removes every installed version.

## License

Licensed under either of

 * Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0>)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.
