---
title: "Préparation d’hôtes Hyper-V (sans System Center VMM) pour la réplication vers Azure | Microsoft Docs"
description: "Décrit comment préparer des ordinateurs hôtes Hyper-V pour la réplication vers Azure à l’aide d’Azure Site Recovery"
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
ms.openlocfilehash: f9bcaa8e55be6e8fddaf88ebc3f18f5dbb2811e4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-to-azure"></a><span data-ttu-id="905df-103">Étape 6 : préparer des ordinateurs hôtes Hyper-V pour la réplication vers Azure</span><span class="sxs-lookup"><span data-stu-id="905df-103">Step 6: Prepare Hyper-V hosts for replication to Azure</span></span>

<span data-ttu-id="905df-104">Suivez les instructions de cet article pour préparer des hôtes Hyper-V locaux à interagir avec Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="905df-104">Use the instructions in this article to prepare on-premises Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="905df-105">Après avoir lu cet article, envoyez vos commentaires en bas ou posez vos questions techniques sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="905df-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="905df-106">Préparer des ordinateurs hôtes</span><span class="sxs-lookup"><span data-stu-id="905df-106">Prepare hosts</span></span>

- <span data-ttu-id="905df-107">Assurez-vous que les hôtes Hyper-V respectent la [configuration requise](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="905df-107">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="905df-108">Assurez-vous que les hôtes peuvent accéder aux URL requises :</span><span class="sxs-lookup"><span data-stu-id="905df-108">Make sure that the hosts can access the required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="905df-109">Si vous avez des règles de pare-feu fondées sur l’adresse IP, vérifiez qu’elles autorisent la communication vers Azure.</span><span class="sxs-lookup"><span data-stu-id="905df-109">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="905df-110">Autorisez les [plages d’adresses IP de centres de données Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) et le port HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="905df-110">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="905df-111">Autorisez les plages d’adresses IP relatives à la région de votre abonnement Azure et à la région des États-Unis de l’Ouest (utilisées pour la gestion du contrôle d’accès et des identités).</span><span class="sxs-lookup"><span data-stu-id="905df-111">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="905df-112">Pendant le déploiement de Site Recovery, vous ajoutez des hôtes Hyper-V qui contiennent des machines virtuelles que vous souhaitez répliquer sur un site Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="905df-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want to replicate to a Hyper-V site.</span></span> <span data-ttu-id="905df-113">Le fournisseur et l’agent Site Recovery sont installés sur chaque hôte.</span><span class="sxs-lookup"><span data-stu-id="905df-113">The Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="905df-114">Le site Hyper-V est inscrit dans le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="905df-114">The Hyper-V site is registered in the Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="905df-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="905df-115">Next steps</span></span>

<span data-ttu-id="905df-116">Aller à l’[Étape 7 : créer un coffre](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="905df-116">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

