---
title: "Bien démarrer avec les outils de développement du stockage Azure Stack"
description: "Guide de démarrage pour l’utilisation des outils de développement du stockage Azure Stack"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 9/25/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 5b2898c64c0f1b5d804e63fa4e4e1218fa7a672c
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="2e695-103">Bien démarrer avec les outils de développement du stockage Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2e695-103">Get started with Azure Stack Storage development tools</span></span>

<span data-ttu-id="2e695-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="2e695-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>


<span data-ttu-id="2e695-105">Microsoft Azure Stack fournit un ensemble de services de stockage, notamment le stockage Blob, Table et File d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="2e695-105">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="2e695-106">Cet article fournit des conseils rapides sur l’utilisation des outils de développement du stockage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2e695-106">This article provides quick guidance on how to start using Azure Stack Storage development tools.</span></span> <span data-ttu-id="2e695-107">Des informations plus détaillées et des exemples de code sont disponibles dans les didacticiels correspondants du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2e695-107">You can find more detailed information and sample code in the corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="2e695-108">Le stockage Azure et le stockage Azure Stack présentent quelques différences connues, y compris certaines exigences spécifiques pour chaque plateforme.</span><span class="sxs-lookup"><span data-stu-id="2e695-108">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="2e695-109">Par exemple, Azure Stack a des bibliothèques clientes spécifiques, de même que des exigences spécifiques en matière de suffixe de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2e695-109">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="2e695-110">Pour plus d’informations, consultez [Stockage Azure Stack : Différences et considérations](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="2e695-110">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="2e695-111">Bibliothèques clientes Azure</span><span class="sxs-lookup"><span data-stu-id="2e695-111">Azure client libraries</span></span>
<span data-ttu-id="2e695-112">La version d’API REST prise en charge pour le stockage Azure Stack est 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="2e695-112">The supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="2e695-113">Elle n’a pas de parité complète avec la dernière version de l’API REST du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2e695-113">It doesn’t have full parity with the latest version of the Azure Storage REST API.</span></span> <span data-ttu-id="2e695-114">Par conséquent, pour les bibliothèques clientes de stockage, vous devez connaître la version compatible avec l’API REST 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="2e695-114">So for the storage client libraries, you need to be aware of the version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="2e695-115">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="2e695-115">Client library</span></span>|<span data-ttu-id="2e695-116">Version prise en charge par Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2e695-116">Azure Stack supported version</span></span>|<span data-ttu-id="2e695-117">Lien</span><span class="sxs-lookup"><span data-stu-id="2e695-117">Link</span></span>|<span data-ttu-id="2e695-118">Spécification du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="2e695-118">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="2e695-119">.NET</span><span class="sxs-lookup"><span data-stu-id="2e695-119">.NET</span></span>     |<span data-ttu-id="2e695-120">6.2.0</span><span class="sxs-lookup"><span data-stu-id="2e695-120">6.2.0</span></span>|<span data-ttu-id="2e695-121">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="2e695-121">Nuget package:</span></span><br>[<span data-ttu-id="2e695-122">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="2e695-122">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="2e695-123">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="2e695-123">GitHub release:</span></span><br>[<span data-ttu-id="2e695-124">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="2e695-124">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="2e695-125">Fichier app.config</span><span class="sxs-lookup"><span data-stu-id="2e695-125">app.config file</span></span>|
|<span data-ttu-id="2e695-126">Java</span><span class="sxs-lookup"><span data-stu-id="2e695-126">Java</span></span>|<span data-ttu-id="2e695-127">4.1.0</span><span class="sxs-lookup"><span data-stu-id="2e695-127">4.1.0</span></span>|<span data-ttu-id="2e695-128">Package Maven :</span><span class="sxs-lookup"><span data-stu-id="2e695-128">Maven package:</span></span><br>[<span data-ttu-id="2e695-129">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="2e695-129">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="2e695-130">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="2e695-130">GitHub release:</span></span><br> [<span data-ttu-id="2e695-131">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="2e695-131">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="2e695-132">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="2e695-132">Connection string setup</span></span>|
|<span data-ttu-id="2e695-133">Node.js</span><span class="sxs-lookup"><span data-stu-id="2e695-133">Node.js</span></span>     |<span data-ttu-id="2e695-134">1.1.0</span><span class="sxs-lookup"><span data-stu-id="2e695-134">1.1.0</span></span>|<span data-ttu-id="2e695-135">Lien NPM :</span><span class="sxs-lookup"><span data-stu-id="2e695-135">NPM link:</span></span><br>[<span data-ttu-id="2e695-136">https://www.npmjs.com/package/azure-storage</span><span class="sxs-lookup"><span data-stu-id="2e695-136">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="2e695-137">(exécuter : `npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="2e695-137">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="2e695-138">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="2e695-138">Github release:</span></span><br>[<span data-ttu-id="2e695-139">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="2e695-139">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="2e695-140">Déclaration d’instance de service</span><span class="sxs-lookup"><span data-stu-id="2e695-140">Service instance declaration</span></span>||<span data-ttu-id="2e695-141">C++</span><span class="sxs-lookup"><span data-stu-id="2e695-141">C++</span></span>|<span data-ttu-id="2e695-142">2.4.0</span><span class="sxs-lookup"><span data-stu-id="2e695-142">2.4.0</span></span>|<span data-ttu-id="2e695-143">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="2e695-143">Nuget package:</span></span><br>[<span data-ttu-id="2e695-144">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="2e695-144">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="2e695-145">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="2e695-145">GitHub release:</span></span><br>[<span data-ttu-id="2e695-146">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="2e695-146">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="2e695-147">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="2e695-147">Connection string setup</span></span>|
|<span data-ttu-id="2e695-148">C++</span><span class="sxs-lookup"><span data-stu-id="2e695-148">C++</span></span>|<span data-ttu-id="2e695-149">2.4.0</span><span class="sxs-lookup"><span data-stu-id="2e695-149">2.4.0</span></span>|<span data-ttu-id="2e695-150">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="2e695-150">Nuget package:</span></span><br>[<span data-ttu-id="2e695-151">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="2e695-151">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="2e695-152">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="2e695-152">GitHub release:</span></span><br>[<span data-ttu-id="2e695-153">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="2e695-153">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="2e695-154">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="2e695-154">Connection string setup</span></span>|
|<span data-ttu-id="2e695-155">PHP</span><span class="sxs-lookup"><span data-stu-id="2e695-155">PHP</span></span>|<span data-ttu-id="2e695-156">0.15.0</span><span class="sxs-lookup"><span data-stu-id="2e695-156">0.15.0</span></span>|<span data-ttu-id="2e695-157">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="2e695-157">GitHub release:</span></span><br>[<span data-ttu-id="2e695-158">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span><span class="sxs-lookup"><span data-stu-id="2e695-158">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="2e695-159">Installation via Composer (voir détails ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="2e695-159">Install via Composer (see details below)</span></span>|<span data-ttu-id="2e695-160">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="2e695-160">Connection string setup</span></span>|
|<span data-ttu-id="2e695-161">Python</span><span class="sxs-lookup"><span data-stu-id="2e695-161">Python</span></span>     |<span data-ttu-id="2e695-162">0.30.0</span><span class="sxs-lookup"><span data-stu-id="2e695-162">0.30.0</span></span>|<span data-ttu-id="2e695-163">Package PIP :</span><span class="sxs-lookup"><span data-stu-id="2e695-163">PIP package:</span></span><br> [<span data-ttu-id="2e695-164">https://pypi.python.org/pypi/azure-storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="2e695-164">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="2e695-165">(Exécuter : `pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="2e695-165">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="2e695-166">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="2e695-166">GitHub release:</span></span><br> [<span data-ttu-id="2e695-167">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span><span class="sxs-lookup"><span data-stu-id="2e695-167">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="2e695-168">Déclaration d’instance de service</span><span class="sxs-lookup"><span data-stu-id="2e695-168">Service instance declaration</span></span>|
|<span data-ttu-id="2e695-169">Ruby</span><span class="sxs-lookup"><span data-stu-id="2e695-169">Ruby</span></span>|<span data-ttu-id="2e695-170">0.12.1</span><span class="sxs-lookup"><span data-stu-id="2e695-170">0.12.1</span></span><br><span data-ttu-id="2e695-171">VERSION PRÉLIMINAIRE</span><span class="sxs-lookup"><span data-stu-id="2e695-171">Preview</span></span>|<span data-ttu-id="2e695-172">Package RubyGems :</span><span class="sxs-lookup"><span data-stu-id="2e695-172">RubyGems package:</span></span><br> [<span data-ttu-id="2e695-173">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span><span class="sxs-lookup"><span data-stu-id="2e695-173">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="2e695-174">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="2e695-174">GitHub release:</span></span><br> [<span data-ttu-id="2e695-175">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span><span class="sxs-lookup"><span data-stu-id="2e695-175">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="2e695-176">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="2e695-176">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="2e695-177">Détails PHP</span><span class="sxs-lookup"><span data-stu-id="2e695-177">PHP details</span></span><br><br>
><span data-ttu-id="2e695-178">Pour installer via Composer :</span><span class="sxs-lookup"><span data-stu-id="2e695-178">To install via Composer:</span></span>
>1. <span data-ttu-id="2e695-179">Créez un fichier nommé `composer.json` à la racine du projet avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="2e695-179">Create a file named `composer.json` in the root of the project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="2e695-180">Téléchargez [composer.phar](http://getcomposer.org/composer.phar) à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="2e695-180">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span></span>
>3. <span data-ttu-id="2e695-181">Exécutez : `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="2e695-181">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="2e695-182">Déclaration de point de terminaison</span><span class="sxs-lookup"><span data-stu-id="2e695-182">Endpoint declaration</span></span>
<span data-ttu-id="2e695-183">Un point de terminaison Azure Stack comprend deux parties : le nom d’une région et le domaine Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2e695-183">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span>
<span data-ttu-id="2e695-184">Dans le Kit de développement Azure Stack, le point de terminaison par défaut est **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="2e695-184">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="2e695-185">Contactez votre administrateur cloud si vous n’êtes pas sûr de votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2e695-185">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="2e695-186">Exemples</span><span class="sxs-lookup"><span data-stu-id="2e695-186">Examples</span></span>


### <a name="net"></a><span data-ttu-id="2e695-187">.NET</span><span class="sxs-lookup"><span data-stu-id="2e695-187">.NET</span></span>

<span data-ttu-id="2e695-188">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans le fichier app.config :</span><span class="sxs-lookup"><span data-stu-id="2e695-188">For Azure Stack, the endpoint suffix is specified in the app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="2e695-189">Java</span><span class="sxs-lookup"><span data-stu-id="2e695-189">Java</span></span>

<span data-ttu-id="2e695-190">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans la configuration de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="2e695-190">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="2e695-191">Node.js</span><span class="sxs-lookup"><span data-stu-id="2e695-191">Node.js</span></span>

<span data-ttu-id="2e695-192">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans l’instance de déclaration :</span><span class="sxs-lookup"><span data-stu-id="2e695-192">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="2e695-193">C++</span><span class="sxs-lookup"><span data-stu-id="2e695-193">C++</span></span>

<span data-ttu-id="2e695-194">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans la configuration de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="2e695-194">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="2e695-195">PHP</span><span class="sxs-lookup"><span data-stu-id="2e695-195">PHP</span></span>

<span data-ttu-id="2e695-196">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans la configuration de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="2e695-196">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="2e695-197">Python</span><span class="sxs-lookup"><span data-stu-id="2e695-197">Python</span></span>

<span data-ttu-id="2e695-198">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans l’instance de déclaration :</span><span class="sxs-lookup"><span data-stu-id="2e695-198">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="2e695-199">Ruby</span><span class="sxs-lookup"><span data-stu-id="2e695-199">Ruby</span></span>

<span data-ttu-id="2e695-200">Pour Azure Stack, le suffixe de point de terminaison est spécifié dans la configuration de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="2e695-200">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="2e695-201">Stockage d'objets blob</span><span class="sxs-lookup"><span data-stu-id="2e695-201">Blob storage</span></span>

<span data-ttu-id="2e695-202">Les didacticiels du stockage Blob Azure suivants sont applicables à Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2e695-202">The following Azure Blob storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="2e695-203">Notez l’exigence particulière d’un suffixe de point de terminaison pour Azure Stack, décrit dans la précédente section [Exemples](#examples).</span><span class="sxs-lookup"><span data-stu-id="2e695-203">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="2e695-204">Prise en main d’Azure Blob Storage à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="2e695-204">Get started with Azure Blob storage using .NET</span></span>](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="2e695-205">Utilisation du stockage d'objets blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="2e695-205">How to use Blob storage from Java</span></span>](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* <span data-ttu-id="2e695-206">[Utilisation du stockage d’objets Blob à partir de Node.js]../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="2e695-206">[How to use Blob storage from Node.js]../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)</span></span>
* [<span data-ttu-id="2e695-207">Utilisation du stockage d’objets blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="2e695-207">How to use Blob storage from C++</span></span>](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="2e695-208">Utilisation du stockage d'objets blob à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="2e695-208">How to use Blob storage from PHP</span></span>](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="2e695-209">Utilisation du stockage Blob Azure à partir de Python</span><span class="sxs-lookup"><span data-stu-id="2e695-209">How to use Azure Blob storage from Python</span></span>](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="2e695-210">Utilisation du stockage d'objets blob à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="2e695-210">How to use Blob storage from Ruby</span></span>](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="2e695-211">Stockage de files d'attente</span><span class="sxs-lookup"><span data-stu-id="2e695-211">Queue storage</span></span>

<span data-ttu-id="2e695-212">Les didacticiels du stockage File d’attente Azure suivants sont applicables à Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2e695-212">The following Azure Queue storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="2e695-213">Notez l’exigence particulière d’un suffixe de point de terminaison pour Azure Stack, décrit dans la précédente section [Exemples](#examples).</span><span class="sxs-lookup"><span data-stu-id="2e695-213">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="2e695-214">Prise en main du stockage de files d’attente Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="2e695-214">Get started with Azure Queue storage using .NET</span></span>](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="2e695-215">Utilisation du stockage de files d'attente à partir de Java</span><span class="sxs-lookup"><span data-stu-id="2e695-215">How to use Queue storage from Java</span></span>](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="2e695-216">Utilisation du stockage de files d'attente à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="2e695-216">How to use Queue storage from Node.js</span></span>](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="2e695-217">Utilisation du service de stockage de files d’attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="2e695-217">How to use Queue storage from C++</span></span>](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="2e695-218">Utilisation du stockage de files d'attente à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="2e695-218">How to use Queue storage from PHP</span></span>](../../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="2e695-219">Utilisation du stockage de files d'attente à partir de Python</span><span class="sxs-lookup"><span data-stu-id="2e695-219">How to use Queue storage from Python</span></span>](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="2e695-220">Utilisation du stockage de files d'attente à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="2e695-220">How to use Queue storage from Ruby</span></span>](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="2e695-221">Stockage de tables</span><span class="sxs-lookup"><span data-stu-id="2e695-221">Table storage</span></span>

<span data-ttu-id="2e695-222">Les didacticiels du stockage Table Azure suivants sont applicables à Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2e695-222">The following Azure Table storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="2e695-223">Notez l’exigence particulière d’un suffixe de point de terminaison pour Azure Stack, décrit dans la précédente section [Exemples](#examples).</span><span class="sxs-lookup"><span data-stu-id="2e695-223">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="2e695-224">Prise en main d’Azure Table Storage à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="2e695-224">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="2e695-225">Utilisation du stockage de tables à partir de Java</span><span class="sxs-lookup"><span data-stu-id="2e695-225">How to use Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="2e695-226">Utilisation du stockage Table Azure à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="2e695-226">How to use Azure Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="2e695-227">Utilisation du stockage Table à partir de C++</span><span class="sxs-lookup"><span data-stu-id="2e695-227">How to use Table storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="2e695-228">Utilisation du stockage de tables à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="2e695-228">How to use Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="2e695-229">Utilisation du stockage Table dans Python</span><span class="sxs-lookup"><span data-stu-id="2e695-229">How to use Table storage in Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="2e695-230">Utilisation du stockage de tables à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="2e695-230">How to use Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="2e695-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e695-231">Next steps</span></span>

* [<span data-ttu-id="2e695-232">Introduction à Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2e695-232">Introduction to Microsoft Azure Storage</span></span>](../../storage/common/storage-introduction.md)