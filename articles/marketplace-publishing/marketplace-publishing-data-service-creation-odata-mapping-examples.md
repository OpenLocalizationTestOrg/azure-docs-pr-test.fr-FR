---
title: "aaaGuide toocreating un Service de données pour hello Marketplace | Documents Microsoft"
description: "Comment toocreate, certifier et déployer un Service de données pour obtenir des instructions détaillées d’achat sur hello Azure Marketplace."
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
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a><span data-ttu-id="4c27f-103">Exemples de mappage existant web tooOData service via CSDLs</span><span class="sxs-lookup"><span data-stu-id="4c27f-103">Examples of mapping an existing web service tooOData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4c27f-104">**À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.**</span><span class="sxs-lookup"><span data-stu-id="4c27f-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="4c27f-105">Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="4c27f-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="4c27f-106">Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="4c27f-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="4c27f-107">Exemple : FunctionImport pour des données de type « Raw » (brutes) renvoyées à l’aide de « POST »</span><span class="sxs-lookup"><span data-stu-id="4c27f-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="4c27f-108">Utiliser toocreate de données brutes de valider un subordonné de nouveau et son serveur URL(location) ou tooupdate partie hello secondaire sur le serveur de hello définie par l’URL de retour.</span><span class="sxs-lookup"><span data-stu-id="4c27f-108">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="4c27f-109">Où hello subordonné est un flux de données, c'est-à-dire non structurée, par ex.</span><span class="sxs-lookup"><span data-stu-id="4c27f-109">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="4c27f-110">un fichier texte.</span><span class="sxs-lookup"><span data-stu-id="4c27f-110">a text file.</span></span>  <span data-ttu-id="4c27f-111">Prenez garde que POST ne soit pas idempotent sans emplacement.</span><span class="sxs-lookup"><span data-stu-id="4c27f-111">Beware POST in not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="4c27f-112">Exemple : FunctionImport utilisant « DELETE »</span><span class="sxs-lookup"><span data-stu-id="4c27f-112">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="4c27f-113">Utilisez supprimer tooremove un URI spécifié.</span><span class="sxs-lookup"><span data-stu-id="4c27f-113">Use DELETE tooremove a specified URI.</span></span>

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

## <a name="example-functionimport-using-post"></a><span data-ttu-id="4c27f-114">Exemple : FunctionImport utilisant « POST »</span><span class="sxs-lookup"><span data-stu-id="4c27f-114">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="4c27f-115">Utiliser toocreate de données brutes de valider un subordonné de nouveau et son serveur URL(location) ou tooupdate partie hello secondaire sur le serveur de hello définie par l’URL de retour.</span><span class="sxs-lookup"><span data-stu-id="4c27f-115">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="4c27f-116">Où hello subordonné est une structure.</span><span class="sxs-lookup"><span data-stu-id="4c27f-116">Where hello subordinate is a structure.</span></span> <span data-ttu-id="4c27f-117">Prenez garde que POST ne soit pas sans emplacement.</span><span class="sxs-lookup"><span data-stu-id="4c27f-117">Beware POST is not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-put"></a><span data-ttu-id="4c27f-118">Exemple : FunctionImport utilisant « PUT »</span><span class="sxs-lookup"><span data-stu-id="4c27f-118">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="4c27f-119">Utilisez PUT toocreate subordonné nouveau ou subordonné entière de hello tooupdate sur un serveur défini par l’URL.</span><span class="sxs-lookup"><span data-stu-id="4c27f-119">Use PUT toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="4c27f-120">Hello subordonné est une structure, PUT est idempotente plusieurs occurrences aboutira alors à hello même état, c'est-à-dire</span><span class="sxs-lookup"><span data-stu-id="4c27f-120">Where hello subordinate is a structure, PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="4c27f-121">par exemple, x=5.</span><span class="sxs-lookup"><span data-stu-id="4c27f-121">x=5.</span></span>  <span data-ttu-id="4c27f-122">Put doit être utilisé avec hello contenu complètes de hello spécifié ressource.</span><span class="sxs-lookup"><span data-stu-id="4c27f-122">Put should be used with hello full content of hello specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="4c27f-123">Exemple : FunctionImport pour des données de type « Raw » (brutes) renvoyées à l’aide de « PUT »</span><span class="sxs-lookup"><span data-stu-id="4c27f-123">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="4c27f-124">Utilisez PUT brutes toocreate données subordonné nouveau ou subordonné entière de hello tooupdate à une URL de serveur défini.</span><span class="sxs-lookup"><span data-stu-id="4c27f-124">Use PUT Raw data toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="4c27f-125">Où hello subordonné est un flux de données, c'est-à-dire non structurée, par ex.</span><span class="sxs-lookup"><span data-stu-id="4c27f-125">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="4c27f-126">un fichier texte.</span><span class="sxs-lookup"><span data-stu-id="4c27f-126">a text file.</span></span>  <span data-ttu-id="4c27f-127">PUT est idempotente plusieurs occurrences aboutira alors à hello même état, c'est-à-dire</span><span class="sxs-lookup"><span data-stu-id="4c27f-127">PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="4c27f-128">par exemple, x=5.</span><span class="sxs-lookup"><span data-stu-id="4c27f-128">x=5.</span></span>  <span data-ttu-id="4c27f-129">Put doit être utilisé avec hello contenu complètes de hello spécifié ressource.</span><span class="sxs-lookup"><span data-stu-id="4c27f-129">Put should be used with hello full content of hello specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="4c27f-130">Exemple : FunctionImport pour des données de type « Raw » (brutes) renvoyées à l’aide de « GET »</span><span class="sxs-lookup"><span data-stu-id="4c27f-130">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="4c27f-131">Utilisez obtenir brutes données tooreturn subordonné qui n’est pas structuré, par exemple, le texte.</span><span class="sxs-lookup"><span data-stu-id="4c27f-131">Use GET Raw data tooreturn a subordinate that is unstructured, i.e. text.</span></span>

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

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="4c27f-132">Exemple : FunctionImport pour « Paging » via des données renvoyées</span><span class="sxs-lookup"><span data-stu-id="4c27f-132">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="4c27f-133">Utilisez la pagination RESTful d’implémentation via vos données avec GET.</span><span class="sxs-lookup"><span data-stu-id="4c27f-133">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="4c27f-134">Pagination par défaut est définie de ligne too100 par page de données.</span><span class="sxs-lookup"><span data-stu-id="4c27f-134">Default paging is set too100 row per page of data.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="4c27f-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4c27f-135">See Also</span></span>
* <span data-ttu-id="4c27f-136">Si vous êtes intéressé par le fonctionnement hello le processus de mappage global OData et leur objectif, lisez cet article [mappage du Service de données OData](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview définitions, des structures et des instructions.</span><span class="sxs-lookup"><span data-stu-id="4c27f-136">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="4c27f-137">Si vous êtes intéressé par apprentissage et comprendre les nœuds spécifiques hello et leurs paramètres, lisez cet article [nœuds de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) pour les définitions et des explications, des exemples et contexte de cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4c27f-137">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="4c27f-138">toohello tooreturn prescrit le chemin d’accès pour la publication d’un Service de données de toohello Azure Marketplace, lisez cet article [Guide de publication de Service de données](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="4c27f-138">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

