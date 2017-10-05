---
title: "Création d'API dans Gestion des API Azure"
description: "Apprenez à créer et à configurer des API dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="50da6-103">Création d'API dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="50da6-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="50da6-104">Une API du service Gestion des API représente un ensemble d'opérations qui peuvent être appelées par des applications clientes.</span><span class="sxs-lookup"><span data-stu-id="50da6-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="50da6-105">Les nouvelles API sont créées dans le portail des éditeurs, puis les opérations souhaitées sont ajoutées.</span><span class="sxs-lookup"><span data-stu-id="50da6-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="50da6-106">Une fois les opérations ajoutées, l'API est ajoutée à un produit et peut être publiée.</span><span class="sxs-lookup"><span data-stu-id="50da6-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="50da6-107">Une fois l'API publiée, les développeurs peuvent s'y abonner et l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="50da6-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="50da6-108">Ce guide présente la première étape du processus : comment créer et configurer une nouvelle API dans Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="50da6-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="50da6-109">Pour plus d’informations sur l’ajout d’opérations et la publication d’un produit, consultez les rubriques [Ajout d’opérations à une API][How to add operations to an API] et [Création et publication d’un produit][How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="50da6-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="50da6-110"><a name="create-new-api"> </a>Création d’une API</span><span class="sxs-lookup"><span data-stu-id="50da6-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="50da6-111">Les API sont créées et configurées dans le portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="50da6-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="50da6-112">Pour accéder au portail des éditeurs, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="50da6-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="50da6-114">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="50da6-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="50da6-115">Cliquez sur **API** dans le menu **Gestion des API** à gauche, puis sur **Ajouter des API**.</span><span class="sxs-lookup"><span data-stu-id="50da6-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![Create API][api-management-create-api]

<span data-ttu-id="50da6-117">Utilisez la fenêtre **Ajouter une nouvelle API** pour configurer la nouvelle API.</span><span class="sxs-lookup"><span data-stu-id="50da6-117">Use the **Add new API** window to configure the new API.</span></span>

![Ajouter une nouvelle API][api-management-add-new-api]

<span data-ttu-id="50da6-119">Les champs suivants permettent de configurer la nouvelle API.</span><span class="sxs-lookup"><span data-stu-id="50da6-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="50da6-120">**Titre d'API web** fournit un nom descriptif unique pour l'API.</span><span class="sxs-lookup"><span data-stu-id="50da6-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="50da6-121">Il s’affiche dans les portails des développeurs et de publication.</span><span class="sxs-lookup"><span data-stu-id="50da6-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="50da6-122">**URL du service web** indique le service HTTP implémentant l'API.</span><span class="sxs-lookup"><span data-stu-id="50da6-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="50da6-123">La gestion des API transmet les demandes à cette adresse.</span><span class="sxs-lookup"><span data-stu-id="50da6-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="50da6-124">Le **suffixe de l’URL d’API web** est ajouté à l’URL de base du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="50da6-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="50da6-125">L'URL de base est commune à toutes les API hébergées par une instance de service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="50da6-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="50da6-126">Gestion des API distingue les API selon leur suffixe. Celui-ci doit donc être unique pour chaque API d'un éditeur donné.</span><span class="sxs-lookup"><span data-stu-id="50da6-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="50da6-127">**schéma d’URL d’API web** détermine quels sont les protocoles qui peuvent être utilisés pour accéder à l’API.</span><span class="sxs-lookup"><span data-stu-id="50da6-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="50da6-128">Le protocole HTTPS est spécifié par défaut.</span><span class="sxs-lookup"><span data-stu-id="50da6-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="50da6-129">Pour ajouter éventuellement cette nouvelle API à un produit, cliquez sur la liste déroulante **Produits (facultatif)** et choisissez un produit.</span><span class="sxs-lookup"><span data-stu-id="50da6-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="50da6-130">Cette étape peut être répétée plusieurs fois pour ajouter l'API à plusieurs produits.</span><span class="sxs-lookup"><span data-stu-id="50da6-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="50da6-131">Une fois les valeurs de votre choix configurées, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="50da6-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="50da6-132">Une fois l'API créée, la page de résumé de l'API s'affiche dans le portail de publication.</span><span class="sxs-lookup"><span data-stu-id="50da6-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![API summary][api-management-api-summary]

## <span data-ttu-id="50da6-134"><a name="configure-api-settings"> </a>Configuration des paramètres de l’API</span><span class="sxs-lookup"><span data-stu-id="50da6-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="50da6-135">L’onglet **Paramètres** permet de vérifier et de modifier la configuration d’une API.</span><span class="sxs-lookup"><span data-stu-id="50da6-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="50da6-136">Les options **Nom d’API web**, **URL du service web** et **Suffixe d’URL de l’API web** sont définis initialement lors de la création de l’API. Vous pouvez les modifier ici.</span><span class="sxs-lookup"><span data-stu-id="50da6-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="50da6-137">**Description** contient une description facultative et **Schéma d’URL d’API web** détermine quels sont les protocoles qui peuvent être utilisés pour accéder à l’API.</span><span class="sxs-lookup"><span data-stu-id="50da6-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![API settings][api-management-api-settings]

<span data-ttu-id="50da6-139">Pour configurer l'authentification de la passerelle pour le service principal avec mise en œuvre de l'API, sélectionnez l’onglet **Sécurité** .</span><span class="sxs-lookup"><span data-stu-id="50da6-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="50da6-140">La liste déroulante **Avec informations d’identification** peut servir à configurer l’authentification **HTTP de base** ou par **Certificats client**.</span><span class="sxs-lookup"><span data-stu-id="50da6-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="50da6-141">Pour utiliser l'authentification HTTP de base, entrez simplement les informations d'identification de votre choix.</span><span class="sxs-lookup"><span data-stu-id="50da6-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="50da6-142">Pour plus d’informations sur l’utilisation de l’authentification avec certificats client, consultez la page [Comment sécuriser les services principaux à l’aide d’une authentification de certificat client dans Gestion des API Azure][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="50da6-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="50da6-143">L’onglet **Sécurité** peut également être utilisé pour configurer **Autorisation utilisateur** avec OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="50da6-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="50da6-144">Pour plus d’informations, consultez la page [Comment autoriser des comptes de développeurs à l’aide d’OAuth 2.0 dans Gestion des API Azure][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="50da6-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Basic authentication settings][api-management-api-settings-credentials]

<span data-ttu-id="50da6-146">Cliquez sur **Enregistrer** pour enregistrer les modifications apportées aux paramètres de l'API.</span><span class="sxs-lookup"><span data-stu-id="50da6-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="50da6-147"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50da6-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="50da6-148">Une fois l'API créée et les paramètres configurés, l'étape suivante consiste à ajouter les opérations à l'API, à ajouter l'API à un produit et à la publier pour la mettre à disposition des développeurs.</span><span class="sxs-lookup"><span data-stu-id="50da6-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="50da6-149">Pour plus d'informations, consultez les articles suivants.</span><span class="sxs-lookup"><span data-stu-id="50da6-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="50da6-150">[Ajout d’opérations à une API][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="50da6-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="50da6-151">[Création et publication d’un produit][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="50da6-151">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
