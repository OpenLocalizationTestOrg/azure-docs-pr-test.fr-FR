---
title: "Configuration d’une chaîne de connexion pour le stockage Azure | Microsoft Docs"
description: "Configurez une chaîne de connexion pour un compte de stockage Azure. Une chaîne de connexion inclut les informations nécessaires pour authentifier l’accès à un compte de stockage à partir de votre application, pendant l’exécution."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 01aa506e2b47fc29a70592e670a206a2b74248a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="cdbb7-104">Configuration des chaînes de connexion Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="cdbb7-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="cdbb7-105">Une chaîne de connexion inclut les informations d’authentification nécessaires pour que votre application accède aux données dans un compte de stockage Azure pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="cdbb7-106">Vous pouvez configurer les chaînes de connexion pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="cdbb7-107">Connexion à l’émulateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="cdbb7-107">Connect to the Azure storage emulator.</span></span>
* <span data-ttu-id="cdbb7-108">Accès à un compte de stockage dans Azure</span><span class="sxs-lookup"><span data-stu-id="cdbb7-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="cdbb7-109">Accès aux ressources spécifiées dans Azure via une signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="cdbb7-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="cdbb7-110">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="cdbb7-110">Storing your connection string</span></span>
<span data-ttu-id="cdbb7-111">Votre application doit accéder à la chaîne de connexion pendant l’exécution pour authentifier les requêtes transmises au stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span></span> <span data-ttu-id="cdbb7-112">Plusieurs options vous permettant de stocker votre chaîne de connexion s’offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="cdbb7-113">Une application s’exécutant sur le bureau ou sur un appareil peut stocker la chaîne de connexion dans un fichier **app.config** ou **web.config**.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="cdbb7-114">Ajoutez la chaîne de connexion dans la section **AppSettings** de ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-114">Add the connection string to the **AppSettings** section in these files.</span></span>
* <span data-ttu-id="cdbb7-115">Une application s’exécutant dans un service cloud Azure peut stocker la chaîne de connexion dans le [schéma de configuration du service Azure (fichier .cscfg)](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="cdbb7-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="cdbb7-116">Ajoutez la chaîne de connexion à la section **ConfigurationSettings** du fichier de configuration du service.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span></span>
* <span data-ttu-id="cdbb7-117">Vous pouvez utiliser votre chaîne de connexion directement dans votre code.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="cdbb7-118">Cependant, le plus souvent, nous vous recommandons de stocker votre chaîne de connexion dans un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="cdbb7-119">Le stockage de votre chaîne de connexion dans un fichier de configuration facilite la mise à jour de la chaîne de connexion qui vous permet de basculer entre l’émulateur de stockage et un compte de stockage Azure dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span></span> <span data-ttu-id="cdbb7-120">Il vous suffit de modifier la chaîne de connexion pour la faire pointer vers votre environnement cible.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-120">You only need to edit the connection string to point to your target environment.</span></span>

<span data-ttu-id="cdbb7-121">Vous pouvez utiliser [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) pour accéder à votre chaîne de connexion lors de l’exécution, quel que soit l’environnement d’exécution de votre application.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-the-storage-emulator"></a><span data-ttu-id="cdbb7-122">Création d’une chaîne de connexion pour l’émulateur de stockage</span><span class="sxs-lookup"><span data-stu-id="cdbb7-122">Create a connection string for the storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="cdbb7-123">Pour plus d’informations sur l’émulateur de stockage, consultez [Utilisation de l'émulateur de stockage Azure pour le développement et le test](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="cdbb7-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="cdbb7-124">Création d’une chaîne de connexion pour un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="cdbb7-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="cdbb7-125">Pour créer une chaîne de connexion pour votre compte de stockage Azure, utilisez le format suivant.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-125">To create a connection string for your Azure storage account, use the following format.</span></span> <span data-ttu-id="cdbb7-126">Indiquez si vous souhaitez vous connecter au compte de stockage via HTTPS (recommandé) ou HTTP, remplacez `myAccountName` par le nom de votre compte de stockage et remplacez `myAccountKey` par la touche d’accès rapide à votre compte :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="cdbb7-127">Par exemple, votre chaîne de connexion peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="cdbb7-128">Même si le stockage Azure prend en charge HTTP et HTTPS au sein d’une chaîne de connexion, nous vous *conseillons vivement d’utiliser HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="cdbb7-129">Vous trouverez les chaînes de connexion de votre compte de stockage dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cdbb7-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="cdbb7-130">Accédez à **PARAMÈTRES** > **Clés d’accès** dans le panneau de menu de votre compte de stockage pour afficher les chaînes de connexion pour les clés d’accès primaire et secondaire.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="cdbb7-131">Création d’une chaîne de connexion à l’aide d’une signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="cdbb7-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="cdbb7-132">Création d’une chaîne de connexion pour un point de terminaison de stockage explicite</span><span class="sxs-lookup"><span data-stu-id="cdbb7-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="cdbb7-133">Vous pouvez spécifier les points de terminaison de service explicites dans votre chaîne de connexion au lieu d’utiliser les points de terminaison par défaut.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span></span> <span data-ttu-id="cdbb7-134">Pour créer une chaîne de connexion spécifiant un point de terminaison explicite, indiquez le point de terminaison complet de chaque service, ainsi que le protocole (HTTPS (recommandé) ou HTTP) au format suivant :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="cdbb7-135">Si vous avez mappé votre point de terminaison Stockage Blob à un [domaine personnalisé](storage-custom-domain-name.md), il vaut mieux spécifier un point de terminaison explicite.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="cdbb7-136">Dans ce cas, vous pouvez spécifier votre point de terminaison personnalisé pour le stockage Blob dans votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="cdbb7-137">Vous pouvez éventuellement spécifier les points de terminaison par défaut pour les autres services si votre application les utilise.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-137">You can optionally specify the default endpoints for the other services if your application uses them.</span></span>

<span data-ttu-id="cdbb7-138">Voici un exemple de chaîne de connexion qui spécifie un point de terminaison explicite pour le service Blob :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="cdbb7-139">Cet exemple spécifie des points de terminaison explicites pour tous les services, notamment un domaine personnalisé pour le service Blob :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="cdbb7-140">Les valeurs des points de terminaison dans une chaîne de connexion sont utilisées pour construire les URI de demande aux services de stockage. Elles indiquent la forme des URI renvoyés à votre code.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span></span>

<span data-ttu-id="cdbb7-141">Si vous avez mappé un point de terminaison de stockage à un domaine personnalisé et omettez ce point de terminaison d’une chaîne de connexion, vous ne pourrez pas accéder aux données de ce service avec votre code à l’aide de cette chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdbb7-142">Les valeurs des points de terminaison de service dans vos chaînes de connexion doivent être des URI correctement formés, notamment `https://` (recommandé) ou `http://`.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="cdbb7-143">Étant donné que le stockage Azure ne prend pas encore en charge HTTPS pour les domaines personnalisés, vous *devez* spécifier `http://` pour n’importe quel URI de point de terminaison qui pointe vers un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="cdbb7-144">Création d’une chaîne de connexion avec un suffixe de point de terminaison</span><span class="sxs-lookup"><span data-stu-id="cdbb7-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="cdbb7-145">Pour créer une chaîne de connexion pour un service de stockage dans les régions ou les instances avec des suffixes de point de terminaison différents, comme pour Azure China ou Azure Government, utilisez le format de chaîne de connexion suivant.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span></span> <span data-ttu-id="cdbb7-146">Indiquez si vous souhaitez vous connecter au compte de stockage via HTTPS (recommandé) ou HTTP, remplacez `myAccountName` par le nom de votre compte de stockage, remplacez `myAccountKey` par votre clé d’accès au compte et remplacez `mySuffix` par le suffixe d’URI :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="cdbb7-147">Voici un exemple de chaîne de connexion pour des services de stockage dans Azure China :</span><span class="sxs-lookup"><span data-stu-id="cdbb7-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="cdbb7-148">Analyse d’une chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="cdbb7-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cdbb7-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cdbb7-149">Next steps</span></span>
* [<span data-ttu-id="cdbb7-150">Utilisation de l’émulateur de stockage Azure pour le développement et le test</span><span class="sxs-lookup"><span data-stu-id="cdbb7-150">Use the Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="cdbb7-151">Explorateurs du stockage Azure</span><span class="sxs-lookup"><span data-stu-id="cdbb7-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="cdbb7-152">Utilisation des signatures d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="cdbb7-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

