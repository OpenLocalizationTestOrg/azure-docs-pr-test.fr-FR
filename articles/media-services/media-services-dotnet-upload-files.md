---
title: "Charger des fichiers dans un compte Media Services à l’aide de .NET | Microsoft Docs"
description: "Apprenez à obtenir du contenu multimédia dans Media Services en créant et en chargeant des ressources."
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
ms.openlocfilehash: ec8c1da633374ba684f6a0a895c542ee76ef73b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="61e66-103">Charger des fichiers dans un compte Media Services à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="61e66-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61e66-104">.NET</span><span class="sxs-lookup"><span data-stu-id="61e66-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="61e66-105">REST</span><span class="sxs-lookup"><span data-stu-id="61e66-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="61e66-106">Portail</span><span class="sxs-lookup"><span data-stu-id="61e66-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="61e66-107">Dans Media Services, vous téléchargez (ou réceptionnez) vos fichiers numériques dans un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="61e66-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="61e66-108">L’entité **Asset** peut contenir des fichiers vidéo et audio, des images, des collections de miniatures, des pistes textuelles et des légendes (et les métadonnées concernant ces fichiers).  Une fois les fichiers téléchargés, votre contenu est stocké en toute sécurité dans le cloud et peut faire l’objet d’un traitement et d’un streaming.</span><span class="sxs-lookup"><span data-stu-id="61e66-108">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="61e66-109">Les fichiers de l'élément multimédia sont appelés **fichiers d'élément multimédia**.</span><span class="sxs-lookup"><span data-stu-id="61e66-109">The files in the asset are called **Asset Files**.</span></span> <span data-ttu-id="61e66-110">L'instance **AssetFile** et le fichier multimédia réel sont deux objets distincts.</span><span class="sxs-lookup"><span data-stu-id="61e66-110">The **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="61e66-111">L’instance AssetFile contient des métadonnées concernant le fichier multimédia, tandis que le fichier multimédia contient le contenu multimédia réel.</span><span class="sxs-lookup"><span data-stu-id="61e66-111">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="61e66-112">Les considérations suivantes s'appliquent :</span><span class="sxs-lookup"><span data-stu-id="61e66-112">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="61e66-113">Media Services utilise la valeur de la propriété IAssetFile.Name lors de la génération d’URL pour le contenu de streaming (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters). Pour cette raison, l’encodage par pourcentage n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="61e66-113">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="61e66-114">La valeur de la propriété **Name** ne peut pas comporter les [caractères réservés à l’encodage en pourcentage suivants](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters) : !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="61e66-114">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="61e66-115">En outre, il ne peut exister qu’un ’.’ pour l’extension de nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="61e66-115">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="61e66-116">La longueur du nom ne doit pas dépasser 260 caractères.</span><span class="sxs-lookup"><span data-stu-id="61e66-116">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="61e66-117">Une limite est appliquée à la taille maximale de fichier prise en charge pour le traitement dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="61e66-117">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="61e66-118">Consultez [cette rubrique](media-services-quotas-and-limitations.md) pour en savoir plus sur les limites de taille des fichiers.</span><span class="sxs-lookup"><span data-stu-id="61e66-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> * <span data-ttu-id="61e66-119">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="61e66-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="61e66-120">Vous devez utiliser le même ID de stratégie si vous utilisez toujours les mêmes jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs destinées à demeurer en place pendant une longue période (stratégies sans chargement).</span><span class="sxs-lookup"><span data-stu-id="61e66-120">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="61e66-121">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="61e66-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="61e66-122">Lorsque vous créez des éléments multimédias, vous pouvez spécifier les options de chiffrement suivantes :</span><span class="sxs-lookup"><span data-stu-id="61e66-122">When you create assets, you can specify the following encryption options.</span></span> 

* <span data-ttu-id="61e66-123">**None** : aucun chiffrement.</span><span class="sxs-lookup"><span data-stu-id="61e66-123">**None** - No encryption is used.</span></span> <span data-ttu-id="61e66-124">Il s’agit de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="61e66-124">This is the default value.</span></span> <span data-ttu-id="61e66-125">À noter que quand vous utilisez cette option, votre contenu n’est pas protégé pendant le transit ou le repos dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="61e66-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="61e66-126">Si vous prévoyez de fournir un MP4 sous forme de téléchargement progressif, utilisez cette option.</span><span class="sxs-lookup"><span data-stu-id="61e66-126">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="61e66-127">**CommonEncryption** : utilisez cette option quand vous téléchargez du contenu qui a déjà été chiffré et protégé par Common Encryption ou PlayReady DRM (par exemple, Smooth Streaming protégé par PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="61e66-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="61e66-128">**EnvelopeEncrypted** : utilisez cette option quand vous téléchargez du contenu au format HLS chiffré avec AES.</span><span class="sxs-lookup"><span data-stu-id="61e66-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="61e66-129">Notez que les fichiers doivent avoir été encodés et chiffrés par le gestionnaire de transformation Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="61e66-129">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="61e66-130">**StorageEncrypted** : permet de chiffrer votre contenu en clair localement en utilisant le chiffrement AES-256 bits, puis de le télécharger vers Azure Storage où il est chiffré pour le stockage, au repos.</span><span class="sxs-lookup"><span data-stu-id="61e66-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="61e66-131">Les éléments multimédias protégés par le chiffrement de stockage sont automatiquement déchiffrés et placés dans un système de fichiers chiffré avant d’être encodés, puis éventuellement rechiffrés avant d’être rechargés sous la forme d’un nouvel élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="61e66-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="61e66-132">Le principal cas d’utilisation du chiffrement de stockage concerne la sécurisation de fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au repos sur le disque.</span><span class="sxs-lookup"><span data-stu-id="61e66-132">The primary use case for Storage Encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="61e66-133">Media Services fournit pour vos éléments multimédias un chiffrement de stockage sur disque, et non pas sur le réseau comme pour la gestion des droits numériques (DRM).</span><span class="sxs-lookup"><span data-stu-id="61e66-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="61e66-134">Si votre ressource est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="61e66-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="61e66-135">Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="61e66-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="61e66-136">Si votre élément multimédia est chiffré avec l'option **CommonEncrypted** ou **EnvelopeEncypted**, vous devez l'associer à une **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="61e66-136">If you specify for your asset to be encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need to associate your asset with a **ContentKey**.</span></span> <span data-ttu-id="61e66-137">Pour plus d'informations, consultez [Comment créer une ContentKey](media-services-dotnet-create-contentkey.md)</span><span class="sxs-lookup"><span data-stu-id="61e66-137">For more information, see [How to create a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="61e66-138">Si votre élément multimédia est chiffré avec l'option **StorageEncrypted**, le Kit de développement logiciel (SDK) Media Services pour .NET crée une **ContentKey** **StorateEncrypted** pour votre élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="61e66-138">If you specify for your asset to be encrypted with a **StorageEncrypted** option, the Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="61e66-139">Cette rubrique montre comment utiliser le Kit de développement logiciel (SDK) Media Services pour .NET, ainsi que les extensions du SDK Media Services pour .NET, pour charger des fichiers vers un élément multimédia Media Services.</span><span class="sxs-lookup"><span data-stu-id="61e66-139">This topic shows how to use Media Services .NET SDK as well as Media Services .NET SDK extensions to upload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="61e66-140">Téléchargement d’un fichier unique avec le Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="61e66-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="61e66-141">L’exemple de code ci-dessous utilise le Kit de développement logiciel (SDK) .NET pour charger un fichier unique.</span><span class="sxs-lookup"><span data-stu-id="61e66-141">The sample code below uses .NET SDK to upload a single file.</span></span> <span data-ttu-id="61e66-142">AccessPolicy et Locator sont créés et détruits par la fonction de chargement.</span><span class="sxs-lookup"><span data-stu-id="61e66-142">The AccessPolicy and Locator are created and destroyed by the Upload function.</span></span> 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="61e66-143">Téléchargement de plusieurs fichiers avec le Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="61e66-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="61e66-144">Le code qui suit présente la création d’un élément multimédia et le chargement de plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="61e66-144">The following code shows how to create an asset and upload multiple files.</span></span>

<span data-ttu-id="61e66-145">Le code effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="61e66-145">The code does the following:</span></span>

* <span data-ttu-id="61e66-146">Création d’un élément multimédia vide à l’aide de la méthode CreateEmptyAsset définie dans l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="61e66-146">Creates an empty asset using the CreateEmptyAsset method defined in the previous step.</span></span>
* <span data-ttu-id="61e66-147">Création d'une instance **AccessPolicy** qui définit les autorisations et la durée de l'accès à l'élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="61e66-147">Creates an **AccessPolicy** instance that defines the permissions and duration of access to the asset.</span></span>
* <span data-ttu-id="61e66-148">Création d'une instance **Locator** qui fournit l'accès à l'élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="61e66-148">Creates a **Locator** instance that provides access to the asset.</span></span>
* <span data-ttu-id="61e66-149">Création d'une instance **BlobTransferClient**.</span><span class="sxs-lookup"><span data-stu-id="61e66-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="61e66-150">Ce type représente un client qui opère sur les objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="61e66-150">This type represents a client that operates on the Azure blobs.</span></span> <span data-ttu-id="61e66-151">Dans cet exemple, nous utilisons le client pour surveiller la progression du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="61e66-151">In this example we use the client to monitor the upload progress.</span></span> 
* <span data-ttu-id="61e66-152">Énumère les fichiers dans le répertoire spécifié et crée une instance **AssetFile** pour chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="61e66-152">Enumerates through files in the specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="61e66-153">Télécharge les fichiers dans Media Services à l'aide de la méthode **UploadAsync** .</span><span class="sxs-lookup"><span data-stu-id="61e66-153">Uploads the files into Media Services using the **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="61e66-154">Utilisez la méthode UploadAsync afin de garantir que les appels ne sont pas bloqués et que les fichiers sont téléchargés en parallèle.</span><span class="sxs-lookup"><span data-stu-id="61e66-154">Use the UploadAsync method to ensure that the calls are not blocking and the files are uploaded in parallel.</span></span>
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

                // It is recommended to validate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading the files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as the upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="61e66-155">Lorsque vous téléchargez un grand nombre d'éléments multimédias, prenez en compte les points suivants.</span><span class="sxs-lookup"><span data-stu-id="61e66-155">When uploading a large number of assets, consider the following.</span></span>

* <span data-ttu-id="61e66-156">Créez un objet **CloudMediaContext** par thread.</span><span class="sxs-lookup"><span data-stu-id="61e66-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="61e66-157">La classe **CloudMediaContext** n'est pas thread-safe.</span><span class="sxs-lookup"><span data-stu-id="61e66-157">The **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="61e66-158">Augmentez la valeur par défaut (2) de NumberOfConcurrentTransfers à une valeur supérieure à 5.</span><span class="sxs-lookup"><span data-stu-id="61e66-158">Increase NumberOfConcurrentTransfers from the default value of 2 to a higher value like 5.</span></span> <span data-ttu-id="61e66-159">Cette propriété affecte toutes les instances de **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="61e66-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="61e66-160">Conservez la valeur par défaut de 10 pour ParallelTransferThreadCount.</span><span class="sxs-lookup"><span data-stu-id="61e66-160">Keep ParallelTransferThreadCount at the default value of 10.</span></span>

## <span data-ttu-id="61e66-161"><a id="ingest_in_bulk"></a>Réception d’éléments multimédias en bloc à l’aide du Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="61e66-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="61e66-162">Le téléchargement de fichiers multimédias volumineux peut entraîner un goulot d’étranglement lors de la création de l'élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="61e66-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="61e66-163">La réception des éléments multimédias en bloc ou « réception en bloc » implique de découpler la création des éléments multimédias du processus de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="61e66-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from the upload process.</span></span> <span data-ttu-id="61e66-164">Pour utiliser une approche de réception en bloc, créez un manifeste (IngestManifest) qui décrit l'élément multimédia et ses fichiers associés.</span><span class="sxs-lookup"><span data-stu-id="61e66-164">To use a bulk ingesting approach, create a manifest (IngestManifest) that describes the asset and its associated files.</span></span> <span data-ttu-id="61e66-165">Utilisez ensuite la méthode de téléchargement de votre choix pour télécharger les fichiers associés sur le conteneur d’objets blob du manifeste.</span><span class="sxs-lookup"><span data-stu-id="61e66-165">Then use the upload method of your choice to upload the associated files to the manifest’s blob container.</span></span> <span data-ttu-id="61e66-166">Microsoft Azure Media Services surveille le conteneur d’objets blob associé au manifeste.</span><span class="sxs-lookup"><span data-stu-id="61e66-166">Microsoft Azure Media Services watches the blob container associated with the manifest.</span></span> <span data-ttu-id="61e66-167">Une fois qu’un fichier est téléchargé vers le conteneur d’objets blob, Microsoft Azure Media Services termine la création des éléments multimédias selon la configuration de l'élément multimédia du manifeste (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="61e66-167">Once a file is uploaded to the blob container, Microsoft Azure Media Services completes the asset creation based on the configuration of the asset in the manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="61e66-168">Pour créer un IngestManifest, appelez la méthode Create exposée par la collection IngestManifests sur le CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="61e66-168">To create a new IngestManifest call the Create method exposed by the IngestManifests collection on the CloudMediaContext.</span></span> <span data-ttu-id="61e66-169">Cette méthode crée un IngestManifest avec le nom de manifeste que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="61e66-169">This method will create a new IngestManifest with the manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="61e66-170">Créez les éléments multimédias associés à l’IngestManifest en bloc.</span><span class="sxs-lookup"><span data-stu-id="61e66-170">Create the assets that will be associated with the bulk IngestManifest.</span></span> <span data-ttu-id="61e66-171">Configurez les options de chiffrement souhaitées sur l'élément multimédia pour la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="61e66-171">Configure the desired encryption options on the asset for bulk ingesting.</span></span>

    // Create the assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="61e66-172">Un IngestManifestAsset associe un élément multimédia à un IngestManifest en bloc pour la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="61e66-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="61e66-173">Il associe également les AssetFiles qui constitueront chaque élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="61e66-173">It also associates the AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="61e66-174">Pour créer un IngestManifestAsset, utilisez la méthode Create dans le contexte de serveur.</span><span class="sxs-lookup"><span data-stu-id="61e66-174">To create an IngestManifestAsset, use the Create method on the server context.</span></span>

<span data-ttu-id="61e66-175">L’exemple suivant illustre l’ajout de deux IngestManifestAssets qui associent les deux éléments multimédias précédemment créés au manifeste de réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="61e66-175">The following example demonstrates adding two new IngestManifestAssets that associate the two assets previously created to the bulk ingest manifest.</span></span> <span data-ttu-id="61e66-176">Chaque IngestManifestAsset associe également un ensemble de fichiers qui seront téléchargés pour chaque élément multimédia lors de la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="61e66-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="61e66-177">Vous pouvez utiliser n'importe quelle application cliente rapide capable de télécharger les fichiers d'éléments multimédias sur l'URI du conteneur de stockage blob fourni par la propriété **IIngestManifest.BlobStorageUriForUpload** de l'IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="61e66-177">You can use any high speed client application capable of uploading the asset files to the blob storage container URI provided by the **IIngestManifest.BlobStorageUriForUpload** property of the IngestManifest.</span></span> <span data-ttu-id="61e66-178">[Aspera On Demand pour l'Application Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)est un service de téléchargement à grande vitesse intéressant.</span><span class="sxs-lookup"><span data-stu-id="61e66-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="61e66-179">Vous pouvez également écrire du code pour télécharger les fichiers d'éléments multimédias, comme illustré dans l’exemple de code suivant.</span><span class="sxs-lookup"><span data-stu-id="61e66-179">You can also write code to upload the assets files as shown in the following code example.</span></span>

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

<span data-ttu-id="61e66-180">Le code pour charger les fichiers d’éléments multimédias de l’exemple utilisé dans cette rubrique est illustré dans l’exemple de code suivant.</span><span class="sxs-lookup"><span data-stu-id="61e66-180">The code for uploading the asset files for the sample used in this topic is shown in the following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="61e66-181">Vous pouvez déterminer la progression de la réception en bloc de tous les éléments multimédias associés à un **IngestManifest** en interrogeant la propriété Statistics de **l’IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="61e66-181">You can determine the progress of the bulk ingesting for all assets associated with an **IngestManifest** by polling the Statistics property of the **IngestManifest**.</span></span> <span data-ttu-id="61e66-182">Pour mettre à jour les informations de progression, vous devez utiliser un nouveau **CloudMediaContext** chaque fois que vous interrogez la propriété Statistics.</span><span class="sxs-lookup"><span data-stu-id="61e66-182">In order to update progress information, you must use a new **CloudMediaContext** each time you poll the Statistics property.</span></span>

<span data-ttu-id="61e66-183">L'exemple suivant illustre l'interrogation d'un IngestManifest par son **Id**.</span><span class="sxs-lookup"><span data-stu-id="61e66-183">The following example demonstrates polling an IngestManifest by its **Id**.</span></span>

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



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="61e66-184">Téléchargement de fichiers à l’aide des extensions du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="61e66-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="61e66-185">L’exemple ci-dessous montre comment télécharger un fichier unique à l’aide des extensions du Kit de développement logiciel (SDK) .NET.</span><span class="sxs-lookup"><span data-stu-id="61e66-185">The example below shows how to upload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="61e66-186">Dans ce cas, on utilise la méthode **CreateFromFile**, mais la version asynchrone est également disponible (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="61e66-186">In this case the **CreateFromFile** method is used, but the asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="61e66-187">La méthode **CreateFromFile** vous permet de spécifier le nom de fichier, l'option de chiffrement et un rappel pour signaler la progression du téléchargement du fichier.</span><span class="sxs-lookup"><span data-stu-id="61e66-187">The **CreateFromFile** method lets you specify the file name, encryption option, and a callback in order to report the upload progress of the file.</span></span>

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

<span data-ttu-id="61e66-188">L’exemple suivant appelle la fonction UploadFile et spécifie le chiffrement de stockage en tant qu’option de création d'éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="61e66-188">The following example calls UploadFile function and specifies storage encryption as the asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="61e66-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61e66-189">Next steps</span></span>

<span data-ttu-id="61e66-190">Vous pouvez désormais encoder vos éléments multimédias téléchargés.</span><span class="sxs-lookup"><span data-stu-id="61e66-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="61e66-191">Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="61e66-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="61e66-192">Vous pouvez également utiliser les fonctions Azure pour déclencher une tâche de codage à partir d’un fichier entrant dans le conteneur configuré.</span><span class="sxs-lookup"><span data-stu-id="61e66-192">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="61e66-193">Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="61e66-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="61e66-194">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="61e66-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="61e66-195">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="61e66-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="61e66-196">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="61e66-196">Next step</span></span>
<span data-ttu-id="61e66-197">Après avoir chargé un élément multimédia dans Media Services, consultez la rubrique [Obtention d’un processeur multimédia][How to Get a Media Processor].</span><span class="sxs-lookup"><span data-stu-id="61e66-197">Now that you have uploaded an asset to Media Services, go to the [How to Get a Media Processor][How to Get a Media Processor] topic.</span></span>

[How to Get a Media Processor]: media-services-get-media-processor.md

