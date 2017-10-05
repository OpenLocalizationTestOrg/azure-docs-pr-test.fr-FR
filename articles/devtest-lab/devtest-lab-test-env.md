---
title: Utiliser Azure DevTest Labs pour les environnements de test de machine virtuelle et PaaS | Microsoft Docs
description: "Découvrez comment utiliser Azure DevTest Labs pour les scénarios d’environnements de test de machine virtuelle et PaaS."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: a556cee9d7b665cd7df23c97e7e2c8c2afabbe58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="5671f-103">Utiliser Azure DevTest Labs pour les environnements de test de machine virtuelle et PaaS</span><span class="sxs-lookup"><span data-stu-id="5671f-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="5671f-104">Vous pouvez utiliser Azure DevTest Labs pour implémenter de nombreux scénarios clés, mais un scénario principal implique l’utilisation de DevTest Labs pour héberger des machines à l’usage des testeurs.</span><span class="sxs-lookup"><span data-stu-id="5671f-104">You can use Azure DevTest Labs to implement many key scenarios, but a primary scenario involves using DevTest Labs to host machines for testers.</span></span> 

<span data-ttu-id="5671f-105">Dans ce scénario, DevTest Labs offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5671f-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="5671f-106">Les testeurs peuvent tester la dernière version de l’application en approvisionnant rapidement des environnements Windows et Linux à l’aide d’artefacts et de modèles réutilisables.</span><span class="sxs-lookup"><span data-stu-id="5671f-106">Testers can test the latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="5671f-107">Ils peuvent faire monter en puissance leur test de charge en approvisionnant plusieurs agents de test.</span><span class="sxs-lookup"><span data-stu-id="5671f-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="5671f-108">Les administrateurs peuvent contrôler les coûts en s’assurant que :</span><span class="sxs-lookup"><span data-stu-id="5671f-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="5671f-109">Les testeurs ne peuvent pas obtenir plus de machines virtuelles qu’il n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5671f-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="5671f-110">Les machines virtuelles sont éteintes lorsqu’elles ne sont pas utilisées.</span><span class="sxs-lookup"><span data-stu-id="5671f-110">VMs are shut down when not in use.</span></span>

![Utiliser DevTest Labs à des fins de formation](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="5671f-112">Cet article présente les différentes fonctionnalités d’Azure DevTest Labs utilisées pour satisfaire les exigences du testeur, et détaille la procédure à suivre pour mettre en place un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-112">In this article, you learn about various Azure DevTest Labs features used to meet tester requirements and the detailed steps to follow to set up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="5671f-113">Implémentation d’environnements de test avec Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5671f-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="5671f-114">**Créer le laboratoire**</span><span class="sxs-lookup"><span data-stu-id="5671f-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="5671f-115">Les laboratoires sont le point de départ dans Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="5671f-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="5671f-116">Une fois que vous avez créé un laboratoire, vous pouvez ajouter des utilisateurs (testeurs) au laboratoire, mettre en place des stratégies pour contrôler les coûts, définir des images de machine virtuelle qui peuvent être créées rapidement, etc.</span><span class="sxs-lookup"><span data-stu-id="5671f-116">Once you create a lab, you can perform tasks such as adding users (testers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="5671f-117">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-118">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-118">Task</span></span> | <span data-ttu-id="5671f-119">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-120">Créer un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5671f-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="5671f-121">Découvrez comment créer un laboratoire dans Azure DevTest Labs à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5671f-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="5671f-122">**Créer des machines virtuelles en quelques minutes à l’aide d’images Marketplace prêtes à l’emploi et d’images personnalisées**</span><span class="sxs-lookup"><span data-stu-id="5671f-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="5671f-123">Vous pouvez choisir des images prêtes à l’emploi parmi le large éventail d’images disponible dans Azure Marketplace et les mettre à disposition dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="5671f-124">Si les images prêtes à l’emploi ne répondent pas à vos besoins, vous pouvez créer une image personnalisée de machine virtuelle de laboratoire en utilisant une image prête à l’emploi de la Place de marché Azure, en installant tous les logiciels dont vous avez besoin et en enregistrant la machine virtuelle en tant qu’image personnalisée dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="5671f-125">Si vous utilisez des images personnalisées, n’hésitez pas à utiliser une fabrique d’images pour créer et distribuer vos images.</span><span class="sxs-lookup"><span data-stu-id="5671f-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="5671f-126">Une fabrique d’images est une solution en tant que code de configuration qui crée et distribue vos images configurées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="5671f-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="5671f-127">C’est un gain de temps sur la configuration manuelle du système après la création d’une machine virtuelle avec le système d’exploitation de base.</span><span class="sxs-lookup"><span data-stu-id="5671f-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="5671f-128">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-129">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-129">Task</span></span> | <span data-ttu-id="5671f-130">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-131">Configurer des images Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5671f-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="5671f-132">Découvrez comment mettre sur liste blanche des images Azure Marketplace afin que seules les images souhaitées pour la formation soient sélectionnables pour les testeurs.</span><span class="sxs-lookup"><span data-stu-id="5671f-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the testers.</span></span>|
   | [<span data-ttu-id="5671f-133">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="5671f-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="5671f-134">Créez une image personnalisée en préinstallant les logiciels dont vous avez besoin afin que les testeurs puissent créer rapidement une machine virtuelle à l’aide de cette image.</span><span class="sxs-lookup"><span data-stu-id="5671f-134">Create a custom image by pre-installing the software you need so that testers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="5671f-135">Découvrir la fabrique d’images</span><span class="sxs-lookup"><span data-stu-id="5671f-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="5671f-136">Regardez une vidéo expliquant comment configurer et utiliser une fabrique d’images.</span><span class="sxs-lookup"><span data-stu-id="5671f-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="5671f-137">**Créer des modèles réutilisables pour les machines de test**</span><span class="sxs-lookup"><span data-stu-id="5671f-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="5671f-138">Dans Azure DevTest Labs, une formule est une liste de valeurs de propriétés par défaut utilisée pour créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5671f-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="5671f-139">Vous pouvez créer une formule dans le laboratoire en choisissant une image, une taille de machine virtuelle (une combinaison de puissance processeur et de RAM) et un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5671f-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="5671f-140">Chaque testeur peut accéder à la formule dans le laboratoire et l’utiliser pour créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5671f-140">Each tester can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="5671f-141">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-142">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-142">Task</span></span> | <span data-ttu-id="5671f-143">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-144">Gérer les formules DevTest Labs pour créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="5671f-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="5671f-145">Découvrez comment créer une formule en choisissant une image, une taille de machine virtuelle (une combinaison de puissance processeur et de RAM) et un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5671f-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="5671f-146">**Créer des environnements de test multimachine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="5671f-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="5671f-147">Vous pouvez utiliser des modèles Azure Resource Manager pour définir l’infrastructure et la configuration de votre solution Azure, et de déployer de manière répétée plusieurs machines virtuelles de test dans un état cohérent.</span><span class="sxs-lookup"><span data-stu-id="5671f-147">You can use Azure Resource Manager templates to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="5671f-148">Les ressources PaaS Azure peuvent être approvisionnées dans un environnement à partir d’un modèle Azure Resource Manager et apparaître dans le suivi des coûts.</span><span class="sxs-lookup"><span data-stu-id="5671f-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="5671f-149">Toutefois, l’arrêt automatique de machine virtuelle ne s’applique pas aux ressources PaaS.</span><span class="sxs-lookup"><span data-stu-id="5671f-149">However, VM auto shutdown does not apply to PaaS resources.</span></span>

    <span data-ttu-id="5671f-150">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-151">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-151">Task</span></span> | <span data-ttu-id="5671f-152">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-153">Créer des environnements de plusieurs machines virtuelles et des ressources PaaS avec les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5671f-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="5671f-154">Découvrez comment vous déployer plusieurs machines virtuelles dans un état cohérent pour votre environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5671f-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="5671f-155">**Créer des artefacts pour activer la personnalisation flexible de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="5671f-155">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="5671f-156">Les artefacts sont utilisés pour déployer et configurer votre application après l’approvisionnement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5671f-156">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="5671f-157">Les artefacts peuvent être :</span><span class="sxs-lookup"><span data-stu-id="5671f-157">Artifacts can be:</span></span>

   - <span data-ttu-id="5671f-158">des outils que vous voulez installer sur la machine virtuelle, tels que des agents, Fiddler, Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="5671f-158">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="5671f-159">des actions que vous souhaitez exécuter sur la machine virtuelle, telles que le clonage d’un dépôt ;</span><span class="sxs-lookup"><span data-stu-id="5671f-159">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="5671f-160">des applications que vous voulez tester.</span><span class="sxs-lookup"><span data-stu-id="5671f-160">Applications that you want to test.</span></span>

   <span data-ttu-id="5671f-161">De nombreux artefacts prêts à l’emploi sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="5671f-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="5671f-162">Toutefois, si vos besoins spécifiques requièrent davantage de personnalisation, vous pouvez créer vos propres artefacts personnalisés.</span><span class="sxs-lookup"><span data-stu-id="5671f-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="5671f-163">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-163">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-164">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-164">Task</span></span> | <span data-ttu-id="5671f-165">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-166">Créer des artefacts personnalisés pour vos machines virtuelles DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5671f-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="5671f-167">Créer vos propres artefacts personnalisés pour les machines virtuelles de votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-167">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="5671f-168">Ajouter un référentiel Git pour stocker des artefacts personnalisés et des modèles Azure Resource Manager pour une utilisation dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5671f-168">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="5671f-169">Apprenez à stocker vos artefacts personnalisés dans votre propre référentiel Git privé.</span><span class="sxs-lookup"><span data-stu-id="5671f-169">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="5671f-170">**Contrôle des coûts**</span><span class="sxs-lookup"><span data-stu-id="5671f-170">**Control costs**</span></span>
   
    <span data-ttu-id="5671f-171">Azure DevTest Labs vous permet de mettre en place une stratégie dans le laboratoire pour spécifier le nombre maximal de machines virtuelles qui peuvent être créées par un testeur.</span><span class="sxs-lookup"><span data-stu-id="5671f-171">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a tester in the lab.</span></span> 
   
    <span data-ttu-id="5671f-172">Si votre équipe de test a un planning de travail défini et que vous souhaitez arrêter toutes les machines virtuelles à un moment précis de la journée, puis les redémarrer automatiquement le lendemain, vous pouvez le faire aisément en définissant des stratégies d’arrêt et de démarrage automatiques dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-172">If your test team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="5671f-173">Enfin, une fois le développement de l’application terminé, vous pouvez supprimer toutes les machines virtuelles d’un coup en exécutant un simple script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5671f-173">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="5671f-174">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-174">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-175">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-175">Task</span></span> | <span data-ttu-id="5671f-176">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-177">Définir des stratégies de laboratoire</span><span class="sxs-lookup"><span data-stu-id="5671f-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="5671f-178">Contrôlez les coûts en mettant en place des stratégies dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-178">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="5671f-179">Supprimer toutes les machines virtuelles de laboratoire à l’aide d’un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="5671f-179">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="5671f-180">Une fois les tests terminés, supprimez tous les laboratoires en une seule opération.</span><span class="sxs-lookup"><span data-stu-id="5671f-180">Delete all the labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="5671f-181">**Ajouter un réseau virtuel à un laboratoire**</span><span class="sxs-lookup"><span data-stu-id="5671f-181">**Add a virtual network to a Lab**</span></span> 
   
    <span data-ttu-id="5671f-182">DevTest Labs crée un réseau virtuel (VNET) à chaque création de laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="5671f-183">Si vous avez configuré votre propre réseau virtuel (par exemple, en utilisant ExpressRoute ou un VPN de site à site), vous pouvez l’ajouter aux paramètres de réseau virtuel de votre laboratoire afin qu’il soit disponible lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5671f-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="5671f-184">De plus, un artefact de jonction de domaine Azure Active Directory est disponible, qui lie une machine virtuelle à un domaine dans lequel la machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="5671f-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="5671f-185">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-186">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-186">Task</span></span> | <span data-ttu-id="5671f-187">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-188">Configuration d’un réseau virtuel dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5671f-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="5671f-189">Apprenez à configurer un réseau virtuel dans Azure DevTest Labs à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5671f-189">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="5671f-190">**Partager le laboratoire avec chaque testeur**</span><span class="sxs-lookup"><span data-stu-id="5671f-190">**Share the lab with each tester**</span></span>
   
    <span data-ttu-id="5671f-191">Les laboratoires sont directement accessibles à l’aide d’un lien que vous partagez avec les testeurs.</span><span class="sxs-lookup"><span data-stu-id="5671f-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="5671f-192">Ceux-ci n’ont même pas besoin d’un compte Azure pour autant qu’ils aient un [compte Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="5671f-192">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="5671f-193">Les testeurs ne voient pas les machines virtuelles créées par d’autres testeurs.</span><span class="sxs-lookup"><span data-stu-id="5671f-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="5671f-194">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-194">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-195">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-195">Task</span></span> | <span data-ttu-id="5671f-196">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-197">Ajouter un testeur à un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5671f-197">Add a tester to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="5671f-198">Utilisez le portail Azure pour ajouter des testeurs à votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-198">Use the Azure portal to add testers to your lab.</span></span>|
   | [<span data-ttu-id="5671f-199">Ajouter des testeur au laboratoire à l’aide d’un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="5671f-199">Add testers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="5671f-200">Utilisez PowerShell pour automatiser l’ajout de testeurs à votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="5671f-200">Use PowerShell to automate adding testers to your lab.</span></span> |
   | [<span data-ttu-id="5671f-201">Obtenir un lien vers le laboratoire</span><span class="sxs-lookup"><span data-stu-id="5671f-201">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="5671f-202">Découvrez comment les testeurs peuvent accéder directement à un laboratoire via un lien hypertexte.</span><span class="sxs-lookup"><span data-stu-id="5671f-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="5671f-203">**Automatiser la création de laboratoire pour d’autres équipes**</span><span class="sxs-lookup"><span data-stu-id="5671f-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="5671f-204">Vous pouvez automatiser la création de laboratoires, y compris les paramètres personnalisés, en créant un modèle Resource Manager qui vous permettra de mettre en place des laboratoires identiques à l’infini.</span><span class="sxs-lookup"><span data-stu-id="5671f-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="5671f-205">Pour en savoir plus, cliquez sur les liens du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="5671f-205">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="5671f-206">Task</span><span class="sxs-lookup"><span data-stu-id="5671f-206">Task</span></span> | <span data-ttu-id="5671f-207">Contenu</span><span class="sxs-lookup"><span data-stu-id="5671f-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="5671f-208">Créer un laboratoire à l’aide d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5671f-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="5671f-209">Créez des laboratoires dans Azure DevTest Labs à l’aide de modèles Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5671f-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

