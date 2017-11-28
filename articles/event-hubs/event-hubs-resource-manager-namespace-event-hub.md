---
title: "un groupe d’espace de noms et le consommateur concentrateurs d’événements Azure à l’aide d’un modèle d’aaaCreate | Documents Microsoft"
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
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="eca32-103">Créer un espace de noms Event Hubs avec un Event Hub et un groupe de consommateurs à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eca32-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="eca32-104">Cet article explique comment toouse un modèle Azure Resource Manager qui crée un espace de noms de type Event Hubs, avec un concentrateur d’un événements et un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="eca32-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="eca32-105">Hello article montre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="eca32-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="eca32-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins</span><span class="sxs-lookup"><span data-stu-id="eca32-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="eca32-107">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="eca32-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="eca32-108">Pour le modèle complète de hello, consultez hello [modèle groupe hub et consommateur d’événement] [ Event Hub and consumer group template] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="eca32-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="eca32-109">toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherche pour les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="eca32-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="eca32-110">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="eca32-110">What will you deploy?</span></span>
<span data-ttu-id="eca32-111">Avec ce modèle, vous allez déployer un espace de noms Event Hubs avec un concentrateur d’événements et un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="eca32-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="eca32-112">[Concentrateurs d’événements](event-hubs-what-is-event-hubs.md) est un événement de traitement de service utilisé tooprovide événement et les données de télémétrie entrée tooAzure à très grande échelle, avec une latence faible et une haute fiabilité.</span><span class="sxs-lookup"><span data-stu-id="eca32-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="eca32-113">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="eca32-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="eca32-114">[![Déployer tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="eca32-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="eca32-115">Paramètres</span><span class="sxs-lookup"><span data-stu-id="eca32-115">Parameters</span></span>
<span data-ttu-id="eca32-116">Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="eca32-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="eca32-117">modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="eca32-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="eca32-118">Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou sur toowhich d’environnement hello que vous déployez.</span><span class="sxs-lookup"><span data-stu-id="eca32-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="eca32-119">Ne définissez pas de paramètres pour les valeurs qui doivent restent hello identiques.</span><span class="sxs-lookup"><span data-stu-id="eca32-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="eca32-120">Chaque valeur de paramètre dans le modèle de hello définit les ressources de hello qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="eca32-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="eca32-121">modèle de Hello définit hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="eca32-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="eca32-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="eca32-122">eventHubNamespaceName</span></span>
<span data-ttu-id="eca32-123">nom de Hello de toocreate d’espace de noms hello concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="eca32-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="eca32-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="eca32-124">eventHubName</span></span>
<span data-ttu-id="eca32-125">nom de Hello du concentrateur d’événements hello créé dans l’espace de noms hello concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="eca32-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="eca32-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="eca32-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="eca32-127">nom de Hello du groupe de consommateurs hello créé pour le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="eca32-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="eca32-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="eca32-128">apiVersion</span></span>
<span data-ttu-id="eca32-129">version de Hello API du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="eca32-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="eca32-130">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="eca32-130">Resources toodeploy</span></span>
<span data-ttu-id="eca32-131">Crée un espace de noms de type **Event Hubs**, avec un concentrateur d’événements et un groupe de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="eca32-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="eca32-132">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="eca32-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="eca32-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eca32-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="eca32-134">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="eca32-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="eca32-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eca32-135">Next steps</span></span>
<span data-ttu-id="eca32-136">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="eca32-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="eca32-137">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="eca32-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="eca32-138">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="eca32-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="eca32-139">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="eca32-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
