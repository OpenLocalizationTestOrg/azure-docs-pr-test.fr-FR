---
title: "aaaGet démarrer avec les outils de développement de pile le stockage Azure"
description: "Tooget Guide main à l’aide des outils de développement Azure Storage de pile"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 7/21/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 0756ed1b9fad4aed0cca4cfd719ef3334dec6700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="d0d25-103">Bien démarrer avec les outils de développement du stockage Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d0d25-103">Get started with Azure Stack Storage development tools</span></span> 

<span data-ttu-id="d0d25-104">Microsoft Azure Stack fournit un ensemble de services de stockage, notamment le stockage Blob, Table et File d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d25-104">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="d0d25-105">Cet article fournit des conseils rapides sur la façon de toostart à l’aide des outils de développement de pile le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d25-105">This article provides quick guidance on how toostart using Azure Stack Storage development tools.</span></span> <span data-ttu-id="d0d25-106">Vous trouverez des exemples de code et des informations plus détaillées dans les didacticiels de stockage Azure hello correspondants.</span><span class="sxs-lookup"><span data-stu-id="d0d25-106">You can find more detailed information and sample code in hello corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="d0d25-107">Le stockage Azure et le stockage Azure Stack présentent quelques différences connues, y compris certaines exigences spécifiques pour chaque plateforme.</span><span class="sxs-lookup"><span data-stu-id="d0d25-107">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="d0d25-108">Par exemple, Azure Stack a des bibliothèques clientes spécifiques, de même que des exigences spécifiques en matière de suffixe de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d0d25-108">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="d0d25-109">Pour plus d’informations, consultez [Stockage Azure Stack : Différences et considérations](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="d0d25-109">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="d0d25-110">Bibliothèques clientes Azure</span><span class="sxs-lookup"><span data-stu-id="d0d25-110">Azure client libraries</span></span>
<span data-ttu-id="d0d25-111">version d’API REST Hello pris en charge pour le stockage Azure pile est 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="d0d25-111">hello supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="d0d25-112">Il n’a pas une parité complète avec la version la plus récente hello Hello API REST de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d25-112">It doesn’t have full parity with hello latest version of hello Azure Storage REST API.</span></span> <span data-ttu-id="d0d25-113">Pour les bibliothèques clientes de stockage hello, vous devez donc toobe prenant en charge de la version de hello est compatible avec REST API 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="d0d25-113">So for hello storage client libraries, you need toobe aware of hello version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="d0d25-114">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="d0d25-114">Client library</span></span>|<span data-ttu-id="d0d25-115">Version prise en charge par Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d0d25-115">Azure Stack supported version</span></span>|<span data-ttu-id="d0d25-116">Lien</span><span class="sxs-lookup"><span data-stu-id="d0d25-116">Link</span></span>|<span data-ttu-id="d0d25-117">Spécification du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="d0d25-117">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="d0d25-118">.NET</span><span class="sxs-lookup"><span data-stu-id="d0d25-118">.NET</span></span>     |<span data-ttu-id="d0d25-119">6.2.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-119">6.2.0</span></span>|<span data-ttu-id="d0d25-120">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="d0d25-120">Nuget package:</span></span><br>[<span data-ttu-id="d0d25-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="d0d25-122">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0d25-122">GitHub release:</span></span><br>[<span data-ttu-id="d0d25-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="d0d25-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="d0d25-124">Fichier app.config</span><span class="sxs-lookup"><span data-stu-id="d0d25-124">app.config file</span></span>|
|<span data-ttu-id="d0d25-125">Java</span><span class="sxs-lookup"><span data-stu-id="d0d25-125">Java</span></span>|<span data-ttu-id="d0d25-126">4.1.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-126">4.1.0</span></span>|<span data-ttu-id="d0d25-127">Package Maven :</span><span class="sxs-lookup"><span data-stu-id="d0d25-127">Maven package:</span></span><br>[<span data-ttu-id="d0d25-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="d0d25-129">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0d25-129">GitHub release:</span></span><br> [<span data-ttu-id="d0d25-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="d0d25-131">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="d0d25-131">Connection string setup</span></span>|
|<span data-ttu-id="d0d25-132">Node.js</span><span class="sxs-lookup"><span data-stu-id="d0d25-132">Node.js</span></span>     |<span data-ttu-id="d0d25-133">1.1.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-133">1.1.0</span></span>|<span data-ttu-id="d0d25-134">Lien NPM :</span><span class="sxs-lookup"><span data-stu-id="d0d25-134">NPM link:</span></span><br>[<span data-ttu-id="d0d25-135">https://www.npmjs.com/package/azure-storage</span><span class="sxs-lookup"><span data-stu-id="d0d25-135">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="d0d25-136">(exécuter : `npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="d0d25-136">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="d0d25-137">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0d25-137">Github release:</span></span><br>[<span data-ttu-id="d0d25-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="d0d25-139">Déclaration d’instance de service</span><span class="sxs-lookup"><span data-stu-id="d0d25-139">Service instance declaration</span></span>||<span data-ttu-id="d0d25-140">C++</span><span class="sxs-lookup"><span data-stu-id="d0d25-140">C++</span></span>|<span data-ttu-id="d0d25-141">2.4.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-141">2.4.0</span></span>|<span data-ttu-id="d0d25-142">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="d0d25-142">Nuget package:</span></span><br>[<span data-ttu-id="d0d25-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="d0d25-144">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0d25-144">GitHub release:</span></span><br>[<span data-ttu-id="d0d25-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="d0d25-146">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="d0d25-146">Connection string setup</span></span>|
|<span data-ttu-id="d0d25-147">C++</span><span class="sxs-lookup"><span data-stu-id="d0d25-147">C++</span></span>|<span data-ttu-id="d0d25-148">2.4.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-148">2.4.0</span></span>|<span data-ttu-id="d0d25-149">Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="d0d25-149">Nuget package:</span></span><br>[<span data-ttu-id="d0d25-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="d0d25-151">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0d25-151">GitHub release:</span></span><br>[<span data-ttu-id="d0d25-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="d0d25-153">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="d0d25-153">Connection string setup</span></span>|
|<span data-ttu-id="d0d25-154">PHP</span><span class="sxs-lookup"><span data-stu-id="d0d25-154">PHP</span></span>|<span data-ttu-id="d0d25-155">0.15.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-155">0.15.0</span></span>|<span data-ttu-id="d0d25-156">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0d25-156">GitHub release:</span></span><br>[<span data-ttu-id="d0d25-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="d0d25-158">Installation via Composer (voir détails ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="d0d25-158">Install via Composer (see details below)</span></span>|<span data-ttu-id="d0d25-159">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="d0d25-159">Connection string setup</span></span>|
|<span data-ttu-id="d0d25-160">Python</span><span class="sxs-lookup"><span data-stu-id="d0d25-160">Python</span></span>     |<span data-ttu-id="d0d25-161">0.30.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-161">0.30.0</span></span>|<span data-ttu-id="d0d25-162">Package PIP :</span><span class="sxs-lookup"><span data-stu-id="d0d25-162">PIP package:</span></span><br> [<span data-ttu-id="d0d25-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="d0d25-164">(Exécuter : `pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="d0d25-164">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="d0d25-165">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0d25-165">GitHub release:</span></span><br> [<span data-ttu-id="d0d25-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span><span class="sxs-lookup"><span data-stu-id="d0d25-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="d0d25-167">Déclaration d’instance de service</span><span class="sxs-lookup"><span data-stu-id="d0d25-167">Service instance declaration</span></span>|
|<span data-ttu-id="d0d25-168">Ruby</span><span class="sxs-lookup"><span data-stu-id="d0d25-168">Ruby</span></span>|<span data-ttu-id="d0d25-169">0.12.1</span><span class="sxs-lookup"><span data-stu-id="d0d25-169">0.12.1</span></span><br><span data-ttu-id="d0d25-170">VERSION PRÉLIMINAIRE</span><span class="sxs-lookup"><span data-stu-id="d0d25-170">Preview</span></span>|<span data-ttu-id="d0d25-171">Package RubyGems :</span><span class="sxs-lookup"><span data-stu-id="d0d25-171">RubyGems package:</span></span><br> [<span data-ttu-id="d0d25-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span><span class="sxs-lookup"><span data-stu-id="d0d25-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="d0d25-173">Version de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0d25-173">GitHub release:</span></span><br> [<span data-ttu-id="d0d25-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span><span class="sxs-lookup"><span data-stu-id="d0d25-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="d0d25-175">Configuration de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="d0d25-175">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="d0d25-176">Détails PHP</span><span class="sxs-lookup"><span data-stu-id="d0d25-176">PHP details</span></span><br><br>
><span data-ttu-id="d0d25-177">tooinstall via l’éditeur :</span><span class="sxs-lookup"><span data-stu-id="d0d25-177">tooinstall via Composer:</span></span>
>1. <span data-ttu-id="d0d25-178">Créez un fichier nommé `composer.json` dans racine hello du projet hello avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="d0d25-178">Create a file named `composer.json` in hello root of hello project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="d0d25-179">Télécharger [composer.phar](http://getcomposer.org/composer.phar) dans la racine du projet hello.</span><span class="sxs-lookup"><span data-stu-id="d0d25-179">Download [composer.phar](http://getcomposer.org/composer.phar) into hello project root.</span></span>
>3. <span data-ttu-id="d0d25-180">Exécutez : `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="d0d25-180">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="d0d25-181">Déclaration de point de terminaison</span><span class="sxs-lookup"><span data-stu-id="d0d25-181">Endpoint declaration</span></span>
<span data-ttu-id="d0d25-182">Un point de terminaison Azure pile comprend deux parties : nom hello d’un domaine Azure pile région et hello.</span><span class="sxs-lookup"><span data-stu-id="d0d25-182">An Azure Stack endpoint includes two parts: hello name of a region and hello Azure Stack domain.</span></span>
<span data-ttu-id="d0d25-183">Dans le Kit de développement Azure pile de hello, point de terminaison par défaut hello est **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="d0d25-183">In hello Azure Stack Development Kit, hello default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="d0d25-184">Contactez votre administrateur cloud si vous n’êtes pas sûr de votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d0d25-184">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="d0d25-185">Exemples</span><span class="sxs-lookup"><span data-stu-id="d0d25-185">Examples</span></span>


### <a name="net"></a><span data-ttu-id="d0d25-186">.NET</span><span class="sxs-lookup"><span data-stu-id="d0d25-186">.NET</span></span>

<span data-ttu-id="d0d25-187">Pour la pile de Azure, suffixe de point de terminaison hello est spécifié dans le fichier app.config hello :</span><span class="sxs-lookup"><span data-stu-id="d0d25-187">For Azure Stack, hello endpoint suffix is specified in hello app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="d0d25-188">Java</span><span class="sxs-lookup"><span data-stu-id="d0d25-188">Java</span></span>

<span data-ttu-id="d0d25-189">Pour la pile de Azure, suffixe de point de terminaison hello est spécifié dans le programme d’installation de hello de chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="d0d25-189">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="d0d25-190">Node.js</span><span class="sxs-lookup"><span data-stu-id="d0d25-190">Node.js</span></span>

<span data-ttu-id="d0d25-191">Pour la pile de Azure, suffixe de point de terminaison hello est spécifié dans l’instance de déclaration hello :</span><span class="sxs-lookup"><span data-stu-id="d0d25-191">For Azure Stack, hello endpoint suffix is specified in hello declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="d0d25-192">C++</span><span class="sxs-lookup"><span data-stu-id="d0d25-192">C++</span></span>

<span data-ttu-id="d0d25-193">Pour la pile de Azure, suffixe de point de terminaison hello est spécifié dans le programme d’installation de hello de chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="d0d25-193">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="d0d25-194">PHP</span><span class="sxs-lookup"><span data-stu-id="d0d25-194">PHP</span></span>

<span data-ttu-id="d0d25-195">Pour la pile de Azure, suffixe de point de terminaison hello est spécifié dans le programme d’installation de hello de chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="d0d25-195">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="d0d25-196">Python</span><span class="sxs-lookup"><span data-stu-id="d0d25-196">Python</span></span>

<span data-ttu-id="d0d25-197">Pour la pile de Azure, suffixe de point de terminaison hello est spécifié dans l’instance de déclaration hello :</span><span class="sxs-lookup"><span data-stu-id="d0d25-197">For Azure Stack, hello endpoint suffix is specified in hello declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="d0d25-198">Ruby</span><span class="sxs-lookup"><span data-stu-id="d0d25-198">Ruby</span></span>

<span data-ttu-id="d0d25-199">Pour la pile de Azure, suffixe de point de terminaison hello est spécifié dans le programme d’installation de hello de chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="d0d25-199">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="d0d25-200">Stockage d'objets blob</span><span class="sxs-lookup"><span data-stu-id="d0d25-200">Blob storage</span></span>

<span data-ttu-id="d0d25-201">Hello didacticiels du stockage Blob Azure suivants sont applicable tooAzure pile.</span><span class="sxs-lookup"><span data-stu-id="d0d25-201">hello following Azure Blob storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="d0d25-202">Spécification de suffixe Remarque hello point de terminaison spécifique pour la pile Azure décrit dans hello précédente [exemples](#examples) section.</span><span class="sxs-lookup"><span data-stu-id="d0d25-202">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="d0d25-203">Prise en main d’Azure Blob Storage à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="d0d25-203">Get started with Azure Blob storage using .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="d0d25-204">Comment toouse stockage d’objets Blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="d0d25-204">How toouse Blob storage from Java</span></span>](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="d0d25-205">Comment toouse stockage d’objets Blob à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="d0d25-205">How toouse Blob storage from Node.js</span></span>](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="d0d25-206">Comment toouse stockage d’objets Blob à partir de C++</span><span class="sxs-lookup"><span data-stu-id="d0d25-206">How toouse Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="d0d25-207">Comment toouse stockage d’objets Blob à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="d0d25-207">How toouse Blob storage from PHP</span></span>](../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="d0d25-208">Comment toouse le stockage Blob Azure à partir de Python</span><span class="sxs-lookup"><span data-stu-id="d0d25-208">How toouse Azure Blob storage from Python</span></span>](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="d0d25-209">Comment toouse stockage d’objets Blob à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="d0d25-209">How toouse Blob storage from Ruby</span></span>](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="d0d25-210">Stockage de files d'attente</span><span class="sxs-lookup"><span data-stu-id="d0d25-210">Queue storage</span></span>

<span data-ttu-id="d0d25-211">Hello didacticiels de stockage de file d’attente Azure suivants sont applicable tooAzure pile.</span><span class="sxs-lookup"><span data-stu-id="d0d25-211">hello following Azure Queue storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="d0d25-212">Spécification de suffixe Remarque hello point de terminaison spécifique pour la pile Azure décrit dans hello précédente [exemples](#examples) section.</span><span class="sxs-lookup"><span data-stu-id="d0d25-212">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="d0d25-213">Prise en main du stockage de files d’attente Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="d0d25-213">Get started with Azure Queue storage using .NET</span></span>](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="d0d25-214">Comment toouse stockage de file d’attente à partir de Java</span><span class="sxs-lookup"><span data-stu-id="d0d25-214">How toouse Queue storage from Java</span></span>](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="d0d25-215">Comment toouse stockage de file d’attente à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="d0d25-215">How toouse Queue storage from Node.js</span></span>](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="d0d25-216">Comment toouse stockage de file d’attente à partir de C++</span><span class="sxs-lookup"><span data-stu-id="d0d25-216">How toouse Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="d0d25-217">Comment toouse stockage de file d’attente à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="d0d25-217">How toouse Queue storage from PHP</span></span>](../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="d0d25-218">Comment toouse stockage de file d’attente à partir de Python</span><span class="sxs-lookup"><span data-stu-id="d0d25-218">How toouse Queue storage from Python</span></span>](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="d0d25-219">Comment toouse stockage de file d’attente à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="d0d25-219">How toouse Queue storage from Ruby</span></span>](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="d0d25-220">Stockage de tables</span><span class="sxs-lookup"><span data-stu-id="d0d25-220">Table storage</span></span>

<span data-ttu-id="d0d25-221">Hello didacticiels de stockage de Table Azure suivants sont applicable tooAzure pile.</span><span class="sxs-lookup"><span data-stu-id="d0d25-221">hello following Azure Table storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="d0d25-222">Spécification de suffixe Remarque hello point de terminaison spécifique pour la pile Azure décrit dans hello précédente [exemples](#examples) section.</span><span class="sxs-lookup"><span data-stu-id="d0d25-222">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="d0d25-223">Prise en main d’Azure Table Storage à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="d0d25-223">Get started with Azure Table storage using .NET</span></span>](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="d0d25-224">Comment toouse le stockage de Table à partir de Java</span><span class="sxs-lookup"><span data-stu-id="d0d25-224">How toouse Table storage from Java</span></span>](../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="d0d25-225">Comment toouse stockage de Table Azure à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="d0d25-225">How toouse Azure Table storage from Node.js</span></span>](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="d0d25-226">Comment toouse le stockage de Table à partir de C++</span><span class="sxs-lookup"><span data-stu-id="d0d25-226">How toouse Table storage from C++</span></span>](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="d0d25-227">Comment toouse le stockage de Table à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="d0d25-227">How toouse Table storage from PHP</span></span>](../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="d0d25-228">Comment toouse le stockage de Table dans Python</span><span class="sxs-lookup"><span data-stu-id="d0d25-228">How toouse Table storage in Python</span></span>](../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="d0d25-229">Comment toouse le stockage de Table à partir de Ruby</span><span class="sxs-lookup"><span data-stu-id="d0d25-229">How toouse Table storage from Ruby</span></span>](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="d0d25-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0d25-230">Next steps</span></span>

* [<span data-ttu-id="d0d25-231">Introduction tooMicrosoft stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d0d25-231">Introduction tooMicrosoft Azure Storage</span></span>](../storage/common/storage-introduction.md)
