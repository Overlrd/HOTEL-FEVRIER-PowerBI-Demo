# Guide support — Dashboard Hôtel 2 Février

**Version : 0.8 — Dossier fiscalité et conformité**

Le dashboard comporte huit pages visibles :
- Vue d'ensemble
- Trésorerie
- Exploitation
- Ressources humaines
- Achats et stocks
- Performance financière
- Documents
- Fiscalité & conformité

## Vue d'ensemble

La page d'accueil présente 6 indicateurs : chiffre d'affaires HT, trésorerie disponible, créances échues, résultat de gestion, taux d'occupation et revenu par chambre disponible.

Elle contient aussi l'évolution mensuelle du chiffre d'affaires réalisé vs budget, la répartition par activité, les points à suivre, un filtre de période et le bouton **Réinitialiser**.

## Interactions et détails

- Les graphiques filtrent les autres visuels lorsque le contexte est compatible.
- Le survol des principaux indicateurs affiche une info-bulle contextuelle.
- Les pages d'analyse proposent un accès au détail après sélection d'un élément.
- Chaque page de détail dispose d'un bouton de retour.
- **Réinitialiser** efface les filtres de la page.

Détails disponibles : activité → commandes sources ; facture en retard → fiche de recouvrement ; type de chambre → détail journalier ; département → employés et paie ; catégorie → mouvements de stock ; ligne du compte de gestion → écritures sources ; suivi conformité → dossier d'obligation ; synthèse CNSS → registre administratif salarié.

## Performance financière

- Chiffre d'affaires HT : ventes terminées.
- Achats directs HT : achats terminés affectés aux activités.
- Marge sur achats : chiffre d'affaires HT − achats directs HT.
- Coût personnel disponible : salaire de base + primes.
- Charges d'exploitation : table Excel `ChargesExploitation`.
- Résultat de gestion disponible : chiffre d'affaires HT − achats directs HT − personnel − charges d'exploitation.

Le résultat reste indicatif : amortissements, charges financières, fiscalité et charges patronales ne sont pas disponibles dans la source de démonstration.

## Fiscalité & conformité

La page rassemble les obligations OTR, CNSS et sectorielles sous la forme d'un dossier administratif. Elle donne d'abord une lecture simple : situation générale, actions immédiates, échéances à préparer, dossiers à confirmer, pièces manquantes et reste à payer.

Les filtres portent uniquement sur la période et la situation. Le registre est trié par action requise et échéance. Un clic droit sur une ligne permet d'ouvrir **Dossier d'obligation**, avec les dates, montants, sources, justificatifs et références comptables de la ligne. La synthèse CNSS ne montre aucun nom ; le bouton **Voir les situations salariés** ouvre une page séparée filtrable par département et statut.

Cette page constitue une exception visuelle assumée : fond papier, encre sombre et statuts vert sauge, ambre, rouge atténué ou bleu-gris. Elle n'utilise ni le grand menu latéral bleu ni les graphiques des pages analytiques.

Toutes les données sont fictives. Les responsables, règles d'applicabilité et sources officielles doivent être revalidés avant tout usage réel. Voir `COMPLIANCE_SOURCE.md`.

## Source documentaire

Le classeur Excel SharePoint contient une table structurée `Documents` avec 24 pièces de démonstration.

Les fichiers sont stockés sous `HOTEL2FEVRIER/POWERBI-DEMO/DOCUMENTS-DEMO/` dans quatre dossiers : `Factures`, `Commandes`, `Justificatifs` et `Conformite`.

Le registre lie chaque pièce aux références existantes. La colonne `Document_URL` contient l'URL SharePoint du fichier. Le modèle expose `DocumentTable` et les liens sont utilisés par les pages Documents et Fiscalité & conformité. Voir `DOCUMENTS_SOURCE.md`.

## Maintenance Excel

`BudgetMensuel`, `ChargesExploitation`, `Documents` et les quatre tables de conformité restent modifiables manuellement pour la démonstration. Utiliser `Commun` pour les coûts non affectables proprement. Ne pas renommer les tables ni leurs en-têtes.

## Contrôles avant démo

1. Dans Fabric, lancer **Update all** puis actualiser le modèle sémantique.
2. Vérifier les huit pages visibles et leur navigation.
3. Tester les boutons **Réinitialiser**.
4. Survoler les indicateurs et vérifier les info-bulles.
5. Tester chaque accès au détail puis son bouton de retour.
6. Cliquer les catégories/barres principales et vérifier le filtrage croisé.
7. Vérifier : chiffre d'affaires total = somme des activités ; résultat = chiffre d'affaires − achats − personnel − charges.
8. Conserver `culture: en-US` et `sourceQueryCulture: en-US` pour Fabric.
9. Sur Fiscalité & conformité, tester les deux filtres, les URL officielles, les preuves et le drillthrough par `Suivi_ID`.
10. Ouvrir le détail CNSS, tester ses deux filtres et le bouton de retour.
11. Confirmer que chaque écran et chaque PDF de conformité reste clairement identifié comme fictif.

## Historique

- v0.1 : base du dashboard.
- v0.2 : navigation, comparaisons et suivi de trésorerie.
- v0.3 : performance financière, budget, charges, info-bulles et détail source.
- v0.4 : page d'accueil restructurée, branding homogène, filtres et détails contextuels.
- v0.5 : correction JSON des boutons de retour et simplification des libellés.
- v0.6 : ajout du registre documentaire Excel et du stockage SharePoint de démonstration.
- v0.7 : ajout des sources, du modèle, des pages et de la navigation Fiscalité & conformité.
- v0.8 : correction des statuts, suppression des visuels en erreur et refonte en dossier administratif avec détails obligation et CNSS séparés.
