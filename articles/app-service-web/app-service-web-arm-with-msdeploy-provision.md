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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Déployer une application web avec MSDeploy, un nom d’hôte personnalisé et un certificat SSL
Ce guide décrit la création d’un déploiement de bout en bout pour une application Web Azure, en exploitant MSDeploy ainsi que l’ajout un nom d’hôte personnalisé et un modèle ARM de toohello de certificat SSL.

Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Créer un exemple d’application
Vous allez déployer une application web ASP.NET. première étape de Hello est toocreate une application web simple (ou vous pouvez choisir toouse un existant, dans ce cas, vous pouvez ignorer cette étape).

Ouvrez Visual Studio 2015 et sélectionnez Fichier > Nouveau Projet. Dans la boîte de dialogue hello choisissez Web > Application Web ASP.NET. Sous modèles choisissez Web et choisissez le modèle MVC de hello. Sélectionnez *modifier le type d’authentification* trop*aucune authentification*. Il s’agit simplement toomake hello exemple d’application aussi simple que possible.

À ce stade, vous aurez un système ASP.Net web application prêt toouse base dans le cadre de votre processus de déploiement.

### <a name="create-msdeploy-package"></a>Créer un package MSDeploy
Étape suivante consiste à toocreate hello package toodeploy hello web application tooAzure. toodo, enregistrez votre projet et puis exécutez hello qui suit à partir de la ligne de commande hello :

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Cela crée un package compressé sous le dossier de PackageLocation hello. Hello application est maintenant prête toobe déployé, ce qui vous pouvez à présent générer out une toodo de modèle Azure Resource Manager qui.

### <a name="create-arm-template"></a>Créer un modèle ARM
Nous allons commencer par un modèle ARM de base qui va créer une application web et un plan d’hébergement (Notez que les paramètres et les variables ne sont pas affichés, par souci de concision).

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

Ensuite, vous devez toomodify hello web application ressource tootake une ressource MSDeploy imbriquée. Cela vous tooreference hello package créé précédemment et de savoir Azure Resource Manager toouse MSDeploy toodeploy hello package toohello WebApp d’Azure. Hello Voici ressource Microsoft.Web/sites hello hello imbriqué MSDeploy ressource :

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

Maintenant, vous remarquez que les ressources MSDeploy hello prend un **packageUri** propriété qui est définie comme suit :

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Cela **packageUri** prend hello uri du compte de stockage pointant toohello compte de stockage dans lequel vous allez télécharger votre zip de package pour. Bonjour Azure Resource Manager reposera sur [Signatures d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md) package de hello toopull bas localement à partir de compte de stockage hello lorsque vous déployez le modèle de hello. Ce processus sera automatisé via un script PowerShell pour télécharger le package de hello et appeler les clés hello toocreate de l’API de gestion Azure de hello requises et passer en modèle de hello en tant que paramètres (*_artifactsLocation* et *_artifactsLocationSasToken*). Vous devez toodefine paramètres pour le dossier de hello et nom de fichier package hello est le conteneur de stockage hello toounder téléchargé.

Vous devez ensuite tooadd dans une autre ressource imbriquée toosetup hello hostname liaisons tooleverage un domaine personnalisé. Est de première nécessité tooensure, possède le nom d’hôte hello et de le configurer toobe vérifié par Azure qu’il vous appartient, voir [configurer un nom de domaine personnalisé dans Azure App Service](app-service-web-tutorial-custom-domain.md). Une fois que vous avez terminé, vous pouvez ajouter hello suivant le modèle tooyour sous la section de ressources Microsoft.Web/sites hello :

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

Vous devez enfin tooadd une autre ressource de niveau supérieur, Microsoft.Web/certificates. Cette ressource contient votre certificat SSL et existera à hello que votre application web et l’hébergement plan.

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

Vous devez toohave un certificat SSL valide dans tooset d’ordre haut de cette ressource. Une fois que vous avez ce certificat valid puis vous avez besoin tooextract hello pfx octets sous forme de chaîne base64. Une option tooextract il s’agit de hello toouse suivant de commande PowerShell :

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

Vous pouvez ensuite le passer comme un modèle de déploiement de paramètre tooyour ARM.

À ce stade, modèle de hello ARM est prêt.

### <a name="deploy-template"></a>Déployer un modèle
Hello dernières étapes sont toopiece cela ensemble dans un déploiement de bout en bout complète. déploiement toomake plus facile de tirer parti des hello **Deploy-azureresourcegroup.ps1** script PowerShell qui est ajouté lorsque vous créez un projet de groupe de ressources Azure dans toohelp Visual Studio avec le téléchargement de tous les artefacts requis dans modèle de Hello. Il requiert toohave créé un compte de stockage que vous souhaitez toouse avance. Pour cet exemple, j’ai créé un compte de stockage partagé pour hello package.zip toobe est téléchargé. script de Hello reposera sur compte de stockage toohello AzCopy tooupload hello package. Vous passez dans votre emplacement de dossier artefact et script de hello télécharge automatiquement tous les fichiers dans ce toohello Active un conteneur de stockage nommé. Après avoir appelé Deploy-azureresourcegroup.ps1, vous avez toothen mise à jour hello SSL liaisons toomap hello nom d’hôte personnalisé avec votre certificat SSL.

Hello ci-dessous illustre de PowerShell hello hello appelant de déploiement complet Deploy-azureresourcegroup.ps1 :

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

À ce stade votre application doit être déployée et vous devez être tooit en mesure de toobrowse via https://www.yourcustomdomain.com

