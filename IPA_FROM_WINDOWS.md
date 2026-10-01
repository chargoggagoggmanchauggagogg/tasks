# Get an IPA for your iPad using only Windows

You cannot build an IPA on Windows, so GitHub builds it for you on a Mac in the cloud (free for public repositories). Then you install it on your iPad from your PC.
This workflow is untested. If a step fails, copy the red error lines and send them to Claude.

## Part 1: Build the IPA
1. Make a free account at github.com.
2. Click New repository. Name it `tasks-app`, choose **Public**, and click Create. (Private repos use your free minutes at a 10x rate on macOS.)
3. Unzip `tasks-store-app.zip`. In the new repo, click "uploading an existing file" and drag in everything INSIDE the unzipped folder (`package.json`, `capacitor.config.json`, `www`, `resources`, `.github`, and the rest). Click Commit changes.
   - `package.json` must be at the top level of the repo, not inside another folder.
   - If `.github` did not upload: Add file > Create new file, name it `.github/workflows/build-ios.yml`, and paste in the contents of that file.
4. Open the **Actions** tab. The build "Build iOS IPA (unsigned)" starts by itself, or choose it and click Run workflow. Wait for a green tick.
5. Open the finished run, scroll to **Artifacts**, and download `Tasks-ipa`. Unzip it to get `Tasks.ipa`.

## Part 2: Put it on your iPad (free Apple ID)
Use Sideloadly (sideloadly.io) or AltStore (altstore.io). Both sign the IPA with your own Apple ID. On Windows they need iTunes installed from Apple's website, not the Microsoft Store version. Their setup pages list the exact steps.
1. Connect the iPad to your PC with a USB cable and tap Trust on the iPad.
2. Drag `Tasks.ipa` into Sideloadly, enter your Apple ID, and click Start.
3. On the iPad: Settings > General > VPN & Device Management > tap your Apple ID > Trust.
4. If asked, turn on Developer Mode: Settings > Privacy & Security > Developer Mode, then restart the iPad.

## Limits
- An app signed with a free Apple ID stops working after 7 days. Re-run Sideloadly, or let AltStore refresh it.
- A free Apple ID can have about 3 sideloaded apps at once.
- Consider a spare Apple ID rather than your main one.
- A paid Apple Developer account ($99/year) lasts a year and allows TestFlight.
