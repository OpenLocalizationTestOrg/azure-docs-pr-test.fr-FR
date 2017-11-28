---
title: "aaaGet main d’Azure Search dans Java | Documents Microsoft"
description: "Comment toobuild un nuage hébergé recherche application sur Azure à l’aide de Java comme langage de programmation."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="c09c1-103">Prise en main d'Azure Search dans Java</span><span class="sxs-lookup"><span data-stu-id="c09c1-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c09c1-104">Portail</span><span class="sxs-lookup"><span data-stu-id="c09c1-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="c09c1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c09c1-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="c09c1-106">Découvrez comment toobuild Java personnalisé recherche application qui utilise Azure Search pour son expérience de recherche.</span><span class="sxs-lookup"><span data-stu-id="c09c1-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="c09c1-107">Ce didacticiel utilise hello [API REST de Service Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello des objets et les opérations utilisées dans cet exercice.</span><span class="sxs-lookup"><span data-stu-id="c09c1-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="c09c1-108">toorun cet exemple, vous devez disposer un service Azure Search, vous pouvez vous connecter à hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c09c1-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="c09c1-109">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) pour obtenir des instructions pas à pas.</span><span class="sxs-lookup"><span data-stu-id="c09c1-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="c09c1-110">Nous utilisé hello suivant logiciel toobuild et tester cet exemple :</span><span class="sxs-lookup"><span data-stu-id="c09c1-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="c09c1-111">[Environnement de développement intégré (IDE) Eclipse pour développeurs Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="c09c1-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="c09c1-112">La version Java EE hello toodownload vraiment être.</span><span class="sxs-lookup"><span data-stu-id="c09c1-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="c09c1-113">Une des étapes de vérification hello nécessite une fonctionnalité qui se trouve uniquement dans cette édition.</span><span class="sxs-lookup"><span data-stu-id="c09c1-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="c09c1-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="c09c1-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="c09c1-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="c09c1-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="c09c1-116">Sur les données de salutation</span><span class="sxs-lookup"><span data-stu-id="c09c1-116">About hello data</span></span>
<span data-ttu-id="c09c1-117">Cet exemple d’application utilise des données de hello [États-Unis géologique Services (USG)](http://geonames.usgs.gov/domestic/download_data.htm), filtrée sur la taille du jeu de données hello état de Rhode Island tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="c09c1-118">Nous utiliserons cette toobuild données une application de recherche qui retourne les bâtiments repère telles que le nombre et écoles, ainsi que les fonctionnalités géologiques, flux, lacs et sommets.</span><span class="sxs-lookup"><span data-stu-id="c09c1-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="c09c1-119">Dans cette application, hello **SearchServlet.java** programme génère et charges hello à l’aide de l’index une [indexeur](https://msdn.microsoft.com/library/azure/dn798918.aspx) construction, la récupération hello filtré des groupes universels de sécurité de groupe de données à partir d’une base de données SQL Azure publique.</span><span class="sxs-lookup"><span data-stu-id="c09c1-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="c09c1-120">Les informations d’identification prédéfinies et de la source de données en ligne de connexion informations toohello sont fournies dans le code de programme hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="c09c1-121">Pour accéder aux données, aucune configuration supplémentaire n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c09c1-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="c09c1-122">Nous avons appliqué un filtre sur cette toostay dataset sous limite de document 10 000 hello Hello libre niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="c09c1-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="c09c1-123">Si vous utilisez le niveau standard de hello, cette limite ne s’applique pas, et vous pouvez modifier ce code de toouse un plus grand jeu de données.</span><span class="sxs-lookup"><span data-stu-id="c09c1-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="c09c1-124">Pour plus d'informations sur la capacité de chaque niveau de tarification, consultez la section [Limites et contraintes](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="c09c1-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="c09c1-125">À propos des fichiers de programme hello</span><span class="sxs-lookup"><span data-stu-id="c09c1-125">About hello program files</span></span>
<span data-ttu-id="c09c1-126">Hello liste suivante décrit les fichiers hello qui sont pertinentes toothis échantillon.</span><span class="sxs-lookup"><span data-stu-id="c09c1-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="c09c1-127">Search.jsp : Fournit l’interface utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="c09c1-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="c09c1-128">SearchServlet.java : Fournit des méthodes (similaire tooa contrôleur MVC)</span><span class="sxs-lookup"><span data-stu-id="c09c1-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="c09c1-129">SearchServiceClient.java : gère les descripteurs HTTP.</span><span class="sxs-lookup"><span data-stu-id="c09c1-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="c09c1-130">SearchServiceHelper.java : classe d’utilitaire qui fournit des méthodes statiques.</span><span class="sxs-lookup"><span data-stu-id="c09c1-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="c09c1-131">Document.Java : Fournit le modèle de données hello</span><span class="sxs-lookup"><span data-stu-id="c09c1-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="c09c1-132">config.Properties : définit l’URL du service recherche hello et clé d’api</span><span class="sxs-lookup"><span data-stu-id="c09c1-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="c09c1-133">Pom.XML : dépendance Maven.</span><span class="sxs-lookup"><span data-stu-id="c09c1-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="c09c1-134">Rechercher le nom du service hello et la clé api de votre service Azure Search</span><span class="sxs-lookup"><span data-stu-id="c09c1-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="c09c1-135">Tous les appels d’API REST dans Azure Search nécessitent que vous fournissiez hello URL du service et une clé d’api.</span><span class="sxs-lookup"><span data-stu-id="c09c1-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="c09c1-136">Connectez-vous à toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c09c1-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c09c1-137">Dans la barre de saut hello, cliquez sur **service de recherche** toolist tous les services d’Azure Search hello définis pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="c09c1-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="c09c1-138">Sélectionnez le service hello toouse.</span><span class="sxs-lookup"><span data-stu-id="c09c1-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="c09c1-139">Tableau de bord de service hello, vous verrez des vignettes pour des informations essentielles ainsi qu’icône de clé hello pour accéder aux clés d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="c09c1-140">Copiez l’URL du service hello et une clé d’administration.</span><span class="sxs-lookup"><span data-stu-id="c09c1-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="c09c1-141">Vous en aurez besoin plus tard, lorsque vous les ajoutez toohello **config.Properties** fichier.</span><span class="sxs-lookup"><span data-stu-id="c09c1-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="c09c1-142">Télécharger les fichiers d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="c09c1-142">Download hello sample files</span></span>
1. <span data-ttu-id="c09c1-143">Accédez trop[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="c09c1-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="c09c1-144">Cliquez sur **ZIP de téléchargement**, enregistrer toodisk de fichier .zip hello, puis extraire tous les fichiers hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="c09c1-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="c09c1-145">Envisagez l’extraction hello fichiers dans votre toomake d’espace de travail Java qu’il plus facile projet de hello toofind plus tard.</span><span class="sxs-lookup"><span data-stu-id="c09c1-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="c09c1-146">fichiers d’exemple Hello sont en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="c09c1-146">hello sample files are read-only.</span></span> <span data-ttu-id="c09c1-147">Cliquez sur Propriétés du dossier et désactivez hello en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="c09c1-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="c09c1-148">Toutes les modifications et instructions d'exécution ultérieures seront effectuées sur les fichiers de ce dossier.</span><span class="sxs-lookup"><span data-stu-id="c09c1-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="c09c1-149">Importer le projet</span><span class="sxs-lookup"><span data-stu-id="c09c1-149">Import project</span></span>
1. <span data-ttu-id="c09c1-150">Dans Eclipse, choisissez **File** > **Import** > **General** > **Existing Projects into Workspace**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="c09c1-151">Dans **répertoire racine sélectionnez**, parcourir le dossier toohello contenant des exemples de fichiers.</span><span class="sxs-lookup"><span data-stu-id="c09c1-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="c09c1-152">Sélectionnez le dossier hello qui contient le dossier de .project hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="c09c1-153">projet de Hello doit apparaître dans hello **projets** liste comme un élément sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c09c1-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="c09c1-154">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-154">Click **Finish**.</span></span>
4. <span data-ttu-id="c09c1-155">Utilisez **Explorateur de projets** tooview et modifier les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="c09c1-156">Si elle n’est pas déjà ouverte, cliquez sur **fenêtre** > **afficher la vue** > **Explorateur de projets** ou utilisez hello contextuel tooopen il.</span><span class="sxs-lookup"><span data-stu-id="c09c1-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="c09c1-157">Configurer l’URL du service hello et clé d’api</span><span class="sxs-lookup"><span data-stu-id="c09c1-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="c09c1-158">Dans **Explorateur de projets**, double-cliquez sur **config.Properties** tooedit hello de configuration qui contient le nom du serveur hello et clé d’api.</span><span class="sxs-lookup"><span data-stu-id="c09c1-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="c09c1-159">Consultez les étapes toohello plus haut dans cet article, où vous avez trouvé hello URL du service et la clé d’api dans hello [portail Azure](https://portal.azure.com), les valeurs de hello tooget vous entrerez dans **config.Properties**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="c09c1-160">Dans **config.Properties**, remplacez « Clé Api » avec la clé api hello pour votre service.</span><span class="sxs-lookup"><span data-stu-id="c09c1-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="c09c1-161">Ensuite, le nom de service (hello premier composant du hello URL http://servicename.search.windows.net) remplace le « nom du service » Bonjour même fichier.</span><span class="sxs-lookup"><span data-stu-id="c09c1-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="c09c1-162">Configurez des environnements de projet, de génération et d’exécution hello</span><span class="sxs-lookup"><span data-stu-id="c09c1-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="c09c1-163">Dans Eclipse, dans l’Explorateur de projets, cliquez sur projet de hello > **propriétés** > **projet facettes**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="c09c1-164">Sélectionnez **Dynamic Web Module**, **Java** et **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="c09c1-165">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-165">Click **Apply**.</span></span>
4. <span data-ttu-id="c09c1-166">Sélectionnez **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="c09c1-167">Développez Apache et sélectionnez version hello du serveur d’Apache Tomcat hello que vous avez installé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c09c1-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="c09c1-168">Sur notre système, nous avons installé la version 8.</span><span class="sxs-lookup"><span data-stu-id="c09c1-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="c09c1-169">Sur la page suivante de hello, spécifiez le répertoire d’installation de Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="c09c1-170">Sur un ordinateur Windows, il s’agit très probablement du répertoire C:\Program Files\Apache Software Foundation\Tomcat *version*.</span><span class="sxs-lookup"><span data-stu-id="c09c1-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="c09c1-171">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-171">Click **Finish**.</span></span>
8. <span data-ttu-id="c09c1-172">Sélectionnez **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="c09c1-173">Dans **Add JRE**, sélectionnez **Standard VM**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="c09c1-174">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-174">Click **Next**.</span></span>
11. <span data-ttu-id="c09c1-175">Dans JRE Definition de la page d’accueil de JRE, cliquez sur **Directory**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="c09c1-176">Accédez trop**Program Files** > **Java** et sélectionnez hello JDK que vous avez installé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c09c1-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="c09c1-177">Il est important de tooselect hello JDK hello JRE.</span><span class="sxs-lookup"><span data-stu-id="c09c1-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="c09c1-178">Dans JRE installé, choisissez hello **JDK**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="c09c1-179">Vos paramètres doivent ressembler toohello similaire après la capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="c09c1-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="c09c1-180">Si vous le souhaitez, sélectionnez **fenêtre** > **navigateur Web** > **Internet Explorer** application hello de tooopen dans une fenêtre de navigateur externe.</span><span class="sxs-lookup"><span data-stu-id="c09c1-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="c09c1-181">Un navigateur externe vous donne une meilleure expérience de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="c09c1-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="c09c1-182">Vous avez maintenant terminé les tâches de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="c09c1-183">Ensuite, vous allez générer et exécuter des projets de hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="c09c1-184">Générez le projet de hello</span><span class="sxs-lookup"><span data-stu-id="c09c1-184">Build hello project</span></span>
1. <span data-ttu-id="c09c1-185">Dans l’Explorateur de projets, cliquez sur le nom de projet hello et choisissez **exécuter en tant que** > **build Maven...**  projet hello de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c09c1-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="c09c1-186">Dans le champ Goals de Edit Configuration, saisissez « clean install », puis cliquez sur **Run**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="c09c1-187">Messages d’état sont la fenêtre de console toohello de sortie.</span><span class="sxs-lookup"><span data-stu-id="c09c1-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="c09c1-188">Vous devez voir le projet hello indiquant de réussite des builds, généré sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="c09c1-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="c09c1-189">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="c09c1-189">Run hello app</span></span>
<span data-ttu-id="c09c1-190">Dans cette dernière étape, vous allez exécuter l’application hello dans un environnement d’exécution de serveur local.</span><span class="sxs-lookup"><span data-stu-id="c09c1-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="c09c1-191">Si vous n’avez pas encore spécifié un environnement d’exécution de serveur dans Eclipse, vous devez d’abord toodo.</span><span class="sxs-lookup"><span data-stu-id="c09c1-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="c09c1-192">Dans Project Explorer, développez **WebContent**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="c09c1-193">Cliquez avec le bouton droit sur **Search.jsp** > **Run As** > **Run on Server**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="c09c1-194">Sélectionnez hello Apache Tomcat serveur, puis cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="c09c1-195">Si vous avez utilisé un toostore de l’espace de travail par défaut de votre projet, vous devez toomodify **exécuter Configuration** toopoint toohello projet emplacement tooavoid une erreur de démarrage du serveur.</span><span class="sxs-lookup"><span data-stu-id="c09c1-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="c09c1-196">Dans Project Explorer, cliquez avec le bouton droit sur **Search.jsp** > **Run As** > **Run Configurations**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="c09c1-197">Sélectionnez serveur d’Apache Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="c09c1-198">Cliquez sur **Arguments**.</span><span class="sxs-lookup"><span data-stu-id="c09c1-198">Click **Arguments**.</span></span> <span data-ttu-id="c09c1-199">Cliquez sur **espace de travail** ou **système de fichiers** tooset dossier de hello contenant le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="c09c1-200">Lorsque vous exécutez des application hello, vous devez voir une fenêtre de navigateur, en fournissant une zone de recherche permettant d’entrer des termes du contrat.</span><span class="sxs-lookup"><span data-stu-id="c09c1-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="c09c1-201">Attendez environ une minute avant de cliquer sur **recherche** toogive hello service temps toocreate et charge hello l’index.</span><span class="sxs-lookup"><span data-stu-id="c09c1-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="c09c1-202">Si vous obtenez une erreur HTTP 404, vous devez simplement toowait un peu plus longtemps avant de réessayer.</span><span class="sxs-lookup"><span data-stu-id="c09c1-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="c09c1-203">Exécuter une recherche sur les données USGS</span><span class="sxs-lookup"><span data-stu-id="c09c1-203">Search on USGS data</span></span>
<span data-ttu-id="c09c1-204">jeu de données de groupes universels de sécurité Hello comprend les enregistrements qui sont pertinentes toohello état de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="c09c1-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="c09c1-205">Si vous cliquez sur **recherche** sur une zone de recherche vide, vous obtiendrez les entrées de 50 premiers hello, qui est la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="c09c1-206">Entrer un terme de recherche donne moteur de recherche hello quelque chose toogo sur.</span><span class="sxs-lookup"><span data-stu-id="c09c1-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="c09c1-207">Essayez d'entrer le nom d’une figure locale.</span><span class="sxs-lookup"><span data-stu-id="c09c1-207">Try entering a regional name.</span></span> <span data-ttu-id="c09c1-208">« Roger Williams » a été gouverneur de première hello de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="c09c1-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="c09c1-209">De nombreux parcs, bâtiments et écoles portent son nom.</span><span class="sxs-lookup"><span data-stu-id="c09c1-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="c09c1-210">Vous pouvez également essayer les termes suivants :</span><span class="sxs-lookup"><span data-stu-id="c09c1-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="c09c1-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="c09c1-211">Pawtucket</span></span>
* <span data-ttu-id="c09c1-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="c09c1-212">Pembroke</span></span>
* <span data-ttu-id="c09c1-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="c09c1-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="c09c1-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c09c1-214">Next steps</span></span>
<span data-ttu-id="c09c1-215">Il s’agit de premier didacticiel Azure Search hello, basée sur Java et hello dataset des groupes universels de sécurité.</span><span class="sxs-lookup"><span data-stu-id="c09c1-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="c09c1-216">Au fil du temps, nous allons étendre ce didacticiel toodemonstrate les fonctionnalités de recherche supplémentaires vous pourriez toouse dans vos solutions personnalisées.</span><span class="sxs-lookup"><span data-stu-id="c09c1-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="c09c1-217">Si vous avez déjà quelques arrière-plan dans Azure Search, vous pouvez utiliser cet exemple comme un springboard pour expérimentation supplémentaire, peut-être augmenter hello [page de recherche](search-pagination-page-layout.md), ou de l’implémentation [une navigation par facettes](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="c09c1-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="c09c1-218">Vous pouvez également améliorer sur la page de résultats hello en ajoutant des nombres et le traitement par lot des documents afin que les utilisateurs peuvent parcourir les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="c09c1-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="c09c1-219">TooAzure nouvelle recherche ?</span><span class="sxs-lookup"><span data-stu-id="c09c1-219">New tooAzure Search?</span></span> <span data-ttu-id="c09c1-220">Nous vous recommandons d’essayer d’autres toodevelop didacticiels comprendre ce que vous pouvez créer.</span><span class="sxs-lookup"><span data-stu-id="c09c1-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="c09c1-221">Visitez notre [page de documentation](https://azure.microsoft.com/documentation/services/search/) toofind davantage de ressources.</span><span class="sxs-lookup"><span data-stu-id="c09c1-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="c09c1-222">Vous pouvez également afficher les liens hello dans notre [liste vidéo et didacticiel](search-video-demo-tutorial-list.md) tooaccess plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c09c1-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
