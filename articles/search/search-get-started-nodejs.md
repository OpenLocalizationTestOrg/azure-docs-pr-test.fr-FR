---
title: "aaaGet main d’Azure Search dans Node.js | Documents Microsoft"
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
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="16051-103">Prise en main d’Azure Search dans Node.js</span><span class="sxs-lookup"><span data-stu-id="16051-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16051-104">Portail</span><span class="sxs-lookup"><span data-stu-id="16051-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="16051-105">.NET</span><span class="sxs-lookup"><span data-stu-id="16051-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="16051-106">Découvrez comment toobuild un Node.js personnalisé recherche application qui utilise Azure Search pour son expérience de recherche.</span><span class="sxs-lookup"><span data-stu-id="16051-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="16051-107">Ce didacticiel utilise hello [API REST de Service Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello des objets et les opérations utilisées dans cet exercice.</span><span class="sxs-lookup"><span data-stu-id="16051-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="16051-108">Nous avons utilisé [Node.js](https://Nodejs.org) et NPM, [Sublime texte 3](http://www.sublimetext.com/3)et Windows PowerShell sur Windows 8.1 toodevelop et tester ce code.</span><span class="sxs-lookup"><span data-stu-id="16051-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="16051-109">toorun cet exemple, vous devez disposer un service Azure Search, vous pouvez vous connecter à hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16051-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="16051-110">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) pour obtenir des instructions pas à pas.</span><span class="sxs-lookup"><span data-stu-id="16051-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="16051-111">Sur les données de salutation</span><span class="sxs-lookup"><span data-stu-id="16051-111">About hello data</span></span>
<span data-ttu-id="16051-112">Cet exemple d’application utilise des données de hello [États-Unis géologique Services (USG)](http://geonames.usgs.gov/domestic/download_data.htm), filtrée sur la taille du jeu de données hello état de Rhode Island tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="16051-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="16051-113">Nous utiliserons cette toobuild données une application de recherche qui retourne les bâtiments repère telles que le nombre et écoles, ainsi que les fonctionnalités géologiques, flux, lacs et sommets.</span><span class="sxs-lookup"><span data-stu-id="16051-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="16051-114">Dans cette application, hello **DataIndexer** programme génère et charges hello à l’aide de l’index une [indexeur](https://msdn.microsoft.com/library/azure/dn798918.aspx) construction, la récupération hello filtré des groupes universels de sécurité de groupe de données à partir d’une base de données SQL Azure publique.</span><span class="sxs-lookup"><span data-stu-id="16051-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="16051-115">Informations d’identification et de connexion de source de données en ligne d’informations toohello est fourni dans le code de programme hello.</span><span class="sxs-lookup"><span data-stu-id="16051-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="16051-116">Aucune configuration supplémentaire n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="16051-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="16051-117">Nous avons appliqué un filtre sur cette toostay dataset sous limite de document 10 000 hello Hello libre niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="16051-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="16051-118">Si vous utilisez le niveau standard de hello, cette limite ne s’applique pas.</span><span class="sxs-lookup"><span data-stu-id="16051-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="16051-119">Pour plus d’informations sur la capacité de chaque niveau de tarification, consultez la page [Limites de service d’Azure Search](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="16051-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="16051-120">Rechercher le nom du service hello et la clé api de votre service Azure Search</span><span class="sxs-lookup"><span data-stu-id="16051-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="16051-121">Après avoir créé le service de hello, retourner toohello tooget portail hello URL ou `api-key`.</span><span class="sxs-lookup"><span data-stu-id="16051-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="16051-122">Connexions tooyour service de recherche nécessitent que vous avez les deux URL hello et un `api-key` appel de hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="16051-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="16051-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16051-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="16051-124">Dans la barre de saut hello, cliquez sur **service de recherche** toolist tous les services Azure Search est configurés pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="16051-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="16051-125">Sélectionnez le service hello toouse.</span><span class="sxs-lookup"><span data-stu-id="16051-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="16051-126">Tableau de bord de service hello, vous devez voir les vignettes pour des informations essentielles, telles que de l’icône de clé hello pour accéder aux clés d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="16051-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="16051-127">Copiez l’URL du service hello, une clé d’administration et une clé de requête.</span><span class="sxs-lookup"><span data-stu-id="16051-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="16051-128">Vous avez besoin de trois lorsque vous les ajoutez toohello config.js fichier.</span><span class="sxs-lookup"><span data-stu-id="16051-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="16051-129">Télécharger les fichiers d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="16051-129">Download hello sample files</span></span>
<span data-ttu-id="16051-130">Utilisez l’un des hello suivant approches toodownload hello, exemple.</span><span class="sxs-lookup"><span data-stu-id="16051-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="16051-131">Accédez trop[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="16051-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="16051-132">Cliquez sur **ZIP de téléchargement**, enregistrez le fichier .zip de hello, puis extraire tous les fichiers hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="16051-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="16051-133">Toutes les modifications et instructions d’exécution ultérieures seront effectuées sur les fichiers de ce dossier.</span><span class="sxs-lookup"><span data-stu-id="16051-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="16051-134">Mettre à jour hello config.js.</span><span class="sxs-lookup"><span data-stu-id="16051-134">Update hello config.js.</span></span> <span data-ttu-id="16051-135">avec l’URL et la clé API du service de recherche</span><span class="sxs-lookup"><span data-stu-id="16051-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="16051-136">À l’aide de hello URL et la clé d’api que vous avez copiée précédemment, spécifier des URL hello, clé d’administration et de clé de requête dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="16051-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="16051-137">Les clés d’administration octroient un contrôle total sur les opérations du service, notamment la création ou la suppression d'un index et le chargement de documents.</span><span class="sxs-lookup"><span data-stu-id="16051-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="16051-138">En revanche, les clés de requête sont pour les opérations en lecture seule, généralement utilisées par les applications clientes qui se connectent tooAzure recherche.</span><span class="sxs-lookup"><span data-stu-id="16051-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="16051-139">Dans cet exemple, nous incluons requête hello toohelp clé renforcer hello meilleure pratique qui consiste à l’aide de la clé de requête hello dans les applications clientes.</span><span class="sxs-lookup"><span data-stu-id="16051-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="16051-140">Hello ci-dessous capture d’écran illustre **config.js** ouvert dans un éditeur de texte avec hello pertinentes entrées délimitées afin que vous puissiez voir où le fichier hello tooupdate hello valeurs qui sont valides pour votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="16051-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="16051-141">Héberger un environnement d’exécution de l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="16051-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="16051-142">exemple Hello nécessite un serveur HTTP, que vous pouvez installer globalement à l’aide de npm.</span><span class="sxs-lookup"><span data-stu-id="16051-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="16051-143">Utiliser une fenêtre PowerShell pour hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="16051-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="16051-144">Exploration du dossier toohello contenant hello **package.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="16051-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="16051-145">Saisissez `npm install`.</span><span class="sxs-lookup"><span data-stu-id="16051-145">Type `npm install`.</span></span>
3. <span data-ttu-id="16051-146">Saisissez `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="16051-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="16051-147">Créer des index de hello et exécuter l’application hello</span><span class="sxs-lookup"><span data-stu-id="16051-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="16051-148">Saisissez `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="16051-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="16051-149">Saisissez `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="16051-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="16051-150">Saisissez `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="16051-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="16051-151">Dans votre navigateur, accédez à `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="16051-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="16051-152">Exécuter une recherche sur les données USGS</span><span class="sxs-lookup"><span data-stu-id="16051-152">Search on USGS data</span></span>
<span data-ttu-id="16051-153">jeu de données de groupes universels de sécurité Hello comprend les enregistrements qui sont pertinentes toohello état de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="16051-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="16051-154">Si vous cliquez sur **recherche** sur une zone de recherche vide, vous obtenez hello 50 premières entrées, qui est la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="16051-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="16051-155">Entrer un terme de recherche donne moteur de recherche hello quelque chose toogo sur.</span><span class="sxs-lookup"><span data-stu-id="16051-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="16051-156">Essayez d'entrer le nom d’une figure locale.</span><span class="sxs-lookup"><span data-stu-id="16051-156">Try entering a regional name.</span></span> <span data-ttu-id="16051-157">« Roger Williams » a été gouverneur de première hello de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="16051-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="16051-158">De nombreux parcs, bâtiments et écoles portent son nom.</span><span class="sxs-lookup"><span data-stu-id="16051-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="16051-159">Vous pouvez également essayer les termes suivants :</span><span class="sxs-lookup"><span data-stu-id="16051-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="16051-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="16051-160">Pawtucket</span></span>
* <span data-ttu-id="16051-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="16051-161">Pembroke</span></span>
* <span data-ttu-id="16051-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="16051-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="16051-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="16051-163">Next steps</span></span>
<span data-ttu-id="16051-164">Il s’agit de premier didacticiel Azure Search hello, en fonction de Node.js et hello dataset des groupes universels de sécurité.</span><span class="sxs-lookup"><span data-stu-id="16051-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="16051-165">Au fil du temps, nous allons étendre ce didacticiel toodemonstrate les fonctionnalités de recherche supplémentaires vous pourriez toouse dans vos solutions personnalisées.</span><span class="sxs-lookup"><span data-stu-id="16051-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="16051-166">Si vous connaissez déjà Azure Search, vous pouvez utiliser cet exemple comme tremplin pour tester des générateurs de suggestions (requêtes prédictives ou à saisie semi-automatique), des filtres et la navigation à facettes.</span><span class="sxs-lookup"><span data-stu-id="16051-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="16051-167">Vous pouvez également améliorer sur la page de résultats hello en ajoutant des nombres et le traitement par lot des documents afin que les utilisateurs peuvent parcourir les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="16051-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="16051-168">TooAzure nouvelle recherche ?</span><span class="sxs-lookup"><span data-stu-id="16051-168">New tooAzure Search?</span></span> <span data-ttu-id="16051-169">Nous vous recommandons d’essayer d’autres toodevelop didacticiels comprendre ce que vous pouvez créer.</span><span class="sxs-lookup"><span data-stu-id="16051-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="16051-170">Visitez notre [page de documentation](https://azure.microsoft.com/documentation/services/search/) toofind davantage de ressources.</span><span class="sxs-lookup"><span data-stu-id="16051-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="16051-171">Vous pouvez également afficher les liens hello dans notre [liste vidéo et didacticiel](search-video-demo-tutorial-list.md) tooaccess plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="16051-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
