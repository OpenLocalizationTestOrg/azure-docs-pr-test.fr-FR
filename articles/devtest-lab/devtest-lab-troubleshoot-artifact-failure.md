---
title: "Diagnostiquer les échecs d’artefacts dans une machine virtuelle Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment résoudre les échecs des artefacts dans DevTest Labs."
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
ms.openlocfilehash: e4f2946d0ba0756f36622aded0e8594acabb9527
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="diagnose-artifact-failures-in-the-lab"></a><span data-ttu-id="20586-103">Diagnostiquer les échecs d’artefacts dans le labo</span><span class="sxs-lookup"><span data-stu-id="20586-103">Diagnose artifact failures in the lab</span></span> 
<span data-ttu-id="20586-104">Une fois que vous avez créé un artefact, vous pouvez vérifier si la procédure a réussi ou échoué.</span><span class="sxs-lookup"><span data-stu-id="20586-104">After you have created an artifact, you can check to see if it succeeded or failed.</span></span> <span data-ttu-id="20586-105">Les journaux d’artefact de DevTest Labs fournissent des informations qui permettent de diagnostiquer un échec d’artefact.</span><span class="sxs-lookup"><span data-stu-id="20586-105">Artifact logs in DevTest Labs provide information you can use to diagnose an artifact failure.</span></span> <span data-ttu-id="20586-106">Il existe plusieurs façons d’afficher les informations du journal de l’artefact pour une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="20586-106">There are a couple different ways you can view the artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="20586-107">Pour que les échecs sont correctement identifiés et expliqués, il est important que l’artefact soit correctement structuré.</span><span class="sxs-lookup"><span data-stu-id="20586-107">To ensure that failures are correctly identified and explained, it is important that the artifact is properly structured.</span></span> <span data-ttu-id="20586-108">Pour plus d’informations sur la bonne façon de créer un artefact, consultez la page [Créer des artefacts personnalisés](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="20586-108">For information about how to correctly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="20586-109">Par ailleurs, l’artefact [Types de paramètres de test](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) est un exemple d’artefact structuré correctement.</span><span class="sxs-lookup"><span data-stu-id="20586-109">And to see an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-the-azure-portal"></a><span data-ttu-id="20586-110">Résoudre les échecs des artefacts avec le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="20586-110">Troubleshoot artifact failures using the Azure portal</span></span>
<span data-ttu-id="20586-111">Pour utiliser le Portail Azure afin de diagnostiquer les échecs à la création d’un artefact, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="20586-111">To use the Azure portal to diagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="20586-112">Dans la liste de ressources, sélectionnez votre labo.</span><span class="sxs-lookup"><span data-stu-id="20586-112">From the list of resources, select your lab.</span></span>

2. <span data-ttu-id="20586-113">Choisissez la machine virtuelle Windows qui inclut l’artefact à analyser.</span><span class="sxs-lookup"><span data-stu-id="20586-113">Choose the Windows VM that includes the artifact you want to investigate.</span></span>

3. <span data-ttu-id="20586-114">Dans le volet gauche sous **GÉNÉRAL**, choisissez **Artefacts**.</span><span class="sxs-lookup"><span data-stu-id="20586-114">In the left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="20586-115">La liste des artefacts associés à cette machine virtuelle s’affiche, indiquant le nom de l’artefact et son état.</span><span class="sxs-lookup"><span data-stu-id="20586-115">A list of artifacts associated with that VM appears, indicating the name of the artifact and its status.</span></span>

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="20586-117">Choisissez un artefact qui présente l’état **Échec**.</span><span class="sxs-lookup"><span data-stu-id="20586-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="20586-118">L’artefact s’ouvre et affiche un message d’extension comportant des détails sur son échec.</span><span class="sxs-lookup"><span data-stu-id="20586-118">The artifact opens and shows an extension message that includes details about the failure of the artifact.</span></span>

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-the-vm"></a><span data-ttu-id="20586-120">Résoudre les échecs des artefacts au sein de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="20586-120">Troubleshoot artifact failures from within the VM</span></span>
<span data-ttu-id="20586-121">Pour afficher les journaux d’artefacts au sein de la machine virtuelle, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="20586-121">To view the artifact logs from within the virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="20586-122">Connectez-vous à la machine virtuelle qui contient l’artefact à diagnostiquer.</span><span class="sxs-lookup"><span data-stu-id="20586-122">Log in to the VM that contains the artifact you want to diagnose.</span></span>

2. <span data-ttu-id="20586-123">Accédez à C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status, « 1.9 » étant le numéro de version CSE.</span><span class="sxs-lookup"><span data-stu-id="20586-123">Navigate to C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is the CSE version number.</span></span>

   ![Exemple de dépôt git d'artefacts](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="20586-125">Ouvrez le fichier **état** pour afficher les informations qui vous aideront à diagnostiquer les échecs d’artefacts de cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="20586-125">Open the **status** file to view information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="20586-126">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="20586-126">Related blog posts</span></span>
* [<span data-ttu-id="20586-127">Joindre une machine virtuelle à un domaine AD existant à l’aide d’un modèle Resource Manager dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="20586-127">Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="20586-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="20586-128">Next steps</span></span>
* <span data-ttu-id="20586-129">Découvrez comment [ajouter un référentiel Git à un labo](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="20586-129">Learn how to [add a Git repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

