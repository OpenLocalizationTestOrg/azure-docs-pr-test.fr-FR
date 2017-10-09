---
title: "aaaPrepare System Center VMM pour Hyper-V réplication tooAzure | Documents Microsoft"
description: "Décrit comment serveur de System Center VMM tooprepare pour tooAzure de réplication Hyper-V, à l’aide d’Azure Site Recovery"
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
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="3fd39-103">Étape 6 : Préparer les serveurs VMM et des ordinateurs hôtes Hyper-V pour tooAzure de réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="3fd39-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="3fd39-104">Après avoir configuré [composants Azure](vmm-to-azure-walkthrough-prepare-azure.md) pour le déploiement de hello, utilisez les instructions de hello dans cet article tooprepare par VMM serveurs locaux et de toointeract des ordinateurs hôtes Hyper-V avec Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3fd39-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="3fd39-105">Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3fd39-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="3fd39-106">Préparer les serveurs VMM</span><span class="sxs-lookup"><span data-stu-id="3fd39-106">Prepare VMM servers</span></span>

- <span data-ttu-id="3fd39-107">Vous devez au moins un serveur VMM qui répondent aux exigences de prise en charge hello pour la réplication de Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="3fd39-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="3fd39-108">Vérifiez que vous avez préparé serveur VMM de hello pour [le mappage réseau](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="3fd39-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="3fd39-109">Assurez-vous que le serveur VMM hello peut accéder à ces URL</span><span class="sxs-lookup"><span data-stu-id="3fd39-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="3fd39-110">Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.</span><span class="sxs-lookup"><span data-stu-id="3fd39-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="3fd39-111">Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="3fd39-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="3fd39-112">Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).</span><span class="sxs-lookup"><span data-stu-id="3fd39-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="3fd39-113">Pendant le déploiement de la récupération de Site, vous téléchargez hello fournisseur Site Recovery et l’installer sur chaque serveur VMM.</span><span class="sxs-lookup"><span data-stu-id="3fd39-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="3fd39-114">serveur VMM de Hello est inscrit dans hello de coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="3fd39-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="3fd39-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3fd39-115">Next steps</span></span>

<span data-ttu-id="3fd39-116">Accédez trop[étape 7 : créer un coffre](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="3fd39-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

