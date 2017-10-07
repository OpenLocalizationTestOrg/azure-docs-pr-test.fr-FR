---
title: "aaaDisaster des scénarios de récupération pour les machines virtuelles Azure | Documents Microsoft"
description: "Découvrez quels toodo dans l’événement hello une interruption de service Azure a un impact sur les machines virtuelles Azure."
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Le toodo dans l’événement hello qu’une interruption de service Azure a un impact sur des machines virtuelles Azure
Chez Microsoft, nous travaillons dur toomake assurer que nos services sont toujours tooyou disponible lorsque vous avez besoin. Il arrive parfois que des phénomènes incontrôlables entraînent des interruptions de service non planifiées.

Microsoft fournit un Contrat de niveau de service (SLA) pour ses services en guise d’engagement en matière de disponibilité et de connectivité. Hello SLA des différents services Azure, consultez [les contrats de niveau de Service Azure](https://azure.microsoft.com/support/legal/sla/).

Azure dispose déjà de nombreuses fonctionnalités intégrées de plateforme qui prennent en charge des applications hautement disponibles. Pour plus d’informations sur ces services, consultez [Récupération d’urgence et haute disponibilité pour les applications Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Cet article décrit un scénario de récupération d’urgence true, lorsqu’un ensemble de la région connaît une panne en raison d’une catastrophe naturelle toomajor ou l’interruption de service étendu. Il s’agit des occurrences rares, mais vous devez préparer pour la possibilité de hello qu’il y a une panne d’une région entière. Si une région entière est confronté à une interruption de service, copies redondantes localement de hello de vos données sont temporairement indisponibles. Si vous avez activé la géoréplication, trois copies supplémentaires de vos tables et objets blob Azure Storage sont stockées dans une autre région. En cas de hello de panne régionale totale ou d’une catastrophe quels Bonjour la région principale n’est pas récupérable, Azure remappe toutes les du hello DNS entrées toohello géo-répliquées de la région.

toohelp vous gérez ces occurrences rares, nous fournissons hello suivant les instructions fournies pour les machines virtuelles dans les cas de hello d’une interruption de service de hello ensemble de la région où votre application de la machine virtuelle Azure est déployée.

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>Option 1 : Lancer un basculement à l’aide d’Azure Site Recovery
Vous pouvez configurer Azure Site Recovery pour vos machines virtuelles afin de pouvoir récupérer votre application en un seul clic en quelques minutes. Vous pouvez répliquer tooAzure la région de votre choix et les régions toopaired non restreint. Vous pouvez commencer par [répliquer vos machines virtuelles](https://aka.ms/a2a-getting-started). Vous pouvez [créer un plan de récupération](../site-recovery/site-recovery-create-recovery-plans.md) afin que vous pouvez automatiser le processus de basculements de hello pour votre application. Vous pouvez [tester votre basculements](../site-recovery/site-recovery-test-failover-to-azure.md) avance sans impact sur la réplication en cours de production application ou hello. Dans le cas de hello d’une interruption de la région principale, que vous venez [initier un basculement](../site-recovery/site-recovery-failover.md) et mettre votre application dans la région cible.


## <a name="option-2-wait-for-recovery"></a>Option 2 : Attendre la récupération
Dans ce cas, aucune action n’est requise de votre part. Savoir que nous travaillons soigneusement toorestore disponibilité du service. Vous pouvez voir l’état du service actuel hello sur notre [tableau de bord d’intégrité de Service Azure](https://azure.microsoft.com/status/).

Cette option de meilleures hello est si vous n’avez pas défini d’Azure Site Recovery, un stockage géo-redondant avec accès en lecture ou interruption de service de stockage géo-redondant toohello préalable. Si vous avez configuré un stockage géo-redondant ou le stockage de géo-redondant avec accès en lecture pour le compte de stockage hello où sont stockés vos disques durs virtuels de l’ordinateur virtuel (VHD), vous pouvez rechercher l’image de base hello toorecover disque dur virtuel et essayez tooprovision une nouvelle machine virtuelle à partir de celui-ci. Cette option n’est pas recommandée, car elle ne garantit pas la synchronisation des données. Par conséquent, cette option n’est pas garantie toowork.


> [!NOTE]
> N’oubliez pas que vous n’avez aucun contrôle sur ce processus et qu’il ne se produit que pour des interruptions du service au niveau régional. Pour cette raison, vous devez également reposer sur les autres stratégies de sauvegarde spécifiques à l’application tooachieve hello plus haut niveau de disponibilité. Pour plus d’informations, consultez la section de hello sur [stratégies de données pour la récupération d’urgence](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).
>
>

## <a name="next-steps"></a>Étapes suivantes

- Commencez à [protéger vos applications s’exécutant sur des machines virtuelles Azure ](https://aka.ms/a2a-getting-started) en utilisant Azure Site Recovery

- toolearn plus en détail comment tooimplement une récupération d’urgence et la stratégie de haute disponibilité, consultez [la récupération d’urgence et haute disponibilité pour les applications Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

- toodevelop une compréhension technique détaillée des fonctionnalités de la plateforme cloud, consultez [Guide technique de résilience Azure](../resiliency/resiliency-technical-guidance.md).


- Si les instructions hello ne sont pas claire, ou si vous souhaitez que les opérations de hello toodo Microsoft en votre nom, contactez [Support technique](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
