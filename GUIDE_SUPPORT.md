# Guide support — Dashboard Hôtel 2 Février

**Version : 0.3 — Performance financière**

La page Performance financière donne au DAF une lecture de gestion combinant réalisé, budget, rentabilité par activité et accès aux écritures sources.

## KPI
- Chiffre d'affaires HT : commandes de vente terminées, montant HT.
- Achats directs HT : achats terminés affectés aux activités selon la catégorie.
- Marge sur achats : CA HT − achats directs HT.
- Coût personnel disponible : salaire de base + primes.
- Charges d'exploitation : table Excel `ChargesExploitation`.
- Résultat de gestion disponible : CA HT − achats directs HT − personnel disponible − charges d'exploitation.
- Taux de marge gestion : résultat de gestion disponible / CA HT.

Le résultat est indicatif. Sont exclus faute de source : amortissements, charges financières, fiscalité et charges patronales.

## Interactions
- Période filtre le ou les mois choisis.
- Activité filtre réalisé, budget et rentabilité ; `Commun` regroupe les coûts non affectables à une activité métier.
- Cliquer une catégorie de charge cible l'analyse.
- Sélectionner une ligne source du compte de gestion puis utiliser **Voir les écritures source**.
- **Réinitialiser** efface les slicers de la page.
- Le survol des KPI affiche définition, réalisé, budget et période précédente.

Le détail transactionnel est disponible pour `Chiffre d'affaires`, `Achats directs`, `Personnel` et `Charges d'exploitation`. `Marge sur achats` et `Résultat de gestion` sont des synthèses calculées.

## Maintenance Excel
`BudgetMensuel` : Budget_ID, Mois, Activité, Ligne_P&L, Catégorie, Budget_XOF, Commentaire.
`ChargesExploitation` : Charge_ID, Date, Catégorie, Sous_Catégorie, Activité, Fournisseur, Référence, Montant_XOF, Nature, Commentaire.
Utiliser `Commun` pour les coûts non affectables proprement.

## Contrôles
1. CA total = somme des activités.
2. Résultat = CA - Achats - Personnel - Charges.
3. Le point final du waterfall correspond au résultat.
4. Les totaux P&L correspondent aux KPI.
5. Tester période, activité, catégorie, info-bulles et drill-through.
6. Conserver `culture: en-US` et `sourceQueryCulture: en-US` pour Fabric.

## Déploiement
1. Conserver le classeur SharePoint sous le nom consommé par le modèle.
2. Synchroniser Git vers Fabric avec **Update all**.
3. Actualiser le modèle sémantique.
4. Vérifier les six pages visibles et les interactions.

## Limites
- Les achats directs ne sont pas une valorisation comptable exhaustive des consommations.
- Le personnel n'inclut pas les charges patronales.
- Le résultat n'est pas un résultat comptable légal.
- Les budgets sont des données de démonstration maintenables manuellement dans Excel.

## Historique
- v0.1 : base du dashboard.
- v0.2 : navigation, comparaisons et BFR actionnable.
- v0.3 : performance financière, budget, charges, info-bulles et détail source.
