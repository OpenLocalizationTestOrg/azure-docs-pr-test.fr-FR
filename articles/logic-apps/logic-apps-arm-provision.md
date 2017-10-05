---
title: "Créer une application logique à l’aide d’un modèle dans Azure | Microsoft Docs"
description: "Utiliser un modèle Azure Resource Manager pour déployer une application logique pour la définition de workflows."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="62c13-103">Créer une application logique à l'aide d'un modèle</span><span class="sxs-lookup"><span data-stu-id="62c13-103">Create a Logic App using a template</span></span>
<span data-ttu-id="62c13-104">Les modèles constituent un moyen rapide d’utiliser des connecteurs différents au sein d’une application logique.</span><span class="sxs-lookup"><span data-stu-id="62c13-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="62c13-105">Les applications logiques comportent des modèles Azure Resource Manager qui vous permettent de créer une application logique à mettre à profit pour la définition de workflows professionnels.</span><span class="sxs-lookup"><span data-stu-id="62c13-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="62c13-106">Vous pouvez définir les ressources à déployer et la méthode de définition des paramètres lors du déploiement de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="62c13-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="62c13-107">Vous pouvez utiliser ce modèle pour vos propres scénarios professionnels, ou le personnaliser selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="62c13-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="62c13-108">Pour plus d'informations sur les propriétés de l'application logique, consultez l' [API de gestion du flux de travail d'application logique](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="62c13-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="62c13-109">Pour obtenir des exemples sur la définition proprement dite, consultez [Créer des définitions d'application logique](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="62c13-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="62c13-110">Pour plus d'informations sur la création de modèles, consultez la rubrique [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="62c13-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="62c13-111">Pour le modèle complet, consultez le [modèle d'application logique](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="62c13-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="62c13-112">Que déployer ?</span><span class="sxs-lookup"><span data-stu-id="62c13-112">What you deploy</span></span>
<span data-ttu-id="62c13-113">Avec ce modèle, vous déployez une application logique.</span><span class="sxs-lookup"><span data-stu-id="62c13-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="62c13-114">Pour exécuter automatiquement le déploiement, sélectionnez le bouton ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="62c13-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="62c13-115">[![Déploiement sur Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="62c13-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="62c13-116">Paramètres</span><span class="sxs-lookup"><span data-stu-id="62c13-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="62c13-117">testUri</span><span class="sxs-lookup"><span data-stu-id="62c13-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="62c13-118">Ressources à déployer</span><span class="sxs-lookup"><span data-stu-id="62c13-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="62c13-119">Application logique</span><span class="sxs-lookup"><span data-stu-id="62c13-119">Logic app</span></span>
<span data-ttu-id="62c13-120">Crée l'application logique</span><span class="sxs-lookup"><span data-stu-id="62c13-120">Creates the logic app.</span></span>

<span data-ttu-id="62c13-121">Le modèle utilise une valeur de paramètre pour le nom de l'application logique.</span><span class="sxs-lookup"><span data-stu-id="62c13-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="62c13-122">Il définit l'emplacement de l'application logique sur le même emplacement que le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="62c13-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="62c13-123">Cette définition spécifique s’exécute une fois par heure et exécute une commande ping sur l’emplacement spécifié dans le paramètre **testUri** .</span><span class="sxs-lookup"><span data-stu-id="62c13-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-to-run-deployment"></a><span data-ttu-id="62c13-124">Commandes pour l’exécution du déploiement</span><span class="sxs-lookup"><span data-stu-id="62c13-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="62c13-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62c13-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="62c13-126">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="62c13-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



