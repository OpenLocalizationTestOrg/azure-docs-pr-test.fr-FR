---
title: "Gestion des exceptions - Outil Microsoft de modélisation des menaces - Azure | Microsoft Docs"
description: "mesures de correction des menaces exposées dans l’outil de modélisation des menaces"
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
ms.openlocfilehash: bbf357b902474a1812eb7a5a2c914d0c8b91934b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="b9e91-103">Infrastructure de sécurité : Gestion des exceptions | Corrections</span><span class="sxs-lookup"><span data-stu-id="b9e91-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="b9e91-104">Produit/service</span><span class="sxs-lookup"><span data-stu-id="b9e91-104">Product/Service</span></span> | <span data-ttu-id="b9e91-105">Article</span><span class="sxs-lookup"><span data-stu-id="b9e91-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="b9e91-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="b9e91-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="b9e91-107">WCF - Ne pas inclure le nœud serviceDebug dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="b9e91-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="b9e91-108">WCF - Ne pas inclure le nœud serviceMetadata dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="b9e91-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="b9e91-109">**API Web**</span><span class="sxs-lookup"><span data-stu-id="b9e91-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="b9e91-110">Vérifier que la gestion des exceptions correcte est effectuée dans l’API web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e91-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="b9e91-111">**Application web**</span><span class="sxs-lookup"><span data-stu-id="b9e91-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="b9e91-112">Ne pas exposer les détails de sécurité dans les messages d’erreur </span><span class="sxs-lookup"><span data-stu-id="b9e91-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="b9e91-113">Implémenter la page de gestion des erreurs par défaut </span><span class="sxs-lookup"><span data-stu-id="b9e91-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="b9e91-114">Définir la méthode de déploiement sur Vente au détail dans IIS</span><span class="sxs-lookup"><span data-stu-id="b9e91-114">Set Deployment Method to Retail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="b9e91-115">Les exceptions doivent échouer en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="b9e91-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="b9e91-116"><a id="servicedebug"></a>WCF - Ne pas inclure le nœud serviceDebug dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="b9e91-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="b9e91-117">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b9e91-117">Title</span></span>                   | <span data-ttu-id="b9e91-118">Détails</span><span class="sxs-lookup"><span data-stu-id="b9e91-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b9e91-119">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b9e91-119">**Component**</span></span>               | <span data-ttu-id="b9e91-120">WCF</span><span class="sxs-lookup"><span data-stu-id="b9e91-120">WCF</span></span> | 
| <span data-ttu-id="b9e91-121">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b9e91-121">**SDL Phase**</span></span>               | <span data-ttu-id="b9e91-122">Créer</span><span class="sxs-lookup"><span data-stu-id="b9e91-122">Build</span></span> |  
| <span data-ttu-id="b9e91-123">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b9e91-123">**Applicable Technologies**</span></span> | <span data-ttu-id="b9e91-124">Générique, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="b9e91-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="b9e91-125">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b9e91-125">**Attributes**</span></span>              | <span data-ttu-id="b9e91-126">N/A</span><span class="sxs-lookup"><span data-stu-id="b9e91-126">N/A</span></span>  |
| <span data-ttu-id="b9e91-127">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b9e91-127">**References**</span></span>              | <span data-ttu-id="b9e91-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="b9e91-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="b9e91-129">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b9e91-129">**Steps**</span></span> | <span data-ttu-id="b9e91-130">Des services Windows Communication Framework (WCF) peuvent être configurés pour exposer des informations de débogage.</span><span class="sxs-lookup"><span data-stu-id="b9e91-130">Windows Communication Framework (WCF) services can be configured to expose debugging information.</span></span> <span data-ttu-id="b9e91-131">Les informations de débogage ne doivent pas être utilisées dans les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="b9e91-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="b9e91-132">La balise `<serviceDebug>` définit si la fonctionnalité d’informations de débogage est activée pour un service WCF.</span><span class="sxs-lookup"><span data-stu-id="b9e91-132">The `<serviceDebug>` tag defines whether the debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="b9e91-133">Si l’attribut includeExceptionDetailInFaults est défini sur true, les informations sur les exceptions de l’application sont renvoyées aux clients.</span><span class="sxs-lookup"><span data-stu-id="b9e91-133">If the attribute includeExceptionDetailInFaults is set to true, exception information from the application will be returned to clients.</span></span> <span data-ttu-id="b9e91-134">Les personnes malveillantes peuvent exploiter les informations supplémentaires qu’elles obtiennent de la sortie de débogage pour lancer des attaques ciblées sur l’infrastructure, la base de données ou d’autres ressources utilisées par l’application.</span><span class="sxs-lookup"><span data-stu-id="b9e91-134">Attackers can leverage the additional information they gain from debugging output to mount attacks targeted on the framework, database, or other resources used by the application.</span></span> |

### <a name="example"></a><span data-ttu-id="b9e91-135">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-135">Example</span></span>
<span data-ttu-id="b9e91-136">Le fichier de configuration suivant inclut la balise `<serviceDebug>` :</span><span class="sxs-lookup"><span data-stu-id="b9e91-136">The following configuration file includes the `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="b9e91-137">Désactivez les informations de débogage dans le service.</span><span class="sxs-lookup"><span data-stu-id="b9e91-137">Disable debugging information in the service.</span></span> <span data-ttu-id="b9e91-138">Ceci peut être effectué en supprimant la balise `<serviceDebug>` du fichier de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="b9e91-138">This can be accomplished by removing the `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="b9e91-139"><a id="servicemetadata"></a>WCF - Ne pas inclure le nœud serviceMetadata dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="b9e91-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="b9e91-140">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b9e91-140">Title</span></span>                   | <span data-ttu-id="b9e91-141">Détails</span><span class="sxs-lookup"><span data-stu-id="b9e91-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b9e91-142">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b9e91-142">**Component**</span></span>               | <span data-ttu-id="b9e91-143">WCF</span><span class="sxs-lookup"><span data-stu-id="b9e91-143">WCF</span></span> | 
| <span data-ttu-id="b9e91-144">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b9e91-144">**SDL Phase**</span></span>               | <span data-ttu-id="b9e91-145">Créer</span><span class="sxs-lookup"><span data-stu-id="b9e91-145">Build</span></span> |  
| <span data-ttu-id="b9e91-146">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b9e91-146">**Applicable Technologies**</span></span> | <span data-ttu-id="b9e91-147">Générique</span><span class="sxs-lookup"><span data-stu-id="b9e91-147">Generic</span></span> |
| <span data-ttu-id="b9e91-148">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b9e91-148">**Attributes**</span></span>              | <span data-ttu-id="b9e91-149">Générique, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="b9e91-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="b9e91-150">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b9e91-150">**References**</span></span>              | <span data-ttu-id="b9e91-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="b9e91-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="b9e91-152">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b9e91-152">**Steps**</span></span> | <span data-ttu-id="b9e91-153">L’exposition publique des informations sur un service peut fournir aux personnes malveillantes une piste précieuse sur la manière dont elles peuvent exploiter le service.</span><span class="sxs-lookup"><span data-stu-id="b9e91-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit the service.</span></span> <span data-ttu-id="b9e91-154">La balise `<serviceMetadata>` active la fonctionnalité de publication de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="b9e91-154">The `<serviceMetadata>` tag enables the metadata publishing feature.</span></span> <span data-ttu-id="b9e91-155">Les métadonnées de service peuvent contenir des informations sensibles qui ne doivent pas être accessibles publiquement.</span><span class="sxs-lookup"><span data-stu-id="b9e91-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="b9e91-156">Au minimum, autorisez uniquement les utilisateurs approuvés à accéder aux métadonnées et vérifiez que les informations inutiles ne sont pas exposées.</span><span class="sxs-lookup"><span data-stu-id="b9e91-156">At a minimum, only allow trusted users to access the metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="b9e91-157">Mieux encore, désactivez complètement la possibilité de publier des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="b9e91-157">Better yet, entirely disable the ability to publish metadata.</span></span> <span data-ttu-id="b9e91-158">Une configuration WCF sûre ne contiendra pas la balise `<serviceMetadata>`.</span><span class="sxs-lookup"><span data-stu-id="b9e91-158">A safe WCF configuration will not contain the `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="b9e91-159"><a id="exception"></a>Vérifier que la gestion des exceptions correcte est effectuée dans l’API web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9e91-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="b9e91-160">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b9e91-160">Title</span></span>                   | <span data-ttu-id="b9e91-161">Détails</span><span class="sxs-lookup"><span data-stu-id="b9e91-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b9e91-162">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b9e91-162">**Component**</span></span>               | <span data-ttu-id="b9e91-163">API Web</span><span class="sxs-lookup"><span data-stu-id="b9e91-163">Web API</span></span> | 
| <span data-ttu-id="b9e91-164">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b9e91-164">**SDL Phase**</span></span>               | <span data-ttu-id="b9e91-165">Créer</span><span class="sxs-lookup"><span data-stu-id="b9e91-165">Build</span></span> |  
| <span data-ttu-id="b9e91-166">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b9e91-166">**Applicable Technologies**</span></span> | <span data-ttu-id="b9e91-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="b9e91-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="b9e91-168">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b9e91-168">**Attributes**</span></span>              | <span data-ttu-id="b9e91-169">N/A</span><span class="sxs-lookup"><span data-stu-id="b9e91-169">N/A</span></span>  |
| <span data-ttu-id="b9e91-170">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b9e91-170">**References**</span></span>              | <span data-ttu-id="b9e91-171">[Gestion des exceptions dans l’API web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Validation de modèle dans l’API web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="b9e91-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="b9e91-172">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b9e91-172">**Steps**</span></span> | <span data-ttu-id="b9e91-173">Par défaut, la plupart des exceptions non interceptées dans l’API web ASP.NET sont converties en réponse HTTP avec le code d’état`500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="b9e91-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="b9e91-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-174">Example</span></span>
<span data-ttu-id="b9e91-175">Pour contrôler le code d’état renvoyé par l’API, `HttpResponseException` peut être utilisé comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b9e91-175">To control the status code returned by the API, `HttpResponseException` can be used as shown below:</span></span> 
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

### <a name="example"></a><span data-ttu-id="b9e91-176">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-176">Example</span></span>
<span data-ttu-id="b9e91-177">Pour contrôler davantage la réponse d’exception, la classe `HttpResponseMessage` peut être utilisée comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b9e91-177">For further control on the exception response, the `HttpResponseMessage` class can be used as shown below:</span></span> 
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
<span data-ttu-id="b9e91-178">Pour intercepter les exceptions non prises en charge qui ne sont pas du type `HttpResponseException`, des filtres d’exception peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="b9e91-178">To catch unhandled exceptions that are not of the type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="b9e91-179">Les filtres d’exception implémentent l’interface `System.Web.Http.Filters.IExceptionFilter`.</span><span class="sxs-lookup"><span data-stu-id="b9e91-179">Exception filters implement the `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="b9e91-180">La méthode la plus simple pour écrire un filtre d’exception consiste à le dériver de la classe `System.Web.Http.Filters.ExceptionFilterAttribute` et à remplacer la méthode OnException.</span><span class="sxs-lookup"><span data-stu-id="b9e91-180">The simplest way to write an exception filter is to derive from the `System.Web.Http.Filters.ExceptionFilterAttribute` class and override the OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="b9e91-181">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-181">Example</span></span>
<span data-ttu-id="b9e91-182">Voici un filtre qui convertit des `NotImplementedException` exceptions en code d’état HTTP `501, Not Implemented` :</span><span class="sxs-lookup"><span data-stu-id="b9e91-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
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

<span data-ttu-id="b9e91-183">Plusieurs méthodes pour enregistrer un filtre d’exception d’API web sont possibles :</span><span class="sxs-lookup"><span data-stu-id="b9e91-183">There are several ways to register a Web API exception filter:</span></span>
- <span data-ttu-id="b9e91-184">Par action</span><span class="sxs-lookup"><span data-stu-id="b9e91-184">By action</span></span>
- <span data-ttu-id="b9e91-185">Par contrôleur</span><span class="sxs-lookup"><span data-stu-id="b9e91-185">By controller</span></span>
- <span data-ttu-id="b9e91-186">Globalement</span><span class="sxs-lookup"><span data-stu-id="b9e91-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="b9e91-187">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-187">Example</span></span>
<span data-ttu-id="b9e91-188">Pour appliquer le filtre à une action spécifique, ajoutez le filtre en tant qu’attribut à l’action :</span><span class="sxs-lookup"><span data-stu-id="b9e91-188">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span> 
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
### <a name="example"></a><span data-ttu-id="b9e91-189">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-189">Example</span></span>
<span data-ttu-id="b9e91-190">Pour appliquer le filtre à toutes les actions sur un `controller`, ajoutez le filtre en tant qu’attribut à la classe `controller` :</span><span class="sxs-lookup"><span data-stu-id="b9e91-190">To apply the filter to all of the actions on a `controller`, add the filter as an attribute to the `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="b9e91-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-191">Example</span></span>
<span data-ttu-id="b9e91-192">Pour appliquer le filtre globalement à tous les contrôleurs d’API web, ajoutez une instance du filtre à la collection `GlobalConfiguration.Configuration.Filters`.</span><span class="sxs-lookup"><span data-stu-id="b9e91-192">To apply the filter globally to all Web API controllers, add an instance of the filter to the `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="b9e91-193">Les filtres d’exception de cette collection s’appliquent à n’importe quelle action de contrôleur d’API web.</span><span class="sxs-lookup"><span data-stu-id="b9e91-193">Exception filters in this collection apply to any Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="b9e91-194">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-194">Example</span></span>
<span data-ttu-id="b9e91-195">Pour valider un modèle, l’état du modèle peut être transmis à la méthode CreateErrorResponse comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b9e91-195">For model validation, the model state can be passed to CreateErrorResponse method as shown below:</span></span> 
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

<span data-ttu-id="b9e91-196">Vérifiez les liens dans la section Références pour plus d’informations sur la gestion exceptionnelle et la validation de modèle dans l’API web ASP.Net</span><span class="sxs-lookup"><span data-stu-id="b9e91-196">Check the links in the references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="b9e91-197"><a id="messages"></a>Ne pas exposer les détails de sécurité dans les messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="b9e91-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="b9e91-198">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b9e91-198">Title</span></span>                   | <span data-ttu-id="b9e91-199">Détails</span><span class="sxs-lookup"><span data-stu-id="b9e91-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b9e91-200">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b9e91-200">**Component**</span></span>               | <span data-ttu-id="b9e91-201">Application web</span><span class="sxs-lookup"><span data-stu-id="b9e91-201">Web Application</span></span> | 
| <span data-ttu-id="b9e91-202">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b9e91-202">**SDL Phase**</span></span>               | <span data-ttu-id="b9e91-203">Créer</span><span class="sxs-lookup"><span data-stu-id="b9e91-203">Build</span></span> |  
| <span data-ttu-id="b9e91-204">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b9e91-204">**Applicable Technologies**</span></span> | <span data-ttu-id="b9e91-205">Générique</span><span class="sxs-lookup"><span data-stu-id="b9e91-205">Generic</span></span> |
| <span data-ttu-id="b9e91-206">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b9e91-206">**Attributes**</span></span>              | <span data-ttu-id="b9e91-207">N/A</span><span class="sxs-lookup"><span data-stu-id="b9e91-207">N/A</span></span>  |
| <span data-ttu-id="b9e91-208">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b9e91-208">**References**</span></span>              | <span data-ttu-id="b9e91-209">N/A</span><span class="sxs-lookup"><span data-stu-id="b9e91-209">N/A</span></span>  |
| <span data-ttu-id="b9e91-210">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b9e91-210">**Steps**</span></span> | <p><span data-ttu-id="b9e91-211">Des messages d’erreur génériques sont fournis directement à l’utilisateur sans inclure de données d’application sensibles.</span><span class="sxs-lookup"><span data-stu-id="b9e91-211">Generic error messages are provided directly to the user without including sensitive application data.</span></span> <span data-ttu-id="b9e91-212">Voici quelques exemples de données sensibles :</span><span class="sxs-lookup"><span data-stu-id="b9e91-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="b9e91-213">Noms de serveur</span><span class="sxs-lookup"><span data-stu-id="b9e91-213">Server names</span></span></li><li><span data-ttu-id="b9e91-214">Chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="b9e91-214">Connection strings</span></span></li><li><span data-ttu-id="b9e91-215">Noms d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b9e91-215">Usernames</span></span></li><li><span data-ttu-id="b9e91-216">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="b9e91-216">Passwords</span></span></li><li><span data-ttu-id="b9e91-217">Procédures SQL</span><span class="sxs-lookup"><span data-stu-id="b9e91-217">SQL procedures</span></span></li><li><span data-ttu-id="b9e91-218">Détail des échecs SQL dynamiques</span><span class="sxs-lookup"><span data-stu-id="b9e91-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="b9e91-219">Arborescence des appels de procédure et lignes de code</span><span class="sxs-lookup"><span data-stu-id="b9e91-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="b9e91-220">Variables stockées dans la mémoire</span><span class="sxs-lookup"><span data-stu-id="b9e91-220">Variables stored in memory</span></span></li><li><span data-ttu-id="b9e91-221">Emplacements de lecteur et de dossier</span><span class="sxs-lookup"><span data-stu-id="b9e91-221">Drive and folder locations</span></span></li><li><span data-ttu-id="b9e91-222">Points d’installation d’application</span><span class="sxs-lookup"><span data-stu-id="b9e91-222">Application install points</span></span></li><li><span data-ttu-id="b9e91-223">Paramètres de configuration d’hôte</span><span class="sxs-lookup"><span data-stu-id="b9e91-223">Host configuration settings</span></span></li><li><span data-ttu-id="b9e91-224">Autres détails de l’application internes</span><span class="sxs-lookup"><span data-stu-id="b9e91-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="b9e91-225">L’interception de toutes les erreurs dans une application, la fourniture de messages d’erreur génériques, ainsi que l’activation des messages d’erreur personnalisés dans IIS permettent d’éviter la divulgation d’informations.</span><span class="sxs-lookup"><span data-stu-id="b9e91-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="b9e91-226">La base de données SQL Server et la gestion des exceptions .NET, entre autres architectures de gestion des erreurs, sont particulièrement détaillées et extrêmement utiles à un utilisateur malveillant profilant votre application.</span><span class="sxs-lookup"><span data-stu-id="b9e91-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful to a malicious user profiling your application.</span></span> <span data-ttu-id="b9e91-227">N’affichez pas directement le contenu d’une classe dérivée de la classe d’exceptions .NET et vérifiez que vous disposez de la gestion des exceptions appropriée afin qu’une exception inattendue ne soit pas présentée directement par inadvertance à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b9e91-227">Do not directly display the contents of a class derived from the .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly to the user.</span></span></p><ul><li><span data-ttu-id="b9e91-228">Fournissez des messages d’erreur génériques directement à l’utilisateur qui résument les détails spécifiques trouvés directement dans le message d’exception/d’erreur</span><span class="sxs-lookup"><span data-stu-id="b9e91-228">Provide generic error messages directly to the user that abstract away specific details found directly in the exception/error message</span></span></li><li><span data-ttu-id="b9e91-229">Ne présentez pas le contenu d’une classe d’exceptions .NET directement à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b9e91-229">Do not display the contents of a .NET exception class directly to the user</span></span></li><li><span data-ttu-id="b9e91-230">Interceptez tous les messages d’erreur et, le cas échéant, informez l’utilisateur à l’aide d’un message d’erreur générique envoyé au client de l’application</span><span class="sxs-lookup"><span data-stu-id="b9e91-230">Trap all error messages and if appropriate inform the user via a generic error message sent to the application client</span></span></li><li><span data-ttu-id="b9e91-231">N’exposez pas le contenu de la classe d’exceptions directement à l’utilisateur, et plus particulièrement la valeur renvoyée par `.ToString()`, ou les valeurs des propriétés Message ou StackTrace.</span><span class="sxs-lookup"><span data-stu-id="b9e91-231">Do not expose the contents of the Exception class directly to the user, especially the return value from `.ToString()`, or the values of the Message or StackTrace properties.</span></span> <span data-ttu-id="b9e91-232">Journalisez ces informations de manière sécurisée et présentez un message plus inoffensif à l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b9e91-232">Securely log this information and display a more innocuous message to the user</span></span></li></ul>|

## <span data-ttu-id="b9e91-233"><a id="default"></a>Implémenter la page de gestion des erreurs par défaut</span><span class="sxs-lookup"><span data-stu-id="b9e91-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="b9e91-234">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b9e91-234">Title</span></span>                   | <span data-ttu-id="b9e91-235">Détails</span><span class="sxs-lookup"><span data-stu-id="b9e91-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b9e91-236">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b9e91-236">**Component**</span></span>               | <span data-ttu-id="b9e91-237">Application web</span><span class="sxs-lookup"><span data-stu-id="b9e91-237">Web Application</span></span> | 
| <span data-ttu-id="b9e91-238">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b9e91-238">**SDL Phase**</span></span>               | <span data-ttu-id="b9e91-239">Créer</span><span class="sxs-lookup"><span data-stu-id="b9e91-239">Build</span></span> |  
| <span data-ttu-id="b9e91-240">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b9e91-240">**Applicable Technologies**</span></span> | <span data-ttu-id="b9e91-241">Générique</span><span class="sxs-lookup"><span data-stu-id="b9e91-241">Generic</span></span> |
| <span data-ttu-id="b9e91-242">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b9e91-242">**Attributes**</span></span>              | <span data-ttu-id="b9e91-243">N/A</span><span class="sxs-lookup"><span data-stu-id="b9e91-243">N/A</span></span>  |
| <span data-ttu-id="b9e91-244">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b9e91-244">**References**</span></span>              | <span data-ttu-id="b9e91-245">[Modifier la boîte de dialogue des paramètres des pages d’erreur ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="b9e91-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="b9e91-246">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b9e91-246">**Steps**</span></span> | <p><span data-ttu-id="b9e91-247">Lorsqu’une application ASP.NET échoue et provoque une erreur serveur interne HTTP/1.x 500, ou que la configuration d’une fonctionnalité (comme le filtrage des demandes) empêche l’affichage d’une page, un message d’erreur est généré.</span><span class="sxs-lookup"><span data-stu-id="b9e91-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="b9e91-248">Les administrateurs peuvent choisir si l’application doit afficher ou non un message convivial pour le client, un message d’erreur détaillé au client ou un message d’erreur détaillé à l’hôte local uniquement.</span><span class="sxs-lookup"><span data-stu-id="b9e91-248">Administrators can choose whether or not the application should display a friendly message to the client, detailed error message to the client, or detailed error message to localhost only.</span></span> <span data-ttu-id="b9e91-249">La balise <customErrors> dans le fichier web.config comporte trois modes :</span><span class="sxs-lookup"><span data-stu-id="b9e91-249">The <customErrors> tag in the web.config has three modes:</span></span></p><ul><li><span data-ttu-id="b9e91-250">**On :** spécifie que les erreurs personnalisées sont activées.</span><span class="sxs-lookup"><span data-stu-id="b9e91-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="b9e91-251">Si aucun attribut defaultRedirect n’est spécifié, les utilisateurs voient une erreur générique.</span><span class="sxs-lookup"><span data-stu-id="b9e91-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="b9e91-252">Les erreurs personnalisées sont présentées aux clients distants et à l’hôte local</span><span class="sxs-lookup"><span data-stu-id="b9e91-252">The custom errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="b9e91-253">**Off :** spécifie que les erreurs personnalisées sont désactivées.</span><span class="sxs-lookup"><span data-stu-id="b9e91-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="b9e91-254">Les erreurs ASP.NET détaillées sont présentées aux clients distants et à l’hôte local</span><span class="sxs-lookup"><span data-stu-id="b9e91-254">The detailed ASP.NET errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="b9e91-255">**RemoteOnly :** spécifie que les erreurs personnalisées sont visibles uniquement pour les clients distants, et que les erreurs ASP.NET sont visibles pour l’hôte local.</span><span class="sxs-lookup"><span data-stu-id="b9e91-255">**RemoteOnly:** Specifies that custom errors are shown only to the remote clients, and that ASP.NET errors are shown to the local host.</span></span> <span data-ttu-id="b9e91-256">Il s’agit de la valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="b9e91-256">This is the default value</span></span></li></ul><p><span data-ttu-id="b9e91-257">Ouvrez le fichier `web.config` pour l’application/le site et vérifiez que la balise est définie sur `<customErrors mode="RemoteOnly" />` ou `<customErrors mode="On" />`.</span><span class="sxs-lookup"><span data-stu-id="b9e91-257">Open the `web.config` file for the application/site and ensure that the tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="b9e91-258"><a id="deployment"></a>Définir la méthode de déploiement sur Vente au détail dans IIS</span><span class="sxs-lookup"><span data-stu-id="b9e91-258"><a id="deployment"></a>Set Deployment Method to Retail in IIS</span></span>

| <span data-ttu-id="b9e91-259">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b9e91-259">Title</span></span>                   | <span data-ttu-id="b9e91-260">Détails</span><span class="sxs-lookup"><span data-stu-id="b9e91-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b9e91-261">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b9e91-261">**Component**</span></span>               | <span data-ttu-id="b9e91-262">Application web</span><span class="sxs-lookup"><span data-stu-id="b9e91-262">Web Application</span></span> | 
| <span data-ttu-id="b9e91-263">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b9e91-263">**SDL Phase**</span></span>               | <span data-ttu-id="b9e91-264">Déploiement</span><span class="sxs-lookup"><span data-stu-id="b9e91-264">Deployment</span></span> |  
| <span data-ttu-id="b9e91-265">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b9e91-265">**Applicable Technologies**</span></span> | <span data-ttu-id="b9e91-266">Générique</span><span class="sxs-lookup"><span data-stu-id="b9e91-266">Generic</span></span> |
| <span data-ttu-id="b9e91-267">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b9e91-267">**Attributes**</span></span>              | <span data-ttu-id="b9e91-268">N/A</span><span class="sxs-lookup"><span data-stu-id="b9e91-268">N/A</span></span>  |
| <span data-ttu-id="b9e91-269">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b9e91-269">**References**</span></span>              | <span data-ttu-id="b9e91-270">[Élément de déploiement (schéma des paramètres ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="b9e91-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="b9e91-271">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b9e91-271">**Steps**</span></span> | <p><span data-ttu-id="b9e91-272">Le commutateur `<deployment retail>` est conçu pour être utilisé par les serveurs IIS de production.</span><span class="sxs-lookup"><span data-stu-id="b9e91-272">The `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="b9e91-273">Ce commutateur est utilisé pour permettre aux applications de s’exécuter avec les meilleurs niveaux de performances et le moins de fuites d’informations de sécurité possibles en désactivant la capacité de l’application à générer la sortie de trace sur une page, en désactivant la capacité à afficher des messages d’erreur détaillés pour les utilisateurs finaux et en désactivant le commutateur de débogage.</span><span class="sxs-lookup"><span data-stu-id="b9e91-273">This switch is used to help applications run with the best possible performance and least possible security information leakages by disabling the application's ability to generate trace output on a page, disabling the ability to display detailed error messages to end users, and disabling the debug switch.</span></span></p><p><span data-ttu-id="b9e91-274">Les commutateurs et les options destinés aux développeurs, comme le suivi et le débogage des échecs de demande, sont généralement activés pendant le développement actif.</span><span class="sxs-lookup"><span data-stu-id="b9e91-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="b9e91-275">Il est recommandé de définir la méthode de déploiement de n’importe quel serveur de production sur Vente au détail.</span><span class="sxs-lookup"><span data-stu-id="b9e91-275">It is recommended that the deployment method on any production server be set to retail.</span></span> <span data-ttu-id="b9e91-276">Ouvrez le fichier machine.config et vérifiez que `<deployment retail="true" />` est toujours défini sur true.</span><span class="sxs-lookup"><span data-stu-id="b9e91-276">open the machine.config file and ensure that `<deployment retail="true" />` remains set to true.</span></span></p>|

## <span data-ttu-id="b9e91-277"><a id="fail"></a>Les exceptions doivent échouer en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="b9e91-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="b9e91-278">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b9e91-278">Title</span></span>                   | <span data-ttu-id="b9e91-279">Détails</span><span class="sxs-lookup"><span data-stu-id="b9e91-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b9e91-280">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b9e91-280">**Component**</span></span>               | <span data-ttu-id="b9e91-281">Application web</span><span class="sxs-lookup"><span data-stu-id="b9e91-281">Web Application</span></span> | 
| <span data-ttu-id="b9e91-282">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b9e91-282">**SDL Phase**</span></span>               | <span data-ttu-id="b9e91-283">Créer</span><span class="sxs-lookup"><span data-stu-id="b9e91-283">Build</span></span> |  
| <span data-ttu-id="b9e91-284">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b9e91-284">**Applicable Technologies**</span></span> | <span data-ttu-id="b9e91-285">Générique</span><span class="sxs-lookup"><span data-stu-id="b9e91-285">Generic</span></span> |
| <span data-ttu-id="b9e91-286">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b9e91-286">**Attributes**</span></span>              | <span data-ttu-id="b9e91-287">N/A</span><span class="sxs-lookup"><span data-stu-id="b9e91-287">N/A</span></span>  |
| <span data-ttu-id="b9e91-288">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b9e91-288">**References**</span></span>              | [<span data-ttu-id="b9e91-289">Échec en toute sécurité</span><span class="sxs-lookup"><span data-stu-id="b9e91-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="b9e91-290">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b9e91-290">**Steps**</span></span> | <span data-ttu-id="b9e91-291">L’application doit échouer en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="b9e91-291">Application should fail safely.</span></span> <span data-ttu-id="b9e91-292">Toute méthode renvoyant une valeur booléenne, en fonction de la décision prise, doit comporter un bloc d’exception créé avec soin.</span><span class="sxs-lookup"><span data-stu-id="b9e91-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="b9e91-293">Il existe un grand nombre d’erreurs logiques dues à des problèmes de sécurité lorsque le bloc d’exception n’est pas écrit correctement.</span><span class="sxs-lookup"><span data-stu-id="b9e91-293">There are lot of logical errors due to which security issues creep in, when the exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="b9e91-294">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9e91-294">Example</span></span>
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
                        //// Adding additional check to enable CMS urls if they are not hosted on same domain.
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
<span data-ttu-id="b9e91-295">La méthode ci-dessus renvoie toujours la valeur True si une exception se produit.</span><span class="sxs-lookup"><span data-stu-id="b9e91-295">The above method will always return True, if some exception happens.</span></span> <span data-ttu-id="b9e91-296">Si l’utilisateur final fournit une URL incorrecte acceptée par le navigateur mais pas par le constructeur `Uri()`, une exception est levée et la victime est dirigée vers l’URL valide mais mal formée.</span><span class="sxs-lookup"><span data-stu-id="b9e91-296">If the end user provides a malformed URL, that the browser respects, but the `Uri()` constructor doesn't, this will throw an exception, and the victim will be taken to the valid but malformed URL.</span></span> 