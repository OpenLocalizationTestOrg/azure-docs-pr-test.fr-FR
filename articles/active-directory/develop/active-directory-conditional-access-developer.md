---
title: "aaaDeveloper des conseils pour l’accès conditionnel Azure Active Directory | Documents Microsoft"
description: "Guide du développeur et scénarios pour l’accès conditionnel à Azure AD"
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Guide du développeur pour l’accès conditionnel à Azure Active Directory

Azure Active Directory (AD) offre plusieurs façons toosecure votre application et protéger un service.  Une de ces fonctionnalités uniques est l’accès conditionnel.  Accès conditionnel permet aux développeurs et des services tooprotect de clients d’entreprise dans une multitude de façons, notamment :

* Authentification multifacteur
* Autoriser uniquement Intune inscrit des services spécifiques de périphériques tooaccess
* Restriction des plages IP et emplacements utilisateur

Pour plus d’informations sur les fonctionnalités complètes hello de l’accès conditionnel, consultez [l’accès conditionnel dans hello portail Azure classic](../active-directory-conditional-access.md). 

Dans cet article, nous nous concentrer sur les accès conditionnel signifie toodevelopers génération d’applications pour Azure AD.  Il suppose des connaissances [d’applications uniques](active-directory-integrating-applications.md) et [mutualisées](active-directory-devhowto-multi-tenant-overview.md) et [des modèles courants d’authentification](active-directory-authentication-scenarios.md).

Nous allons approfondir impact hello de l’accès aux ressources que vous ne contrôlez pas et qui peuvent avoir des stratégies d’accès conditionnel appliquées.  En outre, nous explorons hello implications en matière d’accès conditionnel dans le flux de la part de hello, des applications web, l’accès hello Microsoft Graph et appeler des API.

## <a name="how-does-conditional-access-impact-an-app"></a>Comment l’accès conditionnel impacte-t-il une application ?

### <a name="app-topologies-impacted"></a>Topologies d’application affectées

Dans les scénarios les plus courants, l’accès conditionnel ne modifie pas le comportement d’une application ou nécessite des modifications du développeur de hello.  Que dans certains cas lorsqu’une application en mode silencieux ou indirectement demande un jeton pour un service, une application requiert des modifications de code défis « toohandle accès conditionnel ».  Cela peut être aussi simple que l’exécution d’une demande de connexion interactive. 

Plus particulièrement, hello scénarios suivants requièrent accès conditionnel du code toohandle « défis » : 

* Applications qui accèdent au hello Microsoft Graph
* Applications effectuant hello sur à la place de flux
* Applications accédant à plusieurs services/ressources
* Applications à page unique en utilisant ADAL.js

Stratégies d’accès conditionnel peut être appliqué toohello application, mais peut également être appliqué tooa web API votre application accède. toolearn savoir plus sur comment tooconfigure une stratégie d’accès conditionnel, consultez [mise en route avec un accès conditionnel Azure Active Directory](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules).

Selon le scénario de hello, un client d’entreprise peut appliquer et supprimer des stratégies d’accès conditionnel à tout moment.  Votre application toocontinue de fonctionnement lorsqu’une nouvelle stratégie est appliquée, vous devez la gestion de stimulation « tooimplement hello ». Hello exemple suivant illustre la gestion de la demande d’accès. 

### <a name="conditional-access-examples"></a>Exemples d’accès conditionnel

Certains scénarios requièrent code change toohandle l’accès conditionnel, tandis que d’autres en l’état du travail.  Voici quelques scénarios à l’aide de l’authentification multifacteur accès conditionnel toodo qui donne une idée de la différence de hello.

* Vous générez une application iOS de client unique et appliquez une stratégie d’accès conditionnel.  application Hello se connecte un utilisateur et ne demande l’accès tooan API.  Lorsque hello utilisateur se connecte, hello stratégie est automatiquement appelée et l’utilisateur hello doit tooperform l’authentification multifacteur (MFA). 
* Vous générez une application web d’architecture mutualisée qui utilise hello Microsoft Graph tooaccess Exchange, entre autres services.  Un client d’entreprise qui adopte cette application définit une stratégie sur SharePoint Online.  Lorsque l’application hello web demande un jeton MS Graph, une stratégie sur tous les services Microsoft est appliquée (en particulier les services qui sont accessibles via le graphique).  Cet utilisateur final est invité à fournir l’authentification multifacteur. Dans les cas de hello, l’utilisateur final hello est connecté avec des jetons valides, un défi « revendications » est renvoyé à l’application web toohello.  
* Vous générez une application native qui utilise un Bonjour de tooaccess de service de couche intermédiaire Microsoft Graph.  Un client d’entreprise au niveau de l’entreprise hello à l’aide de cette application s’applique à un tooExchange de stratégie en ligne.  Lorsqu’un utilisateur final se connecte à la couche intermédiaire toohello d’accès aux demandes hello application native et envoie le jeton de hello.  niveau intermédiaire de Hello effectue sur la part de flux toorequest accès toohello MS Graph.  À ce stade, un défi « revendications » est présenté intermédiaire toohello. niveau intermédiaire de Hello envoie hello stimulation toohello arrière application native, qui doit toocomply avec la stratégie d’accès conditionnel hello.

### <a name="complying-with-a-conditional-access-policy"></a>Conformité à une stratégie d’accès conditionnel

Pour plusieurs topologies d’application différents, une stratégie d’accès conditionnel est évaluée lors de la session de hello est établie.  Comme une stratégie d’accès conditionnel fonctionne à l’échelle de hello d’applications et services, point hello à laquelle elle est appelée dépend fortement sur le scénario de hello que vous essayez de tooaccomplish.

Quand votre application tente de tooaccess un service avec une stratégie d’accès conditionnel, il peut rencontrer une vérification d’accès conditionnel.  Cette demande est encodée dans hello `claims` paramètre qui est fourni dans la réponse d’Azure AD ou hello Microsoft Graph.  Voici un exemple de ce paramètre de défi : 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Les développeurs peuvent prendre ce défi et l’ajouter dans une nouvelle tooAzure de requête AD.  Passer l’état de cet demande tooperform de l’utilisateur final hello tout toocomply nécessaire d’action avec la stratégie d’accès conditionnel hello. Bonjour les scénarios suivants, les détails de l’erreur de hello et comment tooextract hello paramètre sont expliqués. 

## <a name="scenarios"></a>Scénarios

### <a name="prerequisites"></a>Composants requis

L’accès conditionnel Azure AD est une fonctionnalité inclue dans [Azure AD Premium](../active-directory-whatis.md#choose-an-edition).  Des informations complémentaires sur les licences requises Bonjour [rapport d’utilisation sans licence](../active-directory-conditional-access-unlicensed-usage-report.md).  Les développeurs peuvent joindre hello [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), qui inclut un toohello abonnement gratuit Enterprise Mobility Suite, qui inclut Azure AD Premium.

### <a name="considerations-for-specific-scenarios"></a>Considérations pour des scénarios spécifiques

Hello uniquement les informations suivantes s’appliquent dans ces scénarios d’accès conditionnel :

* Applications qui accèdent au hello Microsoft Graph
* Applications effectuant hello sur à la place de flux
* Applications accédant à plusieurs services/ressources
* Applications à page unique en utilisant ADAL.js

Bonjour les sections suivantes, nous aborderons commun scénarios dans lesquels sont plus complexes.  core Hello principe de fonctionnement est l’accès conditionnel, les stratégies sont évaluées au moment de hello hello jeton est demandé pour le service hello qui comporte une stratégie de l’accès conditionnel, sauf si elle est accessible via hello Microsoft Graph.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Scénario : Application accéder à hello Microsoft Graph

Dans ce scénario, nous guider les cas de hello lorsqu’une application web demande accès toohello Microsoft Graph. stratégie d’accès conditionnel Hello dans ce cas peut être attribuée tooSharePoint, Exchange ou un autre service qui est accessible en tant qu’une charge de travail via hello Microsoft Graph.  Dans cet exemple, supposons qu’il existe une stratégie d’accès conditionnel sur Sharepoint Online.

![Diagramme de flux Microsoft Graph hello de l’accès à des applications](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

application Hello demande d’autorisation toohello Microsoft Graph qui nécessite l’accès à une charge de travail en aval sans accès conditionnel.  demande de Hello aboutit sans appeler n’importe quelle stratégie et application hello reçoit les jetons de Microsoft Graph.  À ce stade, application hello peut utiliser le jeton d’accès hello dans une demande de support pour le point de terminaison hello demandé. Maintenant, hello application a besoin tooaccess un point de terminaison Sharepoint Online de Microsoft Graph, par exemple :`https://graph.microsoft.com/v1.0/me/mySite`

application Hello possède déjà un jeton valide pour hello Microsoft Graph, afin d’exécuter nouvelle demande de hello sans un nouveau jeton émis. Cette demande échoue et un défi de revendications est émis à partir de Microsoft Graph sous forme de hello d’un HTTP 403 Interdit avec un ```WWW-Authenticate``` défi.
Voici un exemple de réponse de hello : 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

Hello revendications défi consiste à l’intérieur de hello ```WWW-Authenticate``` en-tête qui peut être analysé tooextract hello revendications paramètre pour la prochaine demande de hello.  Une fois ajouté toohello nouvelle demande, Azure AD connaît stratégie d’accès conditionnel tooevaluate hello lors de l’ouverture de session utilisateur de hello et application hello est désormais conforme à la stratégie d’accès conditionnel hello.  Point de terminaison extensible toohello de demande hello Sharepoint Online réussit.

Pour des exemples de code qui montrent comment toohandle hello revendications défi, consultez toohello [exemple de code .NET Desktop](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) ADAL .NET ou hello [exemple de code de la part de](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) pour .NET de la bibliothèque ADAL.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Scénario : Application exécution hello sur à la place de flux

Dans ce scénario, nous guider cas hello dans laquelle une application native appelle une API du service web /.  À son tour, fait de ce service [hello « de la part de » flux](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall un service en aval.  Dans notre cas, nous avoir appliqué à notre service en aval accès conditionnel stratégie toohello (API Web 2) et utilisez une application native, plutôt qu’une application démon/serveur. 

![Application effectuant hello sur à la place de diagramme de flux](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

demande de jeton initial Hello pour API Web 1 n’affiche aucune invite l’utilisateur final hello pour l’authentification multifacteur que l’API Web 1 ne peut pas atteindre toujours les API en aval hello.  Une fois que l’API Web 1 tente de toorequest un utilisateur d’émission de jeton de la part de hello pour API Web 2, demande de hello échoue, car l’utilisateur de hello n’a pas été signé avec l’authentification multifacteur.

Azure AD renvoie une réponse HTTP avec des données intéressantes : 

> [!NOTE]
> Dans ce cas, il est une description d’erreur de l’authentification multifacteur, mais il existe une large gamme de `interaction_required` accès tooconditional correspondantes.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Dans notre API Web 1, nous interceptons l’erreur de hello `error=interaction_required`et envoyer hello arrière `claims` application de bureau toohello défi.  À ce stade, l’application de bureau hello faire une nouvelle `acquireToken()` appeler et ajouter hello `claims`défi comme un paramètre de chaîne de requête supplémentaires.  Cette nouvelle demande requiert une authentification multifacteur de hello utilisateur toodo, puis envoyer ce nouveau jeton précédent tooWeb API 1 et le hello complète de la part de flux.

tootry ce scénario, consultez notre [exemple de code .NET](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Il montre comment toopass hello défi de revendications de l’application native de toohello API Web 1 et construire une nouvelle demande au sein de l’application cliente de hello. 

### <a name="scenario-app-accessing-multiple-services"></a>Scénario : applications accédant à plusieurs services

Dans ce scénario, nous guider les cas de hello dans lequel une application web accède aux deux services dont a affectée une stratégie d’accès conditionnel.  En fonction de votre logique d’application, il peut exister un chemin d’accès dans lequel votre application ne nécessite pas d’accès tooboth web services.  Dans ce scénario, commande hello dans lequel vous demandez un jeton joue un rôle important dans l’expérience de l’utilisateur final hello.

Supposons que nous disposons d’un service Web A et B et que le service Web B applique notre stratégie d’accès conditionnel.  Lors de la demande d’authentification interactive initiale hello requiert le consentement pour les deux services, la stratégie d’accès conditionnel hello n’est pas nécessaire dans tous les cas.  Si l’application hello demande un jeton pour le service web B, puis hello stratégie est appelée et les demandes suivantes pour le service web A réussit également comme suit.

![Application accédant à un diagramme de flux multi-services](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

Ou bien, si l’application hello demande initialement un jeton d’un service web, l’utilisateur final hello n’appelle pas la stratégie d’accès conditionnel hello.  Cela permet à l’utilisateur final toocontrol hello développeur d’application hello et ne force pas toobe de stratégie d’accès conditionnel hello appelée dans tous les cas. les cas délicate Hello sont si hello application demande ensuite un jeton pour le service web B. À ce stade, l’utilisateur final hello doit toocomply avec la stratégie d’accès conditionnel hello.  Lorsque l’application hello tente trop`acquireToken`, il peut générer hello (illustrée dans hello suivant schéma) de l’erreur suivante : 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![Application accédant à plusieurs services demandant un nouveau jeton](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Si l’application hello utilise la bibliothèque ADAL de hello, un jeton de hello tooacquire échec est toujours une nouvelle tentative interactivement.  Lorsque cette requête se produit, l’utilisateur final hello a toocomply d’opportunité hello avec l’accès conditionnel hello.  Cela est vrai, sauf si la demande de hello est un `AcquireTokenSilentAsync` ou `PromptBehavior.Never` dans ce cas application hello doit tooperform interactif ```AcquireToken``` demande toogive hello utilisations hello opportunité toocomply avec la stratégie de hello. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>Scénario : application à page unique (SPA) en utilisant ADAL.js

Dans ce scénario, nous décrivons les cas de hello lorsque nous avons une application à page unique (SPA), à l’aide de ADAL.js toocall un accès conditionnel protégées API web.  Ceci est une architecture simple mais a des nuances qui doivent toobe pris en compte lors du développement autour de l’accès conditionnel.

Dans ADAL.js, il existe quelques fonctions qui obtiennent des jetons : `login()`, `acquireToken(...)`, `acquireTokenPopup(…)`, et `acquireTokenRedirect(…)`. 

* `login()`Obtient un jeton d’ID via une demande de connexion interactive, mais n’obtient pas les jetons d’accès pour n’importe quel service (y compris une API Web protégée par l’accès conditionnel).  
* `acquireToken(…)`peut ensuite être toosilently utilisé obtenir un jeton d’accès c'est-à-dire qu’il n’affiche pas l’interface utilisateur dans les cas.  
* `acquireTokenPopup(…)`et `acquireTokenRedirect(…)` sont les deux toointeractively utilisé demander un jeton pour une ressource, c'est-à-dire qu’ils affichent toujours l’authentification dans l’interface utilisateur.

Lorsqu’une application a besoin d’un toocall de jeton d’accès une API Web, il tente une `acquireToken(…)`.  Si la session de jeton hello a expiré ou que nous devons toocomply avec une stratégie d’accès conditionnel, puis hello *acquireToken* la fonction échoue et hello application utilise `acquireTokenPopup()` ou `acquireTokenRedirect()`.

![Application à page unique en utilisant le diagramme de flux ADAL](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

Examinons un exemple avec notre scénario d’accès conditionnel.  l’utilisateur final Hello simplement étant récupérées sur le site de hello et qu’il n’a pas une session.  Nous effectuons un appel `login()` et obtenons un jeton d’ID sans authentification multifacteur.  Puis utilisateur de hello appuie sur un bouton qui requiert des données de toorequest hello application à partir d’une API web.  application Hello tente toodo un `acquireToken()` appel échoue, mais étant donné que l’utilisateur de hello n’a pas effectué l’authentification multifacteur encore et a besoin de toocomply avec la stratégie d’accès conditionnel hello.

Azure AD envoie hello différé suivant la réponse HTTP : 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

Notre application a besoin toocatch hello `error=interaction_required`.  Hello application peut utiliser ensuite soit `acquireTokenPopup()` ou `acquireTokenRedirect()` sur hello même ressource.  l’utilisateur Hello est forcé toodo une authentification multifacteur. Utilisateur de hello après l’authentification multifacteur hello, application hello est émise une nouvelle ressource de jeton d’accès pour hello demandée.

tootry ce scénario, consultez notre [exemple de code de la part de JS SPA](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Cet exemple de code utilise la stratégie d’accès conditionnel hello et web API vous précédemment inscrites avec un toodemonstrate JS SPA ce scénario. Il montre comment tooproperly handle hello revendications stimulation et obtient un jeton d’accès qui peut être utilisé pour votre API Web. Vous pouvez également les hello extraction général [exemple de code Angular.js](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) pour obtenir des conseils sur une SPA angulaire


## <a name="see-also"></a>Voir aussi

* toolearn en savoir plus sur les fonctionnalités de hello, consultez [accès conditionnel dans Azure AD](../active-directory-conditional-access.md).
* Pour obtenir plus d’exemples de code Azure AD, consultez [Référentiel Github d’exemples de code](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory). 
* Pour plus d’informations sur hello une documentation de référence du Kit de développement ADAL et l’accès hello, consultez [guide de la bibliothèque](active-directory-authentication-libraries.md).
* toolearn en savoir plus sur les scénarios mutualisés, consultez [comment toosign les utilisateurs à l’aide du modèle d’architecture mutualisée hello](active-directory-devhowto-multi-tenant-overview.md).
