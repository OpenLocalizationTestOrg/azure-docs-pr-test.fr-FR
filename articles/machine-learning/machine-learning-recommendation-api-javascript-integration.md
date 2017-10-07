---
title: "Machine Learning Recommendations : intégration à l’aide de JavaScript | Microsoft Docs"
description: "Azure Machine Learning Recommendations - Intégration à l’aide de JavaScript - documentation"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Azure Machine Learning Recommendations - Intégration à l’aide de JavaScript
> [!NOTE]
> Vous devez commencer à l’aide de hello Service cognitifs de recommandations API au lieu de cette version. Hello Service cognitifs recommandations remplacera ce service et toutes les hello nouvelles fonctionnalités seront développées il. Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.
> En savoir plus sur [migration toohello nouveau Service cognitifs](http://aka.ms/recomigrate)
> 
> 

Ce document décrivent comment toointegrate votre site à l’aide de JavaScript. Hello JavaScript vous permet de toosend les événements d’Acquisition de données et les recommandations de tooconsume une fois que vous générez un modèle de recommandation. Toutes les opérations effectuées via JS peuvent également être effectuées côté serveur.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Présentation générale
L’intégration de votre site avec Azure ML Recommandations se compose de 2 phases :

1. Envoi d’événements dans Azure ML Recommendations. Cette opération activera toobuild un modèle de recommandation.
2. Utiliser les recommandations hello. Après la génération de modèle de hello, vous pouvez utiliser les recommandations hello. (Ce document n’explique pas comment toobuild un modèle, lire hello tooget guide de démarrage rapide plus d’informations sur la façon de).

<ins>Phase I</ins>

Bonjour première phase, de que vous insérez dans vos pages html une petite bibliothèque JavaScript qui permet hello événements de page toosend qu’ils se produisent sur une page html de hello en tant que serveurs Azure ML recommandations (via Data Market) :

![Drawing1][1]

<ins>Phase II</ins>

Bonjour deuxième phase, lorsque vous souhaitez que les recommandations de hello tooshow sur la page de hello vous sélectionnez une des options suivantes de hello :

1. votre serveur (sur la phase de hello de rendu de page) appelle recommandations tooget de serveur de recommandations Azure ML (via Data Market). les résultats de Hello incluent une liste des id d’éléments. Votre serveur a besoin des résultats de hello tooenrich avec hello des éléments de métadonnées (par exemple, les images, description) et envoyer hello créé de page toohello navigateur.

![Drawing2][2]

2. hello autre option est toouse hello JavaScript fichier de petite taille à partir de la phase d’un tooget une simple liste d’éléments recommandés. les données de salutation reçues ici sont très optimisées à hello une option de première hello.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. Composants requis
1. Créer un modèle à l’aide des API de hello. Consultez le guide de démarrage rapide hello sur la façon de toodo il.
2. Encodez votre &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; avec base64. (Cela sera utilisé pour hello l’authentification de base tooenable hello JS code toocall hello API).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Envoyer des événements d’acquisition de données à l’aide de JavaScript
Hello suit facilite l’envoi d’événements :

1. Incluez la bibliothèque JQuery dans votre code. Vous pouvez le télécharger à partir de nuget Bonjour suivant l’URL.
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. Inclure bibliothèque de Script de recommandations Java hello de hello suivant URL : http://aka.ms/RecoJSLib1
3. Initialisation de la bibliothèque d’Azure ML recommandations avec les paramètres appropriés hello.
   
     <script>AzureMLRecommendationsStart («<base64encoding of username:key>», « < model_id > ») ; </script> 
4. Événement approprié d’envoi hello. Consultez la section détaillée ci-dessous sur tous les types d’événements (exemple d’événement Click) <script> if (typeof AzureMLRecommendationsEvent=="undefined") {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Limitations et prise en charge du navigateur
Il s’agit d’une implémentation de référence, fournie en l’état. Elle prend normalement en charge les principaux navigateurs.

### <a name="32----type-of-events"></a>3.2.    Type d’événements
Il existe 5 types d’événement qui prend en charge de la bibliothèque de hello : cliquez sur, la recommandation, cliquez sur, ajouter tooShop panier d’achat, supprimer de panier d’usine et d’achat. Il existe un événement supplémentaire qui est utilisé tooset hello utilisateur contexte appelé compte de connexion.

#### <a name="321-click-event"></a>3.2.1. Événement clic
Cet événement doit être utilisé chaque fois qu’un utilisateur clique sur un article. En général lorsque l’utilisateur clique sur un élément une nouvelle page est ouvert avec les détails de l’élément hello ; Cet événement doit être déclenché dans cette page.

Paramètres :

* event (chaîne, obligatoire) - “click”
* élément (string, obligatoire) - identificateur Unique de l’élément de hello
* nom de l’élément (string, facultatif) - nom hello d’élément de hello
* DescriptionArticle (string, facultatif) - description hello d’élément de hello
* itemCategory (string, facultatif) - catégorie hello de hello
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

Ou avec des données facultatives :

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Événement clic de recommandation
Cet événement doit être utilisé chaque fois qu’un utilisateur clique sur un article recommandé reçu à partir d’Azure ML Recommandations. En général lorsque l’utilisateur clique sur un élément une nouvelle page est ouvert avec les détails de l’élément hello ; Cet événement doit être déclenché dans cette page.

Paramètres :

* event (chaîne, obligatoire) - “recommendationclick”
* élément (string, obligatoire) - identificateur Unique de l’élément de hello
* nom de l’élément (string, facultatif) - nom hello d’élément de hello
* DescriptionArticle (string, facultatif) - description hello d’élément de hello
* itemCategory (string, facultatif) - catégorie hello de hello
* semences (tableau de chaînes, facultatif) - hello semences qui a généré la requête de recommandation hello.
* recoList (tableau de chaînes, facultatif) - hello du résultat de demande de recommandation hello qui a généré l’élément hello que l’utilisateur a cliqué.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

Ou avec des données facultatives :

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Événement ajouter au panier
Cet événement doit être utilisé lorsque l’utilisateur hello ajouter un toohello élément panier d’achat.
Paramètres :

* event (chaîne, obligatoire) - “addshopcart”
* élément (string, obligatoire) - identificateur Unique de l’élément de hello
* nom de l’élément (string, facultatif) - nom hello d’élément de hello
* DescriptionArticle (string, facultatif) - description hello d’élément de hello
* itemCategory (string, facultatif) - catégorie hello de hello
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Événement supprimer du panier
Cet événement doit être utilisé lorsque l’utilisateur de hello supprime un élément toohello panier d’achat.

Paramètres :

* event (chaîne, obligatoire) - “removeshopcart”
* élément (string, obligatoire) - identificateur Unique de l’élément de hello
* nom de l’élément (string, facultatif) - nom hello d’élément de hello
* DescriptionArticle (string, facultatif) - description hello d’élément de hello
* itemCategory (string, facultatif) - catégorie hello de hello
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Événement d’achat
Cet événement doit être utilisé lors de l’utilisateur de hello achat son panier d’achat.

Paramètres :

* event (chaîne) - “purchase”
* items ( Purchased ) - Tableau contenant une entrée pour chaque article acheté.<br><br>
  Format d’achat :
  * élément (chaîne), un identificateur Unique de l’élément de hello.
  * count (entier ou chaîne) - nombre d'articles achetés.
  * prix (float ou string) - champ facultatif - hello prix de hello.

exemple Hello ci-dessous montre l’achat de 3 éléments (33, 34, 35), deux avec tous les champs renseignés (élément, nombre, prix) et l’autre (élément 34) sans un prix.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Événement de connexion utilisateur
Azure ML événement de recommandations bibliothèque crée et utiliser un cookie dans les événements de tooidentify commande provenant hello même navigateur. Dans le modèle hello tooimprove résultats Azure ML recommandations permet tooset une identification unique utilisateur qui remplace l’utilisation du cookie hello.

Cet événement doit être utilisé après le site de tooyour de connexion de l’utilisateur hello.

Paramètres :

* event (chaîne) - “userlogin”
* utilisateur (chaîne), une identification unique de l’utilisateur de hello.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Utiliser les recommandations via JavaScript
code Hello qui consomme la recommandation de hello est déclenché par un événement JavaScript par la page Web de hello client. réponse de recommandation Hello inclut hello ID des éléments, leurs noms et leurs classements recommandés. Il s’agit des meilleures toouse cette option uniquement pour un affichage de liste de hello recommandé des éléments - plus complexes à gérer (par exemple, l’ajout de métadonnées de l’élément hello) doit être effectuée sur l’intégration de côté serveur hello.

### <a name="41-consume-recommendations"></a>4.1 Utilisation des recommandations
recommandations tooconsume que vous devez tooinclude hello requis des bibliothèques JavaScript dans votre page et de toocall AzureMLRecommendationsStart. Consultez la section 2.

recommandations tooconsume pour un ou plusieurs éléments, vous devez toocall une méthode appelée : AzureMLRecommendationsGetI2IRecommendation.

Paramètres :

* Un ou plusieurs éléments tooget recommandations relatives à des éléments (tableau de chaînes -). Si vous consommez une build Fbt, vous ne pouvez définir qu'un seul élément ici.
* numberOfResults (entier) - nombre de résultats requis.
* includeMetadata (boolean, facultatif) - si définir too'true' indique ce champ de métadonnées hello doit être rempli dans le résultat de hello.
* Fonction de traitement - une fonction qui gérera les recommandations hello renvoyées. les données de salutation sont retournées sous forme de tableau de :
  * Item - ID unique de l’élément
  * name - nom de l'élément (s’il existe dans le catalogue)
  * rating - évaluation de la recommandation
  * métadonnées - une chaîne qui représente les métadonnées d’élément de hello hello

Exemple : hello suivant code demande 8 recommandations pour l’élément « 64f6eb0d-947a-4c18-a16c-888da9e228ba » (et en ne spécifiant includeMetadata - implicitement indique qu’aucune métadonnée n’est nécessaire), puis, il concaténer les résultats hello dans une mémoire tampon.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
