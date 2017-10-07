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
# <a name="customize-swashbuckle-generated-api-definitions"></a>Personnaliser des définitions d’API générées par Swashbuckle
## <a name="overview"></a>Vue d'ensemble
Cet article explique comment toocustomize Swashbuckle toohandle scénarios courants que vous deviez tooalter hello le comportement par défaut :

* Swashbuckle génère des identificateurs d'opération en double pour les surcharges des méthodes de contrôleur.
* Swashbuckle part du principe que hello uniquement une réponse valide à partir d’une méthode est HTTP 200 (OK) 

## <a name="customize-operation-identifier-generation"></a>Personnaliser la génération d'identificateurs d'opération
Swashbuckle génère des identificateurs d’opération Swagger en concaténant le nom du contrôleur et le nom de la méthode. Ce modèle crée un problème lorsque vous avez plusieurs surcharges pour une méthode : Swashbuckle génère les ID d’opération en double, ce qui est incompatible avec le format Swagger JSON.

Par exemple, hello suivant le code du contrôleur, Swashbuckle toogenerate ID d’opération Contact_Get trois.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

Vous pouvez résoudre le problème de hello manuellement en fournissant des méthodes de hello des noms uniques, tels que les suivants hello pour cet exemple :

* Obtenir
* GetById
* GetPage

Hello consiste toomake de Swashbuckle tooextend générer automatiquement des ID d’opération unique.

Hello étapes suivantes montrent comment toocustomize Swashbuckle à l’aide de hello *SwaggerConfig.cs* fichier qui est inclus dans le projet de hello par modèle de projet Visual Studio API Apps Preview hello.  Vous pouvez également personnaliser Swashbuckle dans un projet d’API Web que vous configurerez pour être déployé sous la forme d’une application API.

1. Créer une implémentation `IOperationFilter` personnalisée 
   
    Hello `IOperationFilter` interface fournit un point d’extensibilité pour les utilisateurs Swashbuckle qui veulent toocustomize différents aspects du processus de métadonnées Swagger hello. Hello de code suivant illustre une méthode de la modification du comportement de génération d’id d’opération hello. code de Hello ajoute le nom de l’id de paramètre noms toohello opération.  
   
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
2. Dans *App_Start\SwaggerConfig.cs* fichier, l’appel hello `OperationFilter` nouveau de hello de toouse du Swashbuckle toocause méthode `IOperationFilter` implémentation.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    Hello *SwaggerConfig.cs* fichier est supprimé par hello Swashbuckle NuGet package contient de nombreux exemples commenté de points d’extensibilité. les commentaires supplémentaires Hello ne sont pas affichés ici. 
   
    Après avoir apporté cette modification, votre `IOperationFilter` implémentation est utilisée et provoque une opération unique ID toobe est généré.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Autoriser les codes de réponse autres que 200
Par défaut, Swashbuckle part du principe qu’une réponse HTTP 200 (OK) est hello *uniquement* légitimes de réponse d’une méthode d’API Web. Dans certains cas, vous souhaiterez aux tooreturn autres codes de réponse sans provoquer hello client tooraise une exception.  Par exemple, hello Web API code suivant montre un scénario dans lequel vous souhaiteriez hello client tooaccept 200 ou une erreur 404 en guise de réponse valide.

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

Dans ce scénario, hello Swagger Swashbuckle génère par défaut ne spécifie qu’un seul légitime HTTP code d’état HTTP 200.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Étant donné que Visual Studio utilise hello code toogenerate de définition Swagger des API pour les clients de hello, il crée un code client qui lève une exception pour toute réponse autre que d’un HTTP 200. code Hello ci-dessous provient d’un client c# généré pour cet exemple de méthode d’API Web.

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

Swashbuckle fournit deux méthodes de personnalisation de la liste hello des codes de réponse HTTP attendus qu’il génère, à l’aide de commentaires XML ou hello `SwaggerResponse` attribut. attribut de Hello est plus facile, mais il est uniquement disponible dans Swashbuckle 5.1.5 ou version ultérieure. Hello applications API aperçu nouveau projet de Visual Studio 2013 comprend Swashbuckle version 5.0.0, donc si vous utilisé hello modèle et que vous ne souhaitez pas tooupdate Swashbuckle, votre seule option toouse des commentaires XML. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Personnaliser les codes de réponse attendue à l'aide de commentaires XML
Utilisez les codes de réponse de toospecify de cette méthode si votre version de Swashbuckle est antérieure à 5.1.5.

1. Tout d’abord, ajouter des commentaires de documentation XML par rapport aux méthodes hello pour que vous souhaitez toospecify les codes de réponse HTTP. Prend l’action d’API Web exemple hello tooit de documentation XML illustré ci-dessus et application hello entraînerait le code comme hello l’exemple suivant. 
   
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
2. Ajouter des instructions Bonjour *SwaggerConfig.cs* toodirect Swashbuckle toomake utilisation du fichier de documentation XML hello du fichier.
   
   * Ouvrez *SwaggerConfig.cs* et créer une méthode sur hello *SwaggerConfig* fichier XML de la documentation toohello de classe toospecify hello chemin d’accès. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Faites défiler hello *SwaggerConfig.cs* fichier jusqu'à ce que vous voyez la ligne de commentaire hello du code qui ressemble à hello capture d’écran ci-dessous. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Supprimez les commentaires de commentaires XML hello ligne tooenable hello du traitement au cours de la génération de Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. Dans le fichier de documentation XML ordre toogenerate hello, dans les propriétés du projet hello, activez le fichier de documentation XML hello comme indiqué dans la capture d’écran hello ci-dessous. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Une fois que vous effectuez ces étapes, hello JSON Swagger généré par Swashbuckle reflètent les codes de réponse HTTP hello que vous avez spécifié dans les commentaires XML hello. capture d’écran Hello ci-dessous illustre cette nouvelle charge JSON. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Lorsque vous utilisez le code de Visual Studio tooregenerate hello client pour votre API REST, hello code c# accepte les deux codes d’état HTTP OK et introuvable hello sans lever d’exception, ce qui permet de vos décisions de toomake beaucoup de code sur la façon dont toohandle hello de retour d’une valeur null Enregistrement de contact. 

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

code Hello pour cette démonstration se trouve dans [ce référentiel GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). En même temps que hello Web API projet marqué avec les commentaires de documentation XML est un projet d’Application Console qui contient un client généré pour cette API. 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>Personnaliser les codes de réponse attendue à l’aide des attributs de SwaggerResponse hello
Hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribut est disponible dans Swashbuckle 5.1.5 et versions ultérieures. Au cas où vous avez une version antérieure de votre projet, cette section explique tout d’abord comment tooupdate hello Swashbuckle NuGet package afin que vous pouvez utiliser cet attribut.

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet d’API Web, puis sélectionnez **Gérer les packages NuGet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Cliquez sur hello *mise à jour* toohello suivant du bouton *Swashbuckle* package NuGet. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Ajouter hello *SwaggerResponse* attributs des méthodes d’action toohello API Web pour lesquels vous souhaitez toospecify les codes de réponse HTTP valides. 
   
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
4. Ajouter un `using` instruction pour l’espace de noms de l’attribut hello :
   
        using Swashbuckle.Swagger.Annotations;
5. Parcourir toohello */swagger/docs/v1* URL de votre projet et le hello différents codes de réponse HTTP sera visibles dans hello Swagger de JSON. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

code Hello pour cette démonstration se trouve dans [ce référentiel GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). En même temps que hello projet d’API Web décorée avec hello *SwaggerResponse* attribut est un projet d’Application Console qui contient un client généré pour cette API. 

## <a name="next-steps"></a>Étapes suivantes
Cet article a montré comment moyen de hello toocustomize Swashbuckle génère l’ID d’opération et les codes de réponse valide. Pour plus d’informations, consultez [Swashbuckle sur GitHub](https://github.com/domaindrivendev/Swashbuckle).

