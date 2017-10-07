---
title: "les charges de travail aaaWhat peuvent vous protéger avec Azure Site Recovery ?"
description: "Azure Site Recovery protège les charges de travail et les applications en coordonnant la réplication hello, le basculement et récupération des ordinateurs virtuels locaux et serveurs physiques tooAzure ou tooa secondaire sur-site local"
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
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Quelles charges de travail pouvez-vous protéger avec Azure Site Recovery ?
Cet article décrit les charges de travail et applications que vous pouvez répliquer avec hello service Azure Site Recovery.

Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="overview"></a>Vue d'ensemble
Les organisations doivent une continuité des activités et les charges de travail d’urgence (BCDR) de récupération stratégie tookeep et données sécurisées et disponibles pendant les temps morts planifiés et non planifiés et récupérer les conditions de travail tooregular dès que possible.

Récupération de site est un service Azure qui contribue de stratégie BCDR tooyour. À l’aide de la récupération de Site, vous pouvez déployer la réplication en fonction des applications toohello cloud ou site secondaire de tooa. Si vos applications sont Windows ou basés sur Linux, en cours d’exécution sur des serveurs physiques, VMware ou Hyper-V, vous pouvez utiliser la réplication tooorchestrate Site Recovery, effectuez un test de récupération d’urgence et exécuter des basculements et la restauration.

Site Recovery s’intègre avec les applications Microsoft, y compris SharePoint, Exchange, Dynamics, SQL Server et Active Directory. Par ailleurs, Microsoft travaille en étroite collaboration avec les principaux fournisseurs, notamment Oracle, SAP, IBM et Red Hat. Vous pouvez personnaliser les solutions de réplication application par application.

## <a name="why-use-site-recovery-for-application-replication"></a>Pourquoi utiliser Site Recovery pour la réplication des applications ?
Récupération de site contribue tooapplication au niveau de protection et récupération comme suit :

* Service indépendant de l’application qui assure la réplication de n’importe quelle charge de travail exécutée sur une machine prise en charge.
* Près de-de réplication synchrone, RPO aussi faible que les besoins de hello toomeet 30 secondes des applications métier critiques.
* Captures instantanées cohérentes de l’application pour les applications uniques ou multiniveau.
* Intégration avec SQL Server AlwaysOn et partenariat avec d’autres technologies de réplication au niveau des applications, y compris la réplication AD, SQL AlwaysOn, les groupes de disponibilité de base de données (DAG) Exchange et Oracle Data Guard.
* Plans de récupération flexible, qui toorecover une pile de l’ensemble de l’application d’un simple clic et d’incluent des scripts externes tooinclude et des actions manuelles dans le plan de hello.
* Gestion de réseau dans le Site Recovery et Azure toosimplify avancée spécifications de réseau des applications, notamment hello capacité tooreserve des adresses IP, configurer l’équilibrage de charge et l’intégration avec Azure Traffic Manager, pour basculements de réseau faibles RTO.
* Une bibliothèque d’automatisation avancée qui fournit des scripts spécifiques d’application prêts pour la production, qui peuvent être téléchargés et intégrés avec des plans de récupération.

## <a name="workload-summary"></a>Synthèse relative aux charges de travail
Site Recovery permet de répliquer n’importe quelle application exécutée sur une machine prise en charge. En outre, nous avons collaboré avec toocarry les équipes de produit des essais supplémentaires spécifiques de l’application.

| **Charge de travail** | **Site secondaire de répliquer des ordinateurs virtuels Hyper-V tooa** | **Répliquer des ordinateurs virtuels Hyper-V tooAzure** | **Répliquer le site secondaire de tooa les ordinateurs virtuels VMware** | **Répliquer des ordinateurs virtuels VMware tooAzure** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS |O |O |O |O |
| Applications web (IIS, SQL) |O |O |O |O |
| System Center Operations Manager |O |O |O |O |
| SharePoint |O |O |O |O |
| SAP<br/><br/>Répliquer tooAzure de site SAP pour non cluster |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |
| Microsoft Exchange (aucun DAG) |O |O |O |O |
| Bureau à distance/VDI |O |O |O |N/A |
| Linux (système d’exploitation et applications) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |
| Dynamics AX |O |O |O |O |
| Dynamics CRM |O |Bientôt disponible |O |Bientôt disponible |
| Oracle |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |O (opération testée par Microsoft) |
| Serveur de fichiers Windows |O |O |O |O |
| Citrix XenApp et XenDesktop |N/A |O |N/A |O |

## <a name="replicate-active-directory-and-dns"></a>Répliquer Active Directory et DNS
Une infrastructure Active Directory et DNS sont essentielles toomost les applications d’entreprise. Lors de la récupération d’urgence, vous devez tooprotect et restaurer ces composants d’infrastructure, avant la restauration de vos applications et charges de travail.

Vous pouvez utiliser la récupération de Site toocreate un plan de récupération après sinistre automatisée complète pour Active Directory et DNS. Par exemple, si vous souhaitez toofail par SharePoint et SAP à partir d’un site secondaire tooa principal, vous pouvez configurer un plan de récupération qui bascule de Active Directory tout d’abord, puis une supplémentaire spécifique à l’application un plan de récupération toofail sur hello toutes les applications qui s’appuient sur Active Répertoire.

[En savoir plus](site-recovery-active-directory.md) sur la protection d’Active Directory et DNS

## <a name="protect-sql-server"></a>Protéger SQL Server
SQL Server fournit une base pour les services de données pour de nombreuses applications professionnelles dans un centre de données local.  Récupération de site peut être utilisée avec les technologies SQL Server à haute disponibilité/récupération d’urgence, des applications d’entreprise de plusieurs niveaux tooprotect qui utilisent SQL Server. Site Recovery présente les caractéristiques suivantes :

* Solution de récupération d’urgence simple et économique pour SQL Server. Répliquer plusieurs versions et éditions de serveurs autonomes de SQL Server et les clusters, tooAzure ou tooa site secondaire.  
* Intégration avec les groupes de disponibilité AlwaysOn SQL, toomanage basculement et la restauration automatique avec les plans de récupération Azure Site Recovery.
* Plans de récupération de bout en bout pour hello tous les niveaux dans une application, y compris les bases de données SQL Server hello.
* Mise à l’échelle de SQL Server pour les charges maximales à l’aide de Site Recovery par « éclatement » en tailles de machines virtuelles IaaS plus volumineuses dans Azure.
* Test facile de récupération d’urgence de SQL Server. Vous pouvez exécuter des tests de basculement tooanalyze données et exécuter des vérifications de conformité, sans affecter votre environnement de production.

[En savoir plus](site-recovery-sql.md) sur la protection de SQL server.

## <a name="protect-sharepoint"></a>Protéger SharePoint
Azure Site Recovery vous aide à protéger vos déploiements SharePoint comme suit :

* Élimine le besoin de hello et les coûts d’infrastructure associés pour une batterie de secours pour la récupération d’urgence. Utilisez le Site Recovery tooreplicate un site de la batterie entière (niveaux Web et application de base de données) tooAzure ou tooa secondaire.
* Simplifie la gestion et le déploiement de l’application. Site de mises à jour déployées toohello principal sont automatiquement répliquées et sont donc disponible après le basculement et la récupération d’une batterie de serveurs dans un site secondaire. Réduit également la complexité de la gestion hello et les coûts associés à jour une batterie de secours.
* Simplifie le développement et le test d’applications SharePoint en créant un environnement de réplica de copie à la demande de type production pour le test et le débogage.
* Simplifie le cloud toohello de transition à l’aide de récupération de Site toomigrate SharePoint déploiements tooAzure.

[En savoir plus](site-recovery-sharepoint.md) sur la protection de SharePoint.

## <a name="protect-dynamics-ax"></a>Protéger Dynamics AX
Azure Site Recovery vous permet de protéger votre solution Dynamics AX ERP à travers :

* Coordonnant la réplication de votre environnement Dynamics AX (niveaux Web et AOS, niveaux de base de données, SharePoint) tooAzure, ou tooa un site secondaire.
* Ce qui simplifie la migration du cloud de toohello déploiements Dynamics AX (Azure).
* La simplification du développement et du test d’applications Dynamics AX en créant une copie de type production à la demande pour le test et le débogage.

[En savoir plus](site-recovery-dynamicsax.md) sur la protection de Dynamic AX.

## <a name="protect-rds"></a>Protéger les services Bureau à distance
Services Bureau à distance (RDS) permet infrastructure de bureau virtuel (VDI), les bureaux basés sur session et les applications, toowork les utilisateurs n’importe où. Avec Azure Site Recovery, vous pouvez :

* Répliquer des bureaux virtuels mis en pool gérés ou non gérés tooa du site secondaire et les applications et les sessions tooa site secondaire distant ou Azure.
* Voici ce que vous pouvez répliquer :

| **RDS** | **Site secondaire de répliquer des ordinateurs virtuels Hyper-V tooa** | **Répliquer des ordinateurs virtuels Hyper-V tooAzure** | **Répliquer le site secondaire de tooa les ordinateurs virtuels VMware** | **Répliquer des ordinateurs virtuels VMware tooAzure** | **Répliquer le site secondaire de serveurs physiques tooa** | **Répliquer les serveurs physiques tooAzure** |
| --- | --- | --- | --- | --- | --- | --- |
| **Bureau virtuel en pool (non géré)** |Oui |Non |Oui |Non |Oui |Non |
| **Bureau virtuel en pool (géré et sans UPD)** |Oui |Non |Oui |Non |Oui |Non |
| **Applications à distance et sessions de bureau (sans UPD)** |Oui |Oui |Oui |Oui |Oui |Oui |

[En savoir plus](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) sur la protection de RDS.

## <a name="protect-exchange"></a>Protéger Exchange
Site Recovery vous permet de protéger Exchange comme suit :

* Pour les petits déploiements Exchange, comme un serveur unique ou autonome, Site Recovery peut répliquer et basculer tooAzure ou tooa site secondaire.
* Pour les déploiements plus importants, Site Recovery s’intègre avec les groupes de disponibilité de base de données (DAG) Exchange.
* Exchange DAG sont hello recommandé de solution pour la récupération d’urgence Exchange dans une entreprise.  Plans de récupération de site peuvent inclure décisionnels, basculement tooorchestrate DAG entre sites.

[En savoir plus](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) sur la protection d’Exchange.

## <a name="protect-sap"></a>Protéger SAP
Utilisez Site Recovery tooprotect votre déploiement de SAP, comme suit :

* Activez la protection des applications SAP NetWeaver et NetWeaver non-production exécuté localement, en répliquant tooAzure de composants.
* Activez la protection des applications SAP NetWeaver et NetWeaver non-production Azure, en cours d’exécution en répliquant les composants tooanother centre de données Azure.
* Simplifier la migration de cloud, à l’aide de récupération de Site toomigrate votre tooAzure de déploiement de SAP.
* Simplifiez les mises à niveau, les tests et la création de prototypes du projet SAP, par la création d’un clone de production à la demande pour tester les applications SAP.

[En savoir plus](site-recovery-sap.md) sur la protection de SAP.

## <a name="protect-iis"></a>Protection IIS
Utilisez tooprotect de récupération de Site IIS est déployé, comme suit :

Azure Site Recovery assure la récupération d’urgence en répliquant les composants essentiels de hello dans votre site distant à froid environnement tooa ou un cloud public comme Microsoft Azure. Étant donné que la machine virtuelle hello hello web server et de la base de données hello soient répliquées toohello le site de récupération, il est sans les fichiers de configuration toobackup exigence ou des certificats séparément. Hello des mappages d’application et les liaisons en fonction de variables d’environnement qui sont modifiées après basculement peut être mis à jour à partir de scripts intégrés dans les plans de récupération d’urgence hello. Machines virtuelles sont appelés sur le site de récupération hello uniquement dans l’événement hello d’un basculement. Non seulement cette opération, Azure Site Recovery vous aide également à orchestrer hello fin tooend basculement en fournissant que vous hello suivant de fonctionnalités :

-   Séquencement hello l’arrêt et démarrage des machines virtuelles dans hello divers niveaux.
-   Ajout de mise à jour de scripts tooallow des liaisons et les dépendances des applications sur des machines virtuelles de hello après le démarrage. les scripts Hello peuvent également être site de récupération utilisé tooupdate hello DNS server toopoint toohello.
-   Allouer des adresses toovirtual machines pre-basculement IP en mappant les réseaux principaux et de restauration hello et utilisent donc les scripts qui ne doivent pas toobe mis à jour après basculement.
-   Possibilité pour un basculement d’un clic pour plusieurs applications web sur des serveurs web hello, éliminant ainsi étendue hello confusions dans les événements hello d’un incident.
-   Capacité tootest hello plans de récupération dans un environnement isolé pour les exercices de récupération d’urgence.

[En savoir plus](https://aka.ms/asr-iis) sur la protection de la batterie de serveurs web IIS.

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Protéger Citrix XenApp et XenDesktop
Utilisez Site Recovery tooprotect vos déploiements Citrix XenApp et XenDesktop, comme suit :

* Activer la protection de hello déploiement Citrix XenApp et XenDesktop, en répliquant de déploiement différentes couches notamment (serveur DNS Active Directory, SQL base de données serveur, le contrôleur de Citrix, StoreFront server, XenApp Master (VDA), serveur de licences Citrix XenApp) tooAzure.
* Simplifier la migration de cloud, à l’aide de récupération de Site toomigrate votre tooAzure déploiement Citrix XenApp et XenDesktop.
* Simplifiez le test de Citrix XenApp/XenDesktop en créant une copie de type production à la demande pour le test et le débogage.
* Cette solution est uniquement applicable pour les bureaux virtuels du système d’exploitation Windows Server, et non pour les bureaux virtuels client. En effet, ces derniers ne sont pas encore pris en charge pour la gestion des licences dans Azure.
[Apprenez-en plus](https://azure.microsoft.com/pricing/licensing-faq/) sur les licences pour les bureaux client/serveur dans Azure.

[Apprenez-en plus](site-recovery-citrix-xenapp-and-xendesktop.md) sur la protection des déploiements de Citrix XenApp et XenDesktop. Ou bien, vous pouvez faire référence hello [livre blanc de Citrix](https://aka.ms/citrix-xenapp-xendesktop-with-asr) détaillant hello identiques.

## <a name="next-steps"></a>Étapes suivantes
[Vérifiez les composants requis](site-recovery-prereq.md)
