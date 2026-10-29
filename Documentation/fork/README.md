# About this fork

xDripSaf is a fork of [NightscoutFoundation/xDrip](https://github.com/NightscoutFoundation/xDrip)
(xDrip+). It follows upstream and adds changes in a few areas. Like upstream, it is licensed under
GPL-3.0.

## Focus

- The Wear OS watch app: watch faces and complications on current watches.
- Current Android versions, on the phone and on the watch.
- A friendlier design.
- One-minute readings, for data sources that deliver them.

## Starting point

Upstream at `c42cf55c6` (2026-10-23):

| Item | Value | Where |
|---|---|---|
| App compileSdk / minSdk / targetSdk | 36 / 26 / 26 | `app/build.gradle` |
| Watch app compileSdk / minSdk / targetSdk | 36 / 21 / 23 | `wear/build.gradle` |
| Android Gradle Plugin / Kotlin / Gradle | 8.13.2 / 2.2.0 / 8.14.3 | `build.gradle`, `gradle/wrapper/gradle-wrapper.properties` |
| Java | toolchain 17, source and target 1.8 | `app/build.gradle` |
| Watch libraries | `com.google.android.support:wearable:2.5.0`, `play-services-wearable:10.2.1`; no AndroidX | `wear/build.gradle` |

Platform changes that matter here:

- **Target SDK 24.** Android 15 and later refuse to install an app that targets an SDK below 24.
  An app installed before the OS upgrade keeps working. Wear OS 6, for example One UI 8 Watch, is
  built on Android 16, so the rule is expected to apply there as well; this is still to be
  confirmed on a watch. Raising the watch app's target SDK is the first watch task.
- **Watch faces.** The watch faces in the wear module are built on the Wearable Support Library.
  Since 2026-01-14 Google Play no longer installs watch faces of this kind, and newer watches do not
  accept them. They need the Watch Face Format. Complications are not affected.

## One-minute readings

- **Upstream setting.** "Libre 1-minute" (`libre_one_minute`, Advanced settings) sets a one-minute
  sample period for the "Libre2 (patched App)" data source, and takes effect after a restart. That
  source also receives values from other apps, for example Juggluco's "Patched Libre broadcast".
- **The sensor decides the real rate.** According to Juggluco's documentation, Sibionics GS3 gives
  a new value every 5 minutes, while GS1 also has per-minute raw values.

Code written around the 5-minute period, to review once readings arrive every minute:

| Area | What to check | Where |
|---|---|---|
| Rise and fall alerts | uses the last 4 readings, so the window becomes ~3 minutes instead of ~15 | `BgReading.checkForDropRiseAllert`, `BgReading.trendingToAlertEnd` |
| Displayed delta | the slope of the last two readings is scaled to 5 minutes | `BestGlucose.java` |
| Noise | needs more than 5 points in 20 minutes; thresholds are tuned for 5-minute data | `BgGraphBuilder.java` |
| Statistics | capture percentage and GVI/PGS assume a 5-minute step | `StatsResult.java`, `FirstPageFragment.java` |
| Watch sync | a resend carries the last 60 readings: 5 hours of 5-minute data, 1 hour of 1-minute data | `WatchUpdaterService.resendData` |
| Uploads | five times as many records | uploaders |

## Ideas from other forks

[xdripJH](https://github.com/jakobheyman/xdripJH) by Jakob Heyman adds display and statistics
features. These are candidates for this fork:

- a raw data plot, and the last raw value on the home screen;
- the calibration graph in one unit;
- statistics for a custom date range;
- vertical zoom in the preview graph;
- an option to hide the noise line;
- a custom vibration pattern per alert.

Each one comes over as a change of its own, with credit to the original commit.
