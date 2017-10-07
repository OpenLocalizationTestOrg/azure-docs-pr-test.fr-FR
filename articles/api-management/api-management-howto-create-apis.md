---
title: aaaHow toocreate API de gestion des API Azure
description: "Découvrez comment toocreate et configurer les API de gestion des API Azure."
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
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="e5d4c-103">Comment toocreate API de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="e5d4c-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="e5d4c-104">Une API du service Gestion des API représente un ensemble d'opérations qui peuvent être appelées par des applications clientes.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="e5d4c-105">Nouvelles API est créés dans le portail de publication hello et puis hello souhaité opérations sont ajoutées.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="e5d4c-106">Une fois ajoutées, les opérations hello hello API est ajouté tooa produit et peut être publié.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="e5d4c-107">Une fois qu’une API est publiée, il peut être souscrit tooand utilisée par les développeurs.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="e5d4c-108">Ce guide montre la première étape de hello dans les processus hello : comment toocreate et configurer une nouvelle API de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="e5d4c-109">Pour plus d’informations sur l’ajout des opérations et la publication d’un produit, consultez [comment tooadd opérations tooan API] [ How tooadd operations tooan API] et [comment toocreate et publier un produit] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="e5d4c-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="e5d4c-110"><a name="create-new-api"></a>Création d’une API</span><span class="sxs-lookup"><span data-stu-id="e5d4c-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="e5d4c-111">API est créés et configurés dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="e5d4c-112">tooaccess hello cliquez portail, du serveur de publication **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="e5d4c-114">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="e5d4c-115">Cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **ajouter API**.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![Create API][api-management-create-api]

<span data-ttu-id="e5d4c-117">Hello d’utilisation **ajouter la nouvelle API** fenêtre tooconfigure hello nouvelle API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Ajouter une nouvelle API][api-management-add-new-api]

<span data-ttu-id="e5d4c-119">Hello suivant les champs est utilisés tooconfigure hello nouvelle API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="e5d4c-120">**Nom de l’API Web** fournit un nom unique et descriptif pour hello API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="e5d4c-121">Il est affiché dans les portails de développeur et éditeur hello.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="e5d4c-122">**URL du service Web** références hello service HTTP hello API de mise en œuvre.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="e5d4c-123">Gestion des API transfère les demandes de toothis adresse.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="e5d4c-124">**Suffixe d’URL de l’API Web** est l’URL de base toohello ajouté hello API de service de gestion.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="e5d4c-125">URL de base Hello est courant pour toutes les API hébergées par une instance de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="e5d4c-126">Gestion des API distingue les API par leur suffixe et par conséquent le suffixe de hello doit être unique pour toutes les API pour un serveur de publication donné.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="e5d4c-127">**Schéma de l’URL de l’API Web** détermine les protocoles qui peuvent être utilisés tooaccess hello API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="e5d4c-128">Le protocole HTTPS est spécifié par défaut.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="e5d4c-129">toooptionally ajouter ce produit tooa de nouvelles API, cliquez sur hello **produits (facultatifs)** liste déroulante et choisissez un produit.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="e5d4c-130">Cette étape peut être répété à plusieurs reprises tooadd hello API toomultiple produits.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="e5d4c-131">Une fois hello souhaité de valeurs sont configurées, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="e5d4c-132">Après la création de la nouvelle API de hello, hello page Résumé pour l’API de hello s’affiche dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Résumé des API][api-management-api-summary]

## <span data-ttu-id="e5d4c-134"><a name="configure-api-settings"></a>Configuration des paramètres de l’API</span><span class="sxs-lookup"><span data-stu-id="e5d4c-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="e5d4c-135">Vous pouvez utiliser hello **paramètres** onglet tooverify et modifier la configuration de hello d’API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="e5d4c-136">**Nom de l’API Web**, **URL du service Web**, et **suffixe d’URL d’API Web** sont initialement définies lors de l’API de hello est créé et peut être modifié.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="e5d4c-137">**Description** fournit une description facultative, et **le modèle d’URL d’API Web** détermine les protocoles qui peuvent être utilisés tooaccess hello API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![API settings][api-management-api-settings]

<span data-ttu-id="e5d4c-139">authentification de la passerelle tooconfigure hello principal de service application hello API, sélectionnez hello **sécurité** hello d’onglet **avec les informations d’identification** déroulante peut être utilisé tooconfigure **HTTP base** ou **les certificats clients** l’authentification.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="e5d4c-140">l’authentification de base toouse HTTP, il suffit d’entrer les informations d’identification de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="e5d4c-141">Pour plus d’informations sur l’utilisation de l’authentification du certificat client, consultez [comment toosecure services de back-end à l’aide du client de certificat d’authentification dans la gestion des API Azure][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="e5d4c-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="e5d4c-142">Hello **sécurité** onglet peut également être utilisé tooconfigure **autorisation de l’utilisateur** à l’aide d’OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="e5d4c-143">Pour plus d’informations, consultez [comment tooauthorize développeur comptes à l’aide OAuth 2.0 dans Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="e5d4c-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Basic authentication settings][api-management-api-settings-credentials]

<span data-ttu-id="e5d4c-145">Cliquez sur **enregistrer** toosave toutes les modifications que vous apportez toohello paramètres de l’API.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="e5d4c-146"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5d4c-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="e5d4c-147">Une fois qu’une API est créée et configurés les paramètres hello, hello suivants étapes tooadd hello operations toohello API, ajouter hello API tooa produit et publiez-le afin qu’il soit disponible pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="e5d4c-148">Pour plus d’informations, consultez hello suivant des articles.</span><span class="sxs-lookup"><span data-stu-id="e5d4c-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="e5d4c-149">[Comment tooadd opérations tooan API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="e5d4c-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="e5d4c-150">[Comment toocreate et publier un produit][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="e5d4c-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
