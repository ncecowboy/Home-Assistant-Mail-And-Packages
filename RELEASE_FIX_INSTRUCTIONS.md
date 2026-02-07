# HACS Download Error Fix

## Problem
HACS was unable to install this integration due to a 404 error when trying to download `mail_and_packages.zip` from the v1.0.0 release.

**Error:**
```
Got status code 404 when trying to download 
https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/releases/download/v1.0.0/mail_and_packages.zip
```

## Root Cause
The GitHub Actions release workflow (`release.yaml`) had deprecated actions and commands that prevented it from running successfully when the v1.0.0 release was published. As a result, the required `mail_and_packages.zip` file was never created and uploaded to the release.

### Issues Fixed:
1. **Deprecated checkout action**: Updated from `actions/checkout@v1` to `actions/checkout@v4`
2. **Deprecated set-output command**: Updated from `::set-output` to `$GITHUB_OUTPUT`
3. **Old upload action**: Updated from `svenstaro/upload-release-action@v1-release` to `v2`

## Solution

The release workflow has been updated to:
- Use modern GitHub Actions versions
- Support manual triggering via `workflow_dispatch` for fixing existing releases
- Automatically trigger on new release publications

## How to Fix the v1.0.0 Release

Once this PR is merged to the main branch, follow these steps to add the missing zip file to the v1.0.0 release:

1. Go to the repository's **Actions** tab
2. Click on the **Release** workflow in the left sidebar
3. Click the **Run workflow** button (top right)
4. Enter `v1.0.0` in the "Tag to create release for" field
5. Click the green **Run workflow** button

The workflow will:
- Check out the code at tag v1.0.0
- Create the `mail_and_packages.zip` file
- Upload it to the v1.0.0 release (overwriting if it already exists)

After the workflow completes successfully, HACS will be able to download and install the integration from the v1.0.0 release.

## For Future Releases

Future releases will automatically have the zip file created and uploaded when a new release is published on GitHub, thanks to the workflow improvements.

## Verification

After running the workflow manually, verify the fix by:
1. Checking that the release has the `mail_and_packages.zip` asset: https://github.com/ncecowboy/Home-Assistant-Mail-And-Packages/releases/tag/v1.0.0
2. Testing HACS installation in Home Assistant
