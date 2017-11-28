---
title: "Préparation de System Center VMM pour la réplication Hyper-V vers Azure | Microsoft Docs"
description: "Décrit comment préparer le serveur System Center VMM pour la réplication Hyper-V vers Azure à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ec118ed837dbf140083b3ae1e4ecd41c81562018
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-to-azure"></a><span data-ttu-id="4fabb-103">Étape 6 : Préparer les serveurs VMM et les hôtes Hyper-V pour la réplication Hyper-V vers Azure</span><span class="sxs-lookup"><span data-stu-id="4fabb-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication to Azure</span></span>

<span data-ttu-id="4fabb-104">Après avoir configuré les [composants Azure](vmm-to-azure-walkthrough-prepare-azure.md) pour le déploiement, suivez les instructions dans cet article pour préparer les serveurs VMM et les hôtes Hyper-V locaux pour interagir avec Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4fabb-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for the deployment, use the instructions in this article to prepare on-premises VMM servers and Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="4fabb-105">Après avoir lu cet article, envoyez vos commentaires en bas ou posez vos questions techniques sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4fabb-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="4fabb-106">Préparer les serveurs VMM</span><span class="sxs-lookup"><span data-stu-id="4fabb-106">Prepare VMM servers</span></span>

- <span data-ttu-id="4fabb-107">Vous devez avoir au moins un serveur VMM conforme aux exigences de la réplication Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="4fabb-107">You need at least one VMM server that meet the support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="4fabb-108">Assurez-vous d’avoir préparé le serveur VMM pour le [mappage réseau](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="4fabb-108">Make sure you've prepared the VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="4fabb-109">Vérifier que le serveur VMM peut accéder à ces URL</span><span class="sxs-lookup"><span data-stu-id="4fabb-109">Make sure that the VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="4fabb-110">Si vous avez des règles de pare-feu fondées sur l’adresse IP, vérifiez qu’elles autorisent la communication vers Azure.</span><span class="sxs-lookup"><span data-stu-id="4fabb-110">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="4fabb-111">Autorisez les [plages d’adresses IP de centres de données Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) et le port HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="4fabb-111">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="4fabb-112">Autorisez les plages d’adresses IP relatives à la région de votre abonnement Azure et à la région des États-Unis de l’Ouest (utilisées pour la gestion du contrôle d’accès et des identités).</span><span class="sxs-lookup"><span data-stu-id="4fabb-112">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="4fabb-113">Pendant un déploiement de Site Recovery, vous téléchargez le fournisseur Azure Site Recovery et vous l’installez sur chaque serveur VMM.</span><span class="sxs-lookup"><span data-stu-id="4fabb-113">During Site Recovery deployment, you download the Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="4fabb-114">Le serveur VMM est inscrit dans le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4fabb-114">The VMM server is registered in the Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="4fabb-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fabb-115">Next steps</span></span>

<span data-ttu-id="4fabb-116">Aller à l’[Étape 7 : créer un coffre](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="4fabb-116">Go to [Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

