---
title: aaaDiagnose erreurs et exceptions dans les applications avec Azure Application Insights web | Documents Microsoft
description: "Capturez des exceptions à partir d’applications ASP.NET, ainsi que des données de télémétrie des demandes."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Diagnostiquez les exceptions dans vos applications web avec Application Insights
Les exceptions dans votre application web dynamique sont signalées par [Application Insights](app-insights-overview.md). Vous pouvez associer des demandes ayant échoué avec les exceptions et d’autres événements à hello client et le serveur, afin que vous puissiez diagnostiquer rapidement hello causes.

## <a name="set-up-exception-reporting"></a>Configurer les rapports d’exceptions
* exceptions toohave signalées à partir de votre application de serveur :
  * Installez le [SDK Application Insights](app-insights-asp-net.md) dans votre code d’application, ou
  * Serveurs web IIS : exécutez l’[Agent Application Insights](app-insights-monitor-performance-live-website-now.md) ; ou
  * Les applications web Azure : ajouter hello [Extension Application Insights](app-insights-azure-web-apps.md)
  * Applications web Java : installation hello [agent Java](app-insights-java-agent.md)
* Installer hello [extrait de code JavaScript](app-insights-javascript.md) dans vos pages web toocatch les exceptions du navigateur.
* Dans certaines infrastructures d’application ou avec des paramètres, vous devez tootake toocatch de certaines étapes supplémentaires plus des exceptions :
  * [Web forms](#web-forms)
  * [MVC](#mvc)
  * [API web 1.*](#web-api-1)
  * [API web 2.*](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Diagnostic des exceptions à l’aide de Visual Studio
Ouvrez la solution d’application hello dans toohelp Visual Studio avec le débogage.

Exécutez l’application hello, sur votre serveur ou sur votre ordinateur de développement à l’aide de F5.

Ouvrez la fenêtre de recherche Application Insights hello dans Visual Studio et la définir toodisplay événements à partir de votre application. Pendant que vous déboguez, faire cela suffit de cliquer sur le bouton d’Application Insights hello.

![Droit hello projet, puis choisissez Application Insights, ouvrir.](./media/app-insights-asp-net-exceptions/34.png)

Notez que vous pouvez filtrer les exceptions simplement hello rapport tooshow.

*Aucune exception ne s’affiche ? Consultez [Capture des exceptions](#exceptions)* 

Cliquez sur un tooshow de rapport d’exception de trace de la pile.
Cliquez sur une référence de ligne dans la trace de la pile hello, fichier de code approprié tooopen hello.  

Dans le code hello, notez que CodeLens affiche les données sur les exceptions hello :

![Notification CodeLens des exceptions.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>Diagnostiquer les défaillances à l’aide de hello portail Azure
Vue d’ensemble d’Application Insights hello de votre application, vignette de défaillances hello vous montre des graphiques des exceptions et les demandes HTTP ayant échoué, ainsi que la liste de hello URL de la requête qui provoquent des échecs de hello plus fréquentes.

![Sélectionnez Paramètres, Défaillances](./media/app-insights-asp-net-exceptions/012-start.png)

Cliquez sur un des hello Échec de types d’exceptions dans les occurrences de tooindividual tooget hello liste d’exception hello, où vous pouvez afficher les détails de hello et trace de la pile :

![Sélectionnez une instance de la demande a échoué et sous Détails de l’exception, obtenir tooinstances d’exception de hello.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**Vous pouvez également** vous pouvez démarrer à partir de la liste des demandes hello et trouver tooit connexes d’exceptions.

*Aucune exception ne s’affiche ? Consultez [Capture des exceptions](#exceptions)* 


## <a name="custom-tracing-and-log-data"></a>Suivi personnalisé et données du journal
application de tooyour spécifique de données de diagnostic tooget, vous pouvez insérer un code toosend vos propres données de télémétrie. Cela est affiché dans la recherche de diagnostic en même temps que la demande de hello, affichage de page et autres données automatiquement collectées.

Vous disposez de plusieurs options :

* [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) est généralement utilisé pour l’analyse des tendances d’utilisation, mais il envoie également des données s’affiche sous les événements personnalisés dans la recherche de diagnostic de hello. Les événements sont nommés et peuvent contenir des propriétés de type chaîne et des métriques numériques sur lesquels vous pouvez [filtrer vos recherches de diagnostic](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) vous permet d’envoyer des données plus longues telles que des informations POST.
* [TrackException()](#exceptions) envoie des arborescences des appels de procédure. [Plus d’informations sur les exceptions](#exceptions).
* Si vous utilisez déjà un framework de journalisation comme Log4Net ou NLog, vous pouvez [capturer ces journaux](app-insights-asp-net-trace-logs.md) et les visualiser dans Recherche de diagnostic avec les données sur les demandes et les exceptions.

Ouvrez de ces événements, toosee [recherche](app-insights-diagnostic-search.md), ouvrez le filtre, puis choisissez Custom Event, de Trace ou d’Exception.

![Extraire](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Si votre application génère un grand nombre de télémétrie, module d’échantillonnage adaptive hello réduira automatiquement volume hello envoyé toohello portail en envoyant qu’une fraction représentative d’événements. Les événements qui font partie de hello même opération sera sélectionnée ou désélectionnée en tant que groupe, afin que vous pouvez naviguer entre les événements connexes. [En savoir plus sur l'échantillonnage.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>Comment toosee demander les données de publication
Détails de la demande n’incluent pas les données hello envoyées tooyour application dans un appel POST. toohave signalés par ces données :

* [Installer hello SDK](app-insights-asp-net.md) dans votre projet d’application.
* Insérez le code de votre application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Envoyer les données de publication hello dans le paramètre de message hello. Est une limite de taille toohello autorisée, donc vous devez essayer des données essentielles toosend simplement hello.
* Lorsque vous examinez une demande ayant échoué, recherchez les traces hello associé.  

![Extraire](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> Capture des exceptions et des données de diagnostic connexes
Dans un premier temps, vous ne voyez dans le portail de hello toutes les exceptions hello entraînent l’échec de votre application. Vous verrez toutes les exceptions du navigateur (si vous utilisez hello [SDK JavaScript](app-insights-javascript.md) dans vos pages web). Mais la plupart des exceptions de serveur sont interceptées par IIS et que vous avez toowrite un peu de code toosee les.

Vous pouvez :

* **Enregistrer les exceptions explicitement** en insérant le code dans les exceptions de hello tooreport exception gestionnaires.
* **Capturer automatiquement des exceptions** en configurant votre infrastructure ASP.NET. les ajouts nécessaires Hello sont différents pour différents types de framework.

## <a name="reporting-exceptions-explicitly"></a>Signalisation explicite des exceptions
Bonjour façon la plus simple est tooinsert un appel tooTrackException() dans un gestionnaire d’exceptions.

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Hello les mesures et les propriétés de paramètres sont facultatifs, mais sont utiles pour [le filtrage et l’ajout de](app-insights-diagnostic-search.md) des informations supplémentaires. Par exemple, si vous avez une application qui peut exécuter plusieurs jeux, vous pouvez rechercher tous les hello exception rapports connexes tooa jeu particulier. Vous pouvez ajouter autant d’éléments que vous comme tooeach dictionnaire.

## <a name="browser-exceptions"></a>Exceptions du navigateur
La plupart des exceptions de navigateur sont signalées.

Si votre page web inclut des fichiers de script à partir des réseaux de diffusion de contenu ou d’autres domaines, vérifiez votre balise de script a l’attribut de hello ```crossorigin="anonymous"```, et ce serveur hello envoie [en-têtes CORS](http://enable-cors.org/). Cela vous permettra de tooget une trace de pile et les détails des exceptions JavaScript non gérées à partir de ces ressources.

## <a name="web-forms"></a>Formulaires web
Pour web forms, hello HTTP Module sera toocollect en mesure des exceptions hello lorsqu’il n’y a aucuns configurée avec CustomErrors de redirection.

Toutefois, si vous avez des redirections actives, ajouter hello suivant lignes toohello Application_Error fonction dans Global.asax.cs. (Ajouter un fichier Global.asax si vous n'en avez pas déjà).

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
Si hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration est `Off`, exceptions seront alors disponibles pour hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect. Toutefois, si elle est `RemoteOnly` (valeur par défaut), ou `On`, puis hello est désactivée et non disponible pour l’Application Insights tooautomatically collecter. Vous pouvez résoudre cela en substituant hello [System.Web.Mvc.HandleErrorAttribute classe](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)et en appliquant la classe hello substitué comme indiqué pour les versions MVC hello différents ci-dessous ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)) :

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Remplacer l’attribut de HandleError de hello avec votre nouvel attribut sur vos contrôleurs.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[Exemple](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Enregistrez `AiHandleErrorAttribute` en tant que filtre global dans Global.asax.cs :

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[Exemple](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC 5
Enregistrez AiHandleErrorAttribute en tant que filtre global dans FilterConfig.cs :

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[Exemple](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>API Web 1.x
Remplacez System.Web.Http.Filters.ExceptionFilterAttribute :

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

Vous pourriez ajouter ce contrôleurs de toospecific attribut substituée ou ajouter de configuration de filtres globaux toohello dans la classe WebApiConfig de hello :

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[Exemple](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Il existe un nombre de cas qui ne peut pas gérer les filtres d’exception hello. Par exemple :

* Les exceptions lancées à partir des constructeurs de contrôleur.
* Les exceptions lancées à partir des gestionnaires de messages.
* Les exceptions lancées pendant le routage.
* Les exceptions lancées pendant la sérialisation du contenu de réponse.

## <a name="web-api-2x"></a>API Web 2.x
Ajoutez d'une implémentation de IExceptionLogger :

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

Ajoutez ce service toohello dans WebApiConfig :

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[Exemple](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

Alternativement, vous pouvez :

1. Remplacez hello uniquement ExceptionHandler avec une implémentation personnalisée de IExceptionHandler. Cela est uniquement appelée lorsque l’infrastructure hello est toujours en mesure de toochoose la réponse de message toosend (et non pas au moment de la connexion de hello est abandonnée pour l’instance)
2. Filtres d’exception (comme décrit dans la section hello sur les contrôleurs de 1.x API Web ci-dessus) - ne pas appelées dans tous les cas.

## <a name="wcf"></a>WCF
Ajoutez une classe qui étend l'attribut et implémente IErrorHandler et IServiceBehavior.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Ajoutez les implémentations de service toohello hello attribut :

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Exemple](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Compteurs de performance des exceptions
Si vous avez [installé hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) sur votre serveur, vous pouvez obtenir un graphique du taux d’exceptions hello, mesurée par .NET. Celui-ci comprend les exceptions .NET gérées et non gérées.

Ouvrez un panneau d'explorateur de mesures, ajoutez un nouveau graphique, puis sélectionnez **Taux d'exception**sous Compteurs de performances.

.NET framework de Hello calcule le taux de hello en comptant le nombre hello d’exceptions dans un intervalle et en divisant par la longueur de l’intervalle de salutation hello.

Notez qu’il sera différent de nombre hello « Exceptions » calculé par le portail Application Insights de hello à partir des rapports de TrackException. intervalles d’échantillonnage de Hello sont différentes, et hello SDK n’envoie pas de rapports TrackException pour toutes les exceptions gérées et non gérées.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>Étapes suivantes
* [Surveiller le reste, SQL et autres toodependencies d’appels](app-insights-asp-net-dependencies.md)
* [Surveiller les durées de chargement des pages, les exceptions du navigateur et les appels AJAX](app-insights-javascript.md)
* [Surveiller les compteurs de performances](app-insights-performance-counters.md)
