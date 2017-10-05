---
title: "Guide de création d’un service de données pour le Marketplace | Microsoft Docs"
description: "Instructions détaillées pour créer, certifier et déployer un service de données que d’autres peuvent acheter sur Azure Marketplace."
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
ms.openlocfilehash: a853b4dbd1952ba4ea8ee68ea3ca98f588bb71a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="mapping-an-existing-web-service-to-odata-through-csdl"></a><span data-ttu-id="4e9fe-103">Mappage d’un service web existant à OData via des le langage CSDL</span><span class="sxs-lookup"><span data-stu-id="4e9fe-103">Mapping an existing web service to OData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4e9fe-104">**À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.**</span><span class="sxs-lookup"><span data-stu-id="4e9fe-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="4e9fe-105">Si vous avez une application SaaS professionnelle à publier sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="4e9fe-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="4e9fe-106">Si vous avez une application IaaS ou un service de développement à publier sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="4e9fe-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="4e9fe-107">Cet article offre une vue d’ensemble de l’utilisation d’un langage CSDL pour mapper un service existant à un service compatible OData.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-107">This article gives an overview on how to use a CSDL to map an existing service to an OData compatible service.</span></span> <span data-ttu-id="4e9fe-108">Il explique comment créer le document de mappage (CSDL) qui transforme la requête d’entrée provenant du client via un appel de service et la sortie (données) renvoyée au client via un flux compatible OData.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-108">It explains how to create the mapping document (CSDL) that transforms the input request from the client via a service call and the output (data) back to the client via an OData compatible feed.</span></span> <span data-ttu-id="4e9fe-109">Microsoft Azure Marketplace utilise le protocole OData pour exposer des services aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-109">Microsoft’s Azure Marketplace exposes services to the end-users by using the OData protocol.</span></span> <span data-ttu-id="4e9fe-110">L’exposition des services par les fournisseurs de contenu (les propriétaires de données) s’effectue sous diverses formes, telles que REST, SOAP, etc.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="4e9fe-111">Qu’est un langage CSDL et sa structure ?</span><span class="sxs-lookup"><span data-stu-id="4e9fe-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="4e9fe-112">Un langage CSDL (Conceptual Schema Definition Language) est une spécification définissant la façon de décrire un service web ou un service de base de données dans un verbiage XML commun sur Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span>

<span data-ttu-id="4e9fe-113">Vue d’ensemble simple du **flux de requêtes :**</span><span class="sxs-lookup"><span data-stu-id="4e9fe-113">Simple overview of the **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="4e9fe-114">Le **flux de données** est dans le sens opposé :</span><span class="sxs-lookup"><span data-stu-id="4e9fe-114">The **data flow** is in the opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="4e9fe-115">**figure 1** présente un diagramme de la façon dont un client obtient des données provenant d’un fournisseur de contenu (votre service) en passant par Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through the Azure Marketplace.</span></span>  <span data-ttu-id="4e9fe-116">Le langage CSDL est utilisé par le composant de mappage/transformation pour traiter le passage de requêtes et de données entre le ou les services du fournisseur de contenu et le client demandeur.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-116">The CSDL is used by the Mapping/Transformation component to handle the request and data pass between the content provider’s service(s) and the requesting client.</span></span>

<span data-ttu-id="4e9fe-117">*Figure 1 : Flux détaillé du client demandeur vers le fournisseur de contenu via Azure Marketplace*</span><span class="sxs-lookup"><span data-stu-id="4e9fe-117">*Figure 1: Detailed flow from requesting client to content provider via Azure Marketplace*</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="4e9fe-119">Pour obtenir des informations générales sur Atom, Atom Pub et le protocole OData sur lequel reposent les extensions Azure Marketplace, consultez le site suivant : [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-119">For background on Atom, Atom Pub, and the OData protocol upon which the Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="4e9fe-120">Extrait du site ci-dessus : *« L’objectif du protocole Open Data (ci-après dénommé OData) est de fournir un protocole basé sur REST pour les opérations de style CRUD (Create, Read, Update et Delete, c’est-à-dire créer, lire, mettre à jour et supprimer) sur les ressources exposées en tant que services de données. Un « service de données » est un point de terminaison où des données sont exposées à partir d’une ou de plusieurs « collections », chacune comportant zéro « entrées » ou plus, qui consistent en des paires nom-valeur typées. OData est publié par Microsoft sous les normes OASIS (Organization for the Advancement of Structured Information Standards) afin que toute personne qui le souhaite puisse générer des serveurs, des clients ou des outils sans droits d’auteur ou restrictions. »*</span><span class="sxs-lookup"><span data-stu-id="4e9fe-120">Excerpt from above link: *“The purpose of the Open Data protocol (hereafter referred to as OData) is to provide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for the Advancement of Structured Information Standards) Standards so that anyone that wants to can build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-to-be-defined-by-the-csdl-are"></a><span data-ttu-id="4e9fe-121">Les trois éléments critiques qui doivent être définis par le langage CSDL sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="4e9fe-121">Three Critical Pieces that have to be defined by the CSDL are:</span></span>
* <span data-ttu-id="4e9fe-122">Le **point de terminaison** du service fournisseur : adresse web (URI) du service</span><span class="sxs-lookup"><span data-stu-id="4e9fe-122">The **endpoint** of the Service Provider The Web Address (URI) of the Service</span></span>
* <span data-ttu-id="4e9fe-123">Les **paramètres de données** transmis en tant qu’entrée au fournisseur de services : définitions des paramètres envoyés au service du fournisseur de contenu jusqu’au type de données.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-123">The **data parameters** being passed as input to the Service Provider The definitions of the parameters being sent to the Content Provider’s service down to the data type.</span></span>
* <span data-ttu-id="4e9fe-124">**Schéma** des données renvoyées au service demandeur : schéma des données remises par le service du fournisseur de contenu, notamment le conteneur, les collections/tables, les variables/colonnes et les types de données.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-124">**Schema** of the data being returned to the Requesting Service The schema of the data being delivered by the Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="4e9fe-125">Le diagramme suivant présente une vue d’ensemble du flux depuis lequel le client entre l’instruction OData (appel au service web du fournisseur de contenu) de récupération des résultats/données.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-125">The following diagram shows an overview of the flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back.</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="4e9fe-127">Étapes :</span><span class="sxs-lookup"><span data-stu-id="4e9fe-127">Steps:</span></span>
1. <span data-ttu-id="4e9fe-128">Le client envoie la requête via l’appel du service avec les paramètres d’entrée définis en XML sur Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4e9fe-128">Client sends request via Service call complete with Input Parameters defined in XML to the Azure Marketplace</span></span>
2. <span data-ttu-id="4e9fe-129">Le langage CSDL est utilisé pour valider l’appel du service.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-129">CSDL is used to validate the Service call.</span></span>
   * <span data-ttu-id="4e9fe-130">L’appel du service mis en forme est envoyé au service des fournisseurs de contenu par Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4e9fe-130">The Formatted Service Call is then sent to the Content Providers Service by the Azure Marketplace</span></span>
3. <span data-ttu-id="4e9fe-131">Le service web s’exécute et effectue l’action du verbe HTTP (c’est-à-dire GET). Les données sont renvoyées à Azure Marketplace où les données demandées (le cas échéant) sont exposées au format XML au client à l’aide du mappage défini dans le langage CSDL.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-131">The Webservice executes and preforms the action of the Http Verb (i.e. GET) The data is returned to Azure Marketplace where the requested data (if any) is exposes in XML Format to the Client using the Mapping defined in the CSDL.</span></span>
4. <span data-ttu-id="4e9fe-132">Le client reçoit les données (le cas échéant) au format XML ou JSON</span><span class="sxs-lookup"><span data-stu-id="4e9fe-132">The Client is sent the data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="4e9fe-133">Définitions</span><span class="sxs-lookup"><span data-stu-id="4e9fe-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="4e9fe-134">ATOM Pub OData</span><span class="sxs-lookup"><span data-stu-id="4e9fe-134">OData ATOM pub</span></span>
<span data-ttu-id="4e9fe-135">Extension du service ATOM Pub où chaque entrée représente une ligne d’un jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-135">An extension to the ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="4e9fe-136">La partie de contenu de l’entrée a été améliorée de façon à contenir les valeurs de la ligne, sous la forme de paires clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-136">The content part of the entry is enhanced to contain the values of the row – as key value pairs.</span></span> <span data-ttu-id="4e9fe-137">Vous trouverez des informations supplémentaires ici : [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="4e9fe-138">CSDL (Conceptual Schema Definition Language)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="4e9fe-139">Permet de définir des fonctions (SPROC) et des entités qui sont exposées via une base de données.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="4e9fe-140">Vous trouverez des informations supplémentaires ici : [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="4e9fe-141">Cliquez sur la liste déroulante des **autres versions** et sélectionnez une version l’article ne s’affiche pas.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-141">Click the **other versions** dropdown and select a version if you don’t see the article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="4e9fe-142">EDM (Entry Data Model)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="4e9fe-143">Vue d’ensemble : [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="4e9fe-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="4e9fe-144">Aperçu : [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="4e9fe-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="4e9fe-145">Types de données : [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="4e9fe-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="4e9fe-146">Le diagramme suivant présente un flux de gauche à droite détaillé depuis lequel le client entre l’instruction OData (appel au service web du fournisseur de contenu) de récupération des résultats/données.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-146">The following shows the detailed Left to Right flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back:</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="4e9fe-148">Concepts de base du langage CSDL</span><span class="sxs-lookup"><span data-stu-id="4e9fe-148">CSDL Basics</span></span>
<span data-ttu-id="4e9fe-149">Un langage CSDL (Conceptual Schema Definition Language) est une spécification définissant la façon de décrire un service web ou un service de base de données dans un verbiage XML commun sur Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span> <span data-ttu-id="4e9fe-150">Les données CSDL décrivent les éléments critiques qui **permettent la transmission de données à partir de la source de données à Azure Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="4e9fe-150">CSDL describes the critical pieces that **makes the passing of data from the Data Source to the Azure Marketplace possible.**</span></span> <span data-ttu-id="4e9fe-151">Les éléments principaux sont décrits ici :</span><span class="sxs-lookup"><span data-stu-id="4e9fe-151">The main pieces are described here:</span></span>

* <span data-ttu-id="4e9fe-152">Des informations d’interface qui décrivent toutes les fonctions disponibles publiquement (nœud FunctionImport)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="4e9fe-153">Des informations de type de données pour toutes les requêtes de messages (entrée) et réponses aux messages (sorties) (nœuds EntityContainer/EntitySet/EntityType)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="4e9fe-154">Des informations de liaison sur le protocole de transport à utilisé (nœud Header)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-154">Binding information about the transport protocol to be used (Header Node)</span></span>
* <span data-ttu-id="4e9fe-155">Des informations d’adresse pour localiser le service spécifié (attribut BaseURI)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-155">Address information for locating the specified service (BaseURI attribute)</span></span>

<span data-ttu-id="4e9fe-156">En résumé, le langage CSDL représente un contrat non spécifique à une plateforme et indépendant du langage entre le demandeur de services et le fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-156">In a nutshell, the CSDL represents a platform- and language-independent contract between the service requestor and the service provider.</span></span> <span data-ttu-id="4e9fe-157">Le langage CSDL permet à un client de localiser un service web/service de base de données et d’appeler n’importe laquelle de ses fonctions disponibles publiquement.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-157">Using the CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-to-a-database-or-a-collection"></a><span data-ttu-id="4e9fe-158">Mise en relation d’un langage CSDL avec une base de données ou une collection</span><span class="sxs-lookup"><span data-stu-id="4e9fe-158">Relating a CSDL to a Database or a Collection</span></span>
<span data-ttu-id="4e9fe-159">**La spécification CSDL**</span><span class="sxs-lookup"><span data-stu-id="4e9fe-159">**The CSDL Specification**</span></span>

<span data-ttu-id="4e9fe-160">CSDL est une grammaire XML utilisée pour décrire un service web.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="4e9fe-161">La spécification est elle-même divisée en 4 éléments principaux : EntitySet, FunctionImport, NameSpace et EntityType.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-161">The specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="4e9fe-162">Pour rendre cette abstraction plus facile à comprendre, associons un CSDL à une table.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-162">To make this abstraction easier to understand lets relate a CSDL to a table.</span></span>

<span data-ttu-id="4e9fe-163">N’oubliez pas les points suivants :</span><span class="sxs-lookup"><span data-stu-id="4e9fe-163">Remember;</span></span>

  <span data-ttu-id="4e9fe-164">Le langage CSDL représente un contrat non spécifique à une plateforme et indépendant du langage entre le **demandeur de services** et le **fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-164">CSDL represents a platform- and language-independent contract between the **service requestor** and the **service provider**.</span></span> <span data-ttu-id="4e9fe-165">Le langage CSDL permet à un **client** de localiser un **service web/service de base de données** et d’appeler n’importe laquelle de ses **fonctions** disponibles publiquement.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="4e9fe-166">Pour un service de données, vous pouvez considérer les quatre parties d’un élément CSDL comme une base de données, une table, une colonne et une procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-166">For a Data Service the four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="4e9fe-167">Mise en relation de ces éléments comme suit pour un service de données :</span><span class="sxs-lookup"><span data-stu-id="4e9fe-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="4e9fe-168">EntityContainer ~= Base de données</span><span class="sxs-lookup"><span data-stu-id="4e9fe-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="4e9fe-169">EntitySet ~= Table</span><span class="sxs-lookup"><span data-stu-id="4e9fe-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="4e9fe-170">EntityType ~= Colonnes</span><span class="sxs-lookup"><span data-stu-id="4e9fe-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="4e9fe-171">FunctionImport ~= Procédure stockée</span><span class="sxs-lookup"><span data-stu-id="4e9fe-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="4e9fe-172">**Verbes HTTP autorisés**</span><span class="sxs-lookup"><span data-stu-id="4e9fe-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="4e9fe-173">GET - renvoie les valeurs à partir de la base de données (renvoie une collection)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-173">GET – returns values from the db (returns a Collection)</span></span>
* <span data-ttu-id="4e9fe-174">POST - permet de transmettre des données et des valeurs de retour facultatives à partir de la base de données (créer une entrée dans la collection, renvoyer un ID/URI)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-174">POST – used to pass data to and optional return values from the db (Create a new entry in the collection, return id/URI)</span></span>
* <span data-ttu-id="4e9fe-175">DELETE - supprime les données de la base de données (supprime une collection)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-175">DELETE – Deletes data from the DB (Deletes a collection)</span></span>
* <span data-ttu-id="4e9fe-176">PUT - met à jour les données dans une base de données (remplace ou crée une collection)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="4e9fe-177">Document de métadonnées/de mappage</span><span class="sxs-lookup"><span data-stu-id="4e9fe-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="4e9fe-178">Le document de métadonnées/de mappage permet de mapper les services web existants d’un fournisseur de contenu afin qu’il puisse être exposé en tant que service web OData par le système Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-178">The metadata/mapping document is used to map a content provider’s existing web services so that it can be exposed as an OData web service by the Azure Marketplace system.</span></span> <span data-ttu-id="4e9fe-179">Il est basé sur le langage CSDL et implémente certaines extensions dans l’élément CSDL pour répondre aux besoins de REST en fonction des services web exposés via Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-179">It is based on CSDL and implements a few extensions to CSDL to accommodate the needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="4e9fe-180">Les extensions sont trouvent dans l’espace de noms [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) .</span><span class="sxs-lookup"><span data-stu-id="4e9fe-180">The extensions are found in the [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="4e9fe-181">Voici un exemple d’élément CSDL : (Copiez et collez l’exemple CSDL ci-dessous dans un éditeur XML et apportez les modifications nécessaires en fonction de votre service.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-181">An example of the CSDL follows:  (Copy and paste the below example CSDL into an XML editor and change to match your Service.</span></span>  <span data-ttu-id="4e9fe-182">Collez-le ensuite dans un mappage CSDL sous l’onglet Service de données lors de la création de votre service dans le [portail de publication Azure Marketplace](https://publish.windowsazure.com).)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-182">Then paste into CSDL Mapping under DataService tab when creating your service in the  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="4e9fe-183">**Termes :** met en relation les termes CSDL avec les termes de l’interface utilisateur du [portail de publication](https://publish.windowsazure.com) (PPUI).</span><span class="sxs-lookup"><span data-stu-id="4e9fe-183">**Terms:** Relating the CSDL terms to the [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="4e9fe-184">Le « titre » de l’offre dans le PPUI est associé à MyWebOffer</span><span class="sxs-lookup"><span data-stu-id="4e9fe-184">Offer “Title” in the PPUI relates to MyWebOffer</span></span>
* <span data-ttu-id="4e9fe-185">MyCompany dans le PPUI est associé au **nom d’affichage de l’éditeur** dans l’interface utilisateur [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-185">MyCompany in the PPUI relates to **Publisher Display Name** in the [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="4e9fe-186">Votre API est associée à un service web ou de données (un plan dans le PPUI)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-186">Your API relates to a Web or Data Service (a Plan in the PPUI)</span></span>

<span data-ttu-id="4e9fe-187">**Hiérarchie :** une entreprise (fournisseur de contenu) possède une ou plusieurs offres qui comprennent des plans, c’est-à-dire des services, qui sont associés à une API.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="4e9fe-188">Exemple de service web CSDL</span><span class="sxs-lookup"><span data-stu-id="4e9fe-188">WebService CSDL Example</span></span>
<span data-ttu-id="4e9fe-189">L’exemple suivant établit une connexion à un service qui expose un point de terminaison d’application web (comme une application C#).</span><span class="sxs-lookup"><span data-stu-id="4e9fe-189">Connects to a service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all the web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition near the bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is the entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines the service call, replace & with the encode value (&amp;).
        In the input name value pairs {param} represents passed in value.
        Or the value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows the CSDL to specifically specify the verb of the service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes the parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how the web service call is exposed to marketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, the {...} point to the parameters defined below.
        Marketplace will read the parameters from this URITemplate and fill the values into the corresponding parameters of the BaseUri or RequestBody (below) during calls to your service.  
        It is okay for @d:BaseUri to include information only for Marketplace consumption, it will not be exposed to end users. i.e. the hardcoded AccountKey in the above BaseURI does not show up in the client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of the RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders to insert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how to pass userid and password via the header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed to end users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with the value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited to appearing as the value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used to specify values to insert into the ATOM feed returned to the end user.  You can specify the element to contain a fixed message by providing a value for the element (this is the default value).  @d:Map is an XPath expression that points into the response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay to also add a d:Map attribute to override this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of the web service call:
        @Name should match exactly (case sensitive) the {…} placeholders in the @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether the parameter is required.
        @d:Regex - optional, attribute to describe the string, limiting unwanted input at the entry of the system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in the Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating the service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in the order listed.
        @d:Match is an Xpath query on the service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is the error code to return if an response matches the error.
        @d:errorMessage is the user friendly message to return when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect to the service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- The EntityContainer defines the output data schema -->
        </EntityContainer>
        <!-- The EntityType @d:Map defines the repeating node (an XPath query) in the response (output data schema). -->
        <!-- If these nodes are outside a namespace, add the prefix in the xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in the ATOM feed, so comply with the XML element naming restrictions (no spaces or other illegal characters).
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query to point at the location to extract the content from your services response.
        The "." is relative to the repeating node in the EntityType @d:Map Xpath expression.
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
> <span data-ttu-id="4e9fe-190">Affichez d’autres exemples de services web CSDL dans l’article [Exemples de mappage d’un service web existant à OData par le biais des données CSDL](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="4e9fe-190">View more CSDL Web Service examples in the article [Examples of mapping an existing web service to OData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="4e9fe-191">Exemple de service de données CSDL</span><span class="sxs-lookup"><span data-stu-id="4e9fe-191">DataService CSDL Example</span></span>
<span data-ttu-id="4e9fe-192">L’exemple suivant établit une connexion à un service qui expose une table ou une vue de base de données sous la forme d’un point de terminaison. Il présente deux API pour la base de données en fonction du CSDL de l’API (possibilité d’utiliser des vues plutôt que des tables).</span><span class="sxs-lookup"><span data-stu-id="4e9fe-192">Connects to a service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all the data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of the EntitySet as a Service
        @Name is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); the table (or view) and columns to be returned by the data service.)
            Map is the schema.tabel or schema.view
            dals.TableName is the table Name
            Name is the name identifier for the EntityType and the Name of the service exposed to the client via the UI.
            dals:IsExposed determines if the table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is the schema name of the table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines the column properties and the output of the service.
            dals:ColumnName is the name of the column in the table /view.
            Type is the emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is the maximum length of the output value
            Name is the name of the Property and is exposed to the client facing UI
            dals:IsReturned is the Boolean that determines if the Service exposes this value to the client.
            IsQueryable is the Boolean that determines if the column can be used in a database query
            (For data Services: To improve Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is the numerical position x in the table or the View, where x is from 1 to the number of columns in the table.
            dals:DatabaseDataType is the data type of the column in the database, i.e. SQL data type dals:IsPrimaryKey indicates if the column is the Primary key in the table/view.  (The columns marked ISPrimaryKey are used in the Order by clause when returning data.)
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

## <a name="see-also"></a><span data-ttu-id="4e9fe-193">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4e9fe-193">See Also</span></span>
* <span data-ttu-id="4e9fe-194">Si vous souhaitez découvrir et comprendre les nœuds spécifiques et leurs paramètres, lisez l’article [Nœuds de mappage du service de données OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) pour obtenir des définitions et des explications, des exemples, ainsi qu’un contexte de cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-194">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="4e9fe-195">Si vous souhaitez passer en revue des exemples, lisez l’article [Exemples de mappage du service de données OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) pour consulter des exemples de code et pour comprendre la syntaxe et le contexte du code.</span><span class="sxs-lookup"><span data-stu-id="4e9fe-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="4e9fe-196">Pour retourner au chemin indiqué pour la publication d’un service de données sur Azure Marketplace, lisez l’article [Guide de publication de services de données](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="4e9fe-196">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

