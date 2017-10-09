---
title: "aaaOperations vue d’ensemble du Management Suite (OMS) | Documents Microsoft"
description: "Microsoft Operations Management Suite (OMS) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.  Cet article décrit la valeur hello d’OMS, identifie hello différents services et des offres incluses dans OMS et fournit des liens tootheir détaillée le contenu."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Présentation d’Operations Management Suite (OMS)
Cet article fournit une introduction de tooOperations Management Suite (OMS), y compris un bref aperçu de la valeur commerciale de hello il fournit, solutions de gestion et de services hello y et des offres de hello qui réunissent des différents services et solutions.  Liens toohello détaillées de la documentation sur le déploiement et à l’aide de chaque service et la solution.

## <a name="from-on-premises-toohello-cloud"></a>À partir du cloud de toohello local
Depuis longtemps déjà, Microsoft fournit des produits de gestion d’environnements d’entreprise.  Plusieurs produits ont été consolidées dans une suite de produits de gestion System Center de hello en 2007.  Cela inclus le Gestionnaire de Configuration qui fournit des fonctionnalités telles que la distribution de logiciels et d’inventaire, Operations Manager qui permet une analyse proactive des systèmes et applications, Orchestrator qui inclut des procédures opérationnelles tooautomate des processus manuels et Data Protection Manager pour la sauvegarde et récupération de données critiques.

Avec plus de ressources informatiques déplacement toohello cloud, les produits System Center acquise davantage de fonctionnalités cloud tels que Operations Manager et Orchestrator la gestion des ressources dans Azure.  Cependant, ils étaient toujours essentiellement conçus comme des solutions locales et nécessitaient un important investissement en matière de déploiement et d’administration d’un environnement de gestion local.  toocompletely tirer parti de cloud de hello et prend en charge les futures applications, un nouveau toomanagement d’approche était nécessaire.

## <a name="introducing-operations-management-suite"></a>Présentation d’Operations Management Suite
Operations Management Suite (également appelé OMS) est une collection de services de gestion qui ont été conçus dans le cloud hello du début de hello.  Plutôt que de déployer et de gérer des ressources locales, les composants OMS sont entièrement hébergés dans Azure.  OMS ne requiert qu’une configuration minime et vous permet d’être opérationnel en quelques minutes seulement.  

- **Coût minimal et facilité de déploiement.**  Étant donné que tous les composants de hello et des données pour OMS sont stockées dans Azure, possible en cours d’exécution dans une courte période sans la complexité de hello et placement dans locaux et sur les composants.
- **Niveaux de toocloud de mise à l’échelle.**  Vous n’avez pas tooworry sur le paiement des ressources de calcul que vous n’avez pas besoin ou sur manquer d’espace de stockage depuis hello cloud vous permet de toopay uniquement pour ce que vous réellement utilisez et mettra à l’échelle facilement charge tooany que vous avez besoin.  Vous pouvez commencer par la gestion de plusieurs ressources tooget démarré et ensuite évoluer tooyour ensemble de l’environnement.
- **Tirer parti des fonctionnalités les plus récentes hello.**  Les fonctionnalités des services d’OMS sont continuellement enrichies ou mises à jour.  Vous disposez en permanence toohello accès aux dernières fonctionnalités sans les mises à jour de toodeploy exigence.
- **Services intégrés.**  Chacun des services d’OMS hello offrent une valeur ajoutée significative sur leurs propres, ils peuvent travailler ensemble toosolve les scénarios de gestion complexes.  Par exemple, un runbook dans Azure Automation peut-être lecteur d’un processus de basculement avec Azure Site Recovery, puis informations tooLog Analytique toogenerate une alerte.
- **Application des connaissances recueillies au niveau mondial.**  Solutions de gestion d’OMS disposent en permanence accès toohello dernières informations.  Hello solution de sécurité et d’Audit par exemple, pouvez effectuer une analyse à l’aide de hello dernières menaces détectées monde hello.
- **Accessibilité en tout lieu.**  Accédez à votre environnement de gestion depuis tout emplacement où vous disposez d’un navigateur.  Installer hello OMS application sur votre téléphone intelligent pour les données d’analyse tooyour des accès.

### <a name="is-it-just-for-hello-cloud"></a>Il est seulement pour le cloud de hello ?
Le fait qu’OMS services s’exécutent dans cloud de hello ne signifie pas qu’ils ne peuvent pas gérer efficacement votre environnement local.  Place un agent sur toutes les fenêtres ou ordinateur Linux dans votre centre de données et il enverra tooLog données Analytique où il peut être analysé, ainsi que toutes les autres données collectées à partir des services de cloud ou localement.  Utiliser le cloud de hello tooleverage Azure Backup et Azure Site Recovery pour la sauvegarde et la haute disponibilité pour les ressources locales.  
Procédures opérationnelles dans le cloud de hello ne peut pas accéder en général de vos ressources locales, mais vous pouvez installer un agent sur un ou plusieurs ordinateurs trop qui hébergera les runbooks dans votre centre de données.  Lorsque vous démarrez un runbook, vous spécifiez simplement si vous souhaitez toorun dans le cloud de hello ou sur un thread de travail local.

## <a name="hybrid-management-with-system-center"></a>Gestion hybride avec System Center
Si vous avez une installation existante de System Center, vous pouvez intégrer ces composants OMS services tooprovide une solution hybride pour vos locaux et cloud environnements tirant parti des spécialisations de relatif hello de chaque produit.  Connectez votre Operations Manager management groupe tooLog Analytique tooanalyze géré agents existants dans le cloud de hello.  Utiliser votre processus de sauvegarde existants avec Data Protection Manager toobackup vos données toohello dans le cloud.  


## <a name="oms-services"></a>Services d’OMS
fonctionnalités principales de Hello d’OMS sont fournie par un ensemble de services qui s’exécutent dans Azure.  Chaque service fournit une fonction de gestion spécifique, et vous pouvez combiner des scénarios de gestion de services tooachieve.

|| Service | Description |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | Surveiller et analyser hello et performances des différentes ressources, y compris physiques et virtuels. |
| ![Azure Automation](media/operations-management-suite-overview/icon-automation.png) | Automatisation | Automatisez des processus manuels et appliquez des configurations pour machines physiques et virtuelles. |
| ![Azure Backup](media/operations-management-suite-overview/icon-backup.png) | Sauvegarde | Sauvegardez et restaurez les données critiques. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | Site Recovery | Assurez la haute disponibilité des applications critiques. |

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) assure des services de surveillance pour OMS en collectant les données de ressources gérées et en les regroupant dans un référentiel central.  Ces données peuvent inclure des événements, données de performances ou des données personnalisées fournies par le biais hello API. Une fois collectées, les données de salutation sont disponibles pour la génération d’alertes, analyse et l’exportation.  Cette méthode vous permet tooconsolidate des données à partir de diverses sources, donc vous pouvez combiner des données à partir de vos services Azure avec votre environnement local existant.  Elle sépare clairement collection hello de données de salutation à l’action de hello entreprise sur ces données afin que toutes les actions sont tooall disponibles les types de données.  

![Présentation de Log Analytics](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>Collecte de données
Il existe diverses façons dont vous pouvez obtenir des données dans le référentiel hello pour tooanalyze d’Analytique de journal.

- **Ordinateurs et machines virtuelles Windows ou Linux.**  Vous installez hello Microsoft Monitoring Agent sur [Windows](../log-analytics/log-analytics-windows-agents.md) et [Linux](../log-analytics/log-analytics-linux-agents.md) ordinateurs ou ordinateurs virtuels que vous souhaitez toocollect les données de.  l’agent de Hello téléchargera automatiquement à partir de la configuration Analytique de journal qui définit les événements et toocollect des données de performances.  Vous pouvez facilement installer l’agent de hello sur des ordinateurs virtuels en cours d’exécution dans Azure à l’aide de hello portail Azure.  Si vous avez un environnement Operations Manager existant, vous pouvez connecter tooLog de groupe d’administration hello Analytique et démarre automatiquement la collecte de données à partir de tous les agents existants.
- **Services Azure.**  Analytique de journal collecte une télémétrie de [Diagnostics Azure et surveillance Azure](../log-analytics/log-analytics-azure-storage.md) dans le référentiel de hello afin que vous puissiez surveiller les ressources Azure.
- **API Collecteur de données.**  Log Analytics comporte une [API REST assurant le remplissage de données issues de n’importe quel client](../log-analytics/log-analytics-data-collector-api.md).  Cela vous permet de toocollect des données depuis des applications tierces ou implémenter des scénarios de gestion personnalisées.  Une méthode courante est toouse un runbook dans les données de toocollect Azure Automation et ensuite utiliser hello API de collecteur de données toowrite il toohello référentiel.

#### <a name="reporting-and-analyzing-data"></a>Signalement et analyse de données
Analytique de journal inclut une requête puissantes langage tooextract les données stockées dans le référentiel de hello.  Étant donné que toutes les sources de données sont stockées sous forme d’enregistrements, vous pouvez analyser les données provenant de plusieurs sources dans une seule et même requête.
  
En outre, tooad hoc analysis, Analytique de journal fournit plusieurs façons tooreport et analyser les données à partir d’une requête.

- **Vues et tableaux de bord.**  [Vues](../log-analytics/log-analytics-view-designer.md) et [tableaux de bord](../log-analytics/log-analytics-dashboards.md) visualiser hello les résultats d’une requête dans le portail de hello.  Solutions de gestion inclut généralement les vues qui analysent les données de salutation à partir de la solution de hello.  Vous pouvez également créer vos propres affichages personnalisés tooanalyze données et les rendre disponibles dans votre portail personnalisé.
- **Exportation.**  Vous avez hello option tooexport hello des résultats de toute requête afin que vous pouvez les analyser en dehors de l’Analytique des journaux.  Vous pouvez même planifier une exportation régulière trop[Power BI](../log-analytics/log-analytics-powerbi.md) qui fournit des fonctions de visualisation et d’analyse.
- **API Recherche dans les journaux.**  Log Analytics comporte une [API REST assurant la collecte de données à partir de n’importe quel client](../log-analytics/log-analytics-log-search-api.md).  Cela vous permet de tooprogrammatically travail avec les données collectées dans le référentiel de hello ou à partir d’un autre outil d’analyse.

#### <a name="alerting"></a>Génération d’alertes
Lorsque le service Log Analytics détecte un problème, il peut vous [alerter de manière proactive](../log-analytics/log-analytics-alerts.md) ou prendre des mesures correctives.  Comme toutes les autres analyses de Log Analytics, cette opération est effectuée par le biais d’une recherche dans les journaux.  Cette recherche s’exécute selon une planification régulière, et une alerte est créée si les résultats de hello correspondent aux critères particuliers.

![Alertes Log Analytics](media/operations-management-suite-overview/overview-alerts.png)

En outre toocreating un enregistrement d’alerte dans le référentiel d’Analytique de journal hello, alertes peuvent prendre hello suivant des actions.

- **E-mail.**  Envoyer un courrier électronique tooproactively vous signale un problème détecté.
- **Runbook.**  Une alerte de Log Analytics peut démarrer un runbook dans Azure Automation.  En général, cela problème de tooattempt toocorrect hello détecté.  Hello runbook peut être démarré dans le cloud hello Bonjour cas d’un problème dans Azure ou un autre cloud ou il pu être démarré sur un agent local à un problème sur un ordinateur physique ou virtuel.
- **Webhook.**  Une alerte peut démarrer un webhook et transmettre des données à partir des résultats de recherche de journal hello hello.  Cela permet l’intégration avec les services externes, tel qu’un autre système d’alerte, ou il peut entreprendre une action corrective de tootake pour un site web externe.

### <a name="azure-automation"></a>Azure Automation
[Azure Automation](http://azure.microsoft.com/documentation/services/automation) fournit tooOMS de gestion automation et la configuration de processus.  Il automatise les processus manuels et permet des configurations tooenforce pour les ordinateurs physiques et virtuels.  

#### <a name="process-automation"></a>Automatisation de processus
Azure Automation automatise les processus manuels à l’aide de [runbooks](../automation/automation-runbook-types.md) qui reposent sur un script PowerShell ou un workflow PowerShell.  Il inclut également les ressources prenant en charge les procédures opérationnelles tels que des variables qui peuvent être partagées entre plusieurs runbooks et les informations d’identification et des connexions qui vous permettent d’informations toostore chiffré qui peuvent être nécessaire pour un runbook pour l’authentification.
Procédures opérationnelles offrent des autres services dans la suite de hello automatisation des processus pour hello.  Étant donné que chaque Hello autres services sont accessibles avec PowerShell ou via une API REST, vous pouvez créer runbooks tooperform fonctions telles que la collecte de données de gestion dans le journal Analytique ou lancer une sauvegarde avec Azure Backup.

##### <a name="accessing-resources"></a>Accès aux ressources
Étant donné que les runbooks reposent sur PowerShell, ils peuvent gérer n’importe quelle ressource accessible avec les applets de commande PowerShell.  Lorsque vous [charger un module](../automation/automation-integration-modules.md) dans votre compte Automation, elle devient runbooks tooall disponibles dans ce compte. 
 
Lorsque les runbooks s’exécutent dans le cloud de hello, ils peuvent accéder à toutes les ressources accessibles à partir du cloud de hello.  Il peut s’agir de ressources dans votre abonnement Azure, dans un autre cloud tel qu’Amazon Web Services (AWS), ou dans un service accessible par le biais d’une API REST.  Procédures opérationnelles dans le cloud de hello ne s’exécutent sous les informations d’identification, mais elles peuvent tirer parti des ressources Automation tels que les informations d’identification, les connexions et tooresources tooauthenticate de certificats qu'ils accèdent.

Ressources dans votre centre de données ne sont pas très probablement accessibles à partir d’un runbook en cours d’exécution dans le cloud de hello.  Vous pouvez installer un ou plusieurs [Workers hybrides](../automation/automation-hybrid-runbook-worker.md) dans vos données center cependant runbooks toorun nécessitant toolocal d’accéder aux ressources.  Lorsque vous démarrez un runbook, vous spécifiez si elle doit s’exécuter dans le cloud de hello ou un traitement spécifique.

![Runbooks Azure Automation](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Démarrage d'un runbook
Les runbooks peuvent être [démarrés par un certain nombre de méthodes](../automation/automation-starting-a-runbook.md) et donc être inclus dans divers scénarios de gestion.  

- **Portail Azure.**  Comme d’autres services Azure, Azure Automation peuvent être gérée à partir de hello portail Azure.  En outre toostarting runbooks, vous pouvez les importer ou créer votre propre.
- **Planification.**  Vous pouvez planifier les procédures opérationnelles toostart à intervalles réguliers.  Cela vous permet de tooautomatically répéter un processus de gestion régulière ou collecter des données tooLog Analytique.
- **PowerShell et API.**  Vous pouvez démarrer des runbook et passe les requis des informations sur les paramètres à partir d’une applet de commande PowerShell ou hello les API REST Azure Automation.  
- **Webhook.**  Un webhook peut être créé pour n’importe quel runbook qui lui permet de toobe démarré à partir des applications externes ou des sites web.
- **Alerte Log Analytics.**  Une alerte dans le journal Analytique peut démarrer automatiquement un problème de hello runbook tooattempt toocorrect identifié par l’alerte de hello.

#### <a name="configuration-management"></a>Gestion des configurations
[Configuration d’état souhaité (DSC) PowerShell](../automation/automation-dsc-overview.md) est une plateforme de gestion de Windows PowerShell qui vous permet de toodeploy et appliquer la configuration hello physique et les ordinateurs virtuels.  Azure Automation gère les configurations DSC et fournit un serveur collecteur dans le cloud de hello que les agents peuvent accéder les configurations tooretrieve requis.

![Azure Automation DSC](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Sauvegarde Azure et Azure Site Recovery
Azure Backup et Azure Site Recovery contribuent toobusiness la continuité des activités et récupération d’urgence.  Elles ont des fonctionnalités qui vous aident à tooensure que les applications restent disponibles lors de pannes se produisent et retournent les opérations de toonormal lorsque les systèmes reviennent en ligne.  Les deux services contribuent toohello objectifs de point de récupération (RPO) et les objectifs de temps de récupération (RTO) définis dans votre organisation. Votre RPO définit les limites acceptables hello dans lequel données n’est pas disponibles pendant la panne, et hello RTO limite hello laps de temps acceptable dans lequel un service ou une application n’est pas disponible pendant une panne.

#### <a name="azure-backup"></a>Sauvegarde Azure
Le service [Sauvegarde Azure](http://azure.microsoft.com/documentation/services/backup) fournit des services de sauvegarde et de restauration des données pour OMS.  Il protège les données de vos applications et les conserve des années durant, sans nécessiter aucun investissement en capital et moyennant des frais d’exploitation minimes.  Il peut sauvegarder les données à partir de serveurs Windows physiques et virtuels dans les charges de travail plus tooapplication telles que SQL Server et SharePoint.  Il peut également être utilisé par tooAzure de données de System Center Data Protection Manager (DPM) tooreplicate protégé pour la redondance et de stockage à long terme.

Les données protégées dans le service Sauvegarde Azure sont stockées dans un archivage de sauvegarde situé dans une zone géographique spécifique. Hello sont répliquées dans hello même région et, en fonction de type hello de coffre, peut également être région tooanother répliquées pour assurer la résilience supplémentaire.

Dans Azure Backup, il existe trois scénarios fondamentaux.

- **Machine Windows avec un agent Sauvegarde Azure.** Sauvegarder des fichiers et dossiers à partir de n’importe quel client ou un serveur Windows directement tooyour coffre de sauvegarde Azure.<br><br>![Machine Windows avec un agent Sauvegarde Backup](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center Data Protection Manager (DPM) ou serveur de sauvegarde Microsoft Azure.** Tirer parti de DPM Microsoft Azure Backup Server toobackup fichiers et dossiers ou dans les charges de travail plus tooapplication tels que le stockage toolocal SQL et SharePoint et sont ensuite répliquées tooyour coffre de sauvegarde Azure. Ce scénario prend en charge les machines virtuelles Windows et Linux sur Hyper-V ou VMware.<br><br>![System Center Data Protection Manager (DPM) ou serveur de sauvegarde Microsoft Azure](media/operations-management-suite-overview/overview-backup-02.png)
- **Extensions de machine virtuelle Azure.** Sauvegarde Windows ou Linux virtual machines dans Azure tooyour coffre de sauvegarde Azure.<br><br>![Extensions de machine virtuelle Azure](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) permet la continuité en coordonnant la réplication des locaux virtuels et tooAzure de machines physiques ou site secondaire de tooa. Si votre site principal est indisponible, vous basculez les emplacement secondaire toohello afin que les utilisateurs peuvent continuer de travailler et restauré lorsque systèmes tooworking de retour. 

Le service Azure Site Recovery assure la haute disponibilité des serveurs et des applications.  Il contribue tooyour continuité des activités et une stratégie de récupération d’urgence en coordonnant la réplication, le basculement et récupération des machines virtuelles de Hyper-V local, les machines virtuelles VMware et les serveurs Windows/Linux physiques. Vous pouvez répliquer le centre de données secondaire tooa machines ou étendre votre centre de données en les répliquant tooAzure. Site Recovery fournit également un basculement et une récupération des charges de travail en toute simplicité. Cette solution s’intègre avec des mécanismes de récupération d’urgence tels que SQL Server AlwaysOn et fournit des plans de récupération pour un basculement facile des charges de travail réparties sur plusieurs machines.

Dans Azure Site Recovery, il existe trois scénarios de réplication fondamentaux.

- **Réplication de machines virtuelles Hyper-V.**  Si les ordinateurs virtuels Hyper-V sont gérées dans les clouds VMM, vous pouvez répliquer le stockage de tooAzure ou de centre de données secondaire tooa. Réplication tooAzure est d’une connexion internet sécurisée. Réplication tooa centre de données secondaire est hello LAN.  Si les ordinateurs virtuels Hyper-V ne sont pas gérés par VMM, vous pouvez répliquer stockage tooAzure uniquement. Réplication tooAzure est d’une connexion internet sécurisée.<br><br>![La réplication de machines virtuelles Hyper-V](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **Réplication de machines virtuelles VMware.**  Vous pouvez répliquer VMware virtual machines tooa centre de données secondaire exécutant VMware ou tooAzure de stockage. TooAzure de réplication peut se produire sur un réseau VPN de site à site ou Azure ExpressRoute ou d’une connexion Internet sécurisée. Centre de données secondaire de tooa de réplication se produit sur hello le canal de données InMage Scout.<br><br>![Réplication de machines virtuelles VMware](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **Réplication de serveurs physiques Windows et Linux.**  Vous pouvez répliquer les serveurs physiques tooa secondaire datacenter ou tooAzure storage. TooAzure de réplication peut se produire sur un réseau VPN de site à site ou Azure ExpressRoute ou d’une connexion Internet sécurisée. Centre de données secondaire de tooa de réplication se produit sur hello le canal de données InMage Scout. Azure Site Recovery dispose d’une solution OMS qui affiche certaines statistiques, mais vous devez utiliser hello portail Azure pour toutes les opérations.<br><br>![La réplication de serveurs physiques Windows ou Linux](media/operations-management-suite-overview/overview-siterecovery-physical.png)


Site Recovery stocke les métadonnées dans des archivages situés dans une zone géographique Azure spécifique. Aucune donnée répliquée est stockée par hello service Site Recovery.

## <a name="management-solutions"></a>Solutions de gestion
Les [solutions de gestion](operations-management-suite-solutions.md) constituent des ensembles de logiques prépackagés qui implémentent un scénario de gestion spécifique tirant profit d’un ou de plusieurs services OMS.  Différentes solutions sont disponibles à partir de Microsoft et de partenaires que vous pouvez facilement ajouter valeur de hello tooincrease tooyour abonnement Azure de votre investissement dans OMS.  En tant que partenaire, vous pouvez créer vos propres solutions toosupport vos applications et services et les fournir toousers via hello Azure Marketplace ou modèles de démarrage rapide.

Un bon exemple d’une solution qui tire parti des fonctionnalités supplémentaires de plusieurs services tooprovide est hello [solution de gestion de la mise à jour](oms-solution-update-management.md).  Cette solution utilise l’agent de journal Analytique hello pour Windows et Linux toocollect plus d’informations sur les mises à jour requises sur chaque agent.  Il écrit ce référentiel Analytique de journal de toohello de données où vous pouvez l’analyser avec un tableau de bord inclus.  Lorsque vous créez un déploiement, procédures opérationnelles dans Azure Automation sont utilisés tooinstall requis des mises à jour.  Vous gérez tout ce processus dans le portail de hello et que vous n’avez pas besoin de tooworry sur les détails sous-jacents hello.

![Solution](media/operations-management-suite-overview/overview-solution.png)

La plupart des solutions peuvent effectuer une ou plusieurs des hello suivant des fonctions.

- Collecte d’informations supplémentaires.  Log Analytics collecte diverses données émanant des clients et des services, notamment les événements et les données de performances.  Une solution de gestion peut collecter des informations supplémentaires non disponibles à partir d’autres sources de données, généralement à l’aide de runbooks Azure Automation.
- Analyse supplémentaire des informations collectées.  Les solutions de gestion intègrent des tableaux de bord et des vues qui assurent l’analyse et la visualisation des données.  Ces recherches de journal précédent toopredefined lien qui vous permettent de toodrill dans hello des données détaillées.  Ils peuvent également effectuer des analyses sur les données qui sont déjà été recueillies dans le référentiel de hello, par exemple entre les événements de sécurité pour indiquer une menace pour la recherche.
- Ajout de fonctionnalités.  Certaines solutions fournies par Microsoft peuvent s’appuient sur les fonctions hello hello core tooprovide supplémentaire des fonctionnalités de services.  Par exemple, carte de service fournit son propre toodiscover console et mappe le serveur et les dépendances de processus en temps réel.
Les solutions sont régulièrement ajoutées tooOMS par Microsoft et partenaires, ce qui vous toocontinuously augmentent la valeur hello de votre investissement.  Vous pouvez parcourir et installer des solutions de Microsoft via hello catalogue des Solutions de portail d’OMS hello ou parcourir et installer des solutions de Microsoft et partenaire via hello Azure Marketplace de hello portail Azure.  

![Galerie de solutions](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* En savoir plus sur [Azure Automation](../automation/automation-intro.md).
* En savoir plus sur [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* En savoir plus sur [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).
* Découvrir hello [solutions disponibles](../log-analytics/log-analytics-add-solutions.md) dans les offres OMS hello. 

