---
title: "espace de noms aaaCreate Azure Service Bus et de file d’attente à l’aide du modèle Azure Resource Manager | Documents Microsoft"
description: "Créer un espace de noms Service Bus et une file d’attente à l’aide d’un modèle Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="5434a-103">Créer un espace de noms Service Bus et une file d’attente à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5434a-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="5434a-104">Cet article explique comment toouse un modèle Azure Resource Manager qui crée un espace de noms Service Bus et une file d’attente au sein de cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="5434a-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="5434a-105">Vous allez apprendre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="5434a-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="5434a-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="5434a-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="5434a-107">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="5434a-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="5434a-108">Pour le modèle complète de hello, consultez hello [modèle d’espace de noms et de file d’attente Service Bus] [ Service Bus namespace and queue template] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="5434a-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="5434a-109">Hello suivant modèles Azure Resource Manager est disponible pour le téléchargement et déploiement.</span><span class="sxs-lookup"><span data-stu-id="5434a-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="5434a-110">Créer un espace de noms Service Bus avec file d'attente et règle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="5434a-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="5434a-111">Créer un espace de noms Service Bus par rubrique et abonnement</span><span class="sxs-lookup"><span data-stu-id="5434a-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="5434a-112">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="5434a-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="5434a-113">Créer un modèle d’espace de noms Service Bus avec rubrique, abonnement et règle</span><span class="sxs-lookup"><span data-stu-id="5434a-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="5434a-114">toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherchez « Service Bus ».</span><span class="sxs-lookup"><span data-stu-id="5434a-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="5434a-115">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="5434a-115">What will you deploy?</span></span>

<span data-ttu-id="5434a-116">Avec ce modèle, vous allez déployer un espace de noms Service Bus avec une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5434a-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="5434a-117">[Les files d’attente Service Bus](service-bus-queues-topics-subscriptions.md#queues) offrent la, tooone de remise de message de premier sorti (FIFO) ou plusieurs consommateurs concurrents.</span><span class="sxs-lookup"><span data-stu-id="5434a-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="5434a-118">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="5434a-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="5434a-119">[![Déployer tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5434a-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="5434a-120">Paramètres</span><span class="sxs-lookup"><span data-stu-id="5434a-120">Parameters</span></span>

<span data-ttu-id="5434a-121">Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="5434a-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="5434a-122">modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="5434a-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="5434a-123">Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="5434a-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="5434a-124">Ne définissez pas de paramètres pour les valeurs qui resteront toujours hello même.</span><span class="sxs-lookup"><span data-stu-id="5434a-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="5434a-125">Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="5434a-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="5434a-126">modèle de Hello définit hello paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="5434a-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="5434a-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="5434a-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="5434a-128">nom de Hello de toocreate d’espace de noms hello Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5434a-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="5434a-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="5434a-129">serviceBusQueueName</span></span>
<span data-ttu-id="5434a-130">nom Hello de file d’attente hello créé dans l’espace de noms Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="5434a-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="5434a-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="5434a-131">serviceBusApiVersion</span></span>
<span data-ttu-id="5434a-132">version de l’API Service Bus Hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="5434a-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="5434a-133">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="5434a-133">Resources toodeploy</span></span>
<span data-ttu-id="5434a-134">Crée un espace de noms Service Bus standard de type **Messagerie**, avec une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5434a-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="5434a-135">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="5434a-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="5434a-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5434a-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="5434a-137">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="5434a-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="5434a-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5434a-138">Next steps</span></span>
<span data-ttu-id="5434a-139">Maintenant que vous avez créé et déployé des ressources à l’aide du Gestionnaire de ressources Azure, découvrez comment toomanage ces ressources en consultant les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="5434a-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="5434a-140">Gestion de Service Bus avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="5434a-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="5434a-141">Gérer les ressources de Service Bus avec hello Explorateur Service Bus</span><span class="sxs-lookup"><span data-stu-id="5434a-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
