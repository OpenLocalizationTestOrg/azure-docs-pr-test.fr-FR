---
title: aaaIT connecteur de gestion de Service dans OMS | Documents Microsoft
description: "Utiliser le moniteur de toocentrally hello connecteur de gestion du Service informatique et gérer des éléments de travail ITSM hello dans OMS et résoudre les problèmes rapidement."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>Gérer de manière centralisée les éléments de travail ITSM à l’aide d’IT Service Management Connector (version préliminaire)

![Symbole d’IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

Vous pouvez utiliser hello connecteur de gestion de Service informatique (ITSMC) dans le moniteur de toocentrally Analytique des journaux OMS et gérer des éléments de travail sur votre ITSM produits/services.

Connecteur de gestion du Service informatique de Hello intègre Analytique des journaux OMS vos produits de gestion de services informatiques (ITSM) existants et les services.  solution de Hello offre une intégration bidirectionnelle avec ITSM produits/services, où il fournit hello utilisateurs d’OMS un incident de toocreate option, les alertes ou les événements dans les solutions ITSM. connecteur de Hello importe également les données, tels que les incidents et les demandes de modification à partir de la solution ITSM dans Analytique de journal d’OMS.

IT Service Management Connector vous offre de nombreuses possibilités :

  - Surveiller et gérer de manière centralisée des éléments de travail pour les produits/services ITSM utilisés au sein de votre organisation.
  - Créer des éléments de travail ITSM (tels que des alertes, des événements et des incidents) dans ITSM à partir des alertes OMS et via la fonctionnalité de recherche dans les journaux.
  - Lire les incidents et les demandes de modification de votre solution ITSM et les mettre en corrélation avec les données de journal pertinentes dans l’espace de travail Log Analytics.
  - Retrouver des événements inattendus et inhabituels et résolvez-les avant même que les utilisateurs finaux de hello appeler et les signaler du support technique toohello.
  - Importer des données d’éléments de travail dans Log Analytics et créer des rapports d’indicateurs de performance clés.  Grâce à ces rapports, vous pouvez identifier, analyser et agir sur plusieurs éléments importants tels que l’évaluation des programmes malveillants.
  - Afficher des tableaux de bord spécialement conçus pour fournir des informations plus détaillées sur les incidents, les demandes de modification et les systèmes concernés.
  - Résoudre les problèmes plus rapidement en mettant en corrélation avec d’autres solutions de gestion dans l’espace de travail hello Analytique de journal.


## <a name="prerequisites"></a>Composants requis

éléments de travail ITSM tooimport hello dans Analytique des journaux OMS, solution de hello requiert une connexion entre hello connecteur de gestion du Service informatique Bonjour OMS et hello informatique SM produits et services à partir duquel vous importez des éléments de travail hello.


## <a name="configuration"></a>Configuration

Ajouter hello espace de travail du connecteur de gestion du Service informatique solution tooyour OMS, à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).

Connecteur de gestion du Service informatique vignette que vous voyez dans la galerie des Solutions hello :

![vignette du connecteur](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Après avoir été ajoutée avec succès, vous verrez hello connecteur de gestion de Service informatique sous **OMS** > **paramètres** > **Sources connectées.**

![ITSMC connecté](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Par défaut, hello connecteur de gestion du Service informatique actualise les données de la connexion hello qu’une seule fois dans toutes les 24 heures. toorefresh données de votre connexion instantanément pour les modifications ou d’un modèle de mises à jour que vous apportez, cliquez sur la connexion suivante tooyour hello actualisation bouton affiché.

 ![Actualisation d’ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Packs d’administration
Cette solution ne requiert aucun pack d’administration.

## <a name="connected-sources"></a>Sources connectées

Hello ITSM produits/services suivants sont pris en charge par hello connecteur de gestion du Service informatique :

- [System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>À l’aide de la solution de hello

Lorsque vous connectez hello connecteur de gestion du Service OMS informatique avec votre service ITSM, services d’Analytique de journal hello démarre collecte des données de hello de hello connecté ITSM produits/service.

> [!NOTE]
> - Les données importées par la solution IT Service Management Connector s’affichent dans Log Analytics en tant qu’événements nommés **ServiceDesk_CL**.
- Chaque événement contient un champ nommé **ServiceDeskWorkItemType_s** qui peut prendre sa valeur comme un incident, ou la demande de modification, selon hello d’élément de travail données contenues dans hello **ServiceDesk_CL** événement.

## <a name="input-data"></a>Données d’entrée
Éléments de travail importés à partir de hello ITSM produits/services.

Hello informations suivantes montre des exemples de données collectées par le connecteur de gestion des services informatiques hello :

> [!NOTE]
> En fonction de hello type élément de travail importé dans le journal Analytique, **ServiceDesk_CL** contient hello champs qui suivent :

**Élément de travail :****Incidents**  
ServiceDeskWorkItemType_s="Incident"

**Champs**

- ServiceDeskConnectionName
- ID du service d’assistance
- State
- Urgence
- Impact
- Priorité
- Escalade
- Créé par
- Résolu par
- Fermé par
- Source
- Affecté à
- Catégorie
- Intitulé
- Description
- Date de création
- Date de fermeture
- Date de résolution
- Date de dernière modification
- Ordinateur


**Élément de travail :****Demandes de modification**

ServiceDeskWorkItemType_s="ChangeRequest"

**Champs**
- ServiceDeskConnectionName
- ID du service d’assistance
- Créé par
- Fermé par
- Source
- Affecté à
- Intitulé
- Type
- Catégorie
- State
- Escalade
- État conflictuel
- Urgence
- Priorité
- Risque
- Impact
- Affecté à
- Date de création
- Date de fermeture
- Date de dernière modification
- Date de la demande
- Date de début prévue
- Date de fin prévue
- Date de début du travail
- Date de fin du travail
- Description
- Ordinateur

## <a name="output-data-for-a-servicenow-incident"></a>Données de sortie pour un incident ServiceNow

| Champ OMS | Champ ITSM |
|:--- |:--- |
| ServiceDeskId_s| Number |
| IncidentState_s | State |
| Urgency_s |Urgence |
| Impact_s |Impact|
| Priority_s | Priorité |
| CreatedBy_s | Ouvert par |
| ResolvedBy_s | Résolu par|
| ClosedBy_s  | Fermé par |
| Source_s| Type de contact |
| AssignedTo_s | Trop d’assigné |
| Category_s | Catégorie |
| Title_s|  Brève description |
| Description_s|  Remarques |
| CreatedDate_t|  Ouvert |
| ClosedDate_t| Fermé|
| ResolvedDate_t|Résolu|
| Ordinateur  | Élément de configuration |

## <a name="output-data-for-a-servicenow-change-request"></a>Données de sortie pour une demande de modification ServiceNow

| Champ OMS | Champ ITSM |
|:--- |:--- |
| ServiceDeskId_s| Number |
| CreatedBy_s | Demandé par |
| ClosedBy_s | Fermé par |
| AssignedTo_s | Trop d’assigné |
| Title_s|  Brève description |
| Type_s|  Type |
| Category_s|  Catégorie |
| CRState_s|  State|
| Urgency_s|  Urgence |
| Priority_s| Priorité|
| Risk_s| Risque|
| Impact_s| Impact|
| RequestedDate_t  | Date demandée |
| ClosedDate_t | Date de fermeture |
| PlannedStartDate_t  |     Date de début prévue |
| PlannedEndDate_t  |   Date de fin prévue |
| WorkStartDate_t  | Date de début réelle |
| WorkEndDate_t | Date de fin réelle|
| Description_s | Description |
| Ordinateur  | Élément de configuration |

**Exemple d’écran Log Analytics pour les données ITSM :**

![Écran Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>IT Service Management Connector – intégration avec d’autres solutions OMS

Connecteur de gestion du Service informatique, prend actuellement en charge l’intégration avec hello solutions de carte de Service.

Carte de service découvre automatiquement les hello des composants de l’application sur Windows et les mappages et les systèmes Linux hello la communication entre les services. Il vous permet de tooview vos serveurs en tant que vous les – considérer comme des réseaux interconnectés qui fournissent des services critiques. Carte de service affiche les connexions entre les serveurs, les processus et les ports sur n’importe quelle architecture connectée à TCP, sans configuration requise autre que l’installation d’un agent. Pour en savoir plus : [Carte de service](../operations-management-suite/operations-management-suite-service-map.md).

Avec cette intégration, vous pouvez afficher les éléments de support de service hello créés dans les solutions ITSM hello comme indiqué dans hello l’exemple suivant :

![Solution intégrée ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>Créer des éléments de travail ITSM pour des alertes OMS

Pour les alertes d’OMS hello, vous pouvez créer des éléments de travail associés dans les sources de ITSM hello connecté.  toodo, hello utilisez procédure :

1. À partir de **recherche de journal** fenêtre, exécutez une données tooview journal des requêtes. Résultats de la requête sont source de hello pour les éléments de travail.
2. Dans **recherche de journal**, cliquez sur **alerte** tooopen hello **ajouter une règle d’alerte** page.

    ![Écran Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. Sur hello **ajouter une règle d’alerte** fenêtre, fournissent des détails hello requis pour **nom**, **gravité**, **recherche**, et  **Critères d’alerte** (mesure fenêtre/métrique de temps).
4. Sélectionnez **Oui** pour **Actions ITSM**.
5. Sélectionnez votre connexion ITSM hello **sélectionner une connexion** liste.
6. Fournir des détails hello en fonction des besoins.
7. toocreate un élément de travail distinct pour chaque entrée de journal de hello de cette alerte, sélectionnez **créer des éléments de travail pour chaque entrée de journal** case à cocher.

    Ou

    Laissez cet case à cocher toocreate non sélectionnées uniquement un élément de travail pour n’importe quel nombre d’entrées de journal sous cette alerte.

7. Cliquez sur **Enregistrer**.

alerte d’OMS Hello est créé sous **alertes**. Bonjour le travail de la connexion correspondante ITSM éléments sont créés lorsque condition l’alerte spécifiée hello est remplie.

## <a name="create-itsm-work-items-from-oms-logs"></a>Créer des éléments de travail ITSM à partir de journaux OMS

Vous pouvez créer des éléments de travail dans les sources de ITSM hello connecté à l’aide de recherche de journal d’OMS. toodo, hello utilisez procédure :

1. À partir de **recherche de journal**, rechercher les données de salutation requis, sélectionnez les détails de hello, puis cliquez sur **élément de travail de création**.

    Hello **élément de travail de ITSM créer** fenêtre s’affiche :

    ![Écran Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Ajoutez hello les détails suivants :

  - **Titre de l’élément de travail**: titre de l’élément de travail hello.
  - **Description de l’élément de travail**: Description pour le nouvel élément de travail hello.
  - **Impact sur ordinateur**: nom de l’ordinateur hello où les données de journal a été trouvées.
  - **Sélectionnez la connexion**: connexion ITSM dans lequel vous souhaitez toocreate cet élément de travail.
  - **Élément de travail** : type d’élément de travail.

3. toouse un modèle d’élément de travail existant d’un incident, cliquez sur **Oui** sous **élément de travail de génération basé sur le modèle de hello** option, puis cliquez sur **créer**.

    Ou,

    Cliquez sur **non** si vous souhaitez tooprovide vos valeurs personnalisées.

4. Entrez les valeurs appropriées hello Bonjour **Type de Contact**, **Impact**, **urgence**, **catégorie**, et **sous-catégorie**  zones de texte, puis cliquez sur **créer**.

élément de travail Hello sera créé dans hello ITSM, que vous pouvez également afficher dans OMS.

## <a name="troubleshoot-itsm-connections-in-oms"></a>Dépanner des connexions ITSM dans OMS
1.  Si connexion échoue à partir de l’interface utilisateur de la source connecté et que vous obtenez hello **erreur lors de l’enregistrement de connexion** message, procédez comme hello suivant :
 - En cas de connexions de ServiceNow, Cherwell et Provance, vérifiez que vous entré correctement hello client et le nom d’utilisateur/mot de passe ID/question secrète du client pour chacune des connexions de hello. Si hello erreur persiste, vérifiez si vous disposez de privilèges suffisants dans hello correspondant ITSM produit toomake hello de connexion.
 - En cas de Service Manager, vérifiez que hello Web application est déployée avec succès et que la connexion hybride est créée. tooverify hello connexion est correctement établie avec ordinateur de Service Manager local hello, visitez les URL de l’application hello Web comme indiqué dans la documentation hello de fabrication hello [connexion hybride](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  Si les données issues de ServiceNow ne sont pas mise en route synchronisées dans OMS, assurez-vous qu’une instance ServiceNow hello n’est pas en sommeil. Cela peut être plus tard dans hello instances ServiceNow Dev, lorsqu’il est inactif. Else, signaler un problème technique hello.
3.  Si les alertes sont mise en route déclenchés à partir d’OMS, mais ne sont pas des éléments de travail créé dans ITSM produits ou de configuration ne pas obtenir les éléments toowork de créé/lié ou pour des informations générales, hello suivant :
 -  Solution de connecteur de gestion des services informatiques dans le portail OMS peut être utilisé tooget un récapitulatif des connexions/le travail des éléments/ordinateurs, etc.. Cliquez sur le message d’erreur hello dans le panneau d’état hello, accédez trop**recherche de journal** et afficher hello connexion qui possède l’erreur de hello dans le message d’erreur hello à l’aide des détails de hello.
 - Vous pouvez afficher directement les hello erreurs/informations Bonjour **recherche de journal** à l’aide de la page *Type = ServiceDeskLog_CL*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Résoudre les problèmes de déploiement de l’application web Service Manager
1.  En cas de tout problème avec le déploiement de l’application web, assurez-vous d’avoir des autorisations suffisantes dans l’abonnement de hello mentionné toocreate/déployer des ressources.
2.  Si **tooinstance d’un objet exclut la référence d’objet** message d’erreur apparaît lors de l’exécution hello [script](log-analytics-itsmc-service-manager-script.md) vous assurer que vous avez entré des valeurs valides sous **Configuration de l’utilisateur**section.
3.  Si vous ne parvenez pas d’espace de noms relais toocreate service bus, vérifiez que hello requis de fournisseur de ressources est inscrit dans l’abonnement de hello. Si ne pas inscrit, le créer manuellement à partir de hello portail Azure. Vous pouvez également créer tandis que [création de la connexion hybride hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) de hello portail Azure.


## <a name="contact-us"></a>Nous contacter

Pour toutes les requêtes ou des commentaires sur le connecteur de gestion du Service informatique de hello, contactez-nous à l’adresse [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Étapes suivantes
[Ajouter tooIT de produits/services ITSM connecteur de Service Management](log-analytics-itsmc-connections.md).
