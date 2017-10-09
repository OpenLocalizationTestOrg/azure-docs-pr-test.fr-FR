---
title: "aaaGet en main de diffusion de contenu sur demande à l’aide de .NET | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’une application de diffusion de contenu sur la demande avec Azure Media Services à l’aide de .NET."
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
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="f7d95-103">Prendre en main la diffusion de contenus à la demande à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="f7d95-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="f7d95-104">Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’un service de diffusion de contenu vidéo à la demande (VoD) base avec l’application Azure Media Services (AMS) à l’aide de hello Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="f7d95-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7d95-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f7d95-105">Prerequisites</span></span>

<span data-ttu-id="f7d95-106">Hello Voici didacticiel de hello toocomplete requis :</span><span class="sxs-lookup"><span data-stu-id="f7d95-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="f7d95-107">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f7d95-107">An Azure account.</span></span> <span data-ttu-id="f7d95-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7d95-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f7d95-109">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="f7d95-109">A Media Services account.</span></span> <span data-ttu-id="f7d95-110">toocreate un compte Media Services, consultez [comment tooCreate un compte Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="f7d95-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="f7d95-111">.NET Framework 4.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f7d95-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="f7d95-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7d95-112">Visual Studio.</span></span>

<span data-ttu-id="f7d95-113">Ce didacticiel inclut hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7d95-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="f7d95-114">Début de la diffusion en continu de point de terminaison (à l’aide de hello portail Azure).</span><span class="sxs-lookup"><span data-stu-id="f7d95-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="f7d95-115">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f7d95-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="f7d95-116">Connectez le compte de service de média toohello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="f7d95-117">Télécharger un fichier vidéo.</span><span class="sxs-lookup"><span data-stu-id="f7d95-117">Upload a video file.</span></span>
3. <span data-ttu-id="f7d95-118">Encoder le fichier de source de hello en un ensemble de fichiers MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="f7d95-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="f7d95-119">Publier les actifs hello et get de diffusion en continu et URL de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="f7d95-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="f7d95-120">Lire votre contenu.</span><span class="sxs-lookup"><span data-stu-id="f7d95-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="f7d95-121">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f7d95-121">Overview</span></span>
<span data-ttu-id="f7d95-122">Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’une application de diffusion de contenu vidéo à la demande (VoD) à l’aide d’Azure Media Services (AMS) SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="f7d95-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="f7d95-123">didacticiel de Hello présente des flux de travail Media Services hello et objets de programmation courants hello et tâches requises pour le développement de Media Services.</span><span class="sxs-lookup"><span data-stu-id="f7d95-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="f7d95-124">À l’achèvement de hello du didacticiel de hello, vous être en mesure de toostream ou télécharger progressivement un exemple de fichier de média que vous avez téléchargé, encodé, téléchargé.</span><span class="sxs-lookup"><span data-stu-id="f7d95-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="f7d95-125">Modèle d’AMS</span><span class="sxs-lookup"><span data-stu-id="f7d95-125">AMS model</span></span>

<span data-ttu-id="f7d95-126">Hello image suivante montre certains des objets de hello couramment utilisé lors du développement d’applications VoD sur le modèle de Media Services OData hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="f7d95-127">Cliquez sur tooview d’image hello il plein écran.</span><span class="sxs-lookup"><span data-stu-id="f7d95-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="f7d95-128">Vous pouvez afficher hello ensemble modèle [ici](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="f7d95-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="f7d95-129">Démarrer la diffusion en continu des points de terminaison à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f7d95-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="f7d95-130">Lorsque vous travaillez avec un des scénarios les plus courants de hello est diffusion vidéo via à débit adaptatif de diffusion en continu Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="f7d95-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="f7d95-131">Media Services propose un empaquetage dynamique, ce qui vous permet de toodeliver votre vitesse de transmission adaptative MP4 encodés le contenu de diffusion en continu des formats pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) juste-à-temps, sans que vous ayez toostore préconçue versions de chacune de ces formats de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f7d95-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="f7d95-132">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="f7d95-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="f7d95-133">toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="f7d95-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="f7d95-134">toostart hello du point de terminaison de diffusion en continu, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f7d95-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="f7d95-135">Connectez-vous à l’adresse hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f7d95-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f7d95-136">Dans la fenêtre des paramètres hello, cliquez sur les points de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f7d95-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="f7d95-137">Cliquez sur le point de terminaison de diffusion en continu de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="f7d95-138">fenêtre de détails par défaut du point de terminaison de diffusion en continu Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f7d95-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="f7d95-139">Cliquez sur l’icône Démarrer hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="f7d95-140">Cliquez sur toosave de bouton hello enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="f7d95-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="f7d95-141">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f7d95-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="f7d95-142">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f7d95-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="f7d95-143">Créer un nouveau dossier (dossier peut être n’importe où sur votre disque local) et copiez le fichier .mp4 que vous voulez tooencode et flux de données ou téléchargez progressivement.</span><span class="sxs-lookup"><span data-stu-id="f7d95-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="f7d95-144">Dans cet exemple, le chemin d’accès de hello « C:\VideoFiles » est utilisé.</span><span class="sxs-lookup"><span data-stu-id="f7d95-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="f7d95-145">Compte de service de média toohello de connexion</span><span class="sxs-lookup"><span data-stu-id="f7d95-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="f7d95-146">Lorsque vous utilisez Media Services avec .NET, vous devez utiliser hello **CloudMediaContext** classe pour les Services de support la plupart des tâches de programmation : la connexion de compte de Services tooMedia ; la création, mise à jour, l’accès à et suppression suivantes de hello objets : actifs, fichiers d’éléments multimédias, travaux, les stratégies d’accès, les localisateurs, etc..</span><span class="sxs-lookup"><span data-stu-id="f7d95-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="f7d95-147">Remplacer classe de programme par défaut hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="f7d95-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="f7d95-148">Hello de code montre comment les valeurs de connexion de hello tooread à partir du fichier App.config de hello et toocreate hello **CloudMediaContext** Services d’objet dans l’ordre tooconnect tooMedia.</span><span class="sxs-lookup"><span data-stu-id="f7d95-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="f7d95-149">Pour plus d’informations, consultez [connexion toohello API Media Services](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f7d95-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="f7d95-150">Assurez-vous que tooupdate hello fichier nom et chemin d’accès toowhere que vous avez votre fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="f7d95-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="f7d95-151">Hello **Main** fonction appelle des méthodes qui seront définies ultérieurement dans cette section.</span><span class="sxs-lookup"><span data-stu-id="f7d95-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="f7d95-152">Vous allez récupérer les erreurs de compilation jusqu'à ce que vous ajoutez des définitions pour toutes les fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

    class Program
    {
        // Read values from hello App.config file.
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

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="f7d95-153">Créer un nouvel élément et charger un fichier vidéo</span><span class="sxs-lookup"><span data-stu-id="f7d95-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="f7d95-154">Dans Media Services, vous téléchargez (ou réceptionnez) vos fichiers numériques dans un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="f7d95-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="f7d95-155">Hello **Asset** entité peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.)  Une fois que les fichiers hello sont téléchargés, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f7d95-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="f7d95-156">fichiers Hello dans asset de hello sont appelés **des fichiers**.</span><span class="sxs-lookup"><span data-stu-id="f7d95-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="f7d95-157">Hello **UploadFile** définie sous les appels de méthode **CreateFromFile** (défini dans les Extensions du Kit de développement logiciel .NET).</span><span class="sxs-lookup"><span data-stu-id="f7d95-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="f7d95-158">**CreateFromFile** crée un nouvel élément multimédia dans quel hello fichier source spécifié est chargé.</span><span class="sxs-lookup"><span data-stu-id="f7d95-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="f7d95-159">Hello **CreateFromFile** méthode **AssetCreationOptions** qui vous permet de spécifier l’une des hello asset création options suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7d95-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="f7d95-160">**None** : aucun chiffrement.</span><span class="sxs-lookup"><span data-stu-id="f7d95-160">**None** - No encryption is used.</span></span> <span data-ttu-id="f7d95-161">Il s’agit de valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-161">This is hello default value.</span></span> <span data-ttu-id="f7d95-162">À noter que quand vous utilisez cette option, votre contenu n'est pas protégé pendant le transit ou le repos dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="f7d95-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="f7d95-163">Si vous envisagez de toodeliver un fichier MP4 à l’aide d’un téléchargement progressif, utilisez cette option.</span><span class="sxs-lookup"><span data-stu-id="f7d95-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="f7d95-164">**StorageEncrypted** -Utilisez cette option tooencrypt votre contenu en clair localement à l’aide de chiffrement Advanced Encryption Standard (AES)-256 bits, qui télécharge tooAzure Storage où il est stocké et chiffré au repos.</span><span class="sxs-lookup"><span data-stu-id="f7d95-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="f7d95-165">Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="f7d95-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="f7d95-166">Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au repos sur le disque.</span><span class="sxs-lookup"><span data-stu-id="f7d95-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="f7d95-167">**CommonEncryptionProtected** : utilisez cette option quand vous chargez du contenu qui a déjà été chiffré et protégé avec la DRM Common Encryption ou PlayReady (par exemple Smooth Streaming protégé avec la DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="f7d95-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="f7d95-168">**EnvelopeEncryptionProtected** : utilisez cette option lorsque vous téléchargez un contenu au format TLS chiffré avec AES.</span><span class="sxs-lookup"><span data-stu-id="f7d95-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="f7d95-169">Notez que les fichiers hello doivent avoir été codés et chiffrés par Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="f7d95-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="f7d95-170">Hello **CreateFromFile** méthode vous permet également de spécifier un rappel de progression du téléchargement ordre tooreport hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="f7d95-171">Bonjour l’exemple suivant, nous spécifions **aucun** pour les options d’asset hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="f7d95-172">Ajoutez hello suivant de méthode toohello classe de programme.</span><span class="sxs-lookup"><span data-stu-id="f7d95-172">Add hello following method toohello Program class.</span></span>

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="f7d95-173">Encoder le fichier de source de hello en un ensemble de fichiers MP4 à débit adaptatif</span><span class="sxs-lookup"><span data-stu-id="f7d95-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="f7d95-174">Après réception d’éléments multimédias dans Media Services, support peut être codée, transmuxed, filigrane et ainsi de suite, avant de le livrer tooclients.</span><span class="sxs-lookup"><span data-stu-id="f7d95-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="f7d95-175">Ces activités sont planifiées et exécutées sur plusieurs arrière-plan rôle instances tooensure performances et la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="f7d95-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="f7d95-176">Ces activités sont appellent des travaux, et chaque tâche se compose de tâches atomiques qui hello travail réel dans le fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="f7d95-177">Comme mentionné précédemment, lorsque vous travaillez avec Azure Media Services, un des scénarios les plus courants de hello est remise à débit adaptatif tooyour clients de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f7d95-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="f7d95-178">Media Services peut package dynamiquement un ensemble de fichiers MP4 à débit adaptatif dans une des hello suivant formats : HTTP Live Streaming (HLS), la diffusion en continu lisse et MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="f7d95-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="f7d95-179">tootake parti de l’empaquetage dynamique, vous devez tooencode ou transcoder votre fichier mezzanine (source) dans un ensemble de fichiers MP4 ou de fichiers de diffusion en continu lisse à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="f7d95-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="f7d95-180">Hello suivant de code montre comment toosubmit un encodage de la tâche.</span><span class="sxs-lookup"><span data-stu-id="f7d95-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="f7d95-181">tâche Hello contient une tâche qui spécifie un fichier mezzanine de hello tootranscode dans un ensemble de l’utilisation de fichiers à débit adaptatif MP4s **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="f7d95-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="f7d95-182">code de Hello soumet le travail de hello et attend jusqu'à son terme.</span><span class="sxs-lookup"><span data-stu-id="f7d95-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="f7d95-183">Une fois le travail de hello est terminé, vous est en mesure de toostream votre élément multimédia ou télécharger progressivement les fichiers MP4 qui ont été créés à la suite de transcodage.</span><span class="sxs-lookup"><span data-stu-id="f7d95-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="f7d95-184">Ajoutez hello suivant de méthode toohello classe de programme.</span><span class="sxs-lookup"><span data-stu-id="f7d95-184">Add hello following method toohello Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
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

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="f7d95-185">Publier l’élément multimédia de hello et obtenir l’URL pour le téléchargement progressif et de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="f7d95-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="f7d95-186">toostream ou téléchargement d’un élément multimédia, vous tout d’abord besoin trop « publier » en créant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="f7d95-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="f7d95-187">Les localisateurs offrent toofiles accès contenues dans l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="f7d95-188">Media Services prend en charge deux types de localisateurs : OnDemandOrigin localisateurs, support toostream utilisé (par exemple, MPEG DASH, HLS ou Smooth Streaming) et les localisateurs de Signature d’accès (SAS), les fichiers de support de toodownload (pour plus d’informations sur SAS localisateurs, consultez utilisés[cela](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="f7d95-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="f7d95-189">Informations sur les formats d’URL</span><span class="sxs-lookup"><span data-stu-id="f7d95-189">Some details about URL formats</span></span>

<span data-ttu-id="f7d95-190">Après avoir créé les localisateurs hello, vous pouvez générer des URL hello qui est utilisé toostream ou téléchargez vos fichiers.</span><span class="sxs-lookup"><span data-stu-id="f7d95-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="f7d95-191">exemple Hello dans ce didacticiel ne produira pas les URL que vous pouvez coller dans les navigateurs appropriés.</span><span class="sxs-lookup"><span data-stu-id="f7d95-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="f7d95-192">Cette section donne simplement quelques rapides exemples de l’aspect des différents formats.</span><span class="sxs-lookup"><span data-stu-id="f7d95-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="f7d95-193">Une URL de diffusion en continu pour MPEG DASH a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="f7d95-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="f7d95-194">{nom du point de terminaison de streaming-nom du compte media services}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="f7d95-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="f7d95-195">Une URL de diffusion en continu pour TLS a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="f7d95-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="f7d95-196">{nom du point de terminaison de streaming-nom du compte media services}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="f7d95-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="f7d95-197">Une URL de diffusion pour Smooth Streaming a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="f7d95-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="f7d95-198">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest</span><span class="sxs-lookup"><span data-stu-id="f7d95-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="f7d95-199">Une URL SAS utilisé des fichiers toodownload a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="f7d95-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="f7d95-200">{nom du conteneur d’objets blob}/{nom de la ressource}/{nom du fichier}/{signature SAS}</span><span class="sxs-lookup"><span data-stu-id="f7d95-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="f7d95-201">Extensions de Media Services .NET SDK fournissent des méthodes d’assistance pratiques que retour mise en forme des URL pour hello publié actif.</span><span class="sxs-lookup"><span data-stu-id="f7d95-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="f7d95-202">Hello de code suivant utilise les localisateurs toocreate Extensions du Kit de développement .NET et URL de téléchargement progressif et tooget de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f7d95-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="f7d95-203">code de Hello montre également comment toodownload fichiers tooa les dossier local.</span><span class="sxs-lookup"><span data-stu-id="f7d95-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="f7d95-204">Ajoutez hello suivant de méthode toohello classe de programme.</span><span class="sxs-lookup"><span data-stu-id="f7d95-204">Add hello following method toohello Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
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

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="f7d95-205">Tester en lisant votre contenu</span><span class="sxs-lookup"><span data-stu-id="f7d95-205">Test by playing your content</span></span>

<span data-ttu-id="f7d95-206">Une fois que vous exécutez le programme hello défini dans la section précédente de hello, hello URL similaire toohello suivant s’affichera dans la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="f7d95-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="f7d95-207">URL de diffusion adaptative :</span><span class="sxs-lookup"><span data-stu-id="f7d95-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="f7d95-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="f7d95-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="f7d95-209">HLS</span><span class="sxs-lookup"><span data-stu-id="f7d95-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="f7d95-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="f7d95-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="f7d95-211">URL de téléchargement progressif (audio et vidéo).</span><span class="sxs-lookup"><span data-stu-id="f7d95-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="f7d95-212">toostream votre vidéo, collez l’URL dans la zone de texte URL hello Bonjour [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="f7d95-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="f7d95-213">tootest progressif de téléchargement, collez une URL dans un navigateur (par exemple, Internet Explorer, Chrome ou Safari).</span><span class="sxs-lookup"><span data-stu-id="f7d95-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="f7d95-214">Pour plus d’informations, consultez hello rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7d95-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="f7d95-215">Lecture de votre contenu à l’aide des lecteurs existants</span><span class="sxs-lookup"><span data-stu-id="f7d95-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="f7d95-216">Développement d'applications de lecteur vidéo</span><span class="sxs-lookup"><span data-stu-id="f7d95-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="f7d95-217">Incorporation d'une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js</span><span class="sxs-lookup"><span data-stu-id="f7d95-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="f7d95-218">Charger l’exemple</span><span class="sxs-lookup"><span data-stu-id="f7d95-218">Download sample</span></span>
<span data-ttu-id="f7d95-219">exemple de code suivant Hello contient code hello que vous avez créé dans ce didacticiel : [exemple](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="f7d95-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7d95-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f7d95-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f7d95-221">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="f7d95-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
