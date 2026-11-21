# YouTube Cleanup — uBlock Origin filter list

A [uBlock Origin](https://github.com/gorhill/uBlock) filter list that removes the parts of YouTube that pull your attention away from the videos you actually came to watch: **Shorts, Playables, AI features, auto-dubbed audio, Premium upsells, and shopping/merch shelves**. It covers both the desktop site (`www.youtube.com`) and the mobile site (`m.youtube.com`).

## Add to uBlock Origin

### One-click install

> **[➕ Add to uBlock Origin](https://subscribe.adblockplus.org/?location=https%3A%2F%2Fraw.githubusercontent.com%2FYOUR_USERNAME%2FYOUR_REPO%2Fmain%2Fyoutube-cleanup-filters.txt&title=YouTube%20Cleanup)**

1. Make sure uBlock Origin is installed in your browser.
2. Click the link above.
3. In the page that opens, press **Subscribe**.

If nothing happens (for example, because several content blockers are installed), use the manual method below.

### Manual install (desktop)

1. Click the uBlock Origin icon in the toolbar, then open the **Dashboard** (gear icon).
2. Go to the **Filter lists** tab.
3. Scroll to the bottom and expand **Import...**.
4. Paste this link into the box:

   ```
   https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/youtube-cleanup-filters.txt
   ```

5. Click **Apply changes**.

### Manual install (Firefox for Android)

1. Open Firefox, tap the menu (⋮), and choose **Extensions**.
2. Tap **uBlock Origin**, then **Settings**.
3. Open the **Filter lists** tab and scroll to the bottom.
4. Tap **Import...** and paste the link from above.
5. Tap **Apply changes**.

### Alternative: paste into "My filters"

If you don't want to subscribe to a list, open the Dashboard, go to **My filters**, paste the contents of [`youtube-cleanup-filters.txt`](youtube-cleanup-filters.txt), and click **Apply changes**. You won't get automatic updates this way.

### Auto-dub rules and the "requires trusted source" message

The auto-dub section uses scriptlets that may need to be trusted. If uBlock Origin shows *"Invalid filter: Filter requires trusted source"* for those lines:

- **Subscribed list:** open the Dashboard → **Settings**, turn on **I am an advanced user**, click the gear icon next to it to open the advanced settings, and add this to `trustedListPrefixes`:

  ```
  https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/
  ```

- **"My filters":** turn on **Allow custom filters requiring trust** in uBlock Origin's settings.

Everything else in the list works without trust. Only trust lists you have read and are comfortable with, since trusted filters can run code on web pages.

## Features

| What | Details |
| --- | --- |
| **YouTube Shorts** | Removed everywhere: home feed, search, subscriptions, channel pages, the watch-page sidebar, the sidebar and bottom navigation bar entries, the Shorts tab and filter chip. Direct `/shorts/` links are blocked. |
| **Playables** | Game cards and shelves, the sidebar entry, and the `/playables` pages. |
| **AI features** | The "Ask" button, AI video summaries, "Ask YouTube" in search, and AI prompts in the feed. |
| **Auto-dubbed audio** | Strips auto-dubbed audio tracks so videos play in their original language (needs trust, see above). |
| **Premium upsells and promo banners** | Premium banners and pop-ups, promo bars, and the Premium entry in the sidebar. |
| **Shopping and merch** | Merch and product shelves, the "View products" badge on the player, and the channel Store tab. |

Where possible, the rules hide the whole card around a Shorts-marked video (not just its thumbnail), so you don't get empty gaps in your feed.

## Compatibility

- **Works with:** uBlock Origin (Firefox on desktop, Firefox on Android, and other browsers that support the full uBlock Origin extension).
- **Mobile:** the `m.youtube.com` rules only apply in a browser that runs uBlock Origin. They do **not** affect the YouTube app.
- **Not supported or not tested:** uBlock Origin Lite, Safari/iOS content blockers, and other blockers. This list uses uBlock Origin–specific syntax (procedural cosmetic filters such as `:upward()` and `:has-text()`, and scriptlets).

## Known limitations

- **Videos marked as AI** can't be hidden by this list. YouTube's "altered or synthetic content" label isn't shown on thumbnails in feeds, so there is nothing for a filter to match. Channel blocklists or dedicated extensions are the practical option.
- **YouTube changes its page structure often.** Rules can stop working after a redesign. If something reappears, please [open an issue](../../issues).
- **Text-based rules** (for example the "Ask" and "Summary" matches) rely on English labels and may not match other interface languages.
- **Rules marked "Unverified"** inside the list are best guesses and may need adjusting.

## Optional: always open the desktop site on mobile

uBlock Origin can't redirect `m.youtube.com` to `www.youtube.com`, but a userscript (Violentmonkey or Tampermonkey) can:

```js
// ==UserScript==
// @name         m.youtube.com → www.youtube.com
// @match        https://m.youtube.com/*
// @run-at       document-start
// @grant        none
// ==/UserScript==

location.replace(location.href.replace(/^https:\/\/m\.youtube\.com/, 'https://www.youtube.com'));
```

On a phone, also turn on your browser's **Desktop site** option for YouTube. Otherwise YouTube sends mobile browsers back to `m.youtube.com` and the page loops.

## Reporting problems

If something still shows up (or something it shouldn't hide disappears), open an issue with:

1. The page where it happens (home, search, watch page, channel, and so on) and whether you're on desktop or mobile.
2. A screenshot.
3. If you can, the element name from uBlock Origin's element picker (for example `ytd-...` or `ytm-...`).

## Contributing

Pull requests are welcome. Keep rules grouped by feature, add a short `!` comment for anything non-obvious, and mark guesses as "Unverified" until they have been tested.

## Credits

This list builds on the work of others:

- [gijsdev/ublock-hide-yt-shorts](https://github.com/gijsdev/ublock-hide-yt-shorts) (MIT) for the Shorts-hiding approach.
- [Vivian-Green/ublock-hide-yt-playables-too](https://github.com/Vivian-Green/ublock-hide-yt-playables-too) for the Playables card selector.
- [Fanboy's Anti-AI Suggestion List](https://github.com/easylist/easylist/blob/master/fanboy-addon/fanboy_ai_suggestions.txt) ([CC BY 3.0](https://creativecommons.org/licenses/by/3.0/)) for several YouTube AI selectors.
- The uBlock Origin community for the auto-dub scriptlet rules.
- Other community YouTube lists, for the Premium promo and merch selectors.

## License

Add your chosen license here (for example MIT). Check that it is compatible with the licenses of the lists credited above, and keep the attribution to Fanboy's list.
