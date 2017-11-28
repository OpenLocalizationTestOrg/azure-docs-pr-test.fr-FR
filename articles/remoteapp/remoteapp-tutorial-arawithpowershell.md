---
title: Utiliser les applets de commande PowerShell avec Azure RemoteApp | Microsoft Docs
description: "Apprenez à utiliser les applets de commande Windows PowerShell dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="1939f-103">Utiliser les applets de commande Windows PowerShell avec Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1939f-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1939f-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="1939f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1939f-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="1939f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="1939f-106">Vous pouvez utiliser les applets de commande PowerShell pour Azure RemoteApp afin d’administrer et de gérer vos collections.</span><span class="sxs-lookup"><span data-stu-id="1939f-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span></span> <span data-ttu-id="1939f-107">Utilisez les informations suivantes pour commencer.</span><span class="sxs-lookup"><span data-stu-id="1939f-107">Use the following information to get started.</span></span>

## <a name="get-the-cmdlets"></a><span data-ttu-id="1939f-108">Récupération des applets de commande</span><span class="sxs-lookup"><span data-stu-id="1939f-108">Get the cmdlets</span></span>
- - -
<span data-ttu-id="1939f-109">Téléchargez d’abord les applets de commande Azure PowerShell [ici](http://go.microsoft.com/?linkid=9811175); les applets de commande RemoteApp sont incluses.</span><span class="sxs-lookup"><span data-stu-id="1939f-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="1939f-110">Consultez [l’aide sur les applets de commande Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="1939f-110">Check out the [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a><span data-ttu-id="1939f-111">Configuration des applets de commande Azure pour utiliser votre abonnement</span><span class="sxs-lookup"><span data-stu-id="1939f-111">Configure Azure cmdlets to use your subscription</span></span>
- - -
<span data-ttu-id="1939f-112">Suivez [ce guide](/powershell/azure/overview) pour apprendre à utiliser les applets de commande sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1939f-112">Follow [this guide](/powershell/azure/overview) so you can use the cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="1939f-113">Vous pouvez utiliser ces étapes pour démarrer rapidement :</span><span class="sxs-lookup"><span data-stu-id="1939f-113">You can use these steps to get started quickly:</span></span>

1. <span data-ttu-id="1939f-114">Téléchargez et installez les applets de commande [Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="1939f-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="1939f-115">Lancez Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1939f-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="1939f-116">Exécutez **Add-AzureAccount** pour vous authentifier auprès de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1939f-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span></span> <span data-ttu-id="1939f-117">À l’invite, entrez le nom d’utilisateur et le mot de passe que vous utilisez pour vous connecter au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1939f-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span></span>  
4. <span data-ttu-id="1939f-118">Exécutez **Get-AzureSubscription** pour répertorier les abonnements associés à votre compte utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1939f-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="1939f-119">Exécutez **Select-AzureSubscription - SubscriptionName &lt;Nom de l’abonnement&gt;** ou **Select-AzureSubscription - SubscriptionId &lt;ID de l’abonnement&gt;** pour spécifier l’abonnement à utiliser.</span><span class="sxs-lookup"><span data-stu-id="1939f-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** to specify the subscription to use.</span></span>

<span data-ttu-id="1939f-120">Félicitations, votre console Azure PowerShell est configurée et opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="1939f-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span></span> <span data-ttu-id="1939f-121">N'oubliez pas que vous devez répéter les étapes 2 à 5 chaque fois que vous démarrez la console Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1939f-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="1939f-122">Afficher la liste de toutes les collections</span><span class="sxs-lookup"><span data-stu-id="1939f-122">List all collections</span></span>
- - -
     <span data-ttu-id="1939f-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1939f-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="1939f-124">Supprimer une collection</span><span class="sxs-lookup"><span data-stu-id="1939f-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="1939f-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="1939f-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="1939f-126">Exemple : `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="1939f-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="1939f-127">Création d'une collection cloud</span><span class="sxs-lookup"><span data-stu-id="1939f-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="1939f-128">Exécutez simplement la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1939f-128">It's simple, run the following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="1939f-129">La commande ci-dessus publie automatiquement les applications Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio et Word).</span><span class="sxs-lookup"><span data-stu-id="1939f-129">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="1939f-130">La création de la collection peut prendre 30 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="1939f-130">Collection creation can take 30 minutes or longer to complete.</span></span> <span data-ttu-id="1939f-131">Par conséquent, cette commande renvoie un ID de suivi que vous pouvez utiliser de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="1939f-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="1939f-132">Une fois la collection terminée, vous pouvez ajouter des utilisateurs à la collection avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1939f-132">After the collection is done, you can add users to the collection with the following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="1939f-133">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="1939f-133">And you're done!</span></span> <span data-ttu-id="1939f-134">Cet utilisateur doit pouvoir se connecter à l’application à l’aide du client Azure RemoteApp disponible [ici](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="1939f-134">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="1939f-135">Applets de commande disponibles</span><span class="sxs-lookup"><span data-stu-id="1939f-135">Available cmdlets</span></span>
<span data-ttu-id="1939f-136">Nous proposons de nombreuses autres commandes. Leur documentation sera disponible prochainement :</span><span class="sxs-lookup"><span data-stu-id="1939f-136">There are lots of other commands that we have, the documentation for them will be coming shortly:</span></span>

<span data-ttu-id="1939f-137">Applets de commande de base de la collection RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="1939f-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="1939f-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1939f-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1939f-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1939f-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1939f-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1939f-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1939f-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1939f-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1939f-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1939f-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1939f-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1939f-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1939f-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1939f-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1939f-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1939f-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1939f-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="1939f-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="1939f-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="1939f-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="1939f-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="1939f-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="1939f-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="1939f-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="1939f-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1939f-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1939f-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="1939f-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="1939f-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1939f-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1939f-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1939f-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1939f-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="1939f-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="1939f-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="1939f-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="1939f-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="1939f-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="1939f-157">Applets de commande du réseau virtuel RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="1939f-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="1939f-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1939f-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1939f-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1939f-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1939f-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1939f-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1939f-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1939f-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1939f-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="1939f-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="1939f-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="1939f-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="1939f-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="1939f-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="1939f-165">Applets de commande de l’image du modèle RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="1939f-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="1939f-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1939f-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1939f-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1939f-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1939f-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1939f-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1939f-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1939f-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="1939f-170">Autres applets de commande RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="1939f-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="1939f-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="1939f-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="1939f-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="1939f-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="1939f-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="1939f-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="1939f-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="1939f-174">Get-AzureRemoteAppOperationResult</span></span>

