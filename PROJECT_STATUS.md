# HOTEL 2 FEVRIER — Project Status

Last updated: 2026-08-26

## Purpose

Power BI demo for Hôtel 2 Février, targeted at a DAF / finance-management audience. The report uses an Excel workbook stored in SharePoint as the current demo data source.

## Current demo source

- SharePoint tenant: `ivorygoldconsulting-my.sharepoint.com`
- Personal site: `/personal/augustin_kpadonou_ivorygoldglobal_com`
- Folder: `HOTEL2FEVRIER/POWERBI-DEMO`
- Workbook consumed by the semantic model: `Hotel_2_Fevrier_Donnees_Demo_PowerBI.xlsx`
- Do not rename the workbook without updating every semantic-model Power Query partition.

## Current visible pages

1. `b439328a601fc7db4685` — Tableau de bord
2. `99dab0509d84bfba0c6c` — Trésorerie
3. `d17cbae5e73cb06aa65c` — Exploitation
4. `931df8dd8347317259b3` — Ressources humaines
5. `a6f3c9e72b145d8091fa` — Achats et stocks
6. `e5a591c45102421280f3` — Performance financière
7. `1fa8d86ede5f462ebf51` — Documents

## Important hidden/detail pages

- `9834d9fea5a59ae826a2` — Détail facture et relance
- `1fb9e97f0f6a47d9ac62` — Documents liés à la facture
- `20caa08f3d1b4f0fb073` — Dossier client
- `5da760addaad4b708968` — Détail performance
- `72a1c9530c8b4ed8a101` — Détail de l'activité
- `72b2d0641d9c4fe9b202` — Détail exploitation
- `72c3e1752ead40fac303` — Détail RH
- `72d4f2863fbe41abd404` — Détail stocks

## Document base

Implemented and validated:

- SharePoint folder `DOCUMENTS-DEMO`
- Subfolders: `Factures`, `Commandes`, `Justificatifs`
- Excel structured table: `Documents`
- Semantic model table: `DocumentTable`
- Documents page with filters and clickable SharePoint links
- Invoice -> related documents contextual access
- Client dossier with profile, invoices, orders and documents
- Documents/client filter is based on `PartnerTable`

Current demo document count: 16.

## Financial-model conventions

- Revenue and purchases are handled HT in the finance analysis.
- Personnel cost currently uses base salary + bonuses and excludes employer charges.
- `Résultat de gestion` is an indicative management result, not a statutory accounting result.
- It excludes amortisation, finance charges, tax and employer charges where data is unavailable.
- `Achats directs` must not be presented as an exact COGS/stock-consumption valuation.

## Design direction

Reference design approved for cleanup:

- blue/navy primary theme inspired by the DAF mockup
- light blue/grey page background
- white content cards
- teal for favourable values
- orange for warnings / operational metrics
- red for negative or unfavourable values
- consistent rounded cards and compact spacing
- French user-facing labels only; avoid internal model field names in subtitles
- KPI tooltip principle: the card gives the headline value; the hover tooltip gives the diagnostic / explanation rather than repeating the KPI

The Tableau de bord page is the visual reference page. Other pages should be cleaned up one by one after this page is stable.

## Current cleanup sequence

1. Tableau de bord — cleanup substantially complete; diagnostic tooltips awaiting Fabric validation
2. Trésorerie
3. Exploitation
4. Ressources humaines
5. Achats et stocks
6. Performance financière
7. Documents

## Diagnostic KPI tooltips

Current implementation commit: `70e402f6` — awaiting Fabric validation.

Implemented without changing the Excel source:

- Chiffre d'affaires: budget, budget variance in XOF and %, previous-period evolution, leading revenue activity
- Résultat de gestion: CA HT, direct purchases, personnel, operating expenses, result vs budget, previous-period evolution
- Trésorerie: opening balance, receipts, payments, net flow, previous-month evolution
- Recouvrement: overdue invoice count, average delay, maximum delay, overdue share, largest overdue debtor
- Exploitation: available/sold rooms, occupancy evolution, room revenue
- Revenu par chambre disponible: average realised rate, previous-period RevPAR and RevPAR evolution

Tooltip-only measures are kept in `PointsSuivi.tmdl` to avoid unnecessary changes to the core source tables.

## Known implementation lessons

- Fabric validates report JSON more strictly than plain JSON parsing.
- Avoid malformed duplicated formatting objects, especially `outline`, `border`, `visualLink`, `subTitle` and table-formatting arrays.
- New or modified report JSON must be generated/parsed structurally before a Fabric-facing commit; do not hand-edit brace-heavy JSON when avoidable.
- When a formatting error pattern is found, audit all sibling/generated visuals for the same pattern before retrying Fabric.
- Prefer small, testable chunks and run Fabric `Update all` after each cleanup/feature chunk.
- Drill-through buttons remain disabled unless Power BI has the correct visual selection context. Use normal page navigation when the intended flow starts from slicers or general page context.

## Current checkpoint

Base before diagnostic-tooltip work: `6992db7d`.

Current main implementation: `70e402f6` plus this tracking-document update.

Next action: Fabric `Update all`, validate the semantic-model measures and the four redesigned tooltip pages, then visually confirm the hover experience on all six KPI cards.

## Next work after Tableau de bord validation

Continue page-by-page cleanup. No additional large feature should be added until the current dashboard/tooltips are validated visually and in Fabric.
