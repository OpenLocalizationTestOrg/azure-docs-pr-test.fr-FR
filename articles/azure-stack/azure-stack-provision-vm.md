---
title: "Créer une machine virtuelle de test dans Azure Stack | Microsoft Docs"
description: "Découvrez comment approvisionner une machine virtuelle dans Azure Stack en tant qu’opérateur cloud."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: erikje
ms.openlocfilehash: 233cf4df53af6a49e5fe4c5d51e112d8196a7530
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="3443a-103">Créer une machine virtuelle de test dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3443a-103">Create a test virtual machine in Azure Stack</span></span>

<span data-ttu-id="3443a-104">*S’applique à : Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="3443a-104">*Applies to: Azure Stack Development Kit*</span></span>

<span data-ttu-id="3443a-105">En tant qu’opérateur Azure Stack, vous pouvez créer une machine virtuelle de test pour valider votre déploiement du kit de développeur [Azure Stack](azure-stack-poc.md).</span><span class="sxs-lookup"><span data-stu-id="3443a-105">As an Azure Stack operator, you can create a test virtual machine to validate your [Azure Stack](azure-stack-poc.md) Developer Kit deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="3443a-106">Avant de pouvoir approvisionner des machines virtuelles, vous devez [ajouter l’image d’évaluation de Windows Server 2016 à la Place de marché Azure Stack](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="3443a-106">Before you can provision virtual machines, you must [add the Windows Server 2016 Evaluation image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="3443a-107">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3443a-107">Create a virtual machine</span></span>
1. <span data-ttu-id="3443a-108">Sur l’hôte du Kit de développement Azure Stack, [connectez-vous](azure-stack-connect-azure-stack.md) au portail d’administration (`https://adminportal.local.azurestack.external`), puis cliquez sur **Nouveau** > **Calcul** > **Windows Server 2016 Datacenter Evaluation** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3443a-108">On the Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) to the administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="3443a-109">Dans le panneau **Informations de base**, entrez un **Nom**, un **Nom d’utilisateur** et un **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3443a-109">In the **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="3443a-110">Choisissez un **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="3443a-110">Choose a **Subscription**.</span></span> <span data-ttu-id="3443a-111">Créez un **Groupe de ressources** ou sélectionnez un groupe existant, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3443a-111">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="3443a-112">Dans le panneau **Choisir une taille**, cliquez sur **A1 Standard**, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="3443a-112">In the **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="3443a-113">Dans le panneau **Paramètres**, acceptez les valeurs par défaut et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3443a-113">In the **Settings** blade, accept the defaults and click **OK**</span></span>
5. <span data-ttu-id="3443a-114">Dans le panneau **Résumé**, cliquez sur **OK** pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3443a-114">In the **Summary** blade, click **OK** to create the virtual machine.</span></span>  
6. <span data-ttu-id="3443a-115">Pour voir votre nouvelle machine virtuelle, cliquez sur **Toutes les ressources**, puis recherchez la machine virtuelle et cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="3443a-115">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="3443a-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3443a-116">Next steps</span></span>
[<span data-ttu-id="3443a-117">Utilisation des portails administrateur et utilisateur dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3443a-117">Using the administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
