---
title: "Préparer la cible (tooAzure physique) | Documents Microsoft"
description: "Cet article décrit comment tooprepare votre toostart environnement Azure réplication des serveurs physiques exécutant tooAzure Windows ou Linux."
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
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="8e7ee-103">Préparer la cible (tooAzure VMware)</span><span class="sxs-lookup"><span data-stu-id="8e7ee-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e7ee-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="8e7ee-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="8e7ee-105">TooAzure physique</span><span class="sxs-lookup"><span data-stu-id="8e7ee-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="8e7ee-106">Cet article décrit comment tooprepare votre toostart environnement Azure réplication des serveurs physiques (x 64) exécutant Windows ou Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-106">This article describes how tooprepare your Azure environment toostart replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e7ee-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8e7ee-107">Prerequisites</span></span>

<span data-ttu-id="8e7ee-108">article de Hello suppose hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="8e7ee-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="8e7ee-109">Vous avez créé un tooprotect coffre Recovery Services vos serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-109">You have created a Recovery Services Vault tooprotect your physical servers.</span></span> <span data-ttu-id="8e7ee-110">Vous pouvez créer un coffre Recovery Services depuis hello [portail Azure](http://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="8e7ee-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="8e7ee-111">Vous avez [le programme d’installation de votre environnement local](./site-recovery-set-up-physical-to-azure.md) tooreplicate serveurs physiques tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) tooreplicate physical servers tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="8e7ee-112">Préparer la cible</span><span class="sxs-lookup"><span data-stu-id="8e7ee-112">Prepare target</span></span>

<span data-ttu-id="8e7ee-113">Après avoir effectué hello **objectif de Protection étape 1 : sélectionnez** et **étape 2 : préparer la Source**, vous accédez trop**étape 3 : cible**</span><span class="sxs-lookup"><span data-stu-id="8e7ee-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Préparer la cible](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="8e7ee-115">**L’abonnement :** de hello menu déroulant, sélectionnez hello abonnement que vous souhaitez tooreplicate vos serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your physical servers to.</span></span>
2. <span data-ttu-id="8e7ee-116">**Modèle de déploiement :** modèle de déploiement hello Select (Gestionnaire de ressources ou classique)</span><span class="sxs-lookup"><span data-stu-id="8e7ee-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="8e7ee-117">En fonction de hello choisi le modèle de déploiement, une validation est exécutée tooensure avoir au moins un compte de stockage compatible et le réseau virtuel dans tooreplicate d’abonnement hello cible et le basculement de vos serveurs physiques à.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your physical servers to.</span></span>

<span data-ttu-id="8e7ee-118">Une fois les validations hello se terminent correctement, cliquez sur OK toogo toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="8e7ee-119">Si vous n’avez pas un compte de stockage compatible avec le Gestionnaire de ressources ou d’un réseau virtuel, ou que vous voulez que tooadd plus, vous pouvez le faire en cliquant sur hello **+ compte de stockage** ou **+ réseau** boutons haut hello Hello panneau.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e7ee-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e7ee-120">Next steps</span></span>
<span data-ttu-id="8e7ee-121">[Configurer les paramètres de réplication](./site-recovery-setup-replication-settings-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="8e7ee-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
