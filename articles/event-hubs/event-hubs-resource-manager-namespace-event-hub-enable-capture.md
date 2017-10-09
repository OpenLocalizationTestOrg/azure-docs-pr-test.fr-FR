---
title: "un espace de noms Azure Event Hubs et l’activer à l’aide d’un modèle de Capture d’aaaCreate | Documents Microsoft"
description: "Créer un espace de noms Azure Event Hubs avec un concentrateur d’événements et activer Capture à l’aide d’un modèle Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="4361f-103">Créer un espace de noms Event Hubs avec un concentrateur d’événements et activer Capture à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4361f-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="4361f-104">Cet article explique comment toouse un modèle Azure Resource Manager qui crée un espace de noms du service Event Hubs, instance de concentrateur d’un événement, mais aussi Active hello [la fonctionnalité de Capture](event-hubs-capture-overview.md) sur le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="4361f-105">Hello explique comment toodefine quelles ressources sont déployées, et comment toodefine les paramètres qui sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="4361f-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="4361f-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="4361f-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="4361f-107">Cet article également indique comment toospecify que les événements sont capturés dans des objets BLOB de stockage Azure ou d’un Azure Data Lake Store, en se basant sur hello destination que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="4361f-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="4361f-108">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="4361f-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="4361f-109">Pour plus d’informations sur les modèles et les pratiques des conventions d’affectation de noms des ressources Azure, consultez [Conventions d’affectation de noms des ressources Azure][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="4361f-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="4361f-110">Pour les modèles de hello terminée, cliquez sur hello suivant les liens de GitHub :</span><span class="sxs-lookup"><span data-stu-id="4361f-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="4361f-111">[Modèle de tooStorage Capture hub et activer des événements][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="4361f-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="4361f-112">[Concentrateur et activer la Capture tooAzure Data Lake Store modèle d’événement][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="4361f-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="4361f-113">toocheck pour les derniers modèles de hello, visitez hello [modèles de démarrage rapide Azure] [ Azure Quickstart Templates] la galerie et recherche pour les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="4361f-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="4361f-114">Qu'allez-vous déployer ?</span><span class="sxs-lookup"><span data-stu-id="4361f-114">What will you deploy?</span></span>

<span data-ttu-id="4361f-115">Avec ce modèle, vous déployez un espace de noms Event Hubs avec un concentrateur d’événements, et activez [Event Hubs Capture](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4361f-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="4361f-116">[Concentrateurs d’événements](event-hubs-what-is-event-hubs.md) est un événement de traitement de service utilisé tooprovide événement et les données de télémétrie entrée tooAzure à très grande échelle, avec une latence faible et une haute fiabilité.</span><span class="sxs-lookup"><span data-stu-id="4361f-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="4361f-117">Événement concentrateurs Capture permet de vous tooautomatically remettre hello de diffusion en continu des données dans le stockage d’objets Blob tooAzure concentrateurs d’événements ou Azure Data Lake Store dans un intervalle de taille de votre choix ou de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="4361f-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="4361f-118">Cliquez sur hello suivant tooenable bouton capturer des concentrateurs d’événements dans le stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="4361f-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="4361f-119">[![Déployer tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="4361f-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="4361f-120">Cliquez sur hello suivant tooenable bouton capturer des concentrateurs d’événements dans Azure Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="4361f-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="4361f-121">[![Déployer tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="4361f-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="4361f-122">Paramètres</span><span class="sxs-lookup"><span data-stu-id="4361f-122">Parameters</span></span>

<span data-ttu-id="4361f-123">Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="4361f-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="4361f-124">modèle de Hello inclut une section appelée `Parameters` qui contient toutes les valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="4361f-125">Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="4361f-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="4361f-126">Ne définissez pas de paramètres pour les valeurs qui doivent restent hello identiques.</span><span class="sxs-lookup"><span data-stu-id="4361f-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="4361f-127">Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="4361f-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="4361f-128">modèle de Hello définit hello paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="4361f-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="4361f-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="4361f-129">eventHubNamespaceName</span></span>

<span data-ttu-id="4361f-130">nom Hello Hello [espace de noms de concentrateurs d’événements](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="4361f-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="4361f-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="4361f-131">eventHubName</span></span>

<span data-ttu-id="4361f-132">nom de Hello du concentrateur d’événements hello créé Bonjour [espace de noms de concentrateurs d’événements](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="4361f-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="4361f-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="4361f-133">messageRetentionInDays</span></span>

<span data-ttu-id="4361f-134">nombre de Hello de messages de type hello tooretain jours dans le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="4361f-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="4361f-135">partitionCount</span></span>

<span data-ttu-id="4361f-136">nombre de Hello de toocreate de partitions dans le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-136">hello number of partitions toocreate in hello event hub.</span></span>

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a><span data-ttu-id="4361f-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="4361f-137">captureEnabled</span></span>

<span data-ttu-id="4361f-138">Activer la Capture sur le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-138">Enable Capture on hello event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="4361f-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="4361f-139">captureEncodingFormat</span></span>

<span data-ttu-id="4361f-140">format d’encodage Hello vous spécifiez les données d’événement tooserialize hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-140">hello encoding format you specify tooserialize hello event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="4361f-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="4361f-141">captureTime</span></span>

<span data-ttu-id="4361f-142">intervalle de temps Hello dans lequel capturer des concentrateurs d’événements démarre la capture des données de hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="4361f-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="4361f-143">captureSize</span></span>
<span data-ttu-id="4361f-144">intervalle de salutation taille à laquelle la Capture démarre la capture des données de hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-144">hello size interval at which Capture starts capturing hello data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="4361f-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="4361f-145">captureNameFormat</span></span>

<span data-ttu-id="4361f-146">format du nom Hello utilisé par les fichiers d’Avro capturer des concentrateurs d’événements toowrite hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="4361f-147">Notez qu’un format de nom de Capture doit contenir les champs `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` et `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="4361f-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="4361f-148">Ceux-ci peuvent être organisés dans n’importe quel ordre, avec ou sans délimiteurs.</span><span class="sxs-lookup"><span data-stu-id="4361f-148">These can be arranged in any order, with or without delimiters.</span></span>
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a><span data-ttu-id="4361f-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4361f-149">apiVersion</span></span>

<span data-ttu-id="4361f-150">version de Hello API du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="4361f-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="4361f-151">Utilisez hello paramètres suivants si vous choisissez le stockage Azure comme destination.</span><span class="sxs-lookup"><span data-stu-id="4361f-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="4361f-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="4361f-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="4361f-153">Capture requiert un compte de stockage Azure ressource tooenable ID capture tooyour souhaité compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4361f-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="4361f-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="4361f-154">blobContainerName</span></span>

<span data-ttu-id="4361f-155">Bonjour conteneur d’objets blob qui toocapture vos données d’événement.</span><span class="sxs-lookup"><span data-stu-id="4361f-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="4361f-156">Utilisez hello paramètres suivants si vous choisissez Azure Data Lake Store comme destination.</span><span class="sxs-lookup"><span data-stu-id="4361f-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="4361f-157">Vous devez définir des autorisations sur votre chemin d’accès Data Lake Store, dans lequel vous souhaitez les événements de hello tooCapture.</span><span class="sxs-lookup"><span data-stu-id="4361f-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="4361f-158">autorisations de tooset, consultez [cet article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="4361f-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="4361f-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4361f-159">subscriptionId</span></span>

<span data-ttu-id="4361f-160">ID d’abonnement pour l’espace de noms de concentrateurs d’événements hello et Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4361f-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="4361f-161">Les deux ces ressources doivent être sous hello même ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="4361f-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="4361f-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="4361f-162">dataLakeAccountName</span></span>

<span data-ttu-id="4361f-163">nom d’Azure Data Lake Store Hello pourquoi les événements capturés.</span><span class="sxs-lookup"><span data-stu-id="4361f-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="4361f-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="4361f-164">dataLakeFolderPath</span></span>

<span data-ttu-id="4361f-165">chemin d’accès du dossier de destination Hello pourquoi les événements capturés.</span><span class="sxs-lookup"><span data-stu-id="4361f-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="4361f-166">Toodeploy de ressources pour le stockage Azure en tant qu’événements toocaptured de destination</span><span class="sxs-lookup"><span data-stu-id="4361f-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="4361f-167">Crée un espace de noms de type **EventHubs**, concentrateur d’un événements et également permet de capturer tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="4361f-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="4361f-168">Toodeploy de ressources pour Azure Data Lake Store en tant que destination</span><span class="sxs-lookup"><span data-stu-id="4361f-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="4361f-169">Crée un espace de noms de type **EventHubs**, concentrateur d’un événements et également Active Capture tooAzure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4361f-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="4361f-170">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="4361f-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="4361f-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4361f-171">PowerShell</span></span>

<span data-ttu-id="4361f-172">Déployer votre tooenable modèle capturer des concentrateurs d’événements dans le stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="4361f-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="4361f-173">Déployer votre tooenable modèle capturer des concentrateurs d’événements dans Azure Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="4361f-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="4361f-174">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4361f-174">Azure CLI</span></span>

<span data-ttu-id="4361f-175">Choisir le stockage Blob Azure comme destination :</span><span class="sxs-lookup"><span data-stu-id="4361f-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="4361f-176">Choisir Azure Data Lake Store comme destination :</span><span class="sxs-lookup"><span data-stu-id="4361f-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="4361f-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4361f-177">Next steps</span></span>

<span data-ttu-id="4361f-178">Vous pouvez également configurer capturer des concentrateurs d’événements via hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4361f-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4361f-179">Pour plus d’informations, consultez [à l’aide d’activer la Capture de concentrateurs événement hello Azure portal](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4361f-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="4361f-180">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="4361f-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="4361f-181">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="4361f-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="4361f-182">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="4361f-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="4361f-183">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="4361f-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
