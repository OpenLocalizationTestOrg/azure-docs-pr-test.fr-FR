---
title: "aaaGuide toocreating un Service de données pour hello Marketplace | Documents Microsoft"
description: "Comment toocreate, certifier et déployer un Service de données pour obtenir des instructions détaillées d’achat sur hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a><span data-ttu-id="a0cd3-103">Mappage d’un tooOData de service web existant via CSDL</span><span class="sxs-lookup"><span data-stu-id="a0cd3-103">Mapping an existing web service tooOData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a0cd3-104">**À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.**</span><span class="sxs-lookup"><span data-stu-id="a0cd3-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="a0cd3-105">Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="a0cd3-106">Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="a0cd3-107">Cet article donne une vue d’ensemble sur la façon de toouse un toomap CSDL un tooan de service service compatible OData existante.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-107">This article gives an overview on how toouse a CSDL toomap an existing service tooan OData compatible service.</span></span> <span data-ttu-id="a0cd3-108">Il explique comment toocreate hello document de mappage (CSDL) qui transforme la demande d’entrée hello client de hello via un appel de service et un hello sortie client de toohello (données) via un flux compatible OData.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-108">It explains how toocreate hello mapping document (CSDL) that transforms hello input request from hello client via a service call and hello output (data) back toohello client via an OData compatible feed.</span></span> <span data-ttu-id="a0cd3-109">Microsoft Azure Marketplace expose les utilisateurs finaux toohello de services à l’aide du protocole OData de hello.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-109">Microsoft’s Azure Marketplace exposes services toohello end-users by using hello OData protocol.</span></span> <span data-ttu-id="a0cd3-110">L’exposition des services par les fournisseurs de contenu (les propriétaires de données) s’effectue sous diverses formes, telles que REST, SOAP, etc.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="a0cd3-111">Qu’est un langage CSDL et sa structure ?</span><span class="sxs-lookup"><span data-stu-id="a0cd3-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="a0cd3-112">Un langage CSDL (Conceptual Schema Definition Language) est une spécification définissant comment toodescribe web service ou une base de données de service en commun XML est affecté toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span>

<span data-ttu-id="a0cd3-113">Vue d’ensemble simple de hello **flux de demande :**</span><span class="sxs-lookup"><span data-stu-id="a0cd3-113">Simple overview of hello **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="a0cd3-114">Hello **flux de données** est Bonjour opposé direction :</span><span class="sxs-lookup"><span data-stu-id="a0cd3-114">hello **data flow** is in hello opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="a0cd3-115">**Figure 1** diagrammes comment un client serait obtenir des données à partir d’un fournisseur de contenu (votre service) en accédant via hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through hello Azure Marketplace.</span></span>  <span data-ttu-id="a0cd3-116">Hello CSDL est utilisé à la demande de hello mappage/la Transformation composant toohandle hello et passer des données entre hello demande du client et des services du fournisseur de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-116">hello CSDL is used by hello Mapping/Transformation component toohandle hello request and data pass between hello content provider’s service(s) and hello requesting client.</span></span>

<span data-ttu-id="a0cd3-117">*Figure 1 : Le flux détaillé émanant du fournisseur de toocontent client via Azure Marketplace*</span><span class="sxs-lookup"><span data-stu-id="a0cd3-117">*Figure 1: Detailed flow from requesting client toocontent provider via Azure Marketplace*</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="a0cd3-119">Pour plus d’informations sur le protocole OData de hello lors de quelle version des extensions Azure Marketplace hello Atom et Atom Pub, passez en revue : [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-119">For background on Atom, Atom Pub, and hello OData protocol upon which hello Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="a0cd3-120">Extrait supérieure lien : *« hello hello Open Data protocol (OData visés ci-après tooas) vise protocole tooprovide basé sur un REST pour les opérations CRUD-style (création, lecture, mise à jour et suppression) sur les ressources exposées en tant que services de données. Un « service de données » est un point de terminaison où des données sont exposées à partir d’une ou de plusieurs « collections », chacune comportant zéro « entrées » ou plus, qui consistent en des paires nom-valeur typées. OData est publié par Microsoft sous les Standards OASIS (Organization for hello for the Advancement of Structured Information Standards) afin que toute personne qui souhaite toocan générer des serveurs, des clients ou des outils sans les droits d’auteur ou restrictions. »*</span><span class="sxs-lookup"><span data-stu-id="a0cd3-120">Excerpt from above link: *“hello purpose of hello Open Data protocol (hereafter referred tooas OData) is tooprovide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for hello Advancement of Structured Information Standards) Standards so that anyone that wants toocan build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a><span data-ttu-id="a0cd3-121">Trois éléments critiques qui ont toobe défini par hello CSDL sont :</span><span class="sxs-lookup"><span data-stu-id="a0cd3-121">Three Critical Pieces that have toobe defined by hello CSDL are:</span></span>
* <span data-ttu-id="a0cd3-122">Hello **point de terminaison** de fournisseur de services de hello hello Web adresse (URI) de hello Service</span><span class="sxs-lookup"><span data-stu-id="a0cd3-122">hello **endpoint** of hello Service Provider hello Web Address (URI) of hello Service</span></span>
* <span data-ttu-id="a0cd3-123">Hello **des paramètres de données** passé en tant que fournisseur de services de toohello d’entrée des définitions de hello des paramètres de hello envoyés service du fournisseur de contenu toohello toohello les type de données.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-123">hello **data parameters** being passed as input toohello Service Provider hello definitions of hello parameters being sent toohello Content Provider’s service down toohello data type.</span></span>
* <span data-ttu-id="a0cd3-124">**Schéma** de schéma de hello toohello demandant un Service de données hello remises en service du fournisseur de contenu hello de renvoi des données hello, y compris les types de conteneur, les collections et les tables, les variables ou des colonnes et les données.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-124">**Schema** of hello data being returned toohello Requesting Service hello schema of hello data being delivered by hello Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="a0cd3-125">Hello suivant schéma montre une vue d’ensemble du flux de hello d’où client de hello entre hello OData instruction (service web de l’appel toohello du fournisseur du contenu) toogetting hello résultats/stockage des données.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-125">hello following diagram shows an overview of hello flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back.</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="a0cd3-127">Étapes :</span><span class="sxs-lookup"><span data-stu-id="a0cd3-127">Steps:</span></span>
1. <span data-ttu-id="a0cd3-128">Client envoie la demande via l’appel de Service terminée avec des paramètres d’entrée définis dans XML toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a0cd3-128">Client sends request via Service call complete with Input Parameters defined in XML toohello Azure Marketplace</span></span>
2. <span data-ttu-id="a0cd3-129">CSDL est utilisé toovalidate hello appel de Service.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-129">CSDL is used toovalidate hello Service call.</span></span>
   * <span data-ttu-id="a0cd3-130">Hello mis en forme un appel de Service est ensuite envoyé toohello Service de fournisseurs de contenu en hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a0cd3-130">hello Formatted Service Call is then sent toohello Content Providers Service by hello Azure Marketplace</span></span>
3. <span data-ttu-id="a0cd3-131">exécute Hello Webservice et valide l’action hello Hello verbe Http (c'est-à-dire GET) les données de salutation sont retournées tooAzure Marketplace où hello demande des données (le cas échéant) est présente dans un Format XML toohello Client à l’aide de hello mappage défini dans hello CSDL.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-131">hello Webservice executes and preforms hello action of hello Http Verb (i.e. GET) hello data is returned tooAzure Marketplace where hello requested data (if any) is exposes in XML Format toohello Client using hello Mapping defined in hello CSDL.</span></span>
4. <span data-ttu-id="a0cd3-132">Hello Client reçoit les données de salutation (le cas échéant) au format XML ou JSON</span><span class="sxs-lookup"><span data-stu-id="a0cd3-132">hello Client is sent hello data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="a0cd3-133">Définitions</span><span class="sxs-lookup"><span data-stu-id="a0cd3-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="a0cd3-134">ATOM Pub OData</span><span class="sxs-lookup"><span data-stu-id="a0cd3-134">OData ATOM pub</span></span>
<span data-ttu-id="a0cd3-135">ATOM pub d’un toohello extension où chaque entrée représente une ligne d’un résultat défini.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-135">An extension toohello ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="a0cd3-136">Hello contenu partie entrée de hello est toocontain améliorée des valeurs de hello de ligne de hello – en tant que paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-136">hello content part of hello entry is enhanced toocontain hello values of hello row – as key value pairs.</span></span> <span data-ttu-id="a0cd3-137">Vous trouverez des informations supplémentaires ici : [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="a0cd3-138">CSDL (Conceptual Schema Definition Language)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="a0cd3-139">Permet de définir des fonctions (SPROC) et des entités qui sont exposées via une base de données.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="a0cd3-140">Vous trouverez des informations supplémentaires ici : [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="a0cd3-141">Cliquez sur hello **autres versions** liste déroulante et sélectionnez une version, si vous ne voyez pas l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-141">Click hello **other versions** dropdown and select a version if you don’t see hello article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="a0cd3-142">EDM (Entry Data Model)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="a0cd3-143">Vue d’ensemble : [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="a0cd3-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="a0cd3-144">Aperçu : [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="a0cd3-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="a0cd3-145">Types de données : [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="a0cd3-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="a0cd3-146">Hello Voici hello détaillé tooRight gauche d’où client de hello entre hello OData instruction (service web de l’appel toohello du fournisseur du contenu) toogetting hello résultats/stockage des données :</span><span class="sxs-lookup"><span data-stu-id="a0cd3-146">hello following shows hello detailed Left tooRight flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back:</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="a0cd3-148">Concepts de base du langage CSDL</span><span class="sxs-lookup"><span data-stu-id="a0cd3-148">CSDL Basics</span></span>
<span data-ttu-id="a0cd3-149">Un langage CSDL (Conceptual Schema Definition Language) est une spécification définissant comment toodescribe web service ou une base de données de service en commun XML est affecté toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span> <span data-ttu-id="a0cd3-150">Décrit les CSDL hello critiques pièces qui **permet la transmission hello de données à partir de la Source de données de hello toohello Azure Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="a0cd3-150">CSDL describes hello critical pieces that **makes hello passing of data from hello Data Source toohello Azure Marketplace possible.**</span></span> <span data-ttu-id="a0cd3-151">les parties principales Hello sont décrits ici :</span><span class="sxs-lookup"><span data-stu-id="a0cd3-151">hello main pieces are described here:</span></span>

* <span data-ttu-id="a0cd3-152">Des informations d’interface qui décrivent toutes les fonctions disponibles publiquement (nœud FunctionImport)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="a0cd3-153">Des informations de type de données pour toutes les requêtes de messages (entrée) et réponses aux messages (sorties) (nœuds EntityContainer/EntitySet/EntityType)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="a0cd3-154">Informations sur les toobe de protocole de transport hello de liaison utilisé (en-tête de nœud)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-154">Binding information about hello transport protocol toobe used (Header Node)</span></span>
* <span data-ttu-id="a0cd3-155">Informations d’adresse pour la localisation hello spécifié service (attribut BaseURI)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-155">Address information for locating hello specified service (BaseURI attribute)</span></span>

<span data-ttu-id="a0cd3-156">En bref, hello CSDL représente un contrat de plateforme - et indépendants du langage entre le demandeur de service hello et fournisseur de services hello.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-156">In a nutshell, hello CSDL represents a platform- and language-independent contract between hello service requestor and hello service provider.</span></span> <span data-ttu-id="a0cd3-157">À l’aide de hello CSDL, un client peut localiser un service de base de données de service/web et appeler ses fonctions publiquement disponibles.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-157">Using hello CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a><span data-ttu-id="a0cd3-158">Concernant une base de données de tooa CSDL ou d’une Collection</span><span class="sxs-lookup"><span data-stu-id="a0cd3-158">Relating a CSDL tooa Database or a Collection</span></span>
<span data-ttu-id="a0cd3-159">**Hello spécification CSDL**</span><span class="sxs-lookup"><span data-stu-id="a0cd3-159">**hello CSDL Specification**</span></span>

<span data-ttu-id="a0cd3-160">CSDL est une grammaire XML utilisée pour décrire un service web.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="a0cd3-161">spécification de Hello proprement dite est divisée en 4 éléments principaux : EntitySet, FunctionImport ; Espace de noms et EntityType.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-161">hello specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="a0cd3-162">toomake cette toounderstand plus facile d’abstraction permet de lier une table de tooa CSDL.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-162">toomake this abstraction easier toounderstand lets relate a CSDL tooa table.</span></span>

<span data-ttu-id="a0cd3-163">N’oubliez pas les points suivants :</span><span class="sxs-lookup"><span data-stu-id="a0cd3-163">Remember;</span></span>

  <span data-ttu-id="a0cd3-164">CSDL représente un contrat de plateforme - et indépendants du langage entre hello **demandeur de service** et hello **fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-164">CSDL represents a platform- and language-independent contract between hello **service requestor** and hello **service provider**.</span></span> <span data-ttu-id="a0cd3-165">Le langage CSDL permet à un **client** de localiser un **service web/service de base de données** et d’appeler n’importe laquelle de ses **fonctions** disponibles publiquement.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="a0cd3-166">Un Bonjour du Service de données pour les quatre parties d’un langage CSDL peuvent être considérés en termes de base de données, de Table, d’une colonne et d’une procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-166">For a Data Service hello four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="a0cd3-167">Mise en relation de ces éléments comme suit pour un service de données :</span><span class="sxs-lookup"><span data-stu-id="a0cd3-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="a0cd3-168">EntityContainer ~= Base de données</span><span class="sxs-lookup"><span data-stu-id="a0cd3-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="a0cd3-169">EntitySet ~= Table</span><span class="sxs-lookup"><span data-stu-id="a0cd3-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="a0cd3-170">EntityType ~= Colonnes</span><span class="sxs-lookup"><span data-stu-id="a0cd3-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="a0cd3-171">FunctionImport ~= Procédure stockée</span><span class="sxs-lookup"><span data-stu-id="a0cd3-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="a0cd3-172">**Verbes HTTP autorisés**</span><span class="sxs-lookup"><span data-stu-id="a0cd3-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="a0cd3-173">GET-renvoie les valeurs à partir de la base de données hello (retourne une Collection)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-173">GET – returns values from hello db (returns a Collection)</span></span>
* <span data-ttu-id="a0cd3-174">VALIDER – utilisé toopass tooand facultatif retour valeurs de données de base de données hello (créer une nouvelle entrée dans la collection hello, URI d’id/retour)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-174">POST – used toopass data tooand optional return values from hello db (Create a new entry in hello collection, return id/URI)</span></span>
* <span data-ttu-id="a0cd3-175">Supprimer : supprime des données à partir de hello DB (supprime une collection)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-175">DELETE – Deletes data from hello DB (Deletes a collection)</span></span>
* <span data-ttu-id="a0cd3-176">PUT - met à jour les données dans une base de données (remplace ou crée une collection)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="a0cd3-177">Document de métadonnées/de mappage</span><span class="sxs-lookup"><span data-stu-id="a0cd3-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="a0cd3-178">document de métadonnées/mappage Hello est utilisé toomap web existant du contenu d’un fournisseur de services afin qu’il peut être exposé comme un service web OData par système d’Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-178">hello metadata/mapping document is used toomap a content provider’s existing web services so that it can be exposed as an OData web service by hello Azure Marketplace system.</span></span> <span data-ttu-id="a0cd3-179">Il est basé sur le langage CSDL et implémente quelques extensions tooCSDL tooaccommodate hello aux besoins de REST en fonction des services web exposés via Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-179">It is based on CSDL and implements a few extensions tooCSDL tooaccommodate hello needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="a0cd3-180">extensions de Hello sont trouvent dans hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) espace de noms.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-180">hello extensions are found in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="a0cd3-181">Voici un exemple de hello CSDL : (copier et coller hello exemple CSDL dans un éditeur XML ci-dessous et modifiez toomatch votre Service.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-181">An example of hello CSDL follows:  (Copy and paste hello below example CSDL into an XML editor and change toomatch your Service.</span></span>  <span data-ttu-id="a0cd3-182">Puis collez dans CSDL mappage sous l’onglet de DataService lors de la création de votre service Bonjour [portail de publication Azure Marketplace](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-182">Then paste into CSDL Mapping under DataService tab when creating your service in hello  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="a0cd3-183">**Termes du contrat :** toohello des termes du contrat relatif hello CSDL [portail de publication](https://publish.windowsazure.com) les termes du contrat de l’interface utilisateur (PPUI).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-183">**Terms:** Relating hello CSDL terms toohello [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="a0cd3-184">Offrent « Title » Bonjour PPUI rapporte tooMyWebOffer</span><span class="sxs-lookup"><span data-stu-id="a0cd3-184">Offer “Title” in hello PPUI relates tooMyWebOffer</span></span>
* <span data-ttu-id="a0cd3-185">MyCompany Bonjour PPUI se rapporte trop**nom de l’éditeur** Bonjour [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="a0cd3-185">MyCompany in hello PPUI relates too**Publisher Display Name** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="a0cd3-186">Votre API rapporte tooa Web ou un Service de données (il s’agit d’un Plan Bonjour PPUI)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-186">Your API relates tooa Web or Data Service (a Plan in hello PPUI)</span></span>

<span data-ttu-id="a0cd3-187">**Hiérarchie :** une entreprise (fournisseur de contenu) possède une ou plusieurs offres qui comprennent des plans, c’est-à-dire des services, qui sont associés à une API.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="a0cd3-188">Exemple de service web CSDL</span><span class="sxs-lookup"><span data-stu-id="a0cd3-188">WebService CSDL Example</span></span>
<span data-ttu-id="a0cd3-189">Se connecte tooa service qui expose un point de terminaison web application (par exemple, une application c#)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-189">Connects tooa service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> <span data-ttu-id="a0cd3-190">Afficher plus d’exemples de Service Web de CSDL dans l’article de hello [exemples de mappage existant web tooOData service via CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-190">View more CSDL Web Service examples in hello article [Examples of mapping an existing web service tooOData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="a0cd3-191">Exemple de service de données CSDL</span><span class="sxs-lookup"><span data-stu-id="a0cd3-191">DataService CSDL Example</span></span>
<span data-ttu-id="a0cd3-192">Se connecte tooa service qui expose une table de base de données ou une vue comme un point de terminaison exemple ci-dessous montre deux Qu'api pour la base de données en fonction de CSDL API (il peut utiliser des vues plutôt que des tables).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-192">Connects tooa service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a><span data-ttu-id="a0cd3-193">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a0cd3-193">See Also</span></span>
* <span data-ttu-id="a0cd3-194">Si vous êtes intéressé par apprentissage et comprendre les nœuds spécifiques hello et leurs paramètres, lisez cet article [nœuds de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) pour les définitions et des explications, des exemples et contexte de cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-194">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="a0cd3-195">Si vous souhaitez parcourir les exemples, consultez cet article [exemples de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee exemple de code et comprendre la syntaxe du code et du contexte.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="a0cd3-196">toohello tooreturn prescrit le chemin d’accès pour la publication d’un Service de données de toohello Azure Marketplace, lisez cet article [Guide de publication de Service de données](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-196">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

