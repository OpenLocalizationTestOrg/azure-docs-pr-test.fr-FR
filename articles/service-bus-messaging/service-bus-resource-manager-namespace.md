---
title: "espace de noms Service Bus aaaCreate à l’aide d’un modèle Azure Resource Manager | Documents Microsoft"
description: "Utilisez Azure Resource Manager modèle toocreate un espace de noms Service Bus"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="c7763-103">Créer un espace de noms Service Bus à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7763-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="c7763-104">Cet article décrit comment toouse un modèle Azure Resource Manager qui crée un espace de noms Service Bus de type **messagerie** avec une référence de base/Standard.</span><span class="sxs-lookup"><span data-stu-id="c7763-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="c7763-105">article de Hello définit également les paramètres de hello qui sont spécifiés pour l’exécution de hello du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="c7763-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="c7763-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="c7763-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="c7763-107">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="c7763-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="c7763-108">Pour le modèle complète de hello, consultez hello [modèle d’espace de noms Service Bus] [ Service Bus namespace template] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="c7763-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="c7763-109">Hello suivant modèles Azure Resource Manager est disponible pour le téléchargement et déploiement.</span><span class="sxs-lookup"><span data-stu-id="c7763-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="c7763-110">Créer un espace de noms Service Bus avec file d’attente</span><span class="sxs-lookup"><span data-stu-id="c7763-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="c7763-111">Créer un espace de noms Service Bus par rubrique et abonnement</span><span class="sxs-lookup"><span data-stu-id="c7763-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="c7763-112">Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="c7763-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="c7763-113">Créer un modèle d’espace de noms Service Bus avec rubrique, abonnement et règle</span><span class="sxs-lookup"><span data-stu-id="c7763-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="c7763-114">toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherchez le Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c7763-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="c7763-115">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="c7763-115">What will you deploy?</span></span>
<span data-ttu-id="c7763-116">Avec ce modèle, vous allez déployer un espace de noms Service Bus avec une référence (SKU) [De base, Standard ou Premium](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="c7763-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="c7763-117">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="c7763-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="c7763-118">[![Déployer tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="c7763-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="c7763-119">Paramètres</span><span class="sxs-lookup"><span data-stu-id="c7763-119">Parameters</span></span>
<span data-ttu-id="c7763-120">Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="c7763-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="c7763-121">modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="c7763-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="c7763-122">Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="c7763-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="c7763-123">Ne définissez pas de paramètres pour les valeurs qui resteront toujours hello même.</span><span class="sxs-lookup"><span data-stu-id="c7763-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="c7763-124">Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="c7763-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="c7763-125">Ce modèle définit les paramètres suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="c7763-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="c7763-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="c7763-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="c7763-127">nom de Hello de toocreate d’espace de noms hello Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c7763-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="c7763-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="c7763-128">serviceBusSKU</span></span>
<span data-ttu-id="c7763-129">nom Hello Hello Service Bus [référence (SKU)](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span><span class="sxs-lookup"><span data-stu-id="c7763-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="c7763-130">modèle de Hello définit les valeurs hello qui sont autorisées pour ce paramètre (Basic, Standard ou Premium) et affecte la valeur par défaut (Standard) si aucune valeur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="c7763-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="c7763-131">Pour plus d’informations sur la tarification de Service Bus, consultez [Service Bus pricing and billing (Tarification et facturation de Service Bus)][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="c7763-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="c7763-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="c7763-132">serviceBusApiVersion</span></span>
<span data-ttu-id="c7763-133">version de l’API Service Bus Hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="c7763-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="c7763-134">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="c7763-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="c7763-135">Espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="c7763-135">Service Bus namespace</span></span>
<span data-ttu-id="c7763-136">Crée un espace de noms Service Bus standard de type **Messagerie**.</span><span class="sxs-lookup"><span data-stu-id="c7763-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="c7763-137">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="c7763-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="c7763-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7763-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="c7763-139">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c7763-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="c7763-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7763-140">Next steps</span></span>
<span data-ttu-id="c7763-141">Maintenant que vous avez créé et déployé des ressources à l’aide du Gestionnaire de ressources Azure, découvrez comment toomanage ces ressources en lisant les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="c7763-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="c7763-142">Gestion de Service Bus avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7763-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="c7763-143">Gérer les ressources de Service Bus avec hello Explorateur Service Bus</span><span class="sxs-lookup"><span data-stu-id="c7763-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
