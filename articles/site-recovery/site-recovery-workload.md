---
title: "Quelles charges de travail pouvez-vous protéger avec Azure Site Recovery ? | Microsoft Docs"
description: "Décrit les charges de travail qui peuvent être protégées à l’aide de la récupération d’urgence avec le service Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 12/15/2017
ms.author: raynew
ms.openlocfilehash: 03d311f84a4b9bc5f3a4c3c488ee7c84b1ef49ad
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2018
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Quelles charges de travail pouvez-vous protéger avec Azure Site Recovery ?

Cet article décrit les charges de travail et les applications que vous pouvez répliquer avec le service [Azure Site Recovery](site-recovery-overview.md).



## <a name="overview"></a>Vue d'ensemble

Les organisations ont besoin d’une stratégie de continuité des activités et de récupération d’urgence pour que les charges de travail et les données demeurent en sécurité et disponibles pendant les temps d’arrêt prévus et imprévus, et pour rétablir au plus vite des conditions de travail normales.

Site Recovery est un service Azure qui participe à votre stratégie de continuité des activités et de récupération d’urgence. À l’aide de Site Recovery, vous pouvez déployer une réplication compatible avec les applications vers le cloud ou un site secondaire. Qu’il s’agisse d’applications Windows ou Linux s’exécutant sur des serveurs physiques ou des machines virtuelles VMware ou Hyper-V, vous pouvez utiliser Site Recovery pour orchestrer la réplication, effectuer un test de récupération d’urgence et exécuter des opérations de basculement et de restauration automatique.

Site Recovery s’intègre à des applications Microsoft, notamment SharePoint, Exchange, Dynamics, SQL Server et Active Directory. Par ailleurs, Microsoft travaille en étroite collaboration avec les principaux fournisseurs, notamment Oracle, SAP et Red Hat. Vous pouvez personnaliser les solutions de réplication application par application.

## <a name="why-use-site-recovery-for-application-replication"></a>Pourquoi utiliser Site Recovery pour la réplication des applications ?

Site Recovery contribue à la protection des applications et à la récupération comme suit :

* Service indépendant de l’application qui assure la réplication de n’importe quelle charge de travail exécutée sur une machine prise en charge.
* Réplication presque synchrone avec des RPO de 30 secondes pour répondre aux besoins des applications professionnelles les plus critiques.
* Captures instantanées cohérentes de l’application pour les applications uniques ou multiniveau.
* Intégration avec SQL Server AlwaysOn et partenariat avec d’autres technologies de réplication au niveau des applications, y compris la réplication AD, SQL AlwaysOn, les groupes de disponibilité de base de données (DAG) Exchange et Oracle Data Guard.
* Plans de récupération flexibles qui vous permettent de récupérer une pile de l’application entière en un seul clic, et incluent les scripts externes et des actions manuelles.
* Gestion réseau avancée dans Site Recovery et Azure simplifiant la configuration réseau requise pour une application, notamment la réservation d’adresses IP, la configuration de l’équilibrage de charge et l’intégration avec Azure Traffic Manager pour les commutations réseau à RTO faible.
* Une bibliothèque d’automatisation avancée qui fournit des scripts spécifiques d’application prêts pour la production, qui peuvent être téléchargés et intégrés avec des plans de récupération.

## <a name="workload-summary"></a>Synthèse relative aux charges de travail
Site Recovery permet de répliquer n’importe quelle application exécutée sur une machine prise en charge. En outre, nous collaborons avec les équipes produit pour effectuer des tests supplémentaires propres à l’application.

| **Charge de travail** |**Réplication de machines virtuelles Azure dans Azure** |**Réplication de machines virtuelles Hyper-V vers un site secondaire** | **Réplication de machines virtuelles Hyper-V dans Azure** | **Réplication de machines virtuelles VMware vers un site secondaire** | **Réplication de machines virtuelles VMware dans Azure** |
| --- | --- | --- | --- | --- |---|
| Active Directory, DNS |O |O |O |O |O|
| Applications web (IIS, SQL) |O |O |O |O |O|
| System Center Operations Manager |O |O |O |O |O|
| SharePoint |O |O |O |O |O|
| SAP<br/><br/>Réplication d’un site SAP vers Microsoft Azure (aucun cluster) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft)|
| Microsoft Exchange (aucun DAG) |O |O |O |O |O|
| Bureau à distance/VDI |O |O |O |O |O|
| Linux (système d’exploitation et applications) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft)|
| Dynamics AX |O |O |O |O |O|
| Oracle |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft)|
| Serveur de fichiers Windows |O |O |O |O |O|
| Citrix XenApp et XenDesktop |O|Non applicable |O |Non applicable |O |

## <a name="replicate-active-directory-and-dns"></a>Répliquer Active Directory et DNS
Une infrastructure DNS et Active Directory sont essentiels pour la plupart des applications d’entreprise. Dans le cadre d’une récupération d’urgence, vous devez protéger et récupérer ces composants d’infrastructure avant de récupérer vos charges de travail et applications.

À l’aide de Site Recovery, vous pouvez créer un plan de récupération d’urgence automatisé complet pour Active Directory et DNS. Par exemple, si vous souhaitez basculer SharePoint et SAP d’un site principal vers un site secondaire, vous pouvez configurer un plan de récupération qui bascule Active Directory dans un premier temps, puis un plan de récupération spécifique à l’application supplémentaire pour le basculement des autres applications reposant sur Active Directory.

[En savoir plus](site-recovery-active-directory.md) sur la protection d’Active Directory et DNS

## <a name="protect-sql-server"></a>Protéger SQL Server
SQL Server fournit une base pour les services de données pour de nombreuses applications professionnelles dans un centre de données local.  Site Recovery peut être utilisé avec les technologies SQL Server HA/DR pour protéger les applications d’entreprise multiniveau faisant appel à SQL Server. Site Recovery présente les caractéristiques suivantes :

* Solution de récupération d’urgence simple et économique pour SQL Server. Réplication de plusieurs versions et éditions de serveurs et clusters autonomes SQL Server vers Azure ou un site secondaire.  
* Intégration avec les groupes de disponibilité SQL AlwaysOn pour gérer le basculement et la restauration automatique avec les plans de récupération Azure Site Recovery.
* Plans de récupération de bout en bout pour tous les niveaux d’une application, y compris les bases de données SQL Server.
* Mise à l’échelle de SQL Server pour les charges maximales à l’aide de Site Recovery par « éclatement » en tailles de machines virtuelles IaaS plus volumineuses dans Azure.
* Test facile de récupération d’urgence de SQL Server. Vous pouvez effectuer des basculements tests pour l’analyse et les vérifications de conformité des données, sans impact sur votre environnement de production.

[En savoir plus](site-recovery-sql.md) sur la protection de SQL server.

## <a name="protect-sharepoint"></a>Protéger SharePoint
Azure Site Recovery vous aide à protéger vos déploiements SharePoint comme suit :

* Élimine le besoin et les coûts de l’infrastructure associée à une batterie de secours pour la récupération d’urgence. Utilisez Site Recovery, pour répliquer la protection de la batterie entière (niveaux web, application et base de données) sur Azure ou sur un site secondaire.
* Simplifie la gestion et le déploiement de l’application. Les mises à jour déployées sur le site principal sont automatiquement répliquées et disponibles après le basculement et la récupération d’une batterie de serveurs sur un site secondaire. Cela réduit également la complexité de gestion et les coûts associés au maintien d’une batterie de secours à jour.
* Simplifie le développement et le test d’applications SharePoint en créant un environnement de réplica de copie à la demande de type production pour le test et le débogage.
* Simplifie la transition vers le cloud en utilisant Site Recovery pour migrer les déploiements SharePoint vers Azure.

[En savoir plus](site-recovery-sharepoint.md) sur la protection de SharePoint.

## <a name="protect-dynamics-ax"></a>Protéger Dynamics AX
Azure Site Recovery vous permet de protéger votre solution Dynamics AX ERP à travers :

* L’orchestration de la réplication de l’ensemble de votre environnement Dynamics AX (niveaux web et AOS, niveaux bases de données, SharePoint) sur Azure ou sur un site secondaire.
* La simplification de la migration des déploiements de Dynamics AX dans le cloud (Azure).
* La simplification du développement et du test d’applications Dynamics AX en créant une copie de type production à la demande pour le test et le débogage.

[En savoir plus](site-recovery-dynamicsax.md) sur la protection de Dynamic AX.

## <a name="protect-rds"></a>Protéger les services Bureau à distance
RDS active l’infrastructure de bureau virtuel (VDI), les bureaux basés sur session et les applications, permettant aux utilisateurs de travailler n’importe où. Avec Azure Site Recovery, vous pouvez :

* Répliquer des bureaux virtuels en pool gérés ou non gérés sur un site secondaire, ainsi que des applications et des sessions à distance sur un site secondaire ou sur Azure.

* Voici ce que vous pouvez répliquer :

| **RDS** |**Réplication de machines virtuelles Azure dans Azure** | **Réplication de machines virtuelles Hyper-V vers un site secondaire** | **Réplication de machines virtuelles Hyper-V dans Azure** | **Réplication de machines virtuelles VMware vers un site secondaire** | **Réplication de machines virtuelles VMware dans Azure** | **Réplication de serveurs physiques vers un site secondaire** | **Répliquer des serveurs physiques dans Azure** |
|---| --- | --- | --- | --- | --- | --- | --- |
| **Bureau virtuel en pool (non géré)** |Non |Oui |Non  |Oui |Non  |Oui |Non  |
| **Bureau virtuel en pool (géré et sans UPD)** |Non |Oui |Non  |Oui |Non  |Oui |Non  |
| **Applications à distance et sessions de bureau (sans UPD)** |Oui|Oui |Oui |Oui |Oui |Oui |Oui |

[Configurez la récupération d’urgence de RDS à l’aide d’Azure Site Recovery](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-disaster-recovery-with-azure).

[En savoir plus](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) sur la protection de RDS.

## <a name="protect-exchange"></a>Protéger Exchange
Site Recovery vous permet de protéger Exchange comme suit :

* Site Recovery peut répliquer et basculer les déploiements Exchange de petite taille, par exemple des serveurs uniques ou autonomes, vers Azure ou un site secondaire.
* Pour les déploiements plus importants, Site Recovery s’intègre avec les groupes de disponibilité de base de données (DAG) Exchange.
* Les groupes de disponibilité de base de données (DAG) Exchange sont la solution recommandée pour la récupération d’urgence Exchange dans une entreprise.  Les plans de récupération Site Recovery peuvent inclure des groupes de disponibilité de base de données (DAG) pour orchestrer le basculement de ceux-ci entre les sites.

[En savoir plus](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) sur la protection d’Exchange.

## <a name="protect-sap"></a>Protéger SAP
Utilisez Site Recovery pour protéger votre déploiement SAP comme suit :

* Activez la protection des applications de production SAP NetWeaver et non-NetWeaver exécutées localement, par la réplication des composants sur Azure.
* Activez la protection des applications de production SAP NetWeaver et non-NetWeaver exécutant Azure, par la réplication des composants sur un autre centre de données Azure.
* Simplifiez la migration vers le cloud en utilisant Site Recovery pour migrer votre déploiement SAP vers Azure.
* Simplifiez les mises à niveau, les tests et la création de prototypes du projet SAP, par la création d’un clone de production à la demande pour tester les applications SAP.

[En savoir plus](site-recovery-sap.md) sur la protection de SAP.

## <a name="protect-iis"></a>Protection IIS
Utilisez Site Recovery pour protéger votre déploiement IIS comme suit :

Azure Site Recovery assure la récupération d’urgence en répliquant les composants critiques de votre environnement vers un site distant à froid ou un cloud public comme Microsoft Azure. Étant donné que les machines virtuelles avec le serveur web et la base de données sont répliquées vers le site de récupération, il n’est pas obligatoire de sauvegarder séparément les certificats ou les fichiers de configuration. Les mappages et les liaisons d’application dépendant des variables d’environnement modifiées post-basculement peuvent être mis à jour via des scripts intégrés dans les plans de récupération d’urgence. Les machines virtuelles sont montées sur le site de récupération uniquement en cas de basculement. Azure Site Recovery vous aide également à orchestrer le basculement de bout en bout en mettant à disposition les fonctionnalités suivantes :

-   Séquencement de l’arrêt et du démarrage des machines virtuelles dans les différents niveaux.
-   Ajout de scripts pour autoriser la mise à jour des liaisons et des dépendances d’applications sur les machines virtuelles après le démarrage. Les scripts peuvent également être utilisés pour mettre à jour le serveur DNS pour pointer vers le site de récupération.
-   Allouez des adresses IP aux machines virtuelles pré-basculement en mappant les réseaux principaux et de récupération et, par conséquent, utilisez des scripts qui ne nécessitent pas de mise à jour post-basculement.
-   Possibilité de basculement en un clic pour plusieurs applications web sur les serveurs web, limitant ainsi la confusion en cas de sinistre.
-   Possibilité de tester les plans de récupération dans un environnement isolé pour les exercices de récupération d’urgence.

[En savoir plus](https://aka.ms/asr-iis) sur la protection de la batterie de serveurs web IIS.

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Protéger Citrix XenApp et XenDesktop
Site Recovery permet de protéger vos déploiements Citrix XenApp XenDesktop, comme suit :

* Protégez votre déploiement Citrix XenApp et XenDesktop en répliquant différentes couches de déploiement (serveur DNS Active Directory, serveur de base de données SQL, Citrix Delivery Controller, serveur StoreFront, XenApp Master (VDA), serveur de licences de Citrix XenApp) sur Azure.
* Simplifiez la migration vers le cloud en utilisant Site Recovery pour migrer votre déploiement Citrix XenApp et XenDesktop sur Azure.
* Simplifiez le test de Citrix XenApp/XenDesktop en créant une copie de type production à la demande pour le test et le débogage.
* Cette solution est uniquement applicable pour les bureaux virtuels du système d’exploitation Windows Server, et non pour les bureaux virtuels client. En effet, ces derniers ne sont pas encore pris en charge pour la gestion des licences dans Azure.
[Apprenez-en plus](https://azure.microsoft.com/pricing/licensing-faq/) sur les licences pour les bureaux client/serveur dans Azure.

[Apprenez-en plus](site-recovery-citrix-xenapp-and-xendesktop.md) sur la protection des déploiements de Citrix XenApp et XenDesktop. Vous pouvez également consulter le [livre blanc de Citrix](https://aka.ms/citrix-xenapp-xendesktop-with-asr) détaillant les mêmes informations.

## <a name="next-steps"></a>étapes suivantes

[Prise en main](azure-to-azure-quickstart.md) de la réplication d’une machine virtuelle Azure.
