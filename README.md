# OpenAuto releases

Signed APKs of OpenAuto, one app for the car's screen and the phone (Android 8.1 and up).
This repo holds builds only. The source is not public.

## Install with Obtainium

1. Add app, source URL `https://github.com/vardstein/openauto-releases`
2. Turn on "Include prereleases" (builds from dev are pre-releases named `v0.1.0-dev.N`)
3. Install. On the car's screen, pick "Car screen" at first start, then press Home and choose
   OpenAuto, Always

## Check the signature

Every APK is signed with this certificate (SHA-256):

```
51:7E:D7:5B:05:65:EA:DF:5C:72:69:10:89:1A:16:E6:40:FA:54:75:85:9C:AE:B0:B0:09:70:8F:7F:F6:9C:D4
```

`apksigner verify --print-certs openauto-*.apk` must show the same digest. Android refuses an
update signed with another key, so a swapped APK can't replace an installed one.
Each release also lists the APK's own SHA-256.

## How builds get here

OpenAuto's CI hands each dev build over on a branch `incoming/v<version>`. The publish workflow
checks the APK's SHA-256, package, version and signing certificate against `cert-sha256.txt`,
then makes the pre-release and deletes the branch.
