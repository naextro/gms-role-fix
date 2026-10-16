# Google Play Services Role Holders Permission Fix

APatch / Magisk / KernelSU module that resolves Google account authentication failures, Play Store sign-in loops, and Play Services crashes on Android ROMs running newer Google Play Services versions.

## Problem
Newer versions of `com.google.android.gms` invoke `RoleManager.getRoleHolders()`, requiring `android.permission.GET_ROLE_HOLDERS` or `android.permission.MANAGE_ROLE_HOLDERS`.
If the ROM's `/product/etc/permissions/privapp-permissions-google-product.xml` does not grant these privileged permissions to GMS, Play Services crashes during auth token generation with:
```
java.lang.SecurityException: getRoleHoldersAsUser: Neither user 10282 nor current process has at least one of [android.permission.MANAGE_ROLE_HOLDERS, android.permission.GET_ROLE_HOLDERS].
```
This causes Play Store to prompt "Authentication is required, you need to sign in to your google account" even when signed in, and prevents YouTube, Gmail, and Google Sync from functioning.

## Fix
Injects `GET_ROLE_HOLDERS`, `MANAGE_ROLE_HOLDERS`, and `OBSERVE_ROLE_HOLDERS` into the privileged permissions whitelist for `com.google.android.gms`.

## Compatibility
- Root: APatch / Magisk / KernelSU
- Android: 13, 14, 15, 16
