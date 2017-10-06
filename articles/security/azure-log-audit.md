---
title: "aaaAzure journalisation et d’audit | Documents Microsoft"
description: "Découvrez comment vous pouvez utiliser la journalisation des données toogain informations détaillées relatives à votre application."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Journalisation et audit Azure
## <a name="introduction"></a>Introduction
### <a name="overview"></a>Vue d'ensemble
tooassist actuels et futurs Azure aux clients de comprendre et à l’aide de hello différentes fonctionnalités liées à la sécurité disponibles dans et se rapportant à hello plateforme Azure, Microsoft a développé une série de livres blancs, les vues d’ensemble de la sécurité, les meilleures pratiques et les listes de contrôle. les rubriques de Hello en termes de largeur et la profondeur de plage et sont régulièrement mises à jour. Ce document fait partie de cette série comme résumé dans hello après section abstraite.
### <a name="azure-platform"></a>Plateforme Azure
Azure est une plateforme de service de cloud ouverte et flexible qui prend en charge hello plus vaste choix de systèmes d’exploitation, langages de programmation, infrastructures, outils, bases de données et les appareils.

Vous pouvez par exemple afficher :
-   Exécuter des conteneurs Linux avec l’intégration Docker.

-   Créer des applications avec JavaScript, Python, .NET, PHP, Java et Node.js

-   Créer des serveurs principaux pour les appareils iOS, Android et Windows.

Services de cloud public Azure prend en charge hello mêmes technologies des millions de développeurs et professionnels de l’informatique s’appuient sur déjà et faites confiance.

Lorsque vous générez, ou migrez des ressources informatiques à un fournisseur de cloud, vous recourez tooprotect des capacités de cette organisation vos applications et données avec hello contrôles hello et les services qu’ils sécurisent toomanage hello vos ressources de cloud.

L’infrastructure Azure est conçu de tooapplications de fonctionnalité hello pour l’hébergement des millions de clients simultanément, et fournit une base fiable sur laquelle entreprises peuvent répondre aux besoins de leur sécurité. En outre, Azure vous offre un large éventail de toocontrol de capacité hello et les options de sécurité configurables leur afin que vous pouvez personnaliser les exigences uniques de hello toomeet sécurité de vos déploiements. Ce document vous aidera à répondre à ces exigences.

### <a name="abstract"></a>Résumé
L’audit et la journalisation des événements liés à la sécurité, de même que les alertes associées, constituent des composants importants dans une stratégie de protection des données efficace. Les rapports et les journaux de sécurité vous fournissent un enregistrement électronique des activités suspectes et aide à détecter les modèles qui peuvent indiquer des intrusions externes tentative réussie ou non de hello réseau, ainsi que les attaques internes. Vous pouvez utiliser l’activité utilisateur d’audit toomonitor, conformité aux normes de document, effectuer une analyse d’investigation et bien plus encore. Les alertes envoient une notification immédiate lorsque des événements de sécurité se produisent.

Produits et services Microsoft Azure vous fournissent l’audit de sécurité configurable et empêche les violations de journalisation toohelp options vous identifiez les écarts de vos stratégies de sécurité et les mécanismes et toohelp de ces espaces d’adresses. Les services Microsoft offrent certains (et dans certains cas, toutes les) Hello options suivantes : centralisée de surveillance, la journalisation et la visibilité continue analyse les systèmes tooprovide ; génération d’alertes ; et toohelp de rapports que vous gérez hello grande quantité d’informations générées par les appareils et services.

Les données de journal de Microsoft Azure peuvent être exporté tooSecurity systèmes Incident et la gestion des événements (SIEM) pour l’analyse et s’intègre avec les solutions d’audit tiers.

Ce livre blanc présente la génération, la collecte et l’analyse des journaux de sécurité provenant de services hébergés dans Azure. Il vous permettra également d’obtenir des informations sur la sécurité de vos déploiements Azure. étendue Hello de ce livre blanc est tooapplications limitées et services générées et déployées dans Azure.

> [!Note]
> Certaines recommandations contenues dans ce document peuvent augmenter l’utilisation des données, des réseaux ou des ressources de calcul et entraîner des coûts de licence ou d’abonnement supplémentaires.

## <a name="types-of-logs-in-azure"></a>Types de journaux dans Azure
Les applications cloud sont complexes, et se composent de nombreux éléments mobiles. Journaux fournissent des données tooensure que votre application reste opérationnel et en cours d’exécution dans un état sain. Cela permet également vous toostave désactivé des problèmes potentiels ou de dépanner au-delà de celles. En outre, vous pouvez utiliser la journalisation des données toogain informations détaillées sur votre application. Ces connaissances peuvent vous aider à tooimprove des performances des applications ou facilité de maintenance, ou automatiser des actions qui nécessiteraient sinon une intervention manuelle.

Azure génère une journalisation complète pour chaque service Azure. Ces journaux sont classés selon ces deux types principaux :
-   **Des journaux de contrôle/gestion** offrent une visibilité en hello les opérations de création de gestionnaire de ressources Azure, UPDATE et DELETE. Les [journaux d’activité Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) sont un exemple de ce type de journal.

-   **Données plan journaux** offrent une visibilité en événements hello déclenché dans le cadre de l’utilisation de hello d’une ressource Azure. Hello des événements Windows, système de sécurité, et de journaux des applications dans une machine virtuelle et le hello sont des exemples de ce type de journal [les journaux de diagnostic](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) configuré via le moniteur de Windows Azure


-   Les **événements traités** fournissent des informations sur les événements/alertes analysés en votre nom. Les alertes [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) en sont un exemple, où [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) a traité et analysé votre abonnement et fournit des alertes de sécurité très concises.

la table suivante de Hello type le plus important liste des journaux disponibles dans Azure.

| Catégorie du journal | Type de journal | Utilisations | Intégration |
| ------------ | -------- | ------ | ----------- |
|[Journaux d’activité](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Événements de plan de contrôle sur les ressources d’Azure Resource Manager| Fournit des détails sur les opérations de hello qui ont été effectuées sur les ressources dans votre abonnement.|   API Rest et [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Journaux de diagnostic Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|données fréquentes relatives au fonctionnement de hello des ressources Azure Resource Manager dans l’abonnement| Fournissent des informations sur les opérations effectuées par votre ressource| Azure Monitor, [diffusion](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[Création de rapports AAD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|Journaux et rapports|Activités d’authentification des utilisateurs et informations sur l’activité système en matière de gestion des utilisateurs et des groupes|[API Graph](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[Machines virtuelles et services cloud](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Journal des événements Windows et Syslog Linux|  Capture des données système et les données de journalisation sur les ordinateurs virtuels de hello et transfère les données dans un compte de stockage de votre choix.| Windows avec stockage [WAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (Windows Azure Diagnostics) et Linux dans Azure Monitor|
|[Analyse du stockage](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|Journalise le stockage et fournit des données de métriques pour un compte de stockage|Fournit des informations sur les demandes, analyse les tendances d’utilisation et diagnostique les problèmes liés à votre compte de stockage.|  API REST ou hello [bibliothèque cliente](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[Journalisation des flux de groupe de sécurité réseau](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|Format JSON, affiche les flux entrants et sortants, par règle|Afficher des informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau|[Network Watcher](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|Journaux, exceptions et diagnostics personnalisés|  Service de gestion des performances des applications (APM) destiné aux développeurs web sur de multiples plateformes.| API REST, [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|Traitement des données/alertes de sécurité| Alerte Azure Security Center, alerte OMS| Informations relatives à la sécurité et alertes.|   API REST, JSON|

### <a name="activity-log"></a>Journal d’activité
Hello [journal des activités Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), fournissent des indications sur les opérations de hello qui ont été effectuées sur les ressources dans votre abonnement. Hello journal d’activité était précédemment appelé « Journaux d’Audit » ou « Journaux des opérations », car elle indique [panneau événements](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) pour vos abonnements. À l’aide de hello journal d’activité, vous pouvez déterminer hello », qui et à quel moment » pour toutes les opérations (PUT, POST, DELETE) effectuées sur les ressources hello dans votre abonnement d’écriture. Vous pouvez également comprendre état hello d’opération de hello et d’autres propriétés pertinentes. Hello journal d’activité n’inclut pas les opérations de lecture (GET).

PUT, POST, DELETE fait ici référence d’opérations d’écriture tooall hello journal d’activité contient les ressources hello. Par exemple, vous pouvez utiliser hello activité journaux toofind une erreur lors de la résolution des problèmes ou toomonitor comment un utilisateur dans votre organisation a modifié une ressource.

![Journal d’activité](./media/azure-log-audit/azure-log-audit-fig1.png)


Vous pouvez récupérer des événements à partir de votre journal des activités à l’aide du portail Azure, de hello [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), applets de commande PowerShell, et [API REST de Azure analyse](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough). La période de rétention des données des journaux d’activité est de 19 jours.

Scénarios d’intégration
-   [Créez une alerte via e-mail ou webhook qui déclenche un événement de journal d’activité.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [Tooan concentrateur d’événements de flux](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) pour l’ingestion par un service tiers ou d’une solution personnalisée analytique telles que Power BI.

-   Analyser dans Power BI à l’aide de hello [pack de contenu Power BI.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [Enregistrez-le tooa compte de stockage pour l’inspection d’archivage ou manuelle.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) Vous pouvez spécifier la durée de rétention hello (en jours) à l’aide de profils de journal.

-   Interroger et afficher dans hello portail Azure.

-   Interrogez-le via l’applet de commande PowerShell, l’interface de ligne de commande ou l’API REST.

-   Exporter hello journal d’activité avec des profils de journal trop[Analytique de journal](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

Vous pouvez utiliser un compte de stockage ou [espace de noms hub événement](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) qui ne figure pas dans hello même abonnement que hello un journal de l’émission. utilisateur Hello qui configure hello paramètre doit avoir hello approprié [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) accéder tooboth abonnements
### <a name="azure-diagnostic-logs"></a>Journaux de diagnostic Azure
Les journaux de Diagnostic Azure sont émis par une ressource qui fournissent des données riches et fréquentes relatives au fonctionnement de hello de cette ressource. le contenu de ces journaux Hello varie selon le type de ressource (par exemple, [journaux des événements système Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)sont une catégorie de journal de diagnostics pour les machines virtuelles et [blob, table et journaux de la file d’attente](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) sont les catégories de journaux de Diagnostic pour les comptes de stockage) et diffèrent hello journal d’activité, qui permet de connaître les opérations hello qui ont été effectuées sur les ressources dans votre abonnement.

![Journaux de diagnostic Azure](./media/azure-log-audit/azure-log-audit-fig2.png)

Les journaux de diagnostic Azure offrent plusieurs options de configuration (portail Azure) via PowerShell, l’interface de ligne de commande (CLI) et l’API REST.

**Scénarios d’intégration**
-   Enregistrer les tooa [compte de stockage](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) pour l’inspection de l’audit ou manuelle. Vous pouvez spécifier la durée de rétention hello (en jours) à l’aide des paramètres de Diagnostic hello.

-   [Les flux tooEvent concentrateurs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) pour l’ingestion par un service tiers ou d’une solution d’analytique personnalisé comme [Power BI.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   Analysez-les avec [OMS Log Analytics.](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

**Services pris en charge, schéma pour les journaux de diagnostic et catégories de journaux prises en charge par type de ressource**


| Service | Schéma et documentation | Type de ressource | Catégorie |
| ------- | ------------- | ------------- | -------- |
|Load Balancer| [Analyse des journaux de l’équilibreur de charge Azure (version préliminaire)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|Groupes de sécurité réseau|[Analyse de journaux pour les groupes de sécurité réseau (NSG)](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|Passerelles d’application|[Journalisation des diagnostics pour Application Gateway](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|Key Vault|[Journalisation d’Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Recherche Azure|[Activation et utilisation de la fonctionnalité Rechercher l’analyse du trafic](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Data Lake Store|[Accès aux journaux de diagnostic d’Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|Audit|
|Data Lake Analytics|[Accès aux journaux de diagnostic d’Azure Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|Audit|
|||Microsoft.DataLakeAnalytics/accounts|Demandes|
|||Microsoft.DataLakeStore/accounts|Demandes|
|Logic Apps|[Schéma de suivi personnalisé Logic Apps B2B](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Azure Batch|[Journalisation des diagnostics Azure Batch](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Azure Automation|[Log Analytics pour Azure Automation](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Event Hubs|[Journaux de diagnostic d’Azure Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|Stream Analytics|[Journaux de diagnostic des travaux](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|Exécution|
|||Microsoft.StreamAnalytics/streamingjobs|Création|
|Service Bus|[Journaux de diagnostic Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Création de rapports Active Directory
Azure Active Directory (Azure AD) comprend des rapports sur la sécurité, les activités et l’audit concernant votre annuaire. Hello [rapport de d’Audit Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) permet aux clients les actions tooidentify privilégié qui s’est produite dans leur annuaire Active Directory de Azure. Des actions privilégiées incluent des modifications d’élévation (par exemple, la création de rôle ou les réinitialisations de mot de passe), la modification des configurations de stratégie (par exemple des stratégies de mot de passe), ou la configuration de toodirectory de modifications (par exemple, modifications toodomain paramètres de fédération).

Hello rapports fournissent un enregistrement d’audit de hello pour nom de l’événement hello, acteur hello qui a effectué l’action hello, les ressources de cible hello affectées par la modification de hello et hello date et heure (UTC). Les clients sont liste de hello tooretrieve en mesure d’événements d’audit pour leurs Azure Active Directory via hello [portail Azure](https://portal.azure.com/), comme décrit dans [afficher vos journaux d’Audit](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Voici une liste des rapports hello inclus :

| Rapports de sécurité | Rapports d’activité | Rapport d’audit |
| :--------------- | :--------------- | :------------ |
|Connexions à partir de sources inconnues| Utilisation des applications : résumé| Rapport d’audit d’annuaire|
|Connexions après plusieurs échecs|  Utilisation des applications : présentation détaillée||
|Connexions depuis plusieurs zones géographiques|    Tableau de bord de l’application||
|Connexions depuis des adresses IP avec des activités suspectes|   Erreurs de configuration de compte||
|Activité de connexion anormale|    Appareils des utilisateur individuels||
|Connexions à partir d’appareils potentiellement infectés|   Activité des utilisateurs individuels||
|Utilisateurs ayant une activité de connexion anormale| Rapport d'activité de groupes||
||Rapport d’activité de l’enregistrement de la réinitialisation de mot de passe||
||Activité de réinitialisation de mot de passe|||

données de Hello de ces rapports peuvent être des applications de tooyour utiles, telles que les systèmes SIEM, l’audit et les outils Business intelligence. Bonjour Azure AD reporting Qu'api fournit des données de toohello de l’accès par programme via un ensemble d’API REST. Vous pouvez appeler ces [API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) à partir de divers outils et langages de programmation.

Événements dans les rapports d’Audit Azure AD de hello sont conservées pendant 180 jours.

> [!Note]
> Pour plus d’informations sur la rétention des rapports, consultez la page [Stratégies de rétention des rapports Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Pour les clients intéressés par le stockage aux événements d’audit pour les périodes de rétention plus longues, hello API Reporting peut être utilisé par extraction de données tooregularly [événements d’audit](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) dans un magasin de données distinct.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>Journaux de machines virtuelles avec Azure Diagnostics
[Diagnostics Azure](https://docs.microsoft.com/azure/azure-diagnostics) est une fonctionnalité hello dans Azure qui active la collecte de hello de données de diagnostic sur une application déployée. Vous pouvez utiliser l’extension de diagnostics hello dans différentes sources. Sont actuellement pris en charge les [rôles de travail et web Azure Cloud Services](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me).

![Journaux de machines virtuelles avec Azure Diagnostics](./media/azure-log-audit/azure-log-audit-fig3.png)

[Machines virtuelles Azure](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) fonctionnant sous Microsoft Windows et [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

Vous pouvez activer Azure Diagnostics sur une machine virtuelle, comme suit :

-   À l’aide de Visual Studio, consultez [utilisez Visual Studio tootrace des Machines virtuelles Azure](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Configurer les diagnostics Azure sur une machine virtuelle Azure à distance](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Utilisez tooset PowerShell des diagnostics sur des Machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [Créer une machine virtuelle Windows avec des fonctionnalités de surveillance et de diagnostics à l’aide d’un modèle Azure Resource Manager](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>Storage Analytics
[L’analyse du stockage Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) effectue la journalisation et fournit les données d’indicateurs de performance d’un compte de stockage. Vous pouvez utiliser cette tootrace des demandes de données, analyser les tendances d’utilisation et diagnostiquer les problèmes avec votre compte de stockage. Journalisation d’Analytique de stockage est disponible pour hello [services Blob, file d’attente et Table.](https://docs.microsoft.com/azure/storage/storage-introduction) Stockage Analytique enregistre des informations détaillées sur le service de stockage tooa demandes réussies et ayant échoué.

Ces informations peuvent être utilisées toomonitor des requêtes individuelles et les problèmes de toodiagnose avec un service de stockage. Les demandes sont enregistrées sur la base du meilleur effort. Entrées de journal sont créées uniquement si des requêtes sont effectuées sur le point de terminaison de service hello. Par exemple, si un compte de stockage comporte des activités dans son point de terminaison d’objet Blob, mais pas dans ses points de terminaison de file d’attente ou Table consigne uniquement se rapportant toohello service Blob est créé.

toouse Analytique de stockage, vous devez l’activer individuellement pour chaque service, vous souhaitez toomonitor. Vous pouvez l’activer dans hello [portail Azure](https://portal.azure.com/); pour plus d’informations, consultez [surveiller un compte de stockage Bonjour portail Azure.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) Vous pouvez également activer Analytique de stockage par programme via l’API REST de hello ou de la bibliothèque cliente de hello. Utilisez hello Set Service Properties opération tooenable stockage Analytique individuellement pour chaque service.

données agrégées Hello sont stockées dans un objet blob connu (pour la journalisation) et dans des tables connues (pour les métriques), qui est accessible à l’aide des API du service de Table et de service d’objets Blob hello.

Analytique de stockage a une limite de 20 To montant hello des données stockées qui est indépendantes de la limite totale de hello pour votre compte de stockage. Tous les journaux sont stockés dans des objets [blob de blocs](https://docs.microsoft.com/azure/storage/storage-analytics) dans un conteneur nommé $logs, qui est automatiquement créé lorsque Storage Analytics est activé pour un compte de stockage.

> [!Note]
> Pour plus d’informations sur les stratégies de facturation et de rétention de données, consultez l’article [Storage Analytics and Billing (Storage Analytics et facturation)](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing).
>
> [!Note]
> Pour plus d’informations sur les limites des comptes de stockage, consultez la page [Objectifs de performance et évolutivité d’Azure Storage](https://docs.microsoft.com/azure/storage/storage-scalability-targets).

Hello, les types de demandes authentifiées et anonymes suivants est enregistré.



| Authentifiée  | Anonyme|
| :------------- | :-------------|
| Demandes ayant réussi | Demandes ayant réussi |
|Demandes ayant échoué, y compris les erreurs de délai d’expiration, limitation, réseau, autorisation et autres erreurs | Demandes utilisant une signature d’accès partagé (SAS), y compris les demandes ayant réussi et ayant échoué |
| Demandes utilisant une signature d’accès partagé (SAS), y compris les demandes ayant réussi et ayant échoué |Erreurs de délai d’expiration pour le client et le serveur |
|   Demande des données tooanalytics |    Demandes GET ayant échoué avec le code d’erreur 304 (non modifié) |
| Les demandes effectuées par Storage Analytics lui-même, telles que la création ou la suppression d'un journal, ne sont pas enregistrées. Une liste complète des données de salutation connectée est documentée dans hello [les Messages d’état et les opérations de journalisation de stockage Analytique](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) et [le Format de journal Analytique stockage](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) rubriques. | Aucune autre demande anonyme ayant échoué n'est enregistrée. Une liste complète des données de salutation connectée est documentée dans hello [les Messages d’état et les opérations de journalisation de stockage Analytique](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) et [Format de stockage du journal Analytique](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |

### <a name="azure-networking-logs"></a>Journaux réseaux Azure
La journalisation et la surveillance réseau dans Azure sont complètes et couvrent deux grandes catégories :

-   [Observateur de réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -réseau basé sur un scénario d’analyse est fourni avec les fonctions hello dans l’Observateur réseau. Ce service inclut la capture de paquets, le tronçon saut suivant, la vérification des flux IP, l’affichage de groupe de sécurité, les journaux de flux de groupe de sécurité réseau. Surveillance au niveau du scénario présente une fin tooend des ressources réseau dans l’analyse de ressource contraste tooindividual réseau.

-   [Surveillance des ressources](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring) - La surveillance au niveau des ressources se compose de quatre fonctionnalités : journaux de diagnostic, mesures, résolution des problèmes et intégrité des ressources. Toutes ces fonctionnalités sont créées au niveau de ressources réseau hello.

![Journaux réseaux Azure](./media/azure-log-audit/azure-log-audit-fig4.png)

Observateur réseau est un service régional qui permet de vous toomonitor et diagnostiquer des conditions à un niveau de scénario réseau, vers et depuis Azure. Diagnostic de réseau et les outils de visualisation disponibles avec l’Observateur réseau vous aider à comprendre, de diagnostiquer et de mieux réseau de tooyour insights dans Azure.

**Enregistrement de flux de groupe de sécurité réseau** -journaux de flux pour les groupes de sécurité réseau permettent de tootraffic connexes toocapture journaux qui sont autorisés ou refusés par des règles de sécurité hello dans le groupe de hello. Ces flux de journaux est écrits au format JSON et affiche sortant des flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur le flux hello (protocole IP Source et de Destination, Port Source et de Destination) et si hello le trafic a été autorisé ou refusé.

### <a name="network-security-group-flow-logging"></a>Journalisation des flux de groupe de sécurité réseau

[Journaux du groupe de sécurité réseau de flux](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau. Ces flux de journaux est écrits au format JSON et affiche sortant des flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur le flux hello (protocole IP Source et de Destination, Port Source et de Destination) et si hello le trafic a été autorisé ou refusé.

Flux enregistre les groupes de sécurité réseau cible, ils ne sont pas affichés même hello comme hello autres journaux. Les journaux de flux sont uniquement stockés au sein d’un compte de stockage.

Hello même des stratégies de rétention comme sur les autres journaux appliquent les journaux de tooflow. Les journaux ont une stratégie de rétention peut être définie de jours too365 de 1 jour. Si une stratégie de rétention n’est pas définie, les journaux de hello sont conservées indéfiniment.

**Journaux de diagnostic**

Événements périodiques et spontanées sont créées par les ressources réseau et enregistrées dans les comptes de stockage, envoyés tooan concentrateur d’événements ou Analytique de journal. Ces journaux fournissent des analyses d’intégrité de hello d’une ressource. Ces journaux peuvent être affichés dans des outils tels que Power BI et Log Analytics. toolearn comment tooview journaux de diagnostic, visitez [Analytique de journal.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![Journaux de diagnostic](./media/azure-log-audit/azure-log-audit-fig5.png)

Les journaux de diagnostic sont disponibles pour [l’équilibrage de charge](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [les groupes de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), les itinéraires et [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Network Watcher permet d’afficher les journaux de diagnostic. Cet affichage contient toutes les ressources réseau qui prennent en charge la journalisation des diagnostics. À partir de celui-ci, vous pouvez activer et désactiver les ressources réseau facilement et rapidement.


Dans les fonctionnalités de journalisation de toopreceding addition, Observateur réseau a actuellement hello suivant de fonctionnalités :
- [Topologie](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -fournit un Bonjour montrant de vue de niveau réseau différents interconnexions et les associations entre les ressources réseau dans un groupe de ressources.

- [Capture de paquets variables](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) - Capture des données de paquets dans et en dehors d’une machine virtuelle. Filtrage des options avancées et des contrôles ajustées par exemple, tooset en mesure de limites de temps et la taille fournissent des données du paquet versatility.hello peuvent être stockées dans un magasin d’objets blob ou sur le disque local dans un format de .cap hello.

-   [Vérification des flux IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) - Vérifie si un paquet est autorisé ou refusé en fonction des paramètres de paquet des informations à 5 tuples de flux (adresse IP de destination, adresse IP source, port de destination, port source et protocole). Si les paquets hello sont refusée par un groupe de sécurité, hello règle et groupe qui a refusé les paquets hello est retournée.

-   [Tronçon suivant](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -détermine le saut suivant de hello pour les paquets routés Bonjour Azure Fabric de réseau, ce qui vous les itinéraires toodiagnose toute mauvaise configuration définie par l’utilisateur.

-   [Affichage de groupe de sécurité](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -Obtient les règles de sécurité efficace et appliquées hello qui sont appliquées sur une machine virtuelle.

-   [Passerelle de réseau virtuel et la résolution des problèmes de connexion](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -hello capacité tootroubleshoot fournit des connexions et des passerelles de réseau virtuel.

-   [Limites de l’abonnement du réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) -vous permet de l’utilisation des ressources réseau tooview par rapport aux limites.

### <a name="application-insight"></a>Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) est un service extensible de gestion des performances des applications (APM) destiné aux développeurs web sur de multiples plateformes. Utiliser toomonitor votre application web dynamique. Ce service détecte automatiquement les problèmes de performances. Il inclut toohelp d’outils puissants analytique vous diagnostiquez des problèmes et toounderstand ce que les utilisateurs effectuent avec votre application.

 Il est conçu toohelp vous améliorer en permanence les performances et la facilité d’utilisation.

 Il fonctionne pour les applications sur un large éventail de plateformes, y compris .NET, Node.js et J2EE, hébergé localement ou dans le cloud de hello. Il s’intègre à votre processus devOps et outils de développement toovarious de points de connexion.

![Application Insights](./media/azure-log-audit/azure-log-audit-fig6.png)

Application Insights est destiné à l’équipe de développement hello, toohelp vous comprenez comment votre application s’exécute et comment il est utilisé. Il analyse les éléments suivants :

-   **Taux de demandes, temps de réponse et taux d’échec** : identifiez les pages les plus consultées, à quel moment de la journée, et déterminez où se trouvent vos utilisateurs. Identifiez les pages qui offrent les meilleures performances. Si vos temps de réponse et votre taux d’échec augmentent lorsqu’il y a plus de requêtes, vous avez peut-être un problème de ressources.

-   **Taux de dépendance, temps de réponse et taux d’échec** : déterminez si des services externes vous ralentissent.

-   **Exceptions** : analyser les statistiques de hello agrégée, ou choisir des instances spécifiques et explorez de trace de la pile hello et requêtes connexes. Les exceptions de serveur et de navigateur sont signalées.

-   **Consultations de pages et performances de chargement** : indiquées par le navigateur de vos utilisateurs.

-   **Appels AJAX** à partir de pages web : taux, temps de réponse et taux d’échec.

-   **Nombre de sessions et d’utilisateurs**.

-   **Compteurs de performances** de vos ordinateurs serveurs Windows ou Linux, par exemple le processeur, la mémoire et l’utilisation du réseau.

-   **Diagnostics d’hébergement** de Docker ou Azure.

-   **Journaux de suivi des diagnostics** de votre application : pour pouvoir mettre en corrélation les événements de suivi avec les demandes.

-   **Événements personnalisés et des mesures** que vous écrivez vous-même dans hello client ou le code serveur, tootrack des événements commerciaux tels que les articles vendus ou jeux won.

**Liste et description des scénarios d’intégration :**

| Scénarios d’intégration | Description |
| --------------------- | :---------- |
|[Plan de l’application](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|composants Hello de votre application, avec des mesures clés et les alertes.||
|[Recherche de diagnostic pour les données d’instance](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| Cherchez et filtrez les événements, comme les requêtes, les exceptions, les appels de dépendance, les suivis de journaux et les affichages de pages.||
|[Metrics Explorer pour les données agrégées](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|Explorez, filtrez et segmentez des données agrégées, comme les taux de demandes, d’échecs et d’exceptions, les temps de réponse et les durées de chargement des pages.||
|[Tableaux de bord](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|Combinez des données de plusieurs sources et partagez-les avec d’autres. Idéal pour les applications à plusieurs composantes et d’affichage en continu dans la salle d’équipe hello.||
|[Flux de métriques temps réel](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|Lorsque vous déployez une nouvelle build, regardez ces toomake d’indicateurs de performance de proximité en temps réel que tout fonctionne comme prévu.||
|[Analyse](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|Répondez à des questions difficiles sur les performances et l’utilisation de votre application avec ce langage de requêtes puissant.||
|[Alertes automatiques et manuelles](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|Alertes automatiques adaptent modèles normal de l’application tooyour de télémétrie et le déclencheur lorsqu’il existe un élément en dehors du modèle habituel de hello. Vous pouvez également définir des alertes sur des niveaux particuliers de mesures personnalisées ou standard.||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Consultez les données de performances dans le code hello. Accédez toocode à partir des traces de pile.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|Intégrez des mesures d’utilisation à d’autres données décisionnelles.||
|[API REST](https://dev.applicationinsights.io/)|Écrire du code toorun requêtes via vos métriques et les données brutes.||
|[Exportation continue](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|Exportation en bloc de données brutes toostorage lorsqu’il atteint.||

### <a name="azure-security-center-alerts"></a>Alertes Azure Security Center
[Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) collecte, analyse automatiquement et intègre des données de journal à partir de vos ressources Azure, hello réseau et les solutions de partenaire connectés, tels que des solutions de protection pare-feu et de point de terminaison, les menaces réelles toodetect et réduire faux positifs. Une liste des alertes de sécurité hiérarchisée est indiquée dans le centre de sécurité, ainsi que de hello informations dont vous avez besoin tooquickly examiner le problème de hello et des recommandations sur la manière tooremediate une attaque.

Détection des menaces de sécurité Center fonctionne en collectant automatiquement des informations de sécurité à partir de vos ressources Azure, hello réseau et les solutions de partenaire connecté. Il analyse cette information, corrélation souvent des informations provenant de plusieurs sources, les menaces tooidentify. Alertes de sécurité sont définies dans le centre de sécurité ainsi que des recommandations sur la tooremediate hello menace.

![Azure Security Center](./media/azure-log-audit/azure-log-audit-fig7.png)

Azure Security Center emploie des analyses de sécurité avancées allant bien au-delà des approches simplement basées sur la signature. Découvertes dans les données de grande taille et [apprentissage](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologies sont des événements de tooevaluate appliquée sur l’infrastructure de cloud entière hello : détection des menaces qui seraient impossible tooidentify à l’aide des méthodes manuelles et de prédiction hello évolution d’attaques. Ces analyses de sécurité comprennent les éléments suivants :

-   **Intégré sur les menaces :** recherche pour connus mauvais acteurs en appliquant des menaces global de produits et services, Microsoft hello Microsoft Digital Crimes unité (DCU), hello MSRC Microsoft Security Response Center () et est externe les flux.

-   **Analytique comportementale :** applique le comportement de modèles connus toodiscover malveillant.

-   **Détection d’anomalie :** utilise statistiques de profilage toobuild une ligne de base historique. Il avertit sur des écarts par rapport à des lignes de base établies conformes vecteur d’attaque potentielle tooa.


De nombreuses opérations de sécurité et les équipes de réponse aux incidents s’appuient sur une solution d’informations sur la sécurité et de gestion des événements (SIEM) en tant que point de départ pour le triage et examen des alertes de sécurité de hello. Grâce à l’intégration des journaux Azure, les clients peuvent synchroniser quasiment en temps réel les alertes de l’Azure Security Center, ainsi que les événements de sécurité des machines virtuelles collectés par les journaux de diagnostics et d’audit Azure, avec leur solution SIEM ou Log Analytics.


## <a name="log-analytics"></a>Log Analytics

Log Analytics est un service d’[Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) qui vous permet de collecter et d’analyser les données générées par les ressources de votre cloud et de vos environnements locaux. Vous donne des informations en temps réel à l’aide de la recherche intégrée et tableaux de bord personnalisés tooreadily l’analyse de millions d’enregistrements dans toutes vos charges de travail et serveurs, quelle que soit leur emplacement physique.

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Centre de journal Analytique hello est référentiel OMS hello, qui est hébergé dans hello cloud Azure. Collecte de données dans le référentiel de hello à partir de sources connectées par la configuration des sources de données et ajout abonnement tooyour de solutions. Solutions et sources de données créent chacune différents types d’enregistrements qui ont leur propre jeu de propriétés, mais peuvent toujours être analysées ensemble dans le référentiel toohello de requêtes. Cela vous permet de hello toouse même toowork outils et méthodes avec différents types de données collecté par différentes sources.

Sources connectées sont les ordinateurs hello et autres ressources qui génèrent des données collectées par Analytique de journal. Cela peut inclure des agents installés sur des ordinateurs [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) et [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) directement connectés, ou des agents d’un [groupe d’administration System Center Operations Manager connecté](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents). Log Analytics peut également collecter des données à partir d’un [stockage Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage).

[Sources de données](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) hello différents types de données collectées à partir de chaque source connectée. Cela inclut les événements et [les données de performances](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) à partir de [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) et des agents de Linux dans toosources ajout comme [journaux IIS](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), et [journaux texte personnalisé.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) Vous configurez chaque source de données que vous souhaitez toocollect et configuration de hello provient tooeach remis automatiquement connecté.

Il existe quatre façons différentes de [collecter des journaux et des métriques pour les services Azure :](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)
1.  Diagnostics Azure directe tooLog Analytique (Diagnostics Bonjour tableau suivant)

2.  Diagnostics Azure tooAzure stockage tooLog Analytique (stockage Bonjour tableau suivant)

3.  Connecteurs pour les services Azure (connecteurs Bonjour tableau suivant)

4.  Scripts toocollect, puis les données de publication dans le journal Analytique (vides Bonjour tableau suivant et pour les services qui ne sont pas répertoriées)

| Service | Type de ressource | Journaux | Mesures | Solution |
| :------ | :------------ | :--- | :------ | :------- |
|Passerelles d’application|  Microsoft.Network/<br>applicationGateways|  Diagnostics|Diagnostics|    [Azure Application](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)[Gateway Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application Insights||     Connecteur|  Connecteur|  [Connecteur](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)[Application Insights (version préliminaire)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|Comptes Automation|   Microsoft.Automation/<br>AutomationAccounts|    Diagnostics||       [Plus d’informations](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Comptes Batch|    Microsoft.Batch/<br>batchAccounts|  Diagnostics|    Diagnostics||
|Services cloud classiques||       Storage||       [Plus d’informations](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Cognitive services|    Microsoft.CognitiveServices/<br>accounts|       Diagnostics|||
|Data Lake analytics|   Microsoft.DataLakeAnalytics/<br>accounts|   Diagnostics|||
|Data Lake Store|   Microsoft.DataLakeStore/<br>accounts|   Diagnostics|||
|Espace de noms Event Hub|   Microsoft.EventHub/<br>namespaces|  Diagnostics|    Diagnostics||
|IoT Hubs|  Microsoft.Devices/<br>IoTHubs||     Diagnostics||
|Key Vault| Microsoft.KeyVault/<br>vaults|  Diagnostics  || [KeyVault Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|Équilibreurs de charge|    Microsoft.Network/<br>loadBalancers|    Diagnostics|||
|Logic Apps|    Microsoft.Logic/<br>workflows|  Diagnostics|    Diagnostics||
||Microsoft.Logic/<br>integrationAccounts||||
|Groupes de sécurité réseau|   Microsoft.Network/<br>networksecuritygroups|Diagnostics||   [Azure Network Security Group Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|Coffres de récupération|   Microsoft.RecoveryServices/<br>vaults|||[Azure Recovery Services Analytics (version préliminaire)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Services de recherche|   Microsoft.Search/<br>searchServices|    Diagnostics|    Diagnostics||
|Espace de noms Service Bus| Microsoft.ServiceBus/<br>namespaces|    Diagnostics|Diagnostics|    [Service Bus Analytics (version préliminaire)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       Storage||    [Service Fabric Analytics (version préliminaire)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (v12)| Microsoft.Sql/<br>servers/<br>bases de données||       Diagnostics||
||Microsoft.Sql/<br>servers/<br>elasticPools||||
|Storage|||         Script| [Azure Storage Analytics (version préliminaire)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|Machines virtuelles|  Microsoft.Compute/<br>virtualMachines|  Extension|  Extension||
||||Diagnostics||
|Groupes de machines virtuelles identiques|   Microsoft.Compute/<br>virtualMachines    ||Diagnostics||
||Microsoft.Compute/<br>virtualMachineScaleSets/<br>virtualMachines||||
|Batteries de serveurs web|Microsoft.Web/<br>serverfarms||   Diagnostics
|Sites web| Microsoft.Web/<br>sites ||      Diagnostics|    [Plus d’informations](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>sites/<br>slots|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>Intégration des journaux avec les systèmes SIEM locaux
[Intégration d’Azure journal](https://www.microsoft.com/download/details.aspx?id=53324) vous permet de toointegrate les journaux brut à partir de vos ressources Azure tooyour locaux **systèmes d’informations sur la sécurité et de gestion des événements (SIEM)**.

![Intégration des journaux](./media/azure-log-audit/azure-log-audit-fig9.png)

L’intégration des journaux Azure collecte des diagnostics Azure à partir de vos machines virtuelles Windows (WAD), de journaux d’activité Azure, d’alertes Azure Security Center et de journaux du fournisseur de ressources Azure. Cette intégration offre un tableau de bord unifiée pour tous vos actifs, localement ou dans le cloud de hello, afin que vous pouvez agréger, mettre en corrélation, analyser et d’alerte pour les événements de sécurité.



L’intégration des journaux Azure prend actuellement en charge l’intégration des journaux d’activité Azure, du journal des événements Windows à partir des machines virtuelles Windows de votre abonnement Azure, des alertes Azure Security Center, des journaux de diagnostic Azure et des journaux d’audit Azure Active Directory.

| Type de journal | Log Analytics prenant en charge JSON (Splunk, ArcSight, Qradar) |
| :------- | :-------------------------------------------------------- |
|Journaux d’audit AAD|    Oui|
|Journaux d’activité| Oui|
|Alertes ASC |Oui|
|Journaux de diagnostic (journaux des ressources)|  Oui|
|Journaux des machines virtuelles|   Oui, via les événements transmis et non via JSON|


Hello tableau suivant explique catégorie hello du journal et les détails de l’intégration de SIEM.

[Prise en main de l’intégration des journaux Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started) : ce didacticiel vous guide dans la procédure d’installation de l’intégration des journaux Azure et d’intégration des journaux du stockage Azure WAD, des journaux d’activité Azure, des alertes Azure Security Center et des journaux d’audit Azure Active Directory.

Scénarios d’intégration

-   [Étapes de configuration du partenaire](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – ce billet de blog montre comment tooconfigure Azure du journal toowork d’intégration avec les solutions de partenaire Splunk, HP ArcSight et QRadar d’IBM.

-   [FAQ de l’intégration des journaux Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) : ce forum aux questions répond aux questions sur l’intégration des journaux Azure.

-   [Intégration de centre de sécurité les alertes avec Azure journal intégration](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) – ce document vous montre comment le centre de sécurité toosync des alertes, ainsi que des événements de sécurité d’ordinateur virtuel collectées par Diagnostics Azure et les journaux d’Audit Azure, avec votre analytique de journal ou Solution SIEM.

## <a name="next-steps"></a>Étapes suivantes

- [Audit et journalisation](https://www.microsoft.com/trustcenter/security/auditingandlogging)

Protéger les données par le maintien de la visibilité et réagir rapidement les alertes de sécurité tootimely

- [Collecte des journaux de sécurité et d’audit dans Azure](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/)

Les paramètres que vous devez toomake tooenforce que vos instances Azure collectez hello sécurité correctes et les journaux d’Audit.

- [Configurer les paramètres d’audit pour la collection de sites](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

Comme administrateur de collection de sites, un peut récupérer historique hello des actions effectuées par un utilisateur particulier et permettre également récupérer historique hello des actions effectuées pendant une plage de dates. 

- [Journal d’audit de hello des recherches dans Office 365 sécurité Bonjour centre de conformité](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Un permet hello Office 365 sécurité & centre de conformité toosearch hello d’audit unifiée journal tooview d’utilisateur et l’activité de l’administrateur de votre organisation à Office 365.


