---
title: "Utiliser la boîte à outils Place de Marché pour créer et publier des éléments de Place de Marché | Microsoft Docs"
description: "Découvrez comment créer rapidement des éléments de Place de Marché avec la boîte à outils de publication."
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
ms.openlocfilehash: 5b2c04d2cbc06e1572dc2e40712f6cf9d886aa1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a><span data-ttu-id="0caa4-103">Ajouter des éléments de Place de Marché à l’aide de l’outil de publication</span><span class="sxs-lookup"><span data-stu-id="0caa4-103">Add marketplace items using publishing tool</span></span>
<span data-ttu-id="0caa4-104">L’ajout de votre contenu à la [Place de Marché Azure Stack](azure-stack-marketplace.md) met vos solutions à disposition de vos locataires (et de vous-même) pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="0caa4-104">Adding your content to the [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available to you and your tenants for deployment.</span></span>  <span data-ttu-id="0caa4-105">La boîte à outils Place de Marché crée des fichiers de packages Place de Marché Azure (.azpkg) basés sur vos extensions de machine virtuelle ou vos modèles IaaS Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0caa4-105">The Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span></span>  <span data-ttu-id="0caa4-106">Vous pouvez également utiliser la boîte à outils Place de Marché pour publier des fichiers .azpkg créés avec l’outil ou par le biais d’étapes [manuelles](azure-stack-create-and-publish-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="0caa4-106">You can also use the Marketplace Toolkit to publish .azpkg files, either created with the tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span></span>  <span data-ttu-id="0caa4-107">Cette rubrique vous montre comment télécharger l’outil, créer un élément de Place de Marché basé sur un modèle de machine virtuelle, puis publier cet élément sur la Place de Marché Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="0caa4-107">This topic guides you through downloading the tool, creating a marketplace item based on a VM template, and then publishing that item to the Azure Stack Marketplace.</span></span>     


## <a name="prerequisites"></a><span data-ttu-id="0caa4-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0caa4-108">Prerequisites</span></span>
 - <span data-ttu-id="0caa4-109">Vous devez exécuter la boîte à outils sur l’hôte Azure Stack ou disposer d’une connectivité [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) à partir de l’ordinateur sur lequel vous exécutez l’outil.</span><span class="sxs-lookup"><span data-stu-id="0caa4-109">You must run the toolkit on the Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from the machine where you run the tool.</span></span>

 - <span data-ttu-id="0caa4-110">Téléchargez les [modèles de démarrage rapide Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) et effectuez leur extraction.</span><span class="sxs-lookup"><span data-stu-id="0caa4-110">Download the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span></span>

 - <span data-ttu-id="0caa4-111">Téléchargez l’[outil d’empaquetage de la galerie Azure](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span><span class="sxs-lookup"><span data-stu-id="0caa4-111">Download the [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span></span> 

 - <span data-ttu-id="0caa4-112">La publication sur la Place de Marché nécessite des icônes et un fichier de miniature.</span><span class="sxs-lookup"><span data-stu-id="0caa4-112">Publishing to the marketplace requires icons and a thumbnail file.</span></span>  <span data-ttu-id="0caa4-113">Vous pouvez utiliser vos propres fichiers ou enregistrer les [exemples](azure-stack-marketplace-publisher.md#support-files) de fichiers localement pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="0caa4-113">You can use your own, or save the [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span></span>

## <a name="download-the-tool"></a><span data-ttu-id="0caa4-114">Télécharger l’outil</span><span class="sxs-lookup"><span data-stu-id="0caa4-114">Download the tool</span></span>
<span data-ttu-id="0caa4-115">Vous pouvez [télécharger la boîte à outils Place de Marché à partir du dépôt d’outils Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="0caa4-115">The Marketplace Toolkit can be [downloaded from the Azure Stack Tools repo](azure-stack-powershell-download.md).</span></span>


##  <a name="create-marketplace-items"></a><span data-ttu-id="0caa4-116">Créer des éléments de Place de Marché</span><span class="sxs-lookup"><span data-stu-id="0caa4-116">Create marketplace items</span></span>
<span data-ttu-id="0caa4-117">Dans cette section, vous allez utiliser la boîte à outils Place de Marché pour créer un package d’élément Place de Marché au format .azpkg.</span><span class="sxs-lookup"><span data-stu-id="0caa4-117">In this section, you use the Marketplace Toolkit to create a marketplace item package in .azpkg format.</span></span>  

### <a name="provide-marketplace-information-with-wizard"></a><span data-ttu-id="0caa4-118">Fournir des informations de Place de Marché avec l’Assistant</span><span class="sxs-lookup"><span data-stu-id="0caa4-118">Provide marketplace information with wizard</span></span>
1. <span data-ttu-id="0caa4-119">Exécutez la boîte à outils Place de Marché à partir d’une session PowerShell :</span><span class="sxs-lookup"><span data-stu-id="0caa4-119">Run the Marketplace Toolkit from a PowerShell session:</span></span>
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. <span data-ttu-id="0caa4-120">Cliquez sur l’onglet **Solution**.  Cet écran accepte des informations sur votre élément de Place de Marché.</span><span class="sxs-lookup"><span data-stu-id="0caa4-120">Click the **Solution** tab.  This screen accepts information about your marketplace item.</span></span> <span data-ttu-id="0caa4-121">Entrez des informations sur votre élément, telles que vous souhaitez qu’elles apparaissent sur la Place de Marché.</span><span class="sxs-lookup"><span data-stu-id="0caa4-121">Enter information about your item as you want it to appear in the marketplace.</span></span>  <span data-ttu-id="0caa4-122">Vous pouvez également spécifier un [fichier de paramètres](azure-stack-marketplace-publisher.md#use-a-parameters-file) pour préremplir le formulaire.</span><span class="sxs-lookup"><span data-stu-id="0caa4-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) to prepopulate the form.</span></span>  
    
    ![capture d’écran du premier écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image7.png)
3. <span data-ttu-id="0caa4-124">Cliquez sur **Parcourir** et sélectionnez un fichier image pour chaque champ d’icône et de capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="0caa4-124">Click **Browse** and select an image file for each icon and screenshot field.</span></span>  <span data-ttu-id="0caa4-125">Vous pouvez utiliser vos propres icônes ou les exemples fournis dans la section [Fichiers de prise en charge](azure-stack-marketplace-publisher.md#support-files).</span><span class="sxs-lookup"><span data-stu-id="0caa4-125">You can use your own icons, or the sample icons in the [support files](azure-stack-marketplace-publisher.md#support-files) section.</span></span>
4. <span data-ttu-id="0caa4-126">Une fois tous les champs renseignés, sélectionnez « Aperçu de la solution » pour afficher un aperçu de la solution sur la Place de Marché.</span><span class="sxs-lookup"><span data-stu-id="0caa4-126">Once all fields are populated, select "Preview Solution" for a preview of the solution within the Marketplace.</span></span>  <span data-ttu-id="0caa4-127">Vous pouvez réviser et modifier le texte, les images et la capture d’écran avant de cliquer sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0caa4-127">You can revise and edit the text, images, and screenshot before clicking **Next**.</span></span>  

### <a name="import-template-and-create-package"></a><span data-ttu-id="0caa4-128">Importer le modèle et créer le package</span><span class="sxs-lookup"><span data-stu-id="0caa4-128">Import template and create package</span></span>
<span data-ttu-id="0caa4-129">Dans cette section, vous allez importer le modèle et utiliser l’entrée pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="0caa4-129">In this section, you import the template and work with input for your solution.</span></span>

1.  <span data-ttu-id="0caa4-130">Cliquez sur **Parcourir** et sélectionnez le fichier *azuredeploy.json* dans le dossier 101-Simple-Windows-VM dans les modèles téléchargés.</span><span class="sxs-lookup"><span data-stu-id="0caa4-130">Click **Browse** and select the *azuredeploy.json* from the 101-Simple-Windows-VM folder in the downloaded templates.</span></span>

    ![capture d’écran du deuxième écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image8.png)
2.  <span data-ttu-id="0caa4-132">L’Assistant Déploiement est renseigné avec une étape *De base* et des éléments d’entrée pour chaque paramètre spécifié dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="0caa4-132">The Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in the template.</span></span>  <span data-ttu-id="0caa4-133">Vous pouvez ajouter des étapes supplémentaires et déplacer des entrées d’une étape à une autre.</span><span class="sxs-lookup"><span data-stu-id="0caa4-133">You can add additional steps and move inputs between steps.</span></span>  <span data-ttu-id="0caa4-134">Par exemple, vous souhaiterez peut-être avoir des étapes « Configuration frontale » et « Configuration backend » pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="0caa4-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span></span>
3.  <span data-ttu-id="0caa4-135">Spécifiez le chemin vers AzureGalleryPackager.exe.</span><span class="sxs-lookup"><span data-stu-id="0caa4-135">Specify the path to AzureGalleryPackager.exe.</span></span>  
4.  <span data-ttu-id="0caa4-136">Cliquez sur **Créer**. La boîte à outils Place de Marché empaquète votre solution dans un fichier .azpkg.</span><span class="sxs-lookup"><span data-stu-id="0caa4-136">Click **Create** and the Marketplace Toolkit packages your solution into an .azpkg file.</span></span>  <span data-ttu-id="0caa4-137">Une fois terminé, l’Assistant affiche le chemin de votre fichier de solution et vous donne la possibilité de continuer à publier votre package sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="0caa4-137">Once complete, the wizard displays the path to your solution file and give you the option to continue publishing your package to Azure Stack.</span></span>


## <a name="publish-marketplace-items"></a><span data-ttu-id="0caa4-138">Publier des éléments de Place de Marché</span><span class="sxs-lookup"><span data-stu-id="0caa4-138">Publish marketplace items</span></span>
<span data-ttu-id="0caa4-139">Dans cette section, vous allez publier l’élément de Place de Marché sur votre Place de Marché Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="0caa4-139">In this section, you publish the marketplace item to your Azure Stack Marketplace.</span></span>

![capture d’écran du premier écran de la boîte à outils Place de Marché](./media/azure-stack-marketplace-publisher/image9.png)

1.  <span data-ttu-id="0caa4-141">L’Assistant a besoin d’informations pour publier votre solution :</span><span class="sxs-lookup"><span data-stu-id="0caa4-141">The wizard requires information to publish your solution:</span></span>
    
    |<span data-ttu-id="0caa4-142">Champ</span><span class="sxs-lookup"><span data-stu-id="0caa4-142">Field</span></span>|<span data-ttu-id="0caa4-143">Description</span><span class="sxs-lookup"><span data-stu-id="0caa4-143">Description</span></span>|
    |-----|-----|
    | <span data-ttu-id="0caa4-144">Nom de l’administrateur de service</span><span class="sxs-lookup"><span data-stu-id="0caa4-144">Service Admin Name</span></span> | <span data-ttu-id="0caa4-145">Compte de l’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="0caa4-145">Service Administrator account.</span></span>  <span data-ttu-id="0caa4-146">Exemple : ServiceAdmin@mydomain.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="0caa4-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span></span> |
    | <span data-ttu-id="0caa4-147">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="0caa4-147">Password</span></span> | <span data-ttu-id="0caa4-148">Mot de passe du compte d’administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="0caa4-148">Password for Service Administrator account.</span></span> |
    | <span data-ttu-id="0caa4-149">Point de terminaison d’API</span><span class="sxs-lookup"><span data-stu-id="0caa4-149">API Endpoint</span></span> | <span data-ttu-id="0caa4-150">Point de terminaison Azure Resource Manager Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="0caa4-150">Azure Stack Azure Resource Manager endpoint.</span></span>  <span data-ttu-id="0caa4-151">Exemple : management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="0caa4-151">Example: management.local.azurestack.external</span></span> |
2.  <span data-ttu-id="0caa4-152">Cliquez sur **Publier**. Le journal de publication apparaît.</span><span class="sxs-lookup"><span data-stu-id="0caa4-152">Click **Publish** and the publishing log is displayed.</span></span>
3.  <span data-ttu-id="0caa4-153">Vous pouvez désormais déployer votre élément publié par le biais du portail Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="0caa4-153">You are now able to deploy your published item via the Azure Stack portal.</span></span>


## <a name="use-a-parameters-file"></a><span data-ttu-id="0caa4-154">Utiliser un fichier de paramètres</span><span class="sxs-lookup"><span data-stu-id="0caa4-154">Use a parameters file</span></span>
<span data-ttu-id="0caa4-155">Vous pouvez également utiliser un fichier de paramètres pour renseigner les informations de Place de Marché.</span><span class="sxs-lookup"><span data-stu-id="0caa4-155">You can also use a parameters file to complete the marketplace item information.</span></span>  

<span data-ttu-id="0caa4-156">La boîte à outils Place de Marché comprend un fichier *solution.parameters.ps1* que vous pouvez utiliser pour créer votre propre fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="0caa4-156">The Marketplace Toolkit includes a *solution.parameters.ps1* you can use to create your own parameters file.</span></span>


## <a name="support-files"></a><span data-ttu-id="0caa4-157">Fichiers de prise en charge</span><span class="sxs-lookup"><span data-stu-id="0caa4-157">Support files</span></span>
| <span data-ttu-id="0caa4-158">Description</span><span class="sxs-lookup"><span data-stu-id="0caa4-158">Description</span></span> | <span data-ttu-id="0caa4-159">Exemple</span><span class="sxs-lookup"><span data-stu-id="0caa4-159">Sample</span></span> |
| ----- | ----- |
| <span data-ttu-id="0caa4-160">icône .png de 40x40</span><span class="sxs-lookup"><span data-stu-id="0caa4-160">40x40 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| <span data-ttu-id="0caa4-161">icône .png de 90x90</span><span class="sxs-lookup"><span data-stu-id="0caa4-161">90x90 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| <span data-ttu-id="0caa4-162">icône .png de 115x115</span><span class="sxs-lookup"><span data-stu-id="0caa4-162">115x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| <span data-ttu-id="0caa4-163">icône .png de 255x115</span><span class="sxs-lookup"><span data-stu-id="0caa4-163">255x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| <span data-ttu-id="0caa4-164">Miniature .png de 533x324</span><span class="sxs-lookup"><span data-stu-id="0caa4-164">533x324 .png thumbnail</span></span> | ![](./media/azure-stack-marketplace-publisher/image5.png) |


