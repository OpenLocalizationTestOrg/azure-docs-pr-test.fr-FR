---
title: "échecs d’artefact aaaDiagnose dans une machine virtuelle de Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment les échecs d’artefact tootroubleshoot dans DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="4b88c-103">Diagnostiquer les échecs d’artefact dans le laboratoire de hello</span><span class="sxs-lookup"><span data-stu-id="4b88c-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="4b88c-104">Après avoir créé un artefact, vous pouvez vérifier toosee si elle a réussi ou échoué.</span><span class="sxs-lookup"><span data-stu-id="4b88c-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="4b88c-105">Journaux d’artefact dans DevTest Labs fournissent des informations vous pouvez utiliser toodiagnose un échec de l’artefact.</span><span class="sxs-lookup"><span data-stu-id="4b88c-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="4b88c-106">Il existe plusieurs façons différentes, vous pouvez afficher les informations de journal d’artefact hello pour une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="4b88c-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4b88c-107">tooensure que les échecs sont correctement identifiés et expliqués, il est important de cet artefact hello est correctement structuré.</span><span class="sxs-lookup"><span data-stu-id="4b88c-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="4b88c-108">Pour plus d’informations sur comment toocorrectly construire un artefact, consultez [créer des artefacts personnalisés](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="4b88c-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="4b88c-109">Et toosee, par exemple, d’un objet structuré correctement, consultez ce [les Types de paramètres de Test](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefact.</span><span class="sxs-lookup"><span data-stu-id="4b88c-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="4b88c-110">Résoudre les échecs d’artefact à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4b88c-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="4b88c-111">échecs de toodiagnose portail Azure hello toouse lors de la création de l’artefact, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b88c-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="4b88c-112">Dans la liste hello des ressources, sélectionnez votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="4b88c-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="4b88c-113">Choisissez hello machine virtuelle Windows qui inclut l’artefact hello souhaité tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="4b88c-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="4b88c-114">Dans le volet gauche, hello sous **général**, choisissez **artefacts**.</span><span class="sxs-lookup"><span data-stu-id="4b88c-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="4b88c-115">Une liste des artefacts associés à cette machine virtuelle s’affiche, indique nom hello d’artefact de hello et son état.</span><span class="sxs-lookup"><span data-stu-id="4b88c-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="4b88c-117">Choisissez un artefact qui présente l’état **Échec**.</span><span class="sxs-lookup"><span data-stu-id="4b88c-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="4b88c-118">artefact de Hello s’ouvre et affiche un message d’extension qui inclut des détails sur les échecs de hello d’artefact de hello.</span><span class="sxs-lookup"><span data-stu-id="4b88c-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="4b88c-120">Résoudre les échecs d’artefact de hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4b88c-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="4b88c-121">tooview des journaux à partir de l’artefact de hello dans la machine virtuelle de hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b88c-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="4b88c-122">Connectez-vous toohello machine virtuelle qui contient l’artefact hello souhaité toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="4b88c-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="4b88c-123">Accédez tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status où « 1.9 est le numéro de version d’extension côté client hello.</span><span class="sxs-lookup"><span data-stu-id="4b88c-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="4b88c-125">Ouvrez hello **état** fichier tooview les informations que vous aide à diagnostiquer les échecs de l’artefact pour cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4b88c-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4b88c-126">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="4b88c-126">Related blog posts</span></span>
* [<span data-ttu-id="4b88c-127">Joindre un domaine Active Directory à l’aide d’un modèle de gestionnaire de ressources dans Azure DevTest Labs de tooexisting machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4b88c-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="4b88c-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b88c-128">Next steps</span></span>
* <span data-ttu-id="4b88c-129">Découvrez comment trop[ajouter un laboratoire tooa du référentiel Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="4b88c-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

