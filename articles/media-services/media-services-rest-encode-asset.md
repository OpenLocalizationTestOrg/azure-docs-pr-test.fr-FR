---
title: "aaaHow tooencode une ressource Azure à l’aide de Media Encoder Standard | Documents Microsoft"
description: "Découvrez comment du contenu multimédia de tooencode Media Encoder Standard toouse sur Azure Media Services. Les exemples de code utilisent l’API REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="007df-104">Comment tooencode un élément multimédia à l’aide de Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="007df-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="007df-105">.NET</span><span class="sxs-lookup"><span data-stu-id="007df-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="007df-106">REST</span><span class="sxs-lookup"><span data-stu-id="007df-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="007df-107">Portail</span><span class="sxs-lookup"><span data-stu-id="007df-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="007df-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="007df-108">Overview</span></span>
<span data-ttu-id="007df-109">toodeliver vidéo numérique sur hello Internet, vous devez compresser le média de hello.</span><span class="sxs-lookup"><span data-stu-id="007df-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="007df-110">Fichiers vidéo numériques sont volumineux et peuvent être trop toodeliver hello Internet, ou, pour toodisplay des appareils de vos clients correctement.</span><span class="sxs-lookup"><span data-stu-id="007df-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="007df-111">Encodage consiste hello compression vidéo et audio afin que vos clients puissent afficher votre contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="007df-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="007df-112">Travaux d’encodage est une des opérations les plus courantes traitement hello dans Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="007df-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="007df-113">Vous créez des fichiers multimédias tooconvert travaux encodage à partir d’un tooanother de codage.</span><span class="sxs-lookup"><span data-stu-id="007df-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="007df-114">Lorsque vous codez, vous pouvez utiliser hello encodeur Media Services intégré (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="007df-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="007df-115">Vous pouvez également utiliser un encodeur fourni par un partenaire Media Services.</span><span class="sxs-lookup"><span data-stu-id="007df-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="007df-116">Les encodeurs tiers sont disponibles via hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="007df-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="007df-117">Vous pouvez spécifier les détails de hello des tâches d’encodage à l’aide de chaînes de présélection définies pour votre encodeur ou à l’aide de fichiers de configuration prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="007df-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="007df-118">types de hello toosee des paramètres prédéfinis qui sont disponibles, consultez [Présélections de tâches pour Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="007df-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="007df-119">Chaque tâche peut avoir l’une ou plusieurs tâches en fonction de type hello de traitement que vous souhaitez tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="007df-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="007df-120">Via l’API REST de hello, vous pouvez créer des tâches et leurs tâches connexes de deux manières :</span><span class="sxs-lookup"><span data-stu-id="007df-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="007df-121">Tâches peuvent être définies inline via la propriété de navigation hello tâches sur des entités Job.</span><span class="sxs-lookup"><span data-stu-id="007df-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="007df-122">Utilisez le traitement par lots OData.</span><span class="sxs-lookup"><span data-stu-id="007df-122">Use OData batch processing.</span></span>

<span data-ttu-id="007df-123">Nous vous recommandons de toujours encoder vos fichiers sources dans un ensemble de fichiers MP4 de débit adaptatif et de puis convertir le format désiré de hello ensemble toohello à l’aide de [empaquetage dynamique](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="007df-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="007df-124">Si votre élément multimédia de sortie est chiffré de stockage, vous devez configurer la stratégie de livraison des actifs hello.</span><span class="sxs-lookup"><span data-stu-id="007df-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="007df-125">Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="007df-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="007df-126">Considérations</span><span class="sxs-lookup"><span data-stu-id="007df-126">Considerations</span></span>

<span data-ttu-id="007df-127">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="007df-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="007df-128">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="007df-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="007df-129">Avant de commencer, faisant référence à des processeurs multimédias, vérifiez que vous avez hello ID de processeur média approprié.</span><span class="sxs-lookup"><span data-stu-id="007df-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="007df-130">Pour plus d’informations, consultez la rubrique [Obtenir des processeurs multimédias](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="007df-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="007df-131">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="007df-131">Connect tooMedia Services</span></span>

<span data-ttu-id="007df-132">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="007df-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="007df-133">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="007df-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="007df-134">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="007df-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="007df-135">Création d’un travail avec une seule tâche d’encodage</span><span class="sxs-lookup"><span data-stu-id="007df-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="007df-136">Lorsque vous travaillez avec hello API REST Media Services, hello considérations suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="007df-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="007df-137">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="007df-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="007df-138">Pour plus d’informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="007df-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="007df-139">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="007df-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="007df-140">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="007df-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="007df-141">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="007df-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="007df-142">Lors de l’utilisation de JSON et en spécifiant toouse hello **__metadata** mot clé dans la demande de hello (par exemple, tooreferences un objet lié), vous devez définir hello **accepter** en-tête trop[format JSON détaillé ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accepter : application/json ; odata = verbose.</span><span class="sxs-lookup"><span data-stu-id="007df-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="007df-143">Hello l’exemple suivant vous montre toocreate et valider un travail avec une seule tâche définition tooencode une vidéo à une résolution spécifique et la qualité.</span><span class="sxs-lookup"><span data-stu-id="007df-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="007df-144">Quand vous encodez à l’aide de Media Encoder Standard, vous pouvez utiliser les présélections de configuration de tâche spécifiées [ici](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="007df-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="007df-145">Demande :</span><span class="sxs-lookup"><span data-stu-id="007df-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="007df-146">Réponse :</span><span class="sxs-lookup"><span data-stu-id="007df-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="007df-147">Définir le nom de l’élément multimédia de sortie de hello</span><span class="sxs-lookup"><span data-stu-id="007df-147">Set hello output asset's name</span></span>
<span data-ttu-id="007df-148">Bonjour à l’exemple suivant montre comment tooset hello attribut assetName :</span><span class="sxs-lookup"><span data-stu-id="007df-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="007df-149">Considérations</span><span class="sxs-lookup"><span data-stu-id="007df-149">Considerations</span></span>
* <span data-ttu-id="007df-150">Propriétés TaskBody doivent utiliser le nombre de hello de toodefine littéral XML d’entrée, ou d’éléments multimédias de sortie qui sont utilisées par la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="007df-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="007df-151">la rubrique Hello contient hello définition de schéma XML pour hello XML.</span><span class="sxs-lookup"><span data-stu-id="007df-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="007df-152">Bonjour définition de TaskBody, chaque interne valeur <inputAsset> et <outputAsset> doit être définie en tant que JobInputAsset(value) ou JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="007df-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="007df-153">Une tâche peut comporter plusieurs ressources de sortie.</span><span class="sxs-lookup"><span data-stu-id="007df-153">A task can have multiple output assets.</span></span> <span data-ttu-id="007df-154">Un JobOutputAsset(x) ne peut être utilisé qu’une fois en tant que résultat d’une tâche dans un travail.</span><span class="sxs-lookup"><span data-stu-id="007df-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="007df-155">Vous pouvez spécifier JobInputAsset ou JobOutputAsset en tant que ressource d’entrée d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="007df-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="007df-156">Les tâches ne doivent pas former un cycle.</span><span class="sxs-lookup"><span data-stu-id="007df-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="007df-157">paramètre de valeur Hello que vous passez tooJobInputAsset ou JobOutputAsset représente la valeur d’index hello pour un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="007df-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="007df-158">éléments multimédias réels de Hello sont définies dans hello InputMediaAssets et OutputMediaAssets des propriétés de navigation sur la définition de l’entité tâche hello.</span><span class="sxs-lookup"><span data-stu-id="007df-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="007df-159">Comme Media Services repose sur OData v3, hello des éléments multimédias individuels dans hello InputMediaAssets et OutputMediaAssets des ensembles de propriétés de navigation sont référencés par un « __metadata : uri « paire nom-valeur.</span><span class="sxs-lookup"><span data-stu-id="007df-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="007df-160">InputMediaAssets mappe tooone ou plus actifs que vous avez créé dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="007df-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="007df-161">Propriétés OutputMediaAssets sont créées par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="007df-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="007df-162">Ils ne font pas référence à une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="007df-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="007df-163">OutputMediaAssets peut être nommé en utilisant l’attribut assetName de hello.</span><span class="sxs-lookup"><span data-stu-id="007df-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="007df-164">Si cet attribut n’est pas présent, nom hello Hello OutputMediaAsset est la valeur de texte interne hello Hello <outputAsset> élément est avec un suffixe de valeur de nom de la tâche hello ou valeur d’Id de tâche hello (dans le cas de hello où la propriété de nom hello n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="007df-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="007df-165">Par exemple, si vous définissez une valeur pour assetName trop « Exemple », puis hello propriété a la valeur Name du OutputMediaAsset trop « Sample. »</span><span class="sxs-lookup"><span data-stu-id="007df-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="007df-166">Toutefois, si vous n’avez pas de définir une valeur pour assetName, mais qui définissez le nom de la tâche hello trop « NewJob », puis hello Name du OutputMediaAsset serait « JobOutputAsset (valeur) _NewJob. »</span><span class="sxs-lookup"><span data-stu-id="007df-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="007df-167">Création d’un travail avec des tâches chaînées</span><span class="sxs-lookup"><span data-stu-id="007df-167">Create a job with chained tasks</span></span>
<span data-ttu-id="007df-168">Dans de nombreux scénarios d’application, les développeurs souhaitent toocreate une série de tâches de traitement.</span><span class="sxs-lookup"><span data-stu-id="007df-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="007df-169">Dans Media Services, vous pouvez créer une série de tâches chaînées.</span><span class="sxs-lookup"><span data-stu-id="007df-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="007df-170">Chaque tâche effectue différentes étapes de traitement et peut utiliser différents processeurs multimédias.</span><span class="sxs-lookup"><span data-stu-id="007df-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="007df-171">tâches de Hello chaînée peuvent transmettre une ressource à partir d’une tâche tooanother, exécution d’une séquence linéaire de tâches sur les actifs hello.</span><span class="sxs-lookup"><span data-stu-id="007df-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="007df-172">Toutefois, les tâches de hello effectuées dans un travail ne sont pas requis toobe dans une séquence.</span><span class="sxs-lookup"><span data-stu-id="007df-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="007df-173">Lorsque vous créez une tâche chaînée, hello chaînés **ITask** objets sont créés dans un seul **IJob** objet.</span><span class="sxs-lookup"><span data-stu-id="007df-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="007df-174">Il existe actuellement une limite de 30 tâches par travail.</span><span class="sxs-lookup"><span data-stu-id="007df-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="007df-175">Si vous devez toochain plus de 30 tâches, vous pouvez créer plusieurs travaux toocontain des tâches hello.</span><span class="sxs-lookup"><span data-stu-id="007df-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="007df-176">Considérations</span><span class="sxs-lookup"><span data-stu-id="007df-176">Considerations</span></span>
<span data-ttu-id="007df-177">tooenable chaînage des tâches :</span><span class="sxs-lookup"><span data-stu-id="007df-177">tooenable task chaining:</span></span>

* <span data-ttu-id="007df-178">un travail doit comporter au moins deux tâches.</span><span class="sxs-lookup"><span data-stu-id="007df-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="007df-179">Il doit exister au moins une tâche dont l’entrée est sortie hello d’une autre tâche dans la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="007df-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="007df-180">Utiliser le traitement par lots OData</span><span class="sxs-lookup"><span data-stu-id="007df-180">Use OData batch processing</span></span>
<span data-ttu-id="007df-181">Bonjour à l’exemple suivant montre comment toouse OData lot traitement toocreate un projet et les tâches.</span><span class="sxs-lookup"><span data-stu-id="007df-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="007df-182">Pour plus d’informations sur le traitement par lots, consultez [Traitement par lots d’Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="007df-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="007df-183">Création d’un travail à l’aide d’un JobTemplate</span><span class="sxs-lookup"><span data-stu-id="007df-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="007df-184">Lorsque vous traitez plusieurs éléments multimédias à l’aide d’un jeu commun de tâches, utilisez qu'une tâche par défaut de JobTemplate toospecify hello prédéfinis ou ordre de hello tooset des tâches.</span><span class="sxs-lookup"><span data-stu-id="007df-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="007df-185">Bonjour à l’exemple suivant montre comment toocreate un JobTemplate avec un TaskTemplate qui est définie en ligne.</span><span class="sxs-lookup"><span data-stu-id="007df-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="007df-186">Hello TaskTemplate utilise hello Media Encoder Standard en tant que fichier d’élément multimédia hello MediaProcessor tooencode hello.</span><span class="sxs-lookup"><span data-stu-id="007df-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="007df-187">Toutefois, d’autres MediaProcessors peuvent être également utilisés.</span><span class="sxs-lookup"><span data-stu-id="007df-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="007df-188">Contrairement à d’autres entités Media Services, vous devez définir un nouvel identificateur GUID pour chaque TaskTemplate et placez-le dans Propriétés hello taskTemplateId et Id dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="007df-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="007df-189">schéma d’identification du contenu Hello doit suivre hello schéma décrit dans identifier les entités Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="007df-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="007df-190">En outre, les JobTemplates ne peuvent pas être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="007df-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="007df-191">À la place, vous devez en créer un avec vos modifications mises à jour.</span><span class="sxs-lookup"><span data-stu-id="007df-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="007df-192">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="007df-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="007df-193">Hello suivant montre l’exemple de comment toocreate un travail qui fait référence à un JobTemplate Id :</span><span class="sxs-lookup"><span data-stu-id="007df-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="007df-194">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="007df-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="007df-195">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="007df-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="007df-196">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="007df-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="007df-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="007df-197">Next steps</span></span>
<span data-ttu-id="007df-198">Maintenant que vous savez comment toocreate un tooencode de travail un élément multimédia, consultez [comment toocheck travail progression avec Media Services](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="007df-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="007df-199">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="007df-199">See also</span></span>
[<span data-ttu-id="007df-200">Obtenir des processeurs multimédias</span><span class="sxs-lookup"><span data-stu-id="007df-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
