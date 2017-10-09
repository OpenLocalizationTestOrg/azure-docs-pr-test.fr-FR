---
title: demandes de toogenerate HTTP de service de gestion des API aaaUsing
description: "Découvrez les stratégies de demande et de réponse toouse dans Gestion des API toocall des services externes à partir de votre API"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a>À l’aide des services externes à partir de hello service de gestion des API Azure
stratégies de Hello disponibles dans le service de gestion des API Azure faire un large éventail de tâches utiles dépend uniquement de demande entrante de hello, la réponse sortante hello et les informations de configuration de base. Toutefois, les stratégies qui est en mesure de toointeract avec des services externes à partir de la gestion des API ouvre opportunités plus nombreuses.

Nous l’avons déjà vu comment nous pouvons interagissent avec hello [service de concentrateur d’événements Azure pour la journalisation, la surveillance et analytique](api-management-log-to-eventhub-sample.md). Dans cet article, nous allons vous montrer service basé sur des stratégies qui vous toointeract avec n’importe quel HTTP externe. Ces stratégies peuvent être utilisés pour déclencher des événements à distance ou pour récupérer des informations qui seront demande d’origine de hello toomanipulate utilisés et de réponse d’une certaine façon.

## <a name="send-one-way-request"></a>Send-One-Way-Request (Envoyer une requête à sens unique)
Hello interaction externe la plus simple est probablement style d’incendie et oubliez hello de requête qui permet une toobe de service externe notifié d’un type d’événement important. Nous pouvons utiliser la stratégie de flux de contrôle hello `choose` toodetect n’importe quel type de condition qui nous intéressent et ensuite, si hello condition est satisfaite, nous pouvons effectuer une demande HTTP externe à l’aide de hello [envoyer un moyen de demande](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) stratégie. Cela peut être un tooa demande système comme Hipchat Slack ou d’une API de messagerie comme SendGrid ou MailChimp de messagerie, ou pour les incidents de support critiques quelque chose comme PagerDuty. Tous ces systèmes de messagerie ont des API HTTP simples que nous pouvons facilement appeler.

### <a name="alerting-with-slack"></a>Alerte avec Slack
Hello l’exemple suivant montre comment toosend un tooa message marge salle de conversation si le code hello d’état de réponse HTTP est supérieur ou égal à too500. Une erreur de 500 plage indique un problème avec nos API de serveur principal qui hello client de notre API ne peut pas résoudre d’eux-mêmes. Elle nécessite généralement une intervention de notre part.  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

Marge a notion hello des raccordements de web entrantes. Lorsque vous configurez un raccordement web entrantes, Slack génère une URL spéciale qui vous permet de toodo une demande POST simple et toopass un message dans le canal de marge hello. Hello corps JSON que vous créez est basée sur un format défini par la marge.

![Webhook Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>Le style « fire and forget » est-il suffisant ?
L’utilisation d’un style « fire and forget » de requête implique certains compromis. Si, pour une raison quelconque, hello demande échoue, puis Échec de hello n’est pas signalée. Dans ce cas particulier, la complexité hello de disposer d’un système de notification d’échec secondaire et le coût de performances supplémentaires hello d’attente d’une réponse de hello n’est pas justifiée. Pour les scénarios où il s’agit toocheck essentielles hello, puis hello [demande d’envoi](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) stratégie est une meilleure option.

## <a name="send-request"></a>send-request
Hello `send-request` permet de stratégie à l’aide d’un service externe de tooperform complexe de traitement des fonctions et données de retour toohello API management service qui peuvent être utilisée pour la poursuite du traitement de stratégie.

### <a name="authorizing-reference-tokens"></a>Autorisation des jetons de référence
Une fonction majeure de la gestion des API consiste à protéger les ressources principales. Si le serveur d’autorisation de hello utilisé par votre API crée [jetons JWT](http://jwt.io/) dans le cadre de son flux OAuth2, en tant que [Azure Active Directory](../active-directory/active-directory-aadconnect.md) est le cas, vous pouvez ensuite utiliser hello `validate-jwt` validité de hello tooverify de stratégie de jeton de Hello. Toutefois, certains serveurs d’autorisation créent sont appelées [référence jetons](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) qui ne peut pas être vérifié sans passer d’un serveur d’autorisation de toohello précédent appel.

### <a name="standardized-introspection"></a>Introspection normalisée
Hello passée il n’y a eu aucun moyen normalisé de vérification d’un jeton de référence avec un serveur d’autorisation. Cependant une norme récemment [RFC 7662](https://tools.ietf.org/html/rfc7662) a été publiée par hello IETF qui définit comment un serveur de ressources peut vérifier la validité hello d’un jeton.

### <a name="extracting-hello-token"></a>Extraction du jeton de hello
première étape de Hello est jeton de hello tooextract à partir de l’en-tête d’autorisation hello. valeur d’en-tête Hello doit être formaté avec hello `Bearer` schéma d’autorisation, un espace unique et l’autorisation de hello puis jeton en tant que par [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1). Malheureusement, il existe des cas où le schéma d’autorisation de hello est omis. tooaccount pour cela lors de l’analyse, nous diviser la valeur d’en-tête de hello sur un espace et la chaîne hello sélectionnez dernière hello retourné du tableau de chaînes. Une solution de contournement est ainsi trouvée pour les en-têtes d’autorisation mal formés.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Demande de validation hello
Une fois le jeton d’autorisation hello, nous permettent de jeton de hello demande toovalidate hello. RFC 7662 appelle introspection de ce processus et exige que vous `POST` une ressource d’introspection de toohello de formulaire HTML. Hello formulaire HTML doit contenir au moins une paire clé/valeur avec la clé de hello `token`. Cette demande adressée au serveur d’autorisation toohello doit également être authentifié tooensure que des clients malveillants ne peuvent pas atteindre chalutage pour les jetons valides.

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-hello-response"></a>La vérification de la réponse de hello
Hello `response-variable-name` attribut est hello d’accès utilisé toogive a retourné une réponse. Hello nom défini dans cette propriété peut être utilisé comme une clé dans hello `context.Variables` hello tooaccess de dictionnaire `IResponse` objet.

À partir de l’objet de réponse hello, nous pouvons récupérer les corps hello et RFC 7622 nous indique que la réponse de hello doit être un objet JSON et doit contenir au moins une propriété appelée `active` qui est une valeur booléenne. Lorsque `active` est true, le jeton de hello est considéré comme valid.

### <a name="reporting-failure"></a>Signalement d’un échec
Nous utilisons un `<choose>` stratégie toodetect si le jeton de hello n’est pas valide et le cas échéant, renvoyer une réponse 401.

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

Comme pour [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) qui décrit comment `bearer` jetons doivent être utilisés, nous avons également retourner un `WWW-Authenticate` l’en-tête de réponse de hello 401. Hello WWW-Authenticate est prévue tooinstruct un client sur la façon de tooconstruct une demande correctement autorisée. En raison de toohello diverses approches possibles avec les framework hello OAuth2, il est difficile toocommunicate tous hello informations sont nécessaires. Heureusement des efforts en cours d’exécution toohelp [clients découvrir comment tooproperly autoriser le serveur de ressources de demandes tooa](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).

### <a name="final-solution"></a>Solution finale
Assembler tous les éléments de hello, nous obtenons hello suivant de stratégie :

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

Il existe un seul de nombreux exemples de hello `send-request` stratégie peut être des services externes utile toointegrate utilisés dans les processus hello des demandes et réponses transitant par le service de gestion des API de hello.

## <a name="response-composition"></a>Rédaction de réponse
Hello `send-request` stratégie peut être utilisée pour améliorer un système principal demande tooa principal, comme nous l’avons vu dans l’exemple précédent de hello, ou il peut être utilisé comme un remplacement complet pour d’appel de back-end hello. À l’aide de cette technique, nous pouvons facilement créer des ressources composites qui sont agrégées à partir de plusieurs systèmes différents.

### <a name="building-a-dashboard"></a>Génération d’un tableau de bord
Parfois, vous souhaitez toobe tooexpose en mesure d’informations qui existe dans plusieurs systèmes principaux, par exemple, toodrive un tableau de bord. Hello, indicateurs de performance clés proviennent de tous les principaux différents, mais vous préférez pas les toothem tooprovide un accès direct, et il peut être intéressant si toutes les informations de hello pu être récupérées dans une demande unique. Peut-être que certaines informations de serveur principal hello doit certains découpage et découper et expurgation un peu de tout d’abord ! Qui est en mesure de toocache que la ressource composite serait un tooreduce utile hello principal charger puisque vous savez que les utilisateurs ont l’habitude de marteler la touche F5 de hello dans l’ordre toosee si leurs mesures peu performantes peuvent changer.    

### <a name="faking-hello-resource"></a>Ressource de hello émulant
Hello première étape toobuilding nos ressources de tableau de bord est tooconfigure une nouvelle opération dans le portail de publication de gestion des API hello. Cela sera un tooconfigure d’opération utilisée espace réservé de notre toobuild de stratégie de composition notre ressource dynamique.

![Opération de tableau de bord](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Effectuant des demandes de hello
Une fois hello `dashboard` opération a été créée. nous pouvons configurer une stratégie spécifiquement pour cette opération. 

![Opération de tableau de bord](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

première étape de Hello est tooextract tous les paramètres de requête à partir de la demande entrante de hello, afin que nous pouvons transmettre tooour principal. Dans cet exemple, notre tableau de bord affiche des informations selon une période ; il comporte donc un paramètre `fromDate` et `toDate`. Nous pouvons utiliser hello `set-variable` stratégie tooextract hello plus d’informations à partir de l’URL de demande hello.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

Une fois ces informations nous pouvons effectuer des demandes systèmes principaux de hello tooall. Chaque requête construit une nouvelle URL avec informations de paramètre hello et appelle son propre serveur et stocke la réponse de hello dans une variable de contexte.

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

Ces requêtes s’exécutent en séquence, ce qui n’est pas idéal. Dans une prochaine version nous présenterons une nouvelle stratégie nommée `wait` qui activera tous ces tooexecute de requêtes en parallèle.

### <a name="responding"></a>Réponse
Nous pouvons utiliser hello du réponse composite hello tooconstruct [retour-réponse](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) stratégie. Hello `set-body` élément peut utiliser une expression tooconstruct un nouveau `JObject` avec toutes les représentations de composant hello incorporées en tant que propriétés.

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

stratégie complète de Hello se présente comme suit :

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

Dans la configuration de hello d’opération d’espace réservé de hello, nous pouvons configurer hello du tableau de bord ressources toobe mis en cache pour au moins une heure, car nous sommes conscients de nature hello de données de hello signifie que, même s’il s’agit d’une heure plus à jour, qu'il sera toujours suffisamment efficace utilisateurs de toohello tooconvey des informations précieuses.

## <a name="summary"></a>Résumé
Service de gestion des API Azure fournit des stratégies souples qui peuvent être de manière sélective appliquées tooHTTP trafic et composition de services principaux. Si vous souhaitez tooenhance votre passerelle API avec la génération d’alertes de fonctions, la vérification des fonctionnalités de validation ou de créez des ressources composites en fonction de plusieurs services principaux, hello `send-request` et les stratégies associées ouvrir un monde de possibilités.

## <a name="watch-a-video-overview-of-these-policies"></a>Regarder une vidéo de présentation de ces stratégies.
Pour plus d’informations sur hello [envoyer un moyen de demande](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [demande d’envoi](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), et [retour-réponse](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) stratégies abordées dans cet article, veuillez consulter hello suivant vidéo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

