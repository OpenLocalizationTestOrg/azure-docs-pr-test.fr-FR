---
title: toouse aaaHow Power BI Embedded REST | Documents Microsoft
description: "Découvrez comment toouse Power BI Embedded REST "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a>Comment toouse Power BI Embedded REST

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded : présentation et objectif

Décrit une vue d’ensemble de Power BI Embedded officiel de hello [site Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/), mais les jetons un œil rapide avant de passer à hello plus d’informations sur l’utilisation d’autres.

C’est très simple. Vous souhaiterez peut-être visualisations de données dynamiques hello toouse de [Power BI](https://powerbi.microsoft.com) dans votre application.

La plupart des applications personnalisées doivent toodeliver les données de salutation à leurs clients, pas nécessairement les utilisateurs dans leur propre entreprise. Par exemple, si vous êtes offrant un service de la société A et la société B, les utilisateurs de la société A uniquement les données doivent apparaître pour leur propre entreprise A. Autrement dit, l’architecture mutualisée hello est nécessaire pour la remise de hello.

application personnalisée Hello peut également être offre ses propres méthodes d’authentification telles que l’authentification par formulaire, authentification de base, etc... Ensuite, hello incorporation solution doit collaborer en toute sécurité avec cette méthode d’authentification existant. Il est également nécessaire pour toouse en mesure des utilisateurs toobe ces applications ISV sans hello achat supplémentaire ou le Gestionnaire de licences d’un abonnement Power BI.

 **Power BI Embedded** est précisément conçu pour ces types de scénarios. Donc, maintenant que nous avons cette introduction rapide la façon de hello, passons certains détails

Vous pouvez utiliser hello .NET \(c#) ou Node.js SDK, tooeasily générez votre application avec Power BI Embedded. Toutefois, dans cet article, nous expliquerons le flux HTTP \(y compris AuthN) de Power BI sans Kit de développement logiciel (SDK). Présentation de ce flux, vous pouvez générer votre application **avec n’importe quel langage de programmation**, et vous pouvez comprendre profondément essentiellement hello, Power BI Embedded.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Création d’une collection d’espaces de travail Power BI et obtention de la clé d’accès \(approvisionnement)

Power BI Embedded est un des hello services Azure. Hello uniquement ISV qui utilise le portail Azure est facturé pour les frais d’utilisation \(par toutes les heures des session utilisateur), et l’utilisateur hello rapport hello de vues n’est pas chargée ou même un abonnement Azure.
Avant de commencer le développement d’applications, nous devons créer hello **collecte d’espace de travail Power BI** à l’aide du portail Azure.

Chaque espace de travail de Power BI Embedded est hello pour chaque client (client), et nous pouvons ajouter plusieurs espaces de travail dans chaque collection de l’espace de travail. Hello même clé d’accès est utilisé dans chaque collection de l’espace de travail. En effet, collection d’espace de travail hello est la limite de sécurité de hello pour Power BI Embedded.

![](media/power-bi-embedded-iframe/create-workspace.png)

Lorsque nous aurons terminé la création de la collection d’espace de travail hello, copiez la clé d’accès hello à partir du portail Azure.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> Nous pouvons également d’approvisionner la collection d’espace de travail hello et obtenir la clé d’accès via une API REST. toolearn, voir [API de fournisseur de ressources Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Création d’un fichier .pbix avec Power BI Desktop

Ensuite, nous devons créer la connexion de données hello et toobe rapports incorporés.
Pour cette tâche, aucune programmation et aucun code ne sont nécessaires. Nous n’utilisons que Power BI Desktop.
Dans cet article, nous n’entrerons via hello plus d’informations sur la toouse Power BI Desktop. Si vous avez besoin d’aide à ce sujet, consultez [Prise en main de Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). Dans notre exemple, nous allons simplement utiliser hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Création d’un espace de travail Power BI

Maintenant que hello configuration se fait, nous pouvons commencer la création d’espace de travail d’un client dans la collection d’espace de travail hello via les API REST. Hello suivant HTTP POST demande (REST) consiste à créer nouvel espace de travail hello dans notre collection d’espace de travail existant. Il s’agit de hello [API d’espace de travail POST](https://msdn.microsoft.com/library/azure/mt711503.aspx). Dans notre exemple, le nom de la collection hello espace de travail est **mypbiapp**. Nous venons de définir la clé d’accès hello, nous copiés précédemment, en tant que **AppKey**. C’est une authentification très simple !

**Demande HTTP**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**Réponse HTTP**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

Hello retourné **Id_espace_de_travail** est utilisé pour hello après les appels d’API suivants. Notre application doit conserver cette valeur.

## <a name="import-pbix-file-into-hello-workspace"></a>Importer le fichier .pbix dans l’espace de travail hello

Chaque rapport dans un espace de travail correspond tooa le fichier Power BI Desktop unique avec un jeu de données \(y compris les paramètres de source de données). Nous pouvons importer notre espace de travail toohello de fichier .pbix comme indiqué dans le code hello ci-dessous. Comme vous pouvez le voir, nous pouvons télécharger binaire hello du fichier .pbix à l’aide de MIME à parties multiples dans http.

fragment d’uri Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** est hello Id_espace_de_travail et paramètre de requête **datasetDisplayName** est toocreate de nom de dataset hello. Hello créé le jeu de données conserve toutes les données liées artefacts dans le fichier .pbix telles que les données importées, hello source de données de pointeur toohello, etc...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

Cette tâche d’importation peut prendre un certain temps. Lorsque vous avez terminé, notre application peut demander à l’état de la tâche hello à l’aide des id de l’importation. Dans notre exemple, id d’importation hello est **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

suivant de Hello demande état à l’aide de ce code d’importation :

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Si la tâche hello n’est pas terminée, hello réponse HTTP peut être comme suit :

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

Si la tâche hello est terminée, hello réponse HTTP peut être plus comme suit :

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>Connectivité de la source de données \(et architecture mutualisée des données)

Pendant presque tous les artefacts hello dans le fichier .pbix sont importés dans notre espace de travail, informations d’identification de hello pour les sources de données ne sont pas. Par conséquent, lorsque vous utilisez **mode DirectQuery**, hello rapport incorporé ne peut pas s’afficher correctement. Mais, lorsque vous utilisez **mode d’importation**, nous pouvons afficher le rapport de hello à l’aide de données importées de hello existant. Dans ce cas, nous devons définir des informations d’identification de hello à l’aide de hello via les appels REST comme suit.

Tout d’abord, nous devons obtenir la source de données de passerelle hello. Nous savons hello dataset **id** est hello précédemment retourné id.

**Demande HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**Réponse HTTP**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

À l’aide de hello retourné id de la passerelle et l’id de source de données \(voir hello précédente **gatewayId** et **id** Bonjour retourné de résultats), nous pouvons modifier les informations d’identification hello de cette source de données comme suit :

**Demande HTTP**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**Réponse HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

En production, nous pouvons également définir des chaîne de connexion différente hello pour chaque espace de travail à l’aide des API REST. \(Autrement dit, nous pouvons séparer de la base de données hello pour chaque client.)

suivant de Hello change chaîne de connexion hello de source de données via REST.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

Ou bien, nous pouvons utiliser la sécurité au niveau des lignes dans Power BI Embedded et nous pouvons séparer les données de hello tous les utilisateurs dans un rapport. Par conséquent, nous pouvons attribuer à chaque rapport client le même .pbix \(interface utilisateur, etc.) et différentes sources de données.

> [!NOTE]
> Si vous utilisez **mode d’importation** au lieu de **mode DirectQuery**, il n’existe aucun modèle de toorefresh moyen via l’API. Et les sources de données locales à travers la passerelle Power BI ne sont pas encore prises en charge dans Power BI Embedded. Toutefois, vous souhaiterez vraiment tookeep un œil sur hello [blog Power BI](https://powerbi.microsoft.com/blog/) pour quelles sont les nouveautés et les nouveautés à venir dans les futures versions.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Authentification et hébergement (incorporation) de rapports dans notre page web

Dans hello précédente API REST, nous pouvons utiliser la clé d’accès hello **AppKey** en tant que l’en-tête d’autorisation hello. Ces appels peuvent être gérées à côté de serveur principal hello, il est donc plus sûr.

Mais, lorsque nous incorporez des rapports de hello dans notre page web, ce type d’informations de sécurité serait géré à l’aide de JavaScript \(frontal). Puis la valeur de l’en-tête d’autorisation hello doit être sécurisé. Si notre clé d’accès est identifiée par un utilisateur ou du code malveillant, elle peut être utilisée pour appeler toutes les opérations.

Lorsque nous incorporez des rapports de hello dans notre page web, nous devons utiliser le jeton calculée de hello au lieu de la clé d’accès **AppKey**. Notre application doit créer hello OAuth Json Web Token \(JSON) qui se compose de revendications de hello et signature numérique calculée de hello. Comme illustré ci-dessous, cet OAuth JWT est un ensemble de tokens de chaînes encodés délimités par des points.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

Tout d’abord, nous devons préparer la valeur d’entrée de hello, qui est signée ultérieurement. Cette valeur est la chaîne hello en base64 encodé url (rfc4648) de hello suivant json, et ils sont délimités par point de hello \(.) caractères. Une version ultérieure, nous expliquons comment tooget hello id du rapport.

> [!NOTE]
> Si nous voulons toouse au niveau de sécurité des lignes avec Power BI Embedded, nous devons spécifier également **nom d’utilisateur** et **rôles** dans les revendications hello.

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

Ensuite, nous devons créer la chaîne codée en base64 de hello de HMAC \(signature de hello) avec l’algorithme SHA256. Cette valeur d’entrée signée est chaîne précédente de hello.

Enfin, nous devons combiner valeur d’entrée de hello et la chaîne de signature à l’aide de la période \(.) caractères. chaîne de Hello terminée est jeton d’application hello hello l’incorporation de rapport. Même si le jeton d’application hello est découvert par un utilisateur malveillant, ils ne peut pas récupérer la clé d’accès d’origine hello. Ce jeton d’application expirera rapidement.

Voici un exemple PHP de ces étapes :

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a>Enfin, incorporer des rapports de hello hello web page

L’incorporation de notre rapport, nous devons obtenir hello incorporer des url et au rapport **id** à l’aide de hello suivant l’API REST.

**Demande HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**Réponse HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

Nous pouvons incorporer des rapports de hello dans notre application web à l’aide du jeton d’application hello précédente.
Si nous examinons le code exemple suivant de hello, partie d’anciens hello est hello identique à l’exemple précédent de hello. Dans la dernière partie de hello, cet exemple montre hello **embedUrl** \(voir le résultat précédent de hello) de hello iframe et publie le jeton d’application hello dans hello iframe.

> [!NOTE]
> Vous devez toochange hello rapport id valeur tooone de votre choix. En outre, en raison du bogue tooa dans notre système de gestion de contenu, balise iframe de hello dans l’exemple de code hello est lu littéralement. Supprimez le texte hello limitée à partir de la balise de hello si vous copiez et collez cet exemple de code.

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

Et voici notre résultat :

![](media/power-bi-embedded-iframe/view-report.png)

À ce stade, Power BI Embedded affiche uniquement les rapports hello dans hello iframe. Mais garder un œil sur hello [Blog Power BI](https://powerbi.microsoft.com/blog/). Futures améliorations pourrait utiliser côté client nouvelle API qui sera nous envoyer des informations dans hello iframe ainsi que fournir des informations. C’est très intéressant !

## <a name="see-also"></a>Voir aussi
* [Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)

Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)

