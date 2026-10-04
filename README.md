# NKFiles

Distribution files for NinjaKernel.

`version.json` is the manifest the UI reads. It points at the bundle published
as a release asset, with its size and SHA-256 so a partial or tampered download
can be rejected rather than installed.

## Layout once installed

    %LOCALAPPDATA%\NKFILES\<robloxVersion>\
        RobloxPlayerBeta.exe      launched by the shortcut
        RobloxPlayerBeta.dll      emulator
        module.dll                executor, loaded by the emulator at startup
        ...                       the rest of the client

The install is self-contained: it does not touch the normal Roblox install
under `%LOCALAPPDATA%\Roblox`, so both can exist side by side.

## Updating

Publish a new release, upload the new bundle, and bump `version` and the
bundle's `url` / `size` / `sha256` in `version.json` on the default branch.
Clients compare their installed version against that file and re-download only
when it differs.
