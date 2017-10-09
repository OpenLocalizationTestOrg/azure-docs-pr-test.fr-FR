---
title: "toodo aaaWhat dans les cas de hello d’une interruption de service Azure qui a un impact sur les Services de cloud computing de Azure | Documents Microsoft"
description: "Découvrez quels toodo dans les cas de hello d’une interruption de service Azure qui a un impact sur les Services de cloud computing Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Le toodo dans les cas de hello d’une interruption de service Azure qui a un impact sur les Services de cloud computing Azure
Chez Microsoft, nous travaillons dur toomake assurer que nos services sont toujours tooyou disponible lorsque vous avez besoin. Il arrive parfois que des phénomènes incontrôlables entraînent des interruptions de service non planifiées.

Microsoft fournit un Contrat de niveau de service (SLA) pour ses services en guise d’engagement en matière de disponibilité et de connectivité. Hello SLA des différents services Azure, consultez [les contrats de niveau de Service Azure](https://azure.microsoft.com/support/legal/sla/).

Azure dispose déjà de nombreuses fonctionnalités intégrées de plateforme qui prennent en charge des applications hautement disponibles. Pour plus d’informations sur ces services, consultez [Récupération d’urgence et haute disponibilité pour les applications Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Cet article décrit un scénario de récupération d’urgence true, lorsqu’un ensemble de la région connaît une panne en raison d’une catastrophe naturelle toomajor ou l’interruption de service étendu. Il s’agit des occurrences rares, mais vous devez préparer pour la possibilité de hello qu’il y a une panne d’une région entière. Si une région entière est confronté à une interruption de service, copies redondantes localement de hello de vos données sont temporairement indisponibles. Si vous avez activé la géoréplication, trois copies supplémentaires de vos tables et objets blob Azure Storage sont stockées dans une autre région. En cas de hello de panne régionale totale ou d’une catastrophe quels Bonjour la région principale n’est pas récupérable, Azure remappe toutes les du hello DNS entrées toohello géo-répliquées de la région.

> [!NOTE]
> N’oubliez pas que vous n’avez aucun contrôle sur ce processus et qu’il ne se produit que pour les interruptions du service au niveau du centre de données. Pour cette raison, vous devez également reposer sur les autres stratégies de sauvegarde spécifiques à l’application tooachieve hello plus haut niveau de disponibilité. Pour plus d’informations, consultez [Récupération d’urgence et haute disponibilité des applications développées sur Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). Si vous souhaitez que tooaffect en mesure de toobe votre propre basculement, vous souhaiterez peut-être utiliser hello tooconsider [stockage géo-redondant d’accès en lecture (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), ce qui crée une copie en lecture seule de vos données dans une autre région.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Option 1 : utilisation d’un déploiement de sauvegarde par le biais d’Azure Traffic Manager
solution de récupération d’urgence Hello plus robuste implique la gestion de plusieurs déploiements de votre application dans différentes régions, puis à l’aide de [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) trafic toodirect entre eux. Azure Traffic Manager fournit plusieurs [les méthodes de routage](../traffic-manager/traffic-manager-routing-methods.md), vous pouvez donc choisir si toomanage vos déploiements à l’aide d’un modèle de principaux de sauvegarde ou d’un toosplit le trafic entre eux.

![Équilibrage d’Azure Cloud Services entre différentes régions avec Azure Traffic Manager](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Perte de hello plus rapide réponse toohello d’une région, il est important de configurer le Gestionnaire de trafic [surveillance de point de terminaison](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-tooa-new-region"></a>Option 2 : Déployer votre région de nouvelle application tooa
Gestion de plusieurs déploiements actifs comme décrit dans l’option précédente de hello entraîne des frais supplémentaires en cours. Si votre objectif de temps de récupération (RTO) est suffisamment flexible et code d’origine de hello ou un package de Services de cloud computing compilé, vous pouvez créer une nouvelle instance de votre application dans une autre région et mettre à jour DNS les enregistrements toopoint toohello nouveau déploiement.

Pour plus d’informations sur la façon toocreate et le déploiement d’une application de service cloud, consultez [comment toocreate et déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).

En fonction de vos sources de données d’application, vous devrez peut-être les procédures de récupération toocheck hello pour votre source de données d’application.

* Pour les sources de données de stockage Azure, consultez [réplication de stockage Azure](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck sur les options de hello qui sont disponibles dans hello a choisi de réplication pour votre application.
* Pour les sources de base de données SQL, consultez [vue d’ensemble : Cloud d’entreprise la continuité et la base de données de la récupération d’urgence avec la base de données SQL](../sql-database/sql-database-business-continuity.md) toocheck sur les options de hello sont disponibles selon le modèle de réplication hello choisie pour votre application.


## <a name="option-3-wait-for-recovery"></a>Option 3 : attente de récupération
Dans ce cas, aucune action de votre part n’est requise, mais votre service sera indisponible jusqu'à ce que la région de hello est restaurée. Vous pouvez voir hello état actuel du service sur hello [tableau de bord d’intégrité de Service Azure](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Étapes suivantes
toolearn plus en détail comment tooimplement une récupération d’urgence et la stratégie de haute disponibilité, consultez [la récupération d’urgence et haute disponibilité pour les applications Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

toodevelop une compréhension technique détaillée des fonctionnalités de la plateforme cloud, consultez [Guide technique de résilience Azure](../resiliency/resiliency-technical-guidance.md).
