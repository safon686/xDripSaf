# xDripSaf

A fork of [xDrip+](https://github.com/NightscoutFoundation/xDrip), the Android app published by the
Nightscout Foundation that collects, displays and shares data from continuous glucose monitors.

> **Status: in development. No version is available yet.**
> For a working app, use the official xDrip+:
> [download and info page](https://jamorham.github.io/#xdrip-plus) and
> [documentation](https://xdrip.readthedocs.io).

## What this fork works on

- The Wear OS watch app: watch faces and complications on current watches.
- Current Android versions, on the phone and on the watch.
- A friendlier design.
- One-minute readings, for data sources that deliver them.

The starting point and plans are in [Documentation/fork/README.md](Documentation/fork/README.md).

## Relationship to xDrip+

- The fork follows upstream `master` and merges its changes regularly.
- Anything the fork notes do not mention works as in xDrip+, and the
  [xDrip+ documentation](https://xdrip.readthedocs.io) and
  [upstream README](https://github.com/NightscoutFoundation/xDrip#readme) apply.
- Ideas taken from other forks are credited in the fork notes and in the commits that bring them.

## Versions and releases

- Versions are annotated git tags `vMAJOR.MINOR.PATCH`. They stay at `0.x` while the fork is in
  development.
- Each version is published under [Releases](https://github.com/safon686/xDripSaf/releases). Its
  notes name the upstream version it is based on.
- Upstream's date tags (for example `2026.10.23`) belong to xDrip+ and are not this fork's
  versions.
- No version has been tagged yet.

## Safety

Neither xDrip+ nor this fork is a medical device or approved by any regulator. Do not base
treatment decisions on them alone; check readings with a blood glucose meter. Use at your own risk:
the software comes with no warranty (GPL-3.0, sections 15 and 16).

## License

GPL-3.0, see [LICENSE](LICENSE). The original code remains copyright of its authors, the xDrip and
xDrip+ contributors.
