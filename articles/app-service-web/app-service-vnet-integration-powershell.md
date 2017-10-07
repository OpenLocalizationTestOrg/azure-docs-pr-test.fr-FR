---
title: "aaaConnect votre réseau virtuel de tooyour application à l’aide de PowerShell"
description: "Obtenir des instructions sur le fonctionnement de tooconnect tooand avec des réseaux virtuels à l’aide de PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="75c05-103">Connecter votre réseau virtuel de tooyour application à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="75c05-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="75c05-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="75c05-104">Overview</span></span>
<span data-ttu-id="75c05-105">Dans Azure App Service, vous pouvez connecter votre application (API, mobile ou web) tooan réseau virtuel Azure (VNet) dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="75c05-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="75c05-106">Cette fonctionnalité est appelée « intégration au réseau virtuel ».</span><span class="sxs-lookup"><span data-stu-id="75c05-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="75c05-107">fonctionnalité d’intégration de réseau virtuel Hello ne doit pas être confondue avec fonctionnalité d’environnement App Service hello, qui vous permet de toorun une instance de Service d’applications Azure dans votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="75c05-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="75c05-108">fonctionnalité d’intégration de réseau virtuel Hello possède une interface utilisateur (IU) dans le nouveau portail de hello que vous pouvez utiliser toointegrate avec des réseaux virtuels sont déployés à l’aide du modèle de déploiement classique hello ou de modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="75c05-109">Si vous souhaitez toolearn plus d’informations sur la fonctionnalité de hello, consultez [intégrer votre application à un réseau virtuel Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="75c05-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="75c05-110">Cet article n’est pas sur comment toouse hello UI mais plutôt sur l’intégration de tooenable à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="75c05-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="75c05-111">Étant donné que les commandes hello pour chaque modèle de déploiement sont différents, cet article comporte une section pour chaque modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="75c05-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="75c05-112">Avant de poursuivre la lecture de cet article, vérifiez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="75c05-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="75c05-113">Hello que dernière Azure PowerShell SDK installé.</span><span class="sxs-lookup"><span data-stu-id="75c05-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="75c05-114">Vous pouvez installer cette avec hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="75c05-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="75c05-115">Une application dans Azure App Service est en cours d’exécution dans le niveau Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="75c05-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="75c05-116">Réseaux virtuels classiques</span><span class="sxs-lookup"><span data-stu-id="75c05-116">Classic virtual networks</span></span>
<span data-ttu-id="75c05-117">Cette section décrit les trois tâches pour les réseaux virtuels qui utilisent le modèle de déploiement classique hello :</span><span class="sxs-lookup"><span data-stu-id="75c05-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="75c05-118">Connecter votre application tooa préexistants réseau virtuel qui a une passerelle et est configuré pour la connectivité de point-to-site.</span><span class="sxs-lookup"><span data-stu-id="75c05-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="75c05-119">Mettre à jour des informations relatives à l’intégration au réseau virtuel pour votre application.</span><span class="sxs-lookup"><span data-stu-id="75c05-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="75c05-120">Déconnecter votre application du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="75c05-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="75c05-121">Se connecter à une application tooa réseau virtuel classique</span><span class="sxs-lookup"><span data-stu-id="75c05-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="75c05-122">tooconnect un réseau virtuel tooa d’application, suivez ces trois étapes :</span><span class="sxs-lookup"><span data-stu-id="75c05-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="75c05-123">Déclarez l’application web toohello qu’il devra joindre à un réseau virtuel particulier.</span><span class="sxs-lookup"><span data-stu-id="75c05-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="75c05-124">application Hello génère un certificat qui sera allouée toohello des réseaux virtuels pour la connectivité de point-to-site.</span><span class="sxs-lookup"><span data-stu-id="75c05-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="75c05-125">Réseau virtuel toohello du certificat application hello web de télécharger et extraire les URI du package hello point-to-site VPN.</span><span class="sxs-lookup"><span data-stu-id="75c05-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="75c05-126">Mettre à jour la connexion de réseau virtuel de l’application hello web avec l’URI du package de point-to-site hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="75c05-127">Hello premier et troisième étapes sont entièrement scriptable, mais la deuxième étape de hello nécessite une action manuelle à usage unique via le portail de hello ou accès tooperform **PUT** ou **correctif** actions sur le réseau virtuel de hello Point de terminaison du Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="75c05-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="75c05-128">Contactez le Support Azure toohave cette option est activée.</span><span class="sxs-lookup"><span data-stu-id="75c05-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="75c05-129">Avant de commencer, vérifiez que vous disposez d’un réseau virtuel classique avec une connectivité de point à site activée et une passerelle déployée.</span><span class="sxs-lookup"><span data-stu-id="75c05-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="75c05-130">toocreate hello passerelle et activer point-to-site connectivité, vous devez portal de hello toouse comme décrit dans [création d’une passerelle VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="75c05-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="75c05-131">réseau virtuel classique Hello doit toobe Bonjour même abonnement que votre Service d’applications de planifier cette application hello blocages que vous intégrez avec.</span><span class="sxs-lookup"><span data-stu-id="75c05-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="75c05-132">Configurer le Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="75c05-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="75c05-133">Ouvrez une fenêtre PowerShell et configurez votre abonnement et votre compte Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="75c05-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="75c05-134">Cette commande ouvre une invite de commandes tooget vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="75c05-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="75c05-135">Après que vous être connecté, utilisez une de hello suivant l’abonnement de hello tooselect de commandes que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="75c05-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="75c05-136">Assurez-vous que vous utilisez abonnement hello qui se trouvent dans votre réseau virtuel et un plan de Service d’application.</span><span class="sxs-lookup"><span data-stu-id="75c05-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="75c05-137">ou</span><span class="sxs-lookup"><span data-stu-id="75c05-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="75c05-138">Variables utilisées dans cet article</span><span class="sxs-lookup"><span data-stu-id="75c05-138">Variables used in this article</span></span>
<span data-ttu-id="75c05-139">les commandes toosimplify, nous allons définir un **$Configuration** variable PowerShell avec une configuration spécifique hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="75c05-140">Définissez une variable comme suit dans PowerShell avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="75c05-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="75c05-141">emplacement de l’application Hello doit être emplacement hello sans espaces.</span><span class="sxs-lookup"><span data-stu-id="75c05-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="75c05-142">Par exemple, « West US » devient westus.</span><span class="sxs-lookup"><span data-stu-id="75c05-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="75c05-143">élément suivant de Hello est où le certificat de hello doit être écrits.</span><span class="sxs-lookup"><span data-stu-id="75c05-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="75c05-144">Il doit s’agir d’un chemin d’accès en écriture sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="75c05-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="75c05-145">Assurez-vous que tooinclude .cer à fin de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="75c05-146">toosee vous définissez, type **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="75c05-146">toosee what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="75c05-147">reste Hello de cette section part du principe que vous disposez d’une variable créée comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="75c05-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="75c05-148">Déclarer des application toohello de réseau virtuel hello</span><span class="sxs-lookup"><span data-stu-id="75c05-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="75c05-149">Utilisez hello suivant commande tootell hello application qu’il doit utiliser ce réseau virtuel spécifique.</span><span class="sxs-lookup"><span data-stu-id="75c05-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="75c05-150">Cela entraîne hello application toogenerate certificats nécessaires :</span><span class="sxs-lookup"><span data-stu-id="75c05-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="75c05-151">Si cette commande réussit, **$vnet** doit inclure une variable **Properties**.</span><span class="sxs-lookup"><span data-stu-id="75c05-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="75c05-152">Hello **propriétés** variable doit contenir à la fois une empreinte numérique et hello certificat données de certificat.</span><span class="sxs-lookup"><span data-stu-id="75c05-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="75c05-153">Télécharger le réseau virtuel toohello du certificat application hello web</span><span class="sxs-lookup"><span data-stu-id="75c05-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="75c05-154">Une étape unique manuelle est requise pour chaque combinaison réseau virtuel/abonnement.</span><span class="sxs-lookup"><span data-stu-id="75c05-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="75c05-155">Autrement dit, si vous vous connectez des applications dans l’abonnement A tooVirtual réseau A, vous devez toodo cette étape qu’une seule fois, quelle que soit le nombre d’applications que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="75c05-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="75c05-156">Si vous ajoutez un nouveau réseau virtuel de tooanother d’application, vous devez toodo ce message.</span><span class="sxs-lookup"><span data-stu-id="75c05-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="75c05-157">Hello en fait un jeu de certificats est généré au niveau de l’abonnement dans Azure App Service que hello jeu est générée une fois pour chaque réseau virtuel auquel hello applications seront connectent.</span><span class="sxs-lookup"><span data-stu-id="75c05-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="75c05-158">Hello certificats seront ont déjà été définies si vous avez suivi ces étapes, ou si vous avez intégré hello même réseau virtuel à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="75c05-159">première étape de Hello est un fichier .cer de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="75c05-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="75c05-160">deuxième étape de Hello est un réseau virtuel tooyour du fichier .cer tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="75c05-161">toogenerate de fichier .cer hello à partir de l’appel d’API de hello Bonjour étape antérieure, exécutez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="75c05-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="75c05-162">certificat de Hello se trouve dans un emplacement de hello qui **$Configuration.GeneratedCertificatePath** spécifie.</span><span class="sxs-lookup"><span data-stu-id="75c05-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="75c05-163">certificat de hello tooupload utiliser manuellement, hello [portail Azure] [ azureportal] et **parcourir le réseau virtuel (classiques)** > **lesconnexionsVPN**  >  **Point-to-site** > **gérer les certificats**.</span><span class="sxs-lookup"><span data-stu-id="75c05-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="75c05-164">À partir de là, téléchargez votre certificat.</span><span class="sxs-lookup"><span data-stu-id="75c05-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="75c05-165">Obtenir le package de point-to-site hello</span><span class="sxs-lookup"><span data-stu-id="75c05-165">Get hello point-to-site package</span></span>
<span data-ttu-id="75c05-166">étape suivante de Hello dans la configuration d’une connexion de réseau virtuel sur une application web est le package de point-to-site tooget hello et fournit l’application web tooyour.</span><span class="sxs-lookup"><span data-stu-id="75c05-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="75c05-167">Enregistrez hello appelé GetNetworkPackageUri.json quelque part sur votre ordinateur, par exemple, C:\Azure\Templates\GetNetworkPackageUri.json par le fichier modèle tooa suivant.</span><span class="sxs-lookup"><span data-stu-id="75c05-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="75c05-168">Définissez les paramètres d’entrée :</span><span class="sxs-lookup"><span data-stu-id="75c05-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="75c05-169">Script hello d’appel :</span><span class="sxs-lookup"><span data-stu-id="75c05-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="75c05-170">variable de Hello **$output. Outputs.packageUri** contient désormais hello package URI toobe donné tooyour l’application web.</span><span class="sxs-lookup"><span data-stu-id="75c05-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="75c05-171">Télécharger l’application tooyour de package de point-to-site hello</span><span class="sxs-lookup"><span data-stu-id="75c05-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="75c05-172">étape finale de Hello est application hello de tooprovide avec ce package.</span><span class="sxs-lookup"><span data-stu-id="75c05-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="75c05-173">Exécutez simplement la commande suivante hello :</span><span class="sxs-lookup"><span data-stu-id="75c05-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="75c05-174">Si un message vous demande tooconfirm que vous remplacez une ressource existante, assurez-vous que tooallow il.</span><span class="sxs-lookup"><span data-stu-id="75c05-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="75c05-175">Une fois cette commande réussit, votre application doit maintenant être connecté toohello des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="75c05-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="75c05-176">tooconfirm cas de réussite, accédez tooyour console d’application et tapez Bonjour qui suit :</span><span class="sxs-lookup"><span data-stu-id="75c05-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="75c05-177">S’il existe une variable d’environnement appelée WEBSITE_VNETNAME qui a une valeur qui correspond au nom hello du réseau virtuel de hello cible, toutes les configurations ont réussi.</span><span class="sxs-lookup"><span data-stu-id="75c05-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="75c05-178">Mettre à jour des informations relatives à l’intégration au réseau virtuel classique</span><span class="sxs-lookup"><span data-stu-id="75c05-178">Update classic VNet integration information</span></span>
<span data-ttu-id="75c05-179">tooupdate ou resynchronisation de vos informations, répétez simplement les étapes hello que vous avez suivi lors de la création de l’intégration hello en premier lieu de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="75c05-180">à savoir :</span><span class="sxs-lookup"><span data-stu-id="75c05-180">Those steps are:</span></span>

1. <span data-ttu-id="75c05-181">Définir vos informations de configuration.</span><span class="sxs-lookup"><span data-stu-id="75c05-181">Define your configuration information.</span></span>
2. <span data-ttu-id="75c05-182">Déclarer des application toohello de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="75c05-183">Obtenir le package de point-to-site hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="75c05-184">Télécharger l’application tooyour de package de point-to-site hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="75c05-185">Déconnecter votre application d’un réseau virtuel classique</span><span class="sxs-lookup"><span data-stu-id="75c05-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="75c05-186">toodisconnect hello application, vous avez besoin des informations de configuration hello qui a été définies lors de l’intégration de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="75c05-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="75c05-187">À l’aide de ces informations, il est ensuite un toodisconnect de commande votre application à partir de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="75c05-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="75c05-188">Réseaux virtuels Resource Manager</span><span class="sxs-lookup"><span data-stu-id="75c05-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="75c05-189">Les réseaux virtuels Resource Manager disposent d’API Azure Resource Manager, qui simplifient certains processus si on les compare aux réseaux virtuels classiques.</span><span class="sxs-lookup"><span data-stu-id="75c05-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="75c05-190">Nous avons un script qui vous aideront à exécuter hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="75c05-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="75c05-191">Créer un réseau virtuel Resource Manager et y intégrer votre application</span><span class="sxs-lookup"><span data-stu-id="75c05-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="75c05-192">Créer une passerelle, configurer la connectivité de point à site dans un réseau virtuel Resource Manager préexistant, puis y intégrer votre application.</span><span class="sxs-lookup"><span data-stu-id="75c05-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="75c05-193">Intégrer votre application à un réseau virtuel Resource Manager préexistant disposant d’une passerelle et sur lequel la connectivité de point à site est activée.</span><span class="sxs-lookup"><span data-stu-id="75c05-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="75c05-194">Déconnecter votre application du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="75c05-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="75c05-195">Script d’intégration App Service pour les réseaux virtuels Resource Manager</span><span class="sxs-lookup"><span data-stu-id="75c05-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="75c05-196">Copiez hello suivants de script et enregistrement les fichiers tooa.</span><span class="sxs-lookup"><span data-stu-id="75c05-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="75c05-197">Si vous ne souhaitez pas script de hello toouse, vous pouvez toolearn libre à partir de celui-ci toosee comment tooset les choses avec un réseau virtuel du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="75c05-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="75c05-198">Enregistrer une copie du script de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-198">Save a copy of hello script.</span></span> <span data-ttu-id="75c05-199">Dans cet article, il est appelé V2VnetAllinOne.ps1, mais vous pouvez utiliser un autre nom.</span><span class="sxs-lookup"><span data-stu-id="75c05-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="75c05-200">Ce script n’inclut aucun argument.</span><span class="sxs-lookup"><span data-stu-id="75c05-200">There are no arguments for this script.</span></span> <span data-ttu-id="75c05-201">Vous devez simplement l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="75c05-201">You simply run it.</span></span> <span data-ttu-id="75c05-202">Hello première script de hello effectuera est invite toosign dans.</span><span class="sxs-lookup"><span data-stu-id="75c05-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="75c05-203">Après que vous être connecté, script de hello Obtient des informations relatives à votre compte et retourne une liste des abonnements.</span><span class="sxs-lookup"><span data-stu-id="75c05-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="75c05-204">Sans compter demande hello vos informations d’identification, l’exécution du script initiale hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="75c05-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="75c05-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="75c05-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="75c05-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="75c05-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="75c05-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="75c05-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="75c05-208">Choose an option: 3</span><span class="sxs-lookup"><span data-stu-id="75c05-208">Choose an option: 3</span></span>

    <span data-ttu-id="75c05-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="75c05-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="75c05-210">Veuillez entrer hello groupe de ressources de votre application : hcdemo-rg entrez hello nom de votre application : v2vnetpowershell comment vous souhaitez toodo ?</span><span class="sxs-lookup"><span data-stu-id="75c05-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="75c05-211">Ajouter une application de tooan nouveau réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="75c05-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="75c05-212">Ajouter une application de tooan réseau virtuel existant</span><span class="sxs-lookup"><span data-stu-id="75c05-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="75c05-213">Remove a Virtual Network from an App</span><span class="sxs-lookup"><span data-stu-id="75c05-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="75c05-214">reste Hello de cette section décrit chacune de ces trois options.</span><span class="sxs-lookup"><span data-stu-id="75c05-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="75c05-215">Créer et intégrer un réseau virtuel Resource Manager</span><span class="sxs-lookup"><span data-stu-id="75c05-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="75c05-216">Sélectionnez d’un réseau virtuel qu’utilise hello du modèle de déploiement de gestionnaire de ressources et l’intégrer à votre application, toocreate **1) ajouter un nouveau réseau virtuel de tooan application**.</span><span class="sxs-lookup"><span data-stu-id="75c05-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="75c05-217">Vous serez invité pour nom hello du réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="75c05-218">Dans mon cas, comme vous pouvez le voir Bonjour suivant les paramètres, j’ai utilisé le nom hello, v2pshell.</span><span class="sxs-lookup"><span data-stu-id="75c05-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="75c05-219">script de Hello donne des détails de hello sur le réseau virtuel hello en cours de création.</span><span class="sxs-lookup"><span data-stu-id="75c05-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="75c05-220">Si vous le souhaitez, je peux modifier une des valeurs de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="75c05-221">Dans l’exécution de cet exemple, j’ai créé un réseau virtuel qui a hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="75c05-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="75c05-222">Si vous souhaitez une des valeurs de hello toochange, tapez **Y** et apporter des modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="75c05-223">Lorsque vous êtes satisfait des paramètres de réseau virtuel hello, tapez **N** ou appuyez simplement sur ENTRÉE lorsque vous êtes invité à modifier les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="75c05-224">À partir de là sur jusqu'à la fin, le script de hello vous indiquera parmi ce qu’il « i effectuant jusqu'à ce qu’il démarre la passerelle de réseau virtuel toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="75c05-225">Cette étape peut prendre jusqu'à tooan heure.</span><span class="sxs-lookup"><span data-stu-id="75c05-225">That step can take up tooan hour.</span></span> <span data-ttu-id="75c05-226">Il n’existe aucun indicateur de progression durant cette phase, mais le script de hello vous avertit quand une passerelle de hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="75c05-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="75c05-227">Une fois le script de hello, il indiquera **terminé**.</span><span class="sxs-lookup"><span data-stu-id="75c05-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="75c05-228">À ce stade, vous aurez un réseau virtuel du Gestionnaire de ressources qui a le nom de hello et les paramètres que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="75c05-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="75c05-229">Ce nouveau réseau virtuel sera également intégré à votre application.</span><span class="sxs-lookup"><span data-stu-id="75c05-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="75c05-230">Intégrer votre application à un réseau virtuel Resource Manager préexistant</span><span class="sxs-lookup"><span data-stu-id="75c05-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="75c05-231">Lorsque vous intégrez avec un réseau virtuel préexistant, si vous fournissez un réseau virtuel du Gestionnaire de ressources qui n’a pas de passerelle ou de connectivité de point à site, hello script qui définit.</span><span class="sxs-lookup"><span data-stu-id="75c05-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="75c05-232">Si hello réseau virtuel possède déjà les éléments de configuration, le script de hello va intégration toohello droite de l’application.</span><span class="sxs-lookup"><span data-stu-id="75c05-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="75c05-233">toostart ce processus, sélectionnez simplement **2) ajouter un réseau virtuel existant de tooan application**.</span><span class="sxs-lookup"><span data-stu-id="75c05-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="75c05-234">Cette option fonctionne uniquement si vous avez un réseau virtuel Gestionnaire de ressources préexistantes qui se trouve dans hello même abonnement que votre application.</span><span class="sxs-lookup"><span data-stu-id="75c05-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="75c05-235">Une fois que vous sélectionnez hello option, une liste de vos réseaux virtuels du Gestionnaire de ressources s’affiche.</span><span class="sxs-lookup"><span data-stu-id="75c05-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="75c05-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="75c05-236">v2demonetwork</span></span>
    2) <span data-ttu-id="75c05-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="75c05-237">v2pshell</span></span>
    3) <span data-ttu-id="75c05-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="75c05-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="75c05-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="75c05-239">v2asenetwork</span></span>
    5) <span data-ttu-id="75c05-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="75c05-240">v2pshell2</span></span>

    <span data-ttu-id="75c05-241">Choose an option: 5</span><span class="sxs-lookup"><span data-stu-id="75c05-241">Choose an option: 5</span></span>

<span data-ttu-id="75c05-242">Il suffit de sélectionner réseau virtuel hello toointegrate avec souhaitées.</span><span class="sxs-lookup"><span data-stu-id="75c05-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="75c05-243">Si vous disposez déjà d’une passerelle qui dispose d’une connectivité de point-to-site activée, le script de hello s’intègre simplement votre application avec votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="75c05-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="75c05-244">Si vous ne disposez pas d’une passerelle, vous devez le sous-réseau de passerelle toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="75c05-245">Votre sous-réseau de passerelle doit être situé dans votre espace d’adressage de réseau virtuel. Il ne peut pas être situé dans un autre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="75c05-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="75c05-246">Si vous avez un réseau virtuel sans passerelle et que vous exécutez cette étape, voici ce que vous obtenez :</span><span class="sxs-lookup"><span data-stu-id="75c05-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="75c05-247">Dans cet exemple, j’ai créé une passerelle de réseau virtuel qui a hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="75c05-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="75c05-248">Si vous souhaitez toochange un de ces paramètres, vous pouvez le faire.</span><span class="sxs-lookup"><span data-stu-id="75c05-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="75c05-249">Dans le cas contraire, appuyez sur entrée et hello script créer votre passerelle et attacher votre réseau virtuel de tooyour application.</span><span class="sxs-lookup"><span data-stu-id="75c05-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="75c05-250">heure de création de passerelle Hello est toujours une heure, bien que, par conséquent, assurez-vous que vous esprit qui.</span><span class="sxs-lookup"><span data-stu-id="75c05-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="75c05-251">Lorsque tout est terminé, le script de hello indiquera **terminé**.</span><span class="sxs-lookup"><span data-stu-id="75c05-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="75c05-252">Se déconnecter de votre application à partir d’un réseau virtuel Resource Manager</span><span class="sxs-lookup"><span data-stu-id="75c05-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="75c05-253">Déconnexion de votre application à partir de votre réseau virtuel ne pas arrêter la passerelle de hello ou désactiver la connectivité de point-to-site.</span><span class="sxs-lookup"><span data-stu-id="75c05-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="75c05-254">Vous pouvez donc utiliser ces dernières à d’autres fins.</span><span class="sxs-lookup"><span data-stu-id="75c05-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="75c05-255">Il également ne pas déconnecte toutes les autres applications autres que hello vous fourni.</span><span class="sxs-lookup"><span data-stu-id="75c05-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="75c05-256">tooperform cette action, sélectionnez **3) supprimer un réseau virtuel à partir d’une application**.</span><span class="sxs-lookup"><span data-stu-id="75c05-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="75c05-257">Vous obtenez ceci :</span><span class="sxs-lookup"><span data-stu-id="75c05-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="75c05-258">Bien que le script de hello indique que la suppression, il ne supprime pas de réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="75c05-259">Il supprime simplement l’intégration hello.</span><span class="sxs-lookup"><span data-stu-id="75c05-259">It’s just removing hello integration.</span></span> <span data-ttu-id="75c05-260">Après avoir confirmé que c’est ce que vous voulez toodo, commande hello est traitée très rapidement et vous indique **True** quand il est terminé.</span><span class="sxs-lookup"><span data-stu-id="75c05-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
