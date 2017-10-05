---
title: "Créer un groupe de consommateurs et l’espace de noms Azure Event Hubs à l’aide d’un modèle | Microsoft Docs"
description: "Créer un espace de noms Event Hubs avec un concentrateur d’événements et un groupe de consommateurs à l’aide de modèles Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="a5f53-103">Créer un espace de noms Event Hubs avec un Event Hub et un groupe de consommateurs à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a5f53-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="a5f53-104">Cet article montre comment utiliser un modèle Azure Resource Manager qui crée un espace de noms de type Event Hubs avec un concentrateur d’événements et un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="a5f53-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="a5f53-105">L’article montre comment définir les ressources à déployer et configurer les paramètres qui sont spécifiés lors de l’exécution du déploiement.</span><span class="sxs-lookup"><span data-stu-id="a5f53-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="a5f53-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou le personnaliser afin qu’il réponde à vos besoins</span><span class="sxs-lookup"><span data-stu-id="a5f53-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="a5f53-107">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="a5f53-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="a5f53-108">Pour le modèle complet, consultez [Modèle d’Event Hub et de groupe de consommateurs][Event Hub and consumer group template] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a5f53-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="a5f53-109">Pour rechercher les derniers modèles, recherchez Event Hubs dans la galerie de [modèles de démarrage rapide Azure][Azure Quickstart Templates].</span><span class="sxs-lookup"><span data-stu-id="a5f53-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="a5f53-110">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="a5f53-110">What will you deploy?</span></span>
<span data-ttu-id="a5f53-111">Avec ce modèle, vous allez déployer un espace de noms Event Hubs avec un concentrateur d’événements et un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="a5f53-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="a5f53-112">[Event Hubs](event-hubs-what-is-event-hubs.md) est un service de traitement des événements utilisé pour fournir des entrées d’événements et de télémétrie dans Azure à grande échelle, avec faible latence et fiabilité élevée.</span><span class="sxs-lookup"><span data-stu-id="a5f53-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="a5f53-113">Pour exécuter automatiquement le déploiement, cliquez sur le bouton ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a5f53-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="a5f53-114">[![Déploiement sur Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a5f53-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="a5f53-115">Paramètres</span><span class="sxs-lookup"><span data-stu-id="a5f53-115">Parameters</span></span>
<span data-ttu-id="a5f53-116">Azure Resource Manager vous permet de définir des paramètres pour les valeurs que vous voulez spécifier lorsque le modèle est déployé.</span><span class="sxs-lookup"><span data-stu-id="a5f53-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="a5f53-117">Ce modèle inclut une section appelée `Parameters` , qui contient toutes les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="a5f53-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="a5f53-118">Vous devez définir un paramètre pour les valeurs qui varient selon le projet que vous déployez ou l’environnement dans lequel vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="a5f53-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="a5f53-119">Ne définissez pas de paramètres pour les valeurs qui restent inchangées.</span><span class="sxs-lookup"><span data-stu-id="a5f53-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="a5f53-120">Chaque valeur de paramètre dans le modèle définit les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="a5f53-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="a5f53-121">Le modèle définit les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="a5f53-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="a5f53-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="a5f53-122">eventHubNamespaceName</span></span>
<span data-ttu-id="a5f53-123">Nom de l’espace de noms Event Hubs à créer.</span><span class="sxs-lookup"><span data-stu-id="a5f53-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="a5f53-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="a5f53-124">eventHubName</span></span>
<span data-ttu-id="a5f53-125">Nom du concentrateur d’événements créé dans l’espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="a5f53-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="a5f53-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="a5f53-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="a5f53-127">Nom du groupe de consommateurs créé pour le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="a5f53-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="a5f53-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a5f53-128">apiVersion</span></span>
<span data-ttu-id="a5f53-129">Version d’API du modèle.</span><span class="sxs-lookup"><span data-stu-id="a5f53-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="a5f53-130">Ressources à déployer</span><span class="sxs-lookup"><span data-stu-id="a5f53-130">Resources to deploy</span></span>
<span data-ttu-id="a5f53-131">Crée un espace de noms de type **Event Hubs**, avec un concentrateur d’événements et un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="a5f53-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="a5f53-132">Commandes pour l’exécution du déploiement</span><span class="sxs-lookup"><span data-stu-id="a5f53-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="a5f53-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5f53-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="a5f53-134">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="a5f53-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="a5f53-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a5f53-135">Next steps</span></span>
<span data-ttu-id="a5f53-136">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="a5f53-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a5f53-137">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="a5f53-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a5f53-138">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="a5f53-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a5f53-139">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="a5f53-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
