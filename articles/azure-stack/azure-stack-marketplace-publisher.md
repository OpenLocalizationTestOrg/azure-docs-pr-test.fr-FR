---
title: "aaaUse hello Marketplace toolkit toocreate et publier des éléments du marketplace | Documents Microsoft"
description: "Découvrez comment tooquickly créer des éléments du marketplace par hello publication du Kit de ressources"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: ByronR
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: helaw
ms.openlocfilehash: c1cf9ad1da44787901297eec12faf2a3dea82a6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a><span data-ttu-id="8d255-103">Ajouter des éléments de Place de Marché à l’aide de l’outil de publication</span><span class="sxs-lookup"><span data-stu-id="8d255-103">Add marketplace items using publishing tool</span></span>
<span data-ttu-id="8d255-104">Ajout de votre contenu toohello [Azure Marketplace de pile](azure-stack-marketplace.md) rend votre tooyou disponibles de solutions et de vos clients pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8d255-104">Adding your content toohello [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available tooyou and your tenants for deployment.</span></span>  <span data-ttu-id="8d255-105">Hello Marketplace Toolkit crée des fichiers Azure Marketplace Packages (.azpkg) en fonction de vos modèles IaaS Azure Resource Manager ou les Extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8d255-105">hello Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span></span>  <span data-ttu-id="8d255-106">Vous pouvez également utiliser des fichiers de .azpkg toopublish hello Marketplace Toolkit, soit créé avec l’outil de hello ou à l’aide de [manuelle](azure-stack-create-and-publish-marketplace-item.md) étapes.</span><span class="sxs-lookup"><span data-stu-id="8d255-106">You can also use hello Marketplace Toolkit toopublish .azpkg files, either created with hello tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span></span>  <span data-ttu-id="8d255-107">Cette rubrique vous guide de téléchargement hello outil, création d’un élément de marketplace basé sur un modèle d’ordinateur virtuel, puis publier ce toohello élément Azure Marketplace de pile.</span><span class="sxs-lookup"><span data-stu-id="8d255-107">This topic guides you through downloading hello tool, creating a marketplace item based on a VM template, and then publishing that item toohello Azure Stack Marketplace.</span></span>     


## <a name="prerequisites"></a><span data-ttu-id="8d255-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8d255-108">Prerequisites</span></span>
 - <span data-ttu-id="8d255-109">Vous devez exécuter hello toolkit sur l’ordinateur hôte de pile de Azure hello ou avez [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivité à partir de l’ordinateur hello sur lequel vous exécutez l’outil de hello.</span><span class="sxs-lookup"><span data-stu-id="8d255-109">You must run hello toolkit on hello Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from hello machine where you run hello tool.</span></span>

 - <span data-ttu-id="8d255-110">Télécharger hello [modèles de démarrage rapide de pile Azure](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) et extraire.</span><span class="sxs-lookup"><span data-stu-id="8d255-110">Download hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span></span>

 - <span data-ttu-id="8d255-111">Télécharger hello [outil d’empaquetage de la galerie Azure](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span><span class="sxs-lookup"><span data-stu-id="8d255-111">Download hello [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span></span> 

 - <span data-ttu-id="8d255-112">Publication toohello marketplace nécessite des icônes et un fichier de miniature.</span><span class="sxs-lookup"><span data-stu-id="8d255-112">Publishing toohello marketplace requires icons and a thumbnail file.</span></span>  <span data-ttu-id="8d255-113">Vous pouvez utiliser votre propre, ou enregistrer hello [exemple](azure-stack-marketplace-publisher.md#support-files) fichiers localement pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="8d255-113">You can use your own, or save hello [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span></span>

## <a name="download-hello-tool"></a><span data-ttu-id="8d255-114">Télécharger l’outil de hello</span><span class="sxs-lookup"><span data-stu-id="8d255-114">Download hello tool</span></span>
<span data-ttu-id="8d255-115">Hello Marketplace Toolkit peut être [téléchargé à partir du référentiel de pile de Azure Tools hello](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="8d255-115">hello Marketplace Toolkit can be [downloaded from hello Azure Stack Tools repo](azure-stack-powershell-download.md).</span></span>


##  <a name="create-marketplace-items"></a><span data-ttu-id="8d255-116">Créer des éléments de Place de Marché</span><span class="sxs-lookup"><span data-stu-id="8d255-116">Create marketplace items</span></span>
<span data-ttu-id="8d255-117">Dans cette section, vous utilisez hello Marketplace Toolkit toocreate un package de l’élément marketplace .azpkg format.</span><span class="sxs-lookup"><span data-stu-id="8d255-117">In this section, you use hello Marketplace Toolkit toocreate a marketplace item package in .azpkg format.</span></span>  

### <a name="provide-marketplace-information-with-wizard"></a><span data-ttu-id="8d255-118">Fournir des informations de Place de Marché avec l’Assistant</span><span class="sxs-lookup"><span data-stu-id="8d255-118">Provide marketplace information with wizard</span></span>
1. <span data-ttu-id="8d255-119">À partir d’une session PowerShell, exécutez hello Marketplace Toolkit :</span><span class="sxs-lookup"><span data-stu-id="8d255-119">Run hello Marketplace Toolkit from a PowerShell session:</span></span>
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. <span data-ttu-id="8d255-120">Cliquez sur hello **Solution** onglet.  Cet écran accepte des informations sur votre élément de Place de Marché.</span><span class="sxs-lookup"><span data-stu-id="8d255-120">Click hello **Solution** tab.  This screen accepts information about your marketplace item.</span></span> <span data-ttu-id="8d255-121">Entrer des informations sur l’objet que vous le souhaitez tooappear dans marketplace de hello.</span><span class="sxs-lookup"><span data-stu-id="8d255-121">Enter information about your item as you want it tooappear in hello marketplace.</span></span>  <span data-ttu-id="8d255-122">Vous pouvez également spécifier un [fichier de paramètres](azure-stack-marketplace-publisher.md#use-a-parameters-file) formulaire de hello tooprepopulate.</span><span class="sxs-lookup"><span data-stu-id="8d255-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) tooprepopulate hello form.</span></span>  
    
    ![capture d’écran du premier écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image7.png)
3. <span data-ttu-id="8d255-124">Cliquez sur **Parcourir** et sélectionnez un fichier image pour chaque champ d’icône et de capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="8d255-124">Click **Browse** and select an image file for each icon and screenshot field.</span></span>  <span data-ttu-id="8d255-125">Vous pouvez utiliser vos propres icônes ou hello icônes exemple hello [prennent en charge les fichiers](azure-stack-marketplace-publisher.md#support-files) section.</span><span class="sxs-lookup"><span data-stu-id="8d255-125">You can use your own icons, or hello sample icons in hello [support files](azure-stack-marketplace-publisher.md#support-files) section.</span></span>
4. <span data-ttu-id="8d255-126">Une fois que tous les champs sont remplis, sélectionnez « Aperçu de la Solution » pour afficher un aperçu de la solution hello dans hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8d255-126">Once all fields are populated, select "Preview Solution" for a preview of hello solution within hello Marketplace.</span></span>  <span data-ttu-id="8d255-127">Vous pouvez réviser et modifier le texte hello, des images et capture d’écran avant de cliquer sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="8d255-127">You can revise and edit hello text, images, and screenshot before clicking **Next**.</span></span>  

### <a name="import-template-and-create-package"></a><span data-ttu-id="8d255-128">Importer le modèle et créer le package</span><span class="sxs-lookup"><span data-stu-id="8d255-128">Import template and create package</span></span>
<span data-ttu-id="8d255-129">Dans cette section, vous importez le modèle de hello et fonctionne avec une entrée pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="8d255-129">In this section, you import hello template and work with input for your solution.</span></span>

1.  <span data-ttu-id="8d255-130">Cliquez sur **Parcourir** et sélectionnez hello *azuredeploy.json* à partir du dossier 101-Simple-Windows-VM hello Bonjour téléchargé les modèles.</span><span class="sxs-lookup"><span data-stu-id="8d255-130">Click **Browse** and select hello *azuredeploy.json* from hello 101-Simple-Windows-VM folder in hello downloaded templates.</span></span>

    ![capture d’écran du deuxième écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image8.png)
2.  <span data-ttu-id="8d255-132">Assistant Déploiement Hello est rempli avec un *base* éléments d’entrée et l’étape pour chaque paramètre spécifié dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="8d255-132">hello Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in hello template.</span></span>  <span data-ttu-id="8d255-133">Vous pouvez ajouter des étapes supplémentaires et déplacer des entrées d’une étape à une autre.</span><span class="sxs-lookup"><span data-stu-id="8d255-133">You can add additional steps and move inputs between steps.</span></span>  <span data-ttu-id="8d255-134">Par exemple, vous souhaiterez peut-être avoir des étapes « Configuration frontale » et « Configuration backend » pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="8d255-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span></span>
3.  <span data-ttu-id="8d255-135">Spécifiez hello chemin d’accès tooAzureGalleryPackager.exe.</span><span class="sxs-lookup"><span data-stu-id="8d255-135">Specify hello path tooAzureGalleryPackager.exe.</span></span>  
4.  <span data-ttu-id="8d255-136">Cliquez sur **créer** et hello Marketplace Toolkit empaquette votre solution dans un fichier .azpkg.</span><span class="sxs-lookup"><span data-stu-id="8d255-136">Click **Create** and hello Marketplace Toolkit packages your solution into an .azpkg file.</span></span>  <span data-ttu-id="8d255-137">Une fois terminé, Assistant de hello affiche permettent de vous hello toocontinue option votre tooAzure package pile de publication et du fichier de solution de tooyour de chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="8d255-137">Once complete, hello wizard displays hello path tooyour solution file and give you hello option toocontinue publishing your package tooAzure Stack.</span></span>


## <a name="publish-marketplace-items"></a><span data-ttu-id="8d255-138">Publier des éléments de Place de Marché</span><span class="sxs-lookup"><span data-stu-id="8d255-138">Publish marketplace items</span></span>
<span data-ttu-id="8d255-139">Dans cette section, vous publiez hello marketplace élément tooyour Azure Marketplace de pile.</span><span class="sxs-lookup"><span data-stu-id="8d255-139">In this section, you publish hello marketplace item tooyour Azure Stack Marketplace.</span></span>

![capture d’écran du premier écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image9.png)

1.  <span data-ttu-id="8d255-141">Assistant de Hello nécessite des informations toopublish votre solution :</span><span class="sxs-lookup"><span data-stu-id="8d255-141">hello wizard requires information toopublish your solution:</span></span>
    
    |<span data-ttu-id="8d255-142">Champ</span><span class="sxs-lookup"><span data-stu-id="8d255-142">Field</span></span>|<span data-ttu-id="8d255-143">Description</span><span class="sxs-lookup"><span data-stu-id="8d255-143">Description</span></span>|
    |-----|-----|
    | <span data-ttu-id="8d255-144">Nom de l’administrateur de service</span><span class="sxs-lookup"><span data-stu-id="8d255-144">Service Admin Name</span></span> | <span data-ttu-id="8d255-145">Compte de l’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="8d255-145">Service Administrator account.</span></span>  <span data-ttu-id="8d255-146">Exemple : ServiceAdmin@mydomain.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="8d255-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span></span> |
    | <span data-ttu-id="8d255-147">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="8d255-147">Password</span></span> | <span data-ttu-id="8d255-148">Mot de passe du compte d’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="8d255-148">Password for Service Administrator account.</span></span> |
    | <span data-ttu-id="8d255-149">Point de terminaison d’API</span><span class="sxs-lookup"><span data-stu-id="8d255-149">API Endpoint</span></span> | <span data-ttu-id="8d255-150">Point de terminaison Azure Resource Manager Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8d255-150">Azure Stack Azure Resource Manager endpoint.</span></span>  <span data-ttu-id="8d255-151">Exemple : management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="8d255-151">Example: management.local.azurestack.external</span></span> |
2.  <span data-ttu-id="8d255-152">Cliquez sur **publier** et journal de publication hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8d255-152">Click **Publish** and hello publishing log is displayed.</span></span>
3.  <span data-ttu-id="8d255-153">Vous est désormais en mesure de toodeploy votre élément publié via le portail d’Azure pile hello.</span><span class="sxs-lookup"><span data-stu-id="8d255-153">You are now able toodeploy your published item via hello Azure Stack portal.</span></span>


## <a name="use-a-parameters-file"></a><span data-ttu-id="8d255-154">Utiliser un fichier de paramètres</span><span class="sxs-lookup"><span data-stu-id="8d255-154">Use a parameters file</span></span>
<span data-ttu-id="8d255-155">Vous pouvez également utiliser un fichier toocomplete hello marketplace élément informations relatives aux paramètres.</span><span class="sxs-lookup"><span data-stu-id="8d255-155">You can also use a parameters file toocomplete hello marketplace item information.</span></span>  

<span data-ttu-id="8d255-156">Hello Marketplace Toolkit inclut une *solution.parameters.ps1* vous pouvez utiliser toocreate votre propre fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="8d255-156">hello Marketplace Toolkit includes a *solution.parameters.ps1* you can use toocreate your own parameters file.</span></span>


## <a name="support-files"></a><span data-ttu-id="8d255-157">Fichiers de prise en charge</span><span class="sxs-lookup"><span data-stu-id="8d255-157">Support files</span></span>
| <span data-ttu-id="8d255-158">Description</span><span class="sxs-lookup"><span data-stu-id="8d255-158">Description</span></span> | <span data-ttu-id="8d255-159">Exemple</span><span class="sxs-lookup"><span data-stu-id="8d255-159">Sample</span></span> |
| ----- | ----- |
| <span data-ttu-id="8d255-160">icône .png de 40x40</span><span class="sxs-lookup"><span data-stu-id="8d255-160">40x40 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| <span data-ttu-id="8d255-161">icône .png de 90x90</span><span class="sxs-lookup"><span data-stu-id="8d255-161">90x90 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| <span data-ttu-id="8d255-162">icône .png de 115x115</span><span class="sxs-lookup"><span data-stu-id="8d255-162">115x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| <span data-ttu-id="8d255-163">icône .png de 255x115</span><span class="sxs-lookup"><span data-stu-id="8d255-163">255x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| <span data-ttu-id="8d255-164">Miniature .png de 533x324</span><span class="sxs-lookup"><span data-stu-id="8d255-164">533x324 .png thumbnail</span></span> | ![](./media/azure-stack-marketplace-publisher/image5.png) |


