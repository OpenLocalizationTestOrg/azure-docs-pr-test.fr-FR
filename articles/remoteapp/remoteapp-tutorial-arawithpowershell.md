---
title: aaaUse avec Azure RemoteApp, les applets de commande PowerShell | Documents Microsoft
description: "Découvrez comment toouse applets de commande Windows PowerShell dans Azure RemoteApp."
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
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="098b1-103">Utiliser les applets de commande Windows PowerShell avec Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="098b1-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="098b1-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="098b1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="098b1-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="098b1-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="098b1-106">Vous pouvez utiliser des tooadminister d’applets de commande PowerShell de Azure RemoteApp hello et mettre à jour de vos collections.</span><span class="sxs-lookup"><span data-stu-id="098b1-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="098b1-107">Utilisez hello suivant tooget informations a démarré.</span><span class="sxs-lookup"><span data-stu-id="098b1-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="098b1-108">Obtenir les applets de commande hello</span><span class="sxs-lookup"><span data-stu-id="098b1-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="098b1-109">Tout d’abord télécharger les applets de commande Powershell Azure hello [ici](http://go.microsoft.com/?linkid=9811175), applets de commande hello RemoteApp sont inclus.</span><span class="sxs-lookup"><span data-stu-id="098b1-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="098b1-110">Extraire hello [aide d’applet de commande Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="098b1-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="098b1-111">Configurer les applets de commande Azure toouse votre abonnement</span><span class="sxs-lookup"><span data-stu-id="098b1-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="098b1-112">Suivez [ce guide](/powershell/azure/overview) afin de pouvoir utiliser les applets de commande hello sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="098b1-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="098b1-113">Vous pouvez utiliser ces tooget étapes démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="098b1-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="098b1-114">Téléchargez et installez hello [applets de commande Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="098b1-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="098b1-115">Lancez Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="098b1-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="098b1-116">Exécutez **Add-AzureAccount** tooauthenticate tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="098b1-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="098b1-117">Lorsque vous y êtes invité, entrez hello du même nom d’utilisateur et mot de passe que vous utilisez toosign dans tooAzure portal.</span><span class="sxs-lookup"><span data-stu-id="098b1-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="098b1-118">Exécutez **Get-AzureSubscription** les abonnements de hello toolist associés à votre compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="098b1-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="098b1-119">Exécutez **Select-AzureSubscription - SubscriptionName &lt;nom de l’abonnement&gt;**  ou **Select-AzureSubscription - SubscriptionId &lt;ID d’abonnement&gt;**  toospecify hello abonnement toouse.</span><span class="sxs-lookup"><span data-stu-id="098b1-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="098b1-120">Félicitations, votre console Azure PowerShell est configuré et prêt toouse.</span><span class="sxs-lookup"><span data-stu-id="098b1-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="098b1-121">N’oubliez pas que vous devez toorepeate les étapes 2 à 5 chaque fois que vous démarrez la console Azure PowerShell de hello hello.</span><span class="sxs-lookup"><span data-stu-id="098b1-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="098b1-122">Afficher la liste de toutes les collections</span><span class="sxs-lookup"><span data-stu-id="098b1-122">List all collections</span></span>
- - -
     <span data-ttu-id="098b1-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="098b1-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="098b1-124">Supprimer une collection</span><span class="sxs-lookup"><span data-stu-id="098b1-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="098b1-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="098b1-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="098b1-126">Exemple : `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="098b1-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="098b1-127">Création d'une collection cloud</span><span class="sxs-lookup"><span data-stu-id="098b1-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="098b1-128">Il est simple, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="098b1-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="098b1-129">Hello au-dessus de commande publie automatiquement les applications Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio et Word).</span><span class="sxs-lookup"><span data-stu-id="098b1-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="098b1-130">Création de la collection peut prendre 30 minutes ou plu toocomplete.</span><span class="sxs-lookup"><span data-stu-id="098b1-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="098b1-131">Par conséquent, cette commande renvoie un ID de suivi que vous pouvez utiliser de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="098b1-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="098b1-132">Une fois que la collection de hello est terminée, vous pouvez ajouter toohello regroupement des utilisateurs avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="098b1-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="098b1-133">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="098b1-133">And you're done!</span></span> <span data-ttu-id="098b1-134">Cet utilisateur doit être l’application de toohello tooconnect en mesure d’à l’aide du client d’Azure RemoteApp hello trouvé [ici](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="098b1-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="098b1-135">Applets de commande disponibles</span><span class="sxs-lookup"><span data-stu-id="098b1-135">Available cmdlets</span></span>
<span data-ttu-id="098b1-136">Il existe un grand nombre d’autres commandes qui nous ont, documentation hello pour les est bientôt disponibles :</span><span class="sxs-lookup"><span data-stu-id="098b1-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="098b1-137">Applets de commande de base de la collection RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="098b1-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="098b1-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="098b1-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="098b1-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="098b1-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="098b1-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="098b1-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="098b1-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="098b1-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="098b1-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="098b1-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="098b1-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="098b1-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="098b1-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="098b1-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="098b1-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="098b1-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="098b1-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="098b1-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="098b1-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="098b1-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="098b1-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="098b1-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="098b1-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="098b1-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="098b1-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="098b1-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="098b1-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="098b1-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="098b1-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="098b1-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="098b1-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="098b1-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="098b1-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="098b1-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="098b1-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="098b1-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="098b1-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="098b1-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="098b1-157">Applets de commande du réseau virtuel RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="098b1-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="098b1-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="098b1-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="098b1-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="098b1-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="098b1-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="098b1-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="098b1-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="098b1-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="098b1-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="098b1-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="098b1-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="098b1-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="098b1-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="098b1-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="098b1-165">Applets de commande de l’image du modèle RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="098b1-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="098b1-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="098b1-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="098b1-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="098b1-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="098b1-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="098b1-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="098b1-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="098b1-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="098b1-170">Autres applets de commande RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="098b1-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="098b1-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="098b1-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="098b1-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="098b1-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="098b1-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="098b1-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="098b1-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="098b1-174">Get-AzureRemoteAppOperationResult</span></span>

