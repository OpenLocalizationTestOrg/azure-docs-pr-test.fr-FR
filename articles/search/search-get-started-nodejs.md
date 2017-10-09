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
# <a name="get-started-with-azure-search-in-nodejs"></a>Prise en main d’Azure Search dans Node.js
> [!div class="op_single_selector"]
> * [Portail](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Découvrez comment toobuild un Node.js personnalisé recherche application qui utilise Azure Search pour son expérience de recherche. Ce didacticiel utilise hello [API REST de Service Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello des objets et les opérations utilisées dans cet exercice.

Nous avons utilisé [Node.js](https://Nodejs.org) et NPM, [Sublime texte 3](http://www.sublimetext.com/3)et Windows PowerShell sur Windows 8.1 toodevelop et tester ce code.

toorun cet exemple, vous devez disposer un service Azure Search, vous pouvez vous connecter à hello [portail Azure](https://portal.azure.com). Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) pour obtenir des instructions pas à pas.

## <a name="about-hello-data"></a>Sur les données de salutation
Cet exemple d’application utilise des données de hello [États-Unis géologique Services (USG)](http://geonames.usgs.gov/domestic/download_data.htm), filtrée sur la taille du jeu de données hello état de Rhode Island tooreduce hello. Nous utiliserons cette toobuild données une application de recherche qui retourne les bâtiments repère telles que le nombre et écoles, ainsi que les fonctionnalités géologiques, flux, lacs et sommets.

Dans cette application, hello **DataIndexer** programme génère et charges hello à l’aide de l’index une [indexeur](https://msdn.microsoft.com/library/azure/dn798918.aspx) construction, la récupération hello filtré des groupes universels de sécurité de groupe de données à partir d’une base de données SQL Azure publique. Informations d’identification et de connexion de source de données en ligne d’informations toohello est fourni dans le code de programme hello. Aucune configuration supplémentaire n'est nécessaire.

> [!NOTE]
> Nous avons appliqué un filtre sur cette toostay dataset sous limite de document 10 000 hello Hello libre niveau tarifaire. Si vous utilisez le niveau standard de hello, cette limite ne s’applique pas. Pour plus d’informations sur la capacité de chaque niveau de tarification, consultez la page [Limites de service d’Azure Search](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Rechercher le nom du service hello et la clé api de votre service Azure Search
Après avoir créé le service de hello, retourner toohello tooget portail hello URL ou `api-key`. Connexions tooyour service de recherche nécessitent que vous avez les deux URL hello et un `api-key` appel de hello tooauthenticate.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans la barre de saut hello, cliquez sur **service de recherche** toolist tous les services Azure Search est configurés pour votre abonnement.
3. Sélectionnez le service hello toouse.
4. Tableau de bord de service hello, vous devez voir les vignettes pour des informations essentielles, telles que de l’icône de clé hello pour accéder aux clés d’administration hello.
5. Copiez l’URL du service hello, une clé d’administration et une clé de requête. Vous avez besoin de trois lorsque vous les ajoutez toohello config.js fichier.

## <a name="download-hello-sample-files"></a>Télécharger les fichiers d’exemple hello
Utilisez l’un des hello suivant approches toodownload hello, exemple.

1. Accédez trop[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Cliquez sur **ZIP de téléchargement**, enregistrez le fichier .zip de hello, puis extraire tous les fichiers hello qu’il contient.

Toutes les modifications et instructions d’exécution ultérieures seront effectuées sur les fichiers de ce dossier.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Mettre à jour hello config.js. avec l’URL et la clé API du service de recherche
À l’aide de hello URL et la clé d’api que vous avez copiée précédemment, spécifier des URL hello, clé d’administration et de clé de requête dans le fichier de configuration.

Les clés d’administration octroient un contrôle total sur les opérations du service, notamment la création ou la suppression d'un index et le chargement de documents. En revanche, les clés de requête sont pour les opérations en lecture seule, généralement utilisées par les applications clientes qui se connectent tooAzure recherche.

Dans cet exemple, nous incluons requête hello toohelp clé renforcer hello meilleure pratique qui consiste à l’aide de la clé de requête hello dans les applications clientes.

Hello ci-dessous capture d’écran illustre **config.js** ouvert dans un éditeur de texte avec hello pertinentes entrées délimitées afin que vous puissiez voir où le fichier hello tooupdate hello valeurs qui sont valides pour votre service de recherche.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Héberger un environnement d’exécution de l’exemple hello
exemple Hello nécessite un serveur HTTP, que vous pouvez installer globalement à l’aide de npm.

Utiliser une fenêtre PowerShell pour hello suivant les commandes.

1. Exploration du dossier toohello contenant hello **package.json** fichier.
2. Saisissez `npm install`.
3. Saisissez `npm install -g http-server`.

## <a name="build-hello-index-and-run-hello-application"></a>Créer des index de hello et exécuter l’application hello
1. Saisissez `npm run indexDocuments`.
2. Saisissez `npm run build`.
3. Saisissez `npm run start_server`.
4. Dans votre navigateur, accédez à `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Exécuter une recherche sur les données USGS
jeu de données de groupes universels de sécurité Hello comprend les enregistrements qui sont pertinentes toohello état de Rhode Island. Si vous cliquez sur **recherche** sur une zone de recherche vide, vous obtenez hello 50 premières entrées, qui est la valeur par défaut hello.

Entrer un terme de recherche donne moteur de recherche hello quelque chose toogo sur. Essayez d'entrer le nom d’une figure locale. « Roger Williams » a été gouverneur de première hello de Rhode Island. De nombreux parcs, bâtiments et écoles portent son nom.

![][9]

Vous pouvez également essayer les termes suivants :

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Étapes suivantes
Il s’agit de premier didacticiel Azure Search hello, en fonction de Node.js et hello dataset des groupes universels de sécurité. Au fil du temps, nous allons étendre ce didacticiel toodemonstrate les fonctionnalités de recherche supplémentaires vous pourriez toouse dans vos solutions personnalisées.

Si vous connaissez déjà Azure Search, vous pouvez utiliser cet exemple comme tremplin pour tester des générateurs de suggestions (requêtes prédictives ou à saisie semi-automatique), des filtres et la navigation à facettes. Vous pouvez également améliorer sur la page de résultats hello en ajoutant des nombres et le traitement par lot des documents afin que les utilisateurs peuvent parcourir les résultats de hello.

TooAzure nouvelle recherche ? Nous vous recommandons d’essayer d’autres toodevelop didacticiels comprendre ce que vous pouvez créer. Visitez notre [page de documentation](https://azure.microsoft.com/documentation/services/search/) toofind davantage de ressources. Vous pouvez également afficher les liens hello dans notre [liste vidéo et didacticiel](search-video-demo-tutorial-list.md) tooaccess plus d’informations.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
