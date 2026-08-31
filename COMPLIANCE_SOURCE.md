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

Relations principales : obligation → suivi → rapprochement ; date → suivi ; salarié → contrôle salarié ; document → rapprochement. Le lien de rapprochement vers les mouvements de trésorerie est volontairement **inactif** : cela évite deux chemins de filtre actifs vers la table de dates. Il reste disponible pour des mesures explicites avec `USERELATIONSHIP` si un besoin de rapprochement détaillé apparaît.

## Statuts et indicateurs

`Statut opérationnel` transforme le statut de saisie et les éléments du dossier en une lecture exploitable. Une ligne `Clôturé` devient `À jour` ou `Fait hors délai`. Une ligne ouverte est classée selon l'échéance, le paiement et le rapprochement : `En retard`, `Paiement en attente`, `Écart à justifier`, `Urgent`, `À faire bientôt` ou `À préparer`. Une applicabilité ou une date non confirmée reste `À confirmer`.

Les indicateurs principaux couvrent : dossiers à jour, actions immédiates, échéances sous 30 jours, dossiers à confirmer, montant restant à payer, justificatifs disponibles ou à compléter, écart comptable et situations CNSS à régulariser.

Le taux de conformité compare les dossiers `À jour` ou `Fait hors délai` aux dossiers qui nécessitent une action immédiate. Les dossiers futurs ou encore à confirmer restent visibles séparément et ne déforment pas ce ratio.

## Expérience du rapport

La page **Fiscalité & conformité** est volontairement distincte du thème analytique des autres pages. Elle se présente comme un dossier administratif sur fond papier, sans graphique de gestion :

- un résumé rédigé et cinq repères de situation ;
- un registre priorisé des obligations ;
- un panneau de pièces justificatives ;
- une synthèse CNSS sans liste nominative ;
- deux filtres seulement, période et situation.

Le clic droit sur une ligne du registre ouvre **Dossier d’obligation**, qui rassemble déclaration, paiement, cadre officiel, pièces et références comptables. Le bouton **Voir les situations salariés** ouvre la page CNSS détaillée ; cette page est masquée des onglets ordinaires et toutes les identités y sont signalées comme fictives.

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
5. Tester la navigation vers **Fiscalité & conformité**, les deux filtres, les URL et le drillthrough **Dossier d’obligation**.
6. Ouvrir la page **Détail des situations CNSS** depuis son bouton, vérifier les filtres département/statut et revenir au dossier principal.
7. Confirmer visuellement les couleurs, libellés, tableaux et mentions de démonstration avant publication.
