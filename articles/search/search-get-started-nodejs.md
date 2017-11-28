---
title: "Prise en main d’Azure Search dans Node.js | Microsoft Docs"
description: "Guide de création d’une application de recherche sur un service de recherche Azure hébergé dans le cloud en utilisant le langage de programmation Node.js."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="e79f4-103">Prise en main d’Azure Search dans Node.js</span><span class="sxs-lookup"><span data-stu-id="e79f4-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e79f4-104">Portail</span><span class="sxs-lookup"><span data-stu-id="e79f4-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="e79f4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e79f4-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="e79f4-106">Apprenez à créer une application de recherche Node.js personnalisée, qui utilise Azure Search pour ses fonctionnalités de recherche.</span><span class="sxs-lookup"><span data-stu-id="e79f4-106">Learn how to build a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="e79f4-107">Ce didacticiel utilise l’ [API REST du service Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) pour créer les objets et opérations utilisés dans cet exercice.</span><span class="sxs-lookup"><span data-stu-id="e79f4-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="e79f4-108">Nous avons utilisé [Node.js](https://Nodejs.org) et NPM, [Sublime Text 3](http://www.sublimetext.com/3) et Windows PowerShell sur Windows 8.1 pour développer et tester ce code.</span><span class="sxs-lookup"><span data-stu-id="e79f4-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span></span>

<span data-ttu-id="e79f4-109">Pour exécuter cet exemple, vous devez disposer d’un service Azure Search auquel vous pouvez vous connecter dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e79f4-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e79f4-110">Consultez [Création d’un service Azure Search dans le portail](search-create-service-portal.md) pour obtenir des instructions pas-à-pas.</span><span class="sxs-lookup"><span data-stu-id="e79f4-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-the-data"></a><span data-ttu-id="e79f4-111">À propos des données</span><span class="sxs-lookup"><span data-stu-id="e79f4-111">About the data</span></span>
<span data-ttu-id="e79f4-112">Cet exemple d'application utilise des données de l’ [USGS (United States Geological Services)](http://geonames.usgs.gov/domestic/download_data.htm), concernant l'État de Rhode Island pour réduire la taille du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="e79f4-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="e79f4-113">Nous allons utiliser ces données pour créer une application de recherche qui renvoie des bâtiments repères, tels que les hôpitaux et les écoles, ainsi que des caractéristiques géologiques, telles que les ruisseaux, les lacs et les sommets.</span><span class="sxs-lookup"><span data-stu-id="e79f4-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="e79f4-114">Dans cette application, le programme **DataIndexer** crée et charge l'index à l'aide d'une construction de type [Index](https://msdn.microsoft.com/library/azure/dn798918.aspx) , en récupérant le jeu de données USGS filtré à partir d'une base de données SQL Azure publique.</span><span class="sxs-lookup"><span data-stu-id="e79f4-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="e79f4-115">Les informations d'identification et de connexion à la source de données en ligne sont fournies dans le code du programme.</span><span class="sxs-lookup"><span data-stu-id="e79f4-115">Credentials and connection information to the online data source is provided in the program code.</span></span> <span data-ttu-id="e79f4-116">Aucune configuration supplémentaire n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e79f4-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="e79f4-117">Nous avons appliqué un filtre à ce jeu de données pour ne pas dépasser la limite de 10 000 documents du niveau de tarification gratuit.</span><span class="sxs-lookup"><span data-stu-id="e79f4-117">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="e79f4-118">Si vous utilisez le niveau standard, cette limite ne s'applique pas.</span><span class="sxs-lookup"><span data-stu-id="e79f4-118">If you use the standard tier, this limit does not apply.</span></span> <span data-ttu-id="e79f4-119">Pour plus d’informations sur la capacité de chaque niveau de tarification, consultez la page [Limites de service d’Azure Search](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="e79f4-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="e79f4-120">Rechercher le nom et la clé API de votre service Azure Search</span><span class="sxs-lookup"><span data-stu-id="e79f4-120">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="e79f4-121">Une fois le service créé, revenez au portail pour obtenir l'URL ou `api-key`.</span><span class="sxs-lookup"><span data-stu-id="e79f4-121">After you create the service, return to the portal to get the URL or `api-key`.</span></span> <span data-ttu-id="e79f4-122">Pour vous connecter à votre service de recherche, vous devez saisir l'URL et une `api-key` afin d’authentifier l'appel.</span><span class="sxs-lookup"><span data-stu-id="e79f4-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span></span>

1. <span data-ttu-id="e79f4-123">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e79f4-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e79f4-124">Dans la barre d’index, cliquez sur **Service de recherche** pour obtenir la liste des services Azure Search approvisionnés pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e79f4-124">In the jump bar, click **Search service** to list all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="e79f4-125">Sélectionnez le service que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="e79f4-125">Select the service you want to use.</span></span>
4. <span data-ttu-id="e79f4-126">Le tableau de bord des services affiche des vignettes contenant des informations essentielles, ainsi que l’icône de clé permettant d’accéder aux clés administrateur.</span><span class="sxs-lookup"><span data-stu-id="e79f4-126">On the service dashboard, you should see tiles for essential information, such as the key icon for accessing the admin keys.</span></span>
5. <span data-ttu-id="e79f4-127">Copiez l'URL du service, une clé d’administration et une clé de requête.</span><span class="sxs-lookup"><span data-stu-id="e79f4-127">Copy the service URL, an admin key, and a query key.</span></span> <span data-ttu-id="e79f4-128">Vous en aurez besoin plus tard, pour les ajouter au fichier config.js.</span><span class="sxs-lookup"><span data-stu-id="e79f4-128">You need all three later when you add them to the config.js file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="e79f4-129">Télécharger les fichiers exemples</span><span class="sxs-lookup"><span data-stu-id="e79f4-129">Download the sample files</span></span>
<span data-ttu-id="e79f4-130">Utilisez l'une des approches suivantes pour télécharger l'exemple.</span><span class="sxs-lookup"><span data-stu-id="e79f4-130">Use either one of the following approaches to download the sample.</span></span>

1. <span data-ttu-id="e79f4-131">Accédez à [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="e79f4-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="e79f4-132">Cliquez sur **Download ZIP**, enregistrez le fichier ZIP sur le disque, puis extrayez tous les fichiers qu'il contient.</span><span class="sxs-lookup"><span data-stu-id="e79f4-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span></span>

<span data-ttu-id="e79f4-133">Toutes les modifications et instructions d’exécution ultérieures seront effectuées sur les fichiers de ce dossier.</span><span class="sxs-lookup"><span data-stu-id="e79f4-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="e79f4-134">Mettre à jour le fichier config.js.</span><span class="sxs-lookup"><span data-stu-id="e79f4-134">Update the config.js.</span></span> <span data-ttu-id="e79f4-135">avec l’URL et la clé API du service de recherche</span><span class="sxs-lookup"><span data-stu-id="e79f4-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="e79f4-136">À l'aide de l'URL et des clés API que vous avez copiées précédemment, spécifiez l'URL, la clé d’administration et la clé de requête dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="e79f4-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="e79f4-137">Les clés d’administration octroient un contrôle total sur les opérations du service, notamment la création ou la suppression d'un index et le chargement de documents.</span><span class="sxs-lookup"><span data-stu-id="e79f4-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="e79f4-138">En revanche, les clés de requête sont réservées aux opérations en lecture seule, généralement utilisées par les applications clientes qui se connectent à Azure Search.</span><span class="sxs-lookup"><span data-stu-id="e79f4-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span></span>

<span data-ttu-id="e79f4-139">Dans cet exemple, nous incluons la clé de requête pour renforcer la bonne pratique consistant à utiliser la clé de requête dans les applications clientes.</span><span class="sxs-lookup"><span data-stu-id="e79f4-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span></span>

<span data-ttu-id="e79f4-140">La capture d'écran suivante montre le fichier **config.js** ouvert dans un éditeur de texte, avec les entrées appropriées encadrées en rouge pour que vous puissiez voir où mettre à jour le fichier avec les valeurs correspondant à votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="e79f4-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a><span data-ttu-id="e79f4-141">Héberger un environnement d’exécution pour l’exemple</span><span class="sxs-lookup"><span data-stu-id="e79f4-141">Host a runtime environment for the sample</span></span>
<span data-ttu-id="e79f4-142">Cet exemple nécessite un serveur HTTP, que vous pouvez installer globalement à l'aide de npm.</span><span class="sxs-lookup"><span data-stu-id="e79f4-142">The sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="e79f4-143">Exécutez les commandes suivantes dans une fenêtre PowerShell :</span><span class="sxs-lookup"><span data-stu-id="e79f4-143">Use a PowerShell window for the following commands.</span></span>

1. <span data-ttu-id="e79f4-144">Accédez au dossier qui contient le fichier **package.json** .</span><span class="sxs-lookup"><span data-stu-id="e79f4-144">Navigate to the folder that contains the **package.json** file.</span></span>
2. <span data-ttu-id="e79f4-145">Saisissez `npm install`.</span><span class="sxs-lookup"><span data-stu-id="e79f4-145">Type `npm install`.</span></span>
3. <span data-ttu-id="e79f4-146">Saisissez `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="e79f4-146">Type `npm install -g http-server`.</span></span>

## <a name="build-the-index-and-run-the-application"></a><span data-ttu-id="e79f4-147">Générer l’index et exécuter l'application</span><span class="sxs-lookup"><span data-stu-id="e79f4-147">Build the index and run the application</span></span>
1. <span data-ttu-id="e79f4-148">Saisissez `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="e79f4-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="e79f4-149">Saisissez `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="e79f4-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="e79f4-150">Saisissez `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="e79f4-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="e79f4-151">Dans votre navigateur, accédez à `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="e79f4-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="e79f4-152">Exécuter une recherche sur les données USGS</span><span class="sxs-lookup"><span data-stu-id="e79f4-152">Search on USGS data</span></span>
<span data-ttu-id="e79f4-153">Le jeu de données USGS comprend les enregistrements qui correspondent à l'État de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="e79f4-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="e79f4-154">Si vous cliquez sur **Recherche** et que le champ de recherche est vide, vous obtiendrez les 50 premières entrées, ce qui correspond au paramétrage par défaut.</span><span class="sxs-lookup"><span data-stu-id="e79f4-154">If you click **Search** on an empty search box, you get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="e79f4-155">Saisissez un terme pour que le moteur de recherche puisse travailler.</span><span class="sxs-lookup"><span data-stu-id="e79f4-155">Entering a search term gives the search engine something to go on.</span></span> <span data-ttu-id="e79f4-156">Essayez d'entrer le nom d’une figure locale.</span><span class="sxs-lookup"><span data-stu-id="e79f4-156">Try entering a regional name.</span></span> <span data-ttu-id="e79f4-157">« Roger Williams » fut le premier gouverneur de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="e79f4-157">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="e79f4-158">De nombreux parcs, bâtiments et écoles portent son nom.</span><span class="sxs-lookup"><span data-stu-id="e79f4-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="e79f4-159">Vous pouvez également essayer les termes suivants :</span><span class="sxs-lookup"><span data-stu-id="e79f4-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="e79f4-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="e79f4-160">Pawtucket</span></span>
* <span data-ttu-id="e79f4-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="e79f4-161">Pembroke</span></span>
* <span data-ttu-id="e79f4-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="e79f4-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="e79f4-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e79f4-163">Next steps</span></span>
<span data-ttu-id="e79f4-164">Ceci est le premier didacticiel Azure Search basé sur Node.js et le jeu de données USGS.</span><span class="sxs-lookup"><span data-stu-id="e79f4-164">This is the first Azure Search tutorial based on Node.js and the USGS dataset.</span></span> <span data-ttu-id="e79f4-165">Au fil du temps, nous le compléterons avec des fonctionnalités de recherche supplémentaires que vous souhaiterez peut-être utiliser dans vos solutions personnalisées.</span><span class="sxs-lookup"><span data-stu-id="e79f4-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="e79f4-166">Si vous connaissez déjà Azure Search, vous pouvez utiliser cet exemple comme tremplin pour tester des générateurs de suggestions (requêtes prédictives ou à saisie semi-automatique), des filtres et la navigation à facettes.</span><span class="sxs-lookup"><span data-stu-id="e79f4-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="e79f4-167">Vous pouvez également améliorer la page des résultats de la recherche en ajoutant des décomptes et en traitant les documents par lots afin que les utilisateurs puissent parcourir les résultats.</span><span class="sxs-lookup"><span data-stu-id="e79f4-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="e79f4-168">Vous découvrez Azure Search ?</span><span class="sxs-lookup"><span data-stu-id="e79f4-168">New to Azure Search?</span></span> <span data-ttu-id="e79f4-169">Nous vous recommandons de suivre les autres didacticiels pour comprendre ce que vous pouvez créer.</span><span class="sxs-lookup"><span data-stu-id="e79f4-169">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="e79f4-170">Consultez les autres ressources disponibles dans notre [page de documentation](https://azure.microsoft.com/documentation/services/search/) .</span><span class="sxs-lookup"><span data-stu-id="e79f4-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="e79f4-171">Vous pouvez également cliquer sur les liens dans notre [liste de vidéos et de didacticiels](search-video-demo-tutorial-list.md) pour obtenir des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e79f4-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
