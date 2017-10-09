---
title: aaaCreate un test de machine virtuelle dans Azure pile | Documents Microsoft
description: "Découvrez comment tooprovision une machine virtuelle dans la pile d’Azure sous la forme d’un opérateur cloud de test."
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
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 9633cc20852e16283ad4522da78971133028efdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a><span data-ttu-id="acabf-103">Créer une machine virtuelle de test dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="acabf-103">Create a test virtual machine in Azure Stack</span></span>
<span data-ttu-id="acabf-104">Comme un opérateur cloud, vous pouvez créer un toovalidate d’ordinateur virtuel de test votre déploiement Azure pile.</span><span class="sxs-lookup"><span data-stu-id="acabf-104">As a cloud operator, you can create a test virtual machine toovalidate your Azure Stack deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="acabf-105">Vous pouvez configurer des machines virtuelles, vous devez [ajouter le marketplace Azure pile toohello hello Windows Server 2016 Evaluation image](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="acabf-105">Before you can provision virtual machines, you must [add hello Windows Server 2016 Evaluation image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="create-a-virtual-machine"></a><span data-ttu-id="acabf-106">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="acabf-106">Create a virtual machine</span></span>
1. <span data-ttu-id="acabf-107">Sur l’hôte du Kit de développement de pile Azure hello, [connectez-vous](azure-stack-connect-azure-stack.md) toohello portail d’administration (`https://adminportal.local.azurestack.external`), puis cliquez sur **nouveau** > **de calcul**  >  **Windows Server 2016 Datacenter Eval** > **créer**.</span><span class="sxs-lookup"><span data-stu-id="acabf-107">On hello Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) toohello administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.</span></span>  
2. <span data-ttu-id="acabf-108">Bonjour **notions de base** panneau, tapez un **nom**, **nom d’utilisateur**, et **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="acabf-108">In hello **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="acabf-109">Choisissez un **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="acabf-109">Choose a **Subscription**.</span></span> <span data-ttu-id="acabf-110">Créez un **Groupe de ressources** ou sélectionnez un groupe existant, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="acabf-110">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="acabf-111">Bonjour **choisir une taille** panneau, cliquez sur **A1 Standard**, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="acabf-111">In hello **Choose a size** blade, click **A1 Standard**, and then click **Select**.</span></span>  
4. <span data-ttu-id="acabf-112">Bonjour **paramètres** panneau, acceptez les valeurs par défaut hello et cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="acabf-112">In hello **Settings** blade, accept hello defaults and click **OK**</span></span>
5. <span data-ttu-id="acabf-113">Bonjour **Résumé** panneau, cliquez sur **OK** toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="acabf-113">In hello **Summary** blade, click **OK** toocreate hello virtual machine.</span></span>  
6. <span data-ttu-id="acabf-114">toosee votre nouvel ordinateur virtuel, cliquez sur **toutes les ressources**, puis recherchez l’ordinateur virtuel de hello et cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="acabf-114">toosee your new virtual machine, click **All resources**, then search for hello virtual machine and click its name.</span></span>
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a><span data-ttu-id="acabf-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="acabf-115">Next steps</span></span>
[<span data-ttu-id="acabf-116">À l’aide des portails d’administrateur et utilisateur hello dans la pile de Azure</span><span class="sxs-lookup"><span data-stu-id="acabf-116">Using hello administrator and user portals in Azure Stack</span></span>](azure-stack-manage-portals.md)
