---
title: solutions de gestion Azure journal Analytique aaaAdd | Documents Microsoft
description: "Les solutions de gestion Operations Management Suite (OMS)/Log Analytics représentent une collection de règles logiques, de visualisation et d’acquisition des données qui fournissent des mesures cernant un domaine problématique en particulier."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Ajouter l’espace de travail Analytique des journaux Azure management solutions tooyour

Les solutions de gestion Log Analytics représentent une collection de **règles logiques**, de **visualisation** et **d’acquisition des données** qui fournissent des mesures cernant un domaine problématique en particulier. Cet article répertorie les solutions de gestion prises en charge par le journal Analytique et vous montre comment tooadd et suppression d’un espace de travail à l’aide de hello portail Azure. Vous pouvez également ajouter des solutions dans le portail OMS est hello à l’aide de la galerie des Solutions hello.

Les solutions de gestion vous offrent des informations plus approfondies pour :

* étudier et résoudre plus rapidement les problèmes opérationnels ;
* collecter et corréler différents types de données machine ;
* Vous aident à qu'être proactif avec des activités qui expose des solutions de hello.

> [!NOTE]
> Analytique de journal inclut la fonctionnalité de recherche de journal, vous n’avez pas besoin de tooinstall un tooenable de solution de gestion il. Toutefois, vous obtenez des visualisations de données, des recherches suggérées et des idées en ajoutant l’espace de travail de gestion des solutions tooyour.

À l’aide de cet article, vous ajoutez d’espace de travail de gestion des solutions tooa à l’aide du portail Azure Marketplace de hello. Une fois que vous avez ajouté une solution, les données sont collectées à partir de serveurs hello dans votre infrastructure et envoyées service OMS de toohello. Traitement par le service OMS prend généralement quelques heures de tooan minutes de hello. Une fois que le service de hello traite les données de salutation, vous pouvez l’afficher dans OMS.

Vous pouvez facilement supprimer une solution de gestion quand vous n’en avez plus besoin. Lorsque vous supprimez une solution de gestion, ses données ne sont pas envoyées tooOMS. Si vous êtes sur le niveau de tarification gratuit de hello, suppression d’une solution peut réduire hello de données utilisée, ce qui vous permet de dépasser le quota quotidien de données.

## <a name="view-available-management-solutions"></a>Afficher les solutions de gestion disponibles

Azure marketplace Hello contient la liste des hello [solutions de gestion pour l’Analytique des journaux](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Vous pouvez installer des solutions de gestion à partir d’Azure marketplace en cliquant sur hello **maintenant** lien en bas de hello de chaque solution.

## <a name="add-a-management-solution"></a>Ajout d’une solution de gestion
1. Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com) à l’aide de votre abonnement Azure.
2. Bonjour **nouveau** panneau sous **Marketplace**, sélectionnez **analyse + gestion**.
3. Bonjour **analyse + gestion** panneau, cliquez sur **afficher tous les**.  
    ![Panneau Surveillance + gestion](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. toohello à droite de **Solutions de gestion**, cliquez sur **plus**.
5. Bonjour **Solutions de gestion** panneau, sélectionnez une solution de gestion que vous souhaitez tooadd tooa espace de travail.  
    ![Panneau Surveillance + gestion](./media/log-analytics-add-solutions/management-solutions.png)  
6. Dans le panneau de solution de gestion hello, passez en revue les informations sur la solution de gestion hello, puis cliquez sur **créer**.
7. Bonjour *nom de la solution gestion* panneau, sélectionnez un espace de travail que vous souhaitez tooassociate avec la solution de gestion hello.
8. Éventuellement, modifiez les paramètres de l’espace de travail pour hello abonnement Azure, groupe de ressources et l’emplacement. Vous pouvez également choisir les **options d’automatisation**. Cliquez sur **Créer**.  
    ![espace de travail de la solution](./media/log-analytics-add-solutions/solution-workspace.png)  
9. toostart à l’aide de la solution de gestion hello que vous avez ajouté tooyour, espace de travail, accédez trop**Analytique de journal** > **abonnements** > ***nom de l’espace de travail ***  >  **Vue d’ensemble**. Une nouvelle vignette pour votre solution de gestion s’affiche. Cliquez sur tooopen de vignette hello et recommencez à l’aide de la solution de hello après avoir recueilli les données pour la solution de hello.

## <a name="remove-a-management-solution"></a>Suppression d’une solution de gestion

1. Bonjour [portail Azure](https://portal.azure.com), accédez trop**Analytique de journal** > **abonnements** > ***nom de l’espace de travail*** puis, dans hello ***nom de l’espace de travail*** panneau, cliquez sur **Solutions**.
2. Dans liste hello de solutions de gestion, sélectionnez solution hello que vous souhaitez tooremove.
3. Dans le panneau de solution hello pour votre espace de travail, cliquez sur **supprimer**.  
    ![supprimer la solution](./media/log-analytics-add-solutions/solution-delete.png)  
4. Dans la boîte de dialogue hello confirmation, cliquez sur **Oui**.

## <a name="offers-and-pricing-tiers"></a>Offres et niveaux tarifaires

Hello tableau suivant identifie les solutions de gestion appartiennent offre d’Operations Management Suite tooeach.
Hello identifie également hello sont disponibles pour chaque solution de gestion des niveaux de tarification.
Toutes les solutions Bonjour tableau suivant sont disponibles dans hello Azure galerie des solutions portail et hello dans le portail d’Analytique de journal hello.

| Solution de gestion                                                                       | Offre                                                                     | Niveaux tarifaires<sup>1</sup>                                                 | Remarques |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Activity Log Analytics](log-analytics-activity.md)                                                                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | 90 jours de données disponibles gratuitement<br>Extrémité de niveau gratuit toohello pas soumettent de données |
| [Évaluation d'AD](log-analytics-ad-assessment.md)                                           | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [AD Replication Status](log-analytics-ad-replication-status.md)                           | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | Tooadd non disponible à partir du portail Azure/marketplace. |
| [Agent Health](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | Extrémité de niveau gratuit toohello pas soumettent de données<br> Tooadd non disponible à partir du portail Azure/marketplace. |
| [Gestion des alertes](log-analytics-solution-alert-management.md)                            | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | Tooadd non disponible à partir du portail Azure/marketplace. |
| [Application Insights Connector (préversion)](log-analytics-app-insights-connector.md)                                               | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Automation Hybrid Worker](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automation & Control</li></ul>                                  | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)                                                                         | Nécessite votre tooan de toobe lié de l’espace de travail Analytique de journal compte Automation |
| [Azure Application Gateway Analytics](log-analytics-azure-networking-analytics.md)    | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Azure Network Security Group Analytics](log-analytics-azure-networking-analytics.md)     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Azure SQL Analytics (préversion)](log-analytics-azure-sql.md)                                                       | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br>Par&nbsp;nœud&nbsp;(OMS)                                                                          | Nécessite votre tooan de toobe lié de l’espace de travail Analytique de journal compte Automation|
| [Azure Web Apps Analytics](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
|[Sauvegarde](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Insight & Analytics</li></ul>                                   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)                                                                       | Nécessite un archivage de sauvegarde classique.<br> Tooadd non disponible à partir du portail Azure/marketplace. |
| [Capacity and Performance (préversion)](log-analytics-capacity.md)                                                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Suivi des modifications](log-analytics-change-tracking.md)                                       | <ul><li>Automation & Control</li></ul>                                  | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)                                                                         | Nécessite votre tooan de toobe lié de l’espace de travail Analytique de journal compte Automation |
| [Conteneurs](log-analytics-containers.md)                                                 | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [IT Service Management Connector (préversion)](log-analytics-itsmc-overview.md)                                              | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)     | |
| HDInsight HBase Monitoring <br>(Préversion)                                                  | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Key Vault Analytics](log-analytics-azure-key-vault.md)                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Logic Apps B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | Tooadd non disponible à partir du portail Azure/marketplace. |
| [Évaluation des logiciels malveillants](log-analytics-malware.md)                                            | <ul><li>Security and Compliance</li></ul>                                 | Gratuit<br> Standalone<br>Par&nbsp;nœud&nbsp;(OMS)                                                                           | Si vous ajoutez des solutions de sécurité et conformité hello après le 19 juin 2017 [facturation s’effectue pour chaque nœud](https://azure.microsoft.com/pricing/details/security-compliance/), quel que soit le niveau de tarification de l’espace de travail de hello. Hello 60 premiers jours sont gratuits.  |
| [Analyseur de performances réseau](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Insight & Analytics</li></ul>                                   | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)                                                                         | |
| [Office 365 Analytics (préversion)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Security and Audit](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Security&nbsp;&&nbsp;Compliance</li></ul>                       | Gratuit<br> Standalone<br>Par&nbsp;nœud&nbsp;(OMS)                                                                           | La collecte des journaux des événements de sécurité requiert cette solution<br>Si vous ajoutez des solutions de sécurité et conformité hello après le 19 juin 2017 [facturation s’effectue pour chaque nœud](https://azure.microsoft.com/pricing/details/security-compliance/), quel que soit le niveau de tarification de l’espace de travail de hello. Hello 60 premiers jours sont gratuits. |
| [Service Fabric Analytics (version préliminaire)](log-analytics-service-fabric.md)                     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Service Map (préversion)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Insight & Analytics</li></ul>                      | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)                                                                         | Disponible dans les régions Est des États-Unis, Europe de l’Ouest et Ouest-Centre des États-Unis    |
| [Site Recovery](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Insight & Analytics</li></ul>                                   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)                                                                       | Nécessite un coffre Site Recovery classique.<br> Tooadd non disponible à partir du portail Azure/marketplace. |
| [Évaluation de SQL](log-analytics-sql-assessment.md)                                         | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| Démarrer/arrêter des machines virtuelles pendant les heures creuses<br>(Préversion)                                              | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)                                                                         | Nécessite votre tooan de toobe lié de l’espace de travail Analytique de journal compte Automation |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | Tooadd non disponible à partir du portail Azure/marketplace. |
| [System Center Operations Manager Assessment (préversion)](log-analytics-scom-assessment.md)  | <ul><li>Insight & Analytics</li><li>Log Analytics</li></ul>        | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Gestion des mises à jour](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automation & Control</li></ul>                                  | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)                                                                         | Nécessite votre tooan de toobe lié de l’espace de travail Analytique de journal compte Automation |
| [Update Compliance (préversion)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | Pas de frais pour les données ou les nœuds<br>Extrémité de niveau gratuit toohello pas soumettent de données.<br> Tooadd non disponible à partir du portail Azure/marketplace. |
| [Préparation à la mise à niveau](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | Pas de frais pour les données ou les nœuds<br>Extrémité de niveau gratuit toohello pas soumettent de données.<br> Tooadd non disponible à partir du portail Azure/marketplace. |
| [VMware Monitoring (préversion)](log-analytics-vmware.md)                                | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Standard<br> Premium&nbsp;(OMS)<br> Par&nbsp;Go&nbsp;(autonome)<br> Par&nbsp;nœud&nbsp;(OMS)   | |
| [Wire Data 2.0 (préversion)](log-analytics-wire-data.md)                                                                 | <ul><li>Insight & Analytics</li></ul>                                   | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)                                                                         | Disponible dans les régions Est des États-Unis, Europe de l’Ouest et Ouest-Centre des États-Unis |

<sup>1</sup> hello *Standard* et *Premium (OMS)* niveaux de tarification sont uniquement disponibles pour les clients qui a créé leur espace de travail d’Analytique de journal précédente tooSeptember 21, 2016.

### <a name="community-provided-management-solutions"></a>Solutions de gestion fournies par la communauté

Solutions de communauté fournie sont disponibles à partir de hello [galerie de modèles Azure](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) et direct des auteurs de hello.

| Solution de gestion               | Offre                                                                     | Niveaux de tarification                         | Remarques |
| ---                               | ---                                                                       | ---                                   | ---   |
| Toutes les solutions fournies par la communauté  | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuit<br> Par&nbsp;nœud&nbsp;(OMS)     |   Nécessite votre tooan de toobe lié de l’espace de travail Analytique de journal compte Automation |




## <a name="data-collection-details"></a>Détails sur la collecte de données
Hello tableaux suivants présentent les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour l’Analytique des journaux gestion des solutions et sources de données. tables Hello sont classés par les offres de solution, qui sont équivalentes trop[abonnement niveaux tarifaires](https://go.microsoft.com/fwlink/?linkid=827926). Hello solution d’Analytique de journal d’activité est tooall disponible gratuitement des niveaux tarifaires.

Hello agent Windows Analytique de journal et System Center Operations Manager agent sont essentiellement hello identiques. l’agent Windows Hello inclut des fonctionnalités supplémentaires tooallow il tooconnect toohello OMS espace de travail et d’itinéraire via un proxy. Si vous utilisez un agent Operations Manager, il doit être ciblé comme un toocommunicate de l’agent OMS avec OMS. Agents Operations Manager dans cette table sont des agents OMS sont connectées tooOperations Manager. Consultez [connecter Operations Manager tooLog Analytique](log-analytics-om-agents.md) pour plus d’informations sur la connexion de votre tooOMS d’environnement Operations Manager existant.

> [!NOTE]
> type Hello d’agent que vous utilisez détermine la façon dont les données sont envoyées tooOMS, avec hello conditions suivantes :
> - Vous utilisez l’agent Windows hello ou un agent OMS d’attachement Operations Manager.
> - Si Operations Manager est nécessaire, les données de l’agent Operations Manager pour la solution de hello sont toujours envoyées tooOMS à l’aide du groupe d’administration Operations Manager hello. En outre, quand Operations Manager est requis, seulement l’agent Operations Manager hello est utilisé par la solution de hello.
> - Operations Manager n’est pas requis lorsque et de table de hello montre que les données de l’agent Operations Manager sont envoyées tooOMS à l’aide du groupe d’administration hello, puis les données de l’agent Operations Manager sont systématiquement envoyé de tooOMS à l’aide de groupes d’administration. Les agents Windows contourner le groupe d’administration hello et envoyer leurs données directement tooOMS.
> - Lorsque les données de l’agent Operations Manager ne sont pas envoyées à l’aide d’un groupe d’administration, puis hello envoyées directement tooOMS, en ignorant le groupe d’administration hello.

### <a name="insight--analytics--log-analytics"></a>Insight & Analytics / Log Analytics

| Solution de gestion | Plateforme | Microsoft Monitoring Agent | Agent Operations Manager | Stockage Azure | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | Fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Activity Log Analytics | Microsoft Azure |   |   |   |   |   | sur notification |
| AD Assessment |Windows |&#8226; |&#8226; |  |  |&#8226; |7 jours |
| AD Replication Status |Windows |&#8226; |&#8226; |  |  |&#8226; |5 jours |
| Agent Health | Windows et Linux | &#8226; | &#8226; |   |   | &#8226; | 1 minute |
| Alert Management (Nagios) |Linux |&#8226; |  |  |  |  |à l'arrivée |
| Alert Management (Zabbix) |Linux |&#8226; |  |  |  |  |1 minute |
| Alert Management (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 minutes |
| Application Insights Connector (préversion) | Microsoft Azure |   |   |   |   |   | sur notification |
| Azure Application Gateway Analytics | Microsoft Azure |   |   |   |   |   | sur notification |
| Azure Network Security Group Analytics | Microsoft Azure |   |   |   |   |   | sur notification |
| Azure SQL Analytics (préversion) |Windows |  |  |  |  |  | 10 minutes |
| Gestion de la capacité |Windows |&#8226; |&#8226; |  |  |&#8226; |à l'arrivée |
| Conteneurs | Windows et Linux | &#8226; | &#8226; |   |   |   | 3 minutes |
| Key Vault Analytics |Windows |  |  |  |  |  |sur notification |
| Network Performance Monitor | Windows | &#8226; | &#8226; |   |   |   | Établissements de liaisons TCP toutes les 5 secondes, données envoyées toutes les 3 minutes |
| Office 365 Analytics (préversion) |Windows |  |  |  |  |  |sur notification |
| Service Fabric Analytics |Windows |  |  |&#8226; |  |  |5 minutes |
| Service Map | Windows et Linux | &#8226; | &#8226; |   |   |   | 15 secondes |
| SQL Assessment |Windows |&#8226; |&#8226; |  |  |&#8226; |7 jours |
| SurfaceHub |Windows |&#8226; |  |  |  |  |à l'arrivée |
| System Center Operations Manager Assessment (préversion) | Windows | &#8226; | &#8226; |   |   | &#8226; | sept jours |
| Upgrade Analytics (préversion) | Windows | &#8226; |   |   |   |   | 2 jours |
| VMware Monitoring (préversion) | Linux | &#8226; |   |   |   |   | 3 minutes |
| Wire Data |Windows (2012 R2 / 8.1 ou ultérieur) |&#8226; |&#8226; |  |  |  | 1 minute |


### <a name="automation--control"></a>Automation & Control

| Solution de gestion | Plateforme | Microsoft Monitoring Agent | Agent Operations Manager | Stockage Azure | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | Fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Automation Hybrid Worker | Windows | &#8226; | &#8226; |   |   |   | n/a |
| Suivi des modifications |Windows |&#8226; |&#8226; |  |  |&#8226; |Toutes les heures |
| Suivi des modifications |Linux |&#8226; |  |  |  |  |Toutes les heures |
| Update Management | Windows |&#8226; |&#8226; |  |  |&#8226; |au moins 2 fois par jour et 15 minutes après l'installation d'une mise à jour |

### <a name="security--compliance"></a>Security & Compliance

| Solution de gestion | Plateforme | Microsoft Monitoring Agent | Agent Operations Manager | Stockage Azure | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | Fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Antimalware Assessment |Windows |&#8226; |&#8226; |  |  |&#8226; |Toutes les heures |
| Security and Audit<sup>1</sup> | Windows et Linux | partielle | partielle | partielle |   | partielle | divers |

<sup>1</sup> hello de sécurité et la solution d’Audit peut collecter les journaux des agents Windows, Operations Manager et Linux. Consultez [Sources de données](#data-sources) pour obtenir des informations sur la collecte de données concernant :

- syslog
- Journaux des événements de sécurité Windows
- Journaux du pare-feu Windows
- Journaux d’événements Windows



### <a name="protection--recovery"></a>Protection et récupération

| Solution de gestion | Plateforme | Microsoft Monitoring Agent | Agent Operations Manager | Stockage Azure | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | Fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Sauvegarde | Microsoft Azure |   |   |   |   |   | n/a |
| Azure Site Recovery | Microsoft Azure |   |   |   |   |   | n/a |


### <a name="data-sources"></a>Sources de données


| Source de données | Plateforme | Microsoft Monitoring Agent | Agent Operations Manager | Stockage Azure | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | Fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Journaux d’activité Azure |Windows |  |  |  |  |  |sur notification |
| Journaux de diagnostic Azure |Windows |  |  |  |  |  |sur notification |
| Métriques de diagnostic Azure |Windows |  |  |  |  |  |sur notification |
| ETW |Windows |  |  |&#8226; |  |  |5 minutes |
| Journaux IIS |Windows |&#8226; |&#8226; |&#8226; |  |  |5 minutes |
| Compteurs de performance |Windows |&#8226; |&#8226; |  |  |  |comme prévu, minimum de 10 secondes |
| Compteurs de performance |Linux |&#8226; |  |  |  |  |comme prévu, minimum de 10 secondes |
| syslog |Linux |&#8226; |  |  |  |  |depuis le stockage Azure : 10 minutes ; à partir de l’agent : à l’arrivée |
| Journaux des événements de sécurité Windows |Windows |&#8226; |&#8226; |&#8226; |  |  |pour le stockage Azure : 10 minutes ; pour l’agent de hello : à l’arrivée |
| Journaux du pare-feu Windows |Windows |&#8226; |&#8226; |  |  |  |à l'arrivée |
| Journaux des événements Windows |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |pour le stockage Azure : 10 minutes ; pour l’agent de hello : à l’arrivée |



## <a name="preview-management-solutions-and-features"></a>Solutions de gestion et fonctionnalités en préversion
En exécutant un service et en suivant les pratiques devops, nous sommes en mesure de toopartner avec les fonctionnalités de toodevelop de clients et des solutions.

Version préliminaire privée, nous donner un petit groupe de clients accès tooan première mise en œuvre de commentaires de toogain de fonctionnalité ou une solution hello et apporter des améliorations. Cette implémentation anticipée a des fonctionnalités minimales.

Notre objectif est les choses tootry rapidement afin de nous pouvons trouver ce qui fonctionne et ce qui ne fonctionne pas. Nous avons une itération au sein de ce processus jusqu'à ce que les commentaires hello des clients de version préliminaire limitée de hello nous informant que nous sommes prêts pour une version préliminaire publique.

Au cours de la version préliminaire publique de hello, nous rendre hello fonctionnalité ou une solution disponible pour tous les utilisateurs tooget plus de commentaires et valider notre mise à l’échelle et l’efficacité. Pendant cette phase :

* Fonctionnalités d’aperçu s’affichent dans l’onglet Paramètres de hello et peuvent être activées par un utilisateur.
* Solutions d’aperçu sont ajoutées via la galerie de hello ou à l’aide d’un script.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>Que dois-je savoir sur les fonctionnalités et solutions en préversion ?
Nous sommes impatients de nouvelles fonctionnalités et des solutions de gestion et nous aimons travailler avec vous toodevelop les.

Les solutions et fonctionnalités en préversion ne sont pas adaptées à chacun. Avant de demander toojoin un aperçu privé ou l’activation d’une version préliminaire publique, assurez-vous que vous travaillez OK avec un élément qui est en cours de développement.

Lorsque vous activez une fonctionnalité d’aperçu via le portail de hello, vous voyez un avertissement vous rappelant que hello fonctionnalité est en version préliminaire.

#### <a name="for-both-private-and-public-preview"></a>Pour les préversions *privées* et *publiques*
Hello informations suivantes s’appliquent les aperçus publiques et privées tooboth :

* Les choses ne marchent pas toujours correctement.
  * Problèmes de plage ne soient pas un problème secondaire via toosomething ne fonctionne ne pas du tout.
* Possibilités de hello aperçu toohave un impact négatif sur vos systèmes / environnement.
  * Nous essayons tooavoid les choses négatif se produise systèmes de toohello que vous utilisez avec OMS, mais parfois inattendus choses se produisent.
* Une perte/altération des données peut se produire.
* Nous pouvons poser vous toocollect les journaux de diagnostic ou autres toohelp données résoudre les problèmes.
* fonctionnalité de Hello ou une solution peut être supprimée (temporairement ou définitivement).
  * Selon nos connaissances acquises pendant l’aperçu de hello nous pouvons décider toonot version hello fonctionnalité ou une solution.
* Les préversions peuvent ne pas fonctionner ou ne pas avoir été testées avec toutes les configurations, donc nous pouvons limiter :
  * Hello des systèmes d’exploitation qui peut être utilisés (par exemple, une fonction peut uniquement s’appliquer tooLinux dans l’aperçu).
  * Hello du type d’agent (MMA, Operations Manager) qui peut être utilisé (par exemple, une fonctionnalité peuvent ne pas fonctionne avec Operations Manager dans l’aperçu).  
* Aperçu des solutions et fonctionnalités ne sont pas couverts par hello contrat de niveau de Service.
* L’utilisation des fonctionnalités en préversion occasionne des frais d’utilisation.
* Fonctions ou fonctionnalités que vous avez besoin pour la fonctionnalité de hello / toobe solution utile est peut-être manquant ou incomplet.
* Les fonctionnalités et solutions peuvent ne pas être disponibles dans toutes les régions.
* Les fonctionnalités et solutions peuvent ne pas être localisées.
* Fonctionnalités / solutions peuvent avoir une limite sur le nombre hello de clients ou de périphériques qui peuvent l’utiliser.
* Vous devrez peut-être toouse tooperform configuration et tooenable hello solution/fonctionnalité scripts.
* interface utilisateur (IU) du Hello est incomplète et peut changer à partir du jour tooday.
* Les préversions publiques peuvent ne pas être appropriées pour vos systèmes de production ou critiques.

#### <a name="for-private-preview"></a>Pour la préversion *privée*
Dans les éléments toohello Ajout ci-dessus, hello informations suivantes est aperçus de tooprivate spécifique :

* Nous pensons que tooprovide nous avec des commentaires sur votre expérience afin que nous pouvons faire hello fonctionnalité/solution mieux.
* Nous pouvons vous contacter pour recueillir vos commentaires au moyen d’enquêtes, par téléphone ou par e-mail.
* Les choses ne fonctionnent pas toujours correctement.
* Nous pouvons imposer un accord de confidentialité pour la participation ou inclure du contenu confidentiel.
  * Avant la création de blogs, Tweeter ou autre moyen de communication avec des tiers, consultez l’hello responsable de programme qui est chargée de hello aperçu toounderstand des restrictions sur la divulgation d’informations.
* N’exécutez pas la fonctionnalité ou la solution sur des systèmes de production ou critiques.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>Comment obtenir des solutions et des fonctionnalités en version préliminaire tooprivate accès ?
Nous invitons les aperçus de tooprivate clients via plusieurs façons différentes en fonction de la version préliminaire de hello.

* Répondant à enquête utilisateur mensuel de hello et abandonne nous toofollow d’autorisation avec vous améliorent vos chances de version préliminaire limitée de tooa invités.
* Votre équipe des comptes Microsoft peut vous désigner.
* Vous pouvez vous inscrire en fonction des détails publiés sur twitter [msopsmgmt](https://twitter.com/msopsmgmt).
* Vous pouvez vous inscrire en fonction des détails partagés à l’occasion d’événements communautaires : recherchez-nous dans les rencontres, conférences et communautés en ligne.

## <a name="next-steps"></a>Étapes suivantes
* [Rechercher des journaux](log-analytics-log-searches.md) tooview détaillées des informations collectées par les solutions de gestion.
