# SCV Chrome Extension

> Easily keep your Assets availability up to date in Copilot with a Chrome extension.

**Source:** https://help.laminarcopilot.com/en/articles/12120423-scv-chrome-extension  
**Collection:** Solutions > Extensions  
**Last Updated:** August 30, 2025

---

## Sync Assets Data from Amazon Relay

Assets' availability is constantly changing, and it can be difficult for AFP owners and managers to constantly update Laminar Copilot with the latest status of each asset in your fleet.

To automate the update process, Laminar Copilot provides a Chrome extension that will automatically sync your Assets data from Amazon Relay to Laminar Copilot.

**Please note:** This Chrome extension is a complementary solution that is **not** part of the official Laminar Copilot product. The Chrome extension has limited support and is not subject to the Master Service Agreement.

---

## Setting Up the SCV Chrome Extension

1. **Navigate to the extension page** in the [Google Chrome Store](https://chromewebstore.google.com/detail/laminar-copilot-scv-exten/oooiboepfjpbdjkmeboclhadahpinfdp?authuser=0&hl=en). *(Please make sure you're using Google Chrome for this extension.)*
   - If using Microsoft Edge, follow the [instructions to install Google Chrome extensions in Edge](https://support.microsoft.com/en-us/microsoft-edge/add-turn-off-or-remove-extensions-in-microsoft-edge-9c0ec68c-2fbc-2f2c-9ff0-bdc76f46b026#ID0EDL).
2. **Add the extension** to your browser.
3. **Pin your extension** so you can easily access it.
4. **Open the extension** and **log in** with your Laminar Copilot email and password.

## Using the SCV Chrome Extension

1. Open the extension and make sure you are logged into your Laminar Copilot account.
2. Navigate to Amazon Relay and open the [Assets page](https://relay.amazon.com/assets?ref=owp_nav_assets). (If you are already on the Assets page, refresh the page.)
3. You should see a banner at the top of the browser with the message: *"Laminar Copilot SCV Extension" started debugging this browser. (Please do not close the browser or browser tab until the banner disappears.)*
4. After the "debug" session, navigate to the [Assets page of Laminar Copilot](https://app.laminarcopilot.com/tractors) and confirm the Assets page has been updated with the latest data from Amazon Relay.

---

## SCV Extension Sync Rules

- The SCV Extension will sync the **Asset status** (Available/Unavailable) and the **cab type** (Day/Sleeper) of tractors in Amazon Relay with tractors in Laminar Copilot, matched by Asset ID.
- If there are assets in Amazon Relay that are **not in Laminar Copilot**, the extension will not add those assets to Copilot.
- If there are assets in Laminar Copilot that are **not in Amazon Relay**, the extension will not delete those assets from Copilot.
- Assets must first be created and deleted in Laminar Copilot; the extension will only update assets that exist in both platforms.
