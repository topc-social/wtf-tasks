# e-Jagriti: can we bulk-pull district consumer orders by brand?

Checked 2026-10-26, hands-on (curl + reading the site's own JS bundle).

## Bottom line

**Verdict: partly.** The data we want exists and e-Jagriti exposes exactly the right search: judgments filtered by **Respondent / Opposite Party** name (or free text), for any **district commission**, by filing or disposal date, with the **judgment file included in the result row**. But every public search form sits behind an **image captcha**. Using it the intended way means a human solves one captcha per query. We didn't look for ways around it. That rules out automated, unattended bulk pulls through e-Jagriti on our own.

**Smallest free, legal path to thousands of cases:**
1. **Ask for the data.** Email the e-Jagriti helpdesk (helpdesk-ejagriti@nic.in, per secondary sources) or the Department of Consumer Affairs for bulk or API access to disposed district judgments by respondent. If that stalls, file an RTI. The site's own terms ask for permission before reproducing its material (quoted below), so asking also covers that point. This is the only route to thousands per brand that is both automated and clean.
2. **Meanwhile, a human-in-the-loop seed set.** A person uses the public Judgment search in a normal browser: pick a district, search type "Respondent / Opposite Party" = "INTERGLOBE" (or "INDIGO"), order type Judgement, solve one captcha, then page through results 30 at a time. Save case number, date, commission, respondent and outcome. Leave out complainant names. Link to e-Jagriti. This is slow: one captcha per district per brand, and there are hundreds of district commissions. Enough for a credible launch wall (hundreds of cases); thousands per brand this way would be a lot of manual work.
3. **Possible paid-but-free-tier alternative:** the Indian Kanoon API (₹0.50/search, ₹0.20/doc, ₹500 signup credit, and up to ₹10,000/month free for verified non-commercial use). **Not confirmed:** whether Indian Kanoon actually carries *district* consumer orders, and whether its terms allow republishing.

No free open bulk dataset of district consumer orders turned up (data.gov.in, GitHub, Kaggle, HuggingFace).

## 1. Public case and judgment search

e-Jagriti is a single-page app. Public pages: `/judgement`, `/judgements`, `/advance-case-search`, `/casestatus`, `/case-history-case-status`, `/cause-list`, `/analytics`.

**Judgment search (`/judgement`)** fields:
- Commission: NCDRC / SCDRC / DCDRC (required). DCDRC also needs a State and a District, so there is **no all-districts search**.
- Search type: "Search by Free Text" or "More Advanced".
- Advanced "search by": CASE NUMBER, COMPLAINANT / APPELLANT / PETITIONER, **RESPONDENT / OPPOSITE PARTY**, complainant advocate, respondent advocate, INDUSTRY TYPE (case category dropdown), JUDGE.
- Date type: CASE FILING DATE or CASE DISPOSAL DATE, with from/to dates. Optional for free-text search.
- Order type: DAILY ORDER / JUDGEMENT.
- **Captcha: required** before every search.
- Results come 30 per page, with no total count (the UI guesses "has more" when a page is full).
- Result columns: filing date, (disposal date), stage, case number, **complainant name**, complainant advocate, respondent name, respondent advocate, Daily Order "View", Judgement "View".

**Advance Search (`/advance-case-search`)** offers free text by complainant/respondent name or "More Advance Search" for SCDRC/DCDRC, and is also behind a captcha.

**Login/OTP:** not needed for these searches; only the captcha.

## 2. The site's own API

Left out of this public copy on purpose. In short: the frontend talks to a JSON API, search results come back with the judgment file attached, and every search is meant to sit behind the captcha. We did not call any search endpoint and didn't try to get around the captcha.

## 3. Order document format

- **Not fetched from e-Jagriti** (that needs the captcha search).
- From the site's code, a judgment is shown as a PDF or as HTML, and judges can also type or paste a judgement, which suggests a mix of typed (text) and uploaded scanned orders. **Unconfirmed** which share is text and which is scans.
- Spot check from another source: LiveLaw's copy of a Delhi North district order against IndiGo (CC/76/2019) (`https://www.livelaw.in/pdf_upload/2026/09/16/adobe-scan-03-sept-2026-1-700333.pdf`) is a 24-page **Adobe Scan image PDF; pdftotext gives nothing**, so it would need OCR. That is LiveLaw's own scan, not e-Jagriti's file.

## 4. Volume per brand

**Unconfirmed.** Brand counts are only reachable through the captcha search, and even that shows no totals (30 per page, no count). News coverage confirms a steady flow of district orders against IndiGo/InterGlobe (Delhi North, Ernakulam, Chandigarh), but that gives no numbers. For scale only: a 2018 Lok Sabha answer put the total at 50.9 lakh consumer cases filed across all fora since inception (eparlib.nic.in/bitstream/123456789/806200/1/AU385.pdf, via search snippet).

## 5. Rate limits, robots.txt, terms

- **robots.txt:** `https://e-jagriti.gov.in/robots.txt` returns 200, but the body is the SPA's `index.html`, byte-identical. **There is effectively no robots.txt.**
- **Rate limits:** no rate-limit headers on the 3 calls. The frontend retries up to 5 times on "jdbc" errors, a sign of a fragile backend. Untested beyond that.
- **Captcha** on all public search forms (above).
- **Site terms, verbatim from the policy chunks:**
  - Disclaimer (`/disclaimer`): "Material featured on this website may be reproduced free of charge after taking proper permission by sending a mail to us. However, the material has to be reproduced accurately and not to be used in a derogatory manner or in a misleading context. Wherever the material is being published or issued to others, the source must be prominently acknowledged."
  - Website policies (`/website-policies`): "Contents of this website may not be reproduced partially or fully, without due permission from the Department of Consumer Affairs. It's content, if referred to and/or forms a part of content of another website, the content-source must be appropriately acknowledged. The contents of this website cannot be used in any misleading or objectionable context."
  - Terms of service (`/terms-of-service`): "Material featured on this website, if used, has to be reproduced accurately and should not be used in a derogatory manner or in a misleading context. Wherever the material is being published or issued to others, the source must be prominently acknowledged."
  - Hyperlinking (`/terms-and-conditions`): "We do not object to you linking directly to the information that is hosted on this website and no prior permission is required for the same. However, we would like you to inform us about any links provided to this website…" Framing is not allowed.
- **Copyright Act 1957 s.52(1)(q)(iv)** (text via Indian Kanoon, indiankanoon.org/doc/648494; the official copyright.gov.in page wouldn't load here because of a certificate error): not an infringement is "the reproduction or publication of— … (iv) any judgment or order of a court, Tribunal or other judicial authority, unless the reproduction or publication of such judgment or order is prohibited by the court, the Tribunal or other judicial authority, as the case may be;"
  - What this means (not legal advice): the orders themselves are reusable, and linking is explicitly allowed without permission. The portal's own "ask permission" terms cover its material (the database or compilation). One-line summaries plus links to e-Jagriti sit on the safe side; mass-copying the PDFs out of the portal is where permission matters.

## 6. Other free bulk sources

- **CONFONET's old hosts:** `confonet.nic.in`, `cms.nic.in`, `edaakhil.nic.in` all give **DNS failure** (gone). `ncdrc.nic.in` is up (200): bare acts and NCDRC pages, not district orders.
- **data.gov.in:** no consumer-commission case or judgment dataset found by search. Only aggregate filed/disposed figures turn up, in Parliament answers and state commission PDFs.
- **NJDG / eCourts:** consumer commissions are outside eCourts, as expected. Not useful.
- **GitHub:** no e-Jagriti scraper found (the search turned up only eCourts scrapers).
- **HuggingFace / Kaggle:** no district consumer-order dataset found. Grahak-Nyay (arXiv 2507.04854) says it used consumer court judgments and promises a release; **unconfirmed** whether it is out or what licence it has.
- **Indian Kanoon:** has a "Consumer Disputes Redressal" tribunal category (`/browse/consumer/`, years 1989 onward). Its robots.txt **disallows `/search/`**, so no scraping. API pricing (api.indiankanoon.org/pricing): search ₹0.50, document ₹0.20, ₹500 signup credit, ₹10,000/month free for non-commercial use after verification. **Unconfirmed:** district-commission coverage, and terms on republishing.

## Unconfirmed

- Whether e-Jagriti judgment files are mostly text PDFs, HTML or scans.
- Case counts per brand.
- Rate limiting under real load.
- Whether DoCA/NIC grant bulk or API access (nobody has asked yet).
- Indian Kanoon's district coverage and reuse terms.
- Whether the Grahak-Nyay dataset has been released.
