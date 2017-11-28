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
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a><span data-ttu-id="4dac8-103">Le toodo dans l’événement hello qu’une interruption de service Azure a un impact sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="4dac8-103">What toodo in hello event that an Azure service disruption impacts Azure VMs</span></span>
<span data-ttu-id="4dac8-104">Chez Microsoft, nous travaillons dur toomake assurer que nos services sont toujours tooyou disponible lorsque vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="4dac8-104">At Microsoft, we work hard toomake sure that our services are always available tooyou when you need them.</span></span> <span data-ttu-id="4dac8-105">Il arrive parfois que des phénomènes incontrôlables entraînent des interruptions de service non planifiées.</span><span class="sxs-lookup"><span data-stu-id="4dac8-105">Forces beyond our control sometimes impact us in ways that cause unplanned service disruptions.</span></span>

<span data-ttu-id="4dac8-106">Microsoft fournit un Contrat de niveau de service (SLA) pour ses services en guise d’engagement en matière de disponibilité et de connectivité.</span><span class="sxs-lookup"><span data-stu-id="4dac8-106">Microsoft provides a Service Level Agreement (SLA) for its services as a commitment for uptime and connectivity.</span></span> <span data-ttu-id="4dac8-107">Hello SLA des différents services Azure, consultez [les contrats de niveau de Service Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="4dac8-107">hello SLA for individual Azure services can be found at [Azure Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="4dac8-108">Azure dispose déjà de nombreuses fonctionnalités intégrées de plateforme qui prennent en charge des applications hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="4dac8-108">Azure already has many built-in platform features that support highly available applications.</span></span> <span data-ttu-id="4dac8-109">Pour plus d’informations sur ces services, consultez [Récupération d’urgence et haute disponibilité pour les applications Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span><span class="sxs-lookup"><span data-stu-id="4dac8-109">For more about these services, read [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span>

<span data-ttu-id="4dac8-110">Cet article décrit un scénario de récupération d’urgence true, lorsqu’un ensemble de la région connaît une panne en raison d’une catastrophe naturelle toomajor ou l’interruption de service étendu.</span><span class="sxs-lookup"><span data-stu-id="4dac8-110">This article covers a true disaster recovery scenario, when a whole region experiences an outage due toomajor natural disaster or widespread service interruption.</span></span> <span data-ttu-id="4dac8-111">Il s’agit des occurrences rares, mais vous devez préparer pour la possibilité de hello qu’il y a une panne d’une région entière.</span><span class="sxs-lookup"><span data-stu-id="4dac8-111">These are rare occurrences, but you must prepare for hello possibility that there is an outage of an entire region.</span></span> <span data-ttu-id="4dac8-112">Si une région entière est confronté à une interruption de service, copies redondantes localement de hello de vos données sont temporairement indisponibles.</span><span class="sxs-lookup"><span data-stu-id="4dac8-112">If an entire region experiences a service disruption, hello locally redundant copies of your data would temporarily be unavailable.</span></span> <span data-ttu-id="4dac8-113">Si vous avez activé la géoréplication, trois copies supplémentaires de vos tables et objets blob Azure Storage sont stockées dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="4dac8-113">If you have enabled geo-replication, three additional copies of your Azure Storage blobs and tables are stored in a different region.</span></span> <span data-ttu-id="4dac8-114">En cas de hello de panne régionale totale ou d’une catastrophe quels Bonjour la région principale n’est pas récupérable, Azure remappe toutes les du hello DNS entrées toohello géo-répliquées de la région.</span><span class="sxs-lookup"><span data-stu-id="4dac8-114">In hello event of a complete regional outage or a disaster in which hello primary region is not recoverable, Azure remaps all of hello DNS entries toohello geo-replicated region.</span></span>

<span data-ttu-id="4dac8-115">toohelp vous gérez ces occurrences rares, nous fournissons hello suivant les instructions fournies pour les machines virtuelles dans les cas de hello d’une interruption de service de hello ensemble de la région où votre application de la machine virtuelle Azure est déployée.</span><span class="sxs-lookup"><span data-stu-id="4dac8-115">toohelp you handle these rare occurrences, we provide hello following guidance for Azure virtual machines in hello case of a service disruption of hello entire region where your Azure virtual machine application is deployed.</span></span>

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a><span data-ttu-id="4dac8-116">Option 1 : Lancer un basculement à l’aide d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="4dac8-116">Option 1: Initiate a failover by using Azure Site Recovery</span></span>
<span data-ttu-id="4dac8-117">Vous pouvez configurer Azure Site Recovery pour vos machines virtuelles afin de pouvoir récupérer votre application en un seul clic en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4dac8-117">You can configure Azure Site Recovery for your VMs so that you can recover your application with a single click in matter of minutes.</span></span> <span data-ttu-id="4dac8-118">Vous pouvez répliquer tooAzure la région de votre choix et les régions toopaired non restreint.</span><span class="sxs-lookup"><span data-stu-id="4dac8-118">You can replicate tooAzure region of your choice and not restricted toopaired regions.</span></span> <span data-ttu-id="4dac8-119">Vous pouvez commencer par [répliquer vos machines virtuelles](https://aka.ms/a2a-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4dac8-119">You can get started by [replicating your virtual machines](https://aka.ms/a2a-getting-started).</span></span> <span data-ttu-id="4dac8-120">Vous pouvez [créer un plan de récupération](../site-recovery/site-recovery-create-recovery-plans.md) afin que vous pouvez automatiser le processus de basculements de hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4dac8-120">You can [create a recovery plan](../site-recovery/site-recovery-create-recovery-plans.md) so that you can automate hello entire failover process for your application.</span></span> <span data-ttu-id="4dac8-121">Vous pouvez [tester votre basculements](../site-recovery/site-recovery-test-failover-to-azure.md) avance sans impact sur la réplication en cours de production application ou hello.</span><span class="sxs-lookup"><span data-stu-id="4dac8-121">You can [test your failovers](../site-recovery/site-recovery-test-failover-to-azure.md) beforehand without impacting production application or hello ongoing replication.</span></span> <span data-ttu-id="4dac8-122">Dans le cas de hello d’une interruption de la région principale, que vous venez [initier un basculement](../site-recovery/site-recovery-failover.md) et mettre votre application dans la région cible.</span><span class="sxs-lookup"><span data-stu-id="4dac8-122">In hello event of a primary region disruption, you just [initiate a failover](../site-recovery/site-recovery-failover.md) and bring your application in target region.</span></span>


## <a name="option-2-wait-for-recovery"></a><span data-ttu-id="4dac8-123">Option 2 : Attendre la récupération</span><span class="sxs-lookup"><span data-stu-id="4dac8-123">Option 2: Wait for recovery</span></span>
<span data-ttu-id="4dac8-124">Dans ce cas, aucune action n’est requise de votre part.</span><span class="sxs-lookup"><span data-stu-id="4dac8-124">In this case, no action on your part is required.</span></span> <span data-ttu-id="4dac8-125">Savoir que nous travaillons soigneusement toorestore disponibilité du service.</span><span class="sxs-lookup"><span data-stu-id="4dac8-125">Know that we are working diligently toorestore service availability.</span></span> <span data-ttu-id="4dac8-126">Vous pouvez voir l’état du service actuel hello sur notre [tableau de bord d’intégrité de Service Azure](https://azure.microsoft.com/status/).</span><span class="sxs-lookup"><span data-stu-id="4dac8-126">You can see hello current service status on our [Azure Service Health Dashboard](https://azure.microsoft.com/status/).</span></span>

<span data-ttu-id="4dac8-127">Cette option de meilleures hello est si vous n’avez pas défini d’Azure Site Recovery, un stockage géo-redondant avec accès en lecture ou interruption de service de stockage géo-redondant toohello préalable.</span><span class="sxs-lookup"><span data-stu-id="4dac8-127">This is hello best option if you have not set up Azure Site Recovery, read-access geo-redundant storage, or geo-redundant storage prior toohello disruption.</span></span> <span data-ttu-id="4dac8-128">Si vous avez configuré un stockage géo-redondant ou le stockage de géo-redondant avec accès en lecture pour le compte de stockage hello où sont stockés vos disques durs virtuels de l’ordinateur virtuel (VHD), vous pouvez rechercher l’image de base hello toorecover disque dur virtuel et essayez tooprovision une nouvelle machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="4dac8-128">If you have set up geo-redundant storage or read-access geo-redundant storage for hello storage account where your VM virtual hard drives (VHDs) are stored, you can look toorecover hello base image VHD and try tooprovision a new VM from it.</span></span> <span data-ttu-id="4dac8-129">Cette option n’est pas recommandée, car elle ne garantit pas la synchronisation des données.</span><span class="sxs-lookup"><span data-stu-id="4dac8-129">This is not a preferred option because there are no guarantees of synchronization of data.</span></span> <span data-ttu-id="4dac8-130">Par conséquent, cette option n’est pas garantie toowork.</span><span class="sxs-lookup"><span data-stu-id="4dac8-130">Consequently, this option is not guaranteed toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="4dac8-131">N’oubliez pas que vous n’avez aucun contrôle sur ce processus et qu’il ne se produit que pour des interruptions du service au niveau régional.</span><span class="sxs-lookup"><span data-stu-id="4dac8-131">Be aware that you do not have any control over this process, and it will only occur for region-wide service disruptions.</span></span> <span data-ttu-id="4dac8-132">Pour cette raison, vous devez également reposer sur les autres stratégies de sauvegarde spécifiques à l’application tooachieve hello plus haut niveau de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="4dac8-132">Because of this, you must also rely on other application-specific backup strategies tooachieve hello highest level of availability.</span></span> <span data-ttu-id="4dac8-133">Pour plus d’informations, consultez la section de hello sur [stratégies de données pour la récupération d’urgence](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="4dac8-133">For more information, see hello section on [Data strategies for disaster recovery](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4dac8-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4dac8-134">Next steps</span></span>

- <span data-ttu-id="4dac8-135">Commencez à [protéger vos applications s’exécutant sur des machines virtuelles Azure ](https://aka.ms/a2a-getting-started) en utilisant Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="4dac8-135">Start [protecting your applications running on Azure virtual machines](https://aka.ms/a2a-getting-started) using Azure Site Recovery</span></span>

- <span data-ttu-id="4dac8-136">toolearn plus en détail comment tooimplement une récupération d’urgence et la stratégie de haute disponibilité, consultez [la récupération d’urgence et haute disponibilité pour les applications Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span><span class="sxs-lookup"><span data-stu-id="4dac8-136">toolearn more about how tooimplement a disaster recovery and high availability strategy, see [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span>

- <span data-ttu-id="4dac8-137">toodevelop une compréhension technique détaillée des fonctionnalités de la plateforme cloud, consultez [Guide technique de résilience Azure](../resiliency/resiliency-technical-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="4dac8-137">toodevelop a detailed technical understanding of a cloud platform’s capabilities, see [Azure resiliency technical guidance](../resiliency/resiliency-technical-guidance.md).</span></span>


- <span data-ttu-id="4dac8-138">Si les instructions hello ne sont pas claire, ou si vous souhaitez que les opérations de hello toodo Microsoft en votre nom, contactez [Support technique](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="4dac8-138">If hello instructions are not clear, or if you would like Microsoft toodo hello operations on your behalf, contact [Customer Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>