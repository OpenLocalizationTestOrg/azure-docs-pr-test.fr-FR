---
title: "Encodage d’une ressource Azure à l’aide de Media Encoder Standard | Microsoft Docs"
description: "Découvrez comment utiliser Media Encoder Standard pour encoder un contenu multimédia sur Azure Media Services. Les exemples de code utilisent l’API REST."
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
ms.openlocfilehash: 796f3b5a4dd56a0160986600cbbcf38faf8add56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="eb9ee-104">Encodage d’une ressource à l’aide de Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="eb9ee-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb9ee-105">.NET</span><span class="sxs-lookup"><span data-stu-id="eb9ee-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="eb9ee-106">REST</span><span class="sxs-lookup"><span data-stu-id="eb9ee-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="eb9ee-107">Portail</span><span class="sxs-lookup"><span data-stu-id="eb9ee-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="eb9ee-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="eb9ee-108">Overview</span></span>
<span data-ttu-id="eb9ee-109">Pour fournir une vidéo numérique sur Internet, vous devez compresser le contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="eb9ee-110">Les fichiers vidéo numériques sont volumineux et peuvent être trop gros pour être fournis sur Internet ou pour que les appareils de vos clients les affichent correctement.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="eb9ee-111">L’encodage est le processus de compression audio et vidéo permettant à vos clients d’afficher votre contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="eb9ee-112">Les tâches d’encodage sont une des opérations de traitement les plus courantes dans Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="eb9ee-113">Vous créez des tâches d’encodage pour convertir des fichiers multimédias d’un encodage à un autre.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="eb9ee-114">Lorsque vous les encodez, vous pouvez utiliser l’encodeur intégré de Media Services (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="eb9ee-115">Vous pouvez également utiliser un encodeur fourni par un partenaire Media Services.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="eb9ee-116">Les encodeurs tiers sont disponibles via Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="eb9ee-117">Vous pouvez spécifier les détails des tâches d’encodage à l’aide de chaînes de présélection définies pour votre encodeur ou en utilisant des fichiers de configuration prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="eb9ee-118">Pour voir les types de présélections disponibles, consultez [Présélections de tâches pour Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="eb9ee-119">Chaque travail peut comporter une ou plusieurs tâches, en fonction du type de traitement que vous souhaitez accomplir.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="eb9ee-120">Via l’API REST, vous pouvez créer des travaux et les tâches associées de deux manières :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="eb9ee-121">Des tâches peuvent être définies inline via la propriété de navigation de tâches sur les entités de travail.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="eb9ee-122">Utilisez le traitement par lots OData.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-122">Use OData batch processing.</span></span>

<span data-ttu-id="eb9ee-123">Nous vous recommandons de toujours encoder vos fichiers source sous forme de jeu de fichiers MP4 à débit adaptatif, puis de convertir ce jeu au format souhaité au moyen de [l’empaquetage dynamique](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="eb9ee-124">Si votre ressource de sortie est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="eb9ee-125">Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="eb9ee-126">Considérations</span><span class="sxs-lookup"><span data-stu-id="eb9ee-126">Considerations</span></span>

<span data-ttu-id="eb9ee-127">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="eb9ee-128">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="eb9ee-129">Avant de référencer les processeurs multimédias, vérifiez que vous disposez de l’ID de processeur multimédia approprié.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span></span> <span data-ttu-id="eb9ee-130">Pour plus d’informations, consultez la rubrique [Obtenir des processeurs multimédias](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="eb9ee-131">Connexion à Media Services</span><span class="sxs-lookup"><span data-stu-id="eb9ee-131">Connect to Media Services</span></span>

<span data-ttu-id="eb9ee-132">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="eb9ee-133">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-133">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="eb9ee-134">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-134">You must make subsequent calls to the new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="eb9ee-135">Création d’un travail avec une seule tâche d’encodage</span><span class="sxs-lookup"><span data-stu-id="eb9ee-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="eb9ee-136">Lorsque vous utilisez l’API REST de Media Services, les considérations suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-136">When you're working with the Media Services REST API, the following considerations apply:</span></span>
>
> <span data-ttu-id="eb9ee-137">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="eb9ee-138">Pour plus d’informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="eb9ee-139">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-139">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="eb9ee-140">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-140">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="eb9ee-141">Pour savoir comment vous connecter à l’API Azure Media Services, voir [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-141">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="eb9ee-142">Lors de l’utilisation de JSON et la spécification pour utiliser le mot clé **__metadata** dans la demande (par exemple, pour fait référence à un objet lié) vous devez définir l’en-tête **Accept** au [format JSON détaillé](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) : Accept: application/json;odata=verbose.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-142">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="eb9ee-143">L’exemple suivant montre comment créer et publier un projet avec une tâche visant à encoder une vidéo en une résolution et une qualité spécifiques.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-143">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="eb9ee-144">Quand vous encodez à l’aide de Media Encoder Standard, vous pouvez utiliser les présélections de configuration de tâche spécifiées [ici](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="eb9ee-145">Demande :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-145">Request:</span></span>

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

<span data-ttu-id="eb9ee-146">Réponse :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="eb9ee-147">Définir le nom de l’élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="eb9ee-147">Set the output asset's name</span></span>
<span data-ttu-id="eb9ee-148">L’exemple suivant montre comment définir l’attribut assetName :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-148">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="eb9ee-149">Considérations</span><span class="sxs-lookup"><span data-stu-id="eb9ee-149">Considerations</span></span>
* <span data-ttu-id="eb9ee-150">les propriétés TaskBody doivent utiliser un XML littéral pour définir le nombre de ressources d’entrée ou de sortie qui sont utilisées par la tâche.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-150">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="eb9ee-151">La rubrique Tâche contient la définition du schéma XML pour le XML.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-151">The task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="eb9ee-152">Dans la définition TaskBody, chaque valeur interne de <inputAsset> et <outputAsset> doit être définie en tant que JobInputAsset(valeur) ou JobOutputAsset(valeur).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-152">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="eb9ee-153">Une tâche peut comporter plusieurs ressources de sortie.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-153">A task can have multiple output assets.</span></span> <span data-ttu-id="eb9ee-154">Un JobOutputAsset(x) ne peut être utilisé qu’une fois en tant que résultat d’une tâche dans un travail.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="eb9ee-155">Vous pouvez spécifier JobInputAsset ou JobOutputAsset en tant que ressource d’entrée d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="eb9ee-156">Les tâches ne doivent pas former un cycle.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="eb9ee-157">Le paramètre de valeur que vous transmettez à JobInputAsset ou à JobOutputAsset représente la valeur d’index pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-157">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="eb9ee-158">Les ressources réelles sont définies dans les propriétés de navigation InputMediaAssets et OutputMediaAssets de la définition d’entité de travail.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-158">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="eb9ee-159">Étant donné que Media Services est basé sur OData v3, les ressources dans les collections de propriétés de navigation InputMediaAssets et OutputMediaAssets sont référencées par une paire nom-valeur « __metadata : uri ».</span><span class="sxs-lookup"><span data-stu-id="eb9ee-159">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="eb9ee-160">InputMediaAssets mappe vers une ou plusieurs ressources que vous avez créées dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-160">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="eb9ee-161">Les OutputMediaAssets sont créés par le système.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-161">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="eb9ee-162">Ils ne font pas référence à une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="eb9ee-163">OutputMediaAssets peut être nommé à l’aide de l’attribut assetName.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-163">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="eb9ee-164">Si cet attribut n’est pas présent, le nom d’OutputMediaAsset est la valeur de texte interne de l’élément <outputAsset> avec le suffixe de la valeur du nom du travail ou de l’ID de travail (dans le cas où la propriété Name n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-164">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="eb9ee-165">Par exemple, si vous affectez à assetName la valeur « Sample », la propriété de Nom d’OutputMediaAsset est définie sur « Sample ».</span><span class="sxs-lookup"><span data-stu-id="eb9ee-165">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="eb9ee-166">Toutefois, si vous n’avez pas défini de valeur pour assetName, mais avez défini le nom du travail comme « NewJob », le nom d’OutputMediaAsset est « JobOutputAsset(value)_NewJob ».</span><span class="sxs-lookup"><span data-stu-id="eb9ee-166">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="eb9ee-167">Création d’un travail avec des tâches chaînées</span><span class="sxs-lookup"><span data-stu-id="eb9ee-167">Create a job with chained tasks</span></span>
<span data-ttu-id="eb9ee-168">Dans de nombreux scénarios d’application, les développeurs souhaitent créer une série de tâches de traitement.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-168">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="eb9ee-169">Dans Media Services, vous pouvez créer une série de tâches chaînées.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="eb9ee-170">Chaque tâche effectue différentes étapes de traitement et peut utiliser différents processeurs multimédias.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="eb9ee-171">Les tâches chaînées peuvent transférer un élément multimédia d’une tâche à une autre, en effectuant une séquence linéaire de tâches sur la ressource.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-171">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="eb9ee-172">Toutefois, les tâches effectuées dans un travail ne le sont pas obligatoirement dans une séquence.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-172">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="eb9ee-173">Quand vous créez une tâche chaînée, les objets chaînés **ITask** sont créés dans un seul objet **IJob**.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-173">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9ee-174">Il existe actuellement une limite de 30 tâches par travail.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="eb9ee-175">Si vous devez chaîner plus de 30 tâches, créez plusieurs travaux pour contenir les tâches.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-175">If you need to chain more than 30 tasks, create more than one job to contain the tasks.</span></span>
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


### <a name="considerations"></a><span data-ttu-id="eb9ee-176">Considérations</span><span class="sxs-lookup"><span data-stu-id="eb9ee-176">Considerations</span></span>
<span data-ttu-id="eb9ee-177">Pour activer le chaînage des tâches :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-177">To enable task chaining:</span></span>

* <span data-ttu-id="eb9ee-178">un travail doit comporter au moins deux tâches.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="eb9ee-179">Il doit y avoir au moins une tâche dont l’entrée correspond à la sortie d’une autre tâche du travail.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-179">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="eb9ee-180">Utiliser le traitement par lots OData</span><span class="sxs-lookup"><span data-stu-id="eb9ee-180">Use OData batch processing</span></span>
<span data-ttu-id="eb9ee-181">L’exemple suivant illustre l’utilisation du traitement par lots OData pour créer un travail et des tâches.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-181">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="eb9ee-182">Pour plus d’informations sur le traitement par lots, consultez [Traitement par lots d’Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

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



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="eb9ee-183">Création d’un travail à l’aide d’un JobTemplate</span><span class="sxs-lookup"><span data-stu-id="eb9ee-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="eb9ee-184">Pendant le traitement de plusieurs ressources à l’aide d’un jeu commun de tâches, utilisez un JobTemplate pour spécifier les présélections de tâches par défaut ou pour définir l’ordre des tâches.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-184">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="eb9ee-185">L’exemple suivant montre comment créer un JobTemplate avec un TaskTemplate défini en ligne.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-185">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="eb9ee-186">Le TaskTemplate utilise Media Encoder Standard comme MediaProcessor pour encoder le fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-186">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="eb9ee-187">Toutefois, d’autres MediaProcessors peuvent être également utilisés.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-187">However, other MediaProcessors can be used as well.</span></span>

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
> <span data-ttu-id="eb9ee-188">Contrairement à d’autres entités Media Services, vous devez définir un nouvel identificateur GUID pour chaque TaskTemplate et le placer dans la propriété taskTemplateId et Id du corps de votre demande.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="eb9ee-189">Le schéma d’identification de contenu doit respecter le schéma décrit dans la rubrique Identifier les entités Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-189">The content identification scheme must follow the scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="eb9ee-190">En outre, les JobTemplates ne peuvent pas être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="eb9ee-191">À la place, vous devez en créer un avec vos modifications mises à jour.</span><span class="sxs-lookup"><span data-stu-id="eb9ee-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="eb9ee-192">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-192">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="eb9ee-193">L’exemple suivant montre comment créer un travail faisant référence à un ID de JobTemplate :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-193">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="eb9ee-194">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="eb9ee-194">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="eb9ee-195">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="eb9ee-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="eb9ee-196">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="eb9ee-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="eb9ee-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb9ee-197">Next steps</span></span>
<span data-ttu-id="eb9ee-198">Maintenant que vous savez comment créer un travail d'encodage de ressource, consultez [Vérification de la progression d’une tâche avec Media Services](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="eb9ee-198">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="eb9ee-199">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="eb9ee-199">See also</span></span>
[<span data-ttu-id="eb9ee-200">Obtenir des processeurs multimédias</span><span class="sxs-lookup"><span data-stu-id="eb9ee-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
