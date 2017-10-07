---
title: aaaAzure Documentation Operations Management Suite (OMS) - didacticiels | Documents Microsoft
description: "Microsoft Operations Management Suite (OMS) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud. Cet article identifie hello différents services inclus dans OMS et fournit des liens tootheir détaillée le contenu."
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Présentation d’Operations Management Suite (OMS)
Microsoft Operations Management Suite (OMS) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.  La solution OMS étant implémentée sous la forme d’un service informatique, elle peut être opérationnelle rapidement, avec un investissement minimal dans des services d’infrastructure.  Les nouvelles fonctionnalités sont fournies automatiquement, ce qui vous permet d’économiser les coûts de mise à niveau et de maintenance.

En outre des services précieux tooproviding sur son propre, OMS peuvent intégrer des composants de System Center tels que System Center Operations Manager tooextend vos investissements de gestion existants dans le cloud de hello.  System Center et OMS peuvent travailler ensemble tooprovide expérience d’une gestion hybride complète.

Hello les sections suivantes fournit une description générale de hello différentes zones de valeur des services OMS et hello qui les implémentent.  Vous pouvez faire référence tooOMS architecture pour une vue d’ensemble des différents composants d’OMS hello avant révision hello détaillées de documentation de chacun.

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![Insight & Analytics](media/operations-management-suite-overview/icon-insight-analytics.png) Insight & Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) vous permet de collecter, corréler, rechercher et agir sur les données de journal et de performance générées par les applications et les systèmes d’exploitation. Elle vous donne des informations opérationnelles en temps réel à l’aide de la recherche intégrée et tableaux de bord personnalisés tooreadily analyse des millions d’enregistrements dans l’ensemble de vos charges de travail et les serveurs, quelle que soit leur emplacement physique.

Vous pouvez facilement ajouter des solutions tooLog Analytique qui définissent des toobe des données collectée et hello logique de leur analyse.  Les solutions peuvent inclure des fonctionnalités supplémentaires qui sont fournies automatiquement tooagents avec peu ou aucune configuration.  En outre les outils d’analyse toousing fournie par les différentes solutions, vous pouvez effectuer des recherches personnalisées sur le jeu de données complet de hello en données de commandes toocorrelate entre les systèmes et applications.  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![Automation & Control](media/operations-management-suite-overview/icon-automation-control.png) Automation & Control
Azure Automation automatise les processus administratifs avec [runbooks](../automation/automation-runbook-types.md) qui sont basés sur PowerShell et exécutez Bonjour cloud Azure.  Les Runbooks ont accès à tout produit ou service pouvant être géré avec PowerShell, y compris aux ressources situées dans d’autres clouds tels qu’Amazon Web Services (AWS).  Les runbooks peuvent également être exécutés sur un serveur dans votre ressources local toomanage de centre de données local.

Azure Automation assure la gestion de la configuration avec [PowerShell DSC](../automation/automation-dsc-overview.md).  Vous pouvez créer et gérer des ressources DSC hébergées dans Azure et les appliquer toodefine des systèmes locaux et toocloud et appliquer automatiquement leur configuration.

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![Protection et récupération](media/operations-management-suite-overview/icon-protection-recovery.png) Protection et récupération d’urgence
[Azure Backup](http://azure.microsoft.com/documentation/services/backup) protège les données de vos applications et les conserve des années, sans investissement en capital et avec des frais de fonctionnement minimaux.  Il peut sauvegarder les données à partir de serveurs Windows physiques et virtuels dans les charges de travail plus tooapplication telles que SQL Server et SharePoint.  Il peut également être utilisé par tooAzure de données de System Center Data Protection Manager (DPM) tooreplicate protégé pour la redondance et de stockage à long terme.

[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) contribue tooyour continuité des activités et une stratégie de récupération d’urgence en coordonnant la réplication, le basculement et récupération des machines virtuelles de Hyper-V sur site, les machines virtuelles VMware et Windows physique / Serveurs Linux. Vous pouvez répliquer le centre de données secondaire tooa machines ou étendre votre centre de données en les répliquant tooAzure. Site Recovery fournit également un basculement et une récupération des charges de travail en toute simplicité. Cette solution s’intègre avec des mécanismes de récupération d’urgence tels que SQL Server AlwaysOn et fournit des plans de récupération pour un basculement facile des charges de travail réparties sur plusieurs machines.

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![Sécurité et conformité d’OMS](media/operations-management-suite-overview/icon-security-compliance.png) Security and Compliance
Sécurité et conformité vous aide à identifier, évaluer et d’atténuer les risques de sécurité tooyour infrastructure.  Ces fonctionnalités d’OMS sont implémentées via plusieurs solutions en Analytique de journal qui analysent les données du journal et configuration à partir de l’agent systèmes tooassist dans hello de sécurité en cours de votre environnement.

* Hello [solution de sécurité et d’Audit](oms-security-getting-started.md) recueille et analyse les événements de sécurité sur une activité suspecte tooidentify les systèmes gérés.
* Hello [solution anti-programme malveillant](../log-analytics/log-analytics-malware.md) des rapports sur l’état de hello de protection contre les logiciels malveillants sur les systèmes gérés.  
* Hello solution des mises à jour système effectue une analyse des mises à jour de sécurité hello et d’autres mises à jour sur vos systèmes gérés afin que vous identifiiez facilement les systèmes nécessitant une mise à jour corrective.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* En savoir plus sur [Azure Automation](../automation/automation-intro.md).
* En savoir plus sur [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* En savoir plus sur [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

