---
title: "plateformes aaaSupported dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document fournit une liste des systèmes d’exploitation Windows et Linux pris en charge dans Azure Security Center."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: f73e04970749271fc9d75836f4f468b0a4953f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-platforms-in-azure-security-center"></a>Plateformes prises en charge dans Azure Security Center
Sécurité analyse de l’état et les recommandations sont disponibles pour les machines virtuelles (VM) créés à l’aide de hello classique et les modèles de déploiement de gestionnaire de ressources.

> [!NOTE]
> En savoir plus sur hello [classique et les modèles de déploiement Resource Manager](../azure-classic-rm.md) pour les ressources Azure.
>
>

## <a name="supported-platforms-for-windows-vms"></a>Plateformes prises en charge pour les machines virtuelles Windows
Systèmes d’exploitation Windows pris en charge :

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

> [!NOTE]
>
* Les évaluations de la vulnérabilité du système d’exploitation ne sont pas encore disponibles pour Windows Server 2016.
* Les détections d’analyse des incidents sont uniquement prises en charge pour Windows Server 2012 et Windows Server 2012 R2.
>
>

## <a name="supported-platforms-for-linux-vms"></a>Plateformes prises en charge pour les machines virtuelles Linux
Systèmes d’exploitation Linux pris en charge :

* Ubuntu versions 12.04, 14.04, 16.04, 16.10
* Debian versions 7 et 8
* CentOS versions 6.\* et 7.*
* Red Hat Enterprise Linux (RHEL) versions 6.\* et 7.*
* SUSE Linux Enterprise Server (SLES) versions 11 SP4+ et 12.*
* Oracle Linux versions 6.\*, 7.*

> [!NOTE]
> L’analytique comportementale de machine virtuelle n’est pas encore disponible pour les systèmes d’exploitation Linux.
>
>

## <a name="vms-and-cloud-services"></a>Machines virtuelles et services cloud
Les machines virtuelles en cours d’exécution dans un service cloud sont également prises en charge. Seuls les rôles de travail et web des services cloud en cours d’exécution dans des emplacements de production sont surveillés. toolearn en savoir plus sur le service cloud, consultez [vue d’ensemble des Services de cloud computing](../cloud-services/cloud-services-choose-me.md).

## <a name="next-steps"></a>Étapes suivantes

- [Azure Security Center Guide de planification et opérations](security-center-planning-and-operations-guide.md) — Découvrez comment tooplan et comprendre les considérations de conception hello tooadopt Azure Security Center
- [Alertes de sécurité par type dans Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-alerts-type.md#virtual-machine-behavioral-analysis) : en savoir plus sur l’analytique comportementale de machine virtuelle et l’analyse de mémoire de vidage sur incident dans Security Center
- [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche
- [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure
