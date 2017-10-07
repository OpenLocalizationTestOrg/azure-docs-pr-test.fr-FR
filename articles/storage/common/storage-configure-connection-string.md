---
title: "aaaConfigure une chaîne de connexion pour le stockage Azure | Documents Microsoft"
description: "Configurez une chaîne de connexion pour un compte de stockage Azure. Une chaîne de connexion contient des informations de hello nécessaire tooauthenticate accéder au compte de stockage tooa à partir de votre application lors de l’exécution."
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
ms.openlocfilehash: ac1d7d9bf11fa6f44243cda0c40d8faee12e513b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="6a99a-104">Configuration des chaînes de connexion Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="6a99a-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="6a99a-105">Une chaîne de connexion inclut les informations d’authentification hello requises pour vos données d’application tooaccess dans un compte de stockage Azure lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a99a-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="6a99a-106">Vous pouvez configurer les chaînes de connexion pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a99a-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="6a99a-107">Se connecter toohello émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="6a99a-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="6a99a-108">Accès à un compte de stockage dans Azure</span><span class="sxs-lookup"><span data-stu-id="6a99a-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="6a99a-109">Accès aux ressources spécifiées dans Azure via une signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="6a99a-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="6a99a-110">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="6a99a-110">Storing your connection string</span></span>
<span data-ttu-id="6a99a-111">Votre application doit la chaîne de connexion tooaccess hello au runtime tooauthenticate demandes formulées tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="6a99a-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="6a99a-112">Plusieurs options vous permettant de stocker votre chaîne de connexion s’offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="6a99a-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="6a99a-113">Une application en cours d’exécution sur le bureau de hello ou sur un appareil peut stocker la chaîne de connexion hello dans un **app.config** ou **web.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="6a99a-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="6a99a-114">Ajouter toohello de chaîne de connexion hello **AppSettings** section dans ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="6a99a-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="6a99a-115">Une application en cours d’exécution dans un service cloud Azure peut stocker la chaîne de connexion de hello Bonjour [fichier de schéma (.cscfg) de configuration de service Azure](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a99a-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="6a99a-116">Ajouter toohello de chaîne de connexion hello **ConfigurationSettings** section du fichier de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="6a99a-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="6a99a-117">Vous pouvez utiliser votre chaîne de connexion directement dans votre code.</span><span class="sxs-lookup"><span data-stu-id="6a99a-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="6a99a-118">Cependant, le plus souvent, nous vous recommandons de stocker votre chaîne de connexion dans un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="6a99a-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="6a99a-119">Le stockage de votre chaîne de connexion dans un fichier de configuration rend tooswitch de chaîne de connexion de hello tooupdate facile entre l’émulateur de stockage hello et un compte de stockage Azure dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="6a99a-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="6a99a-120">Il vous suffit d’environnement cible de tooedit hello connexion chaîne toopoint tooyour.</span><span class="sxs-lookup"><span data-stu-id="6a99a-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="6a99a-121">Vous pouvez utiliser hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess votre connexion de chaîne lors de l’exécution, quelle que soit l’où votre application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a99a-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="6a99a-122">Créer une chaîne de connexion pour l’émulateur de stockage hello</span><span class="sxs-lookup"><span data-stu-id="6a99a-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="6a99a-123">Pour plus d’informations sur l’émulateur de stockage hello, consultez [utiliser l’émulateur de stockage Azure hello pour le développement et test](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="6a99a-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="6a99a-124">Création d’une chaîne de connexion pour un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="6a99a-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="6a99a-125">mettre en forme toocreate une chaîne de connexion pour votre compte de stockage Azure, suivant de hello d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="6a99a-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="6a99a-126">Indiquer si vous souhaitez que le compte de stockage tooconnect toohello via HTTPS (recommandé) ou HTTP, remplacez `myAccountName` avec nom hello de votre compte de stockage, puis remplacez `myAccountKey` avec votre clé d’accès de compte :</span><span class="sxs-lookup"><span data-stu-id="6a99a-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="6a99a-127">Par exemple, votre chaîne de connexion peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="6a99a-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="6a99a-128">Même si le stockage Azure prend en charge HTTP et HTTPS au sein d’une chaîne de connexion, nous vous *conseillons vivement d’utiliser HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="6a99a-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="6a99a-129">Vous pouvez trouver des chaînes de connexion de votre compte de stockage Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a99a-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6a99a-130">Accédez trop**paramètres** > **clés d’accès** dans les chaînes de connexion de votre compte de stockage menu Panneau toosee pour les deux clés d’accès primaire et secondaire.</span><span class="sxs-lookup"><span data-stu-id="6a99a-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="6a99a-131">Création d’une chaîne de connexion à l’aide d’une signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="6a99a-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="6a99a-132">Création d’une chaîne de connexion pour un point de terminaison de stockage explicite</span><span class="sxs-lookup"><span data-stu-id="6a99a-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="6a99a-133">Vous pouvez spécifier des points de terminaison de service explicite dans votre chaîne de connexion au lieu d’utiliser des points de terminaison par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="6a99a-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="6a99a-134">toocreate une chaîne de connexion qui spécifie un point de terminaison explicite, spécifiez hello point de terminaison complet pour chaque service, y compris la spécification de protocole hello (HTTPS (recommandé) ou HTTP), Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="6a99a-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="6a99a-135">Un scénario dans lequel vous souhaitez toospecify un point de terminaison explicite est lorsque vous avez mappé votre tooa de point de terminaison de stockage Blob [domaine personnalisé](../blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="6a99a-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](../blobs/storage-custom-domain-name.md).</span></span> <span data-ttu-id="6a99a-136">Dans ce cas, vous pouvez spécifier votre point de terminaison personnalisé pour le stockage Blob dans votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="6a99a-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="6a99a-137">Vous pouvez éventuellement spécifier de points de terminaison par défaut de hello pour hello autres services si votre application les utilise.</span><span class="sxs-lookup"><span data-stu-id="6a99a-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="6a99a-138">Voici un exemple de chaîne de connexion qui spécifie un point de terminaison explicite pour hello service Blob :</span><span class="sxs-lookup"><span data-stu-id="6a99a-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="6a99a-139">Cet exemple spécifie les points de terminaison explicites pour tous les services, y compris un domaine personnalisé pour hello service Blob :</span><span class="sxs-lookup"><span data-stu-id="6a99a-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

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

<span data-ttu-id="6a99a-140">les valeurs de point de terminaison Hello dans une chaîne de connexion sont des services de stockage toohello URI demande de hello tooconstruct utilisés et dictent écran hello de n’importe quel URI renvoyés tooyour code.</span><span class="sxs-lookup"><span data-stu-id="6a99a-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="6a99a-141">Si vous avez mappé un domaine personnalisé de tooa de point de terminaison de stockage et que vous omettez ce point de terminaison à partir d’une chaîne de connexion, puis vous ne serez pas en mesure de toouse cette connexion données de type string tooaccess dans ce service à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="6a99a-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a99a-142">Les valeurs des points de terminaison de service dans vos chaînes de connexion doivent être des URI correctement formés, notamment `https://` (recommandé) ou `http://`.</span><span class="sxs-lookup"><span data-stu-id="6a99a-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="6a99a-143">Étant donné que le stockage Azure ne prend pas en charge HTTPS pour les domaines personnalisés, vous *doit* spécifier `http://` pour n’importe quel point de terminaison URI qui pointe de domaine personnalisé de tooa.</span><span class="sxs-lookup"><span data-stu-id="6a99a-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="6a99a-144">Création d’une chaîne de connexion avec un suffixe de point de terminaison</span><span class="sxs-lookup"><span data-stu-id="6a99a-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="6a99a-145">toocreate une chaîne de connexion pour un service de stockage dans des régions ou des instances avec des suffixes de point de terminaison différent, comme pour la Chine de Azure ou Azure Government, hello utilisation suivant le format de chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="6a99a-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="6a99a-146">Indiquer si vous souhaitez que le compte de stockage tooconnect toohello via HTTPS (recommandé) ou HTTP, remplacez `myAccountName` avec nom hello de votre compte de stockage, remplacez `myAccountKey` avec votre clé d’accès de compte, puis remplacez `mySuffix` par hello URI suffixe :</span><span class="sxs-lookup"><span data-stu-id="6a99a-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="6a99a-147">Voici un exemple de chaîne de connexion pour des services de stockage dans Azure China :</span><span class="sxs-lookup"><span data-stu-id="6a99a-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="6a99a-148">Analyse d’une chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="6a99a-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="6a99a-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a99a-149">Next steps</span></span>
* [<span data-ttu-id="6a99a-150">Utiliser l’émulateur de stockage Azure hello pour le développement et test</span><span class="sxs-lookup"><span data-stu-id="6a99a-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="6a99a-151">Explorateurs du stockage Azure</span><span class="sxs-lookup"><span data-stu-id="6a99a-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="6a99a-152">Utilisation des signatures d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="6a99a-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

