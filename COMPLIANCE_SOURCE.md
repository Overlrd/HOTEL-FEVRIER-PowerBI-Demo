# Source fiscalité et conformité — Hôtel 2 Février

## Périmètre

La page **Fiscalité & conformité** est un dispositif de pilotage de démonstration. Elle centralise des obligations fiscales, sociales, comptables et sectorielles afin de suivre les échéances, paiements, rapprochements et pièces justificatives.

Les données, montants, statuts, identifiants de salariés et documents sont fictifs. Le dispositif ne constitue pas un avis juridique, fiscal ou social et ne prouve pas la conformité de l'hôtel.

## Source SharePoint

- Classeur : `HOTEL2FEVRIER/POWERBI-DEMO/Hotel_2_Fevrier_Donnees_Demo_PowerBI.xlsx`
- Preuves fictives : `HOTEL2FEVRIER/POWERBI-DEMO/DOCUMENTS-DEMO/Conformite/`
- Sauvegarde avant ajout : `Hotel_2_Fevrier_Donnees_Demo_PowerBI_backup_2026-08-31_pre-conformite.xlsx`

Ne pas renommer le classeur sans mettre à jour les partitions Power Query du modèle.

## Tables Excel et modèle

| Table Excel / modèle | Grain | Usage principal |
|---|---|---|
| `ComplianceObligationTable` | Une obligation de référence | Domaine, organisme, périodicité, applicabilité, criticité, règle de délai, source officielle |
| `ComplianceTrackingTable` | Une obligation pour une période | Échéance, déclaration, paiement, montants, responsable et statut |
| `ComplianceReconciliationTable` | Un rapprochement ou une preuve | Source comptable, mouvement, document, montants, écart et URL de preuve |
| `EmployeeComplianceTable` | Un contrôle par salarié | Immatriculation, base CNSS, cotisations et anomalie |

Relations principales : obligation → suivi → rapprochement ; date → suivi ; salarié → contrôle salarié ; mouvement de trésorerie et document → rapprochement.

## Statuts et indicateurs

`Statut opérationnel` reprend d'abord `Statut_Saisi`. Si celui-ci est vide, le modèle classe l'échéance selon `Date_Référence` et `Date_Échéance` : `En retard`, `Urgent`, `À venir`, `À préparer` ou `À valider`.

Les indicateurs couvrent : taux de conformité, échéances à traiter, échéances sous 30 jours, montant restant à payer, justificatifs manquants, écart comptable et salariés à régulariser.

Le taux de conformité exclut de sa base les statuts `À préparer`, `Non applicable` et `À valider`. Une ligne `Conforme hors délai` est comptée comme traitée, mais reste identifiable dans le détail.

## Gouvernance attendue

- `Responsable_Client` reste `À confirmer` tant qu'un propriétaire opérationnel n'est pas formellement désigné.
- `Applicabilité` doit être confirmée pour l'entité et la période concernées.
- `Source_URL`, `Source_Version` et `Dernière_Vérification` permettent de tracer la base documentaire officielle ; elles doivent être révisées périodiquement.
- Les PDF de démonstration portent la mention `DOCUMENT FICTIF - AUCUNE VALEUR ADMINISTRATIVE OU FISCALE`.
- Les montants et preuves doivent être rapprochés avec la comptabilité et les portails officiels avant toute décision.

## Actualisation et recette

1. Mettre à jour les tables Excel sans changer leurs noms ni leurs en-têtes.
2. Vérifier la feuille `Controles` du classeur.
3. Dans Power BI Desktop ou Fabric, lancer `Update all` puis actualiser le modèle sémantique.
4. Contrôler les relations, les mesures et l'absence d'erreur de chargement.
5. Tester la navigation vers **Fiscalité & conformité**, les filtres, les URL et le drillthrough **Détail conformité**.
6. Confirmer visuellement les couleurs, libellés, tableaux et mentions de démonstration avant publication.
