---
title: "aaaApp API du Service application déclencheurs | Documents Microsoft"
description: "Comment tooimplement déclenche dans une application API dans Azure App Service"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a>Déclencheurs des applications API Azure App Service
> [!NOTE]
> Cette version de l’article de hello s’applique la version du schéma tooAPI applications 2014-12-01-preview.
>
>

## <a name="overview"></a>Vue d'ensemble
Cet article explique comment tooimplement API application déclenche et les consommer à partir d’une application logique.

Tous les extraits de code hello dans cette rubrique sont copiés à partir de hello [exemple de code d’application d’API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).

Notez que vous devez hello toodownload suivant du package nuget pour le code dans cet article de toobuild hello et exécutez : [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>Que sont les déclencheurs des applications API ?
Il est un scénario courant pour un toofire d’application API un événement afin que les clients de l’application d’API hello prendre les mesures appropriées de hello dans l’événement toohello de réponse. Hello mécanisme d’API REST en fonction qui prend en charge ce scénario est appelé un déclencheur d’application API.

Par exemple, supposons que votre code client à l’aide de hello [application API de connecteur Twitter](../connectors/connectors-create-api-twitter.md) et votre code doit être tooperform une action en fonction de la nouvelle tweets qui contiennent des mots spécifiques. Dans ce cas, vous pouvez configurer un toofacilitate de déclencheur d’interrogation ou de push ce besoin.

## <a name="poll-trigger-versus-push-trigger"></a>Déclencheur d'interrogation et déclencheur d'émission
Deux types de déclencheurs sont actuellement pris en charge :

* Déclencheur d’interrogation - Client interroge application d’API hello pour la notification d’un événement a été déclenché.
* Déclencheur d’émission - Client est averti par application hello API lorsqu’un événement est déclenché

### <a name="poll-trigger"></a>Déclencheur d'interrogation :
Un déclencheur de sondage est implémenté comme une API REST régulière et attend son toopoll clients (par exemple, une application logique) dans la commande tooget notification. Pendant que le client de hello peut-être conserver l’état, le déclencheur de sondage de hello lui-même est sans état.

Hello informations concernant les paquets de demande et de réponse hello suivantes illustre certains aspects clés de contrat de déclencheur d’interrogation hello :

* Demande
  * Méthode HTTP : GET
  * Paramètres
    * triggerState - ce paramètre facultatif permet aux clients toospecify leur état afin que hello déclencheur d’interrogation peut correctement décider si tooreturn notification ou pas selon hello état spécifié.
    * Paramètres spécifiques de l'API
* Réponse
  * Code d’état **200** - demande est valide et qu’il existe une notification de déclencheur de hello. le contenu de la notification de hello Hello sera corps de réponse hello. Un en-tête « Retry-After » dans la réponse de hello indique que les données de notification supplémentaires doivent être récupérées avec un appel de la demande suivante.
  * Code d’état **202** - la demande est valide, mais il n’existe aucune nouvelle notification de déclencheur de hello.
  * Code d'état **4xx** : la demande n'est pas valide. client de Hello doit réessayer pas de demande de hello.
  * Code d'état **5xx** : la demande a entraîné une erreur de serveur interne et/ou un problème temporaire. client de Hello doit réessayer la demande de hello.

Hello suivant extrait de code est un exemple de comment déclencher des tooimplement une interrogation.

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

tootest ce sondage déclencher, procédez comme suit :

1. Déployer hello API application avec un paramètre d’authentification de **public anonyme**.
2. Appelez hello **touch** opération tootouch un fichier. Hello suivant image montre un exemple de demande via Postman.
   ![Appeler une opération Touch via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Appeler hello interrogation avec hello **triggerState** paramètre défini tooa temps horodatage préalable tooStep #2. Hello image suivante illustre demande d’exemple hello via Postman.
   ![Appeler un déclencheur d'interrogation via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Déclencheurs d'émission :
Un déclencheur d’émission est implémenté comme une réguliers API REST qui exécute un push de tooclients de notifications qui ont inscrit toobe averti lorsque des événements spécifiques se déclenchent.

Hello informations concernant les paquets de demande et de réponse hello suivantes illustre certains aspects clés de contrat de déclencheur hello par émission de données.

* Demande
  * Méthode HTTP : PUT
  * Paramètres
    * triggerId : requis - Opaque chaîne (par exemple, un GUID) que représente hello d’inscription d’un déclencheur par émission de données.
    * callbackUrl : requise : URL de hello rappel tooinvoke lors du déclenche de l’événement de hello. appel de Hello est un simple appel HTTP POST.
    * Paramètres spécifiques de l'API
* Réponse
  * Code d’état **200** -client de tooregister demande réussie.
  * Code d'état **4xx** : la demande n'est pas valide. client de Hello doit réessayer pas de demande de hello.
  * Code d'état **5xx** : la demande a entraîné une erreur de serveur interne et/ou un problème temporaire. client de Hello doit réessayer la demande de hello.
* Rappel
  * Méthode HTTP : POST
  * Corps de la demande : contenu de la notification.

Hello suivant extrait de code est un exemple de comment tooimplement push de déclencheur :

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

tootest ce sondage déclencher, procédez comme suit :

1. Déployer hello API application avec un paramètre d’authentification de **public anonyme**.
2. Parcourir trop[http://requestb.in/](http://requestb.in/) toocreate un RequestBin qui servira de votre URL de rappel.
3. Appeler le déclencheur d’émission hello avec un GUID en tant que **triggerId** et hello URL RequestBin **callbackUrl**.
   ![Appeler un déclencheur d'émission via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Appelez hello **touch** opération tootouch un fichier. Hello suivant image montre un exemple de demande via Postman.
   ![Appeler une opération Touch via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Vérifiez que hello RequestBin tooconfirm qui hello push déclencheur rappel est appelé avec la sortie de la propriété.
   ![Appeler un déclencheur d'interrogation via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Décrire des déclencheurs dans une définition d'API
Après l’implémentation de déclencheurs de hello et en déployant votre tooAzure d’application API, accédez à toohello **définition d’API** panneau dans le portail Azure en version préliminaire de hello et vous verrez que les déclencheurs sont automatiquement reconnus Bonjour interface utilisateur, qui est déterminée par les Hello définition Swagger 2.0 API de l’application hello API.

![Panneau Définition de l'API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Si vous cliquez sur hello **télécharger Swagger** bouton et le fichier JSON de hello ouvert, vous verrez toohello similaire de résultats suivant :

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

propriété d’extension de Hello **x-ms-programmation-le déclencheur** est la façon dont les déclencheurs sont décrites dans la définition de l’API et est automatiquement ajoutée par la passerelle d’application hello API lorsque vous demandez une définition hello API via une passerelle de hello hello demande tooone de Hello suivant des critères. (Vous pouvez également ajouter cette propriété manuellement.)

* Déclencheur d'interrogation :
  * Si la méthode HTTP de hello est **obtenir**.
  * Si hello **operationId** propriété contient la chaîne de hello **déclencheur**.
  * Si hello **paramètres** propriété inclut un paramètre avec un **nom** propriété trop**triggerState**.
* Déclencheurs d'émission :
  * Si la méthode HTTP de hello est **PUT**.
  * Si hello **operationId** propriété contient la chaîne de hello **déclencheur**.
  * Si hello **paramètres** propriété inclut un paramètre avec un **nom** propriété trop**triggerId**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Utiliser des déclencheurs d'application API dans les applications logiques
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Répertorier et configurer des déclencheurs d’application API dans le Concepteur d’applications hello logique
Si vous créez une application logique Bonjour même groupe de ressources que hello application API, vous serez en mesure de tooadd il canevas de concepteur toohello simplement en cliquant dessus. Hello suivant des images pour illustrer ce propos :

![Déclencheurs dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurer un déclencheur d'interrogation dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurer un déclencheur d'émission dans le concepteur d'applications logiques](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>Optimiser les déclencheurs d'application API pour les applications logiques
Après avoir ajouté des déclencheurs tooan API app, il existe quelques opérations réalisables expérience de hello tooimprove lors de l’utilisation d’application hello API dans une application logique.

Par exemple, hello **triggerState** pour les déclencheurs d’interrogation doit être défini toohello expression dans l’application logique de hello suivante. Cette expression doit évaluer hello dernière invocation du déclencheur hello à partir de l’application logique de hello et retourne cette valeur.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Remarque : Pour obtenir une explication des fonctions hello utilisé dans l’expression hello ci-dessus, consultez la documentation du toohello sur [langage de définition de flux de travail logique d’application](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Expression de hello tooprovide au-dessus de l’utilisateur d’application logique a besoin pour hello **triggerState** paramètre lors de l’utilisation de déclencheur de hello. Il est possible de toohave cette valeur prédéfinie par le Concepteur d’application hello logique via la propriété d’extension hello **x-ms-planificateur-recommandation**.  Hello **x-ms-visibilité** propriété d’extension peut être valeur tooa *interne* afin que le paramètre hello lui-même n’est pas visible sur le Concepteur de hello.  Hello suivant extrait de code illustre.

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

Pour les déclencheurs de push, hello **triggerId** paramètre doit identifier de façon unique application logique de hello. Meilleure pratique recommandée est tooset ce nom toohello de propriété de flux de travail hello à l’aide de hello l’expression suivante :

    @workflow().name

À l’aide de hello **x-ms-planificateur-recommandation** et **x-ms-visibilité** propriétés d’extension dans sa définition d’API, hello application API peuvent transmettre toohello logique application concepteur tooautomatically définie expression pour l’utilisateur de hello.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>Ajouter des propriétés d'extension dans la définition de l'API
Informations de métadonnées supplémentaires telles que les propriétés d’extension hello - **x-ms-planificateur-recommandation** et **x-ms-visibilité** -peuvent être ajoutées dans la définition de hello API dans un des deux façons : statique ou dynamique.

Pour les métadonnées statiques, vous pouvez modifier directement hello */metadata/apiDefinition.swagger.json* dans votre projet et ajouter manuellement les propriétés de hello.

Pour les applications API en utilisant les métadonnées dynamique, vous pouvez modifier hello SwaggerConfig.cs fichier tooadd un filtre d’opération qui peut ajouter ces extensions.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Hello Voici un exemple de la manière dont cette classe peut être scénario de métadonnées dynamique hello toofacilitate implémenté.

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
