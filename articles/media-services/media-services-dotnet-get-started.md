---
title: Utilisation de Media Services avec .NET | Microsoft Docs
description: "Ce didacticiel vous présente les étapes d’implémentation d’une application de diffusion de contenu à la demande avec Azure Media Services pour .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f0be787ba1ccee067fb1d7e6a6554be32f886089
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="baa39-103">Prendre en main la diffusion de contenus à la demande à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="baa39-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="baa39-104">Ce didacticiel explique comment implémenter un service de base de diffusion de contenu vidéo à la demande (VoD) avec l’application Azure Media Services (AMS) à l’aide du Kit de développement logiciel (SDK) .NET Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="baa39-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baa39-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="baa39-105">Prerequisites</span></span>

<span data-ttu-id="baa39-106">Les éléments suivants sont requis pour suivre le didacticiel :</span><span class="sxs-lookup"><span data-stu-id="baa39-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="baa39-107">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="baa39-107">An Azure account.</span></span> <span data-ttu-id="baa39-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="baa39-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="baa39-109">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="baa39-109">A Media Services account.</span></span> <span data-ttu-id="baa39-110">Pour créer un compte Media Services, consultez [Création d’un compte Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="baa39-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="baa39-111">.NET Framework 4.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="baa39-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="baa39-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="baa39-112">Visual Studio.</span></span>

<span data-ttu-id="baa39-113">Ce didacticiel comprend les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="baa39-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="baa39-114">Démarrer les points de terminaison de streaming (à l’aide du portail Azure).</span><span class="sxs-lookup"><span data-stu-id="baa39-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="baa39-115">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="baa39-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="baa39-116">Se connecter au compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="baa39-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="baa39-117">Télécharger un fichier vidéo.</span><span class="sxs-lookup"><span data-stu-id="baa39-117">Upload a video file.</span></span>
3. <span data-ttu-id="baa39-118">Encoder le fichier source en un ensemble de fichiers MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="baa39-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="baa39-119">Publier l'élément multimédia et obtenir les URL de diffusion et de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="baa39-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="baa39-120">Lire votre contenu.</span><span class="sxs-lookup"><span data-stu-id="baa39-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="baa39-121">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="baa39-121">Overview</span></span>
<span data-ttu-id="baa39-122">Ce didacticiel vous présente les étapes d'implémentation d'une application de diffusion de contenu vidéo à la demande (VoD) avec le Kit de développement logiciel (SDK) Azure Media Services (AMS) pour .NET.</span><span class="sxs-lookup"><span data-stu-id="baa39-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="baa39-123">Il présente le workflow Media Services de base et les objets et tâches de programmation les plus courants requis pour le développement Media Services.</span><span class="sxs-lookup"><span data-stu-id="baa39-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="baa39-124">À la fin de ce didacticiel, vous pourrez lire en continu ou télécharger de façon progressive un exemple de fichier multimédia que vous aurez chargé, encodé et téléchargé.</span><span class="sxs-lookup"><span data-stu-id="baa39-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="baa39-125">Modèle d’AMS</span><span class="sxs-lookup"><span data-stu-id="baa39-125">AMS model</span></span>

<span data-ttu-id="baa39-126">L’image suivante illustre certains des objets couramment utilisés lors du développement d’applications VoD par rapport au modèle OData de Media Services.</span><span class="sxs-lookup"><span data-stu-id="baa39-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="baa39-127">Cliquez sur l’image pour l’afficher en plein écran.</span><span class="sxs-lookup"><span data-stu-id="baa39-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="baa39-128">Vous pouvez afficher l’ensemble du modèle [ici](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="baa39-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="baa39-129">Démarrer les points de terminaison de streaming à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="baa39-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="baa39-130">Lorsque vous utilisez Azure Media Services, la diffusion de vidéos en continu à débit binaire adaptatif constitue l’un des scénarios les plus courants.</span><span class="sxs-lookup"><span data-stu-id="baa39-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="baa39-131">Media Services assure l’empaquetage dynamique, qui vous permet de distribuer juste-à-temps un contenu encodé en MP4 à débit adaptatif dans un format de diffusion en continu pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming), sans qu’il vous soit nécessaire de stocker des versions pré-empaquetées de chacun de ces formats.</span><span class="sxs-lookup"><span data-stu-id="baa39-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="baa39-132">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="baa39-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="baa39-133">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, le point de terminaison de streaming à partir duquel vous souhaitez diffuser du contenu doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="baa39-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="baa39-134">Pour démarrer le point de terminaison de streaming, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="baa39-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="baa39-135">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="baa39-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="baa39-136">Dans la fenêtre Paramètres, cliquez sur Points de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="baa39-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="baa39-137">Cliquez sur le point de terminaison de diffusion en continu par défaut.</span><span class="sxs-lookup"><span data-stu-id="baa39-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="baa39-138">La fenêtre DEFAULT STREAMING ENDPOINT DETAILS (DÉTAILS DU POINT DE TERMINAISON DE STREAMING PAR DÉFAUT) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="baa39-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="baa39-139">Cliquez sur l’icône de démarrage.</span><span class="sxs-lookup"><span data-stu-id="baa39-139">Click the Start icon.</span></span>
5. <span data-ttu-id="baa39-140">Cliquez sur le bouton Enregistrer pour enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="baa39-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="baa39-141">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="baa39-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="baa39-142">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="baa39-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="baa39-143">Créez un dossier (à tout emplacement sur votre disque local) et copiez-y le fichier .mp4 à encoder et à diffuser en continu ou à télécharger.</span><span class="sxs-lookup"><span data-stu-id="baa39-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="baa39-144">Dans cet exemple, le chemin d'accès « C:\VideoFiles » est utilisé.</span><span class="sxs-lookup"><span data-stu-id="baa39-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="baa39-145">Se connecter au compte Media Services</span><span class="sxs-lookup"><span data-stu-id="baa39-145">Connect to the Media Services account</span></span>

<span data-ttu-id="baa39-146">Lorsque vous utilisez Media Services avec .NET, vous devez utiliser la classe **CloudMediaContext** pour la plupart des tâches de programmation Media Services : connexion au compte Media Services, création, mise à jour, accès et suppression des objets suivants : éléments multimédia, fichiers multimédias, travaux, stratégies d'accès, localisateurs, etc.</span><span class="sxs-lookup"><span data-stu-id="baa39-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="baa39-147">Remplacez la classe Program par défaut par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="baa39-147">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="baa39-148">Le code montre comment lire les valeurs de connexion à partir du fichier App.config et comment créer l’objet **CloudMediaContext** pour se connecter à Media Services.</span><span class="sxs-lookup"><span data-stu-id="baa39-148">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="baa39-149">Pour plus d’informations, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="baa39-149">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="baa39-150">Veillez à mettre à jour le nom du fichier et le chemin d’accès où se trouve votre fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="baa39-150">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="baa39-151">La fonction **Main** appelle des méthodes qui seront définies ultérieurement dans cette section.</span><span class="sxs-lookup"><span data-stu-id="baa39-151">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="baa39-152">Vous obtiendrez des erreurs de compilation tant que vous n’aurez pas ajouté des définitions pour toutes les fonctions.</span><span class="sxs-lookup"><span data-stu-id="baa39-152">You will be getting compilation errors until you add definitions for all the functions.</span></span>

    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="baa39-153">Créer un nouvel élément et charger un fichier vidéo</span><span class="sxs-lookup"><span data-stu-id="baa39-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="baa39-154">Dans Media Services, vous téléchargez (ou réceptionnez) vos fichiers numériques dans un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="baa39-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="baa39-155">L’entité **Asset** peut contenir des fichiers vidéo et audio, des images, des collections de miniatures, des pistes textuelles et des légendes (et les métadonnées concernant ces fichiers).  Une fois les fichiers téléchargés, votre contenu est stocké en toute sécurité dans le cloud et peut faire l’objet d’un traitement et d’une diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="baa39-155">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="baa39-156">Les fichiers de l'élément multimédia sont appelés **fichiers d'élément multimédia**.</span><span class="sxs-lookup"><span data-stu-id="baa39-156">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="baa39-157">La méthode **UploadFile** définie ci-dessous appelle **CreateFromFile** (défini dans les extensions du Kit de développement logiciel (SDK) .NET).</span><span class="sxs-lookup"><span data-stu-id="baa39-157">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="baa39-158">**CreateFromFile** crée un nouvel élément multimédia dans lequel le fichier source spécifié est téléchargé.</span><span class="sxs-lookup"><span data-stu-id="baa39-158">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="baa39-159">La méthode **CreateFromFile** prend **AssetCreationOptions**, qui vous permet de spécifier les options de création suivantes :</span><span class="sxs-lookup"><span data-stu-id="baa39-159">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="baa39-160">**None** : aucun chiffrement.</span><span class="sxs-lookup"><span data-stu-id="baa39-160">**None** - No encryption is used.</span></span> <span data-ttu-id="baa39-161">Il s’agit de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="baa39-161">This is the default value.</span></span> <span data-ttu-id="baa39-162">À noter que quand vous utilisez cette option, votre contenu n'est pas protégé pendant le transit ou le repos dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="baa39-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="baa39-163">Si vous prévoyez de fournir un MP4 sous forme de téléchargement progressif, utilisez cette option.</span><span class="sxs-lookup"><span data-stu-id="baa39-163">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="baa39-164">**StorageEncrypted** : utilisez cette option pour chiffrer votre contenu localement à l’aide du chiffrement Advanced Encryption Standard (AES) 256 bits, qui est ensuite chargé sur Azure Storage, où il est stocké au repos sous forme chiffrée.</span><span class="sxs-lookup"><span data-stu-id="baa39-164">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="baa39-165">Les éléments multimédias protégés par le chiffrement de stockage sont automatiquement déchiffrés et placés dans un système de fichiers chiffré avant d’être encodés, puis éventuellement rechiffrés avant d’être rechargés sous la forme d’un nouvel élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="baa39-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="baa39-166">Le principal cas d'utilisation du chiffrement de stockage concerne la sécurisation de fichiers multimédias d'entrée de haute qualité avec un chiffrement renforcé au repos sur le disque.</span><span class="sxs-lookup"><span data-stu-id="baa39-166">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="baa39-167">**CommonEncryptionProtected** : utilisez cette option quand vous chargez du contenu qui a déjà été chiffré et protégé avec la DRM Common Encryption ou PlayReady (par exemple Smooth Streaming protégé avec la DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="baa39-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="baa39-168">**EnvelopeEncryptionProtected** : utilisez cette option lorsque vous téléchargez un contenu au format TLS chiffré avec AES.</span><span class="sxs-lookup"><span data-stu-id="baa39-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="baa39-169">Notez que les fichiers doivent avoir été encodés et chiffrés par le gestionnaire de transformation Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="baa39-169">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="baa39-170">La méthode **CreateFromFile** vous permet également de spécifier un rappel pour indiquer la progression du chargement du fichier.</span><span class="sxs-lookup"><span data-stu-id="baa39-170">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="baa39-171">Dans l’exemple suivant, nous spécifions **None** pour les options de l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="baa39-171">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="baa39-172">Ajoutez la méthode suivante à la classe Program.</span><span class="sxs-lookup"><span data-stu-id="baa39-172">Add the following method to the Program class.</span></span>

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


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="baa39-173">Encoder le fichier source en un ensemble de fichiers MP4 à débit adaptatif</span><span class="sxs-lookup"><span data-stu-id="baa39-173">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="baa39-174">Après avoir reçu des éléments multimédias dans Media Services, vous pouvez encoder un média, modifier le format de ce dernier, lui appliquer un filigrane, etc. avant de le livrer à des clients.</span><span class="sxs-lookup"><span data-stu-id="baa39-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="baa39-175">Afin de garantir des performances et une disponibilité optimales, ces activités sont planifiées et exécutées dans de nombreuses instances de rôle en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="baa39-175">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="baa39-176">Ces activités s’appellent des travaux et chaque Travail se compose de tâches atomiques qui effectuent le travail à proprement parler sur le fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="baa39-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="baa39-177">Comme mentionné précédemment, lorsque vous travaillez avec Azure Media Services, un des scénarios les plus courants est la diffusion de contenu à débit adaptatif à vos clients.</span><span class="sxs-lookup"><span data-stu-id="baa39-177">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="baa39-178">Media Services peut empaqueter de façon dynamique un ensemble de fichiers MP4 à débit adaptatif dans l’un des formats suivants : HTTP Live Streaming (HLS), Smooth Streaming et MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="baa39-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="baa39-179">Pour tirer parti de l’empaquetage dynamique, vous devez encoder ou transcoder votre fichier mezzanine (source) en un ensemble de fichiers MP4 à débit adaptatif ou de fichiers Smooth Streaming à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="baa39-179">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="baa39-180">Le code suivant vous explique comment effectuer envoyer une tâche d'encodage.</span><span class="sxs-lookup"><span data-stu-id="baa39-180">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="baa39-181">Le travail contient une tâche qui spécifie le fichier mezzanine à transcoder en un ensemble de MP4 à débit adaptatif à l’aide de **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="baa39-181">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="baa39-182">Le code envoie la tâche et attend qu'elle soit terminée.</span><span class="sxs-lookup"><span data-stu-id="baa39-182">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="baa39-183">Une fois la tâche terminée, vous pourrez diffuser votre élément multimédia ou télécharger progressivement les fichiers MP4 qui ont été créés après le transcodage.</span><span class="sxs-lookup"><span data-stu-id="baa39-183">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="baa39-184">Ajoutez la méthode suivante à la classe Program.</span><span class="sxs-lookup"><span data-stu-id="baa39-184">Add the following method to the Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="baa39-185">Publier l'élément et obtenir les URL de diffusion et de téléchargement progressif</span><span class="sxs-lookup"><span data-stu-id="baa39-185">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="baa39-186">Pour diffuser en continu ou télécharger un élément multimédia, vous devez tout d'abord le « publier » en créant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="baa39-186">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="baa39-187">Les localisateurs assurent l’accès aux fichiers contenus dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="baa39-187">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="baa39-188">Media Services prend en charge deux types de localisateurs : les localisateurs OnDemandOrigin, utilisés pour diffuser du contenu multimédia (par exemple, MPEG DASH, HLS ou Smooth Streaming) et les localisateurs SAP (signature d’accès partagé), utilisés pour télécharger des fichiers multimédias (pour plus d’informations sur les localisateurs SAP, consultez [ce blog](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)).</span><span class="sxs-lookup"><span data-stu-id="baa39-188">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="baa39-189">Informations sur les formats d’URL</span><span class="sxs-lookup"><span data-stu-id="baa39-189">Some details about URL formats</span></span>

<span data-ttu-id="baa39-190">Une fois que vous avez créé les localisateurs, vous pouvez générer les URL qui seront utilisées pour diffuser en continu ou télécharger vos fichiers.</span><span class="sxs-lookup"><span data-stu-id="baa39-190">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="baa39-191">L’exemple dans ce didacticiel affiche les URL que vous pouvez coller dans les navigateurs appropriés.</span><span class="sxs-lookup"><span data-stu-id="baa39-191">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="baa39-192">Cette section donne simplement quelques rapides exemples de l’aspect des différents formats.</span><span class="sxs-lookup"><span data-stu-id="baa39-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="baa39-193">Les URL de diffusion en continu pour MPEG DASH ont le format suivant :</span><span class="sxs-lookup"><span data-stu-id="baa39-193">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="baa39-194">{nom du point de terminaison de streaming-nom du compte media services}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="baa39-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="baa39-195">Les URL de diffusion en continu pour HLS ont le format suivant :</span><span class="sxs-lookup"><span data-stu-id="baa39-195">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="baa39-196">{nom du point de terminaison de streaming-nom du compte media services}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="baa39-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="baa39-197">Les URL de diffusion en continu pour Smooth Streaming ont le format suivant :</span><span class="sxs-lookup"><span data-stu-id="baa39-197">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="baa39-198">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest</span><span class="sxs-lookup"><span data-stu-id="baa39-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="baa39-199">Les URL SAS permettant de télécharger les fichiers ont le format suivant :</span><span class="sxs-lookup"><span data-stu-id="baa39-199">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="baa39-200">{nom du conteneur d’objets blob}/{nom de la ressource}/{nom du fichier}/{signature SAS}</span><span class="sxs-lookup"><span data-stu-id="baa39-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="baa39-201">Les extensions du Kit de développement logiciel (SDK) Media Services pour .NET fournissent des méthodes d'assistance pratiques qui retournent des URL formatées pour la ressource publiée.</span><span class="sxs-lookup"><span data-stu-id="baa39-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="baa39-202">Le code suivant utilise les extensions du Kit de développement logiciel (SDK) Media Services pour .NET pour créer des localisateurs, obtenir la diffusion en continu et les URL de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="baa39-202">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="baa39-203">Le code montre également comment télécharger les fichiers vers un dossier local.</span><span class="sxs-lookup"><span data-stu-id="baa39-203">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="baa39-204">Ajoutez la méthode suivante à la classe Program.</span><span class="sxs-lookup"><span data-stu-id="baa39-204">Add the following method to the Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="baa39-205">Tester en lisant votre contenu</span><span class="sxs-lookup"><span data-stu-id="baa39-205">Test by playing your content</span></span>

<span data-ttu-id="baa39-206">Une fois que vous exécutez le programme défini dans la section précédente, les URL similaires à celles qui suivent seront affichées dans la fenêtre de la console.</span><span class="sxs-lookup"><span data-stu-id="baa39-206">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="baa39-207">URL de diffusion adaptative :</span><span class="sxs-lookup"><span data-stu-id="baa39-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="baa39-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="baa39-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="baa39-209">HLS</span><span class="sxs-lookup"><span data-stu-id="baa39-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="baa39-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="baa39-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="baa39-211">URL de téléchargement progressif (audio et vidéo).</span><span class="sxs-lookup"><span data-stu-id="baa39-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="baa39-212">Pour diffuser votre vidéo, collez votre URL dans la zone de texte URL du [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="baa39-212">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="baa39-213">Pour tester le téléchargement progressif, collez l'URL dans un navigateur (par exemple, Internet Explorer, Chrome ou Safari).</span><span class="sxs-lookup"><span data-stu-id="baa39-213">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="baa39-214">Pour plus d’informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="baa39-214">For more information, see the following topics:</span></span>

- [<span data-ttu-id="baa39-215">Lecture de votre contenu à l’aide des lecteurs existants</span><span class="sxs-lookup"><span data-stu-id="baa39-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="baa39-216">Développement d'applications de lecteur vidéo</span><span class="sxs-lookup"><span data-stu-id="baa39-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="baa39-217">Incorporation d'une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js</span><span class="sxs-lookup"><span data-stu-id="baa39-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="baa39-218">Charger l’exemple</span><span class="sxs-lookup"><span data-stu-id="baa39-218">Download sample</span></span>
<span data-ttu-id="baa39-219">L’exemple de code suivant contient le code que vous avez créé dans ce didacticiel : [exemple](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="baa39-219">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="baa39-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="baa39-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="baa39-221">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="baa39-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
