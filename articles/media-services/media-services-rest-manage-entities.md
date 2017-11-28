---
title: "Gestion des entités Media Services avec REST | Microsoft Docs"
description: "Découvrez comment gérer des entités Media Services avec l'API REST"
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: a336907b605da962f835b8057ac6071f480cd85e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="32a3e-103">Gestion des entités Media Services avec REST</span><span class="sxs-lookup"><span data-stu-id="32a3e-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32a3e-104">REST</span><span class="sxs-lookup"><span data-stu-id="32a3e-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="32a3e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="32a3e-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="32a3e-106">Microsoft Azure Media Services est un service basé sur REST conçu autour d’OData v3.</span><span class="sxs-lookup"><span data-stu-id="32a3e-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="32a3e-107">Vous pouvez ajouter, interroger, mettre à jour et supprimer des entités de la même façon que vous pouvez le faire dans tout autre service OData.</span><span class="sxs-lookup"><span data-stu-id="32a3e-107">You can add, query, update, and delete entities in much the same way as you can on any other OData service.</span></span> <span data-ttu-id="32a3e-108">Toute exception sera indiquée le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="32a3e-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="32a3e-109">Pour plus d’informations sur OData, consultez la [documentation Open Data Protocol](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="32a3e-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="32a3e-110">Cette rubrique vous montre comment gérer les entités Azure Media Services avec REST.</span><span class="sxs-lookup"><span data-stu-id="32a3e-110">This topic shows you how to manage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="32a3e-111">À compter du 1er avril 2017, les enregistrements de travaux dans votre compte de plus de 90 jours seront automatiquement supprimés, ainsi que leurs enregistrements de tâches associés, même si le nombre total d’enregistrements est inférieur au quota maximum.</span><span class="sxs-lookup"><span data-stu-id="32a3e-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="32a3e-112">Par exemple, le 1er avril 2017, tout enregistrement de travail dans votre compte antérieur au 31 décembre 2016 sera automatiquement supprimé.</span><span class="sxs-lookup"><span data-stu-id="32a3e-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="32a3e-113">Si vous devez archiver les informations sur le travail/la tâche, vous pouvez utiliser le code décrit dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="32a3e-113">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="32a3e-114">Considérations</span><span class="sxs-lookup"><span data-stu-id="32a3e-114">Considerations</span></span>  

<span data-ttu-id="32a3e-115">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="32a3e-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="32a3e-116">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="32a3e-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="32a3e-117">Connexion à Media Services</span><span class="sxs-lookup"><span data-stu-id="32a3e-117">Connect to Media Services</span></span>

<span data-ttu-id="32a3e-118">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="32a3e-118">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="32a3e-119">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="32a3e-119">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="32a3e-120">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="32a3e-120">You must make subsequent calls to the new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="32a3e-121">Ajout d’entités</span><span class="sxs-lookup"><span data-stu-id="32a3e-121">Adding entities</span></span>
<span data-ttu-id="32a3e-122">Chaque entité de Media Services est ajoutée à un jeu d'entités, tel que Assets, via une demande HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="32a3e-122">Every entity in Media Services is added to an entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="32a3e-123">L’exemple suivant montre comment créer une stratégie AccessPolicy :</span><span class="sxs-lookup"><span data-stu-id="32a3e-123">The following example shows how to create an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="32a3e-124">Exécution d’une requête sur les entités</span><span class="sxs-lookup"><span data-stu-id="32a3e-124">Querying entities</span></span>
<span data-ttu-id="32a3e-125">La procédure d’interrogation et d’énumération des entités est simple et ne nécessite qu’une requête HTTP GET et les opérations OData facultatives.</span><span class="sxs-lookup"><span data-stu-id="32a3e-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="32a3e-126">L’exemple suivant montre la récupération d’une liste de toutes les entités MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="32a3e-126">The following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="32a3e-127">Vous pouvez également récupérer une entité spécifique ou tous les jeux d'entités associés à une entité spécifique, comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="32a3e-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in the following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="32a3e-128">L’exemple suivant renvoie uniquement la propriété State de toutes les tâches.</span><span class="sxs-lookup"><span data-stu-id="32a3e-128">The following example returns only the State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="32a3e-129">L'exemple suivant retourne l'ensemble des JobTemplates avec le nom « SampleTemplate ».</span><span class="sxs-lookup"><span data-stu-id="32a3e-129">The following example returns all JobTemplates with the name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="32a3e-130">L’opération $expand n’est pas prise en charge dans Media Services, tout comme les méthodes LINQ non prises en charge décrites dans les considérations sur LINQ (WCF Data Services).</span><span class="sxs-lookup"><span data-stu-id="32a3e-130">The $expand operation is not supported in Media Services as well as the unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="32a3e-131">Énumérer les grandes collections d'entités</span><span class="sxs-lookup"><span data-stu-id="32a3e-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="32a3e-132">Lors de l'interrogation des entités, il existe une limite de 1 000 entités retournées simultanément car l'API REST v2 publique limite les résultats des requêtes à 1 000 résultats.</span><span class="sxs-lookup"><span data-stu-id="32a3e-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="32a3e-133">Utilisez **skip** et **top** pour énumérer les grandes collections d’entités.</span><span class="sxs-lookup"><span data-stu-id="32a3e-133">Use **skip** and **top** to enumerate through the large collection of entities.</span></span> 

<span data-ttu-id="32a3e-134">L’exemple suivant montre comment utiliser **skip** et **top** pour ignorer les 2 000 premiers emplois et obtenir les 1 000 emplois suivants.</span><span class="sxs-lookup"><span data-stu-id="32a3e-134">The following example shows how to use **skip** and **top** to skip the first 2000 jobs and get the next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="32a3e-135">Mise à jour des entités</span><span class="sxs-lookup"><span data-stu-id="32a3e-135">Updating entities</span></span>
<span data-ttu-id="32a3e-136">Selon le type d’entité et l’état dans lequel elle se trouve, vous pouvez mettre à jour les propriétés de cette entité via une requête HTTP PATCH, PUT ou MERGE.</span><span class="sxs-lookup"><span data-stu-id="32a3e-136">Depending on the entity type and the state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="32a3e-137">Pour plus d’informations sur ces opérations, consultez [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="32a3e-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="32a3e-138">L’exemple de code suivant montre comment mettre à jour la propriété Name sur une entité Asset.</span><span class="sxs-lookup"><span data-stu-id="32a3e-138">The following code example shows how to update the Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="32a3e-139">Suppression des entités</span><span class="sxs-lookup"><span data-stu-id="32a3e-139">Deleting entities</span></span>
<span data-ttu-id="32a3e-140">Les entités peuvent être supprimées dans Media Services à l’aide d’une requête HTTP DELETE.</span><span class="sxs-lookup"><span data-stu-id="32a3e-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="32a3e-141">En fonction de l’entité, l’ordre dans lequel vous supprimez les entités peut être important.</span><span class="sxs-lookup"><span data-stu-id="32a3e-141">Depending on the entity, the order in which you delete entities may be important.</span></span> <span data-ttu-id="32a3e-142">Par exemple, les entités telles que Assets nécessitent que vous annuliez (ou supprimiez) tous les localisateurs qui font référence à cet Asset particulier avant de supprimer l’Asset.</span><span class="sxs-lookup"><span data-stu-id="32a3e-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting the Asset.</span></span>

<span data-ttu-id="32a3e-143">L’exemple suivant montre comment supprimer un localisateur qui était utilisé pour charger un fichier dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="32a3e-143">The following example shows how to delete a Locator that was used to upload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="32a3e-144">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="32a3e-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="32a3e-145">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="32a3e-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

