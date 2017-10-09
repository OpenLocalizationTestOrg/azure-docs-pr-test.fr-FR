---
title: "aaaAzure sécurité opérationnelle | Documents Microsoft"
description: "Découvrez Microsoft Operations Management Suite (OMS), ses services et son fonctionnement."
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
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Azure Operational Security
## <a name="introduction"></a>Introduction

### <a name="overview"></a>Vue d'ensemble
Nous savons que la sécurité est une tâche dans le cloud de hello et combien il est important que vous trouvez des informations précises et actuelles sur la sécurité Azure. Un des hello meilleures raisons toouse Azure pour vos applications et services est parti tootake de hello large gamme d’outils de sécurité et les fonctionnalités disponibles. Ces outils et les fonctions permettent de rendre des solutions sécurisées toocreate possible sur la plateforme Azure sécurisé de hello. Windows Azure doit assurer la confidentialité, l’intégrité et la disponibilité des données client, tout en permettant la gestion transparente des responsabilités.

toohelp clients mieux comprennent tableau hello des contrôles de sécurité implémenté dans Microsoft Azure à partir d’un client à la fois hello et perspectives opérationnelles de Microsoft, ce livre blanc, « Sécurité opérationnelle Azure », est écrit, qui fournit un vision détaillée de sécurité opérationnelle de hello disponible avec Windows Azure.

### <a name="azure-platform"></a>Plateforme Azure
Azure est une plateforme de services de cloud public qui prend en charge un large éventail de systèmes d’exploitation, de langages de programmation, d’infrastructures, d’outils, de bases de données et d’appareils. Elle permet d’exécuter des conteneurs Linux avec l’intégration de Docker, de créer des applications avec JavaScript, Python, .NET, PHP, Java et Node.js, de créer des serveurs principaux pour des appareils iOS, Android et Windows. Le service Cloud Azure prend en charge hello mêmes technologies des millions de développeurs et professionnels de l’informatique s’appuient sur déjà et faites confiance.

Lorsque vous générez sur ou migrez les ressources informatiques à, un fournisseur de services de cloud public vous recourez tooprotect des capacités de cette organisation vos applications et les données avec les contrôles de hello et les services de hello ils sécuriser toomanage hello de votre nuage ressources.

L’infrastructure Azure est conçu de tooapplications de fonctionnalité hello pour l’hébergement des millions de clients simultanément, et fournit une base digne de confiance sur lesquelles les entreprises capable de répondre aux impératifs de sécurité. En outre, Azure vous offre un large éventail de toocontrol de capacité hello et les options de sécurité configurables leur afin que vous pouvez personnaliser les exigences uniques de sécurité toomeet hello des déploiements de votre organisation. Ce document vous permettra de comprendre comment les fonctionnalités de sécurité d’Azure peuvent vous aider à répondre à ces besoins.

### <a name="abstract"></a>Résumé
Sécurité opérationnelle Azure fait référence toohello services, des contrôles et toousers disponibles de fonctionnalités pour protéger leurs données, les applications et les autres composants dans Microsoft Azure. Sécurité opérationnelle Azure repose sur une infrastructure qui intègre les connaissances hello acquises via différentes fonctionnalités qui sont tooMicrosoft unique, y compris hello Microsoft du cycle de vie SDL (Security Development), hello Microsoft Security Response Center programme et une connaissance approfondie du paysage des menaces inquiétudes hello.

Ce livre blanc décrit tooAzure d’approche de Microsoft sécurité opérationnelle au sein de la plateforme de cloud de Microsoft Azure hello et couvre suivant services :
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) est hello solution de gestion informatique pour cloud hybride de hello. Utilisée seule ou hello de tooextend votre déploiement de System Center existant, OMS vous donne une flexibilité maximale et contrôle pour la gestion de votre infrastructure cloud.

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

Avec OMS, vous pouvez gérer n’importe quelle instance dans n’importe quel cloud, notamment local, Azure, AWS, Windows Server, Linux, VMware et OpenStack, à moindre coût par rapport aux solutions concurrentes. Conçu pour le cloud en premier Bonjour, OMS offre une nouvelle toomanaging d’approche votre entreprise est hello plus rapide et plus économique toomeet nouveaux contrats défis et prendre en compte les nouvelles charges de travail, applications et les environnements de cloud.

### <a name="oms-services"></a>Services d’OMS

fonctionnalités principales de Hello d’OMS sont fournie par un ensemble de services qui s’exécutent dans Azure. Chaque service fournit une fonction de gestion spécifique, et vous pouvez combiner des scénarios de gestion de services tooachieve.

| Service  | Description|
| :------------- | :-------------|
| Log Analytics | Surveiller et analyser hello et performances des différentes ressources, y compris physiques et virtuels. |
|Automatisation | Automatisez des processus manuels et appliquez des configurations pour machines physiques et virtuelles. |
| Sauvegarde | Sauvegardez et restaurez les données critiques. |
| Site Recovery | Assurez la haute disponibilité des applications critiques. |

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) assure des services de surveillance pour OMS en collectant les données de ressources gérées et en les regroupant dans un référentiel central. Ces données peuvent inclure des événements, données de performances ou des données personnalisées fournies par le biais hello API. Une fois collectées, les données de salutation sont disponibles pour la génération d’alertes, analyse et l’exportation.


Cette méthode vous permet de tooconsolidate des données provenant de différentes sources, donc vous pouvez combiner des données à partir de vos services Azure avec votre environnement local. Elle sépare clairement collection hello de données de salutation à l’action de hello entreprise sur ces données afin que toutes les actions sont tooall disponibles les types de données.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

Hello service d’Analytique de journal gère vos données en nuage en toute sécurité à l’aide de hello méthodes suivantes :
-   ségrégation des données
-   conservation des données
-   sécurité physique
-   gestion des incidents
-   conformité
-   certifications relatives aux normes de sécurité

### <a name="azure-backup"></a>Sauvegarde Azure

[Sauvegarde Azure](http://azure.microsoft.com/documentation/services/backup) fournit des données de sauvegarde et restauration des services et fait partie de la suite d’OMS hello de produits et services.
Il protège les données de vos applications et les conserve des années durant, sans nécessiter aucun investissement en capital et moyennant des frais d’exploitation minimes. Il peut sauvegarder des données à partir des serveurs Windows physiques et virtuels en outre tooapplication les charges de travail telles que SQL Server et SharePoint. Il peut également être utilisé par [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate protégé tooAzure de données pour la redondance et de stockage à long terme.


Les données protégées dans le service Sauvegarde Azure sont stockées dans un archivage de sauvegarde situé dans une zone géographique spécifique. Hello sont répliquées dans hello même région et, en fonction de type hello de coffre, peut également être région tooanother répliquées pour assurer la résilience supplémentaire.

### <a name="management-solutions"></a>Solutions de gestion
[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.


Les [solutions de gestion](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) constituent des ensembles de logiques prépackagés qui implémentent un scénario de gestion spécifique utilisant un ou de plusieurs services OMS. Différentes solutions sont disponibles à partir de Microsoft et de partenaires que vous pouvez facilement ajouter valeur de hello tooincrease tooyour abonnement Azure de votre investissement dans OMS. En tant que partenaire, vous pouvez créer vos propres solutions toosupport vos applications et services et les fournir toousers via hello Azure Marketplace ou modèles de démarrage rapide.


![Solutions de gestion](./media/azure-operational-security/azure-operational-security-fig4.png)

Un bon exemple d’une solution qui utilise des fonctionnalités supplémentaires de plusieurs services tooprovide est hello [solution de gestion de la mise à jour](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management). Cette solution utilise hello [Analytique de journal](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) l’agent pour Windows et Linux toocollect plus d’informations sur les mises à jour requises sur chaque agent. Il écrit ce référentiel Analytique de journal de toohello de données où vous pouvez l’analyser avec un tableau de bord inclus.

Lorsque vous créez un déploiement, les runbooks dans [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) sont mises à jour utilisés tooinstall requis. Vous gérez tout ce processus dans le portail de hello et que vous n’avez pas besoin de tooworry sur les détails sous-jacents hello.

## <a name="azure-security-center"></a>Azure Security Center

Azure Security Center vous permet de protéger vos ressources Azure. Il fournit des fonctions intégrées de surveillance de la sécurité et de gestion des stratégies sur vos abonnements Azure. Dans le service de hello, vous ne pouvez toodefine stratégies non seulement par rapport à vos abonnements Azure, mais également contre [groupes de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups), de sorte que vous pouvez être plus précis.

### <a name="security-policies-and-recommendations"></a>Stratégies et recommandations de sécurité

Une stratégie de sécurité définit un jeu hello de contrôles, qui sont recommandés pour les ressources hello spécifié abonnement ou groupe de ressources.

Dans le centre de sécurité, vous définissez des stratégies en fonction de la société tooyour exigences de sécurité et de type hello d’applications ou de la sensibilité des données de salutation.

![Stratégies et recommandations de sécurité](./media/azure-operational-security/azure-operational-security-fig5.png)


Les stratégies sont activées dans le niveau d’abonnement hello automatiquement propager tooall des groupes de ressources au sein de l’abonnement de hello comme indiqué dans le diagramme hello sur hello droite :


### <a name="data-collection"></a>Collecte des données

Centre de sécurité collecte des données à partir de votre tooassess de machines virtuelles (VM) leur état de sécurité, fournir des recommandations de sécurité et vous alerter toothreats. Lorsque vous accédez à Azure Security Center pour la première fois, la collecte de données est activée sur toutes les machines virtuelles de votre abonnement. Collecte de données est recommandée, mais vous pouvez participer en désactivant la collecte de données dans hello stratégie du centre de sécurité.

### <a name="data-sources"></a>Sources de données

- Azure Security Center analyse les données de hello suivant la visibilité de tooprovide sources dans votre état de sécurité, identifier les failles et recommander des solutions d’atténuation et détecter les menaces actives :

-   Les Services Azure : Utilise les informations sur la configuration de hello des services Azure que vous avez déployé en communiquant avec le fournisseur de ressources du service.

- Trafic réseau : tire parti des métadonnées de trafic réseau échantillonnées provenant de l’infrastructure de Microsoft, telles que l’IP/le port source/de destination, la taille de paquet et le protocole réseau.

-   Solutions de partenaires : collecte les alertes de sécurité des solutions de partenaires intégrées, telles que les solutions de pare-feu et anti-programme malveillant.

-   Vos machines virtuelles : utilise les informations de configuration et les données relatives à des événements de sécurité, telles que des événements Windows et des journaux d’audit, des journaux IIS, des messages syslog et des fichiers de vidage sur incident, sur vos machines virtuelles.

### <a name="data-protection"></a>Protection des données

les clients toohelp empêchent, détectent et répondent toothreats, Azure Security Center collecte et traite les données relatives à la sécurité, y compris les informations de configuration, métadonnées, journaux des événements, les fichiers de vidage sur incident et bien plus encore. Microsoft respecte les instructions de sécurité et de conformité toostrict : du codage toooperating un service.

-   **La segmentation des données**: données sont maintenues séparées logiquement sur chaque composant dans le service de hello. Toutes les données sont balisées en fonction de l'organisation. Ce balisage est conservé tout au long du cycle de vie des données hello, et elle est appliquée à chaque couche de service de hello.

-   **Accès aux données**: recommandations de sécurité tooprovide et examiner les menaces de sécurité potentielles, technique de Microsoft peut accéder aux informations collectées ou analysés par des services Azure, y compris les fichiers de vidage sur incident, traiter les événements de création, disque de machine virtuelle les instantanés et les artefacts, qui peuvent inclure involontairement des données personnelles à vos machines virtuelles ou des données client. Nous respecter toohello [déclaration de confidentialité et les termes du contrat de Services en ligne Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), quel état qui n’est pas Microsoft utilise les données client ou dériver des informations à partir de celle-ci à des fins commerciales de publicité ou similaires.

-   **Utilisation des données**: Microsoft utilise des modèles et menaces vu sur plusieurs locataires tooenhance nos fonctions de détection et la prévention ; nous faire conformément aux engagements de confidentialité hello décrites dans nos [confidentialité Instruction](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).

### <a name="data-location"></a>Emplacement des données

Le Centre de sécurité Azure collecte des copies éphémères de vos fichiers de vidage sur incident et les analyse pour obtenir des preuves de tentatives d’attaque par le biais de code malveillant exploitant une faille de sécurité et de compromis ayant abouti. Centre de sécurité Azure effectue cette analyse dans hello même emplacement que hello d’espace de travail, et suppressions hello copies éphémères lors de l’analyse est terminée. Artefacts de l’ordinateur sont stockées de manière centralisée dans hello même région que hello de machine virtuelle.

-   **Vos comptes de stockage** : un compte de stockage est spécifié pour chaque région où des machines virtuelles fonctionnent. Cela permet de vous toostore données hello même région que l’ordinateur virtuel de hello à partir de quels hello les données sont collectées.

-   **Stockage du centre de sécurité Azure**: plus d’informations sur les alertes de sécurité, y compris l’état d’intégrité de la sécurité, des recommandations et des alertes de partenaire sont stockés centralisée, actuellement hello aux États-Unis. Ces informations peuvent inclure des informations de configuration connexes et les événements de sécurité collectés à vos machines virtuelles comme tooprovide nécessaire vous avec l’état d’intégrité hello sécurité alerte, recommandation ou la sécurité.


## <a name="azure-monitor"></a>Azure Monitor

Hello [sécurité OMS](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) et permet de solution d’Audit informatique tooactively surveiller toutes les ressources, ce qui peuvent aider à réduire l’impact de hello des incidents de sécurité. Cette solution possède des domaines de sécurité qui peuvent être utilisés pour la surveillance des ressources. domaine de sécurité Hello fournit un accès rapide toooptions, hello de surveillance de la sécurité pour les domaines suivants sont traités dans plus de détails :

-   Évaluation des logiciels malveillants
-   Update assessment (Évaluation des mises à jour)
-   Identité et accès.

Moniteur de Azure fournit des pointeurs tooinformation sur des types de ressources. Il offre la visualisation, requête, le routage, alertes, à l’échelle automatique et automation sur chaque ressource Azure (journaux de Diagnostic) et les données à partir de hello infrastructure Azure (journal d’activité).

![Azure Monitor](./media/azure-operational-security/azure-operational-security-fig6.png)


Les applications cloud sont complexes, et se composent de nombreux éléments mobiles. L’analyse fournit des données tooensure que votre application reste opérationnel et en cours d’exécution dans un état sain. Cela permet également vous toostave désactivé des problèmes potentiels ou de dépanner au-delà de celles.

En outre, vous pouvez utiliser l’analyse données toogain des informations détaillées relatives à votre application. Ces connaissances peuvent vous aider à tooimprove des performances des applications ou facilité de maintenance, ou automatiser des actions qui nécessiteraient sinon une intervention manuelle.

### <a name="azure-activity-log"></a>Journaux d’activité


Il s’agit d’un journal qui fournit des indications sur les opérations de hello qui ont été effectuées sur les ressources dans votre abonnement. Hello journal d’activité était précédemment appelé « Journaux d’Audit » ou « Journaux des opérations », dans la mesure où il signale les événements de panneau pour vos abonnements.

![Journaux d’activité](./media/azure-operational-security/azure-operational-security-fig7.png)

À l’aide de hello journal d’activité, vous pouvez déterminer hello », qui et à quel moment » pour toutes les opérations (PUT, POST, DELETE) effectuées sur les ressources hello dans votre abonnement d’écriture. Vous pouvez également comprendre état hello d’opération de hello et d’autres propriétés pertinentes. Hello journal d’activité n’inclut pas les opérations de (GET) en lecture ou de ressources qui utilisent le modèle classique de hello.

### <a name="azure-diagnostic-logs"></a>Journaux de diagnostic Azure

Ces journaux sont émis par une ressource et fournissent des données riches et fréquentes relatives au fonctionnement de hello d’une ressource. le contenu de ces journaux Hello varie selon le type de ressource.

Par exemple, les journaux des événements système Windows sont une catégorie de journal de diagnostic pour les machines virtuelles et les objets blob, les tables, et les journaux de file d’attente sont les catégories de journaux de diagnostic pour les comptes de stockage.

Les journaux de diagnostic diffèrent hello [journal d’activité (anciennement appelé journal d’Audit ou de journal des opérations)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). journal d’activité Hello fournit des indications sur les opérations de hello qui ont été effectuées sur les ressources dans votre abonnement. Les journaux de diagnostic fournissent des informations sur les opérations effectuées par votre ressource.

### <a name="metrics"></a>Mesures

Moniteur de Azure vous permet de tooconsume télémétrie toogain visibilité des performances de hello et de l’intégrité de vos charges de travail sur Azure. type le plus important de données de télémétrie Azure Hello est métriques hello (également appelés des compteurs de performances) est émis par les ressources Azure plus. Moniteur de Azure fournit plusieurs façons tooconfigure et consommez [métriques](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) pour la surveillance et la résolution des problèmes. Métriques sont une source précieuse de télémétrie et vous hello toodo tâches suivantes :

-   **Suivre les performances de hello** de votre ressource (par exemple, une application virtuelle, site Web ou logique) en traçant ses mesures sur un graphique de portail et l’épinglage de ce tableau de bord tooa graphique.

-   **Soyez averti d’un problème** qu’impacts hello les performances de votre ressource lorsqu’une métrique dépasse un certain seuil.

-   **Configurer des actions automatisées**, telles que la mise à l’échelle automatique d’une ressource ou le déclenchement d’un runbook lorsqu’une mesure dépasse un certain seuil.

-   **Effectuer des analyses avancées** ou créer des rapports sur les tendances de performances ou d’utilisation de vos ressources.

-   **Archive** hello l’historique des performances ou l’intégrité de votre ressource pour la conformité ou à des fins d’audit.

### <a name="azure-diagnostics"></a>Azure Diagnostics

Il s’agit de capacité hello dans Azure qui active la collecte de hello de données de diagnostic sur une application déployée. Vous pouvez utiliser l’extension de diagnostics hello provenant de différentes sources différentes. Les sources actuellement prises en charge sont les [rôles Web et les rôles de travail Azure Cloud Service](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/overview) sous Microsoft Windows et [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics). Les autres services Azure ont leurs propres diagnostics distincts.

## <a name="azure-network-watcher"></a>Azure Network Watcher

L’audit de sécurité de votre réseau est essentiel pour détecter ses vulnérabilités et assurer la conformité avec votre modèle de gouvernance réglementaire et de sécurité informatique. Avec l’affichage du groupe de sécurité, vous pouvez récupérer les règles du groupe de sécurité réseau et de sécurité hello configuré et hello des règles de sécurité efficace. Avec liste hello de règles, vous pouvez déterminer les ports hello qui sont ouvertes et évaluer les vulnérabilités du réseau.

[Observateur de réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) est un service régional qui vous permet de toomonitor et diagnostiquer des conditions à un niveau de réseau dans, vers et à partir d’Azure. Diagnostic de réseau et les outils de visualisation disponibles avec l’Observateur réseau vous aider à comprendre, de diagnostiquer et de mieux réseau de tooyour insights dans Azure. Ce service inclut la capture de paquets, le tronçon saut suivant, la vérification des flux IP, l’affichage de groupe de sécurité, les journaux de flux de groupe de sécurité réseau. Surveillance au niveau du scénario présente une fin tooend des ressources réseau dans l’analyse de ressource contraste tooindividual réseau.

![Azure Network Watcher](./media/azure-operational-security/azure-operational-security-fig8.png)

Observateur réseau a actuellement hello suivant de fonctionnalités :

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">Journaux d’audit</a>**-opérations effectuées dans le cadre de la configuration de hello des réseaux sont consignées. Ces journaux peuvent être consultées dans hello portail Azure ou récupérées à l’aide des outils de Microsoft, telles que Power BI ou des outils tiers. Journaux d’audit sont disponibles via le portail de hello, PowerShell, CLI et les API Rest. Pour plus d’informations sur les journaux d’audit, consultez la page Afficher les journaux d’activité pour auditer les actions sur les ressources. Les journaux d’audit sont disponibles pour les opérations effectuées sur toutes les ressources réseau.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">Vérification des flux IP</a>** - Vérifie si un paquet est autorisé ou refusé en fonction des paramètres de paquet des informations à 5 tuples de flux (adresse IP de destination, adresse IP source, port de destination, port source et protocole). Si les paquets hello sont refusée par un groupe de sécurité réseau, la règle de hello et le groupe de sécurité réseau refusé les paquets hello est retournée.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">Tronçon suivant</a>**  -détermine le saut suivant de hello pour les paquets routés Bonjour Azure Fabric de réseau, ce qui vous les itinéraires toodiagnose toute mauvaise configuration définie par l’utilisateur.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">Affichage de groupe de sécurité</a>**  -Obtient les règles de sécurité efficace et appliquées hello qui sont appliquées sur une machine virtuelle.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">Enregistrement de flux de groupe de sécurité réseau</a>**  -journaux de flux pour les groupes de sécurité réseau permettent de tootraffic connexes toocapture journaux qui sont autorisés ou refusés par des règles de sécurité hello dans le groupe de hello. flux de Hello est défini par une 5-tuple d’informations : l’adresse IP Source, adresse IP de Destination, Port Source, le Port de Destination et protocole.

## <a name="azure-storage-analytics"></a>Azure Storage Analytics

[Stockage Analytique](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) peut stocker des métriques qui incluent des données de la capacité et les statistiques groupées des transactions sur le service de stockage tooa de demandes. Les transactions sont déclarées au niveau opération hello API et au niveau de service de stockage hello, et la capacité est signalée au niveau de service de stockage hello. Les données de métriques peuvent être des tooanalyze utilisé d’utilisation de service de stockage, diagnostiquer les problèmes avec les demandes effectuées sur le service de stockage hello et les performances de hello tooimprove des applications qui utilisent un service.

[L’analyse du stockage Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) effectue la journalisation et fournit les données d’indicateurs de performance d’un compte de stockage. Vous pouvez utiliser cette tootrace des demandes de données, analyser les tendances d’utilisation et diagnostiquer les problèmes avec votre compte de stockage. Journalisation d’Analytique de stockage est disponible pour hello [services Blob, file d’attente et Table](https://docs.microsoft.com/azure/storage/storage-introduction). Stockage Analytique enregistre des informations détaillées sur le service de stockage tooa demandes réussies et ayant échoué.

Ces informations peuvent être utilisées toomonitor des requêtes individuelles et les problèmes de toodiagnose avec un service de stockage. Les demandes sont enregistrées sur la base du meilleur effort. Entrées de journal sont créées uniquement si des requêtes sont effectuées sur le point de terminaison de service hello. Pour exemple si un compte de stockage a l’activité dans son point de terminaison d’objet Blob, mais pas dans ses points de terminaison de file d’attente ou Table consigne uniquement se rapportant toohello service Blob est créé.

toouse Analytique de stockage, vous devez l’activer individuellement pour chaque service, vous souhaitez toomonitor. Vous pouvez l’activer dans hello [portail Azure](https://portal.azure.com/); pour plus d’informations, consultez [surveiller un compte de stockage Bonjour Azure portal](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Vous pouvez également activer Analytique de stockage par programme via l’API REST de hello ou de la bibliothèque cliente de hello. Utilisez hello Set Service Properties opération tooenable stockage Analytique individuellement pour chaque service.

données agrégées Hello sont stockées dans un objet blob connu (pour la journalisation) et dans des tables connues (pour les métriques), qui est accessible à l’aide des API du service de Table et de service d’objets Blob hello.

Analytique de stockage a une limite de 20 To montant hello des données stockées qui est indépendantes de la limite totale de hello pour votre compte de stockage. Tous les journaux sont stockés dans des objets [blob de blocs](https://docs.microsoft.com/azure/storage/storage-analytics) dans un conteneur nommé $logs, qui est automatiquement créé lorsque Storage Analytics est activé pour un compte de stockage.

Hello suit les actions effectuées par stockage Analytique est facturable :

-   Objets BLOB toocreate de demandes pour la journalisation
-   Entités de table demandes toocreate pour les mesures.

> [!Note]
> Pour plus d’informations sur les stratégies de facturation et de rétention de données, consultez la page [Storage Analytics and Billing](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing) (Storage Analytics et facturation).
> Pour des performances optimales, vous souhaitez toolimit hello de disques très utilisées associé toohello machine virtuelle tooavoid possible la limitation. Si tous les disques ne sont pas très utilisés à hello simultanément, compte de stockage hello peut prendre en charge un plus grand disque numéro.

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
## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD inclut également une suite complète de fonctionnalités de gestion d’identité, comme l’authentification multifacteur, l’inscription d’appareil, la gestion de mot de passe libre-service, la gestion de groupes libre-service, la gestion des comptes privilégiés, le contrôle d’accès en fonction du rôle, la surveillance de l’utilisation de l’application, ainsi que la création d’audits complets, la surveillance de la sécurité et la création d’alertes.

-   En améliorant la sécurité des applications grâce à l’authentification multifacteur et l’accès conditionnel Azure AD.

-   En surveillant l’utilisation des applications et en protégeant votre entreprise contre les menaces avancées, grâce à des fonctionnalités de création de rapports et de surveillance.

Azure Active Directory (Azure AD) comprend des rapports sur la sécurité, les activités et l’audit concernant votre annuaire. [Bonjour Azure Active Directory d’Audit rapport](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) permet aux clients les actions tooidentify privilégié qui s’est produite dans leur annuaire Active Directory de Azure. Des actions privilégiées incluent des modifications d’élévation (par exemple, la création de rôle ou les réinitialisations de mot de passe), la modification des configurations de stratégie (par exemple des stratégies de mot de passe), ou la configuration de toodirectory de modifications (par exemple, modifications toodomain paramètres de fédération).

Hello rapports fournissent un enregistrement d’audit de hello pour nom de l’événement hello, acteur hello qui a effectué l’action hello, les ressources de cible hello affectées par la modification de hello et hello date et heure (UTC). Les clients sont liste de hello tooretrieve en mesure d’événements d’audit pour leurs Azure Active Directory via hello [portail Azure](https://portal.azure.com/), comme décrit dans [afficher vos journaux d’Audit](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Voici une liste des rapports hello inclus :

| Rapports de sécurité  | Rapports d’activité| Rapport d’audit |
| :------------- | :-------------| :-------------|
|Connexions à partir de sources inconnues | Utilisation des applications : résumé | Rapport d’audit d’annuaire |
|Connexions après plusieurs échecs | Utilisation des applications : présentation détaillée |   |
|Connexions depuis plusieurs zones géographiques | Tableau de bord de l’application |  |
|Connexions depuis des adresses IP avec des activités suspectes |Erreurs de configuration de compte |  |
|Activité de connexion anormale |Appareils des utilisateur individuels |  |
|Connexions à partir d’appareils potentiellement infectés |Activité des utilisateurs individuels |   |
|Utilisateurs ayant une activité de connexion anormale |Rapport d'activité de groupes |   |
| |Rapport d’activité de l’enregistrement de la réinitialisation de mot de passe |   |
| |Activité de réinitialisation de mot de passe |   | |



données de Hello de ces rapports peuvent être des applications de tooyour utiles, telles que les systèmes SIEM, l’audit et les outils Business intelligence. Création de rapports Hello Azure AD [API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) fournissent des données de toohello l’accès par programme via un ensemble d’API REST. Vous pouvez appeler ces API à partir de divers outils et langages de programmation.

Événements dans les rapports d’Audit Azure AD de hello sont conservées pendant 180 jours.

> [!Note]
> Pour plus d’informations sur la rétention des rapports, consultez la page [Stratégies de rétention des rapports Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Pour les clients intéressés par le stockage leur [événements d’audit](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) de plus longues périodes de rétention, hello API Reporting peut être tooregularly utilisé extraire des événements d’audit dans un magasin de données distinct.

## <a name="summary"></a>Résumé

Cette résumés de l’article protéger votre vie privée et de sécuriser vos données, tout en proposant des logiciels et services qui vous aident à gérer hello infrastructure informatique de votre organisation. Microsoft a conscience que lorsqu’ils confient leur tooothers de données, cette confiance exige une sécurité rigoureuse. Microsoft respecte les instructions de sécurité et de conformité toostrict : du codage toooperating un service. La sécurisation et la protection des données constituent une priorité de premier plan pour Microsoft.

Cet article explique

-   Comment les données sont collectées, traitées et sécurisées de hello Operations Management Suite (OMS).

-   Comment analyser rapidement les événements de plusieurs sources de données. Identifier les risques de sécurité et de comprendre la portée de hello et l’impact des menaces et les attaques par des dommages hello toomitigate de violation de la sécurité.

-   Comment identifier les modèles d’attaque en visualisant le trafic IP malveillant sortant et les types de menaces malveillantes. Comprendre les défenses hello de tout votre environnement, quelle que soit la plateforme.

-   Capture toutes les données de journal et événement hello requises pour un audit de sécurité ou de conformité. Barre oblique hello temps et ressources nécessaires toosupply de l’audit de sécurité avec un exportable, complet et interrogeable journal et événement jeu de données.

<ul>
<li>Collecter les événements de sécurité, d’audit et l’analyse de violation tookeep une fermeture des yeux vos ressources :</li>
<ul>
<li>État de la sécurité</li>
<li>Problème important</li>
<li>Résumés des menaces</li>
</ul>
</ul>

## <a name="next-steps"></a>Étapes suivantes

- [Conception et sécurité opérationnelle](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft conçoit ses services et logiciels avec la sécurité en tenant compte toohelp Assurez-vous que son infrastructure cloud est résilient et définies contre les attaques.

- [Operations Management Suite | Security &amp; Compliance](https://www.microsoft.com/cloud-platform/security-and-compliance)

Utiliser Microsoft security analyse et les données tooperform plus intelligente et détection de menaces.

- [Opérations et la planification du centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) un ensemble d’étapes et les tâches que vous pouvez suivre toooptimize votre utilisation du centre de sécurité basée sur les exigences de sécurité de votre organisation et le modèle de gestion de cloud.

