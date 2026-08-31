# HOTEL 2 FEVRIER — Project Status

Last updated: 2026-08-31

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
8. `4a10c9f3e7b24d8a9c01` — Fiscalité & conformité

## Important hidden/detail pages

- `9834d9fea5a59ae826a2` — Détail facture et relance
- `1fb9e97f0f6a47d9ac62` — Documents liés à la facture
- `20caa08f3d1b4f0fb073` — Dossier client
- `5da760addaad4b708968` — Détail performance
- `72a1c9530c8b4ed8a101` — Détail de l'activité
- `72b2d0641d9c4fe9b202` — Détail exploitation
- `72c3e1752ead40fac303` — Détail RH
- `72d4f2863fbe41abd404` — Détail stocks
- `4b21d0e4f8c35e9b0d12` — Dossier d’obligation
- `4c32e1f5a9d46f0c1e23` — Détail des situations CNSS

## Document base

Implemented and validated:

- SharePoint folder `DOCUMENTS-DEMO`
- Subfolders: `Factures`, `Commandes`, `Justificatifs`, `Conformite`
- Excel structured table: `Documents`
- Semantic model table: `DocumentTable`
- Documents page with filters and clickable SharePoint links
- Invoice -> related documents contextual access
- Client dossier with profile, invoices, orders and documents
- Documents/client filter is based on `PartnerTable`

Current demo document count: 24.

## Fiscalité et conformité

Initial scope implemented on `feature/fiscalite-conformite`; dossier redesign implemented on `feature/compliance-dossier-redesign`:

- Excel tables `ComplianceObligationTable`, `ComplianceTrackingTable`, `ComplianceReconciliationTable` and `EmployeeComplianceTable`;
- semantic-model relationships to dates, employees, cash movements and documents;
- DAX status, aging, payment, evidence, reconciliation and CNSS indicators;
- visible paper-style page `Fiscalité & conformité`, hidden drillthrough page `Dossier d’obligation` and hidden page `Détail des situations CNSS`;
- navigation from all eight visible pages;
- eight fictitious compliance evidence records in `Documents` and nine explicitly marked fictitious PDF files under `DOCUMENTS-DEMO/Conformite`.

The redesign removes the global blue sidebar, analytical charts and nominal employee grid from the main compliance page. It uses narrative status cards, a prioritized obligation register, a documentary panel and a non-nominal CNSS summary. Status measures now map the source values `Clôturé`, `Ouvert` and `À confirmer` to operational states used by the report. The reconciliation-to-cash relationship is inactive to prevent an ambiguous filter path to `DateTable`.

The dashboard is a control framework, not a legal conclusion. Applicability and client-side ownership remain `À confirmer`; official-source URLs and verification dates are stored in the obligation register.

## Financial-model conventions

- Revenue and purchases are handled HT in the finance analysis.
- Personnel cost currently uses base salary + bonuses and excludes employer charges.
- `Résultat de gestion` is an indicative management result, not a statutory accounting result.
- It excludes amortisation, finance charges, tax and employer charges where data is unavailable.
- `Achats directs` must not be presented as an exact COGS/stock-consumption valuation.

## Design direction

- blue/navy primary theme inspired by the DAF mockup
- light blue/grey page background
- white content cards
- teal for favourable values
- orange for warnings / operational metrics
- red for negative or unfavourable values
- consistent rounded cards and compact spacing
- French user-facing labels only; avoid internal model field names in subtitles
- KPI tooltip principle: the card gives the headline value; the hover tooltip gives only 2–3 supporting values, not a second report page

The Tableau de bord page remains the visual reference for analytical pages. **Fiscalité & conformité** is the deliberate exception: it follows a warm paper-dossier system because the task is administrative review rather than performance analysis.

## Current cleanup sequence

1. Tableau de bord
2. Trésorerie
3. Exploitation
4. Ressources humaines
5. Achats et stocks
6. Performance financière
7. Documents
8. Fiscalité & conformité

## Known implementation lessons

- Fabric validates report JSON more strictly than plain JSON parsing.
- Avoid malformed duplicated formatting objects, especially `outline`, `border`, `visualLink`, `subTitle` and table-formatting arrays.
- New or modified report JSON must be generated/parsed structurally before a Fabric-facing commit.
- When a formatting error pattern is found, audit all sibling/generated visuals for the same pattern before retrying Fabric.
- Prefer small, testable chunks and run Fabric `Update all` after each cleanup/feature chunk.
- Drillthrough starts from a row carrying `Suivi_ID`; use right-click > Extraire when no selected-row drillthrough button context is available.

## Current checkpoint

Next action: open `feature/compliance-dossier-redesign` in Power BI/Fabric, run `Update all`, refresh the semantic model, then validate the compliance overview, obligation drillthrough, CNSS navigation, links and filtering before merge.
