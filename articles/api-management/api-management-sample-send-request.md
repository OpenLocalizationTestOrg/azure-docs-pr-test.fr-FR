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
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="af163-103">À l’aide des services externes à partir de hello service de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="af163-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="af163-104">stratégies de Hello disponibles dans le service de gestion des API Azure faire un large éventail de tâches utiles dépend uniquement de demande entrante de hello, la réponse sortante hello et les informations de configuration de base.</span><span class="sxs-lookup"><span data-stu-id="af163-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="af163-105">Toutefois, les stratégies qui est en mesure de toointeract avec des services externes à partir de la gestion des API ouvre opportunités plus nombreuses.</span><span class="sxs-lookup"><span data-stu-id="af163-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="af163-106">Nous l’avons déjà vu comment nous pouvons interagissent avec hello [service de concentrateur d’événements Azure pour la journalisation, la surveillance et analytique](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="af163-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="af163-107">Dans cet article, nous allons vous montrer service basé sur des stratégies qui vous toointeract avec n’importe quel HTTP externe.</span><span class="sxs-lookup"><span data-stu-id="af163-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="af163-108">Ces stratégies peuvent être utilisés pour déclencher des événements à distance ou pour récupérer des informations qui seront demande d’origine de hello toomanipulate utilisés et de réponse d’une certaine façon.</span><span class="sxs-lookup"><span data-stu-id="af163-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="af163-109">Send-One-Way-Request (Envoyer une requête à sens unique)</span><span class="sxs-lookup"><span data-stu-id="af163-109">Send-One-Way-Request</span></span>
<span data-ttu-id="af163-110">Hello interaction externe la plus simple est probablement style d’incendie et oubliez hello de requête qui permet une toobe de service externe notifié d’un type d’événement important.</span><span class="sxs-lookup"><span data-stu-id="af163-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="af163-111">Nous pouvons utiliser la stratégie de flux de contrôle hello `choose` toodetect n’importe quel type de condition qui nous intéressent et ensuite, si hello condition est satisfaite, nous pouvons effectuer une demande HTTP externe à l’aide de hello [envoyer un moyen de demande](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) stratégie.</span><span class="sxs-lookup"><span data-stu-id="af163-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="af163-112">Cela peut être un tooa demande système comme Hipchat Slack ou d’une API de messagerie comme SendGrid ou MailChimp de messagerie, ou pour les incidents de support critiques quelque chose comme PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="af163-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="af163-113">Tous ces systèmes de messagerie ont des API HTTP simples que nous pouvons facilement appeler.</span><span class="sxs-lookup"><span data-stu-id="af163-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="af163-114">Alerte avec Slack</span><span class="sxs-lookup"><span data-stu-id="af163-114">Alerting with Slack</span></span>
<span data-ttu-id="af163-115">Hello l’exemple suivant montre comment toosend un tooa message marge salle de conversation si le code hello d’état de réponse HTTP est supérieur ou égal à too500.</span><span class="sxs-lookup"><span data-stu-id="af163-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="af163-116">Une erreur de 500 plage indique un problème avec nos API de serveur principal qui hello client de notre API ne peut pas résoudre d’eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="af163-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="af163-117">Elle nécessite généralement une intervention de notre part.</span><span class="sxs-lookup"><span data-stu-id="af163-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="af163-118">Marge a notion hello des raccordements de web entrantes.</span><span class="sxs-lookup"><span data-stu-id="af163-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="af163-119">Lorsque vous configurez un raccordement web entrantes, Slack génère une URL spéciale qui vous permet de toodo une demande POST simple et toopass un message dans le canal de marge hello.</span><span class="sxs-lookup"><span data-stu-id="af163-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="af163-120">Hello corps JSON que vous créez est basée sur un format défini par la marge.</span><span class="sxs-lookup"><span data-stu-id="af163-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Webhook Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="af163-122">Le style « fire and forget » est-il suffisant ?</span><span class="sxs-lookup"><span data-stu-id="af163-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="af163-123">L’utilisation d’un style « fire and forget » de requête implique certains compromis.</span><span class="sxs-lookup"><span data-stu-id="af163-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="af163-124">Si, pour une raison quelconque, hello demande échoue, puis Échec de hello n’est pas signalée.</span><span class="sxs-lookup"><span data-stu-id="af163-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="af163-125">Dans ce cas particulier, la complexité hello de disposer d’un système de notification d’échec secondaire et le coût de performances supplémentaires hello d’attente d’une réponse de hello n’est pas justifiée.</span><span class="sxs-lookup"><span data-stu-id="af163-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="af163-126">Pour les scénarios où il s’agit toocheck essentielles hello, puis hello [demande d’envoi](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) stratégie est une meilleure option.</span><span class="sxs-lookup"><span data-stu-id="af163-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="af163-127">send-request</span><span class="sxs-lookup"><span data-stu-id="af163-127">Send-Request</span></span>
<span data-ttu-id="af163-128">Hello `send-request` permet de stratégie à l’aide d’un service externe de tooperform complexe de traitement des fonctions et données de retour toohello API management service qui peuvent être utilisée pour la poursuite du traitement de stratégie.</span><span class="sxs-lookup"><span data-stu-id="af163-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="af163-129">Autorisation des jetons de référence</span><span class="sxs-lookup"><span data-stu-id="af163-129">Authorizing reference tokens</span></span>
<span data-ttu-id="af163-130">Une fonction majeure de la gestion des API consiste à protéger les ressources principales.</span><span class="sxs-lookup"><span data-stu-id="af163-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="af163-131">Si le serveur d’autorisation de hello utilisé par votre API crée [jetons JWT](http://jwt.io/) dans le cadre de son flux OAuth2, en tant que [Azure Active Directory](../active-directory/active-directory-aadconnect.md) est le cas, vous pouvez ensuite utiliser hello `validate-jwt` validité de hello tooverify de stratégie de jeton de Hello.</span><span class="sxs-lookup"><span data-stu-id="af163-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="af163-132">Toutefois, certains serveurs d’autorisation créent sont appelées [référence jetons](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) qui ne peut pas être vérifié sans passer d’un serveur d’autorisation de toohello précédent appel.</span><span class="sxs-lookup"><span data-stu-id="af163-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="af163-133">Introspection normalisée</span><span class="sxs-lookup"><span data-stu-id="af163-133">Standardized introspection</span></span>
<span data-ttu-id="af163-134">Hello passée il n’y a eu aucun moyen normalisé de vérification d’un jeton de référence avec un serveur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="af163-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="af163-135">Cependant une norme récemment [RFC 7662](https://tools.ietf.org/html/rfc7662) a été publiée par hello IETF qui définit comment un serveur de ressources peut vérifier la validité hello d’un jeton.</span><span class="sxs-lookup"><span data-stu-id="af163-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="af163-136">Extraction du jeton de hello</span><span class="sxs-lookup"><span data-stu-id="af163-136">Extracting hello token</span></span>
<span data-ttu-id="af163-137">première étape de Hello est jeton de hello tooextract à partir de l’en-tête d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="af163-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="af163-138">valeur d’en-tête Hello doit être formaté avec hello `Bearer` schéma d’autorisation, un espace unique et l’autorisation de hello puis jeton en tant que par [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="af163-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="af163-139">Malheureusement, il existe des cas où le schéma d’autorisation de hello est omis.</span><span class="sxs-lookup"><span data-stu-id="af163-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="af163-140">tooaccount pour cela lors de l’analyse, nous diviser la valeur d’en-tête de hello sur un espace et la chaîne hello sélectionnez dernière hello retourné du tableau de chaînes.</span><span class="sxs-lookup"><span data-stu-id="af163-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="af163-141">Une solution de contournement est ainsi trouvée pour les en-têtes d’autorisation mal formés.</span><span class="sxs-lookup"><span data-stu-id="af163-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="af163-142">Demande de validation hello</span><span class="sxs-lookup"><span data-stu-id="af163-142">Making hello validation request</span></span>
<span data-ttu-id="af163-143">Une fois le jeton d’autorisation hello, nous permettent de jeton de hello demande toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="af163-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="af163-144">RFC 7662 appelle introspection de ce processus et exige que vous `POST` une ressource d’introspection de toohello de formulaire HTML.</span><span class="sxs-lookup"><span data-stu-id="af163-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="af163-145">Hello formulaire HTML doit contenir au moins une paire clé/valeur avec la clé de hello `token`.</span><span class="sxs-lookup"><span data-stu-id="af163-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="af163-146">Cette demande adressée au serveur d’autorisation toohello doit également être authentifié tooensure que des clients malveillants ne peuvent pas atteindre chalutage pour les jetons valides.</span><span class="sxs-lookup"><span data-stu-id="af163-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-hello-response"></a><span data-ttu-id="af163-147">La vérification de la réponse de hello</span><span class="sxs-lookup"><span data-stu-id="af163-147">Checking hello response</span></span>
<span data-ttu-id="af163-148">Hello `response-variable-name` attribut est hello d’accès utilisé toogive a retourné une réponse.</span><span class="sxs-lookup"><span data-stu-id="af163-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="af163-149">Hello nom défini dans cette propriété peut être utilisé comme une clé dans hello `context.Variables` hello tooaccess de dictionnaire `IResponse` objet.</span><span class="sxs-lookup"><span data-stu-id="af163-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="af163-150">À partir de l’objet de réponse hello, nous pouvons récupérer les corps hello et RFC 7622 nous indique que la réponse de hello doit être un objet JSON et doit contenir au moins une propriété appelée `active` qui est une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="af163-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="af163-151">Lorsque `active` est true, le jeton de hello est considéré comme valid.</span><span class="sxs-lookup"><span data-stu-id="af163-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="af163-152">Signalement d’un échec</span><span class="sxs-lookup"><span data-stu-id="af163-152">Reporting failure</span></span>
<span data-ttu-id="af163-153">Nous utilisons un `<choose>` stratégie toodetect si le jeton de hello n’est pas valide et le cas échéant, renvoyer une réponse 401.</span><span class="sxs-lookup"><span data-stu-id="af163-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="af163-154">Comme pour [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) qui décrit comment `bearer` jetons doivent être utilisés, nous avons également retourner un `WWW-Authenticate` l’en-tête de réponse de hello 401.</span><span class="sxs-lookup"><span data-stu-id="af163-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="af163-155">Hello WWW-Authenticate est prévue tooinstruct un client sur la façon de tooconstruct une demande correctement autorisée.</span><span class="sxs-lookup"><span data-stu-id="af163-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="af163-156">En raison de toohello diverses approches possibles avec les framework hello OAuth2, il est difficile toocommunicate tous hello informations sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="af163-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="af163-157">Heureusement des efforts en cours d’exécution toohelp [clients découvrir comment tooproperly autoriser le serveur de ressources de demandes tooa](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="af163-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="af163-158">Solution finale</span><span class="sxs-lookup"><span data-stu-id="af163-158">Final solution</span></span>
<span data-ttu-id="af163-159">Assembler tous les éléments de hello, nous obtenons hello suivant de stratégie :</span><span class="sxs-lookup"><span data-stu-id="af163-159">Putting all hello pieces together, we get hello following policy:</span></span>

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

<span data-ttu-id="af163-160">Il existe un seul de nombreux exemples de hello `send-request` stratégie peut être des services externes utile toointegrate utilisés dans les processus hello des demandes et réponses transitant par le service de gestion des API de hello.</span><span class="sxs-lookup"><span data-stu-id="af163-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="af163-161">Rédaction de réponse</span><span class="sxs-lookup"><span data-stu-id="af163-161">Response Composition</span></span>
<span data-ttu-id="af163-162">Hello `send-request` stratégie peut être utilisée pour améliorer un système principal demande tooa principal, comme nous l’avons vu dans l’exemple précédent de hello, ou il peut être utilisé comme un remplacement complet pour d’appel de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="af163-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="af163-163">À l’aide de cette technique, nous pouvons facilement créer des ressources composites qui sont agrégées à partir de plusieurs systèmes différents.</span><span class="sxs-lookup"><span data-stu-id="af163-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="af163-164">Génération d’un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="af163-164">Building a dashboard</span></span>
<span data-ttu-id="af163-165">Parfois, vous souhaitez toobe tooexpose en mesure d’informations qui existe dans plusieurs systèmes principaux, par exemple, toodrive un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="af163-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="af163-166">Hello, indicateurs de performance clés proviennent de tous les principaux différents, mais vous préférez pas les toothem tooprovide un accès direct, et il peut être intéressant si toutes les informations de hello pu être récupérées dans une demande unique.</span><span class="sxs-lookup"><span data-stu-id="af163-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="af163-167">Peut-être que certaines informations de serveur principal hello doit certains découpage et découper et expurgation un peu de tout d’abord !</span><span class="sxs-lookup"><span data-stu-id="af163-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="af163-168">Qui est en mesure de toocache que la ressource composite serait un tooreduce utile hello principal charger puisque vous savez que les utilisateurs ont l’habitude de marteler la touche F5 de hello dans l’ordre toosee si leurs mesures peu performantes peuvent changer.</span><span class="sxs-lookup"><span data-stu-id="af163-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="af163-169">Ressource de hello émulant</span><span class="sxs-lookup"><span data-stu-id="af163-169">Faking hello resource</span></span>
<span data-ttu-id="af163-170">Hello première étape toobuilding nos ressources de tableau de bord est tooconfigure une nouvelle opération dans le portail de publication de gestion des API hello.</span><span class="sxs-lookup"><span data-stu-id="af163-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="af163-171">Cela sera un tooconfigure d’opération utilisée espace réservé de notre toobuild de stratégie de composition notre ressource dynamique.</span><span class="sxs-lookup"><span data-stu-id="af163-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![Opération de tableau de bord](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="af163-173">Effectuant des demandes de hello</span><span class="sxs-lookup"><span data-stu-id="af163-173">Making hello requests</span></span>
<span data-ttu-id="af163-174">Une fois hello `dashboard` opération a été créée. nous pouvons configurer une stratégie spécifiquement pour cette opération.</span><span class="sxs-lookup"><span data-stu-id="af163-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Opération de tableau de bord](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="af163-176">première étape de Hello est tooextract tous les paramètres de requête à partir de la demande entrante de hello, afin que nous pouvons transmettre tooour principal.</span><span class="sxs-lookup"><span data-stu-id="af163-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="af163-177">Dans cet exemple, notre tableau de bord affiche des informations selon une période ; il comporte donc un paramètre `fromDate` et `toDate`.</span><span class="sxs-lookup"><span data-stu-id="af163-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="af163-178">Nous pouvons utiliser hello `set-variable` stratégie tooextract hello plus d’informations à partir de l’URL de demande hello.</span><span class="sxs-lookup"><span data-stu-id="af163-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="af163-179">Une fois ces informations nous pouvons effectuer des demandes systèmes principaux de hello tooall.</span><span class="sxs-lookup"><span data-stu-id="af163-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="af163-180">Chaque requête construit une nouvelle URL avec informations de paramètre hello et appelle son propre serveur et stocke la réponse de hello dans une variable de contexte.</span><span class="sxs-lookup"><span data-stu-id="af163-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

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

<span data-ttu-id="af163-181">Ces requêtes s’exécutent en séquence, ce qui n’est pas idéal.</span><span class="sxs-lookup"><span data-stu-id="af163-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="af163-182">Dans une prochaine version nous présenterons une nouvelle stratégie nommée `wait` qui activera tous ces tooexecute de requêtes en parallèle.</span><span class="sxs-lookup"><span data-stu-id="af163-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="af163-183">Réponse</span><span class="sxs-lookup"><span data-stu-id="af163-183">Responding</span></span>
<span data-ttu-id="af163-184">Nous pouvons utiliser hello du réponse composite hello tooconstruct [retour-réponse](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) stratégie.</span><span class="sxs-lookup"><span data-stu-id="af163-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="af163-185">Hello `set-body` élément peut utiliser une expression tooconstruct un nouveau `JObject` avec toutes les représentations de composant hello incorporées en tant que propriétés.</span><span class="sxs-lookup"><span data-stu-id="af163-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

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

<span data-ttu-id="af163-186">stratégie complète de Hello se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="af163-186">hello complete policy looks as follows:</span></span>

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

<span data-ttu-id="af163-187">Dans la configuration de hello d’opération d’espace réservé de hello, nous pouvons configurer hello du tableau de bord ressources toobe mis en cache pour au moins une heure, car nous sommes conscients de nature hello de données de hello signifie que, même s’il s’agit d’une heure plus à jour, qu'il sera toujours suffisamment efficace utilisateurs de toohello tooconvey des informations précieuses.</span><span class="sxs-lookup"><span data-stu-id="af163-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="af163-188">Résumé</span><span class="sxs-lookup"><span data-stu-id="af163-188">Summary</span></span>
<span data-ttu-id="af163-189">Service de gestion des API Azure fournit des stratégies souples qui peuvent être de manière sélective appliquées tooHTTP trafic et composition de services principaux.</span><span class="sxs-lookup"><span data-stu-id="af163-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="af163-190">Si vous souhaitez tooenhance votre passerelle API avec la génération d’alertes de fonctions, la vérification des fonctionnalités de validation ou de créez des ressources composites en fonction de plusieurs services principaux, hello `send-request` et les stratégies associées ouvrir un monde de possibilités.</span><span class="sxs-lookup"><span data-stu-id="af163-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="af163-191">Regarder une vidéo de présentation de ces stratégies.</span><span class="sxs-lookup"><span data-stu-id="af163-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="af163-192">Pour plus d’informations sur hello [envoyer un moyen de demande](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [demande d’envoi](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), et [retour-réponse](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) stratégies abordées dans cet article, veuillez consulter hello suivant vidéo.</span><span class="sxs-lookup"><span data-stu-id="af163-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

