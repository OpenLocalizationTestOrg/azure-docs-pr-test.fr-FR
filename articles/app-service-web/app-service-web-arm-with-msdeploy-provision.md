---
title: "aaaDeploy une application web à l’aide de MSDeploy avec le certificat ssl et le nom d’hôte"
description: "Utilisez un toodeploy de modèle Azure Resource Manager à une application web à l’aide de MSDeploy et la configuration de nom d’hôte personnalisé et un certificat SSL"
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="66f1a-103">Déployer une application web avec MSDeploy, un nom d’hôte personnalisé et un certificat SSL</span><span class="sxs-lookup"><span data-stu-id="66f1a-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="66f1a-104">Ce guide décrit la création d’un déploiement de bout en bout pour une application Web Azure, en exploitant MSDeploy ainsi que l’ajout un nom d’hôte personnalisé et un modèle ARM de toohello de certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="66f1a-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="66f1a-105">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="66f1a-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="66f1a-106">Créer un exemple d’application</span><span class="sxs-lookup"><span data-stu-id="66f1a-106">Create Sample Application</span></span>
<span data-ttu-id="66f1a-107">Vous allez déployer une application web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="66f1a-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="66f1a-108">première étape de Hello est toocreate une application web simple (ou vous pouvez choisir toouse un existant, dans ce cas, vous pouvez ignorer cette étape).</span><span class="sxs-lookup"><span data-stu-id="66f1a-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="66f1a-109">Ouvrez Visual Studio 2015 et sélectionnez Fichier > Nouveau Projet.</span><span class="sxs-lookup"><span data-stu-id="66f1a-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="66f1a-110">Dans la boîte de dialogue hello choisissez Web > Application Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="66f1a-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="66f1a-111">Sous modèles choisissez Web et choisissez le modèle MVC de hello.</span><span class="sxs-lookup"><span data-stu-id="66f1a-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="66f1a-112">Sélectionnez *modifier le type d’authentification* trop*aucune authentification*.</span><span class="sxs-lookup"><span data-stu-id="66f1a-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="66f1a-113">Il s’agit simplement toomake hello exemple d’application aussi simple que possible.</span><span class="sxs-lookup"><span data-stu-id="66f1a-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="66f1a-114">À ce stade, vous aurez un système ASP.Net web application prêt toouse base dans le cadre de votre processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="66f1a-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="66f1a-115">Créer un package MSDeploy</span><span class="sxs-lookup"><span data-stu-id="66f1a-115">Create MSDeploy package</span></span>
<span data-ttu-id="66f1a-116">Étape suivante consiste à toocreate hello package toodeploy hello web application tooAzure.</span><span class="sxs-lookup"><span data-stu-id="66f1a-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="66f1a-117">toodo, enregistrez votre projet et puis exécutez hello qui suit à partir de la ligne de commande hello :</span><span class="sxs-lookup"><span data-stu-id="66f1a-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="66f1a-118">Cela crée un package compressé sous le dossier de PackageLocation hello.</span><span class="sxs-lookup"><span data-stu-id="66f1a-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="66f1a-119">Hello application est maintenant prête toobe déployé, ce qui vous pouvez à présent générer out une toodo de modèle Azure Resource Manager qui.</span><span class="sxs-lookup"><span data-stu-id="66f1a-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="66f1a-120">Créer un modèle ARM</span><span class="sxs-lookup"><span data-stu-id="66f1a-120">Create ARM Template</span></span>
<span data-ttu-id="66f1a-121">Nous allons commencer par un modèle ARM de base qui va créer une application web et un plan d’hébergement (Notez que les paramètres et les variables ne sont pas affichés, par souci de concision).</span><span class="sxs-lookup"><span data-stu-id="66f1a-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

<span data-ttu-id="66f1a-122">Ensuite, vous devez toomodify hello web application ressource tootake une ressource MSDeploy imbriquée.</span><span class="sxs-lookup"><span data-stu-id="66f1a-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="66f1a-123">Cela vous tooreference hello package créé précédemment et de savoir Azure Resource Manager toouse MSDeploy toodeploy hello package toohello WebApp d’Azure.</span><span class="sxs-lookup"><span data-stu-id="66f1a-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="66f1a-124">Hello Voici ressource Microsoft.Web/sites hello hello imbriqué MSDeploy ressource :</span><span class="sxs-lookup"><span data-stu-id="66f1a-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

<span data-ttu-id="66f1a-125">Maintenant, vous remarquez que les ressources MSDeploy hello prend un **packageUri** propriété qui est définie comme suit :</span><span class="sxs-lookup"><span data-stu-id="66f1a-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="66f1a-126">Cela **packageUri** prend hello uri du compte de stockage pointant toohello compte de stockage dans lequel vous allez télécharger votre zip de package pour.</span><span class="sxs-lookup"><span data-stu-id="66f1a-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="66f1a-127">Bonjour Azure Resource Manager reposera sur [Signatures d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md) package de hello toopull bas localement à partir de compte de stockage hello lorsque vous déployez le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="66f1a-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="66f1a-128">Ce processus sera automatisé via un script PowerShell pour télécharger le package de hello et appeler les clés hello toocreate de l’API de gestion Azure de hello requises et passer en modèle de hello en tant que paramètres (*_artifactsLocation* et *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="66f1a-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="66f1a-129">Vous devez toodefine paramètres pour le dossier de hello et nom de fichier package hello est le conteneur de stockage hello toounder téléchargé.</span><span class="sxs-lookup"><span data-stu-id="66f1a-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="66f1a-130">Vous devez ensuite tooadd dans une autre ressource imbriquée toosetup hello hostname liaisons tooleverage un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="66f1a-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="66f1a-131">Est de première nécessité tooensure, possède le nom d’hôte hello et de le configurer toobe vérifié par Azure qu’il vous appartient, voir [configurer un nom de domaine personnalisé dans Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="66f1a-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="66f1a-132">Une fois que vous avez terminé, vous pouvez ajouter hello suivant le modèle tooyour sous la section de ressources Microsoft.Web/sites hello :</span><span class="sxs-lookup"><span data-stu-id="66f1a-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

<span data-ttu-id="66f1a-133">Vous devez enfin tooadd une autre ressource de niveau supérieur, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="66f1a-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="66f1a-134">Cette ressource contient votre certificat SSL et existera à hello que votre application web et l’hébergement plan.</span><span class="sxs-lookup"><span data-stu-id="66f1a-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

<span data-ttu-id="66f1a-135">Vous devez toohave un certificat SSL valide dans tooset d’ordre haut de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="66f1a-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="66f1a-136">Une fois que vous avez ce certificat valid puis vous avez besoin tooextract hello pfx octets sous forme de chaîne base64.</span><span class="sxs-lookup"><span data-stu-id="66f1a-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="66f1a-137">Une option tooextract il s’agit de hello toouse suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="66f1a-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="66f1a-138">Vous pouvez ensuite le passer comme un modèle de déploiement de paramètre tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="66f1a-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="66f1a-139">À ce stade, modèle de hello ARM est prêt.</span><span class="sxs-lookup"><span data-stu-id="66f1a-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="66f1a-140">Déployer un modèle</span><span class="sxs-lookup"><span data-stu-id="66f1a-140">Deploy Template</span></span>
<span data-ttu-id="66f1a-141">Hello dernières étapes sont toopiece cela ensemble dans un déploiement de bout en bout complète.</span><span class="sxs-lookup"><span data-stu-id="66f1a-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="66f1a-142">déploiement toomake plus facile de tirer parti des hello **Deploy-azureresourcegroup.ps1** script PowerShell qui est ajouté lorsque vous créez un projet de groupe de ressources Azure dans toohelp Visual Studio avec le téléchargement de tous les artefacts requis dans modèle de Hello.</span><span class="sxs-lookup"><span data-stu-id="66f1a-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="66f1a-143">Il requiert toohave créé un compte de stockage que vous souhaitez toouse avance.</span><span class="sxs-lookup"><span data-stu-id="66f1a-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="66f1a-144">Pour cet exemple, j’ai créé un compte de stockage partagé pour hello package.zip toobe est téléchargé.</span><span class="sxs-lookup"><span data-stu-id="66f1a-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="66f1a-145">script de Hello reposera sur compte de stockage toohello AzCopy tooupload hello package.</span><span class="sxs-lookup"><span data-stu-id="66f1a-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="66f1a-146">Vous passez dans votre emplacement de dossier artefact et script de hello télécharge automatiquement tous les fichiers dans ce toohello Active un conteneur de stockage nommé.</span><span class="sxs-lookup"><span data-stu-id="66f1a-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="66f1a-147">Après avoir appelé Deploy-azureresourcegroup.ps1, vous avez toothen mise à jour hello SSL liaisons toomap hello nom d’hôte personnalisé avec votre certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="66f1a-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="66f1a-148">Hello ci-dessous illustre de PowerShell hello hello appelant de déploiement complet Deploy-azureresourcegroup.ps1 :</span><span class="sxs-lookup"><span data-stu-id="66f1a-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="66f1a-149">À ce stade votre application doit être déployée et vous devez être tooit en mesure de toobrowse via https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="66f1a-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

