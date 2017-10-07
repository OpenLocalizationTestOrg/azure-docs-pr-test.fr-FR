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
# <a name="get-started-with-azure-search-in-java"></a>Prise en main d'Azure Search dans Java
> [!div class="op_single_selector"]
> * [Portail](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Découvrez comment toobuild Java personnalisé recherche application qui utilise Azure Search pour son expérience de recherche. Ce didacticiel utilise hello [API REST de Service Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello des objets et les opérations utilisées dans cet exercice.

toorun cet exemple, vous devez disposer un service Azure Search, vous pouvez vous connecter à hello [Azure Portal](https://portal.azure.com). Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) pour obtenir des instructions pas à pas.

Nous utilisé hello suivant logiciel toobuild et tester cet exemple :

* [Environnement de développement intégré (IDE) Eclipse pour développeurs Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). La version Java EE hello toodownload vraiment être. Une des étapes de vérification hello nécessite une fonctionnalité qui se trouve uniquement dans cette édition.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>Sur les données de salutation
Cet exemple d’application utilise des données de hello [États-Unis géologique Services (USG)](http://geonames.usgs.gov/domestic/download_data.htm), filtrée sur la taille du jeu de données hello état de Rhode Island tooreduce hello. Nous utiliserons cette toobuild données une application de recherche qui retourne les bâtiments repère telles que le nombre et écoles, ainsi que les fonctionnalités géologiques, flux, lacs et sommets.

Dans cette application, hello **SearchServlet.java** programme génère et charges hello à l’aide de l’index une [indexeur](https://msdn.microsoft.com/library/azure/dn798918.aspx) construction, la récupération hello filtré des groupes universels de sécurité de groupe de données à partir d’une base de données SQL Azure publique. Les informations d’identification prédéfinies et de la source de données en ligne de connexion informations toohello sont fournies dans le code de programme hello. Pour accéder aux données, aucune configuration supplémentaire n'est nécessaire.

> [!NOTE]
> Nous avons appliqué un filtre sur cette toostay dataset sous limite de document 10 000 hello Hello libre niveau tarifaire. Si vous utilisez le niveau standard de hello, cette limite ne s’applique pas, et vous pouvez modifier ce code de toouse un plus grand jeu de données. Pour plus d'informations sur la capacité de chaque niveau de tarification, consultez la section [Limites et contraintes](search-limits-quotas-capacity.md).
> 
> 

## <a name="about-hello-program-files"></a>À propos des fichiers de programme hello
Hello liste suivante décrit les fichiers hello qui sont pertinentes toothis échantillon.

* Search.jsp : Fournit l’interface utilisateur de hello
* SearchServlet.java : Fournit des méthodes (similaire tooa contrôleur MVC)
* SearchServiceClient.java : gère les descripteurs HTTP.
* SearchServiceHelper.java : classe d’utilitaire qui fournit des méthodes statiques.
* Document.Java : Fournit le modèle de données hello
* config.Properties : définit l’URL du service recherche hello et clé d’api
* Pom.XML : dépendance Maven.

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Rechercher le nom du service hello et la clé api de votre service Azure Search
Tous les appels d’API REST dans Azure Search nécessitent que vous fournissiez hello URL du service et une clé d’api. 

1. Connectez-vous à toohello [Azure Portal](https://portal.azure.com).
2. Dans la barre de saut hello, cliquez sur **service de recherche** toolist tous les services d’Azure Search hello définis pour votre abonnement.
3. Sélectionnez le service hello toouse.
4. Tableau de bord de service hello, vous verrez des vignettes pour des informations essentielles ainsi qu’icône de clé hello pour accéder aux clés d’administration hello.
   
      ![][3]
5. Copiez l’URL du service hello et une clé d’administration. Vous en aurez besoin plus tard, lorsque vous les ajoutez toohello **config.Properties** fichier.

## <a name="download-hello-sample-files"></a>Télécharger les fichiers d’exemple hello
1. Accédez trop[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) sur GitHub.
2. Cliquez sur **ZIP de téléchargement**, enregistrer toodisk de fichier .zip hello, puis extraire tous les fichiers hello qu’il contient. Envisagez l’extraction hello fichiers dans votre toomake d’espace de travail Java qu’il plus facile projet de hello toofind plus tard.
3. fichiers d’exemple Hello sont en lecture seule. Cliquez sur Propriétés du dossier et désactivez hello en lecture seule.

Toutes les modifications et instructions d'exécution ultérieures seront effectuées sur les fichiers de ce dossier.  

## <a name="import-project"></a>Importer le projet
1. Dans Eclipse, choisissez **File** > **Import** > **General** > **Existing Projects into Workspace**.
   
    ![][4]
2. Dans **répertoire racine sélectionnez**, parcourir le dossier toohello contenant des exemples de fichiers. Sélectionnez le dossier hello qui contient le dossier de .project hello. projet de Hello doit apparaître dans hello **projets** liste comme un élément sélectionné.
   
    ![][12]
3. Cliquez sur **Terminer**.
4. Utilisez **Explorateur de projets** tooview et modifier les fichiers hello. Si elle n’est pas déjà ouverte, cliquez sur **fenêtre** > **afficher la vue** > **Explorateur de projets** ou utilisez hello contextuel tooopen il.

## <a name="configure-hello-service-url-and-api-key"></a>Configurer l’URL du service hello et clé d’api
1. Dans **Explorateur de projets**, double-cliquez sur **config.Properties** tooedit hello de configuration qui contient le nom du serveur hello et clé d’api.
2. Consultez les étapes toohello plus haut dans cet article, où vous avez trouvé hello URL du service et la clé d’api dans hello [portail Azure](https://portal.azure.com), les valeurs de hello tooget vous entrerez dans **config.Properties**.
3. Dans **config.Properties**, remplacez « Clé Api » avec la clé api hello pour votre service. Ensuite, le nom de service (hello premier composant du hello URL http://servicename.search.windows.net) remplace le « nom du service » Bonjour même fichier.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Configurez des environnements de projet, de génération et d’exécution hello
1. Dans Eclipse, dans l’Explorateur de projets, cliquez sur projet de hello > **propriétés** > **projet facettes**.
2. Sélectionnez **Dynamic Web Module**, **Java** et **JavaScript**.
   
    ![][6]
3. Cliquez sur **Apply**.
4. Sélectionnez **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.
5. Développez Apache et sélectionnez version hello du serveur d’Apache Tomcat hello que vous avez installé précédemment. Sur notre système, nous avons installé la version 8.
   
    ![][7]
6. Sur la page suivante de hello, spécifiez le répertoire d’installation de Tomcat hello. Sur un ordinateur Windows, il s’agit très probablement du répertoire C:\Program Files\Apache Software Foundation\Tomcat *version*.
7. Cliquez sur **Terminer**.
8. Sélectionnez **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.
9. Dans **Add JRE**, sélectionnez **Standard VM**.
10. Cliquez sur **Suivant**.
11. Dans JRE Definition de la page d’accueil de JRE, cliquez sur **Directory**.
12. Accédez trop**Program Files** > **Java** et sélectionnez hello JDK que vous avez installé précédemment. Il est important de tooselect hello JDK hello JRE.
13. Dans JRE installé, choisissez hello **JDK**. Vos paramètres doivent ressembler toohello similaire après la capture d’écran.
    
    ![][9]
14. Si vous le souhaitez, sélectionnez **fenêtre** > **navigateur Web** > **Internet Explorer** application hello de tooopen dans une fenêtre de navigateur externe. Un navigateur externe vous donne une meilleure expérience de l’application Web.
    
    ![][8]

Vous avez maintenant terminé les tâches de configuration hello. Ensuite, vous allez générer et exécuter des projets de hello.

## <a name="build-hello-project"></a>Générez le projet de hello
1. Dans l’Explorateur de projets, cliquez sur le nom de projet hello et choisissez **exécuter en tant que** > **build Maven...**  projet hello de tooconfigure.
   
    ![][10]
2. Dans le champ Goals de Edit Configuration, saisissez « clean install », puis cliquez sur **Run**.

Messages d’état sont la fenêtre de console toohello de sortie. Vous devez voir le projet hello indiquant de réussite des builds, généré sans erreurs.

## <a name="run-hello-app"></a>Exécutez l’application hello
Dans cette dernière étape, vous allez exécuter l’application hello dans un environnement d’exécution de serveur local.

Si vous n’avez pas encore spécifié un environnement d’exécution de serveur dans Eclipse, vous devez d’abord toodo.

1. Dans Project Explorer, développez **WebContent**.
2. Cliquez avec le bouton droit sur **Search.jsp** > **Run As** > **Run on Server**. Sélectionnez hello Apache Tomcat serveur, puis cliquez sur **exécuter**.

> [!TIP]
> Si vous avez utilisé un toostore de l’espace de travail par défaut de votre projet, vous devez toomodify **exécuter Configuration** toopoint toohello projet emplacement tooavoid une erreur de démarrage du serveur. Dans Project Explorer, cliquez avec le bouton droit sur **Search.jsp** > **Run As** > **Run Configurations**. Sélectionnez serveur d’Apache Tomcat hello. Cliquez sur **Arguments**. Cliquez sur **espace de travail** ou **système de fichiers** tooset dossier de hello contenant le projet de hello.
> 
> 

Lorsque vous exécutez des application hello, vous devez voir une fenêtre de navigateur, en fournissant une zone de recherche permettant d’entrer des termes du contrat.

Attendez environ une minute avant de cliquer sur **recherche** toogive hello service temps toocreate et charge hello l’index. Si vous obtenez une erreur HTTP 404, vous devez simplement toowait un peu plus longtemps avant de réessayer.

## <a name="search-on-usgs-data"></a>Exécuter une recherche sur les données USGS
jeu de données de groupes universels de sécurité Hello comprend les enregistrements qui sont pertinentes toohello état de Rhode Island. Si vous cliquez sur **recherche** sur une zone de recherche vide, vous obtiendrez les entrées de 50 premiers hello, qui est la valeur par défaut hello.

Entrer un terme de recherche donne moteur de recherche hello quelque chose toogo sur. Essayez d'entrer le nom d’une figure locale. « Roger Williams » a été gouverneur de première hello de Rhode Island. De nombreux parcs, bâtiments et écoles portent son nom.

![][11]

Vous pouvez également essayer les termes suivants :

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Étapes suivantes
Il s’agit de premier didacticiel Azure Search hello, basée sur Java et hello dataset des groupes universels de sécurité. Au fil du temps, nous allons étendre ce didacticiel toodemonstrate les fonctionnalités de recherche supplémentaires vous pourriez toouse dans vos solutions personnalisées.

Si vous avez déjà quelques arrière-plan dans Azure Search, vous pouvez utiliser cet exemple comme un springboard pour expérimentation supplémentaire, peut-être augmenter hello [page de recherche](search-pagination-page-layout.md), ou de l’implémentation [une navigation par facettes](search-faceted-navigation.md). Vous pouvez également améliorer sur la page de résultats hello en ajoutant des nombres et le traitement par lot des documents afin que les utilisateurs peuvent parcourir les résultats de hello.

TooAzure nouvelle recherche ? Nous vous recommandons d’essayer d’autres toodevelop didacticiels comprendre ce que vous pouvez créer. Visitez notre [page de documentation](https://azure.microsoft.com/documentation/services/search/) toofind davantage de ressources. Vous pouvez également afficher les liens hello dans notre [liste vidéo et didacticiel](search-video-demo-tutorial-list.md) tooaccess plus d’informations.

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
