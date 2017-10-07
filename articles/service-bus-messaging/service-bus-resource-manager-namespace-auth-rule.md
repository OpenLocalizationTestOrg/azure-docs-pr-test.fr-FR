---
title: "règle d’autorisation d’aaaCreate Service Bus à l’aide du modèle Azure Resource Manager | Documents Microsoft"
description: "Créer une règle d’autorisation Service Bus pour l’espace de noms et la file d’attente à l’aide d’un modèle Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="5b19a-103">Créer une règle d’autorisation Service Bus pour l’espace de noms et la file d’attente à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5b19a-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="5b19a-104">Cet article explique comment toouse un modèle Azure Resource Manager qui crée un [règle d’autorisation](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) pour un espace de noms Service Bus et la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5b19a-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="5b19a-105">Vous allez apprendre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="5b19a-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="5b19a-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="5b19a-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="5b19a-107">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="5b19a-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="5b19a-108">Pour le modèle complète de hello, consultez hello [le modèle de règle d’autorisation Service Bus] [ Service Bus auth rule template] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="5b19a-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="5b19a-109">Hello suivant modèles Azure Resource Manager est disponible pour le téléchargement et déploiement.</span><span class="sxs-lookup"><span data-stu-id="5b19a-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="5b19a-110">Création d'un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="5b19a-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="5b19a-111">Créer un espace de noms Service Bus avec file d’attente</span><span class="sxs-lookup"><span data-stu-id="5b19a-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="5b19a-112">Créer un espace de noms Service Bus par rubrique et abonnement</span><span class="sxs-lookup"><span data-stu-id="5b19a-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="5b19a-113">Créer un modèle d’espace de noms Service Bus avec rubrique, abonnement et règle</span><span class="sxs-lookup"><span data-stu-id="5b19a-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="5b19a-114">toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherchez « Service Bus ».</span><span class="sxs-lookup"><span data-stu-id="5b19a-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="5b19a-115">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="5b19a-115">What will you deploy?</span></span>
<span data-ttu-id="5b19a-116">Avec ce modèle, vous allez déployer une règle d’autorisation Service Bus pour un espace de noms et une entité de messagerie (une file d’attente, dans le cas présent).</span><span class="sxs-lookup"><span data-stu-id="5b19a-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="5b19a-117">Ce modèle utilise la [signature d’accès partagé (SAP)](service-bus-sas.md) pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="5b19a-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="5b19a-118">SAS permet d’applications tooauthenticate tooService Bus à l’aide d’une clé d’accès configurée sur l’espace de noms hello, ou sur hello messagerie entité (file d’attente ou rubrique) avec les droits spécifiques sont associés.</span><span class="sxs-lookup"><span data-stu-id="5b19a-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="5b19a-119">Vous pouvez ensuite utiliser cette clé toogenerate un jeton SAP que les clients peuvent utiliser ensuite tooauthenticate tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="5b19a-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="5b19a-120">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="5b19a-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="5b19a-121">[![Déployer tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5b19a-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="5b19a-122">Paramètres</span><span class="sxs-lookup"><span data-stu-id="5b19a-122">Parameters</span></span>

<span data-ttu-id="5b19a-123">Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="5b19a-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="5b19a-124">modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="5b19a-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="5b19a-125">Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="5b19a-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="5b19a-126">Ne définissez pas de paramètres pour les valeurs qui resteront toujours hello même.</span><span class="sxs-lookup"><span data-stu-id="5b19a-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="5b19a-127">Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="5b19a-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="5b19a-128">modèle de Hello définit hello paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="5b19a-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="5b19a-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="5b19a-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="5b19a-130">nom de Hello de toocreate d’espace de noms hello Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5b19a-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="5b19a-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="5b19a-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="5b19a-132">Hello nom de la règle d’autorisation hello hello espace de noms.</span><span class="sxs-lookup"><span data-stu-id="5b19a-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="5b19a-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="5b19a-133">serviceBusQueueName</span></span>
<span data-ttu-id="5b19a-134">nom Hello de file d’attente hello dans l’espace de noms Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="5b19a-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="5b19a-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="5b19a-135">serviceBusApiVersion</span></span>
<span data-ttu-id="5b19a-136">version de l’API Service Bus Hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="5b19a-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="5b19a-137">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="5b19a-137">Resources toodeploy</span></span>
<span data-ttu-id="5b19a-138">Crée un espace de noms Service Bus standard de type **Messagerie**et une règle d'autorisation Service Bus pour l'espace de noms et l'entité.</span><span class="sxs-lookup"><span data-stu-id="5b19a-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="5b19a-139">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="5b19a-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="5b19a-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b19a-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="5b19a-141">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="5b19a-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="5b19a-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b19a-142">Next steps</span></span>
<span data-ttu-id="5b19a-143">Maintenant que vous avez créé et déployé des ressources à l’aide du Gestionnaire de ressources Azure, découvrez comment toomanage ces ressources en consultant les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="5b19a-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="5b19a-144">Gestion de Service Bus avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b19a-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="5b19a-145">Gérer les ressources de Service Bus avec hello Explorateur Service Bus</span><span class="sxs-lookup"><span data-stu-id="5b19a-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="5b19a-146">Authentification et de autorisation Service Bus</span><span class="sxs-lookup"><span data-stu-id="5b19a-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
