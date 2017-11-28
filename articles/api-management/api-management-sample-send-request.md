---
title: "Utilisation du service de gestion des API pour générer des requêtes HTTP"
description: "Apprenez à utiliser des stratégies de requête et de réponse dans le service de gestion des API pour appeler des services externes depuis votre API"
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="49d95-103">Utilisation de services externes à partir du service de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="49d95-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="49d95-104">Les stratégies disponibles dans le service de gestion des API Azure permettent de réaliser un large éventail de tâches utiles purement selon la requête entrante, la réponse sortante et les informations de configuration de base.</span><span class="sxs-lookup"><span data-stu-id="49d95-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="49d95-105">En revanche, la possibilité d’interagir avec des services externes à partir des stratégies de gestion des API ouvre bien davantage d’opportunités.</span><span class="sxs-lookup"><span data-stu-id="49d95-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="49d95-106">Nous avons vu précédemment comment interagir avec le service [Azure Event Hub pour la journalisation, la surveillance et l’analyse](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="49d95-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="49d95-107">Dans cet article, nous allons décrire les stratégies qui vous permettent d’interagir avec n’importe quel service HTTP externe.</span><span class="sxs-lookup"><span data-stu-id="49d95-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="49d95-108">Ces stratégies peuvent être utilisées pour déclencher des événements à distance ou récupérer des informations servant à manipuler la requête d’origine et la réponse d’une certaine façon.</span><span class="sxs-lookup"><span data-stu-id="49d95-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="49d95-109">Send-One-Way-Request (Envoyer une requête à sens unique)</span><span class="sxs-lookup"><span data-stu-id="49d95-109">Send-One-Way-Request</span></span>
<span data-ttu-id="49d95-110">L’interaction externe la plus simple est peut-être le style « fire and forget » d’une demande qui permet à un service externe d’être notifié d’un type d’événement important.</span><span class="sxs-lookup"><span data-stu-id="49d95-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="49d95-111">Nous pouvons utiliser la stratégie de flux de contrôle `choose` pour détecter tout type de condition qui nous intéresse et puis, si la condition est remplie, nous pouvons effectuer une requête HTTP externe à l’aide de la stratégie [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) .</span><span class="sxs-lookup"><span data-stu-id="49d95-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="49d95-112">Il peut s’agir d’une requête destinée à un système de messagerie comme Hipchat ou Slack, ou encore à une API de messagerie telle que SendGrid ou MailChimp, ou à quelque chose comme PagerDuty pour les incidents de support critiques.</span><span class="sxs-lookup"><span data-stu-id="49d95-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="49d95-113">Tous ces systèmes de messagerie ont des API HTTP simples que nous pouvons facilement appeler.</span><span class="sxs-lookup"><span data-stu-id="49d95-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="49d95-114">Alerte avec Slack</span><span class="sxs-lookup"><span data-stu-id="49d95-114">Alerting with Slack</span></span>
<span data-ttu-id="49d95-115">L’exemple suivant montre comment envoyer un message à une salle de conversation Slack si le code d’état de la réponse HTTP est supérieur ou égal à 500.</span><span class="sxs-lookup"><span data-stu-id="49d95-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="49d95-116">Une erreur incluse dans la plage 500 indique un problème avec notre API principale que le client de notre API ne peut pas résoudre lui-même.</span><span class="sxs-lookup"><span data-stu-id="49d95-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="49d95-117">Elle nécessite généralement une intervention de notre part.</span><span class="sxs-lookup"><span data-stu-id="49d95-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="49d95-118">Slack inclut la notion de Webhook entrant.</span><span class="sxs-lookup"><span data-stu-id="49d95-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="49d95-119">Quand vous configurez un Webhook entrant, Slack génère une URL spéciale qui vous permet de faire une requête POST simple et de transmettre un message dans le canal Slack.</span><span class="sxs-lookup"><span data-stu-id="49d95-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="49d95-120">Le corps JSON que nous créons se base sur un format défini par Slack.</span><span class="sxs-lookup"><span data-stu-id="49d95-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Webhook Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="49d95-122">Le style « fire and forget » est-il suffisant ?</span><span class="sxs-lookup"><span data-stu-id="49d95-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="49d95-123">L’utilisation d’un style « fire and forget » de requête implique certains compromis.</span><span class="sxs-lookup"><span data-stu-id="49d95-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="49d95-124">Si, pour une raison ou une autre, la requête échoue, alors l’échec n’est pas signalé.</span><span class="sxs-lookup"><span data-stu-id="49d95-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="49d95-125">Dans ce cas particulier, la complexité d’avoir un système de signalement des échecs secondaire et le coût des performances supplémentaires liées à l’attente de la réponse ne sont pas justifiés.</span><span class="sxs-lookup"><span data-stu-id="49d95-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="49d95-126">Pour les scénarios où il est indispensable de vérifier la réponse, la stratégie [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) constitue une meilleure option.</span><span class="sxs-lookup"><span data-stu-id="49d95-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="49d95-127">send-request</span><span class="sxs-lookup"><span data-stu-id="49d95-127">Send-Request</span></span>
<span data-ttu-id="49d95-128">La stratégie `send-request` permet d’utiliser un service externe pour exécuter des fonctions de traitement complexes et retourner des données au service Gestion des API qui peuvent être utilisées pour d’autres traitements de stratégie.</span><span class="sxs-lookup"><span data-stu-id="49d95-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="49d95-129">Autorisation des jetons de référence</span><span class="sxs-lookup"><span data-stu-id="49d95-129">Authorizing reference tokens</span></span>
<span data-ttu-id="49d95-130">Une fonction majeure de la gestion des API consiste à protéger les ressources principales.</span><span class="sxs-lookup"><span data-stu-id="49d95-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="49d95-131">Si le serveur d’autorisation utilisé par votre API crée des [jetons JWT](http://jwt.io/) dans le cadre de son flux OAuth2, comme le fait [Azure Active Directory](../active-directory/active-directory-aadconnect.md), vous pouvez utiliser la stratégie `validate-jwt` pour vérifier la validité du jeton.</span><span class="sxs-lookup"><span data-stu-id="49d95-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="49d95-132">Toutefois, certains serveurs d’autorisation créent des [jetons de référence](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) qui ne peuvent pas être vérifiés sans rappeler le serveur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="49d95-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="49d95-133">Introspection normalisée</span><span class="sxs-lookup"><span data-stu-id="49d95-133">Standardized introspection</span></span>
<span data-ttu-id="49d95-134">Par le passé, il n’existait aucun moyen normalisé de vérifier un jeton de référence avec un serveur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="49d95-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="49d95-135">Néanmoins, une norme récemment proposée, [RFC 7662](https://tools.ietf.org/html/rfc7662) , qui définit comment un serveur de ressources peut vérifier la validité d’un jeton, a été publiée par l’IETF.</span><span class="sxs-lookup"><span data-stu-id="49d95-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="49d95-136">Extraction du jeton</span><span class="sxs-lookup"><span data-stu-id="49d95-136">Extracting the token</span></span>
<span data-ttu-id="49d95-137">La première étape consiste à extraire le jeton de l’en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="49d95-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="49d95-138">La valeur d’en-tête doit être mise en forme à l’aide du modèle d’autorisation `Bearer` , d’un seul espace, puis du jeton d’autorisation conformément à la norme [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="49d95-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="49d95-139">Malheureusement, il existe des cas où le modèle d’autorisation est omis.</span><span class="sxs-lookup"><span data-stu-id="49d95-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="49d95-140">Pour en tenir compte lors de l’analyse, nous fractionnons la valeur d’en-tête sur un espace et sélectionnons la dernière chaîne dans le tableau de chaînes retourné.</span><span class="sxs-lookup"><span data-stu-id="49d95-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="49d95-141">Une solution de contournement est ainsi trouvée pour les en-têtes d’autorisation mal formés.</span><span class="sxs-lookup"><span data-stu-id="49d95-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="49d95-142">Requête de validation</span><span class="sxs-lookup"><span data-stu-id="49d95-142">Making the validation request</span></span>
<span data-ttu-id="49d95-143">Une fois que nous avons le jeton d’autorisation, nous pouvons faire la requête pour valider le jeton.</span><span class="sxs-lookup"><span data-stu-id="49d95-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="49d95-144">La norme RFC 7662 appelle ce processus « introspection » et vous oblige à appliquer une commande `POST` de formulaire HTML à la ressource d’introspection.</span><span class="sxs-lookup"><span data-stu-id="49d95-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="49d95-145">Le formulaire HTML doit contenir au moins une paire clé/valeur avec la clé `token`.</span><span class="sxs-lookup"><span data-stu-id="49d95-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="49d95-146">Cette requête adressée au serveur d’autorisation doit également être authentifiée pour veiller à ce qu’aucun client malveillant ne puisse obtenir des jetons valides.</span><span class="sxs-lookup"><span data-stu-id="49d95-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="49d95-147">Vérification de la réponse</span><span class="sxs-lookup"><span data-stu-id="49d95-147">Checking the response</span></span>
<span data-ttu-id="49d95-148">L’attribut `response-variable-name` est utilisé pour accéder à la réponse retournée.</span><span class="sxs-lookup"><span data-stu-id="49d95-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="49d95-149">Le nom défini dans cette propriété peut être utilisé comme clé dans le dictionnaire `context.Variables` pour accéder à l’objet `IResponse`.</span><span class="sxs-lookup"><span data-stu-id="49d95-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="49d95-150">À partir de l’objet réponse, nous pouvons récupérer le corps et la norme RFC 7622 nous indique que la réponse doit être un objet JSON et contenir au moins une propriété appelée `active` qui est une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="49d95-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="49d95-151">Quand `active` a la valeur true, alors le jeton est considéré comme valide.</span><span class="sxs-lookup"><span data-stu-id="49d95-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="49d95-152">Signalement d’un échec</span><span class="sxs-lookup"><span data-stu-id="49d95-152">Reporting failure</span></span>
<span data-ttu-id="49d95-153">Nous utilisons une stratégie `<choose>` pour détecter si le jeton n’est pas valide et le cas échéant, retourner une réponse 401.</span><span class="sxs-lookup"><span data-stu-id="49d95-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="49d95-154">Conformément à la norme [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) qui décrit comment les jetons `bearer` doivent être utilisés, nous retournons également un en-tête `WWW-Authenticate` avec la réponse 401.</span><span class="sxs-lookup"><span data-stu-id="49d95-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="49d95-155">L’élément WWW-Authenticate a pour but d’informer un client sur la manière de créer une requête dûment autorisée.</span><span class="sxs-lookup"><span data-stu-id="49d95-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="49d95-156">En raison de la grande variété d’approches possibles avec l’infrastructure OAuth2, il est difficile de communiquer toutes les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="49d95-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="49d95-157">Heureusement, tous les efforts sont déployés pour aider les [clients à découvrir comment autoriser correctement les requêtes adressées à un serveur de ressources](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="49d95-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="49d95-158">Solution finale</span><span class="sxs-lookup"><span data-stu-id="49d95-158">Final solution</span></span>
<span data-ttu-id="49d95-159">En rassemblant tous les éléments, nous obtenons la stratégie suivante :</span><span class="sxs-lookup"><span data-stu-id="49d95-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="49d95-160">Il ne s’agit que d’un des nombreux exemples d’utilisation de la stratégie `send-request` pour intégrer des services externes utiles dans le processus des requêtes et réponses transitant par le service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="49d95-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="49d95-161">Rédaction de réponse</span><span class="sxs-lookup"><span data-stu-id="49d95-161">Response Composition</span></span>
<span data-ttu-id="49d95-162">La stratégie `send-request` peut être utilisée pour améliorer une requête principale adressée à un système principal, comme nous l’avons vu dans l’exemple précédent, ou elle peut remplacer totalement l’appel du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="49d95-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="49d95-163">À l’aide de cette technique, nous pouvons facilement créer des ressources composites qui sont agrégées à partir de plusieurs systèmes différents.</span><span class="sxs-lookup"><span data-stu-id="49d95-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="49d95-164">Génération d’un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="49d95-164">Building a dashboard</span></span>
<span data-ttu-id="49d95-165">Vous avez parfois besoin d’exposer des informations qui existent dans plusieurs systèmes principaux, par exemple, pour piloter un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="49d95-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="49d95-166">Les indicateurs de performance clés proviennent de tous les services principaux différents, mais vous préférez ne pas y fournir d’accès direct et il serait intéressant que toutes les informations puissent être récupérées dans une seule requête.</span><span class="sxs-lookup"><span data-stu-id="49d95-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="49d95-167">Certaines informations principales ont peut-être besoin d’être coupées en rondelles ou en tranches, voire d’être assainies dans un premier temps.</span><span class="sxs-lookup"><span data-stu-id="49d95-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="49d95-168">La possibilité de mettre en cache cette ressource composite s’avère utile pour réduire la charge principale puisque vous savez que les utilisateurs ont l’habitude de marteler la touche F5 pour voir si leurs mesures peu performantes peuvent changer.</span><span class="sxs-lookup"><span data-stu-id="49d95-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="49d95-169">Simulation de la ressource</span><span class="sxs-lookup"><span data-stu-id="49d95-169">Faking the resource</span></span>
<span data-ttu-id="49d95-170">La première étape pour générer notre ressource de tableau de bord consiste à configurer une nouvelle opération dans le portail des éditeurs de la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="49d95-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="49d95-171">Il s’agit d’une opération d’espace réservé utilisée pour configurer notre stratégie de rédaction afin de générer notre ressource dynamique.</span><span class="sxs-lookup"><span data-stu-id="49d95-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Opération de tableau de bord](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="49d95-173">Construction des requêtes</span><span class="sxs-lookup"><span data-stu-id="49d95-173">Making the requests</span></span>
<span data-ttu-id="49d95-174">Une fois l’opération `dashboard` créée, nous pouvons configurer une stratégie spécifiquement pour cette opération.</span><span class="sxs-lookup"><span data-stu-id="49d95-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Opération de tableau de bord](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="49d95-176">La première étape consiste à extraire les paramètres de requête à partir de la requête entrante, de sorte à pouvoir les transférer vers notre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="49d95-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="49d95-177">Dans cet exemple, notre tableau de bord affiche des informations selon une période ; il comporte donc un paramètre `fromDate` et `toDate`.</span><span class="sxs-lookup"><span data-stu-id="49d95-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="49d95-178">Nous pouvons utiliser la stratégie `set-variable` pour extraire les informations de l’URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="49d95-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="49d95-179">Une fois que nous avons ces informations, nous pouvons faire des requêtes auprès de tous les systèmes principaux.</span><span class="sxs-lookup"><span data-stu-id="49d95-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="49d95-180">Chaque requête construit une nouvelle URL avec les informations de paramètre, puis appelle son serveur respectif et enregistre la réponse dans une variable de contexte.</span><span class="sxs-lookup"><span data-stu-id="49d95-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="49d95-181">Ces requêtes s’exécutent en séquence, ce qui n’est pas idéal.</span><span class="sxs-lookup"><span data-stu-id="49d95-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="49d95-182">Dans une prochaine version, nous introduirons une nouvelle stratégie nommée `wait` qui permettra à toutes ces requêtes de s’exécuter en parallèle.</span><span class="sxs-lookup"><span data-stu-id="49d95-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="49d95-183">Réponse</span><span class="sxs-lookup"><span data-stu-id="49d95-183">Responding</span></span>
<span data-ttu-id="49d95-184">Pour construire la réponse composite, nous pouvons utiliser la stratégie [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) .</span><span class="sxs-lookup"><span data-stu-id="49d95-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="49d95-185">L’élément `set-body` peut utiliser une expression pour construire un nouveau `JObject` avec toutes les représentations de composant incorporées en tant que propriétés.</span><span class="sxs-lookup"><span data-stu-id="49d95-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="49d95-186">La stratégie complète se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="49d95-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="49d95-187">Pendant la configuration de l’opération d’espace réservé, nous pouvons configurer la ressource de tableau de bord de sorte à la mettre en cache pendant au moins une heure, car nous sommes conscients que la nature des données signifie que même si elle est en retard d’une heure, elle sera quand même suffisamment efficace pour transmettre des informations utiles aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="49d95-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="49d95-188">Résumé</span><span class="sxs-lookup"><span data-stu-id="49d95-188">Summary</span></span>
<span data-ttu-id="49d95-189">Le service de gestion des API Azure offre des stratégies flexibles que vous pouvez appliquer de façon sélective au trafic HTTP et permet de composer des services principaux.</span><span class="sxs-lookup"><span data-stu-id="49d95-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="49d95-190">Que vous vouliez améliorer votre passerelle API avec des fonctions d’alerte, des fonctionnalités de vérification et de validation ou créer des ressources composites reposant sur plusieurs services principaux, la stratégie `send-request` et les stratégies associées vous ouvrent un monde de possibilités.</span><span class="sxs-lookup"><span data-stu-id="49d95-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="49d95-191">Regarder une vidéo de présentation de ces stratégies.</span><span class="sxs-lookup"><span data-stu-id="49d95-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="49d95-192">Pour plus d’informations sur les stratégies [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) et [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) abordées dans cet article, regardez la vidéo suivante.</span><span class="sxs-lookup"><span data-stu-id="49d95-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

