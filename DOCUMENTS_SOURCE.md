# Source documentaire — Hôtel 2 Février

Cette phase ajoute uniquement la fondation documentaire. Le modèle Power BI n'est pas encore modifié.

## Stockage

Les fichiers de démonstration sont stockés dans SharePoint sous :

`HOTEL2FEVRIER/POWERBI-DEMO/DOCUMENTS-DEMO/`

Sous-dossiers :
- `Factures`
- `Commandes`
- `Justificatifs`

Le classeur source reste :

`Hotel_2_Fevrier_Donnees_Demo_PowerBI.xlsx`

## Table Excel `Documents`

La nouvelle table `Documents` contient 16 pièces de démonstration liées à des références existantes du classeur.

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

`Document_URL` contient l'URL SharePoint directe de la pièce et servira de champ Web URL dans Power BI.

## Données de démonstration

Le registre contient :
- 6 factures client ;
- 6 commandes associées ;
- 4 justificatifs de paiement.

Les documents couvrent notamment Groupe Horizon Afrique, Banque Atlantique Togo, Lomé Business Travel, Association Régionale, Jean-Paul Dossou et Mariam Diallo.

Toutes les pièces et données sont fictives et servent uniquement à la démonstration.

## Prochaine phase

Importer `Documents` dans le modèle sémantique, tester les relations par `Facture_ID`, `Commande_ID` et `Client_ID`, puis seulement après validation ajouter une page Documents au rapport.
