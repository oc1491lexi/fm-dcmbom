# fm-dcmbom

Separate GitHub-hosted DCMBOM WebViewer frontend prototype. This repository is **not** the original FileMaker-hosted Option B implementation.

## Deployment status

The static page is a frontend only. It requires a separately deployed Cloudflare Worker and an HTTPS Worker URL in `config.js` before login or data loading will work. The Worker must hold passcodes and (for live mode) FileMaker Data API credentials as server-side secrets. **Do not put any password, passcode, API token, or FileMaker credential into this repository or the WebViewer URL.**

Before enabling live data, verify the Data API layouts, fields, record permissions, and read/write behavior with a disposable record. The current prototype is not production authentication: a shared manager passcode is not per-user identity or auditing.

## FileMaker WebViewer

Once the Worker has been deployed and `config.js` points to it, use this Web Address on a WebViewer object with interaction enabled:

```
https://oc1491lexi.github.io/fm-dcmbom/?gear=on
```

Use `gear=off` for a read-only interface. The Worker still decides write authority; the URL flag is not authorization. Enter the appropriate passcode in the page; never embed a reusable passcode in the URL.

## Source

This publishable folder contains the generated `index.html`, public `config.js`, and vendored Excel library. The tabs and table retain the rounded card treatment while using the original gray tab and dark-navy header palette. The header filter menu includes sort, value search, checkbox counts, and bulk selection; the footer includes page size, record range, and page navigation. In **Settings → Table Views**, managers can configure **Default (To All)**, **Spend Summary**, and **Quarters** independently, with nested **Rows Per Page** and ordered **Sorting** rules. Specific rules override Default separately for each setting; a specific scope may also inherit Default. Initial example: Default 20 rows and Reminder_count / Submission_count descending; Spend Summary 10 rows and Supplier ascending; Quarters inherits Default. The Worker stores and validates these preferences, serves them to authenticated viewers, and limits saves to managers. The Worker source, build transforms, and tests are maintained separately in the local `dcmbom-cloudflare-mock` prototype until a secure Cloudflare deployment is configured.
