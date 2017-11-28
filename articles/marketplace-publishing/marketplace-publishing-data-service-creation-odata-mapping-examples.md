---
title: "Guide de création d’un service de données pour le Marketplace | Microsoft Docs"
description: "Instructions détaillées pour créer, certifier et déployer un service de données que d’autres peuvent acheter sur Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2ab624941fc385f14b62bb5d743927f157955845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="examples-of-mapping-an-existing-web-service-to-odata-through-csdls"></a><span data-ttu-id="4156d-103">Exemples de mappage d’un service web existant à OData via des données CSDL</span><span class="sxs-lookup"><span data-stu-id="4156d-103">Examples of mapping an existing web service to OData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4156d-104">**À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.**</span><span class="sxs-lookup"><span data-stu-id="4156d-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="4156d-105">Si vous avez une application SaaS professionnelle à publier sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="4156d-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="4156d-106">Si vous avez une application IaaS ou un service de développement à publier sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="4156d-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="4156d-107">Exemple : FunctionImport pour des données de type « Raw » (brutes) renvoyées à l’aide de « POST »</span><span class="sxs-lookup"><span data-stu-id="4156d-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="4156d-108">Utilisez des donnés POST Raw pour créer un subordonné et son URL (emplacement) définie par le serveur ou pour mettre à jour la partie du subordonné dans l’URL définie par le serveur.</span><span class="sxs-lookup"><span data-stu-id="4156d-108">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="4156d-109">Où le subordonné est un flux, par exemple</span><span class="sxs-lookup"><span data-stu-id="4156d-109">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="4156d-110">non structuré, notamment</span><span class="sxs-lookup"><span data-stu-id="4156d-110">unstructured, ex.</span></span> <span data-ttu-id="4156d-111">un fichier texte.</span><span class="sxs-lookup"><span data-stu-id="4156d-111">a text file.</span></span>  <span data-ttu-id="4156d-112">Prenez garde que POST ne soit pas idempotent sans emplacement.</span><span class="sxs-lookup"><span data-stu-id="4156d-112">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="4156d-113">Exemple : FunctionImport utilisant « DELETE »</span><span class="sxs-lookup"><span data-stu-id="4156d-113">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="4156d-114">Utilisez DELETE pour supprimer un URI spécifié.</span><span class="sxs-lookup"><span data-stu-id="4156d-114">Use DELETE to remove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="4156d-115">Exemple : FunctionImport utilisant « POST »</span><span class="sxs-lookup"><span data-stu-id="4156d-115">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="4156d-116">Utilisez des donnés POST Raw pour créer un subordonné et son URL (emplacement) définie par le serveur ou pour mettre à jour la partie du subordonné dans l’URL définie par le serveur.</span><span class="sxs-lookup"><span data-stu-id="4156d-116">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="4156d-117">Où le subordonné est une structure.</span><span class="sxs-lookup"><span data-stu-id="4156d-117">Where the subordinate is a structure.</span></span> <span data-ttu-id="4156d-118">Prenez garde que POST ne soit pas sans emplacement.</span><span class="sxs-lookup"><span data-stu-id="4156d-118">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="4156d-119">Exemple : FunctionImport utilisant « PUT »</span><span class="sxs-lookup"><span data-stu-id="4156d-119">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="4156d-120">Utilisez PUT pour créer un subordonné ou mettre à jour la totalité du subordonné entière à une URL défini par le serveur.</span><span class="sxs-lookup"><span data-stu-id="4156d-120">Use PUT to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="4156d-121">Où le subordonné est une structure, PUT est idempotent. Vous obtiendrez donc plusieurs occurrences dans le même état,</span><span class="sxs-lookup"><span data-stu-id="4156d-121">Where the subordinate is a structure, PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="4156d-122">à savoir x=5.</span><span class="sxs-lookup"><span data-stu-id="4156d-122">x=5.</span></span>  <span data-ttu-id="4156d-123">PUT doit être utilisé avec la totalité du contenu de la ressource spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4156d-123">Put should be used with the full content of the specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="4156d-124">Exemple : FunctionImport pour des données de type « Raw » (brutes) renvoyées à l’aide de « PUT »</span><span class="sxs-lookup"><span data-stu-id="4156d-124">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="4156d-125">Utilisez des données PUT Raw pour créer un subordonné ou mettre à jour la totalité du subordonné entière à une URL défini par le serveur.</span><span class="sxs-lookup"><span data-stu-id="4156d-125">Use PUT Raw data to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="4156d-126">Où le subordonné est un flux, par exemple</span><span class="sxs-lookup"><span data-stu-id="4156d-126">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="4156d-127">non structuré, notamment</span><span class="sxs-lookup"><span data-stu-id="4156d-127">unstructured, ex.</span></span> <span data-ttu-id="4156d-128">un fichier texte.</span><span class="sxs-lookup"><span data-stu-id="4156d-128">a text file.</span></span>  <span data-ttu-id="4156d-129">Où le subordonné est une structure, PUT est idempotent. Vous obtiendrez donc plusieurs occurrences dans le même état ;</span><span class="sxs-lookup"><span data-stu-id="4156d-129">PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="4156d-130">par exemple, x=5.</span><span class="sxs-lookup"><span data-stu-id="4156d-130">x=5.</span></span>  <span data-ttu-id="4156d-131">PUT doit être utilisé avec la totalité du contenu de la ressource spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4156d-131">Put should be used with the full content of the specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="4156d-132">Exemple : FunctionImport pour des données de type « Raw » (brutes) renvoyées à l’aide de « GET »</span><span class="sxs-lookup"><span data-stu-id="4156d-132">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="4156d-133">Utilisez des données GET Raw pour renvoyer un subordonné qui n’est pas structuré ; par exemple, du texte.</span><span class="sxs-lookup"><span data-stu-id="4156d-133">Use GET Raw data to return a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="4156d-134">Exemple : FunctionImport pour « Paging » via des données renvoyées</span><span class="sxs-lookup"><span data-stu-id="4156d-134">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="4156d-135">Utilisez la pagination RESTful d’implémentation via vos données avec GET.</span><span class="sxs-lookup"><span data-stu-id="4156d-135">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="4156d-136">La pagination par défaut est définie sur 100 lignes par page de données.</span><span class="sxs-lookup"><span data-stu-id="4156d-136">Default paging is set to 100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="4156d-137">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4156d-137">See Also</span></span>
* <span data-ttu-id="4156d-138">Si vous souhaitez comprendre le processus de mappage OData global et son rôle, lisez l’article [Mappage du service de données OData](marketplace-publishing-data-service-creation-odata-mapping.md) pour passer en revue des définitions, des structures et des instructions.</span><span class="sxs-lookup"><span data-stu-id="4156d-138">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="4156d-139">Si vous souhaitez découvrir et comprendre les nœuds spécifiques et leurs paramètres, lisez l’article [Nœuds de mappage du service de données OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) pour obtenir des définitions et des explications, des exemples, ainsi qu’un contexte de cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4156d-139">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="4156d-140">Pour retourner au chemin indiqué pour la publication d’un service de données sur Azure Marketplace, lisez l’article [Guide de publication de services de données](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="4156d-140">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

