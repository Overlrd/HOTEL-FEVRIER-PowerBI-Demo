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

1. `b439328a601fc7db4685` — Vue d'ensemble
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
- `72a1c9530c8b4ed8a101` — Détail activité
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
- keep existing page names unless a deliberate navigation-wide rename is approved

The Vue d'ensemble page is the design reference page. Other pages should be cleaned up one by one only after this page is validated in Fabric.

## Current cleanup sequence

1. Vue d'ensemble — in progress
2. Trésorerie
3. Exploitation
4. Ressources humaines
5. Achats et stocks
6. Performance financière
7. Documents

## Known implementation lessons

- Fabric validates report JSON more strictly than plain JSON parsing.
- Avoid malformed duplicated formatting objects, especially `outline`, `border`, `visualLink` and table formatting arrays.
- New visual JSON must be locally JSON-parsed before commit.
- Prefer small, testable chunks and run Fabric `Update all` after each cleanup/feature chunk.
- Drill-through buttons remain disabled unless Power BI has the correct visual selection context. Use normal page navigation when the intended flow starts from slicers or general page context.

## Last validated functional checkpoint

Before the Vue d'ensemble visual cleanup, Fabric accepted the report with:

- Documents page working
- SharePoint links opening in a new tab
- invoice -> documents flow
- Dossier client page
- client filter/navigation flow

Git checkpoint before this visual cleanup: `7ab6d76b`.

## Next work after Vue d'ensemble validation

Continue page-by-page cleanup. No new large feature should be added until the current page cleanup is validated visually and in Fabric.
