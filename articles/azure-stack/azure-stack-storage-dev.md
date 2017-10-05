---
title: "Bien démarrer avec les outils de développement du stockage Azure Stack"
description: "Guide de démarrage pour l’utilisation des outils de développement du stockage Azure Stack"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 7/21/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: a4c1c316022f992750fe60d28b9be61b17242a64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="381b2-103">Bien démarrer avec les outils de développement du stockage Azure Stack</span><span class="sxs-lookup"><span data-stu-id="381b2-103">Get started with Azure Stack Storage development tools</span></span> 

<span data-ttu-id="381b2-104">Microsoft Azure Stack fournit un ensemble de services de stockage, notamment le stockage Blob, Table et File d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="381b2-104">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="381b2-105">Cet article fournit des conseils rapides sur l’utilisation des outils de développement du stockage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="381b2-105">This article provides quick guidance on how to start using Azure Stack Storage development tools.</span></span> <span data-ttu-id="381b2-106">Des informations plus détaillées et des exemples de code sont disponibles dans les didacticiels correspondants du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="381b2-106">You can find more detailed information and sample code in the corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="381b2-107">Le stockage Azure et le stockage Azure Stack présentent quelques différences connues, y compris certaines exigences spécifiques pour chaque plateforme.</span><span class="sxs-lookup"><span data-stu-id="381b2-107">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="381b2-108">Par exemple, Azure Stack a des bibliothèques clientes spécifiques, de même que des exigences spécifiques en matière de suffixe de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="381b2-108">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="381b2-109">Pour plus d’informations, consultez [Stockage Azure Stack : Différences et considérations](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="381b2-109">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="381b2-110">Bibliothèques clientes Azure</span><span class="sxs-lookup"><span data-stu-id="381b2-110">Azure client libraries</span></span>
<span data-ttu-id="381b2-111">La version d’API REST prise en charge pour le stockage Azure Stack est 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="381b2-111">The supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="381b2-112">Elle n’a pas de parité complète avec la dernière version de l’API REST du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="381b2-112">It doesn’t have full parity with the latest version of the Azure Storage REST API.</span></span> <span data-ttu-id="381b2-113">Par conséquent, pour les bibliothèques clientes de stockage, vous devez connaître la version compatible avec l’API REST 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="381b2-113">So for the storage client libraries, you need to be aware of the version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="381b2-114">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="381b2-114">Client library</span></span>|<span data-ttu-id="381b2-115">Version prise en charge par Azure Stack</span><span class="sxs-lookup"><span data-stu-id="381b2-115">Azure Stack supported version</span></span>|<span data-ttu-id="381b2-116">Lien</span><span class="sxs-lookup"><span data-stu-id="381b2-116">Link</span></span>|<span data-ttu-id="381b2-117">Spécification du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="381b2-117">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="381b2-118">.NET</span><span class="sxs-lookup"><span data-stu-id="381b2-118">.NET</span></span>     |<span data-ttu-id="381b2-119">6.2.0</span><span class="sxs-lookup"><span data-stu-id="381b2-119">6.2.0</span></span>|<span data-ttu-id="381b2-120">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="381b2-120">Nuget package:</span></span><br>[<span data-ttu-id="381b2-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="381b2-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="381b2-122">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="381b2-122">GitHub release:</span></span><br>[<span data-ttu-id="381b2-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="381b2-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="381b2-124">Fichier app.config</span><span class="sxs-lookup"><span data-stu-id="381b2-124">app.config file</span></span>|
|<span data-ttu-id="381b2-125">Java</span><span class="sxs-lookup"><span data-stu-id="381b2-125">Java</span></span>|<span data-ttu-id="381b2-126">4.1.0</span><span class="sxs-lookup"><span data-stu-id="381b2-126">4.1.0</span></span>|<span data-ttu-id="381b2-127">Package Maven :</span><span class="sxs-lookup"><span data-stu-id="381b2-127">Maven package:</span></span><br>[<span data-ttu-id="381b2-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="381b2-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="381b2-129">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="381b2-129">GitHub release:</span></span><br> [<span data-ttu-id="381b2-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="381b2-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="381b2-131">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="381b2-131">Connection string setup</span></span>|
|<span data-ttu-id="381b2-132">Node.js</span><span class="sxs-lookup"><span data-stu-id="381b2-132">Node.js</span></span>     |<span data-ttu-id="381b2-133">1.1.0</span><span class="sxs-lookup"><span data-stu-id="381b2-133">1.1.0</span></span>|<span data-ttu-id="381b2-134">Lien NPM :</span><span class="sxs-lookup"><span data-stu-id="381b2-134">NPM link:</span></span><br>[<span data-ttu-id="381b2-135">https://www.npmjs.com/package/azure-storage</span><span class="sxs-lookup"><span data-stu-id="381b2-135">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="381b2-136">(exécuter : `npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="381b2-136">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="381b2-137">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="381b2-137">Github release:</span></span><br>[<span data-ttu-id="381b2-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="381b2-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="381b2-139">Déclaration d’instance de service</span><span class="sxs-lookup"><span data-stu-id="381b2-139">Service instance declaration</span></span>||<span data-ttu-id="381b2-140">C++</span><span class="sxs-lookup"><span data-stu-id="381b2-140">C++</span></span>|<span data-ttu-id="381b2-141">2.4.0</span><span class="sxs-lookup"><span data-stu-id="381b2-141">2.4.0</span></span>|<span data-ttu-id="381b2-142">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="381b2-142">Nuget package:</span></span><br>[<span data-ttu-id="381b2-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="381b2-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="381b2-144">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="381b2-144">GitHub release:</span></span><br>[<span data-ttu-id="381b2-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="381b2-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="381b2-146">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="381b2-146">Connection string setup</span></span>|
|<span data-ttu-id="381b2-147">C++</span><span class="sxs-lookup"><span data-stu-id="381b2-147">C++</span></span>|<span data-ttu-id="381b2-148">2.4.0</span><span class="sxs-lookup"><span data-stu-id="381b2-148">2.4.0</span></span>|<span data-ttu-id="381b2-149">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="381b2-149">Nuget package:</span></span><br>[<span data-ttu-id="381b2-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="381b2-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="381b2-151">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="381b2-151">GitHub release:</span></span><br>[<span data-ttu-id="381b2-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="381b2-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="381b2-153">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="381b2-153">Connection string setup</span></span>|
|<span data-ttu-id="381b2-154">PHP</span><span class="sxs-lookup"><span data-stu-id="381b2-154">PHP</span></span>|<span data-ttu-id="381b2-155">0.15.0</span><span class="sxs-lookup"><span data-stu-id="381b2-155">0.15.0</span></span>|<span data-ttu-id="381b2-156">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="381b2-156">GitHub release:</span></span><br>[<span data-ttu-id="381b2-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span><span class="sxs-lookup"><span data-stu-id="381b2-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="381b2-158">Installation via Composer (voir détails ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="381b2-158">Install via Composer (see details below)</span></span>|<span data-ttu-id="381b2-159">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="381b2-159">Connection string setup</span></span>|
|<span data-ttu-id="381b2-160">Python</span><span class="sxs-lookup"><span data-stu-id="381b2-160">Python</span></span>     |<span data-ttu-id="381b2-161">0.30.0</span><span class="sxs-lookup"><span data-stu-id="381b2-161">0.30.0</span></span>|<span data-ttu-id="381b2-162">Package PIP :</span><span class="sxs-lookup"><span data-stu-id="381b2-162">PIP package:</span></span><br> [<span data-ttu-id="381b2-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="381b2-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="381b2-164">(Exécuter : `pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="381b2-164">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="381b2-165">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="381b2-165">GitHub release:</span></span><br> [<span data-ttu-id="381b2-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span><span class="sxs-lookup"><span data-stu-id="381b2-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="381b2-167">Déclaration d’instance de service</span><span class="sxs-lookup"><span data-stu-id="381b2-167">Service instance declaration</span></span>|
|<span data-ttu-id="381b2-168">Ruby</span><span class="sxs-lookup"><span data-stu-id="381b2-168">Ruby</span></span>|<span data-ttu-id="381b2-169">0.12.1</span><span class="sxs-lookup"><span data-stu-id="381b2-169">0.12.1</span></span><br><span data-ttu-id="381b2-170">VERSION PRÉLIMINAIRE</span><span class="sxs-lookup"><span data-stu-id="381b2-170">Preview</span></span>|<span data-ttu-id="381b2-171">Package RubyGems :</span><span class="sxs-lookup"><span data-stu-id="381b2-171">RubyGems package:</span></span><br> [<span data-ttu-id="381b2-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span><span class="sxs-lookup"><span data-stu-id="381b2-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="381b2-173">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="381b2-173">GitHub release:</span></span><br> [<span data-ttu-id="381b2-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span><span class="sxs-lookup"><span data-stu-id="381b2-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="381b2-175">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="381b2-175">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="381b2-176">Détails PHP</span><span class="sxs-lookup"><span data-stu-id="381b2-176">PHP details</span></span><br><br>
><span data-ttu-id="381b2-177">Pour installer via Composer :</span><span class="sxs-lookup"><span data-stu-id="381b2-177">To install via Composer:</span></span>
>1. <span data-ttu-id="381b2-178">Créez un fichier nommé `composer.json` à la racine du projet avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="381b2-178">Create a file named `composer.json` in the root of the project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="381b2-179">Téléchargez [composer.phar](http://getcomposer.org/composer.phar) à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="381b2-179">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span></span>
>3. <span data-ttu-id="381b2-180">Exécutez : `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="381b2-180">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="381b2-181">Déclaration de point de terminaison</span><span class="sxs-lookup"><span data-stu-id="381b2-181">Endpoint declaration</span></span>
<span data-ttu-id="381b2-182">Un point de terminaison Azure Stack comprend deux parties : le nom d’une région et le domaine Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="381b2-182">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span>
<span data-ttu-id="381b2-183">Dans le Kit de développement Azure Stack, le point de terminaison par défaut est **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="381b2-183">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="381b2-184">Contactez votre administrateur cloud si vous n’êtes pas sûr de votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="381b2-184">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="381b2-185">Exemples</span><span class="sxs-lookup"><span data-stu-id="381b2-185">Examples</span></span>


### <a name="net"></a><span data-ttu-id="381b2-186">.NET</span><span class="sxs-lookup"><span data-stu-id="381b2-186">.NET</span></span>

<span data-ttu-id="381b2-187">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans le fichier app.config :</span><span class="sxs-lookup"><span data-stu-id="381b2-187">For Azure Stack, the endpoint suffix is specified in the app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="381b2-188">Java</span><span class="sxs-lookup"><span data-stu-id="381b2-188">Java</span></span>

<span data-ttu-id="381b2-189">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans la configuration de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="381b2-189">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="381b2-190">Node.js</span><span class="sxs-lookup"><span data-stu-id="381b2-190">Node.js</span></span>

<span data-ttu-id="381b2-191">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans l’instance de déclaration :</span><span class="sxs-lookup"><span data-stu-id="381b2-191">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="381b2-192">C++</span><span class="sxs-lookup"><span data-stu-id="381b2-192">C++</span></span>

<span data-ttu-id="381b2-193">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans la configuration de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="381b2-193">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="381b2-194">PHP</span><span class="sxs-lookup"><span data-stu-id="381b2-194">PHP</span></span>

<span data-ttu-id="381b2-195">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans la configuration de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="381b2-195">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="381b2-196">Python</span><span class="sxs-lookup"><span data-stu-id="381b2-196">Python</span></span>

<span data-ttu-id="381b2-197">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans l’instance de déclaration :</span><span class="sxs-lookup"><span data-stu-id="381b2-197">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="381b2-198">Ruby</span><span class="sxs-lookup"><span data-stu-id="381b2-198">Ruby</span></span>

<span data-ttu-id="381b2-199">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans la configuration de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="381b2-199">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="381b2-200">Stockage d'objets blob</span><span class="sxs-lookup"><span data-stu-id="381b2-200">Blob storage</span></span>

<span data-ttu-id="381b2-201">Les didacticiels du stockage Blob Azure suivants sont applicables à Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="381b2-201">The following Azure Blob storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="381b2-202">Notez l’exigence particulière d’un suffixe de point de terminaison pour Azure Stack, décrit dans la précédente section [Exemples](#examples).</span><span class="sxs-lookup"><span data-stu-id="381b2-202">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="381b2-203">Prise en main d’Azure Blob Storage à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="381b2-203">Get started with Azure Blob storage using .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="381b2-204">Utilisation du stockage d'objets blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="381b2-204">How to use Blob storage from Java</span></span>](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="381b2-205">Utilisation du stockage d'objets blob à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="381b2-205">How to use Blob storage from Node.js</span></span>](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="381b2-206">Utilisation du stockage d’objets blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="381b2-206">How to use Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="381b2-207">Utilisation du stockage d'objets blob à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="381b2-207">How to use Blob storage from PHP</span></span>](../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="381b2-208">Utilisation du stockage Blob Azure à partir de Python</span><span class="sxs-lookup"><span data-stu-id="381b2-208">How to use Azure Blob storage from Python</span></span>](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="381b2-209">Utilisation du stockage d'objets blob à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="381b2-209">How to use Blob storage from Ruby</span></span>](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="381b2-210">Stockage de files d'attente</span><span class="sxs-lookup"><span data-stu-id="381b2-210">Queue storage</span></span>

<span data-ttu-id="381b2-211">Les didacticiels du stockage File d’attente Azure suivants sont applicables à Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="381b2-211">The following Azure Queue storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="381b2-212">Notez l’exigence particulière d’un suffixe de point de terminaison pour Azure Stack, décrit dans la précédente section [Exemples](#examples).</span><span class="sxs-lookup"><span data-stu-id="381b2-212">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="381b2-213">Prise en main du stockage de files d’attente Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="381b2-213">Get started with Azure Queue storage using .NET</span></span>](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="381b2-214">Utilisation du stockage de files d'attente à partir de Java</span><span class="sxs-lookup"><span data-stu-id="381b2-214">How to use Queue storage from Java</span></span>](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="381b2-215">Utilisation du stockage de files d'attente à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="381b2-215">How to use Queue storage from Node.js</span></span>](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="381b2-216">Utilisation du service de stockage de files d’attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="381b2-216">How to use Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="381b2-217">Utilisation du stockage de files d'attente à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="381b2-217">How to use Queue storage from PHP</span></span>](../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="381b2-218">Utilisation du stockage de files d'attente à partir de Python</span><span class="sxs-lookup"><span data-stu-id="381b2-218">How to use Queue storage from Python</span></span>](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="381b2-219">Utilisation du stockage de files d'attente à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="381b2-219">How to use Queue storage from Ruby</span></span>](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="381b2-220">Stockage de tables</span><span class="sxs-lookup"><span data-stu-id="381b2-220">Table storage</span></span>

<span data-ttu-id="381b2-221">Les didacticiels du stockage Table Azure suivants sont applicables à Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="381b2-221">The following Azure Table storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="381b2-222">Notez l’exigence particulière d’un suffixe de point de terminaison pour Azure Stack, décrit dans la précédente section [Exemples](#examples).</span><span class="sxs-lookup"><span data-stu-id="381b2-222">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="381b2-223">Prise en main d’Azure Table Storage à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="381b2-223">Get started with Azure Table storage using .NET</span></span>](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="381b2-224">Utilisation du stockage de tables à partir de Java</span><span class="sxs-lookup"><span data-stu-id="381b2-224">How to use Table storage from Java</span></span>](../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="381b2-225">Utilisation du stockage Table Azure à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="381b2-225">How to use Azure Table storage from Node.js</span></span>](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="381b2-226">Utilisation du stockage Table à partir de C++</span><span class="sxs-lookup"><span data-stu-id="381b2-226">How to use Table storage from C++</span></span>](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="381b2-227">Utilisation du stockage de tables à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="381b2-227">How to use Table storage from PHP</span></span>](../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="381b2-228">Utilisation du stockage Table dans Python</span><span class="sxs-lookup"><span data-stu-id="381b2-228">How to use Table storage in Python</span></span>](../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="381b2-229">Utilisation du stockage de tables à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="381b2-229">How to use Table storage from Ruby</span></span>](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="381b2-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="381b2-230">Next steps</span></span>

* [<span data-ttu-id="381b2-231">Introduction à Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="381b2-231">Introduction to Microsoft Azure Storage</span></span>](../storage/common/storage-introduction.md)