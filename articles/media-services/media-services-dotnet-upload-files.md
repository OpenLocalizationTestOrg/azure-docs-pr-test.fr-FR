---
title: "fichiers aaaUpload dans un compte Media Services à l’aide de .NET | Documents Microsoft"
description: "Découvrez comment tooget média du contenu dans Media Services création et téléchargement d’éléments multimédias."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="f9e0a-103">Charger des fichiers dans un compte Media Services à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="f9e0a-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9e0a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f9e0a-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="f9e0a-105">REST</span><span class="sxs-lookup"><span data-stu-id="f9e0a-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="f9e0a-106">Portail</span><span class="sxs-lookup"><span data-stu-id="f9e0a-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="f9e0a-107">Dans Media Services, vous téléchargez (ou réceptionnez) vos fichiers numériques dans un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="f9e0a-108">Hello **Asset** entité peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.)  Une fois que les fichiers hello sont téléchargés, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="f9e0a-109">fichiers Hello dans asset de hello sont appelés **des fichiers**.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="f9e0a-110">Hello **AssetFile** instance et le fichier multimédia lui-même de hello sont deux objets distincts.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="f9e0a-111">instance AssetFile de Hello contient des métadonnées sur le fichier du média hello, tandis que le fichier du média hello contient le contenu du média réel hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="f9e0a-112">Hello suivant considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="f9e0a-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="f9e0a-113">Media Services utilise la valeur hello hello IAssetFile.Name propriété lors de la génération d’URL pour hello de diffusion en continu de contenu (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Pour cette raison, l’encodage par pourcentage n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="f9e0a-114">Hello valeur Hello **nom** propriété ne peut pas avoir un des éléments suivants de hello [% réservés d’encodage de caractères](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ! *' () ; : @& = + $, / ? % # [] ».</span><span class="sxs-lookup"><span data-stu-id="f9e0a-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="f9e0a-115">En outre, il ne peut exister un '.' pour l’extension de nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="f9e0a-116">la longueur du nom de hello Hello ne doit pas dépasser 260 caractères.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="f9e0a-117">Il existe une taille de fichier maximale toohello limite pris en charge pour le traitement dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="f9e0a-118">Consultez [cela](media-services-quotas-and-limitations.md) pour plus d’informations sur la limite de taille de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="f9e0a-119">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f9e0a-120">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f9e0a-121">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="f9e0a-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="f9e0a-122">Lorsque vous créez des ressources, vous pouvez spécifier hello suivant les options de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="f9e0a-123">**None** : aucun chiffrement.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-123">**None** - No encryption is used.</span></span> <span data-ttu-id="f9e0a-124">Il s’agit de valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-124">This is hello default value.</span></span> <span data-ttu-id="f9e0a-125">À noter que quand vous utilisez cette option, votre contenu n’est pas protégé pendant le transit ou le repos dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="f9e0a-126">Si vous envisagez de toodeliver un fichier MP4 à l’aide d’un téléchargement progressif, utilisez cette option.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="f9e0a-127">**CommonEncryption** : utilisez cette option quand vous téléchargez du contenu qui a déjà été chiffré et protégé par chiffrement commun ou gestion des droits numériques (DRM) PlayReady (par exemple, une diffusion en continu lisse, « Smooth Streaming », protégée par gestion des droits numériques (DRM) PlayReady).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="f9e0a-128">**EnvelopeEncrypted** : utilisez cette option quand vous téléchargez du contenu au format HLS chiffré avec AES.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="f9e0a-129">Notez que les fichiers hello doivent avoir été codés et chiffrés par Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="f9e0a-130">**StorageEncrypted** - chiffre votre contenu en clair localement à l’aide du chiffrement AES-256 bits, puis le télécharge tooAzure Storage où il est stocké et chiffré au repos.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="f9e0a-131">Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="f9e0a-132">Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au reste sur le disque.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="f9e0a-133">Media Services fournit pour vos éléments multimédias un chiffrement de stockage sur disque, et non pas sur le réseau comme pour la gestion des droits numériques (DRM).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="f9e0a-134">Si votre ressource est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="f9e0a-135">Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="f9e0a-136">Si vous spécifiez pour toobe de votre élément multimédia chiffré avec un **CommonEncrypted** option, ou un **EnvelopeEncypted** option, vous devez tooassociate votre élément multimédia avec un **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="f9e0a-137">Pour plus d’informations, consultez [comment toocreate une ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="f9e0a-138">Si vous spécifiez pour toobe de votre élément multimédia chiffré avec un **StorageEncrypted** option, hello Media Services SDK pour .NET créera un **StorateEncrypted** **ContentKey** pour votre élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="f9e0a-139">Cette rubrique montre comment toouse Media Services .NET SDK ainsi que les fichiers de tooupload extensions Media Services .NET SDK dans un élément multimédia Media Services.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="f9e0a-140">Téléchargement d’un fichier unique avec le Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="f9e0a-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="f9e0a-141">Hello exemple de code ci-dessous utilise tooupload du Kit de développement .NET un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="f9e0a-142">Hello AccessPolicy et recherche sont créés et détruits par fonction de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="f9e0a-143">Téléchargement de plusieurs fichiers avec le Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="f9e0a-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="f9e0a-144">Hello suivant de code montre comment toocreate un élément multimédia et téléchargement de plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="f9e0a-145">code de Hello hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f9e0a-145">hello code does hello following:</span></span>

* <span data-ttu-id="f9e0a-146">Crée un élément multimédia vide, à l’aide de la méthode de CreateEmptyAsset hello définie à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="f9e0a-147">Crée un **AccessPolicy** instance qui définit les autorisations de hello et la durée de ressource de toohello d’accès.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="f9e0a-148">Crée un **recherche** instance qui fournit les actifs de toohello d’accès.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="f9e0a-149">Création d'une instance **BlobTransferClient**.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="f9e0a-150">Ce type représente un client qui fonctionne sur hello qu'objets BLOB Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="f9e0a-151">Dans cet exemple nous utilisons la progression du téléchargement hello client toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="f9e0a-152">Énumère les fichiers dans le répertoire spécifié de hello et crée un **AssetFile** instance pour chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="f9e0a-153">Téléchargements hello des fichiers dans les Services de support à l’aide de hello **UploadAsync** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="f9e0a-154">Utilisez hello UploadAsync méthode tooensure hello appels ne sont pas bloquées et les fichiers de hello sont téléchargés en parallèle.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="f9e0a-155">Lors du téléchargement d’un grand nombre de ressources, tenez compte hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="f9e0a-156">Créez un objet **CloudMediaContext** par thread.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="f9e0a-157">Hello **CloudMediaContext** classe n’est pas thread-safe.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="f9e0a-158">Augmentez NumberOfConcurrentTransfers de valeur par défaut hello 2 tooa plus élevée, telle que 5.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="f9e0a-159">Cette propriété affecte toutes les instances de **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="f9e0a-160">Conservez ParallelTransferThreadCount valeur hello par défaut 10.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="f9e0a-161"><a id="ingest_in_bulk"></a>Réception d’éléments multimédias en bloc à l’aide du Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="f9e0a-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="f9e0a-162">Le téléchargement de fichiers multimédias volumineux peut entraîner un goulot d’étranglement lors de la création de l'élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="f9e0a-163">Réception d’éléments multimédias en bloc ou « Réception en bloc », implique de découpler la création d’élément multimédia à partir du processus de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="f9e0a-164">toouse une approche de réception en bloc, créez un manifeste (IngestManifest) qui décrit l’élément multimédia de hello et ses fichiers associés.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="f9e0a-165">Utilisez ensuite méthode de téléchargement hello du conteneur d’objets blob de votre choix tooupload hello fichiers associés toohello du manifeste.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="f9e0a-166">Microsoft Azure Media Services surveille le conteneur d’objets blob hello associée hello manifeste.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="f9e0a-167">Une fois qu’un fichier est un conteneur d’objets blob toohello téléchargé, Microsoft Azure Media Services complète de création de ressource de hello en fonction de configuration hello d’actif hello dans le manifeste hello (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="f9e0a-168">toocreate un nouvel IngestManifest appeler la méthode de création de hello exposée par hello collection les IngestManifests sur hello CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="f9e0a-169">Cette méthode crée un nouvel IngestManifest avec le nom de manifeste hello que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="f9e0a-170">Créer des composants de hello qui seront associés au bloc de hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="f9e0a-171">Configurer les options de chiffrement hello souhaité sur asset hello pour la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="f9e0a-172">Un IngestManifestAsset associe un élément multimédia à un IngestManifest en bloc pour la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="f9e0a-173">Il associe également hello AssetFiles qui composent chaque élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="f9e0a-174">toocreate un IngestManifestAsset, utilisez la méthode de création de hello sur le contexte de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="f9e0a-175">Hello exemple suivant montre Ajout deux IngestManifestAssets nouvelles qui associer des éléments de deux hello créé précédemment en bloc de toohello manifeste de réception.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="f9e0a-176">Chaque IngestManifestAsset associe également un ensemble de fichiers qui seront téléchargés pour chaque élément multimédia lors de la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="f9e0a-177">Vous pouvez utiliser n’importe quelle application de client haute vitesse capable de télécharger le conteneur de stockage blob pour les fichiers actifs hello toohello URI fourni par hello **IIngestManifest.BlobStorageUriForUpload** propriété Hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="f9e0a-178">[Aspera On Demand pour l'Application Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)est un service de téléchargement à grande vitesse intéressant.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="f9e0a-179">Vous pouvez également écrire du code les fichiers de ressources hello tooupload comme indiqué dans l’exemple de code suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

<span data-ttu-id="f9e0a-180">code Hello pour le téléchargement des fichiers d’éléments multimédias hello pour exemple hello utilisé dans cette rubrique est illustré hello, exemple de code suivant.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="f9e0a-181">Vous pouvez déterminer la progression hello de réception de hello en bloc pour tous les actifs associés à un **IngestManifest** en interrogeant la propriété de statistiques hello Hello **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="f9e0a-182">Dans les informations de progression tooupdate commande, vous devez utiliser un nouveau **CloudMediaContext** chaque fois que vous interrogez propriété Statistics de hello.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="f9e0a-183">Hello exemple suivant montre comment interroger un IngestManifest par son **Id**.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="f9e0a-184">Téléchargement de fichiers à l’aide des extensions du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="f9e0a-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="f9e0a-185">exemple Hello ci-dessous montre comment tooupload un seul fichier à l’aide des Extensions du Kit de développement logiciel .NET.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="f9e0a-186">Dans ce cas hello **CreateFromFile** méthode est utilisée, mais la version asynchrone de hello est également disponible (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="f9e0a-187">Hello **CreateFromFile** méthode vous permet de spécifier le nom de fichier hello, option de chiffrement et un rappel Bonjour tooreport de commande la progression du fichier de hello du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

<span data-ttu-id="f9e0a-188">Hello exemple suivant appelle la fonction de UploadFile et spécifie le chiffrement de stockage en tant que l’option de création hello actif.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="f9e0a-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9e0a-189">Next steps</span></span>

<span data-ttu-id="f9e0a-190">Vous pouvez désormais encoder vos éléments multimédias téléchargés.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="f9e0a-191">Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="f9e0a-192">Vous pouvez également utiliser les fonctions Azure tootrigger un travail d’encodage basé sur un fichier qui arrivent dans le conteneur de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="f9e0a-193">Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="f9e0a-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f9e0a-194">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="f9e0a-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f9e0a-195">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="f9e0a-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="f9e0a-196">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="f9e0a-196">Next step</span></span>
<span data-ttu-id="f9e0a-197">Maintenant que vous avez téléchargé un élément multimédia tooMedia Services, accédez à toohello [comment tooGet un processeur multimédia] [ How tooGet a Media Processor] rubrique.</span><span class="sxs-lookup"><span data-stu-id="f9e0a-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

