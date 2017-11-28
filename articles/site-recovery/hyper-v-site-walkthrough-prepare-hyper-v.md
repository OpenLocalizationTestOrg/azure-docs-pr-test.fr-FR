---
title: "aaaPrepare Hyper-V héberge (sans System Center VMM) pour la réplication tooAzure | Documents Microsoft"
description: "Décrit comment tooprepare Hyper-V héberge pour tooAzure de réplication à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="652a4-103">Étape 6 : Préparer les ordinateurs hôtes Hyper-V pour la réplication tooAzure</span><span class="sxs-lookup"><span data-stu-id="652a4-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="652a4-104">Suivez les instructions dans cette tooprepare article hello local toointeract d’ordinateurs hôtes Hyper-V avec Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="652a4-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="652a4-105">Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="652a4-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="652a4-106">Préparer des ordinateurs hôtes</span><span class="sxs-lookup"><span data-stu-id="652a4-106">Prepare hosts</span></span>

- <span data-ttu-id="652a4-107">Assurez-vous que les hôtes Hyper-V de hello respectent hello [conditions préalables](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="652a4-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="652a4-108">Assurez-vous que les hôtes de hello peuvent accéder à des URL de hello requis :</span><span class="sxs-lookup"><span data-stu-id="652a4-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="652a4-109">Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.</span><span class="sxs-lookup"><span data-stu-id="652a4-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="652a4-110">Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="652a4-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="652a4-111">Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).</span><span class="sxs-lookup"><span data-stu-id="652a4-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="652a4-112">Pendant le déploiement de la récupération de Site, vous ajoutez les hôtes Hyper-V qui contiennent des machines virtuelles que vous souhaitez tooreplicate tooa Hyper-V site.</span><span class="sxs-lookup"><span data-stu-id="652a4-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="652a4-113">Bonjour fournisseur Site Recovery et l’agent Recovery Services sont installés sur chaque ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="652a4-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="652a4-114">site de Hello Hyper-V est enregistré dans hello de coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="652a4-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="652a4-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="652a4-115">Next steps</span></span>

<span data-ttu-id="652a4-116">Accédez trop[étape 7 : créer un coffre](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="652a4-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

