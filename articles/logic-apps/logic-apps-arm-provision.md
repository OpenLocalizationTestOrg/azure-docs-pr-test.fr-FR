---
title: "aaaCreate une application logique à l’aide d’un modèle dans Azure | Documents Microsoft"
description: "Utilisez un toodeploy de modèle Azure Resource Manager une application logique pour la définition de flux de travail."
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
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="b2bc6-103">Créer une application logique à l'aide d'un modèle</span><span class="sxs-lookup"><span data-stu-id="b2bc6-103">Create a Logic App using a template</span></span>
<span data-ttu-id="b2bc6-104">Les modèles fournissent un moyen rapide de toouse connecteurs différents au sein d’une application logique.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="b2bc6-105">Les applications de logique comprend des modèles Azure Resource Manager pour toocreate une application de la logique qui peut être utilisé toodefine des flux de travail.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="b2bc6-106">Vous pouvez définir quelles ressources sont déployées et la manière dont les paramètres toodefine lorsque vous déployez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="b2bc6-107">Vous pouvez utiliser ce modèle pour vos propres scénarios d’entreprise, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="b2bc6-108">Pour plus d’informations sur les propriétés de l’application hello logique, consultez [API de gestion des flux de travail logique d’application](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2bc6-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="b2bc6-109">Pour obtenir des exemples de définition de hello proprement dite, consultez [définitions d’application logique d’auteur](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="b2bc6-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="b2bc6-110">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b2bc6-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b2bc6-111">Pour le modèle complète de hello, consultez [modèle d’application logique](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b2bc6-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="b2bc6-112">Que déployer ?</span><span class="sxs-lookup"><span data-stu-id="b2bc6-112">What you deploy</span></span>
<span data-ttu-id="b2bc6-113">Avec ce modèle, vous déployez une application logique.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="b2bc6-114">déploiement de hello toorun sélectionner automatiquement, hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="b2bc6-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="b2bc6-115">[![Déployer tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b2bc6-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b2bc6-116">Paramètres</span><span class="sxs-lookup"><span data-stu-id="b2bc6-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="b2bc6-117">testUri</span><span class="sxs-lookup"><span data-stu-id="b2bc6-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="b2bc6-118">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="b2bc6-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="b2bc6-119">Application logique</span><span class="sxs-lookup"><span data-stu-id="b2bc6-119">Logic app</span></span>
<span data-ttu-id="b2bc6-120">Crée l’application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-120">Creates hello logic app.</span></span>

<span data-ttu-id="b2bc6-121">modèles de Hello utilise une valeur de paramètre pour le nom de l’application hello logique.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="b2bc6-122">Il définit l’emplacement hello de hello logique application toohello même emplacement que le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="b2bc6-123">Cette définition spécifique s’exécute une fois par heure et les tests ping hello emplacement spécifié dans hello **testUri** paramètre.</span><span class="sxs-lookup"><span data-stu-id="b2bc6-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

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


## <a name="commands-toorun-deployment"></a><span data-ttu-id="b2bc6-124">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="b2bc6-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="b2bc6-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2bc6-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="b2bc6-126">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b2bc6-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



