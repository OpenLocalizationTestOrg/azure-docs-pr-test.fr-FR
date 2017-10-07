---
title: "aaaAgent solution de contrôle d’intégrité dans OMS | Documents Microsoft"
description: "Cet article est prévue toohelp vous comprenez comment toouse toomonitor de cette solution hello d’intégrité de vos agents de création de rapports directement tooOMS ou System Center Operations Manager."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>Solution Agent Health pour OMS
solution de contrôle d’intégrité de l’Agent Hello dans OMS vous permet de comprendre, pour tous les agents hello reporting directement, espace de travail OMS toohello ou un tooOMS groupe connecté de la gestion de System Center Operations Manager, qui sont des données opérationnelles ne répond pas et de soumission.  Vous pouvez également effectuer le suivi de combien d’agents est déployés, où ils sont distribués géographiquement et effectuer d’autres requêtes toomaintain attiser la conscience de distribution hello des agents déployés dans Azure, autres environnements de cloud ou local.    

## <a name="prerequisites"></a>Composants requis
Avant de déployer cette solution, confirmer vous avez actuellement pris en charge [agents Windows](../log-analytics/log-analytics-windows-agents.md) toohello espace de travail OMS de création de rapports ou le rapport de tooan [groupe d’administration Operations Manager](../log-analytics/log-analytics-om-agents.md) intégré à votre Espace de travail OMS.    

## <a name="solution-components"></a>Composants de la solution
Cette solution se compose de hello suivant les ressources qui sont ajoutées tooyour espace de travail et des agents connectés directement ou groupe d’administration connecté Operations Manager.

### <a name="management-packs"></a>Packs d’administration
Si votre groupe d’administration System Center Operations Manager est un espace de travail OMS tooan connecté, hello suivant des packs d’administration est installé dans Operations Manager.  Ces packs d’administration sont également installés sur des ordinateurs Windows directement connectés après l’ajout de cette solution. Il n’y a rien tooconfigure ou gérer ces packs d’administration.

* Microsoft System Center Advisor HealthAssessment Direct Channel Intelligence Pack  (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Microsoft System Center Advisor HealthAssessment Server Channel Intelligence Pack (Microsoft.IntelligencePacks.HealthAssessmentViaServer).  

Pour plus d’informations sur la façon dont les packs d’administration de solution sont mises à jour, consultez [connecter Operations Manager tooLog Analytique](../log-analytics/log-analytics-om-agents.md).

## <a name="configuration"></a>Configuration
Ajouter tooyour de solution d’intégrité de l’Agent hello espace de travail OMS à l’aide du processus de hello décrit dans [ajouter des solutions](../log-analytics/log-analytics-add-solutions.md). Aucune configuration supplémentaire n’est requise.


## <a name="data-collection"></a>Collecte des données
### <a name="supported-agents"></a>Agents pris en charge
Hello tableau suivant décrit les sources de hello connecté sont pris en charge par cette solution.

| Source connectée | Pris en charge | Description |
| --- | --- | --- |
| Agents Windows | Oui | Les événements de pulsation sont rassemblés par des agents Windows directs.|
| Groupe d’administration Microsoft System Center Operations Manager | Oui | Événements de pulsation sont collectées auprès des agents reporting groupe d’administration toohello toutes les 60 secondes et ensuite transmis tooLog Analytique. Une connexion directe à partir d’Operations Manager agents tooLog Analytique n’est pas nécessaire. Données d’événement de pulsation sont transférées à partir de référentiel de hello gestion groupe toohello Analytique de journal.|

## <a name="using-hello-solution"></a>À l’aide de la solution de hello
Lorsque vous ajoutez d’espace de travail OMS hello solution tooyour, hello **intégrité de l’Agent** vignette sera ajoutée tooyour du tableau de bord OMS. Cette vignette indique nombre total de hello d’agents et nombre hello des agents qui ne répond pas Bonjour des dernières 24 heures.<br><br> ![Vignette de la solution Agent Health du tableau de bord](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Cliquez sur hello **intégrité de l’Agent** vignette tooopen hello **intégrité de l’Agent** tableau de bord.  tableau de bord Hello inclut des colonnes de hello Bonjour tableau suivant. Chaque colonne répertorie les événements de dix principaux de hello par nombre correspondant que les critères de la colonne pour hello spécifié de plage de temps. Vous pouvez exécuter une recherche de journal qui fournit l’intégralité de la liste hello en sélectionnant **afficher tous les** à hello droite en bas de chaque colonne, ou en cliquant sur en-tête de colonne hello.

| Colonne | Description |
|--------|-------------|
| Nombre d’agents au fil du temps | Tendance du nombre d’agents sur une période de sept jours (agents Linux et Windows).|
| Nombre d’agents inactifs | Une liste des agents qui n’ont pas envoyé de pulsation Bonjour dernières 24 heures.|
| Distribution selon le système d’exploitation | Partition du nombre d’agents Windows et Linux dont vous disposez dans votre environnement.|
| Distribution selon la version de l’agent | Une partition hello différent des versions d’agent installés dans votre environnement et le nombre de chacun d’eux.|
| Distribution selon la catégorie de l’agent | Une partition de hello différentes catégories d’agents envoient des événements de pulsation : agents directes, les agents Operations Manager ou hello serveur d’administration Operations Manager.|
| Distribution selon le groupe d’administration | Une partition hello différents SCOM des groupes d’administration dans votre environnement.|
| Géolocalisation des agents | Une partition de hello différents pays où vous avez des agents et un décompte du nombre de hello d’agents qui ont été installés dans chaque pays.|
| Nombre de passerelles installées | nombre de Hello des serveurs hello passerelle OMS installée et une liste de ces serveurs.|

![Exemple de tableau de bord pour la solution Agent Health](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Enregistrements Log Analytics
solution de Hello crée un type d’enregistrement dans le référentiel d’OMS hello.  

### <a name="heartbeat-records"></a>Enregistrements de pulsation
L’enregistrement d’un type de **pulsation** est créé.  Ces enregistrements ont des propriétés de hello Bonjour tableau suivant.  

| Propriété | Description |
| --- | --- |
| Type | *Pulsation*|
| Catégorie | La valeur correspond à *Agent Direct*, *Agent SCOM*, ou *Serveur d’administration SCOM*.|
| Ordinateur | Nom de l’ordinateur.|
| Système d’exploitation | Système d’exploitation : Windows ou Linux.|
| OSMajorVersion | Version principale du système d’exploitation.|
| OSMinorVersion | Version secondaire du système d’exploitation.|
| Version | Version de l’agent OMS ou de l’agent Operations Manager.|
| SCAgentChannel | La valeur correspond à *Direct* et/ou *SCManagementServer*.|
| IsGatewayInstalled | Si la passerelle OMS est installée, la valeur correspond à *true*. Dans le cas contraire, elle correspond à *false*.|
| ComputerIP | Adresse IP de l’ordinateur de hello.|
| RemoteIPCountry | Lieu où l’ordinateur est déployé.|
| ManagementGroupName | Nom du groupe d’administration Operations Manager.|
| SourceComputerId | ID unique de l’ordinateur.|
| RemoteIPLongitude | Longitude de l’emplacement géographique de l’ordinateur.|
| RemoteIPLatitude | Latitude de l’emplacement géographique de l’ordinateur.|

Chaque agent serveur d’administration Operations Manager tooan envoie des deux pulsations et la valeur de la propriété SCAgentChannel inclut les deux reporting **Direct** et **SCManagementServer** selon ce qui Sources de données Analytique de journal et les solutions que vous avez activées dans votre abonnement OMS. Si vous vous souvenez, à partir de solutions, les données sont envoyées directement à partir d’Operations Manager management server toohello OMS service web, ou en raison de hello volume de données collectées sur l’agent hello, sont envoyés directement à partir de service web de hello agent tooOMS. Pour les événements de pulsation qui ont la valeur de hello **SCManagementServer**, hello ComputerIP valeur est adresse hello hello du serveur d’administration dans la mesure où les données de salutation sont réellement téléchargées par celui-ci.  Des pulsations où SCAgentChannel est défini trop**Direct**, il est hello adresse IP publique de l’agent de hello.  

## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux
Hello tableau suivant fournit des exemples des recherches de journaux pour les enregistrements collectées par cette solution.

| Interroger | Description |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |Nombre total d’agents |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |Nombre d’agents qui ne répond pas Bonjour des dernières 24 heures |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |Nombre d’agents qui ne répond pas Bonjour des 15 dernières minutes |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Ordinateurs en ligne (hello des dernières 24 heures) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Total Agents hors connexion dans les 30 dernières minutes (hello des dernières 24 heures) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |Obtenir une tendance du nombre d’agents sur une période selon le système d’exploitation|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |Distribution selon le système d’exploitation |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |Distribution selon la version de l’agent |
| Type=Heartbeat&#124;measure count() by Category |Distribution selon la catégorie de l’agent |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | Distribution selon le groupe d’administration |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |Géolocalisation des agents |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |Nombre de passerelles OMS installées |


>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](../log-analytics/log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivant.
>
>| Interroger | Description |
|:---|:---|
| Heartbeat &#124; distinct Computer |Nombre total d’agents |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |Nombre d’agents qui ne répond pas Bonjour des dernières 24 heures |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |Nombre d’agents qui ne répond pas Bonjour des 15 dernières minutes |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Ordinateurs en ligne (hello des dernières 24 heures) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Total Agents hors connexion dans les 30 dernières minutes (hello des dernières 24 heures) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Obtenir une tendance du nombre d’agents sur une période selon le système d’exploitation|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Distribution selon le système d’exploitation |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |Distribution selon la version de l’agent |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |Distribution selon la catégorie de l’agent |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | Distribution selon le groupe d’administration |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |Géolocalisation des agents |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |Nombre de passerelles OMS installées |

## <a name="next-steps"></a>Étapes suivantes

* Consultez [Alertes dans Log Analytics](../log-analytics/log-analytics-alerts.md) pour obtenir des informations sur la génération d’alertes à partir de Log Analytics.
