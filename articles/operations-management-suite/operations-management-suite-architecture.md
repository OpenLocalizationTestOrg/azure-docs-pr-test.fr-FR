---
title: aaaOperations architecture de Management Suite (OMS) | Documents Microsoft
description: "Microsoft Operations Management Suite (OMS) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.  Cet article identifie hello différents services inclus dans OMS et fournit des liens tootheir détaillée le contenu."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>Architecture OMS
[Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) est un ensemble de services informatiques destinés à gérer vos environnements locaux et de cloud.  Cet article décrit hello différents locaux et cloud des composants d’OMS et leur architecture de calcul cloud niveau.  Vous pouvez consultez la documentation de toohello pour chaque service pour obtenir plus de détails.

## <a name="log-analytics"></a>Log Analytics
Toutes les données collectées par [Analytique de journal](https://azure.microsoft.com/documentation/services/log-analytics/) est stocké dans le référentiel d’OMS hello qui est hébergé dans Azure.  Sources connectées génèrent les données collectées dans le référentiel d’OMS hello.  Actuellement, trois types de sources connectées sont pris en charge.

* Installé un agent sur un [Windows](../log-analytics/log-analytics-windows-agents.md) ou [Linux](../log-analytics/log-analytics-linux-agents.md) ordinateur connecté directement tooOMS.
* Un groupe d’administration System Center Operations Manager (SCOM) [connecté tooLog Analytique](../log-analytics/log-analytics-om-agents.md) .  Agents SCOM continuent toocommunicate avec les serveurs d’administration qui transfèrent des événements et des données de performances tooLog Analytique.
* Un [compte de stockage Azure](../log-analytics/log-analytics-azure-storage.md) qui collecte les données [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) à partir d’un rôle de travail, d’un rôle Web ou d’une machine virtuelle dans Azure.

Sources de données définissent les données hello Analytique de journal de collecte à partir de sources connectées, y compris les journaux des événements et compteurs de performances.  Ajouter des fonctionnalités tooOMS de solutions et peuvent facilement être ajoutées tooyour espace de travail à partir de hello [galerie des Solutions OMS](../log-analytics/log-analytics-add-solutions.md).  Certaines solutions peuvent nécessiter une connexion directe de tooLog Analytique à partir des agents SCOM tandis que d’autres peuvent nécessiter une toobe supplémentaire de l’agent installé.

Analytique de journal a un portail web que vous pouvez utiliser les ressources d’OMS toomanage, ajouter et configurer des solutions d’OMS et afficher et analyser les données dans le référentiel d’OMS hello.

![Architecture Log Analytics haute performance](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Azure Automation
[Runbooks Azure Automation](http://azure.microsoft.com/documentation/services/automation) sont exécutés dans hello cloud Azure et peuvent accéder aux ressources qui se trouvent dans Azure ou dans d’autres services cloud, ou bien accessibles à partir de hello Internet public.  Vous pouvez également désigner des ordinateurs de votre centre de données local avec un [Runbook Worker hybride](../automation/automation-hybrid-runbook-worker.md), afin que les Runbooks puissent accéder aux ressources locales.

[Les configurations DSC](../automation/automation-dsc-overview.md) stockées dans Azure Automation peuvent être appliquées directement tooAzure des machines virtuelles.  Autres machines physiques et virtuelles peuvent demander des configurations de serveur de collecteur Azure Automation DSC hello.

Azure Automation dispose d’une solution OMS qui affiche des statistiques et des liens toolaunch hello portail Azure pour toutes les opérations.

![Architecture Azure Automation haute performance](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Azure Backup
Les données protégées dans [Azure Backup](http://azure.microsoft.com/documentation/services/backup) sont stockées dans un archivage de sauvegarde situé dans une zone géographique spécifique.  Hello sont répliquées dans hello même région et, en fonction de type hello de coffre, peuvent également être région tooanother répliquées pour assurer une redondance supplémentaire.

Dans Azure Backup, il existe trois scénarios fondamentaux.

* Une machine Windows avec un agent Azure Backup.  Ainsi, vous toobackup les fichiers et dossiers à partir de n’importe quel client ou un serveur Windows directement tooyour coffre de sauvegarde Azure.  
* System Center Data Protection Manager (DPM) ou Microsoft Azure Backup Server. Ainsi, vous tooleverage DPM ou Microsoft Azure Backup Server toobackup fichiers et dossiers en outre les charges de travail tooapplication telles que le stockage toolocal SQL et SharePoint et tooyour puis répliquer le coffre de sauvegarde Azure.
* Extensions de machine virtuelle Azure  Cela vous permet de tooyour de machines virtuelles toobackup coffre de sauvegarde Azure.

Azure Backup dispose d’une solution OMS qui affiche des statistiques et des liens toolaunch hello portail Azure pour toutes les opérations.

![Architecture Azure Backup haute performance](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) orchestre la réplication, le basculement et la restauration des machines virtuelles et des serveurs physiques. Les données de réplication sont échangées entre les hôtes Hyper-V, les hyperviseurs VMware et des serveurs physiques dans des centres de données principal et secondaire, ou entre un centre de données hello et le stockage Azure.  Site Recovery stocke les métadonnées dans des archivages situés dans une zone géographique Azure spécifique. Aucune donnée répliquée est stockée par hello service Site Recovery.

Dans Azure Site Recovery, il existe trois scénarios de réplication fondamentaux.

**La réplication de machines virtuelles Hyper-V**

* Si les ordinateurs virtuels Hyper-V sont gérées dans les clouds VMM, vous pouvez répliquer le stockage de tooAzure ou de centre de données secondaire tooa.  Réplication tooAzure est d’une connexion internet sécurisée.  Réplication tooa centre de données secondaire est hello LAN.
* Si les ordinateurs virtuels Hyper-V ne sont pas gérés par VMM, vous pouvez répliquer stockage tooAzure uniquement.  Réplication tooAzure est d’une connexion internet sécurisée.

**La réplication de machines virtuelles VMWare**

* Vous pouvez répliquer VMware virtual machines tooa centre de données secondaire exécutant VMware ou tooAzure de stockage.  TooAzure de réplication peut se produire sur un réseau VPN de site à site ou Azure ExpressRoute ou d’une connexion Internet sécurisée. Centre de données secondaire de tooa de réplication se produit sur hello le canal de données InMage Scout.

**La réplication de serveurs physiques Windows ou Linux** 

* Vous pouvez répliquer les serveurs physiques tooa secondaire datacenter ou tooAzure storage. TooAzure de réplication peut se produire sur un réseau VPN de site à site ou Azure ExpressRoute ou d’une connexion Internet sécurisée. Centre de données secondaire de tooa de réplication se produit sur hello le canal de données InMage Scout.  Azure Site Recovery dispose d’une solution OMS qui affiche certaines statistiques, mais vous devez utiliser hello portail Azure pour toutes les opérations.

![Architecture Azure Site Recovery haute performance](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* En savoir plus sur [Azure Automation](https://azure.microsoft.com/documentation/services/automation).
* En savoir plus sur [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* En savoir plus sur [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

