---
title: Importer une API dans Gestion des API Azure | Microsoft Docs
description: "Découvrez comment importer une API et ses opérations dans Gestion des API Azure."
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
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="d4202-103">Importation de la définition d'une API avec des opérations dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="d4202-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="d4202-104">Dans Gestion des API Azure, de nouvelles API peuvent être créées et les opérations ajoutées de façon manuelle. Il est aussi possible d’importer l’API avec les opérations, en une seule fois.</span><span class="sxs-lookup"><span data-stu-id="d4202-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="d4202-105">Les API et leurs opérations peuvent être importées dans les formats suivants.</span><span class="sxs-lookup"><span data-stu-id="d4202-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="d4202-106">WADL</span><span class="sxs-lookup"><span data-stu-id="d4202-106">WADL</span></span>
* <span data-ttu-id="d4202-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="d4202-107">Swagger</span></span>

<span data-ttu-id="d4202-108">Ce guide vous présente comment créer une API et importer des opérations en une seule fois.</span><span class="sxs-lookup"><span data-stu-id="d4202-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="d4202-109">Pour plus d’informations sur la création manuelle d’une API et l’ajout d’opérations, consultez les rubriques [Création d’API][How to create APIs] et [Ajout d’opérations à une API][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="d4202-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="d4202-110"><a name="import-api"> </a>Importation d’une API</span><span class="sxs-lookup"><span data-stu-id="d4202-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="d4202-111">Les API sont créées et configurées dans le portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="d4202-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="d4202-112">Pour accéder au portail des éditeurs, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d4202-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="d4202-113">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="d4202-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="d4202-115">Cliquez sur **API** dans le menu **Gestion des API** à gauche, puis sur **Importer l’API**.</span><span class="sxs-lookup"><span data-stu-id="d4202-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![Importer l'API][api-management-import-apis]

<span data-ttu-id="d4202-117">La fenêtre **Importer l'API** comporte trois onglets, qui correspondent à trois façons de définir les spécifications de l'API.</span><span class="sxs-lookup"><span data-stu-id="d4202-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="d4202-118">**À partir du Presse-papiers** vous permet de coller la spécification API dans la zone de texte spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d4202-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="d4202-119">**À partir d'un fichier** vous permet de choisir le fichier qui contient la spécification de l'API.</span><span class="sxs-lookup"><span data-stu-id="d4202-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="d4202-120">**À partir d'une URL** vous permet d'indiquer l'URL menant à la spécification de l'API.</span><span class="sxs-lookup"><span data-stu-id="d4202-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Import API format][api-management-import-api-clipboard]

<span data-ttu-id="d4202-122">Une fois la spécification de l'API fournie, utilisez les cases d'option à droite pour indiquer le format de la spécification.</span><span class="sxs-lookup"><span data-stu-id="d4202-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="d4202-123">Les formats suivants sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d4202-123">The following formats are supported.</span></span>

* <span data-ttu-id="d4202-124">WADL</span><span class="sxs-lookup"><span data-stu-id="d4202-124">WADL</span></span>
* <span data-ttu-id="d4202-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="d4202-125">Swagger</span></span>

<span data-ttu-id="d4202-126">Ensuite, entrez un **suffixe d’URL d’API web**.</span><span class="sxs-lookup"><span data-stu-id="d4202-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="d4202-127">Il est ajouté à l'URL de base de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d4202-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="d4202-128">L'URL de base est commune à toutes les API hébergées sur chaque instance du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d4202-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="d4202-129">Gestion des API distingue les API selon leur suffixe. Celui-ci doit donc être unique pour chaque API d'une instance de service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d4202-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="d4202-130">Une fois toutes les valeurs entrées, cliquez sur **Enregistrer** pour créer l'API et les opérations associées.</span><span class="sxs-lookup"><span data-stu-id="d4202-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="d4202-131">Pour voir un didacticiel sur l’importation d’une API de calculatrice de base au format Swagger, consultez [Gestion de votre première API dans Gestion des API Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d4202-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="d4202-132"><a name="export-api"> </a> Exportation d’une API</span><span class="sxs-lookup"><span data-stu-id="d4202-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="d4202-133">En plus de l’importation de nouvelles API, vous pouvez exporter les définitions de vos API depuis le portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="d4202-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="d4202-134">Pour cela, cliquez sur **Exporter l’API** dans l’onglet **Résumé** de votre **API**.</span><span class="sxs-lookup"><span data-stu-id="d4202-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![Export API][api-management-export-api]

<span data-ttu-id="d4202-136">Les API peuvent être exportées avec WADL ou Swagger.</span><span class="sxs-lookup"><span data-stu-id="d4202-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="d4202-137">Sélectionnez le format souhaité, cliquez sur **Enregistrer**, puis choisissez l'emplacement dans lequel enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="d4202-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Export API format][api-management-export-api-format]

## <span data-ttu-id="d4202-139"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4202-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="d4202-140">Une fois l'API créée et les opérations importées, vous pouvez vérifier et configurer les paramètres complémentaires, ajouter l'API à un produit et la publier pour la mettre à disposition des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d4202-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="d4202-141">Pour plus d'informations, consultez les guides suivants :</span><span class="sxs-lookup"><span data-stu-id="d4202-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="d4202-142">[Configuration des paramètres de l’API][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="d4202-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="d4202-143">[Création et publication d’un produit][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="d4202-143">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
