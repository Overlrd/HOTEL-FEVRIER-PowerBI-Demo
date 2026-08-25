# Guide support — Dashboard Hôtel 2 Février

**Version : 0.4 — Nettoyage démo & interactions**

Le dashboard comporte six pages visibles : Tableau de bord DAF, Trésorerie et BFR, Exploitation hôtelière, Ressources humaines, Achats et stocks, Performance financière.

## Vue d'ensemble DAF
La page d'accueil suit une structure exécutive :
- 6 KPI : chiffre d'affaires HT, trésorerie disponible, créances échues, résultat de gestion, taux d'occupation et RevPAR ;
- tendance mensuelle du CA réalisé vs budget ;
- répartition du CA par activité ;
- tableau **Points à suivre** avec valeur, comparaison et signal ;
- filtre de période et bouton **Réinitialiser**.

## Interactions de démonstration
- Les graphiques filtrent les autres visuels lorsque le contexte est compatible.
- Le survol des KPI principaux affiche une info-bulle contextuelle.
- **Réinitialiser** efface les slicers de la page.
- Les pages d'analyse proposent un accès au détail après sélection d'un élément :
  - DAF : activité → commandes sources ;
  - Trésorerie : facture en retard → fiche de recouvrement ;
  - Exploitation : type de chambre → détail journalier ;
  - RH : département → employés et paie ;
  - Achats & stocks : catégorie → mouvements de stock ;
  - Performance financière : ligne P&L → écritures sources.
- Chaque page de détail dispose d'un bouton de retour explicite.

## Performance financière
- Chiffre d'affaires HT : ventes terminées, montant HT.
- Achats directs HT : achats terminés affectés aux activités selon la catégorie.
- Marge sur achats : CA HT − achats directs HT.
- Coût personnel disponible : salaire de base + primes.
- Charges d'exploitation : table Excel `ChargesExploitation`.
- Résultat de gestion disponible : CA HT − achats directs HT − personnel disponible − charges d'exploitation.

Le résultat reste indicatif : amortissements, charges financières, fiscalité et charges patronales ne sont pas disponibles dans la source de démonstration.

## Maintenance Excel
`BudgetMensuel` : Budget_ID, Mois, Activité, Ligne_P&L, Catégorie, Budget_XOF, Commentaire.
`ChargesExploitation` : Charge_ID, Date, Catégorie, Sous_Catégorie, Activité, Fournisseur, Référence, Montant_XOF, Nature, Commentaire.
Utiliser `Commun` pour les coûts non affectables proprement.

## Contrôles avant démo
1. Dans Fabric, lancer **Update all** puis actualiser le modèle sémantique.
2. Vérifier les six pages visibles et leur navigation latérale.
3. Tester les boutons **Réinitialiser**.
4. Survoler les KPI et vérifier les info-bulles.
5. Tester chaque drill-through puis son bouton de retour.
6. Cliquer les catégories/barres principales et vérifier le cross-filtering.
7. Vérifier : CA total = somme des activités ; résultat = CA − achats − personnel − charges.
8. Conserver `culture: en-US` et `sourceQueryCulture: en-US` pour Fabric.

## Limites
- Les achats directs ne constituent pas une valorisation comptable exhaustive des consommations.
- Le personnel n'inclut pas les charges patronales.
- Le résultat n'est pas un résultat comptable légal.
- Les budgets sont des données de démonstration maintenables manuellement dans Excel.

## Historique
- v0.1 : base du dashboard.
- v0.2 : navigation, comparaisons et BFR actionnable.
- v0.3 : performance financière, budget, charges, info-bulles et détail source.
- v0.4 : page DAF restructurée pour la démo, branding homogène, reset, info-bulles et drill-through contextuels.
