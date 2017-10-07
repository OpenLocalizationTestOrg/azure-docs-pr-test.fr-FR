---
title: "aaaException de gestion - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "mesures d’atténuation des menaces exposé Bonjour outil de modélisation des menaces"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="72e8b-103">Infrastructure de sécurité : Gestion des exceptions | Corrections</span><span class="sxs-lookup"><span data-stu-id="72e8b-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="72e8b-104">Produit/service</span><span class="sxs-lookup"><span data-stu-id="72e8b-104">Product/Service</span></span> | <span data-ttu-id="72e8b-105">Article</span><span class="sxs-lookup"><span data-stu-id="72e8b-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="72e8b-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="72e8b-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="72e8b-107">WCF - Ne pas inclure le nœud serviceDebug dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="72e8b-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="72e8b-108">WCF - Ne pas inclure le nœud serviceMetadata dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="72e8b-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="72e8b-109">**API Web**</span><span class="sxs-lookup"><span data-stu-id="72e8b-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="72e8b-110">Vérifier que la gestion des exceptions correcte est effectuée dans l’API web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="72e8b-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="72e8b-111">**Application web**</span><span class="sxs-lookup"><span data-stu-id="72e8b-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="72e8b-112">Ne pas exposer les détails de sécurité dans les messages d’erreur </span><span class="sxs-lookup"><span data-stu-id="72e8b-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="72e8b-113">Implémenter la page de gestion des erreurs par défaut </span><span class="sxs-lookup"><span data-stu-id="72e8b-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="72e8b-114">Définir la méthode de déploiement tooRetail dans IIS</span><span class="sxs-lookup"><span data-stu-id="72e8b-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="72e8b-115">Les exceptions doivent échouer en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="72e8b-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="72e8b-116"><a id="servicedebug"></a>WCF - Ne pas inclure le nœud serviceDebug dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="72e8b-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="72e8b-117">Intitulé</span><span class="sxs-lookup"><span data-stu-id="72e8b-117">Title</span></span>                   | <span data-ttu-id="72e8b-118">Détails</span><span class="sxs-lookup"><span data-stu-id="72e8b-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="72e8b-119">**Composant**</span><span class="sxs-lookup"><span data-stu-id="72e8b-119">**Component**</span></span>               | <span data-ttu-id="72e8b-120">WCF</span><span class="sxs-lookup"><span data-stu-id="72e8b-120">WCF</span></span> | 
| <span data-ttu-id="72e8b-121">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="72e8b-121">**SDL Phase**</span></span>               | <span data-ttu-id="72e8b-122">Créer</span><span class="sxs-lookup"><span data-stu-id="72e8b-122">Build</span></span> |  
| <span data-ttu-id="72e8b-123">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="72e8b-123">**Applicable Technologies**</span></span> | <span data-ttu-id="72e8b-124">Générique, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="72e8b-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="72e8b-125">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="72e8b-125">**Attributes**</span></span>              | <span data-ttu-id="72e8b-126">N/A</span><span class="sxs-lookup"><span data-stu-id="72e8b-126">N/A</span></span>  |
| <span data-ttu-id="72e8b-127">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="72e8b-127">**References**</span></span>              | <span data-ttu-id="72e8b-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="72e8b-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="72e8b-129">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="72e8b-129">**Steps**</span></span> | <span data-ttu-id="72e8b-130">Services Windows Communication Framework (WCF) peuvent être configuré tooexpose les informations de débogage.</span><span class="sxs-lookup"><span data-stu-id="72e8b-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="72e8b-131">Les informations de débogage ne doivent pas être utilisées dans les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="72e8b-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="72e8b-132">Hello `<serviceDebug>` balise définit si la fonctionnalité d’informations de débogage de hello est activée pour un service WCF.</span><span class="sxs-lookup"><span data-stu-id="72e8b-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="72e8b-133">Si a la valeur tootrue hello attribut includeExceptionDetailInFaults, informations sur les exceptions à partir de l’application hello seront affichera tooclients.</span><span class="sxs-lookup"><span data-stu-id="72e8b-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="72e8b-134">Les pirates peuvent tirer parti de hello supplémentaires qu’ils des gains d’informations de débogage de sortie toomount les attaques ciblées sur l’infrastructure de hello, base de données ou d’autres ressources utilisées par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="72e8b-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="72e8b-135">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-135">Example</span></span>
<span data-ttu-id="72e8b-136">fichier de configuration suivant Hello inclut hello `<serviceDebug>` balise :</span><span class="sxs-lookup"><span data-stu-id="72e8b-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="72e8b-137">Désactiver les informations de débogage dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="72e8b-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="72e8b-138">Cela peut être accompli en supprimant hello `<serviceDebug>` étiquette à partir du fichier de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="72e8b-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="72e8b-139"><a id="servicemetadata"></a>WCF - Ne pas inclure le nœud serviceMetadata dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="72e8b-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="72e8b-140">Intitulé</span><span class="sxs-lookup"><span data-stu-id="72e8b-140">Title</span></span>                   | <span data-ttu-id="72e8b-141">Détails</span><span class="sxs-lookup"><span data-stu-id="72e8b-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="72e8b-142">**Composant**</span><span class="sxs-lookup"><span data-stu-id="72e8b-142">**Component**</span></span>               | <span data-ttu-id="72e8b-143">WCF</span><span class="sxs-lookup"><span data-stu-id="72e8b-143">WCF</span></span> | 
| <span data-ttu-id="72e8b-144">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="72e8b-144">**SDL Phase**</span></span>               | <span data-ttu-id="72e8b-145">Créer</span><span class="sxs-lookup"><span data-stu-id="72e8b-145">Build</span></span> |  
| <span data-ttu-id="72e8b-146">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="72e8b-146">**Applicable Technologies**</span></span> | <span data-ttu-id="72e8b-147">Générique</span><span class="sxs-lookup"><span data-stu-id="72e8b-147">Generic</span></span> |
| <span data-ttu-id="72e8b-148">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="72e8b-148">**Attributes**</span></span>              | <span data-ttu-id="72e8b-149">Générique, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="72e8b-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="72e8b-150">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="72e8b-150">**References**</span></span>              | <span data-ttu-id="72e8b-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="72e8b-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="72e8b-152">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="72e8b-152">**Steps**</span></span> | <span data-ttu-id="72e8b-153">Exposer publiquement des informations sur un service peut fournir aux attaquants précieuses dans comment ils peuvent exploiter les service hello.</span><span class="sxs-lookup"><span data-stu-id="72e8b-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="72e8b-154">Hello `<serviceMetadata>` balise active la fonctionnalité de publication de métadonnées hello.</span><span class="sxs-lookup"><span data-stu-id="72e8b-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="72e8b-155">Les métadonnées de service peuvent contenir des informations sensibles qui ne doivent pas être accessibles publiquement.</span><span class="sxs-lookup"><span data-stu-id="72e8b-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="72e8b-156">Au minimum, autoriser uniquement les utilisateurs approuvés tooaccess hello des métadonnées et vous assurer que les informations inutiles ne sont pas exposées.</span><span class="sxs-lookup"><span data-stu-id="72e8b-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="72e8b-157">Mieux encore, de désactiver entièrement hello capacité toopublish métadonnées.</span><span class="sxs-lookup"><span data-stu-id="72e8b-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="72e8b-158">Une configuration sécurisée de WCF ne contiendra pas hello `<serviceMetadata>` balise.</span><span class="sxs-lookup"><span data-stu-id="72e8b-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="72e8b-159"><a id="exception"></a>Vérifier que la gestion des exceptions correcte est effectuée dans l’API web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="72e8b-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="72e8b-160">Intitulé</span><span class="sxs-lookup"><span data-stu-id="72e8b-160">Title</span></span>                   | <span data-ttu-id="72e8b-161">Détails</span><span class="sxs-lookup"><span data-stu-id="72e8b-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="72e8b-162">**Composant**</span><span class="sxs-lookup"><span data-stu-id="72e8b-162">**Component**</span></span>               | <span data-ttu-id="72e8b-163">API Web</span><span class="sxs-lookup"><span data-stu-id="72e8b-163">Web API</span></span> | 
| <span data-ttu-id="72e8b-164">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="72e8b-164">**SDL Phase**</span></span>               | <span data-ttu-id="72e8b-165">Créer</span><span class="sxs-lookup"><span data-stu-id="72e8b-165">Build</span></span> |  
| <span data-ttu-id="72e8b-166">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="72e8b-166">**Applicable Technologies**</span></span> | <span data-ttu-id="72e8b-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="72e8b-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="72e8b-168">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="72e8b-168">**Attributes**</span></span>              | <span data-ttu-id="72e8b-169">N/A</span><span class="sxs-lookup"><span data-stu-id="72e8b-169">N/A</span></span>  |
| <span data-ttu-id="72e8b-170">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="72e8b-170">**References**</span></span>              | <span data-ttu-id="72e8b-171">[Gestion des exceptions dans l’API web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Validation de modèle dans l’API web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="72e8b-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="72e8b-172">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="72e8b-172">**Steps**</span></span> | <span data-ttu-id="72e8b-173">Par défaut, la plupart des exceptions non interceptées dans l’API web ASP.NET sont converties en réponse HTTP avec le code d’état`500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="72e8b-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="72e8b-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-174">Example</span></span>
<span data-ttu-id="72e8b-175">code d’état toocontrol hello retourné par hello API, `HttpResponseException` peut être utilisé comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="72e8b-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="72e8b-176">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-176">Example</span></span>
<span data-ttu-id="72e8b-177">Pour contrôler davantage sur la réponse d’exception hello, hello `HttpResponseMessage` classe peut être utilisée comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="72e8b-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="72e8b-178">toocatch exceptions non gérées qui ne sont pas du type de hello `HttpResponseException`, les filtres d’Exception peut être utilisés.</span><span class="sxs-lookup"><span data-stu-id="72e8b-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="72e8b-179">Filtres d’exception implémentent hello `System.Web.Http.Filters.IExceptionFilter` interface.</span><span class="sxs-lookup"><span data-stu-id="72e8b-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="72e8b-180">toowrite de façon la plus simple Hello un filtre d’exception est tooderive de hello `System.Web.Http.Filters.ExceptionFilterAttribute` classe et substituer la méthode OnException de hello.</span><span class="sxs-lookup"><span data-stu-id="72e8b-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="72e8b-181">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-181">Example</span></span>
<span data-ttu-id="72e8b-182">Voici un filtre qui convertit des `NotImplementedException` exceptions en code d’état HTTP `501, Not Implemented` :</span><span class="sxs-lookup"><span data-stu-id="72e8b-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="72e8b-183">Il existe plusieurs façons tooregister un filtre d’exception API Web :</span><span class="sxs-lookup"><span data-stu-id="72e8b-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="72e8b-184">Par action</span><span class="sxs-lookup"><span data-stu-id="72e8b-184">By action</span></span>
- <span data-ttu-id="72e8b-185">Par contrôleur</span><span class="sxs-lookup"><span data-stu-id="72e8b-185">By controller</span></span>
- <span data-ttu-id="72e8b-186">Globalement</span><span class="sxs-lookup"><span data-stu-id="72e8b-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="72e8b-187">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-187">Example</span></span>
<span data-ttu-id="72e8b-188">tooapply hello filtre d’action spécifique de tooa, ajouter un filtre de hello en tant qu’attribut toohello action :</span><span class="sxs-lookup"><span data-stu-id="72e8b-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="72e8b-189">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-189">Example</span></span>
<span data-ttu-id="72e8b-190">tooapply hello filtre tooall d’actions hello sur un `controller`, ajouter un filtre de hello comme un attribut toohello `controller` classe :</span><span class="sxs-lookup"><span data-stu-id="72e8b-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="72e8b-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-191">Example</span></span>
<span data-ttu-id="72e8b-192">tooapply hello filtrer les contrôleurs d’API Web tooall globalement, ajoutez une instance du hello filtre toohello `GlobalConfiguration.Configuration.Filters` collection.</span><span class="sxs-lookup"><span data-stu-id="72e8b-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="72e8b-193">Filtres d’exception dans cette collection s’appliquent d’action du contrôleur Web API tooany.</span><span class="sxs-lookup"><span data-stu-id="72e8b-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="72e8b-194">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-194">Example</span></span>
<span data-ttu-id="72e8b-195">Pour la validation de modèle, état du modèle hello peut être passé méthode tooCreateErrorResponse comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="72e8b-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="72e8b-196">Vérifiez les liens hello dans la section des références pour plus d’informations sur la gestion des exceptionnelles hello et validation de modèle dans l’API Web ASP.Net</span><span class="sxs-lookup"><span data-stu-id="72e8b-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="72e8b-197"><a id="messages"></a>Ne pas exposer les détails de sécurité dans les messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="72e8b-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="72e8b-198">Intitulé</span><span class="sxs-lookup"><span data-stu-id="72e8b-198">Title</span></span>                   | <span data-ttu-id="72e8b-199">Détails</span><span class="sxs-lookup"><span data-stu-id="72e8b-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="72e8b-200">**Composant**</span><span class="sxs-lookup"><span data-stu-id="72e8b-200">**Component**</span></span>               | <span data-ttu-id="72e8b-201">Application web</span><span class="sxs-lookup"><span data-stu-id="72e8b-201">Web Application</span></span> | 
| <span data-ttu-id="72e8b-202">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="72e8b-202">**SDL Phase**</span></span>               | <span data-ttu-id="72e8b-203">Créer</span><span class="sxs-lookup"><span data-stu-id="72e8b-203">Build</span></span> |  
| <span data-ttu-id="72e8b-204">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="72e8b-204">**Applicable Technologies**</span></span> | <span data-ttu-id="72e8b-205">Générique</span><span class="sxs-lookup"><span data-stu-id="72e8b-205">Generic</span></span> |
| <span data-ttu-id="72e8b-206">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="72e8b-206">**Attributes**</span></span>              | <span data-ttu-id="72e8b-207">N/A</span><span class="sxs-lookup"><span data-stu-id="72e8b-207">N/A</span></span>  |
| <span data-ttu-id="72e8b-208">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="72e8b-208">**References**</span></span>              | <span data-ttu-id="72e8b-209">N/A</span><span class="sxs-lookup"><span data-stu-id="72e8b-209">N/A</span></span>  |
| <span data-ttu-id="72e8b-210">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="72e8b-210">**Steps**</span></span> | <p><span data-ttu-id="72e8b-211">Messages d’erreur génériques sont fournies directement toohello utilisateur sans inclure les données d’application sensibles.</span><span class="sxs-lookup"><span data-stu-id="72e8b-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="72e8b-212">Voici quelques exemples de données sensibles :</span><span class="sxs-lookup"><span data-stu-id="72e8b-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="72e8b-213">Noms de serveur</span><span class="sxs-lookup"><span data-stu-id="72e8b-213">Server names</span></span></li><li><span data-ttu-id="72e8b-214">Chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="72e8b-214">Connection strings</span></span></li><li><span data-ttu-id="72e8b-215">Noms d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="72e8b-215">Usernames</span></span></li><li><span data-ttu-id="72e8b-216">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="72e8b-216">Passwords</span></span></li><li><span data-ttu-id="72e8b-217">Procédures SQL</span><span class="sxs-lookup"><span data-stu-id="72e8b-217">SQL procedures</span></span></li><li><span data-ttu-id="72e8b-218">Détail des échecs SQL dynamiques</span><span class="sxs-lookup"><span data-stu-id="72e8b-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="72e8b-219">Arborescence des appels de procédure et lignes de code</span><span class="sxs-lookup"><span data-stu-id="72e8b-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="72e8b-220">Variables stockées dans la mémoire</span><span class="sxs-lookup"><span data-stu-id="72e8b-220">Variables stored in memory</span></span></li><li><span data-ttu-id="72e8b-221">Emplacements de lecteur et de dossier</span><span class="sxs-lookup"><span data-stu-id="72e8b-221">Drive and folder locations</span></span></li><li><span data-ttu-id="72e8b-222">Points d’installation d’application</span><span class="sxs-lookup"><span data-stu-id="72e8b-222">Application install points</span></span></li><li><span data-ttu-id="72e8b-223">Paramètres de configuration d’hôte</span><span class="sxs-lookup"><span data-stu-id="72e8b-223">Host configuration settings</span></span></li><li><span data-ttu-id="72e8b-224">Autres détails de l’application internes</span><span class="sxs-lookup"><span data-stu-id="72e8b-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="72e8b-225">L’interception de toutes les erreurs dans une application, la fourniture de messages d’erreur génériques, ainsi que l’activation des messages d’erreur personnalisés dans IIS permettent d’éviter la divulgation d’informations.</span><span class="sxs-lookup"><span data-stu-id="72e8b-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="72e8b-226">Base de données SQL Server et de gestion, entre autre erreur de gestion des architectures, des exceptions .NET sont utilisateur malveillant de tooa particulièrement longue et extrêmement utiles profiler votre application.</span><span class="sxs-lookup"><span data-stu-id="72e8b-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="72e8b-227">Faire pas directement hello d’afficher le contenu d’une classe dérivée de la classe d’Exception .NET hello et vérifiez que vous disposez de la gestion des exceptions appropriées afin qu’une exception inattendue n’est pas par inadvertance déclenché directement toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="72e8b-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="72e8b-228">Fournir des messages d’erreur générique directement utilisateur toohello qui résument les détails spécifiques rangements trouvés directement dans le message d’erreur d’exception hello</span><span class="sxs-lookup"><span data-stu-id="72e8b-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="72e8b-229">Non affichage hello contenu d’une exception .NET classe directement toohello utilisateur</span><span class="sxs-lookup"><span data-stu-id="72e8b-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="72e8b-230">Intercepter tous les messages d’erreur et le cas échéant informe l’utilisateur hello via un client d’application erreur générique message envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="72e8b-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="72e8b-231">Ne pas exposer de contenu hello de classe d’Exception hello directement toohello utilisateur, en particulier hello retourner la valeur de `.ToString()`, ou les valeurs des propriétés de Message ou StackTrace hello hello.</span><span class="sxs-lookup"><span data-stu-id="72e8b-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="72e8b-232">Se connecter à ces informations et afficher un utilisateur de toohello plus anodin par message en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="72e8b-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="72e8b-233"><a id="default"></a>Implémenter la page de gestion des erreurs par défaut</span><span class="sxs-lookup"><span data-stu-id="72e8b-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="72e8b-234">Intitulé</span><span class="sxs-lookup"><span data-stu-id="72e8b-234">Title</span></span>                   | <span data-ttu-id="72e8b-235">Détails</span><span class="sxs-lookup"><span data-stu-id="72e8b-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="72e8b-236">**Composant**</span><span class="sxs-lookup"><span data-stu-id="72e8b-236">**Component**</span></span>               | <span data-ttu-id="72e8b-237">Application web</span><span class="sxs-lookup"><span data-stu-id="72e8b-237">Web Application</span></span> | 
| <span data-ttu-id="72e8b-238">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="72e8b-238">**SDL Phase**</span></span>               | <span data-ttu-id="72e8b-239">Créer</span><span class="sxs-lookup"><span data-stu-id="72e8b-239">Build</span></span> |  
| <span data-ttu-id="72e8b-240">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="72e8b-240">**Applicable Technologies**</span></span> | <span data-ttu-id="72e8b-241">Générique</span><span class="sxs-lookup"><span data-stu-id="72e8b-241">Generic</span></span> |
| <span data-ttu-id="72e8b-242">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="72e8b-242">**Attributes**</span></span>              | <span data-ttu-id="72e8b-243">N/A</span><span class="sxs-lookup"><span data-stu-id="72e8b-243">N/A</span></span>  |
| <span data-ttu-id="72e8b-244">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="72e8b-244">**References**</span></span>              | <span data-ttu-id="72e8b-245">[Modifier la boîte de dialogue des paramètres des pages d’erreur ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="72e8b-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="72e8b-246">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="72e8b-246">**Steps**</span></span> | <p><span data-ttu-id="72e8b-247">Lorsqu’une application ASP.NET échoue et provoque une erreur serveur interne HTTP/1.x 500, ou que la configuration d’une fonctionnalité (comme le filtrage des demandes) empêche l’affichage d’une page, un message d’erreur est généré.</span><span class="sxs-lookup"><span data-stu-id="72e8b-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="72e8b-248">Les administrateurs peuvent choisir ou non l’application hello doit afficher un message convivial toohello client, client de toohello message erreur détaillé ou erreur détaillée message toolocalhost uniquement.</span><span class="sxs-lookup"><span data-stu-id="72e8b-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="72e8b-249">Hello <customErrors> balise dans le fichier web.config de hello comporte trois modes :</span><span class="sxs-lookup"><span data-stu-id="72e8b-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="72e8b-250">**On :** spécifie que les erreurs personnalisées sont activées.</span><span class="sxs-lookup"><span data-stu-id="72e8b-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="72e8b-251">Si aucun attribut defaultRedirect n’est spécifié, les utilisateurs voient une erreur générique.</span><span class="sxs-lookup"><span data-stu-id="72e8b-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="72e8b-252">les erreurs personnalisées Hello figurent toohello des clients distants et l’hôte local de toohello</span><span class="sxs-lookup"><span data-stu-id="72e8b-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="72e8b-253">**Off :** spécifie que les erreurs personnalisées sont désactivées.</span><span class="sxs-lookup"><span data-stu-id="72e8b-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="72e8b-254">Hello erreurs ASP.NET détaillées sont affichées toohello des clients distants et l’hôte local de toohello</span><span class="sxs-lookup"><span data-stu-id="72e8b-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="72e8b-255">**RemoteOnly :** Spécifie que les erreurs personnalisées sont affichées uniquement des clients distants toohello, et que les erreurs ASP.NET sont affichées les hôte local toohello.</span><span class="sxs-lookup"><span data-stu-id="72e8b-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="72e8b-256">Il s’agit par défaut hello</span><span class="sxs-lookup"><span data-stu-id="72e8b-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="72e8b-257">Ouvrez hello `web.config` de fichiers pour le site/application hello et vérifiez qu’une balise de hello `<customErrors mode="RemoteOnly" />` ou `<customErrors mode="On" />` défini.</span><span class="sxs-lookup"><span data-stu-id="72e8b-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="72e8b-258"><a id="deployment"></a>Définir la méthode de déploiement tooRetail dans IIS</span><span class="sxs-lookup"><span data-stu-id="72e8b-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="72e8b-259">Intitulé</span><span class="sxs-lookup"><span data-stu-id="72e8b-259">Title</span></span>                   | <span data-ttu-id="72e8b-260">Détails</span><span class="sxs-lookup"><span data-stu-id="72e8b-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="72e8b-261">**Composant**</span><span class="sxs-lookup"><span data-stu-id="72e8b-261">**Component**</span></span>               | <span data-ttu-id="72e8b-262">Application web</span><span class="sxs-lookup"><span data-stu-id="72e8b-262">Web Application</span></span> | 
| <span data-ttu-id="72e8b-263">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="72e8b-263">**SDL Phase**</span></span>               | <span data-ttu-id="72e8b-264">Déploiement</span><span class="sxs-lookup"><span data-stu-id="72e8b-264">Deployment</span></span> |  
| <span data-ttu-id="72e8b-265">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="72e8b-265">**Applicable Technologies**</span></span> | <span data-ttu-id="72e8b-266">Générique</span><span class="sxs-lookup"><span data-stu-id="72e8b-266">Generic</span></span> |
| <span data-ttu-id="72e8b-267">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="72e8b-267">**Attributes**</span></span>              | <span data-ttu-id="72e8b-268">N/A</span><span class="sxs-lookup"><span data-stu-id="72e8b-268">N/A</span></span>  |
| <span data-ttu-id="72e8b-269">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="72e8b-269">**References**</span></span>              | <span data-ttu-id="72e8b-270">[Élément de déploiement (schéma des paramètres ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="72e8b-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="72e8b-271">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="72e8b-271">**Steps**</span></span> | <p><span data-ttu-id="72e8b-272">Hello `<deployment retail>` commutateur est destiné aux serveurs IIS de production.</span><span class="sxs-lookup"><span data-stu-id="72e8b-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="72e8b-273">Ce commutateur est utilisé toohelp aux applications d’exécuter avec des performances optimales hello et des informations de sécurité minimales fuites en désactivant hello la sortie de trace de l’application capacité toogenerate sur une page, la désactivation de la toodisplay de capacité hello d’erreur détaillés messages tooend utilisateurs et hello pour désactiver le commutateur de débogage.</span><span class="sxs-lookup"><span data-stu-id="72e8b-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="72e8b-274">Les commutateurs et les options destinés aux développeurs, comme le suivi et le débogage des échecs de demande, sont généralement activés pendant le développement actif.</span><span class="sxs-lookup"><span data-stu-id="72e8b-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="72e8b-275">Il est recommandé de définir que la méthode de déploiement hello sur n’importe quel serveur de production tooretail.</span><span class="sxs-lookup"><span data-stu-id="72e8b-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="72e8b-276">Ouvrez le fichier machine.config de hello et vérifiez que `<deployment retail="true" />` conserve la valeur tootrue.</span><span class="sxs-lookup"><span data-stu-id="72e8b-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="72e8b-277"><a id="fail"></a>Les exceptions doivent échouer en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="72e8b-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="72e8b-278">Intitulé</span><span class="sxs-lookup"><span data-stu-id="72e8b-278">Title</span></span>                   | <span data-ttu-id="72e8b-279">Détails</span><span class="sxs-lookup"><span data-stu-id="72e8b-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="72e8b-280">**Composant**</span><span class="sxs-lookup"><span data-stu-id="72e8b-280">**Component**</span></span>               | <span data-ttu-id="72e8b-281">Application web</span><span class="sxs-lookup"><span data-stu-id="72e8b-281">Web Application</span></span> | 
| <span data-ttu-id="72e8b-282">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="72e8b-282">**SDL Phase**</span></span>               | <span data-ttu-id="72e8b-283">Créer</span><span class="sxs-lookup"><span data-stu-id="72e8b-283">Build</span></span> |  
| <span data-ttu-id="72e8b-284">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="72e8b-284">**Applicable Technologies**</span></span> | <span data-ttu-id="72e8b-285">Générique</span><span class="sxs-lookup"><span data-stu-id="72e8b-285">Generic</span></span> |
| <span data-ttu-id="72e8b-286">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="72e8b-286">**Attributes**</span></span>              | <span data-ttu-id="72e8b-287">N/A</span><span class="sxs-lookup"><span data-stu-id="72e8b-287">N/A</span></span>  |
| <span data-ttu-id="72e8b-288">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="72e8b-288">**References**</span></span>              | [<span data-ttu-id="72e8b-289">Échec en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="72e8b-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="72e8b-290">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="72e8b-290">**Steps**</span></span> | <span data-ttu-id="72e8b-291">L’application doit échouer en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="72e8b-291">Application should fail safely.</span></span> <span data-ttu-id="72e8b-292">Toute méthode renvoyant une valeur booléenne, en fonction de la décision prise, doit comporter un bloc d’exception créé avec soin.</span><span class="sxs-lookup"><span data-stu-id="72e8b-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="72e8b-293">Il existe de nombreuses erreurs logiques en raison de l’escalade de problèmes de sécurité toowhich dans, lorsque le bloc d’exception hello est écrit sans.</span><span class="sxs-lookup"><span data-stu-id="72e8b-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="72e8b-294">Exemple</span><span class="sxs-lookup"><span data-stu-id="72e8b-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="72e8b-295">Hello au-dessus de la méthode retourne toujours la valeur True, si une exception se produit.</span><span class="sxs-lookup"><span data-stu-id="72e8b-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="72e8b-296">Si l’utilisateur final de hello fournit une URL incorrecte, qui hello navigateur égards, mais hello `Uri()` constructeur n’et une exception est levée victime de hello à entreprendre les URL valides mais incorrect toohello.</span><span class="sxs-lookup"><span data-stu-id="72e8b-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
