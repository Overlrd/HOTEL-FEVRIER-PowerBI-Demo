# Source documentaire — Hôtel 2 Février

Le registre documentaire alimente la page Documents et les preuves de la page Fiscalité & conformité.

## Stockage

Les fichiers de démonstration sont stockés dans SharePoint sous :

`HOTEL2FEVRIER/POWERBI-DEMO/DOCUMENTS-DEMO/`

Sous-dossiers :
- `Factures`
- `Commandes`
- `Justificatifs`
- `Conformite`

Le classeur source reste :

`Hotel_2_Fevrier_Donnees_Demo_PowerBI.xlsx`

## Table Excel `Documents`

La table `Documents` contient 24 pièces de démonstration liées à des références existantes du classeur et aux suivis de conformité.

Colonnes :
- `Document_ID`
- `Type_Document`
- `Reference`
- `Client_ID`
- `Nom_Client`
- `Entite_Type`
- `Entite_ID`
- `Commande_ID`
- `Facture_ID`
- `Date_Document`
- `Montant`
- `Statut_Document`
- `Nom_Fichier`
- `Document_URL`
- `Dossier`

`Document_URL` contient l'URL SharePoint directe de la pièce et sert de champ Web URL dans Power BI.

## Données de démonstration

Le registre contient notamment :
- 6 factures client ;
- 6 commandes associées ;
- 4 justificatifs de paiement ;
- 8 preuves fiscales, sociales ou réglementaires fictives.

Les documents couvrent notamment Groupe Horizon Afrique, Banque Atlantique Togo, Lomé Business Travel, Association Régionale, Jean-Paul Dossou et Mariam Diallo.

Toutes les pièces et données sont fictives et servent uniquement à la démonstration. Les PDF du dossier `Conformite` portent une mention visible indiquant qu'ils n'ont aucune valeur administrative ou fiscale.

## Modèle

`DocumentTable` est importée dans le modèle sémantique. Les documents de conformité sont reliés aux rapprochements via `Document_ID`; les liens `Document_URL` et `Preuve_URL` sont catégorisés comme URL web.
