# Google Play publishing material

Requirements checked against Google's documentation on **25 November 2026**. This folder contains public Markdown
pages for a separate GitHub repository and the remaining Play Console work. Nothing has been published or submitted.

## Publish the pages

Copy the **contents** of [`site/`](site/) to the root of the separate repository, including `_config.yml`. Keep this
checklist in the app repository. The public policy is [`site/privacy-policy.md`](site/privacy-policy.md); the other
pages provide an optional support website. The Markdown front matter and theme configuration render ordinary HTML
pages with GitHub Pages.

1. In the destination repository, open **Settings > Pages**, choose **Deploy from a branch**, and select `main` and
   `/(root)`. Use a public repository if publishing through GitHub Free.
2. Wait for deployment and copy the actual site address shown by GitHub. The examples below use `OWNER` and `REPO`
   as placeholders; no final hosting URL has been selected.
3. Open the privacy and support pages while signed out. Check HTTPS, readable content, working navigation and email
   links, and worldwide access. Use the published HTML address in Play Console; uploading Markdown alone does not host
   the required policy webpage.
4. Keep the published copy and this source in sync when data handling changes. Update the policy date as appropriate.

See GitHub's [Pages setup instructions](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
and [Markdown rendering guidance](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll).

## External links and contacts

| Item | Required for Traced? | Value or page to use |
| --- | --- | --- |
| Privacy policy URL | Yes, even without developer analytics | `https://OWNER.github.io/REPO/privacy-policy.html` after deployment |
| Support email | Yes | `errantstep@gmail.com` |
| Store listing website | Optional, recommended | `https://OWNER.github.io/REPO/` or its `support.html` page |
| Account deletion URL | Not applicable to the current app, which has no app accounts | Answer the account-creation questions accurately; do not claim a remote account-deletion service |
| Official organization website | Conditional on developer account type | Complete website ownership verification if required by the organization-account setup |
| Separate terms/EULA URL | No general Play requirement identified for this app | The app already displays its EULA; this does not replace a privacy policy |

Google requires a public, readable policy webpage without login, geographic restrictions, PDF downloads, or visitor
editing. It also requires a privacy policy link or policy text **inside the app**. The policy must identify the app or
developer and explain access, use, sharing, security, retention, deletion, and privacy contact details.
See the [User Data policy](https://support.google.com/googleplay/android-developer/answer/10144311?hl=en).

The [store listing setup guide](https://support.google.com/googleplay/android-developer/answer/9859152?hl=en) requires
a support email and recommends a website. Organization account verification is a separate requirement; see
[developer identity verification](https://support.google.com/googleplay/android-developer/answer/10841920?hl=en).
An external deletion resource becomes mandatory if the app introduces account creation; see
[account deletion requirements](https://support.google.com/googleplay/android-developer/answer/13327111?hl=en).

## Remaining app and Console work

- [ ] Deploy the public pages and replace the example addresses above with the real URLs.
- [ ] Enter the privacy URL in **App content > Privacy policy**, and the email and optional website in store settings.
- [ ] Add an accessible **Privacy Policy** entry inside the app, using the final URL or bundled policy text. The current
  landing page has an EULA entry but no privacy entry. This documentation change does not implement it.
- [ ] Complete Data safety for closed/open testing or production, including SDK behavior and deletion questions.
  Apps exclusively on internal testing are exempt from the Data safety form, rather than from all Play policies.
- [ ] Complete **App content** declarations: no ads in the current app; no app login required; accurate target audience
  and content rating. The optional support purchase is an in-app purchase, not an advertising SDK. Select age groups
  based on the intended audience; including children brings additional Families policy requirements.
- [ ] Review every other declaration shown under **App content > Needs attention**, including any health, financial,
  or permission questions. Describe actual functionality; a drawing app's support purchase is not a banking feature.
- [ ] Complete store text, category, countries, pricing, app icon, feature graphic, and screenshots. Use screenshots of
  the current build and follow the device-specific asset requirements.
- [ ] Complete developer identity, public contact, payments, and any regional trader declarations requested by Console.
- [ ] If the personal developer account was created after 13 November 2023, complete the required closed test with at
  least 12 testers continuously opted in for 14 days, then apply for production access. Internal testing does not replace it.
- [ ] Follow [`../release.md`](../release.md) for the signed AAB, version code, symbols, and device checks, and
  [`../billing.md`](../billing.md) for product setup and live purchase tests. The current Gradle target is API 36; verify
  current target API, native-library compatibility, and Billing Library eligibility before each submission.
- [ ] Verify 16 KB page-size support for the native libraries and APK packaging, and test on a 16 KB device/emulator.
  See Android's [native compatibility requirements](https://developer.android.com/guide/practices/page-sizes).

Sources: [app review declarations](https://support.google.com/googleplay/android-developer/answer/9859455?hl=en),
[target audience](https://support.google.com/googleplay/android-developer/answer/9867159?hl=en),
[preview assets](https://support.google.com/googleplay/android-developer/answer/9866151?hl=en),
[personal-account testing](https://support.google.com/googleplay/android-developer/answer/14151465?hl=en), and
[target API requirements](https://support.google.com/googleplay/android-developer/answer/11926878?hl=en).

## Data safety preparation

This is an implementation audit, not a completed Console declaration. Review the exact release and all active versions.
Google's [Data safety guidance](https://support.google.com/googleplay/android-developer/answer/10787469?hl=en) covers
SDK transmissions, payment exceptions, user-directed sharing, and when on-device processing falls outside collection.
Do not infer "no data collected" solely from local drawing storage.

| Area | Current implementation and declaration review |
| --- | --- |
| Drawing content, imports, and preferences | Processed locally. Chosen cloud document providers and export recipients can receive files; assess the applicable user-directed transfer rules. |
| Purchases | Google Play Billing `9.1.0` queries and acknowledges purchases using tokens; only an ownership flag is persisted. No developer backend. Review purchase history separately from card details, which Traced never accesses. |
| Billing diagnostics | Billing and its dependencies can communicate with Google. Check the pinned SDK's disclosure and actual release behavior before choosing data categories, purposes, required/optional collection, or sharing answers. |
| Local logs and platform reports | No developer analytics/crash SDK. Local logging alone is not an off-device transmission; separately assess Google Play/Android platform reporting and any SDK diagnostics. |
| Backups | Rules exclude recovery autosave files and purchase preferences. Other private files, including previews and private fallback projects, are eligible for Android backup; chosen document providers have separate rules. |
| Email support | Users can email information to Errant Step through Gmail. Covered by the public policy; review the form's scope for this external support channel. |
| App accounts and deletion | No Traced account creation. Local deletion instructions are on the support page; no developer service can remotely delete drawings or Google's billing records. |

Inspect the release merged manifest and dependency list, not just the handwritten manifest. The existing release manifest
adds `INTERNET`, `ACCESS_NETWORK_STATE`, and `com.android.vending.BILLING`. Network permissions alone do not establish
which data types are transmitted. Review [Google Play SDK Index](https://play.google.com/sdks) and Android's
[data-use audit guidance](https://developer.android.com/privacy-and-security/declare-data-use). The SDK Index's dynamic
pages did not expose a Billing-specific disclosure table during this review, so SDK collection answers remain a release
check rather than a verified "no collection" claim.

## Implementation references

- [`../../platform/android/java/com/errantstep/traced/TracedActivity.java`](../../platform/android/java/com/errantstep/traced/TracedActivity.java):
  picker access, private fallback projects, autosaving, previews, sharing cache, preferences, and existing EULA.
- [`../../platform/android/java/com/errantstep/traced/SupportPurchase.java`](../../platform/android/java/com/errantstep/traced/SupportPurchase.java):
  Play purchase processing and private ownership preference.
- [`../../platform/android/res/xml/backup_rules.xml`](../../platform/android/res/xml/backup_rules.xml) and
  [`../../platform/android/res/xml/data_extraction_rules.xml`](../../platform/android/res/xml/data_extraction_rules.xml):
  cloud-backup and transfer exclusions.
- [`../../platform/android/build.gradle`](../../platform/android/build.gradle): release identity, API level, and dependencies.
