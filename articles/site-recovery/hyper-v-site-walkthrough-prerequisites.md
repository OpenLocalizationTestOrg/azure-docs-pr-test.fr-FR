---
title: "conditions préalables de hello aaaReview pour la réplication de tooAzure Hyper-V (sans System Center VMM) à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Décrit les conditions requises de hello pour configurer la réplication, le basculement et la récupération de tooAzure d’ordinateurs virtuels Hyper-V local avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="51880-103">Étape 2 : Passez en revue les conditions préalables de hello pour la réplication Hyper-V (sans VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="51880-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="51880-104">conditions préalables de Hello sont résumées dans le tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="51880-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="51880-105">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="51880-105">**Prerequisite**</span></span> | <span data-ttu-id="51880-106">**Détails**</span><span class="sxs-lookup"><span data-stu-id="51880-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="51880-107">**Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="51880-107">**Azure**</span></span> | <span data-ttu-id="51880-108">Découvrez la [configuration requise pour Azure](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="51880-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="51880-109">**Serveurs locaux**</span><span class="sxs-lookup"><span data-stu-id="51880-109">**On-premises servers**</span></span> | <span data-ttu-id="51880-110">[En savoir plus](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sur la configuration requise pour les ordinateurs hôtes Hyper-V de hello localement.</span><span class="sxs-lookup"><span data-stu-id="51880-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="51880-111">**Machines virtuelles Hyper-V en local**</span><span class="sxs-lookup"><span data-stu-id="51880-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="51880-112">Machines virtuelles que vous souhaitez tooreplicate doit être en cours d’exécution un [prise en charge du système d’exploitation](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)et être conformes avec [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="51880-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="51880-113">**URL Azure**</span><span class="sxs-lookup"><span data-stu-id="51880-113">**Azure URLs**</span></span> | <span data-ttu-id="51880-114">Hôtes Hyper-V doivent accéder aux URL de toothese :</span><span class="sxs-lookup"><span data-stu-id="51880-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="51880-115">Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.</span><span class="sxs-lookup"><span data-stu-id="51880-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="51880-116">Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="51880-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="51880-117">Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).</span><span class="sxs-lookup"><span data-stu-id="51880-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="51880-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51880-118">Next steps</span></span>

- <span data-ttu-id="51880-119">Si vous effectuez un déploiement complet, passez trop[étape 3 : planifier la capacité](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="51880-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="51880-120">Si vous effectuez un déploiement de test simple, passez trop[étape 4 : planifier la mise en réseau](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="51880-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
