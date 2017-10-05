---
title: "Déployer une application web avec MSDeploy, un nom d’hôte et un certificat SSL"
description: "Utiliser un modèle Azure Resource Manager pour déployer une application web à l’aide de MSDeploy et configurer un nom d’hôte personnalisé et un certificat SSL"
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
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="d6b25-103">Déployer une application web avec MSDeploy, un nom d’hôte personnalisé et un certificat SSL</span><span class="sxs-lookup"><span data-stu-id="d6b25-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="d6b25-104">Ce guide explique la création d’un déploiement de bout en bout pour une Application Web Azure, exploitant MSDeploy, ainsi que l’ajout d’un nom d’hôte personnalisé et un certificat SSL au modèle ARM.</span><span class="sxs-lookup"><span data-stu-id="d6b25-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="d6b25-105">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d6b25-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="d6b25-106">Créer un exemple d’application</span><span class="sxs-lookup"><span data-stu-id="d6b25-106">Create Sample Application</span></span>
<span data-ttu-id="d6b25-107">Vous allez déployer une application web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d6b25-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="d6b25-108">La première étape consiste à créer une application web simple (vous pouvez également choisir d’utiliser une application web existante, auquel cas vous pouvez ignorer cette étape).</span><span class="sxs-lookup"><span data-stu-id="d6b25-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="d6b25-109">Ouvrez Visual Studio 2015 et sélectionnez Fichier > Nouveau Projet.</span><span class="sxs-lookup"><span data-stu-id="d6b25-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="d6b25-110">Dans la boîte de dialogue qui s’affiche, choisissez Web > Application Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d6b25-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="d6b25-111">Sous Modèles, choisissez Web et le modèle MVC.</span><span class="sxs-lookup"><span data-stu-id="d6b25-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="d6b25-112">Pour *Modifier le type d’authentification*, sélectionnez *Aucune authentification*.</span><span class="sxs-lookup"><span data-stu-id="d6b25-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="d6b25-113">uniquement pour simplifier le plus possible l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="d6b25-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="d6b25-114">À ce stade, vous obtiendrez une application web ASP.Net prête à l’emploi à utiliser dans le cadre de votre processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="d6b25-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="d6b25-115">Créer un package MSDeploy</span><span class="sxs-lookup"><span data-stu-id="d6b25-115">Create MSDeploy package</span></span>
<span data-ttu-id="d6b25-116">L’étape suivante consiste à créer le package afin de déployer l’application web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d6b25-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="d6b25-117">Pour ce faire, enregistrez votre projet, puis exécutez la commande suivante à partir de la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="d6b25-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="d6b25-118">Vous créerez ainsi un package compressé dans le dossier PackageLocation.</span><span class="sxs-lookup"><span data-stu-id="d6b25-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="d6b25-119">L’application est désormais prête à être déployée, et vous pouvez ainsi créer un modèle Azure Resource Manager pour réaliser l’opération.</span><span class="sxs-lookup"><span data-stu-id="d6b25-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="d6b25-120">Créer un modèle ARM</span><span class="sxs-lookup"><span data-stu-id="d6b25-120">Create ARM Template</span></span>
<span data-ttu-id="d6b25-121">Nous allons commencer par un modèle ARM de base qui va créer une application web et un plan d’hébergement (Notez que les paramètres et les variables ne sont pas affichés, par souci de concision).</span><span class="sxs-lookup"><span data-stu-id="d6b25-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="d6b25-122">Vous devrez ainsi modifier la ressource d’application web pour prendre une ressource MSDeploy imbriquée.</span><span class="sxs-lookup"><span data-stu-id="d6b25-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="d6b25-123">Vous pourrez ainsi référencer le package créé précédemment et donner à Azure Resource Manager comme instruction d’utiliser MSDeploy afin de déployer le package sur Azure WebApp.</span><span class="sxs-lookup"><span data-stu-id="d6b25-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="d6b25-124">Vous trouverez ci-dessous la ressource Microsoft.Web/sites avec une ressource MSDeploy imbriquée :</span><span class="sxs-lookup"><span data-stu-id="d6b25-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

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

<span data-ttu-id="d6b25-125">À présent, vous remarquerez que la ressource MSDeploy utilise une propriété **packageUri** est définie comme suit :</span><span class="sxs-lookup"><span data-stu-id="d6b25-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="d6b25-126">Ce **packageUri** accepte l’uri de compte de stockage qui pointe vers le compte de stockage dans lequel vous allez télécharger le zip de package.</span><span class="sxs-lookup"><span data-stu-id="d6b25-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="d6b25-127">Le Gestionnaire de ressources Azure s’appuie sur [Signatures d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pour balayer le package localement depuis le compte de stockage lorsque vous déployez le modèle.</span><span class="sxs-lookup"><span data-stu-id="d6b25-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="d6b25-128">Ce processus sera automatisé via un script PowerShell qui téléchargera le package et appellera l’API de gestion Azure pour créer les clés requises et transférer ces informations dans le modèle en tant que paramètres (*_artifactsLocation* et *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="d6b25-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="d6b25-129">Vous devrez définir des paramètres pour le dossier et le nom de fichier dans lequel le package téléchargé sous le conteneur de stockage.</span><span class="sxs-lookup"><span data-stu-id="d6b25-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="d6b25-130">Vous devez ensuite ajouter une autre ressource imbriquée pour configurer les liaisons du nom d’hôte et tirer parti d’un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d6b25-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="d6b25-131">Vous devez d’abord vous assurer que vous êtes propriétaire du nom d’hôte et configurer ce dernier pour qu’Azure le vérifie. Consultez [Configurer un nom de domaine personnalisé dans Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d6b25-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="d6b25-132">Une fois cette opération effectuée, vous pouvez ajouter les éléments suivants à votre modèle dans la section des ressources Microsoft.Web/sites :</span><span class="sxs-lookup"><span data-stu-id="d6b25-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="d6b25-133">Enfin, vous devez ajouter une autre ressource de niveau supérieur, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="d6b25-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="d6b25-134">Cette ressource contient votre certificat SSL et se trouve au même niveau que l’application web et le plan d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="d6b25-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="d6b25-135">Vous devez disposer d’un certificat SSL valide pour pouvoir configurer cette ressource.</span><span class="sxs-lookup"><span data-stu-id="d6b25-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="d6b25-136">Une fois que vous avez ce certificat valide, vous devez extraire les octets pfx sous forme de chaîne Base64.</span><span class="sxs-lookup"><span data-stu-id="d6b25-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="d6b25-137">Pour ce faire, vous pouvez utiliser la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="d6b25-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="d6b25-138">Vous pouvez ensuite la transférer en tant que paramètre de modèle de déploiement ARM.</span><span class="sxs-lookup"><span data-stu-id="d6b25-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="d6b25-139">À ce stade, le modèle ARM est prêt.</span><span class="sxs-lookup"><span data-stu-id="d6b25-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="d6b25-140">Déployer un modèle</span><span class="sxs-lookup"><span data-stu-id="d6b25-140">Deploy Template</span></span>
<span data-ttu-id="d6b25-141">Les étapes finales servent à rassembler les différents éléments pour obtenir un déploiement de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="d6b25-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="d6b25-142">Pour rendre le déploiement plus facile, vous pouvez utiliser le script PowerShell **Deploy-azureresourcegroup.ps1** qui est ajouté lorsque vous créez un projet de groupe de ressources Azure dans Visual Studio pour faciliter le téléchargement de tous les artefacts requis dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="d6b25-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="d6b25-143">Il vous oblige à créer un compte de stockage que vous voulez utiliser à l’avance.</span><span class="sxs-lookup"><span data-stu-id="d6b25-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="d6b25-144">Pour cet exemple, j’ai créé un compte de stockage partagé pour y télécharger le package.zip.</span><span class="sxs-lookup"><span data-stu-id="d6b25-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="d6b25-145">Le script utilisera AzCopy pour télécharger le package sur le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d6b25-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="d6b25-146">Accédez à l’emplacement du dossier de l’artefact et le script téléchargera automatiquement tous les fichiers de ce répertoire dans le conteneur de stockage nommé.</span><span class="sxs-lookup"><span data-stu-id="d6b25-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="d6b25-147">Après avoir appelé Deploy-azureresourcegroup.ps1, vous devez mettre à jour les liaisons SSL pour associer le nom d’hôte personnalisé avec votre certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="d6b25-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="d6b25-148">Le PowerShell suivant montre le déploiement complet appelant Deploy-azureresourcegroup.ps1 :</span><span class="sxs-lookup"><span data-stu-id="d6b25-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="d6b25-149">À ce stade, votre application doit être déployée, et vous devez être en mesure d’y accéder via https://www.votredomainepersonnalisé.com</span><span class="sxs-lookup"><span data-stu-id="d6b25-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

