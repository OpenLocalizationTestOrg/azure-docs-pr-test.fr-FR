---
title: "aaaManaging des entités de Media Services avec REST | Documents Microsoft"
description: "Découvrez comment toomanage Media Services entités avec l’API REST."
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
ms.openlocfilehash: bcdc5288e422ebc4e6f682a97da4e925ce237a79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="b1a82-103">Gestion des entités Media Services avec REST</span><span class="sxs-lookup"><span data-stu-id="b1a82-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1a82-104">REST</span><span class="sxs-lookup"><span data-stu-id="b1a82-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="b1a82-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b1a82-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="b1a82-106">Microsoft Azure Media Services est un service basé sur REST conçu autour d’OData v3.</span><span class="sxs-lookup"><span data-stu-id="b1a82-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="b1a82-107">Vous pouvez ajouter, requête, mise à jour et supprimer des entités à peu près hello même façon que vous pouvez le faire sur n’importe quel autre service OData.</span><span class="sxs-lookup"><span data-stu-id="b1a82-107">You can add, query, update, and delete entities in much hello same way as you can on any other OData service.</span></span> <span data-ttu-id="b1a82-108">Toute exception sera indiquée le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="b1a82-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="b1a82-109">Pour plus d’informations sur OData, consultez la [documentation Open Data Protocol](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="b1a82-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="b1a82-110">Cette rubrique vous montre comment toomanage les entités Azure Media Services avec REST.</span><span class="sxs-lookup"><span data-stu-id="b1a82-110">This topic shows you how toomanage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="b1a82-111">À partir du 1er avril 2017, n’importe quel enregistrement de la tâche dans votre compte plu de 90 jours est automatiquement supprimé, ainsi que ses enregistrements de tâche associés, même si le nombre total de hello d’enregistrements est au-dessous du quota maximal de hello.</span><span class="sxs-lookup"><span data-stu-id="b1a82-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="b1a82-112">Par exemple, le 1er avril 2017, tout enregistrement de travail dans votre compte antérieur au 31 décembre 2016 sera automatiquement supprimé.</span><span class="sxs-lookup"><span data-stu-id="b1a82-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="b1a82-113">Si vous avez besoin des informations de tâche/hello tooarchive, vous pouvez utiliser le code hello décrite dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="b1a82-113">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="b1a82-114">Considérations</span><span class="sxs-lookup"><span data-stu-id="b1a82-114">Considerations</span></span>  

<span data-ttu-id="b1a82-115">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1a82-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b1a82-116">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b1a82-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="b1a82-117">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="b1a82-117">Connect tooMedia Services</span></span>

<span data-ttu-id="b1a82-118">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b1a82-118">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="b1a82-119">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1a82-119">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b1a82-120">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="b1a82-120">You must make subsequent calls toohello new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="b1a82-121">Ajout d’entités</span><span class="sxs-lookup"><span data-stu-id="b1a82-121">Adding entities</span></span>
<span data-ttu-id="b1a82-122">Chaque entité dans Media Services est ajoutée tooan jeu d’entités, telles que des ressources, via une requête HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="b1a82-122">Every entity in Media Services is added tooan entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="b1a82-123">Hello suivant montre l’exemple de comment toocreate une stratégie d’accès.</span><span class="sxs-lookup"><span data-stu-id="b1a82-123">hello following example shows how toocreate an AccessPolicy.</span></span>

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

## <a name="querying-entities"></a><span data-ttu-id="b1a82-124">Exécution d’une requête sur les entités</span><span class="sxs-lookup"><span data-stu-id="b1a82-124">Querying entities</span></span>
<span data-ttu-id="b1a82-125">La procédure d’interrogation et d’énumération des entités est simple et ne nécessite qu’une requête HTTP GET et les opérations OData facultatives.</span><span class="sxs-lookup"><span data-stu-id="b1a82-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="b1a82-126">Hello exemple suivant récupère une liste de toutes les entités MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="b1a82-126">hello following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="b1a82-127">Vous pouvez également récupérer une entité spécifique ou tous les jeux d’entités associés à une entité spécifique, tel que Bonjour exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b1a82-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in hello following examples:</span></span>

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

<span data-ttu-id="b1a82-128">Hello exemple ci-dessous retourne uniquement les propriétés d’état hello de tous les travaux.</span><span class="sxs-lookup"><span data-stu-id="b1a82-128">hello following example returns only hello State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="b1a82-129">Hello exemple suivant retourne tous les JobTemplates avec le nom hello « SampleTemplate ».</span><span class="sxs-lookup"><span data-stu-id="b1a82-129">hello following example returns all JobTemplates with hello name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="b1a82-130">Hello $développez opération n'est pas pris en charge dans Media Services ainsi que hello des méthodes LINQ non prises en charge décrites dans les considérations de LINQ (WCF Data Services).</span><span class="sxs-lookup"><span data-stu-id="b1a82-130">hello $expand operation is not supported in Media Services as well as hello unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="b1a82-131">Énumérer les grandes collections d'entités</span><span class="sxs-lookup"><span data-stu-id="b1a82-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="b1a82-132">Lors de l’interrogation des entités, il existe une limite de 1000 entités retournées à la fois, car il est public reste v2 limite les résultats de too1000 de résultats de requête.</span><span class="sxs-lookup"><span data-stu-id="b1a82-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="b1a82-133">Utilisez **ignorer** et **haut** tooenumerate via hello grande collection d’entités.</span><span class="sxs-lookup"><span data-stu-id="b1a82-133">Use **skip** and **top** tooenumerate through hello large collection of entities.</span></span> 

<span data-ttu-id="b1a82-134">Hello suivant montre l’exemple de comment toouse **ignorer** et **haut** tooskip hello travaux tout d’abord 2000 et get hello ensuite 1 000 travaux.</span><span class="sxs-lookup"><span data-stu-id="b1a82-134">hello following example shows how toouse **skip** and **top** tooskip hello first 2000 jobs and get hello next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="b1a82-135">Mise à jour des entités</span><span class="sxs-lookup"><span data-stu-id="b1a82-135">Updating entities</span></span>
<span data-ttu-id="b1a82-136">Selon le type d’entité hello et état hello qu’il est, vous pouvez mettre à jour les propriétés sur cette entité via un correctif logiciel, des demandes PUT ou HTTP MERGE.</span><span class="sxs-lookup"><span data-stu-id="b1a82-136">Depending on hello entity type and hello state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="b1a82-137">Pour plus d’informations sur ces opérations, consultez [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1a82-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="b1a82-138">Hello, exemple de code suivant montre comment tooupdate hello la propriété de nom sur une entité Asset.</span><span class="sxs-lookup"><span data-stu-id="b1a82-138">hello following code example shows how tooupdate hello Name property on an Asset entity.</span></span>

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

## <a name="deleting-entities"></a><span data-ttu-id="b1a82-139">Suppression des entités</span><span class="sxs-lookup"><span data-stu-id="b1a82-139">Deleting entities</span></span>
<span data-ttu-id="b1a82-140">Les entités peuvent être supprimées dans Media Services à l’aide d’une requête HTTP DELETE.</span><span class="sxs-lookup"><span data-stu-id="b1a82-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="b1a82-141">En fonction de l’entité de hello, la commande hello supprimer des entités peut être important.</span><span class="sxs-lookup"><span data-stu-id="b1a82-141">Depending on hello entity, hello order in which you delete entities may be important.</span></span> <span data-ttu-id="b1a82-142">Par exemple, entités, telles que des ressources exigent révoquer (ou de supprimer) tous les localisateurs qui font référence à cet élément multimédia particulier avant de supprimer hello actif.</span><span class="sxs-lookup"><span data-stu-id="b1a82-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting hello Asset.</span></span>

<span data-ttu-id="b1a82-143">Hello suivant montre l’exemple de comment toodelete un localisateur qui a été utilisé tooupload un fichier dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="b1a82-143">hello following example shows how toodelete a Locator that was used tooupload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="b1a82-144">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="b1a82-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b1a82-145">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="b1a82-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

