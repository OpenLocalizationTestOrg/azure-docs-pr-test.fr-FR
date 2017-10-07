---
title: "aaaDeploy une application web qui est lié le référentiel GitHub de tooa | Documents Microsoft"
description: "Utilisez un toodeploy de modèle Azure Resource Manager une application web qui contient un projet à partir d’un référentiel GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>Déployer un référentiel GitHub de web application lié tooa
Dans cette rubrique, vous allez apprendre comment toocreate un modèle Azure Resource Manager qui déploie une application web qui est lié à project tooa dans un référentiel GitHub. Vous allez apprendre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée. Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.

Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Pour le modèle complète de hello, consultez [Web application lié tooGitHub modèle](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Ce que vous allez déployer
Avec ce modèle, vous allez déployer une application web qui contient le code hello à partir d’un projet dans GitHub.

toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :

[![Déployer tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>Paramètres
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
URL de Hello pour le référentiel GitHub qui contient les hello projet toodeploy. Ce paramètre contient une valeur par défaut, mais cette valeur est uniquement prévue tooshow vous comment tooprovide hello URL du référentiel. Vous pouvez utiliser cette valeur lorsque le test de modèle de hello, mais vous pouvez tooprovide hello URL votre propre référentiel lorsque vous travaillez avec un modèle de hello.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>branche
branche Hello de hello référentiel toouse lors du déploiement d’application hello. la valeur par défaut Hello est master, mais vous pouvez fournir nom hello de n’importe quelle branche dans le référentiel de hello que vous souhaitez toodeploy.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>Ressources toodeploy
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Application web
Crée l’application hello web qui est le projet toohello lié dans GitHub. 

Vous spécifiez le nom hello de l’application web via hello hello **siteName** paramètre et l’emplacement de hello de l’application web via hello hello **sitelocation correspond** paramètre. Bonjour **dependsOn** élément, modèle de hello définit hello web application en tant que dépendant du service hello plan d’hébergement. Comme il est dépendant de hello plan d’hébergement, hello web app n’est pas créé tant que plan d’hébergement de hello est en cours de création. Hello **dependsOn** élément est uniquement un ordre de déploiement toospecify utilisé. Si vous ne marquez pas une application web hello comme dépendant de plan d’hébergement hello, Azure Resource Manager va tenter de toocreate les ressources à hello même temps et que vous receviez une erreur si l’application web hello est créée avant hello plan d’hébergement.

l’application Hello web a également une ressource enfant qui est définie dans **ressources** section ci-dessous. Cette ressource enfant définit le contrôle de code source pour le projet hello déployé avec l’application web hello. Dans ce modèle, contrôle de code source hello est le référentiel GitHub particulier de tooa lié. référentiel GitHub de Hello est défini avec le code de hello **« RepoUrl » : « https://github.com/davidebbo-test/Mvc52Application.git »** vous pouvez coder en dur hello URL du référentiel lorsque vous souhaitez toocreate un modèle à plusieurs reprises déploie un projet unique tout en exigeant le nombre minimal de hello de paramètres.
Au lieu de coder en dur hello URL du référentiel, vous pouvez ajouter un paramètre d’URL du référentiel hello et utilisez cette valeur pour hello **RepoUrl** propriété.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>Déploiement de toorun de commandes
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Interface de ligne de commande Azure

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Azure CLI 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Pour le contenu du fichier JSON de paramètres hello, consultez [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

