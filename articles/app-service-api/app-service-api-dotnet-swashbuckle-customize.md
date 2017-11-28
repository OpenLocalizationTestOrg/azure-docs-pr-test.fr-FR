---
title: "définitions d’aaaCustomize généré Swashbuckle des API"
description: "Découvrez comment les définitions de Swagger des API toocustomize qui sont générées par Swashbuckle pour une application API dans Azure App Service."
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="6b717-103">Personnaliser des définitions d’API générées par Swashbuckle</span><span class="sxs-lookup"><span data-stu-id="6b717-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="6b717-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6b717-104">Overview</span></span>
<span data-ttu-id="6b717-105">Cet article explique comment toocustomize Swashbuckle toohandle scénarios courants que vous deviez tooalter hello le comportement par défaut :</span><span class="sxs-lookup"><span data-stu-id="6b717-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="6b717-106">Swashbuckle génère des identificateurs d'opération en double pour les surcharges des méthodes de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="6b717-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="6b717-107">Swashbuckle part du principe que hello uniquement une réponse valide à partir d’une méthode est HTTP 200 (OK)</span><span class="sxs-lookup"><span data-stu-id="6b717-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="6b717-108">Personnaliser la génération d'identificateurs d'opération</span><span class="sxs-lookup"><span data-stu-id="6b717-108">Customize operation identifier generation</span></span>
<span data-ttu-id="6b717-109">Swashbuckle génère des identificateurs d’opération Swagger en concaténant le nom du contrôleur et le nom de la méthode.</span><span class="sxs-lookup"><span data-stu-id="6b717-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="6b717-110">Ce modèle crée un problème lorsque vous avez plusieurs surcharges pour une méthode : Swashbuckle génère les ID d’opération en double, ce qui est incompatible avec le format Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="6b717-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="6b717-111">Par exemple, hello suivant le code du contrôleur, Swashbuckle toogenerate ID d’opération Contact_Get trois.</span><span class="sxs-lookup"><span data-stu-id="6b717-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="6b717-112">Vous pouvez résoudre le problème de hello manuellement en fournissant des méthodes de hello des noms uniques, tels que les suivants hello pour cet exemple :</span><span class="sxs-lookup"><span data-stu-id="6b717-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="6b717-113">Obtenir</span><span class="sxs-lookup"><span data-stu-id="6b717-113">Get</span></span>
* <span data-ttu-id="6b717-114">GetById</span><span class="sxs-lookup"><span data-stu-id="6b717-114">GetById</span></span>
* <span data-ttu-id="6b717-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="6b717-115">GetPage</span></span>

<span data-ttu-id="6b717-116">Hello consiste toomake de Swashbuckle tooextend générer automatiquement des ID d’opération unique.</span><span class="sxs-lookup"><span data-stu-id="6b717-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="6b717-117">Hello étapes suivantes montrent comment toocustomize Swashbuckle à l’aide de hello *SwaggerConfig.cs* fichier qui est inclus dans le projet de hello par modèle de projet Visual Studio API Apps Preview hello.</span><span class="sxs-lookup"><span data-stu-id="6b717-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="6b717-118">Vous pouvez également personnaliser Swashbuckle dans un projet d’API Web que vous configurerez pour être déployé sous la forme d’une application API.</span><span class="sxs-lookup"><span data-stu-id="6b717-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="6b717-119">Créer une implémentation `IOperationFilter` personnalisée</span><span class="sxs-lookup"><span data-stu-id="6b717-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="6b717-120">Hello `IOperationFilter` interface fournit un point d’extensibilité pour les utilisateurs Swashbuckle qui veulent toocustomize différents aspects du processus de métadonnées Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="6b717-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="6b717-121">Hello de code suivant illustre une méthode de la modification du comportement de génération d’id d’opération hello.</span><span class="sxs-lookup"><span data-stu-id="6b717-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="6b717-122">code de Hello ajoute le nom de l’id de paramètre noms toohello opération.</span><span class="sxs-lookup"><span data-stu-id="6b717-122">hello code appends parameter names toohello operation id name.</span></span>  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="6b717-123">Dans *App_Start\SwaggerConfig.cs* fichier, l’appel hello `OperationFilter` nouveau de hello de toouse du Swashbuckle toocause méthode `IOperationFilter` implémentation.</span><span class="sxs-lookup"><span data-stu-id="6b717-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="6b717-124">Hello *SwaggerConfig.cs* fichier est supprimé par hello Swashbuckle NuGet package contient de nombreux exemples commenté de points d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="6b717-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="6b717-125">les commentaires supplémentaires Hello ne sont pas affichés ici.</span><span class="sxs-lookup"><span data-stu-id="6b717-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="6b717-126">Après avoir apporté cette modification, votre `IOperationFilter` implémentation est utilisée et provoque une opération unique ID toobe est généré.</span><span class="sxs-lookup"><span data-stu-id="6b717-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="6b717-127">Autoriser les codes de réponse autres que 200</span><span class="sxs-lookup"><span data-stu-id="6b717-127">Allow response codes other than 200</span></span>
<span data-ttu-id="6b717-128">Par défaut, Swashbuckle part du principe qu’une réponse HTTP 200 (OK) est hello *uniquement* légitimes de réponse d’une méthode d’API Web.</span><span class="sxs-lookup"><span data-stu-id="6b717-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="6b717-129">Dans certains cas, vous souhaiterez aux tooreturn autres codes de réponse sans provoquer hello client tooraise une exception.</span><span class="sxs-lookup"><span data-stu-id="6b717-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="6b717-130">Par exemple, hello Web API code suivant montre un scénario dans lequel vous souhaiteriez hello client tooaccept 200 ou une erreur 404 en guise de réponse valide.</span><span class="sxs-lookup"><span data-stu-id="6b717-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

<span data-ttu-id="6b717-131">Dans ce scénario, hello Swagger Swashbuckle génère par défaut ne spécifie qu’un seul légitime HTTP code d’état HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="6b717-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="6b717-132">Étant donné que Visual Studio utilise hello code toogenerate de définition Swagger des API pour les clients de hello, il crée un code client qui lève une exception pour toute réponse autre que d’un HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="6b717-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="6b717-133">code Hello ci-dessous provient d’un client c# généré pour cet exemple de méthode d’API Web.</span><span class="sxs-lookup"><span data-stu-id="6b717-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

<span data-ttu-id="6b717-134">Swashbuckle fournit deux méthodes de personnalisation de la liste hello des codes de réponse HTTP attendus qu’il génère, à l’aide de commentaires XML ou hello `SwaggerResponse` attribut.</span><span class="sxs-lookup"><span data-stu-id="6b717-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="6b717-135">attribut de Hello est plus facile, mais il est uniquement disponible dans Swashbuckle 5.1.5 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6b717-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="6b717-136">Hello applications API aperçu nouveau projet de Visual Studio 2013 comprend Swashbuckle version 5.0.0, donc si vous utilisé hello modèle et que vous ne souhaitez pas tooupdate Swashbuckle, votre seule option toouse des commentaires XML.</span><span class="sxs-lookup"><span data-stu-id="6b717-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="6b717-137">Personnaliser les codes de réponse attendue à l'aide de commentaires XML</span><span class="sxs-lookup"><span data-stu-id="6b717-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="6b717-138">Utilisez les codes de réponse de toospecify de cette méthode si votre version de Swashbuckle est antérieure à 5.1.5.</span><span class="sxs-lookup"><span data-stu-id="6b717-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="6b717-139">Tout d’abord, ajouter des commentaires de documentation XML par rapport aux méthodes hello pour que vous souhaitez toospecify les codes de réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b717-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="6b717-140">Prend l’action d’API Web exemple hello tooit de documentation XML illustré ci-dessus et application hello entraînerait le code comme hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="6b717-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. <span data-ttu-id="6b717-141">Ajouter des instructions Bonjour *SwaggerConfig.cs* toodirect Swashbuckle toomake utilisation du fichier de documentation XML hello du fichier.</span><span class="sxs-lookup"><span data-stu-id="6b717-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="6b717-142">Ouvrez *SwaggerConfig.cs* et créer une méthode sur hello *SwaggerConfig* fichier XML de la documentation toohello de classe toospecify hello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="6b717-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="6b717-143">Faites défiler hello *SwaggerConfig.cs* fichier jusqu'à ce que vous voyez la ligne de commentaire hello du code qui ressemble à hello capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6b717-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="6b717-144">Supprimez les commentaires de commentaires XML hello ligne tooenable hello du traitement au cours de la génération de Swagger.</span><span class="sxs-lookup"><span data-stu-id="6b717-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="6b717-145">Dans le fichier de documentation XML ordre toogenerate hello, dans les propriétés du projet hello, activez le fichier de documentation XML hello comme indiqué dans la capture d’écran hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6b717-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="6b717-146">Une fois que vous effectuez ces étapes, hello JSON Swagger généré par Swashbuckle reflètent les codes de réponse HTTP hello que vous avez spécifié dans les commentaires XML hello.</span><span class="sxs-lookup"><span data-stu-id="6b717-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="6b717-147">capture d’écran Hello ci-dessous illustre cette nouvelle charge JSON.</span><span class="sxs-lookup"><span data-stu-id="6b717-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="6b717-148">Lorsque vous utilisez le code de Visual Studio tooregenerate hello client pour votre API REST, hello code c# accepte les deux codes d’état HTTP OK et introuvable hello sans lever d’exception, ce qui permet de vos décisions de toomake beaucoup de code sur la façon dont toohandle hello de retour d’une valeur null Enregistrement de contact.</span><span class="sxs-lookup"><span data-stu-id="6b717-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

<span data-ttu-id="6b717-149">code Hello pour cette démonstration se trouve dans [ce référentiel GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span><span class="sxs-lookup"><span data-stu-id="6b717-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="6b717-150">En même temps que hello Web API projet marqué avec les commentaires de documentation XML est un projet d’Application Console qui contient un client généré pour cette API.</span><span class="sxs-lookup"><span data-stu-id="6b717-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="6b717-151">Personnaliser les codes de réponse attendue à l’aide des attributs de SwaggerResponse hello</span><span class="sxs-lookup"><span data-stu-id="6b717-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="6b717-152">Hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribut est disponible dans Swashbuckle 5.1.5 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="6b717-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="6b717-153">Au cas où vous avez une version antérieure de votre projet, cette section explique tout d’abord comment tooupdate hello Swashbuckle NuGet package afin que vous pouvez utiliser cet attribut.</span><span class="sxs-lookup"><span data-stu-id="6b717-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="6b717-154">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet d’API Web, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6b717-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="6b717-155">Cliquez sur hello *mise à jour* toohello suivant du bouton *Swashbuckle* package NuGet.</span><span class="sxs-lookup"><span data-stu-id="6b717-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="6b717-156">Ajouter hello *SwaggerResponse* attributs des méthodes d’action toohello API Web pour lesquels vous souhaitez toospecify les codes de réponse HTTP valides.</span><span class="sxs-lookup"><span data-stu-id="6b717-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. <span data-ttu-id="6b717-157">Ajouter un `using` instruction pour l’espace de noms de l’attribut hello :</span><span class="sxs-lookup"><span data-stu-id="6b717-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="6b717-158">Parcourir toohello */swagger/docs/v1* URL de votre projet et le hello différents codes de réponse HTTP sera visibles dans hello Swagger de JSON.</span><span class="sxs-lookup"><span data-stu-id="6b717-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="6b717-159">code Hello pour cette démonstration se trouve dans [ce référentiel GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span><span class="sxs-lookup"><span data-stu-id="6b717-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="6b717-160">En même temps que hello projet d’API Web décorée avec hello *SwaggerResponse* attribut est un projet d’Application Console qui contient un client généré pour cette API.</span><span class="sxs-lookup"><span data-stu-id="6b717-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6b717-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b717-161">Next steps</span></span>
<span data-ttu-id="6b717-162">Cet article a montré comment moyen de hello toocustomize Swashbuckle génère l’ID d’opération et les codes de réponse valide.</span><span class="sxs-lookup"><span data-stu-id="6b717-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="6b717-163">Pour plus d’informations, consultez [Swashbuckle sur GitHub](https://github.com/domaindrivendev/Swashbuckle).</span><span class="sxs-lookup"><span data-stu-id="6b717-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

