---
title: "outils d’aaaCommunity - déplacer les ressources classiques tooAzure Gestionnaire de ressources | Documents Microsoft"
description: "Cet outils hello de catalogues article qui ont été fournis par hello Communauté toohelp migrer les ressources IaaS à partir du modèle de déploiement d’Azure Resource Manager toohello classique."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a>Communauté Outils ressources IaaS toomigrate classique tooAzure Gestionnaire de ressources
Cet article catalogues hello les outils qui ont été fournis par hello Communauté tooassist avec la migration des ressources IaaS à partir du modèle de déploiement d’Azure Resource Manager toohello classique.

> [!NOTE]
> Ces outils ne sont pas pris en charge officiellement par le Support Microsoft. Par conséquent, ils sont open source sur GitHub et nous sommes réservations persistantes de tooaccept heureux de correctifs ou des scénarios supplémentaires. tooreport un problème, utilisez hello GitHub problèmes de fonctionnalité.
> 
> Une migration avec ces outils entraînera un temps d’arrêt pour votre machine virtuelle Classic. Si vous souhaitez effectuer une migration prise en charge par la plateforme, consultez les articles suivants : 
> 
>   * [Plateforme prise en charge la migration des ressources IaaS à partir de la pile de Resource Manager tooAzure classique](migration-classic-resource-manager-overview.md)
>   * [Techniques détaillées sur la plateforme prise en charge la migration à partir de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-deep-dive.md)
>   * [Migrer les ressources IaaS classique tooAzure Gestionnaire de ressources à l’aide d’Azure PowerShell](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a>AsmMetadataParser
Il s’agit d’un ensemble d’outils d’assistance créé dans le cadre de migrations d’entreprise à partir de la gestion des services Azure tooAzure Gestionnaire de ressources. Cet outil vous permet de tooreplicate votre infrastructure dans un autre abonnement qui peut être utilisé pour vérifier la migration et tous les points de fer avant d’exécuter la migration hello sur votre abonnement de Production.

[Documentation de l’outil lien toohello](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a>migAz
migAz est une option supplémentaire de toomigrate un ensemble complet de ressources de Resource Manager IaaS tooAzure de ressources IaaS classiques. Hello migration peut se produire dans hello même abonnement ou entre différents abonnements et les types d’abonnements (ex : les abonnements CSP).

[Documentation de l’outil lien toohello](https://github.com/Azure/migAz)

## <a name="next-steps"></a>Étapes suivantes

* [Vue d’ensemble de la plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utiliser les ressources IaaS PowerShell toomigrate classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utiliser les ressources IaaS CLI toomigrate classique tooAzure Gestionnaire de ressources](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Passer en revue les erreurs courantes de migration](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Hello de révision plus Forum aux questions sur la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

