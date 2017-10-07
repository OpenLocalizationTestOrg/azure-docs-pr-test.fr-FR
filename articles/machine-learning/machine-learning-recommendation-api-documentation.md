---
title: "aaaMachine Documentation de l’API Learning recommandations | Documents Microsoft"
description: Documentation Azure Machine Learning recommandations API sur un moteur de recommandations Bonjour Microsoft Azure Marketplace.
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a>Documentation sur les API Azure Machine Learning Recommendations
> [!NOTE]
> Vous devez commencer à l’aide de hello Service cognitifs de recommandations API au lieu de cette version. Hello Service cognitifs recommandations remplacera ce service et toutes les hello nouvelles fonctionnalités seront développées il. Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.
> En savoir plus sur [migration toohello nouveau Service cognitifs](http://aka.ms/recomigrate)
> 
> 

Ce document décrit les API Microsoft Azure Machine Learning Recommendations.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Présentation générale
Ce document fait référence aux API. Vous devez commencer par hello « Azure Machine Learning recommandation – document démarrage rapide ».

Bonjour Azure Machine Learning recommandations API peut être divisé en hello groupes logiques suivants :

* <ins>Limitations</ins> : limitations concernant les API Recommandations.
* <ins>Informations générales</ins> : informations sur l'authentification, l’URI de service et le contrôle de version.
* <ins>Modèle Basic</ins> -API qui vous permettent aux opérations de base hello toodo sur le modèle (par exemple, créer, mettre à jour et supprimer un modèle).
* <ins>Modèle avancé</ins> -API qui vous permettent de tooget avancée des analyses de données sur le modèle de hello.
* <ins>Modèle de règles d’entreprise</ins> -API qui vous permettent de toomanage des règles d’entreprise sur les résultats de recommandation modèle hello.
* <ins>Catalogue</ins> -API qui vous permettent de toodo les opérations de base sur un catalogue de modèle. Un catalogue contient des informations de métadonnées sur les éléments hello hello des données d’utilisation.
* <ins>Fonctionnalité</ins> -API qui permettent aux tooget des informations sur l’élément dans le catalogue de hello et comment toouse ce recommandations de meilleure toobuild plus d’informations.
* <ins>Les données d’utilisation</ins> -API qui vous permettent de toodo les opérations de base de données d’utilisation du modèle hello. Données d’utilisation dans un formulaire de base hello se composent de lignes qui incluent des paires de &#60; userId &#62; &#60; itemId &#62;.
* <ins>Build</ins> - API qui permettent de vous tootrigger un modèle de build et effectuer des opérations de base qui sont associées toothis la build. Vous pouvez déclencher une build de modèle dès que vous avez des données d'utilisation utiles.
* <ins>Recommandation</ins> -API qui permettent de vous tooconsume recommandations une fois la build hello d’un modèle se termine.
* <ins>Données utilisateur</ins> -API qui vous permettent de toofetch plus d’informations sur les données utilisateur hello.
* <ins>Notifications</ins> -API qui permettent de vous tooreceive des notifications sur les problèmes liés à tooyour API operations. (Par exemple, vous signalez via l’Acquisition de données et la plupart des événements hello échouent le traitement des données d’utilisation. une notification d'erreur est déclenchée.)

## <a name="2-limitations"></a>2. Limites
* nombre maximal de Hello de modèles par abonnement est 10.
* Hello le nombre maximal de builds par modèle est 20.
* nombre maximal de Hello d’éléments pouvant être un catalogue est 100 000.
* nombre maximal de Hello de points d’utilisation qui sont conservés est ~ 5 000 000. Hello plus ancien est supprimé si nouveaux sera téléchargé ou signalé.
* taille maximale de Hello des données qui peuvent être envoyées dans la publication (par exemple, importation de données du catalogue, importer des données d’utilisation) est de 200 Mo.
* nombre maximal de Hello d’éléments pouvant être posées pour lors de l’obtention de recommandations est 150.

## <a name="3-apis---general-information"></a>3. API – Informations générales
### <a name="31-authentication"></a>3.1. Authentification
Suivez les instructions de Microsoft Azure Marketplace hello concernant l’authentification. marketplace de Hello prend en charge une méthode d’authentification de base ou OAuth hello.

### <a name="32-service-uri"></a>3.2. URI de service
URI de racine de service Hello pour hello Azure Machine Learning recommandations API est [ici.](https://api.datamarket.azure.com/amla/recommendations/v3/)

URI de service complet Hello est exprimée à l’aide des éléments de spécification d’OData hello.  

### <a name="33-api-version"></a>3.3. Version de l'API
Chaque appel d’API ont à la fin de hello, un paramètre de requête appelé apiVersion qui doit être définie à too1.0.

### <a name="34-ids-are-case-sensitive"></a>3.4. Respect de la casse des ID
ID, retournés par une des API, de hello respectent la casse et doivent être utilisées comme telles lorsqu’il est passé en tant que paramètres dans les appels d’API suivants. Par exemple, les ID de modèle et de catalogue respectent la casse.

## <a name="4-recommendations-quality-and-cold-items"></a>4. Qualité des recommandations et éléments froids
### <a name="41-recommendation-quality"></a>4.1. Qualité de la recommandation
Création d’un modèle de recommandation est généralement suffisamment tooallow hello recommandations système tooprovide s’appliquent. Néanmoins, de qualité de la recommandation varie selon l’utilisation de hello traitée et hello couverture du catalogue de hello. Par exemple si vous avez un grand nombre d’éléments froids (éléments sans significatif d’utilisation), hello système n’aura des difficultés en fournissant une recommandation pour cet élément ou à l’aide de cet élément en tant que recommandée. Dans tooovercome hello à froid élément problème système de hello autorise l’utilisation de hello de métadonnées de recommandations de hello éléments tooenhance hello. Ces métadonnées sont les fonctionnalités tooas référencé. L'auteur d'un livre et l'acteur d'un film sont des exemples de caractéristiques. Fonctionnalités sont fournies via le catalogue hello sous forme de hello de chaînes clé/valeur. Pour le formatage complet de hello hello du fichier de catalogue, consultez toohello [importer section catalogue](#81-import-catalog-data). 

### <a name="42-rank-build"></a>4.2. Build de classement
Fonctionnalités peuvent améliorer le modèle de recommandation hello, mais toodo requiert utilisez hello des fonctionnalités significatives. Dans cette optique, une nouvelle build a été introduite : la build de classement. Cette build sera rank utilité hello de fonctionnalités. Une caractéristique est significative si elle reçoit un score d'au moins 2 de la build de classement.
Après avoir comprenant les fonctionnalités de hello sont significatifs, déclencher une build de recommandation avec la liste de hello (ou sous-liste) des fonctionnalités significatives. Il est possible de toouse que ces fonctionnalités pour améliorer les articles à chaud et à froid hello. Dans l’ordre toouse pour les éléments à chaud, hello `UseFeatureInModel` paramètre de build doit être configuré. Dans les fonctions toouse de commande pour les éléments froids, hello `AllowColdItemPlacement` paramètre de build doit être activé.
Remarque : Il n’est pas possible de tooenable `AllowColdItemPlacement` sans activer `UseFeatureInModel`.

### <a name="43-recommendation-reasoning"></a>4.3. Raisonnement de la recommandation
Le raisonnement de la recommandation est un autre aspect de l'utilisation des caractéristiques. En effet, moteur d’Azure Machine Learning recommandations de hello peut utiliser les explications de recommandation fonctionnalités tooprovide (aussi appelé) Raisonnement), les meilleures toomore confiance hello recommandé élément consommateur de recommandation hello.
tooenable raisonnement, hello `AllowFeatureCorrelation` et `ReasoningFeatureList` paramètres doivent être le programme d’installation toorequesting préalable une build de recommandation.

## <a name="5-model-basic"></a>5. Modèle – De base
### <a name="51-create-model"></a>5.1. Création de modèle
Crée une demande de création de modèle.

| Méthode HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelName |Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.<br>Longueur maximale : 20 |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

* `feed/entry/content/properties/id`-Contient l’ID de modèle hello.
  **Remarque**: l'ID du modèle respecte la casse.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="52-get-model"></a>5.2. Obtention de modèle
Crée une demande d'obtention de modèle.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemple :<br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| id |Identificateur unique du modèle hello (sensible à la casse) |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

Vous trouverez des données de modèle Hello sous hello suivant d’éléments :

* `feed/entry/content/properties/Id` : ID unique du modèle.
* `feed/entry/content/properties/Name` : nom du modèle.
* `feed/entry/content/properties/Date` : date de création du modèle.
* `feed/entry/content/properties/Status` : état du modèle. Une des manières de hello suivantes :
  * Created : le modèle est créé, mais il ne contient pas de données de catalogue et d'utilisation.
  * ReadyForBuild : le modèle est créé et contient des données de catalogue et d’utilisation.
* `feed/entry/content/properties/HasActiveBuild`-Indique si le modèle de hello a été généré correctement.
* `feed/entry/content/properties/BuildId` : ID de build active du modèle.
* `feed/entry/content/properties/Mpr` : classement centile moyen du modèle (MPR, Mean Percentile Ranking ; pour plus d’informations, voir ModelInsight).
* `feed/entry/content/properties/UserName` : nom d’utilisateur interne du modèle.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a>5.3.    Obtention de tous les modèles
Récupère tous les modèles de l’utilisateur actuel hello.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br>Exemple :<br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

* `feed/entry/content/properties/Id` : ID unique du modèle.
* `feed/entry/content/properties/Name` : nom du modèle.
* `feed/entry/content/properties/Date` : date de création du modèle.
* `feed/entry/content/properties/Status` : état du modèle. Une des manières de hello suivantes :
  * Created : le modèle est créé, mais il ne contient pas de données de catalogue et d'utilisation.
  * ReadyForBuild : le modèle est créé et contient des données de catalogue et d’utilisation.
* `feed/entry/content/properties/HasActiveBuild`-Indique si le modèle de hello a été généré correctement.
* `feed/entry/content/properties/BuildId` : ID de build active du modèle.
* `feed/entry/content/properties/Mpr` : MPR du modèle (pour plus d’informations, voir ModelInsight).
* `feed/entry/content/properties/UserName` : nom d’utilisateur interne du modèle.
* `feed/entry/content/properties/UsageFileNames` : liste de fichiers d’utilisation du modèle séparés par des virgules.
* `feed/entry/content/properties/CatalogId` : ID de catalogue du modèle.
* `feed/entry/content/properties/Description` : description du modèle.
* `feed/entry/content/properties/CatalogFileName` : nom de fichier de catalogue du modèle.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a>5.4.    Mise à jour du modèle
Vous pouvez mettre à jour la description du modèle hello ou hello ID de génération active.<br>
<ins>Identifiant de build active</ins> : pour chaque modèle, chaque build possède un identifiant de build. ID de build active Hello est hello première génération réussie de chaque nouveau modèle. Une fois que vous avez un ID de build active et vous faire d’autres builds pour hello même modèle, vous devez tooexplicitly définir comme hello par défaut ID de build si vous le souhaitez. Lorsque vous consommez des recommandations, si vous ne spécifiez pas d’ID de build hello toouse, un est utilisé automatiquement de la valeur par défaut hello souhaitées.<br>
Ce mécanisme vous permet de - une fois que vous disposez d’un modèle de recommandation en production - toobuild de nouveaux modèles et les testez avant de les promouvoir tooproduction.

| Méthode HTTP | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br>Exemple :<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| id |Identificateur unique du modèle hello (sensible à la casse) |
| apiVersion |1.0 |
|  | |
| Corps de la requête |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br>Notez que la Description des balises XML de hello et ActiveBuildId sont facultatifs. Si vous ne souhaitez pas tooset Description ou ActiveBuildId, supprimez la balise dans son ensemble hello. |

**Réponse**:

Code d'état HTTP : 200

### <a name="55----delete-model"></a>5.5.    Suppression de modèle
Supprime un modèle existant par ID.

| Méthode HTTP | URI |
|:--- |:--- |
| SUPPRIMER |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemple :<br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| id |Identificateur unique du modèle hello (sensible à la casse) |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a>6. Modèle – Avancé
### <a name="61----model-data-insight"></a>6.1.    Analyse des données de modèle
Renvoie des données statistiques sur les données d’utilisation de hello ce modèle a été généré à l’aide.

Disponible uniquement pour la build de recommandation.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemple :<br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

les données de salutation sont retournées comme une collection de propriétés.

* `feed/entry/id/content/properties/key`-Contient le nom de la propriété hello.
* `feed/entry/id/content/properties/value`-Contient la valeur de la propriété hello.

tableau Hello ci-dessous représente la valeur hello représentant chaque clé.

| Clé | Description |
|:--- |:--- |
| AvgItemLength |Nombre moyen d'utilisateurs distincts par élément. |
| AvgUserLength |Nombre moyen d'éléments distincts par utilisateur. |
| DensificationNumberOfItems |Nombre d'éléments après nettoyage des éléments ne pouvant pas être modélisés. |
| DensificationNumberOfUsers |Nombre de points d'utilisation après nettoyage des utilisateurs et des éléments ne pouvant pas être modélisés. |
| DensificationNumberOfRecords |Nombre de points d'utilisation après nettoyage des utilisateurs et des éléments ne pouvant pas être modélisés. |
| MaxItemLength |Nombre d’utilisateurs distincts pour les éléments les plus populaires hello. |
| MaxUserLength |Nombre maximal d'éléments distincts pour un utilisateur. |
| MinItemLength |Nombre maximal d'utilisateurs distincts pour un élément. |
| MinUserLength |Nombre minimal d'éléments distincts pour un utilisateur. |
| RawNumberOfItems |Nombre d’éléments dans les fichiers d’utilisation de hello. |
| RawNumberOfUsers |Nombre de points d'utilisation avant nettoyage. |
| RawNumberOfRecords |Nombre de points d'utilisation avant nettoyage. |
| SamplingNumberOfItems |N/A |
| SamplingNumberOfRecords |N/A |
| SamplingNumberOfUsers |N/A |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a>6.2.    Informations de modèle
Retourne le modèle insight sur build active de hello ou (si) sur une build spécifique.

Disponible uniquement pour la build de recommandation.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |Avec une ID de build active :<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Avec l’ID de build spécifique :<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| buildId |Facultatif ; numéro qui identifie une build réussie. |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

les données de salutation sont retournées comme une collection de propriétés.

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

tableau Hello ci-dessous représente la valeur hello représentant chaque clé.

| Clé | Description |
|:--- |:--- |
| CatalogCoverage |Partie du catalogue de hello peut être modelée avec les modèles d’utilisation. Hello des autres hello éléments devez fonctionnalités basées sur le contenu. |
| Mpr |Classement de centile moyenne du modèle de hello. Plus la valeur est faible, mieux c'est. |
| NumberOfDimensions |Nombre de dimensions utilisées par l’algorithme une factorisation de matrice hello. |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a>6.3.    Obtention d'exemple de modèle
Obtient un exemple de modèle de recommandation hello.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemple :<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Avec l’ID de build spécifique :<br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br>Exemple :<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

OData XML

La réponse est retournée au format texte brut :

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a>7. Règles métiers de modèle
Il s’agit de types hello de règles prises en charge :

* <strong>Liste de blocage</strong> -blocage vous permet de tooprovide une liste d’éléments que vous ne voulez pas tooreturn dans les résultats de recommandation hello. 
* <strong>FeatureBlockList</strong> -fonctionnalité de blocage permet de vous tooblock les éléments selon les valeurs hello de ses fonctionnalités.

*N’envoyez pas plus de 1 000 éléments dans une même règle de liste de blocage, car votre appel pourrait dépasser le délai d’attente. Si vous devez tooblock plus de 1 000 éléments, vous pouvez effectuer plusieurs appels de blocage.*

* <strong>Incitatives</strong> -incitatives vous permet de tooreturn d’éléments tooenforce dans les résultats de recommandation hello.
* <strong>Liste blanche</strong> -permet de liste blanche tooonly vous proposer des recommandations à partir d’une liste d’éléments.
* <strong>FeatureWhiteList</strong> -liste d’autorisation de fonction vous permet de tooonly conseillé d’éléments qui ont des valeurs de fonctionnalité spécifique.
* <strong>PerSeedBlockList</strong> - par permet de liste de blocs de valeur initiale vous tooprovide par une liste d’éléments qui ne peuvent pas être retournés sous forme de résultats de la recommandation d’élément.

### <a name="71----get-model-rules"></a>7.1.    Obtention de règles de modèle
| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemple :<br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

* `feed/entry/content/properties/Id` : identificateur unique de cette règle.
* `feed/entry/content/properties/Type`-Type de règle de hello.
* `feed/entry/content/properties/Parameter` : paramètre de la règle.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a>7.2.    Ajout de règle
| Méthode HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Corps de la requête | |

<ins>Chaque fois que des règles d’entreprise, en fournissant les ID d’élément, assurez-vous que toouse hello externe d’Id d’élément de hello (hello même Id que vous avez utilisé dans le fichier de catalogue hello)</ins><br>
<ins>tooadd une règle de blocage :</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd une règle FeatureBlockList :</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><ins>tooadd une règle incitatives :</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<ins>tooadd une règle d’autorisation :</ins><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd une règle FeatureWhiteList :</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><ins>tooadd une règle PerSeedBlockList :</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

**Réponse**:

Code d'état HTTP : 200

Hello API renvoie hello nouvellement créé règle ses détails. propriété de règles Hello peut être extraites de hello suivant des chemins d’accès :

* `feed/entry/content/properties/Id` : identificateur unique de cette règle.
* `feed/entry/content/properties/Type`-Type de règle de hello : liste de blocage ou incitatives.
* `feed/entry/content/properties/Parameter` : paramètre de la règle.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a>7.3.    Suppression de règle
| Méthode HTTP | URI |
|:--- |:--- |
| SUPPRIMER |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| filterId |Identificateur unique de filtre de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

### <a name="74----delete-all-rules"></a>7.4.    Suppression de toutes les règles
| Méthode HTTP | URI |
|:--- |:--- |
| SUPPRIMER |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

## <a name="8-catalog"></a>8. Catalogue
### <a name="81----import-catalog-data"></a>8.1.    Importation de données de catalogue
Si vous téléchargez plusieurs catalogue fichiers toohello même modèle avec plusieurs appels, il insère uniquement hello nouveaux éléments de catalogue. Éléments existants resteront avec les valeurs d’origine hello. Vous ne pouvez pas mettre à jour des données de catalogue à l'aide de cette méthode.

les données du catalogue Hello doivent suivre hello suivant le format suivant :

* Sans caractéristiques : `<Item Id>,<Item Name>,<Item Category>[,<Description>]`
* Avec caractéristiques : `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`

Remarque : la taille de fichier maximale hello est 200 Mo.

** Détails du format **

| Nom | Obligatoire | Type | Description |
|:--- |:--- |:--- |:--- |
| Item Id |Oui |[A-z], [a-z], [0-9], [_] &#40;trait de soulignement&#41;, [-] &#40;tiret&#41;<br> Longueur maximale : 50 |Identificateur unique d'un élément. |
| Item Name |Oui |Caractères alphanumériques<br> Longueur maximale : 255 |Nom de l'élément. |
| Item Category |Oui |Caractères alphanumériques <br> Longueur maximale : 255 |Catégorie toowhich cet élément appartient (par exemple, cuisine la documentation, documentaires...) ; peut être vide. |
| Description |Non, sauf si des caractéristiques sont présentes (mais peut être vide) |Caractères alphanumériques <br> Longueur maximale : 4 000 |Description de cet élément. |
| Features list |Non |Caractères alphanumériques <br> Longueur maximale : 4 000 ; nombre maximal de caractéristiques : 20 |Séparées par des virgules de la liste des noms de fonction = valeur de fonctionnalité qui peut être utilisé tooenhance modèle recommandation ; consultez [rubriques avancées](#2-advanced-topics) section. |

| Méthode HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| filename |Identificateur textuel du catalogue de hello.<br>Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.<br>Longueur maximale : 50 |
| apiVersion |1.0 |
|  | |
| Corps de la requête |Exemple (avec caractéristiques) :<br/>créer des 2406e770-769c-4189-89de-1c9283f93a96, Clara Callan, livre, description du Registre hello, = Richard Wright, publisher = Harper FLAMANT ROSE Canada, année = 2001<br>21bf8088-b6c0-4509-870c-e1c7ac78304a, hello Forgetting salle : une illusion (livre Byzantium), livre, auteur = Nick Bantock, publisher = Harpercollins, année = 1997<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001<br>552a1940-21e4-4399-82bb-594b46d7ed54, retenue d’animaux, livre, description du Registre hello, auteur = Magnus Mills, publisher = publication Arcade, année = 1998</pre> |

**Réponse**:

Code d'état HTTP : 200

Hello API renvoie un rapport d’importation de hello.

* `feed\entry\content\properties\LineCount` : nombre de lignes acceptées.
* `feed\entry\content\properties\ErrorCount`-Nombre de lignes qui n’ont pas été ajoutés en raison de l’erreur de tooan.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a>8.2.    Obtention de catalogue
Récupère tous les éléments de catalogue.
Hello catalogue sera récupéré d’une page à la fois. Si vous souhaitez que les éléments tooget à un index particulier, vous pouvez utiliser le paramètre d’odata hello $skip. Par exemple si vous souhaitez que les éléments tooget commençant à la position 100, ajoutez le paramètre hello $skip = 100 toohello demande.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

réponse de Hello comporte une entrée par un élément de catalogue. Chaque entrée a hello données suivantes :

* `feed/entry/content/properties/ExternalId`-ID externe de l’élément de catalogue, fourni par le client de hello hello.
* `feed/entry/content/properties/InternalId`-ID interne catalogue élément hello Outside Azure Machine Learning recommandations a généré.
* `feed/entry/content/properties/Name` : nom de l’élément de catalogue.
* `feed/entry/content/properties/Category` : catégorie de l’élément de catalogue.
* `feed/entry/content/properties/Description` : description de l’élément de catalogue.
* `feed/entry/content/properties/Metadata` : métadonnées de l’élément de catalogue.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a>8.3.    Obtention d'éléments de catalogue par jeton
| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| token |Jeton de nom de l’élément de catalogue hello. Doit contenir au moins 3 caractères. |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

réponse de Hello comporte une entrée par un élément de catalogue. Chaque entrée a hello données suivantes :

* `feed/entry/content/properties/InternalId`-ID interne catalogue élément hello Outside Azure Machine Learning recommandations a généré.
* `feed/entry/content/properties/Name` : nom de l’élément de catalogue.
* `feed/entry/content/properties/Rating` - (pour une utilisation ultérieure)
* `feed/entry/content/properties/Reasoning` - (pour une utilisation ultérieure)
* `feed/entry/content/properties/Metadata` - (pour une utilisation ultérieure)
* `feed/entry/content/properties/FormattedRating` (pour une utilisation ultérieure)

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a>9. Données d'utilisation
### <a name="91----import-usage-data"></a>9.1.    Importation de données d'utilisation
#### <a name="911-uploading-file"></a>9.1.1. Téléchargement d'un fichier
Cette section montre comment les données d’utilisation tooupload à l’aide d’un fichier. Vous pouvez appeler cette API plusieurs fois avec les données d'utilisation. Toutes les données d'utilisation sont enregistrées pour tous les appels.

| Méthode HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| filename |Identificateur textuel du catalogue de hello.<br>Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.<br>Longueur maximale : 50 |
| apiVersion |1.0 |
|  | |
| Corps de la requête |Données d’utilisation. Format :<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Nom</th><th>Obligatoire</th><th>Type</th><th>Description</th></tr><tr><td>User Id</td><td>Oui</td><td>[A-z], [a-z], [0-9], [_] &#40;trait de soulignement&#41;, [-] &#40;tiret&#41;<br> Longueur maximale : 255 </td><td>Identificateur unique d’un utilisateur.</td></tr><tr><td>Item Id</td><td>Oui</td><td>[A-z], [a-z], [0-9], [&#95;] &#40;trait de soulignement&#41;, [-] &#40;tiret&#41;<br> Longueur maximale : 50</td><td>Identificateur unique d'un élément.</td></tr><tr><td>Time</td><td>Non</td><td>Date au format suivant : AAAA/MM/JJTHH:MM:SS (par exemple, 2013/06/20T10:00:00)</td><td>Indication de temps des données.</td></tr><tr><td>Événement</td><td>Non, mais s'il est indiqué, la date doit l'être également</td><td>Une des manières de hello suivantes :<br>• Click (clic)<br>• RecommendationClick (clic de recommandation)<br>•    AddShopCart (ajout au panier)<br>• RemoveShopCart (suppression du panier)<br>• Purchase</td><td></td></tr></table><br>Taille maximale du fichier : 200 Mo<br><br>Exemple :<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Réponse**:

Code d'état HTTP : 200

* `Feed\entry\content\properties\LineCount` : nombre de lignes acceptées.
* `Feed\entry\content\properties\ErrorCount`-Nombre de lignes qui n’ont pas été ajoutés en raison de l’erreur de tooan.
* `Feed\entry\content\properties\FileId` : identificateur de fichier.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a>9.1.2. Utilisation de l'acquisition de données
Cette section montre comment les événements de toosend dans réel heure tooAzure Machine Learning recommandations, généralement à partir de votre site Web.

| Méthode HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| apiVersion |1.0 |
| Corps de la demande |Entrée de données d’événement pour chaque événement, vous souhaitez toosend. Vous devez envoyer pour le même ID dans le champ de SessionId hello hello hello même session utilisateur ou un navigateur. (Consultez l'exemple du corps d'événement ci-dessous.) |

* Exemple pour l'événement « Click » :
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* Exemple pour l'événement « RecommendationClick » :
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Exemple pour l'événement « AddShopCart » :
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Exemple pour l'événement « RemoveShopCart » :
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
              <EventData>
                      <Name>RemoveShopCart</Name>
                      <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                </EventData>
          </EventData>
        </Event>
* Exemple pour l’événement « Purchase » :
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* Exemple d'envoi de 2 événements « Click » et « AddShopCart » :
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

**Réponse**: Code d'état HTTP : 200

### <a name="92----list-model-usage-files"></a>9.2.    Liste des fichiers d'utilisation de modèle
Récupère les métadonnées de tous les fichiers d'utilisation du modèle.
Hello l’utilisation de fichiers seront récupérés une page à la fois. Chaque page contient 100 éléments. Si vous souhaitez que les éléments tooget à un index particulier, vous pouvez utiliser le paramètre d’odata hello $skip. Par exemple si vous souhaitez que les éléments tooget commençant à la position 100, ajoutez le paramètre hello $skip = 100 toohello demande.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| forModelId |Identificateur unique du modèle de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

réponse de Hello comporte une entrée par fichier d’utilisation. Chaque entrée a hello données suivantes :

* `feed\entry\content\properties\Id` : ID du fichier utilisation.
* `feed\entry\content\properties\Length` : longueur du fichier d’utilisation en Mo.
* `feed\entry\content\properties\DateModified`-Date de création de fichier de l’utilisation de hello.
* `feed\entry\content\properties\UseInModel`-Si le fichier de l’utilisation de hello est utilisé dans le modèle de hello.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a>9.3.    Obtention de statistiques d'utilisation
Obtient les statistiques d'utilisation.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| startDate |Date de début. Format : aaaa/MM/jjTHH:mm:ss |
| endDate |Date de fin. Format : aaaa/MM/jjTHH:mm:ss |
| eventTypes |Types de séparées par des virgules de chaîne d’événement ou null tooget tous les événements |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

Collection d'éléments clé/valeur. Chacune d’elles contient sum hello d’événements pour un type d’événement spécifique groupées par heure.

* `feed\entry[i]\content\properties\Key`-Contient l’heure hello (regroupé par heure) et le type d’événement hello.
* `feed\entry[i]\content\properties\Value` : nombre total d’événements.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a>9.4.    Obtention d'exemple de fichier d'utilisation
Récupère hello premier 2 Ko d’utilisation de contenu du fichier.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| fileId |Identificateur unique hello d’utilisation du fichier de modèle |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

La réponse est retournée au format texte brut :

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a>9.5.    Obtention de fichier d'utilisation de modèle
Récupère le hello le contenu complet du fichier de l’utilisation de hello.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| mid |Identificateur unique du modèle de hello |
| fid |Identificateur unique hello d’utilisation du fichier de modèle |
| télécharger |1 |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

La réponse est retournée au format texte brut :

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a>9.6.    Suppression de fichier d'utilisation
Supprime le fichier d’utilisation de modèle spécifié hello.

| Méthode HTTP | URI |
|:--- |:--- |
| SUPPRIMER |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| fileId |Identificateur unique de hello toobe de fichier supprimé |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

### <a name="97----delete-all-usage-files"></a>9.7.    Suppression de tous les fichiers d'utilisation
Supprime tous les fichiers d'utilisation du modèle.

| Méthode HTTP | URI |
|:--- |:--- |
| SUPPRIMER |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

## <a name="10-features"></a>10. Caractéristiques
Cette section montre comment tooretrieve fonctionnalité plus d’informations, telles que les fonctions hello importé et leurs valeurs, leur rang, et lorsque ce classement a été alloué. Fonctionnalités qui sont importées en tant que partie des données de catalogue hello et puis leur rang est associé à un rang.
Rang dans la fonction peut modifier en fonction de modèle toohello des données d’utilisation et le type des éléments. Mais pour les éléments/utilisation cohérentes, rang de hello doit avoir des petites fluctuations uniquement.
le rang de Hello de fonctionnalités est un nombre non négatif. Hello numéro 0 signifie que cette fonctionnalité hello n’était pas classée (se produit si vous appelez cette saisie semi-automatique toohello préalable de API de première génération de rang hello). date de Hello auquel a été attribué rang de hello est appelée actualisation de score hello.

### <a name="101-get-features-info-for-last-rank-build"></a>10.1. Obtention d'informations sur les caractéristiques (pour la dernière build de classement)
Récupère les informations de fonctionnalité hello, y compris le classement, pour la dernière génération réussie rank hello.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| samplingSize |Nombre de tooinclude de valeurs pour chaque fonctionnalité en fonction des données toohello présentes dans le catalogue de hello. <br/>Les valeurs possibles sont les suivantes :<br> -1 : tous les échantillons. <br>0 : aucun échantillonnage. <br>N : retourne N échantillons pour chaque nom de caractéristique. |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

réponse de Hello contient une liste d’entrées d’informations de fonctionnalité. Chaque entrée contient :

* `feed/entry/content/m:properties/d:Name` : nom de la caractéristique.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Date à quels hello rang a été alloué toothis fonctionnalité, également appelé « actualisation du score »). Une date historique (« 0001-01-01T00:00:00 ») signifie qu'aucune build de classement n'a été exécutée.
* `feed/entry/content/m:properties/d:Rank` : classement de la caractéristique (float). Un classement de 2.0 ou plus désigne une bonne caractéristique.
* `feed/entry/content/m:properties/d:SampleValues`-Liste de séparées par des virgules des valeurs de taille d’échantillonnage de toohello demandée.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a>10.2. Obtention d'informations sur les caractéristiques (pour une build de classement spécifique)
Récupère les informations de fonctionnalité hello, y compris hello de classement pour une build de classement spécifique.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| samplingSize |Nombre de tooinclude de valeurs pour chaque fonctionnalité en fonction des données toohello présentes dans le catalogue de hello.<br/> Les valeurs possibles sont les suivantes :<br> -1 : tous les échantillons. <br>0 : aucun échantillonnage. <br>N : retourne N échantillons pour chaque nom de caractéristique. |
| rankBuildId |Identificateur unique de la génération de rang hello ou -1 pour la dernière build de rang hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

réponse de Hello contient une liste d’entrées d’informations de fonctionnalité. Chaque entrée contient :

* `feed/entry/content/m:properties/d:Name` : nom de la caractéristique.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Date à quels hello rang a été alloué toothis fonctionnalité, également appelé « actualisation du score »). Une date historique (« 0001-01-01T00:00:00 ») signifie qu'aucune build de classement n'a été exécutée.
* `feed/entry/content/m:properties/d:Rank` : classement de la caractéristique (float). Un classement de 2.0 ou plus désigne une bonne caractéristique.
* `feed/entry/content/m:properties/d:SampleValues`-Liste de séparées par des virgules des valeurs de taille d’échantillonnage de toohello demandée.

OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a>11. Créer
  Cette section explique hello différentes API liées toobuilds. Il existe 3 types de builds : une build de recommandation, une build de classement et une build FBT (fréquemment achetés ensemble).

de la build Hello recommandation vise toogenerate utilisé par un modèle de recommandation pour des prédictions. Les prédictions (pour ce type de build) sont de deux types :

* I2I - alias Élément tooItem recommandations - un élément ou une liste d’éléments de cette option prédit une liste d’éléments qui sont susceptibles de toobe intérêt majeur.
* U2I - alias Utilisateur tooItem recommandations - un id d’utilisateur (et éventuellement une liste d’éléments) cette option prédit une liste d’éléments qui sont susceptibles de toobe intérêt majeur pour hello donnée utilisateur (et son choix supplémentaire d’éléments). recommandations de U2I Hello sont basées sur l’historique de hello d’éléments qui ont été dignes d’intérêt pour l’utilisateur hello temps toohello hello modèle a été construit.

Une build rangée est une version technique qui vous permet de toolearn sur l’utilité de hello de vos fonctionnalités. En règle générale, dans l’ordre tooget hello meilleurs résultats pour un modèle de recommandation qui impliquent des fonctionnalités, vous devez prendre hello comme suit :

* Déclencher une build de classement (sauf si le score hello fonctionnalités est stable) et attendez que vous obtenez le score de fonctionnalité hello.
* Récupérer le rang hello de vos fonctionnalités en appelant hello [obtenir les informations de fonctionnalités](#101-get-features-info-for-last-rank-build) API.
* Configurer une build de recommandation par hello paramètres suivants :
  * `useFeatureInModel`-Définissez tooTrue.
  * `ModelingFeatureList`-Set tooa séparées par des virgules liste des fonctions avec un score de 2.0 ou plus (en fonction des rangs toohello récupéré à l’étape précédente de hello).
  * `AllowColdItemPlacement`-Définissez tooTrue.
  * Vous pouvez éventuellement définir `EnableFeatureCorrelation` tooTrue et `ReasoningFeatureList` toohello la liste des fonctionnalités que vous souhaitez toouse des explications approfondies (généralement hello même liste de fonctionnalités utilisée dans la modélisation ou une sous-liste).
* Déclencheur hello recommandation build avec hello configuré les paramètres.

Remarque : Si vous ne configurez pas tous les paramètres (par exemple, appeler build de recommandation hello sans paramètres) ou vous ne désactivez pas explicitement l’utilisation de hello de fonctionnalités (par exemple, `UseFeatureInModel` définir tooFalse), hello système définit les paramètres liés à la fonctionnalité de hello toohello expliqué ci-dessus des valeurs au cas où il existe une build de classement.

Il n’existe aucune restriction sur l’exécution d’une build de classement et une recommandation générer simultanément pour hello même modèle. Néanmoins, vous ne peut pas exécuter deux versions de hello même type sur le même modèle en parallèle de hello.

Une build FBT (Frequently Bought Together) est un autre algorithme de génération de recommandations. Parfois qualifié de « conservateur », ce système de recommandation convient bien aux catalogues qui ne sont pas homogènes par nature (homogènes : livres, films, certains produits alimentaires, articles de mode ; non homogènes : ordinateur et périphériques, produits interdomaines, très diversifiés).

Remarque : si les fichiers d’utilisation que vous avez téléchargé hello contiennent ce champ est facultatif hello « type d’événement » puis de FBT modélisation uniquement les événements « Achat » servira. Si aucun type d’événement n’est fourni, tous les événements sont considérés comme achat (purchase).

#### <a name="111-build-parameters"></a>11.1 Paramètres de build
Chaque type de build peut être configuré via un ensemble de paramètres (décrits ci-dessous). Si vous ne configurez pas les paramètres de hello, hello sera automatiquement attribut système valeurs de paramètres toohello selon les informations toohello présentes au moment de hello vous déclenchez une build.

##### <a name="1111-usage-condenser"></a>11.1.1. Condenseur d'utilisation
Les utilisateurs ou éléments avec peu de points d'utilisation peuvent contenir plus de bruit que d'informations. système de Hello tentatives toopredict hello le nombre minimal de points de l’utilisation par toobe utilisateur ou cet élément utilisé dans un modèle. Ce nombre seront hello dehors des limites définies par hello ItemCutoffLowerBound et paramètres ItemCutoffUpperBound pour plage de hello définie par hello UserCutOffLowerBound et UserCutoffUpperBound des paramètres pour les utilisateurs et les éléments. effet de réfrigérant Hello pour les éléments ou les utilisateurs peut être réduite en définissant au moins une des toozero de limites hello correspondant.

##### <a name="1112-rank-build-parameters"></a>11.1.2. Paramètres de build de classement
tableau de Hello ci-dessous illustre les paramètres de génération hello pour une build de classement.

| Clé | Description | Type | Valeur valide |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |nombre de Hello d’itérations hello modèle fonctionne est reflétée par hello globale de calcul hello heure et la précision du modèle. Hello hello nombre élevé, vous obtiendrez améliorer la précision de hello, mais hello de calcul prend plus de temps. |Entier  |10-50 |
| NumberOfModelDimensions |un nombre de dimensions Hello relative nombre toohello du modèle de hello « features » va tenter de toofind au sein de vos données. Augmentation du nombre hello de dimensions permettra de mieux précisément des résultats de hello dans des clusters plus petits. Toutefois, trop de dimensions empêche le modèle de hello recherche des corrélations entre les éléments. |Entier  |10-40 |
| ItemCutOffLowerBound |Définit la limite d’inférieure élément hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| ItemCutOffUpperBound |Définit la limite de supérieur élément hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| UserCutOffLowerBound |Définit la limite hello utilisateur pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| UserCutOffUpperBound |Définit la limite de supérieur utilisateur hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |

##### <a name="1113-recommendation-build-parameters"></a>11.1.3. Paramètres de build de recommandation
tableau de Hello ci-dessous illustre les paramètres de génération hello pour la build de la recommandation.

| Clé | Description | Type | Valeur valide |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |nombre de Hello d’itérations hello modèle fonctionne est reflétée par hello globale de calcul hello heure et la précision du modèle. Hello hello nombre élevé, vous obtiendrez améliorer la précision de hello, mais hello de calcul prend plus de temps. |Entier  |10-50 |
| NumberOfModelDimensions |un nombre de dimensions Hello relative nombre toohello du modèle de hello « features » va tenter de toofind au sein de vos données. Augmentation du nombre hello de dimensions permettra de mieux précisément des résultats de hello dans des clusters plus petits. Toutefois, trop de dimensions empêche le modèle de hello recherche des corrélations entre les éléments. |Entier  |10-40 |
| ItemCutOffLowerBound |Définit la limite d’inférieure élément hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| ItemCutOffUpperBound |Définit la limite de supérieur élément hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| UserCutOffLowerBound |Définit la limite hello utilisateur pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| UserCutOffUpperBound |Définit la limite de supérieur utilisateur hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| Description |Description de la build. |String |Tout texte, 512 caractères maximum |
| EnableModelingInsights |Vous permet de toocompute métriques sur le modèle de recommandation hello. |Boolean |True/False |
| UseFeaturesInModel |Indique si les fonctionnalités peuvent être utilisées dans le modèle de recommandation d’ordre tooenhance hello. |Boolean |True/False |
| ModelingFeatureList |Liste de séparées par des virgules des toobe de noms de fonction utilisée dans la génération de recommandation hello, dans la recommandation de commande tooenhance hello. |String |Noms de fonctionnalités, des caractères de too512 |
| AllowColdItemPlacement |Indique si la recommandation de hello doit également à orienter éléments froids via la similarité de la fonctionnalité. |Boolean |True/False |
| EnableFeatureCorrelation |Indique si des caractéristiques peuvent être utilisées dans le raisonnement. |Boolean |True/False |
| ReasoningFeatureList |Liste de séparées par des virgules de fonctionnalité toobe de noms utilisé pour le raisonnement phrases (par exemple, les explications de recommandation). |String |Noms de fonctionnalités, des caractères de too512 |
| EnableU2I |Autoriser l’alias hello personnalisé recommandation U2I (recommandations tooitem de l’utilisateur). |Boolean |Vrai/faux (Vrai par défaut) |

##### <a name="1114-fbt-build-parameters"></a>11.1.4. Paramètres de build FBT
tableau de Hello ci-dessous illustre les paramètres de génération hello pour la build de la recommandation.

| Clé | Description | Type | Valeur valide (par défaut) |
|:--- |:--- |:--- |:--- |
| FbtSupportThreshold |Comment le modèle de hello classique est. Nombre d’occurrences de collaboration de toobe éléments pris en compte pour la modélisation. |Entier  |3-50 (6) |
| FbtMaxItemSetSize |Limites hello nombre d’éléments dans un ensemble de fréquent. |Entier  |2-3 (2) |
| FbtMinimalScore |Score minimal un ensemble de fréquent ont dans toobe de commande inclus dans hello retourner des résultats. Bonjour supérieur Bonjour mieux. |Double |0 et plus (0) |
| FbtSimilarityFunction |Définit hello similarité fonction toobe utilisé par la génération de hello. Favorise la finesse serendipity, collaboration occurrence favorise la prévisibilité et Jaccard est une bonne alliera hello deux. |String |cooccurrence, élévation, jaccard (élévation) |

### <a name="112-trigger-a-recommendation-build"></a>11.2. Déclencher une build de recommandation
  Par défaut, cette API déclenche une build de modèle de recommandation. tootrigger un rang égal à générer (dans les fonctions de tooscore de commande), variante d’API de build hello avec le paramètre de type de build doit être utilisé.

| Méthode HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` (en cas d’envoi du corps de la requête) |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| userDescription |Identificateur textuel du catalogue de hello. Notez que si vous utilisez des espaces, vous devez plutôt l'encoder avec %20. Consultez l'exemple ci-dessus.<br>Longueur maximale : 50 |
| apiVersion |1.0 |
|  | |
| Corps de la requête |Si vide build de hello sera exécuté avec des paramètres de build par défaut hello.<br><br>Si vous souhaitez que les paramètres de génération tooset hello, envoyer des paramètres de hello au format XML dans le corps hello comme hello suivant l’exemple. (Consultez la section hello « paramètres de génération » pour obtenir une explication des paramètres de hello.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>` |

**Réponse**:

Code d'état HTTP : 200

Il s'agit d'une API asynchrone. La réponse obtenue est un ID de build. tooknow lors de la génération de hello est terminée, vous devez appeler l’API « Obtenir génère état d’un modèle » hello et localiser cette ID de build dans la réponse de hello. Notez qu’une build peut prendre de toohours minutes selon la taille de hello de données de hello.

Vous ne peut pas consommer recommandations jusqu'à ce que hello build se termine.

État de build valide :

* Create : la demande de build a été créée.
* Queued : la demande de build a été envoyée et mise en file d’attente.
* Building : la build est en cours.
* Success : la build a été correctement exécutée.
* Error : la build s’est terminée par un échec.
* Cancelled : la build a été annulée.
* L’annulation - une demande d’annulation pour la build de hello a été envoyée.

Notez cette build hello QU'ID accessible sous hello suivant le chemin d’accès :`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a>11.3. Déclenchement d'une build (recommandation, classement ou FBT)
| Méthode HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` (en cas d’envoi du corps de la requête) |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| userDescription |Identificateur textuel du catalogue de hello. Notez que si vous utilisez des espaces, vous devez plutôt l'encoder avec %20. Consultez l'exemple ci-dessus.<br>Longueur maximale : 50 |
| buildType |Type de hello build tooinvoke : <br/> - « Recommendation » pour une build de recommandation <br> - « Ranking » pour une build de classement <br/>  : « Fbt » pour une build FBT |
| apiVersion |1.0 |
|  | |
| Corps de la requête |Si vide build de hello sera exécuté avec des paramètres de build par défaut hello.<br><br>Si vous souhaitez que les paramètres de génération tooset, les envoyer en tant que XML dans corps hello comme hello suivant l’exemple. (Consultez la section hello « paramètres de génération » pour une explication et une liste complète des paramètres de hello.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>` |

**Réponse**:

Code d'état HTTP : 200

Il s'agit d'une API asynchrone. La réponse obtenue est un ID de build. tooknow lors de la génération de hello est terminée, vous devez appeler l’API « Obtenir génère état d’un modèle » hello et localiser cette ID de build dans la réponse de hello. Notez qu’une build peut prendre de toohours minutes selon la taille de hello de données de hello.

Vous ne peut pas consommer recommandations jusqu'à ce que hello build se termine.

État de build valide :

* Create : le modèle a été créé.
* Queued : la build de modèle a été déclenchée et mise en file d’attente.
* Building : le modèle est en cours de génération.
* Success : la build a été correctement exécutée.
* Error : la build s’est terminée par un échec.
* Cancelled : la build a été annulée.
* Cancelling : la build est en cours d’annulation.

Notez cette build hello QU'ID accessible sous hello suivant le chemin d’accès :`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>




### <a name="114-get-builds-status-of-a-model"></a>11.4. Obtention de l'état de build d'un modèle
Récupère les builds et leur état pour un modèle spécifié.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| onlyLastBuild |Indique si tooreturn tous hello générer l’historique du modèle de hello ou état hello seule de la build la plus récente hello |
| apiVersion |1.0 |

**Réponse**:

Code d'état HTTP : 200

réponse de Hello inclut une entrée par une build. Chaque entrée a hello données suivantes :

* `feed/entry/content/properties/UserName`-Nom d’utilisateur de hello.
* `feed/entry/content/properties/ModelName`-Nom du modèle de hello.
* `feed/entry/content/properties/ModelId` : identificateur unique du modèle.
* `feed/entry/content/properties/IsDeployed`-Génération de hello est déployé (aussi appelé) (c’est-à-dire active).
* `feed/entry/content/properties/BuildId` : identificateur unique de la build.
* `feed/entry/content/properties/BuildType`-Type de build de hello.
* `feed/entry/content/properties/Status` : état de la build. Peut être une des manières suivantes les hello : erreur, construction, en file d’attente, annulation, annulé, la réussite.
* `feed/entry/content/properties/StatusMessage`-Message d’état détaillée (s’applique uniquement les États toospecific).
* `feed/entry/content/properties/Progress` : progression de l’exécution de la build (%).
* `feed/entry/content/properties/StartTime` : heure de début de l’exécution de la build.
* `feed/entry/content/properties/EndTime` : heure de fin de l’exécution de la build.
* `feed/entry/content/properties/ExecutionTime` : durée de la build.
* `feed/entry/content/properties/ProgressStep`-Des détails concernant la phase actuelle de hello d’une build en cours d’exécution.

État de build valide :

* Created : l’entrée de demande de build a été créée.
* Queued : la demande de build a été déclenchée et mise en file attente.
* Building : la build est en cours.
* Success : la build a été correctement exécutée.
* Error : la build s’est terminée par un échec.
* Cancelled : la build a été annulée.
* Cancelling : la build est en cours d’annulation.

Valeurs valides pour le type de build :

* Rank - Build de classement.
* Recommendation - Build de recommandation.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="115-get-builds-status"></a>11.5. Obtention de l'état de build
Récupère les états de build de tous les modèles d'un utilisateur.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| onlyLastBuild |Indique si tooreturn tous hello générer l’historique du modèle de hello ou état hello seule de la build la plus récente hello. |
| apiVersion |1.0 |

**Réponse**:

Code d'état HTTP : 200

réponse de Hello inclut une entrée par une build. Chaque entrée a hello données suivantes :

* `feed/entry/content/properties/UserName`-Nom d’utilisateur de hello.
* `feed/entry/content/properties/ModelName`-Nom du modèle de hello.
* `feed/entry/content/properties/ModelId` : identificateur unique du modèle.
* `feed/entry/content/properties/IsDeployed`-Si la génération de hello est déployée.
* `feed/entry/content/properties/BuildId` : identificateur unique de la build.
* `feed/entry/content/properties/BuildType`-Type de build de hello.
* `feed/entry/content/properties/Status` : état de la build. Peut être une des manières suivantes les hello : erreur, construction, en file d’attente, annulé, annulation, réussite.
* `feed/entry/content/properties/StatusMessage`-Message d’état détaillée (s’applique uniquement les États toospecific).
* `feed/entry/content/properties/Progress` : progression de l’exécution de la build (%).
* `feed/entry/content/properties/StartTime` : heure de début de l’exécution de la build.
* `feed/entry/content/properties/EndTime` : heure de fin de l’exécution de la build.
* `feed/entry/content/properties/ExecutionTime` : durée de la build.
* `feed/entry/content/properties/ProgressStep`-Des détails concernant la phase actuelle de hello d’une build en cours d’exécution.

État de build valide :

* Created : l’entrée de demande de build a été créée.
* Queued : la demande de build a été déclenchée et mise en file attente.
* Building : la build est en cours.
* Success : la build a été correctement exécutée.
* Error : la build s’est terminée par un échec.
* Cancelled : la build a été annulée.
* Cancelling : la build est en cours d’annulation.

Valeurs valides pour le type de build :

* Rank - Build de classement.
* Recommendation - Build de recommandation.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="116-delete-build"></a>11.6. Suppression de build
Supprime une build.

REMARQUE :  <br>Vous ne pouvez pas supprimer une build active. le modèle Hello doit être mis à jour tooa autre active build avant de le supprimer.<br>Vous ne pouvez pas supprimer une build en cours d'exécution. Vous devez annuler les build hello tout d’abord en appelant <strong>Annuler Build</strong>.

| Méthode HTTP | URI |
|:--- |:--- |
| SUPPRIMER |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| buildId |Identificateur unique de la génération de hello. |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

### <a name="117-cancel-build"></a>11.7. Annulation de build
Annule une build avec l'état Building.

| Méthode HTTP | URI |
|:--- |:--- |
| PUT |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| buildId |Identificateur unique de la génération de hello. |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

### <a name="118-get-build-parameters"></a>11.8. Obtention des paramètres de build
Récupère les paramètres de build.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| buildId |Identificateur unique de la génération de hello. |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

Cette API retourne une collection d'éléments clé/valeur. Chaque élément représente un paramètre et sa valeur :

* `feed/entry/content/properties/Key` : nom du paramètre de la build.
* `feed/entry/content/properties/Value` : valeur du paramètre de la build.

tableau Hello ci-dessous représente la valeur hello représentant chaque clé.

| Clé | Description | Type | Valeur valide |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |nombre de Hello d’itérations hello modèle fonctionne est reflétée par hello globale de calcul hello heure et la précision du modèle. Hello hello nombre élevé, vous obtiendrez améliorer la précision de hello, mais hello de calcul prend plus de temps. |Entier  |10-50 |
| NumberOfModelDimensions |un nombre de dimensions Hello relative nombre toohello du modèle de hello « features » va tenter de toofind au sein de vos données. Augmentation du nombre hello de dimensions permettra de mieux précisément des résultats de hello dans des clusters plus petits. Toutefois, trop de dimensions empêche le modèle de hello recherche des corrélations entre les éléments. |Entier  |10-40 |
| ItemCutOffLowerBound |Définit la limite d’inférieure élément hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| ItemCutOffUpperBound |Définit la limite de supérieur élément hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| UserCutOffLowerBound |Définit la limite hello utilisateur pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| UserCutOffUpperBound |Définit la limite de supérieur utilisateur hello pour les à hello. Consultez Condenseur d'utilisation ci-dessus. |Integer |2 ou plus (0 désactive le condenseur) |
| Description |Description de la build. |String |Tout texte, 512 caractères maximum |
| EnableModelingInsights |Vous permet de toocompute métriques sur le modèle de recommandation hello. |Boolean |True/False |
| UseFeaturesInModel |Indique si les fonctionnalités peuvent être utilisées dans le modèle de recommandation d’ordre tooenhance hello. |Boolean |True/False |
| ModelingFeatureList |Liste de séparées par des virgules des toobe de noms de fonction utilisée dans la génération de recommandation hello, dans la recommandation de commande tooenhance hello. |String |Noms de fonctionnalités, des caractères de too512 |
| AllowColdItemPlacement |Indique si la recommandation de hello doit également à orienter éléments froids via la similarité de la fonctionnalité. |Boolean |True/False |
| EnableFeatureCorrelation |Indique si des caractéristiques peuvent être utilisées dans le raisonnement. |Boolean |True/False |
| ReasoningFeatureList |Liste de séparées par des virgules de fonctionnalité toobe de noms utilisé pour le raisonnement phrases (par exemple, les explications de recommandation). |String |Noms de fonctionnalités, des caractères de too512 |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a>12. Recommandation
### <a name="121-get-item-recommendations-for-active-build"></a>12.1. Obtention de recommandations d’éléments (pour la build active)
Obtenir des recommandations de build active de hello de type « Recommendation » ou « Fbt » basé sur une liste d’éléments de semences (entrée).

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| itemIds |Liste de séparées par des virgules des toorecommend d’éléments hello pour. <br>Si les build active hello est de type FBT puis vous pouvez envoyer qu’un seul élément. <br>Longueur maximale : 1024 |
| numberOfResults |Nombre de résultats requis  <br> Max : 150 |
| includeMetatadata |Utilisation ultérieure, toujours false |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello comporte une entrée par élément recommandé. Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id` : ID d’élément recommandé
* `Feed\entry\content\properties\Name`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.
* `Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)

Hello exemple de réponse ci-dessous comprend 10 éléments recommandés.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="122-get-item-recommendations-of-a-specific-build"></a>12.2. Obtention de recommandations d’éléments (d’une build spécifique)
Obtient des recommandations d'une build spécifique de type « Recommendation » ou « Fbt ».

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| itemIds |Liste de séparées par des virgules des toorecommend d’éléments hello pour. <br>Si les build active hello est de type FBT puis vous pouvez envoyer qu’un seul élément. <br>Longueur maximale : 1024 |
| numberOfResults |Nombre de résultats requis  <br> Max : 150 |
| includeMetatadata |Utilisation ultérieure, toujours false |
| buildId |Hello générer toouse id pour cette demande de recommandation |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello comporte une entrée par élément recommandé. Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id` : ID d’élément recommandé
* `Feed\entry\content\properties\Name`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.
* `Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)

Pour obtenir un exemple de réponse, consultez la section 12.1.

### <a name="123-get-fbt-recommendations-for-active-build"></a>12.3. Obtention de recommandations FBT (pour la build active)
Obtenir des recommandations de build active de hello du type « Fbt » basé sur un élément de valeur initiale (entrée).

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| itemId |Toorecommend élément pour. <br>Longueur maximale : 1024 |
| numberOfResults |Nombre de résultats requis  <br>Max : 150 |
| minimalScore |Score minimal un ensemble de fréquent ont dans toobe de commande inclus dans hello retourner des résultats |
| includeMetatadata |Utilisation ultérieure, toujours false |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello inclut une entrée par l’ensemble de l’élément recommandé (il s’agit d’un ensemble d’éléments qui sont généralement achetés avec l’élément de départ/entrée hello). Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id1` : ID d’élément recommandé
* `Feed\entry\content\properties\Name1`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Id2` : ID du second élément recommandé (facultatif).
* `Feed\entry\content\properties\Name2`-Nom de l’élément 2e hello (facultatif).
* `Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.
* `Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)

Hello exemple de réponse ci-dessous inclut 3 séries d’élément recommandé.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a>12.4. Obtention de recommandations FBT (d’une build spécifique)
Obtient des recommandations d’une build spécifique de type « Fbt ».

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| itemId |Toorecommend élément pour. <br>Longueur maximale : 1024 |
| numberOfResults |Nombre de résultats requis  <br>Max : 150 |
| minimalScore |Score minimal un ensemble de fréquent ont dans toobe de commande inclus dans hello retourner des résultats |
| includeMetatadata |Utilisation ultérieure, toujours false |
| buildId |Hello générer toouse id pour cette demande de recommandation |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello inclut une entrée par l’ensemble de l’élément recommandé (il s’agit d’un ensemble d’éléments qui sont généralement achetés avec l’élément de départ/entrée hello). Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id1` : ID d’élément recommandé
* `Feed\entry\content\properties\Name1`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Id2` : ID du second élément recommandé (facultatif).
* `Feed\entry\content\properties\Name2`-Nom de l’élément 2e hello (facultatif).
* `Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.
* `Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)

Pour obtenir un exemple de réponse, consultez la section 12.3.

### <a name="125-get-user-recommendations-for-active-build"></a>12.5. Obtention de recommandations de l’utilisateur (pour la build active)
Obtient des recommandations de l’utilisateur auprès de la build de type « Recommendation » marquée comme build active.

Hello API renvoie une liste de l’élément prédit en fonction de l’historique d’utilisation de l’utilisateur de hello toohello.

Remarques : 

1. Il n’existe aucune recommandation de l’utilisateur pour une build de type FBT.
2. Si la build de hello active est FBT sera de cette méthode retourne une erreur.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| userId |Identificateur unique de l’utilisateur de hello |
| numberOfResults |Nombre de résultats requis |
| includeMetatadata |Utilisation ultérieure, toujours false |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello comporte une entrée par élément recommandé. Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id` : ID d’élément recommandé
* `Feed\entry\content\properties\Name`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.
* `Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)

Pour obtenir un exemple de réponse, consultez la section 12.1.

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a>12.6. Obtention de recommandations de l’utilisateur avec une liste d’éléments (pour la build active)
Obtient des recommandations de l’utilisateur auprès de la build de type « Recommendation » marquée comme build active, à l’aide d’une liste supplémentaire d’éléments.

Hello API renvoie une liste de l’élément prédit selon l’historique d’utilisation de toohello d’utilisateur de hello et hello autres fourni.

Remarques : 

1. Il n’existe aucune recommandation de l’utilisateur pour une build de type FBT.
2. Si la build de hello active est FBT sera de cette méthode retourne une erreur.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| userId |Identificateur unique de l’utilisateur de hello |
| itemsIds |Liste de séparées par des virgules des toorecommend d’éléments hello pour. Longueur maximale : 1024 |
| numberOfResults |Nombre de résultats requis |
| includeMetatadata |Utilisation ultérieure, toujours false |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello comporte une entrée par élément recommandé. Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id` : ID d’élément recommandé
* `Feed\entry\content\properties\Name`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.
* `Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)

Pour obtenir un exemple de réponse, consultez la section 12.1.

### <a name="127-get-user-recommendations--of-a-specific-build"></a>12.7. Obtention de recommandations de l’utilisateur (d’une build spécifique)
Obtient des recommandations de l’utilisateur auprès d’une build spécifique de type « Recommendation ».

Hello API renvoie une liste de l’élément prédit en fonction de l’historique d’utilisation toohello d’utilisateur hello (utilisé dans une build spécifique de hello).

Remarque : il n’existe aucune recommandation de l’utilisateur pour une build de type FBT.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| userId |Identificateur unique de l’utilisateur de hello |
| numberOfResults |Nombre de résultats requis |
| includeMetatadata |Utilisation ultérieure, toujours false |
| buildId |Hello générer toouse id pour cette demande de recommandation |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello comporte une entrée par élément recommandé. Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id` : ID d’élément recommandé
* `Feed\entry\content\properties\Name`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.
* `Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)

Pour obtenir un exemple de réponse, consultez la section 12.1.

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a>12.8. Obtention de recommandations de l’utilisateur avec une liste d’éléments (pour une build spécifique)
Obtenir des recommandations de l’utilisateur d’une build spécifique de type « Recommendation » et liste hello d’éléments supplémentaires.

Hello API renvoie une liste de l’élément prédit en fonction de l’historique d’utilisation de l’utilisateur de hello toohello et liste supplémentaire de hello d’éléments.

Remarque : il n’existe aucune recommandation de l’utilisateur pour une build de type FBT.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| userId |Identificateur unique de l’utilisateur de hello |
| itemIds |Liste de séparées par des virgules des toorecommend d’éléments hello pour. Longueur maximale : 1024 |
| numberOfResults |Nombre de résultats requis |
| includeMetatadata |Utilisation ultérieure, toujours false |
| buildId |Hello générer toouse id pour cette demande de recommandation |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello comporte une entrée par élément recommandé. Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id` : ID d’élément recommandé
* `Feed\entry\content\properties\Name`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.
* `Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)

Pour obtenir un exemple de réponse, consultez la section 12.1.

## <a name="13-user-usage-history"></a>13. Historique d’utilisation de l’utilisateur
Une fois un modèle de recommandation a été généré hello système autorise tooretrieve hello historique de l’utilisateur (éléments associés tooa utilisateur spécifique) utilisé pour la build de hello.
Cette API permettent d’historique de l’utilisateur tooretrieve hello

Remarque : l’historique de l’utilisateur hello est actuellement disponible uniquement pour les builds de recommandation.

### <a name="131-retrieve-user-history"></a>13.1 Récupération de l’historique de l’utilisateur
Liste de hello de récupération de l’élément utilisé dans hello active générer ou Bonjour spécifié créer pour hello id d’utilisateur donné.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |Obtenir l’historique de l’utilisateur hello pour la build active de hello.<br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/>Obtenir d’historique de l’utilisateur hello pour hello donné de build`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`<br/><br/>Exemple :`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Bonjour à l’identificateur unique du modèle de hello. |
| userId |Bonjour identificateur unique de l’utilisateur de hello. |
| buildId |paramètre facultatif, autoriser tooindicate à partir de la build historique de l’utilisateur hello doit être fetch |
| apiVersion |1.0 |

**Réponse :**

Code d'état HTTP : 200

réponse de Hello comporte une entrée par élément recommandé. Chaque entrée a hello données suivantes :

* `Feed\entry\content\properties\Id` : ID d’élément recommandé
* `Feed\entry\content\properties\Name`-Nom de l’élément de hello.
* `Feed\entry\content\properties\Rating` : N/A.
* `Feed\entry\content\properties\Reasoning` : N/A.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a>14. Notifications
Recommandations d’apprentissage Machine Azure crée des notifications lorsque des erreurs persistantes se produisent dans le système de hello. Il existe 3 types de notifications :

1. Échec de build : cette notification est déclenchée à chaque échec de build.
2. Acquisition de données de traitement Échec - cette notification est déclenchée lorsque nous avons plus de 100 erreurs Bonjour 5 dernières minutes dans le traitement des événements d’utilisation par le modèle hello.
3. Échec de la consommation de recommandation - cette notification est déclenchée lorsque nous avons plus de 100 erreurs Bonjour 5 dernières minutes dans le traitement de demandes de recommandation par modèle hello.

### <a name="141-get-notifications"></a>14.1. Obtention de notifications
Récupère toutes les notifications hello pour tous les modèles ou d’un modèle unique.

| Méthode HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Obtention de toutes les notifications pour tous les modèles :<br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br>Exemple d'obtention des notifications pour un modèle spécifique :<br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Paramètre facultatif. Si vous l'omettez, vous obtenez toutes les notifications pour tous les modèles. <br>Valeur valide : identificateur unique du modèle de hello. |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse :**

Code d'état HTTP : 200

OData XML

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a>14.2. Suppression de notifications de modèle
Supprime toutes les notifications lues pour un modèle.

| Méthode HTTP | URI |
|:--- |:--- |
| SUPPRIMER |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br>Exemple :<br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| modelId |Identificateur unique du modèle de hello |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

### <a name="143-delete-user-notifications"></a>14.3. Suppression de notifications utilisateur
Supprime toutes les notifications pour tous les modèles.

| Méthode HTTP | URI |
|:--- |:--- |
| SUPPRIMER |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| Nom du paramètre | Valeurs valides |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Corps de la requête |AUCUN |

**Réponse**:

Code d'état HTTP : 200

## <a name="15-legal"></a>15. Informations juridiques
Ce document est fourni « en l'état ». Les informations et les points de vue exprimés dans ce document, y compris les URL et autres références à des sites web, peuvent être modifiés sans préavis.<br><br>
Certains exemples sont fournis à titre indicatif uniquement et sont fictifs. Toute association ou lien est purement involontaire ou fortuit.<br><br>
Ce document ne fournit pas vous concède tooany de propriété intellectuelle de tout produit Microsoft. Vous pouvez copier et utiliser ce document pour un usage interne, à titre de référence.<br><br>
© 2015 Microsoft. Tous droits réservés.

