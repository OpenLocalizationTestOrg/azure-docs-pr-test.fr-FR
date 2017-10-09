---
title: aaaImport une API dans la gestion des API Azure | Documents Microsoft
description: "Découvrez comment tooimport une API et ses opérations dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="b9244-103">Comment tooimport hello définition d’une API avec les opérations de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="b9244-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="b9244-104">Gestion des API, nouvelles API peut être créées et opérations hello ajoutées manuellement ou hello API peut être importés, ainsi que les opérations de hello en une seule étape.</span><span class="sxs-lookup"><span data-stu-id="b9244-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="b9244-105">API et leurs opérations peuvent être importées à l’aide de hello suivant formats.</span><span class="sxs-lookup"><span data-stu-id="b9244-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="b9244-106">WADL</span><span class="sxs-lookup"><span data-stu-id="b9244-106">WADL</span></span>
* <span data-ttu-id="b9244-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="b9244-107">Swagger</span></span>

<span data-ttu-id="b9244-108">Ce guide vous présente comment créer une API et importer des opérations en une seule fois.</span><span class="sxs-lookup"><span data-stu-id="b9244-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="b9244-109">Pour plus d’informations sur la création manuelle d’une API et l’ajout des opérations, consultez [comment toocreate API] [ How toocreate APIs] et [comment tooadd opérations tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="b9244-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="b9244-110"><a name="import-api"></a>Importation d’une API</span><span class="sxs-lookup"><span data-stu-id="b9244-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="b9244-111">API est créés et configurés dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="b9244-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="b9244-112">tooaccess hello cliquez portail, du serveur de publication **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="b9244-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="b9244-113">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b9244-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="b9244-115">Cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **importer API**.</span><span class="sxs-lookup"><span data-stu-id="b9244-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![Importer l'API][api-management-import-apis]

<span data-ttu-id="b9244-117">Hello **API d’importation** fenêtre comporte trois onglets correspondant de spécification de hello API tooprovide toohello trois façons.</span><span class="sxs-lookup"><span data-stu-id="b9244-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="b9244-118">**À partir du Presse-papiers** vous permet de spécifier de hello API toopaste dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="b9244-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="b9244-119">**À partir du fichier** vous permet de toobrowse tooand hello Sélectionnez fichier qui contient la spécification de hello API.</span><span class="sxs-lookup"><span data-stu-id="b9244-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="b9244-120">**À partir de l’URL** vous permet de spécification de toohello toosupply hello URL pour hello API.</span><span class="sxs-lookup"><span data-stu-id="b9244-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Import API format][api-management-import-api-clipboard]

<span data-ttu-id="b9244-122">Après avoir entré la spécification de l’API de hello, utilisez cases d’option hello sur format de spécification hello hello tooindicate droite.</span><span class="sxs-lookup"><span data-stu-id="b9244-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="b9244-123">Hello suivant les formats est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b9244-123">hello following formats are supported.</span></span>

* <span data-ttu-id="b9244-124">WADL</span><span class="sxs-lookup"><span data-stu-id="b9244-124">WADL</span></span>
* <span data-ttu-id="b9244-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="b9244-125">Swagger</span></span>

<span data-ttu-id="b9244-126">Ensuite, entrez un **suffixe d’URL d’API web**.</span><span class="sxs-lookup"><span data-stu-id="b9244-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="b9244-127">Il s’agit d’URL de base toohello ajouté pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="b9244-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="b9244-128">URL de base Hello est courant pour toutes les API hébergées sur chaque instance d’un service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="b9244-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="b9244-129">Gestion des API distingue les API par leur suffixe et par conséquent le suffixe de hello doit être unique pour toutes les API dans une instance spécifique du service de gestion de l’API.</span><span class="sxs-lookup"><span data-stu-id="b9244-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="b9244-130">Une fois que toutes les valeurs sont entrées, cliquez sur **enregistrer** toocreate hello API et hello associées des opérations.</span><span class="sxs-lookup"><span data-stu-id="b9244-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="b9244-131">Pour voir un didacticiel sur l’importation d’une API de calculatrice de base au format Swagger, consultez [Gestion de votre première API dans Gestion des API Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9244-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="b9244-132"><a name="export-api"></a> Exportation d’une API</span><span class="sxs-lookup"><span data-stu-id="b9244-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="b9244-133">En outre tooimporting nouvelles API, vous pouvez exporter des définitions de hello de votre API à partir du portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="b9244-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="b9244-134">toodo, cliquez sur **exporter les API** de hello **onglet Résumé** de votre **API**.</span><span class="sxs-lookup"><span data-stu-id="b9244-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![Export API][api-management-export-api]

<span data-ttu-id="b9244-136">Les API peuvent être exportées avec WADL ou Swagger.</span><span class="sxs-lookup"><span data-stu-id="b9244-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="b9244-137">Sélectionnez le format désiré de hello, cliquez sur **enregistrer**et choisir un emplacement de hello dans laquelle le fichier toosave hello.</span><span class="sxs-lookup"><span data-stu-id="b9244-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Export API format][api-management-export-api-format]

## <span data-ttu-id="b9244-139"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b9244-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="b9244-140">Une fois qu’une API est créée et les opérations hello importées, vous pouvez examiner et configurer des paramètres supplémentaires, ajouter hello API tooa produit et publiez-le afin qu’il soit disponible pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="b9244-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="b9244-141">Pour plus d’informations, consultez hello guides de.</span><span class="sxs-lookup"><span data-stu-id="b9244-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="b9244-142">[Comment les paramètres tooconfigure API][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="b9244-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="b9244-143">[Comment toocreate et publier un produit][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="b9244-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
