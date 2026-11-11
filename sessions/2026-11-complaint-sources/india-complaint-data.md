# Indian consumer complaint data for seeding wtf.topc.social

Desk research, 2026-10-26. Every claim has a link; "not confirmed" means I looked and could not verify it.

## Bottom line

There is no legal way to reach ~1M real complaint texts about Indian companies. The big official pipes do carry that volume: the National Consumer Helpline (NCH) registered 12,35,710 grievances in FY2023-24, and RBI's ombudsman scheme received 13,34,244 complaints in FY2024-25. But they publish counts only, and mostly not per company. Where the public data does name companies, it's counts: NCH company-wise daily counts (306 companies, 2025, via Dataful), DGCA airline-wise complaints per 10,000 passengers every month, insurer-wise counts in the Insurance Ombudsman annual report, banks' own annual-report disclosures, and SEBI's monthly lists of entities with complaints pending more than three months. Government data in India is generally under GODL-India, which allows commercial reuse with attribution. The only sizeable source of real complaint *text* that names the company and can be republished is consumer commission and court judgments: the company is the named opposite party, and judgments are public records (reproducing judgments is an exception in Copyright Act s.52, but I couldn't fetch the official text to confirm the wording). They read like rulings, not rants, so they'd need summarising, and complainant names should be stripped. Complaint sites are out: consumercomplaints.in takes a licence for itself only and bans unauthorised commercial use, and MouthShut's terms wouldn't load. Reddit and X: their API licences allow display only, unmodified, through the API, with deletions honoured; Reddit needs its approval for commercial use. Fine for linking or embedding, not for seeding a wall. **Recommendation: seed with per-company count cards ("IndiGo: 0.2 complaints per 10,000 passengers, Dec 2024, source DGCA") plus summarised consumer-court cases, each with a source tag. Real rant text has to come from real users.**

## Table

| Source | What it has | Rough size | Names company? | Granularity | Licence / terms | Access | Verdict |
|---|---|---|---|---|---|---|---|
| NCH via Dataful (dataset 21453) | Day × sector × company grievances + refunds | 31,528 rows, 306 companies, 2025 | Yes | Counts | Dataful page states no licence; original is NCH (gov). Dataful T&C page didn't render | CSV/XLSX/JSON download | **Counts** (confirm Dataful terms, or cite NCH as the source) |
| NCH via Dataful (20715) | Year × company e-commerce grievances | FY21–FY26 | Yes | Counts | as above | download | **Counts** |
| NCH annual reports / Parliament answers | Totals by state/sector; no company tables in the FY21 report | 12.36 lakh grievances FY24 | Mostly no | Counts | Gov publication | PDF | Totals only |
| NCH public dashboard | — | — | — | — | Login required | — | Not usable |
| data.gov.in (NCH convergence companies 2016–19) | Complaints registered/disposed under convergence companies | 2.41 lakh (2018-19) | Not confirmed | Counts | GODL-India | Login; page returned HTTP 500 | Unconfirmed |
| CPGRAMS | Grievances against government ministries | ~1.96 lakh/month (June 2026) | No (ministries, not brands) | Counts | GODL-India | data.gov.in | Not usable for brands |
| e-Jagriti / CONFONET / Indian Kanoon | Consumer commission judgments | NCDRC + 36 state + 651 district commissions; count not confirmed | Yes (opposite party) | **Full text** (judgments) | Judgments are public records (s.52 exception, wording not verified); Indian Kanoon API is paid and requires its logo | Portal search; Indian Kanoon API (prepaid) | **Text, summarised** (strip complainant names) |
| RBI Integrated Ombudsman annual report | Complaints by bank *group* | 13,34,244 (FY25) | No, groups only | Counts | Gov publication | PDF | Not usable per brand |
| Banks' own annual reports (RBI-mandated disclosure) | Complaints received/pending, top 5 grounds, per bank | One table per bank per year | Yes | Counts | Public filings | PDF per bank | **Counts** |
| IRDAI annual report | Grievances on Bima Bharosa | 2,57,790 (FY25) | Insurer-wise annexure not confirmed | Counts | Gov publication | PDF | Unconfirmed |
| Council for Insurance Ombudsmen annual report | Insurer-wise complaints received and disposed | 52,575 complaints (FY24) | Yes (confirmed in the PDF) | Counts | Not stated | PDF | **Counts** |
| SEBI SCORES | Monthly totals + public notice naming entities pending >3 months | ~3,000–4,000/month; 7–13 named entities | Yes, only the laggards | Counts / names | Gov publication | Monthly press release / notice | **Counts (small)** |
| DGCA monthly traffic report | Airline-wise complaints per 10,000 pax, reasons | ~700–1,400 complaints/month | Yes (confirmed) | Rates | Gov publication | Monthly PDF | **Counts (best clean series)** |
| TRAI | Operator-wise complaint counts only in old Parliament answers | 30,131 (2019) | Yes (old) | Counts | Gov | eparlib PDFs | Old counts only |
| MahaRERA | Complaints filterable promoter-wise, orders | ~17,887 complaints (May 2022) | Yes | Counts + orders | Not checked | Portal | Possible counts/orders; unverified |
| consumercomplaints.in | User complaints | Size not found | Yes | Full text | Licence granted to the site only; "personal use only"; unauthorised commercial use prohibited | Scraping | **Not usable** |
| MouthShut | Reviews | 800,000+ products and services (Wikipedia) | Yes | Full text | Terms page returned 403; not confirmed | — | Not usable until terms are read; assume no |
| Voxya | User complaints | Not found | Yes | Full text | Terms not checked | — | Assume no |
| Akosha | — | — | — | — | Not researched (pivoted long ago; not confirmed here) | — | — |
| Reddit | Posts/comments | — | Sometimes | Full text | Data API licence: display only, unmodified, commercial use needs Reddit's approval (secondary sources; redditinc.com blocked) | API | Link/embed only |
| X | Posts at brand handles | — | Yes (@brand) | Full text | Display via API only, no text changes, delete within 24h on request, no redistribution | Paid API | Embed only |
| Hugging Face: faizmubeen/indian_railways_complaint_tweets | ~4,500 tweets about Indian Railways | 4.5k | One entity | Text | Tagged MIT, but the tweets are covered by X's terms | Download | Not usable for seeding |
| Mendeley: Citizen complaints on Twitter | Tweets to @RailMinIndia, @IncomeTaxIndia, @DelhiPolice, @dtpTraffic | Not stated | Government bodies, not brands | Text | CC BY 4.0 (tweets still covered by X's terms) | Download | Not usable (not brands) |
| Hugging Face: ml-hub/flipkart-reviews | 40k product reviews | 40k | Products, not complaints | Text | No licence tagged | Download | Not usable |
| Kaggle | Only US CFPB mirrors found; no Indian complaint set | — | — | — | — | — | Nothing found |
| Google Play reviews | App reviews | Large | Yes | Text | Google's ToS restricts automated access; the official API returns your own apps only | — | Not usable |

## Per-source notes

### National Consumer Helpline (NCH / INGRAM)
- Volume: 10,05,985 grievances in FY2022-23 and 12,35,710 in FY2023-24 (state-wise annexure); about 1,11,951 a month in 2024; 1,049 convergence partner companies. [Lok Sabha USQ 2197, 12.03.2025](https://fcainfoweb.nic.in/PMS/writereaddata/2025_LS_B_2197.pdf)
- The FY2020-21 annual report: 6,74,820 dockets, with sector and state tables but no company-wise counts table (I downloaded and searched it; it only mentions company-specific analyses shared internally). [Annual Report 2020-21](https://consumerhelpline.gov.in/public/assets/docs/annual-reports/Annual%20Report%202020-21.pdf). Other years: [2018-19](https://consumerhelpline.gov.in/public/assets/docs/annual-reports/Annual_Report_2018-19.pdf), [2019-20](https://consumerhelpline.gov.in/public/assets/docs/annual-reports/Annual%20Report%202019-20.pdf).
- Company-wise counts exist through Dataful (a Factly product): [dataset 21453](https://dataful.in/datasets/21453/) has date, sector, company, category and value columns: 31,528 rows, 306 companies, 2025, updated daily, original source listed as the NCH dashboard (which needs a login: [consumerhelpline.gov.in/public/dashboard/Home](https://consumerhelpline.gov.in/public/dashboard/Home)). No licence on the page; the [collection](https://dataful.in/collections/985/) also has year × company e-commerce grievances for FY21–FY26. I couldn't read Dataful's T&C page (it rendered empty), so confirm the terms or ask Factly before republishing.
- Press example of company-level NCH numbers: Factly reports Flipkart had 1,60,857 of 4,45,960 e-commerce grievances in FY2023-24 ([factly.in](https://factly.in/data-in-the-last-4-years-more-than-30-of-grievances-registered-against-e-commerce-companies-on-the-national-consumer-helpline-were-related-to-flipkart); the page returned 403 to me, so the figure comes from search snippets only).
- data.gov.in community post on convergence-company complaints, 2016-17 to 2018-19 ([link](https://community.data.gov.in/?p=108196)): returned HTTP 500 and needs a login, so I couldn't confirm whether it names companies.

### Licence for government data
- GODL-India: worldwide, royalty-free, commercial use allowed, attribution required. Secondary summaries: [OSM wiki](https://wiki.openstreetmap.org/wiki/Open_Geospatial_Data_from_Government_of_India), [Wikimedia template](https://c.enwp.org/wiki/Template:GODL-India). It covers data.gov.in datasets. PDF reports from ministries and regulators don't carry an explicit licence, but per-company counts are facts; cite the source.

### CPGRAMS
- Grievances against government departments, not brands. State-wise datasets on [data.gov.in](https://www.data.gov.in/resource/stateut-wise-details-pending-and-received-complaints-cpgrams-centralized-public-grievance); 1,96,133 cases received in June 2026 ([PIB](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2026/jul/doc2026729936301.pdf)). Not useful for company tags.

### Consumer commissions (e-Daakhil / CONFONET → e-Jagriti)
- e-Jagriti merged e-Daakhil, OCMS, CMS and CONFONET on 1 Jan 2025; it covers the NCDRC, 36 state commissions and 651 district commissions ([Wikipedia](https://en.wikipedia.org/wiki/E-Jagriti), [Rajya Sabha answer](https://rsdebate.nic.in/bitstream/123456789/748111/1/PQ_263_09022024_U869_p284_p284.pdf)). Not confirmed: whether bulk download or an API exists, or how many judgments are public.
- Judgments name the company as opposite party and carry the complaint facts. Copyright Act s.52(1)(q) makes reproducing court/tribunal judgments non-infringing (my recollection; I couldn't fetch [copyright.gov.in/Exceptions.aspx](https://www.copyright.gov.in/Exceptions.aspx) to confirm the wording).
- Indian Kanoon API: lets you show its documents on your own site; prepaid pricing; logo attribution required ([terms](https://api.indiankanoon.org/terms/)). There's been litigation over name-based search for litigants ([Bar & Bench](https://www.barandbench.com/amp/story/news/objectionable-delhi-high-court-on-legal-resource-portals-changing-para-numbers-of-judgments)), so strip complainant names.

### RBI Integrated Ombudsman
- FY2024-25: 13,34,244 complaints under RB-IOS; the tables are by bank *group* (public, private, small finance, foreign), no named banks ([report](https://rbi.org.in/scripts/PublicationsView.aspx?id=23441)). The older Banking Ombudsman reports (2019-20) had a bank-wise distribution (search snippet only).
- Per-bank numbers: RBI requires each bank to disclose in its annual report the complaints received and pending and its top five grounds ([RBI circular index](https://www.rbi.org.in/Scripts/BS_CircularIndexDisplay.aspx?Id=12017), [summary](https://www.gconnect.in/news/strengthening-grievance-redress-mechanism-banks.html)). That means collecting one table per bank by hand.

### Insurance
- IRDAI Annual Report 2024-25: 2,57,790 grievances (1,20,429 life, 1,37,361 general and health) ([Outlook Money](https://www.outlookmoney.com/insurance/insurance-claims-mis-selling-account-for-most-insurance-complaints-in-fy25-reveals-irdai-annual-report)). Whether there's an insurer-wise annexure: not confirmed.
- Council for Insurance Ombudsmen, Annual Report 2023-24: insurer-wise tables confirmed in the PDF (e.g. Star Health and Allied, 13,308 complaints); 52,575 complaints in total ([PDF](https://cioins.co.in/annualreports/AnnualReport2023-2024.pdf)). FY25 per press: Star Health 12,186, Care Health 4,423, Niva Bupa 3,983 ([Insurance Business](https://www.insurancebusinessmag.com/asia/news/life-insurance/latest-india-data-finds-complaints-clustered-in-insurance-segment-565197.aspx)).
- Insurers also publish their own grievance disclosure (form NL-45), e.g. [Go Digit](https://www.godigit.com/content/dam/godigit/general/financials/public-disclosure/fy-26-27/nl-45-grievance-disposal.pdf).

### SEBI SCORES
- Monthly releases give totals and name entities with complaints pending more than three months (e.g. 13 entities as of Dec 2023; Oct 2023 included SBI MF, UTI MF and JSW Steel) ([Outlook Business](https://www.outlookbusiness.com/news/sebis-scores-resolves-over-3000-complaints-in-december), [Business Standard](https://www.business-standard.com/amp/markets/news/sebi-resolves-2-838-complaints-against-firms-via-scores-platform-in-march-123041100569_1.html)). I couldn't reach SEBI's own statistics page (404). Small, but names companies.

### DGCA
- The monthly domestic traffic report has a "Passenger Complaints" section with **airline-wise complaints per 10,000 passengers** and reasons. Confirmed in the December 2024 report: 817 complaints, 0.55 per 10,000 overall; Fly Big 26.4, SpiceJet 4.2, Alliance Air 3.1, Star Air 3.0, Air India 0.9, Fly91 0.8, Akasa 0.4, IndiGo 0.2 (copy of the DGCA PDF, ["Performance of domestic airlines for the year 2024"](https://livefromalounge.com/wp-content/uploads/2025/01/Traffic-Data-Report-December-24.pdf)). The official home is DGCA's Data & Reports → Domestic Air Transport → Monthly ([dgca.gov.in](https://www.dgca.gov.in/digigov-portal/?page=jsp/dgca/InventoryList/dataReports/aviationDataStatistics/airTransport/domestic/airTraffic/domestic.html)); Aug 2025: 1,407 complaints, 1.09 per 10,000 ([Deccan Herald](https://www.deccanherald.com/india/domestic-air-traffic-falls-to-129-crore-in-august-flight-delays-hit-74381-passengers-dgca-data-3751393)). Note: rates, not raw counts per airline (convert using each airline's passenger numbers from the same report).

### TRAI
- TRAI doesn't handle individual complaints (it forwards them to operators). Operator-wise counts appear only in Parliament answers, e.g. 30,131 complaints in 2019 ([eparlib](https://eparlib.nic.in/bitstream/123456789/974044/1/AU647.pdf); other years in [this answer](https://eparlib.nic.in/bitstream/123456789/636142/1/136148.pdf)). No current regular series found.

### RERA
- MahaRERA lets you list complaints promoter-wise or project-wise on its portal ([guide](https://www.homebazaar.com/knowledge/how-to-find-project-details-on-the-maharera-website/)); 17,887 complaints as of May 2022 ([PropertyPistol](https://www.propertypistol.com/blog/maharera-website-to-feature-complaints-about-projects-promoters/)). Terms and bulk access not checked.

### Complaint sites
- **consumercomplaints.in** ([terms](https://www.consumercomplaints.in/terms-conditions.html)): posters grant the *site* an irrevocable licence; the authors keep ownership; "The Service is provided to individuals only and for personal use only"; "Any unauthorized commercial use of the Service ... is expressly prohibited." No licence to third parties, so not usable. Size not found.
- **MouthShut**: 800,000+ products and services ([Wikipedia](https://en.wikipedia.org/wiki/MouthShut.com)); its terms page returned 403, so not confirmed. Treat as not usable.
- **Voxya**: still running, with user complaints naming companies ([voxya.com](https://voxya.com/)); terms not checked. Akosha: not researched.

### Social
- **Reddit**: under the older Data API terms, licence to "copy and display the User Content using the Reddit API through your application ... to end users", no modification beyond formatting ([copy of the old terms](https://members.loria.fr/KFort/?p=406)); commercial use needs Reddit's approval ([The Register](https://www.theregister.com/2023/04/18/reddit_charging_ai_api/)). redditinc.com couldn't be fetched. Fine for embedding with links; not for seeding.
- **X**: [Developer Agreement](https://docs.x.com/developer-terms/agreement): display a "reasonable amount", no edits beyond formatting, no redistribution, delete within 24 hours on request; the API is paid. Embed only.
- Datasets of tweets: [Indian Railways complaint tweets](https://huggingface.co/datasets/faizmubeen/indian_railways_complaint_tweets) (~4,500, tagged MIT); [Mendeley citizen complaint tweets](https://data.mendeley.com/datasets/w2cp7h53s5) (CC BY 4.0, government accounts). The dataset licence doesn't override X's terms on the tweet text.

### Kaggle / Hugging Face
- Kaggle "consumer complaints" sets found are US CFPB mirrors ([example](https://baselight.app/u/kaggle/dataset/meetnagadia_consumer_complaint_finance)). No Indian brand-complaint dataset found on Kaggle or Hugging Face (I searched the Hub API for "india complaint", "indian consumer", "flipkart reviews", "indian tweets"). [onionsalad/india-complaint-directory](https://huggingface.co/datasets/onionsalad/india-complaint-directory) (CC0) is a directory of grievance channels, not complaints. Useful for routing users to where to file.

## What I couldn't confirm
- Dataful's licence and terms; whether the NCH company-wise data is free to download.
- IRDAI insurer-wise annexure; SEBI's own statistics pages; the official DGCA monthly PDF URLs (I confirmed the content through a third-party copy).
- e-Jagriti bulk access and judgment counts; exact s.52(1)(q) wording.
- MouthShut, Voxya and Reddit's current terms (pages blocked); consumercomplaints.in's size.
