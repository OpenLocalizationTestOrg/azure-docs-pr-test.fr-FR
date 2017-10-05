---
title: "Préparer la cible (Physique vers Azure) | Microsoft Docs"
description: "Cet article décrit comment préparer votre environnement Azure pour lancer la réplication des serveurs physiques exécutant Windows ou Linux vers Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: aa7a32ace8354f615a8b8cc137f6bdf48fbadf48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="c0468-103">Préparer la cible (VMware vers Azure)</span><span class="sxs-lookup"><span data-stu-id="c0468-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0468-104">VMware vers Azure</span><span class="sxs-lookup"><span data-stu-id="c0468-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="c0468-105">Physique vers Azure</span><span class="sxs-lookup"><span data-stu-id="c0468-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="c0468-106">Cet article décrit comment préparer votre environnement Azure pour lancer la réplication des serveurs physiques (x64) exécutant Windows ou Linux vers Azure.</span><span class="sxs-lookup"><span data-stu-id="c0468-106">This article describes how to prepare your Azure environment to start replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0468-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c0468-107">Prerequisites</span></span>

<span data-ttu-id="c0468-108">Cet article part des principes suivants :</span><span class="sxs-lookup"><span data-stu-id="c0468-108">The article assumes the following:</span></span>
- <span data-ttu-id="c0468-109">Vous avez créé un coffre Recovery Services pour protéger vos serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="c0468-109">You have created a Recovery Services Vault to protect your physical servers.</span></span> <span data-ttu-id="c0468-110">Vous pouvez créer un coffre Recovery Services dans le [portail Azure](http://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="c0468-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="c0468-111">Vous avez [configuré votre environnement local](./site-recovery-set-up-physical-to-azure.md) pour répliquer les serveurs physiques vers Azure.</span><span class="sxs-lookup"><span data-stu-id="c0468-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) to replicate physical servers to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="c0468-112">Préparer la cible</span><span class="sxs-lookup"><span data-stu-id="c0468-112">Prepare target</span></span>

<span data-ttu-id="c0468-113">Après avoir réalisé **l’Étape 1 : Sélection de l’objectif de la protection** et **l’Étape 2 : Préparation de la source**, vous passez à **l’Étape 3 : Cible**.</span><span class="sxs-lookup"><span data-stu-id="c0468-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Préparer la cible](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="c0468-115">**Abonnement :** dans le menu déroulant, sélectionnez l’abonnement vers lequel vous souhaitez répliquer vos serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="c0468-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your physical servers to.</span></span>
2. <span data-ttu-id="c0468-116">**Modèle de déploiement :** sélectionnez le modèle de déploiement (Classique ou Gestionnaire de ressources).</span><span class="sxs-lookup"><span data-stu-id="c0468-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="c0468-117">Selon le modèle de déploiement choisi, une validation est exécutée pour vérifier que vous disposez au moins d’un compte de stockage et d’un réseau virtuel compatibles dans l’abonnement cible pour la réplication et le basculement de vos serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="c0468-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your physical servers to.</span></span>

<span data-ttu-id="c0468-118">Une fois les validations terminées avec succès, cliquez sur OK pour passer à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="c0468-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="c0468-119">Si vous n’avez pas de compte de stockage Resource Manager ou réseau virtuel compatible, ou si vous souhaitez en ajouter d’autres, vous pouvez le faire en cliquant sur les boutons **+ Compte de stockage** ou **+ Réseau** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="c0468-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0468-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0468-120">Next steps</span></span>
<span data-ttu-id="c0468-121">[Configurer les paramètres de réplication](./site-recovery-setup-replication-settings-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="c0468-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
