---
title: "abonnement d’aaaAzure limites et quotas | Documents Microsoft"
description: Fournit une liste des abonnements Azure et des limites, quotas et contraintes de service habituels. Cela inclut des informations sur comment tooincrease limite ainsi que les valeurs maximales.
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a>Abonnement Azure et limites, quotas et contraintes de service
Ce document répertorie quelques-unes des limites de Microsoft Azure courants hello, qui sont également appelées quotas. Ce document ne couvre pas actuellement tous les services Azure. Au fil du temps, liste de hello sera développé et mis à jour toocover plus de plateforme de hello.

Visitez [vue d’ensemble de la tarification Azure](https://azure.microsoft.com/pricing/) toolearn plus d’informations sur la tarification Azure. Là, vous pouvez estimer les coûts à l’aide de hello [calculatrice de tarification](https://azure.microsoft.com/pricing/calculator/) ou en visitant la page de détails pour un service de tarification de hello (par exemple, [les machines virtuelles Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)). Pour obtenir des conseils toohelp gérer les coûts, consultez [empêcher les coûts inattendus avec la gestion des coûts et la facturation Azure](billing/billing-getting-started.md).

> [!NOTE]
> Si vous souhaitez limite de hello tooraise ou quota ci-dessus hello **par défaut de limite**, [ouvrir une demande de support technique en ligne sans frais](azure-supportability/resource-manager-core-quotas-request.md). Hello limites ne peuvent pas être déclenchés ci-dessus hello **limite maximale** valeur affichée dans les tableaux suivants de hello. S’il existe aucune **limite maximale** colonne, les ressources hello puis ne limites réglables. 
> 
> Les abonnements d’essai gratuit ne permettent pas de bénéficier d’augmentations de la limite ou du quota. Si vous avez une version d’évaluation gratuite, vous pouvez mettre à niveau tooa [paiement à l’utilisation](https://azure.microsoft.com/offers/ms-azr-0003p/) abonnement. Pour plus d’informations, consultez [mise à niveau d’évaluation gratuite Azure tooPay-sous-vous-Go](billing/billing-upgrade-azure-subscription.md).
> 

## <a name="limits-and-hello-azure-resource-manager"></a>Limites et hello Azure Resource Manager
Il est désormais possible toocombine plusieurs ressources Azure dans tooa un seul groupe de ressources Azure. Lorsque vous utilisez des groupes de ressources, les limites qu’une seule fois étaient globaux gérées au niveau régional avec hello Azure Resource Manager. Pour plus d’informations sur les groupes de ressources, consultez la [Vue d’ensemble d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md).

Dans les limites de hello ci-dessous, une nouvelle table a été ajouté tooreflect toutes les différences dans les limites lors de l’utilisation de hello Azure Resource Manager. Par exemple, vous disposez d’une table **Limites d’abonnement** et d’une table **Limites d’abonnement – Azure Resource Manager**. Lorsqu’une limite s’applique aux scénarios de tooboth, il ne s’affiche dans la première table de hello. Sauf indication contraire, les limites sont globales dans toutes les régions.

> [!NOTE]
> Il est important tooemphasize que les quotas pour les ressources dans les groupes de ressources Azure sont accessibles par votre abonnement par région et par abonnement, ne sont pas hello service Gestion des quotas sont. Nous allons utiliser des quotas de base à titre d'exemple. Si vous avez besoin d’un quota augmenter avec prise en charge des cœurs de toorequest, vous devez toodecide comment un nombre de cœurs souhaité toouse dans les différentes régions, puis effectuer une demande spécifique pour un groupe de ressources Azure de base quotas pour les zones que vous souhaitez et les montants de hello. Par conséquent, si vous avez besoin de toouse 30 cœurs dans Europe de l’ouest toorun votre application Vous devez spécifiquement demander 30 cœurs dans Europe de l’ouest. Mais vous n’avez pas un quota de cœurs augmenter dans n’importe quelle autre région--Europe de l’ouest uniquement aura un quota de cœur 30 hello.
> <!-- -->
> Par conséquent, il peut s’avérer utile tooconsider décider ce que les quotas de votre groupe de ressources Azure doivent toobe pour votre charge de travail dans une région et demande que le montant de chaque région dans laquelle vous envisagez de déploiement. Pour vous aider à découvrir vos quotas actuels pour des régions spécifiques, consultez la page [Dépannage de problèmes de déploiement](resource-manager-common-deployment-errors.md)
> 
> 

## <a name="service-specific-limits"></a>Limites de service spécifique
* [Active Directory](#active-directory-limits)
* [Gestion des API](#api-management-limits)
* [App Service](#app-service-limits)
* [Application Gateway](#application-gateway-limits)
* [Application Insights](#application-insights-limits)
* [Automation](#automation-limits)
* [Azure Cosmos DB](#azure-cosmos-db-limits)
* [Azure Event Grid](#azure-event-grid-limits)
* [Cache Redis Azure](#azure-redis-cache-limits)
* [Azure RemoteApp](#azure-remoteapp-limits)
* [Sauvegarde](#backup-limits)
* [Batch](#batch-limits)
* [BizTalk Services](#biztalk-services-limits)
* [CDN](#cdn-limits)
* [Cloud Services](#cloud-services-limits)
* [Container Instances](#container-instances-limits)
* [Data Factory](#data-factory-limits)
* [Data Lake Analytics](#data-lake-analytics-limits)
* [Data Lake Store](#data-lake-store-limits)
* [DNS](#dns-limits)
* [Concentrateurs d'événements](#event-hubs-limits)
* [IoT Hub](#iot-hub-limits)
* [Key Vault](#key-vault-limits)
* [Log Analytics / Operational Insights](#log-analytics-limits)
* [Media Services](#media-services-limits)
* [Mobile Engagement](#mobile-engagement-limits)
* [Mobile Services](#mobile-services-limits)
* [Surveiller](#monitor-limits)
* [Azure Multi-Factor Authentication](#multi-factor-authentication)
* [Mise en réseau](#networking-limits)
* [Network Watcher](#network-watcher-limits)
* [Service de hub de notification](#notification-hub-service-limits)
* [Groupe de ressources](#resource-group-limits)
* [Scheduler](#scheduler-limits)
* [action](#search-limits)
* [Service Bus](#service-bus-limits)
* [Site Recovery](#site-recovery-limits)
* [Base de données SQL](#sql-database-limits)
* [Stockage](#storage-limits)
* [Système StorSimple](#storsimple-system-limits)
* [Stream Analytics](#stream-analytics-limits)
* [Abonnement](#subscription-limits)
* [Traffic Manager](#traffic-manager-limits)
* [Machines virtuelles](#virtual-machines-limits)
* [Jeux de mise à l’échelle de machine virtuelle](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a>Limites d’abonnement
#### <a name="subscription-limits"></a>Limites d’abonnement
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a>Limites d’abonnement – Azure Resource Manager
Hello suivant limites s’appliquent lorsque vous utilisez hello Azure Resource Manager et les groupes de ressources Azure. Les limites qui n’ont pas changé avec hello Azure Resource Manager ne sont pas répertoriées ci-dessous. Pour ces limites, consultez le tableau précédent de toohello.

Pour plus d’informations sur la gestion des limites sur les demandes Resource Manager, consultez [Limitation des requêtes Resource Manager](resource-manager-request-limits.md).

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a>Limites de groupe de ressources
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a>Limites de machines virtuelles
#### <a name="virtual-machine-limits"></a>Limites de machine virtuelle
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a>Limites de machines virtuelles - Azure Resource Manager
Hello suivant limites s’appliquent lorsque vous utilisez hello Azure Resource Manager et les groupes de ressources Azure. Les limites qui n’ont pas changé avec hello Azure Resource Manager ne sont pas répertoriées ci-dessous. Pour ces limites, consultez le tableau précédent de toohello.

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a>Limites des jeux de mise à l’échelle de machine virtuelle
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a>Limites de Container Instances
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a>Limites de mise en réseau
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a>Limites de mise en réseau
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a>Limites d’Application Gateway
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a>Limites de Network Watcher
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a>Limites de Traffic Manager
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a>Limites de DNS
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a>Limites de stockage
Pour plus d'informations sur les limites des comptes de stockage, consultez [Objectifs de performance et d’extensibilité Azure Storage](storage/common/storage-scalability-targets.md).
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a>Limites de service de stockage
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a>Limites du nombre de disques de machine virtuelle 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

Pour plus d'informations, consultez [Tailles des machines virtuelles](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .

#### <a name="managed-virtual-machine-disks"></a>Disques de machines virtuelles gérées

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a>Disques de machines virtuelles non gérées

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a>Limites de fournisseur de ressources de stockage
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a>Limites de services cloud
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a>Limites App Service
suit Hello que du Service d’applications limite inclure des limites pour les applications Web, les applications mobiles, les applications API et Logic Apps.

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a>Limites de planificateur
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a>Limites Azure Batch
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a>Limites de BizTalk Services
Hello tableau suivant présente les limites de hello pour Azure Biztalk Services.

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a>Limites d’Azure Cosmos DB
Base de données Cosmos Azure est une base de données à l’échelle mondiale dans lequel le débit et le stockage peut être mis à l’échelle toohandle tout ce que votre application requiert. Si vous avez des questions sur l’échelle de hello fournit de la base de données Azure Cosmos, envoyez un courrier électronique tooaskcosmosdb@microsoft.com.

### <a name="mobile-engagement-limits"></a>Limites Mobile Engagement
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a>Limites Azure Search
Niveaux de tarification déterminent la capacité de hello et les limites de votre service de recherche. Les niveaux sont les suivants :

* *Gratuit* : service mutualisé, partagé avec d’autres abonnés Azure, destiné à des projets d’évaluation et de développement de petite taille.
* *Base* fournit des ressources de calcul dédiés pour les charges de production à une plus petite échelle, avec des réplicas toothree pour les charges de travail requête hautement disponible.
* *Standard (S1, S2, S3, S3 haute densité)* est approprié pour des charges de travail de production de plus grande taille. Plusieurs niveaux se trouvent au sein du niveau standard de hello afin que vous pouvez choisir une configuration de ressource qui correspond le mieux à votre profil de charge de travail.

**Limites par abonnement**

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

**Limites par service de recherche**

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

toolearn savoir plus sur les limites relatives à un niveau plus granulaire, telles que la taille du document, les requêtes par seconde, les clés, les demandes et réponses, consultez [Service limites dans Azure Search](search/search-limits-quotas-capacity.md).

### <a name="media-services-limits"></a>Limites de Media Services
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a>Limites de CDN
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a>Limites Mobile Services
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a>Limites de Monitor
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a>Limites du service Notification Hub
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a>Limites de concentrateurs d’événements
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a>Limites de Service Bus
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a>Limites de hub IoT (IoT Hub)
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a>Limites de Data Factory
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a>Limites Data Lake Analytics
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a>Limite Data Lake Store
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a>Limites Stream Analytics
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a>Limites d'Active Directory
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a>Limites d’Azure Event Grid
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a>Limites Azure RemoteApp
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a>Limites du système StorSimple
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a>Limites de Log Analytics
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a>Limites Azure Backup
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a>Limites Azure Site Recovery
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a>Limites d’Application Insights
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a>Limites Gestion des API
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a>Limite du service Cache Redis Azure
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a>Limites du coffre de clés
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a>Azure Multi-Factor Authentication
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a>Limites du service Automation
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a>Limites de base de données SQL
Pour connaître les limites de la base de données SQL, consultez [Limites de ressources de base de données SQL](sql-database/sql-database-resource-limits.md).

## <a name="see-also"></a>Voir aussi
[Présentation des limites et des augmentations Azure](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[Tailles de machines virtuelles et services cloud pour Microsoft Azure](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Tailles de services cloud](cloud-services/cloud-services-sizes-specs.md)

