# Guide support — Dashboard Hôtel 2 Février

**Version : 0.5 — Correctif Fabric & libellés simplifiés**

Le dashboard comporte six pages visibles :
- Vue d'ensemble
- Trésorerie
- Exploitation
- Ressources humaines
- Achats et stocks
- Performance financière

## Vue d'ensemble
La page d'accueil présente 6 indicateurs : chiffre d'affaires HT, trésorerie disponible, créances échues, résultat de gestion, taux d'occupation et revenu par chambre disponible.

Elle contient aussi :
- évolution mensuelle du chiffre d'affaires réalisé vs budget ;
- répartition du chiffre d'affaires par activité ;
- tableau **Points à suivre** ;
- filtre de période et bouton **Réinitialiser**.

## Interactions
- Les graphiques filtrent les autres visuels lorsque le contexte est compatible.
- Le survol des principaux indicateurs affiche une info-bulle contextuelle.
- Les pages d'analyse proposent un accès au détail après sélection d'un élément.
- Chaque page de détail dispose d'un bouton de retour.
- **Réinitialiser** efface les filtres de la page.

## Détails disponibles
- Vue d'ensemble : activité → commandes sources.
- Trésorerie : facture en retard → fiche de recouvrement.
- Exploitation : type de chambre → détail journalier.
- Ressources humaines : département → employés et paie.
- Achats et stocks : catégorie → mouvements de stock.
- Performance financière : ligne du compte de gestion → écritures sources.

## Performance financière
- Chiffre d'affaires HT : ventes terminées.
- Achats directs HT : achats terminés affectés aux activités.
- Marge sur achats : chiffre d'affaires HT − achats directs HT.
- Coût personnel disponible : salaire de base + primes.
- Charges d'exploitation : table Excel `ChargesExploitation`.
- Résultat de gestion disponible : chiffre d'affaires HT − achats directs HT − personnel − charges d'exploitation.

Le résultat reste indicatif : amortissements, charges financières, fiscalité et charges patronales ne sont pas disponibles dans la source de démonstration.

## Maintenance Excel
`BudgetMensuel` et `ChargesExploitation` restent modifiables manuellement pour la démonstration.
Utiliser `Commun` pour les coûts non affectables proprement.

## Contrôles avant démo
1. Dans Fabric, lancer **Update all** puis actualiser le modèle sémantique.
2. Vérifier les six pages visibles et leur navigation.
3. Tester les boutons **Réinitialiser**.
4. Survoler les indicateurs et vérifier les info-bulles.
5. Tester chaque accès au détail puis son bouton de retour.
6. Cliquer les catégories/barres principales et vérifier le filtrage croisé.
7. Vérifier : chiffre d'affaires total = somme des activités ; résultat = chiffre d'affaires − achats − personnel − charges.
8. Conserver `culture: en-US` et `sourceQueryCulture: en-US` pour Fabric.

## Historique
- v0.1 : base du dashboard.
- v0.2 : navigation, comparaisons et suivi de trésorerie.
- v0.3 : performance financière, budget, charges, info-bulles et détail source.
- v0.4 : page d'accueil restructurée, branding homogène, filtres et détails contextuels.
- v0.5 : correction JSON des boutons de retour et simplification des libellés.
