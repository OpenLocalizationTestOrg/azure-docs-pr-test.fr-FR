---
title: aaaAuthenticating et autorisation avec Power BI Embedded
description: Authentification et autorisation avec Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Authentification et autorisation avec Power BI Embedded

Hello service Power BI Embedded utilise **clés** et **application jetons** pour l’authentification et d’autorisation, au lieu de l’authentification de l’utilisateur final explicite. Dans ce modèle, votre application gère l’authentification et l’autorisation de vos utilisateurs finaux. Lorsque cela est nécessaire, votre application crée et envoie les jetons d’application hello qui indique à notre toorender service hello rapport demandé. Cette conception ne requiert pas votre toouse application Azure Active Directory pour l’authentification des utilisateurs et l’autorisation, bien que vous puissiez toujours.

## <a name="two-ways-tooauthenticate"></a>Deux façons tooauthenticate

**Clé** : vous pouvez utiliser des clés pour tous les appels d’API REST Power BI Embedded. les clés Hello se trouvent dans hello **portail Azure** en cliquant sur **tous les paramètres** , puis **clés d’accès**. Traitez toujours votre clé comme s’il s’agissait d’un mot de passe. Ces clés ont toomake autorisations toute API REST appeler sur une collection de l’espace de travail particulier.

toouse une clé sur un appel REST, ajoutez hello suivant l’en-tête d’autorisation :            

    Authorization: AppKey {your key}

**Jeton d’application** : les jetons d’application sont utilisés pour toutes les demandes d’incorporation. Ils sont conçus toobe exécuter côté client, afin qu’elles soient restreints tooa unique tooset de pratique meilleur rapport et son délai d’expiration.

Les jetons d’application sont un JWT (JSON Web Token) signé par l’une de vos clés.

Votre jeton d’application peut contenir hello suivant revendications :

| Revendication | Description |
| --- | --- |
| **ver** |version de Hello du jeton d’application hello. 0.2.0 est la version actuelle de hello. |
| **aud** |Hello destiné destinataire du jeton de hello. Pour Power BI Embedded, utilisez : https://analysis.windows.net/powerbi/api. |
| **iss** |Chaîne indiquant l’application hello qui a émis le jeton de hello. |
| **type** |type Hello du jeton d’application en cours de création. Type hello uniquement pris en charge en cours est **incorporer**. |
| **wcn** |Jeton hello de nom d’espace de travail collection est émise. |
| **wid** |Le jeton d’espace de travail ID hello est envoyée. |
| **rid** |Le jeton d’état ID hello est envoyée. |
| **username** (facultatif) |Utilisé avec la sécurité RLS, ceci est une chaîne qui peut aider à identifier l’utilisateur de hello lors de l’application des règles RLS. |
| **roles** (facultatif) |Chaîne contenant le hello rôles tooselect lors de l’application des règles de sécurité de niveau ligne. Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes. |
| **scp** (facultatif) |Chaîne qui contient les étendues d’autorisations hello. Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes. |
| **exp** (facultatif) |Indique le temps hello dans le hello jeton expire. Les heures doivent être transmises en tant qu’horodatages Unix. |
| **nbf** (facultatif) |Indique le temps hello dans le hello jeton commence en cours valide. Les heures doivent être transmises en tant qu’horodatages Unix. |

Un exemple de jeton d’application doit ressembler à ceci :

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

Lorsqu’il est décodé, il doit ressembler à ceci :

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Méthodes sont disponibles dans les kits de développement logiciel qui facilitent la création d’apptokens de hello. Par exemple, pour .NET vous pouvez examiner hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) classe et hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) méthodes.

Pour hello .NET SDK, vous pouvez vous reporter trop[étendues](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Étendues

Lorsque vous utilisez les jetons incorporé, vous souhaiterez toorestrict de l’utilisation d’hello que vous autoriser à accéder. Dans cette optique, vous pouvez générer un jeton avec des autorisations étendues.

Hello Voici étendues disponibles de hello pour Power BI Embedded.

|Scope|Description|
|---|---|
|Dataset.Read|Fournit l’autorisation tooread hello spécifié le jeu de données.|
|Dataset.Write|Fournit des toohello de toowrite d’autorisation spécifié jeu de données.|
|Dataset.ReadWrite|Fournit le dataset sont recompilé toohello autorisation tooread et en écriture.|
|Report.Read|Fournit l’autorisation tooview hello spécifié de rapport.|
|Report.ReadWrite|Fournit la modifier et autorisation tooview hello rapport spécifié.|
|Workspace.Report.Create|Fournit des autorisation toocreate un nouveau rapport dans hello spécifié espace de travail.|
|Workspace.Report.Copy|Fournit des autorisation tooclone un rapport existant dans hello spécifié espace de travail.|

Vous pouvez fournir plusieurs étendues à l’aide d’un espace entre les portées hello hello suivante.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Revendications requises - Étendues**

SCP : {scopesClaim} scopesClaim peut être une chaîne ou un tableau de chaînes, en notant hello les autorisations accordées tooworkspace ressources (rapports, jeu de données, etc.).

Un jeton décodé, avec des étendues définies, se présenterait comme toohello suivant.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>Opérations et étendues

|Opération|Ressource cible|Autorisations du jeton|
|---|---|---|
|Créer (en mémoire) un rapport basé sur un jeu de données.|Jeu de données|Dataset.Read|
|Créer (mémoire) un rapport basé sur un jeu de données et enregistrer le rapport de hello.|Jeu de données|* Dataset.Read<br>* Workspace.Report.Create|
|Afficher et explorer/modifier (en mémoire) un rapport existant. Report.Read implies Dataset.Read. Cela n’autorise pas les autorisations toosave modifications.|Rapport|Report.Read|
|Modifier et enregistrer un rapport existant.|Rapport|Report.ReadWrite|
|Enregistrer la copie d’un rapport (Enregistrer sous).|Rapport|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Voici comment fonctionne les flux de hello
1. Copiez hello API clés tooyour application. Vous pouvez obtenir les clés hello **Azure Portal**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. Le jeton envoie une revendication et comporte un délai d'expiration.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. Le jeton est signé à l’aide des clés d'accès API.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. Utilisateur demande tooview un rapport.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. Le jeton est validé à l’aide d’une clé d'accès API.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded envoie un rapport toouser.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Après avoir **Power BI Embedded** envoie un utilisateur toohello de rapports, utilisateur de hello peut afficher des rapports de hello dans votre application personnalisée. Par exemple, si vous avez importé hello [exemple d’analyse de vente données PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello exemple d’application web ressemble à ceci :

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Voir aussi

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Prise en main de l’exemple Microsoft Power BI Embedded Preview](power-bi-embedded-get-started-sample.md)  
[Scénarios Microsoft Power BI Embedded courants](power-bi-embedded-scenarios.md)  
[Prise en main de Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Dépôt Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)

