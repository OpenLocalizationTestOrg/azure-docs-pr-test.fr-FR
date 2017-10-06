---
title: aaaMonitor un site SharePoint avec Application Insights
description: "Démarrage de la surveillance d'une nouvelle application avec une nouvelle clé d'instrumentation"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Surveillance d’un site SharePoint avec Application Insights
Azure Application Insights hello contrôle la disponibilité, performances et l’utilisation de vos applications. Ici, vous allez apprendre comment tooset pour un site SharePoint.

## <a name="create-an-application-insights-resource"></a>Création d’une ressource Application Insights dans Azure
Bonjour [portail Azure](https://portal.azure.com), créez une ressource Application Insights. Choisissez ASP.NET en tant que type de l’application hello.

![Cliquez sur Propriétés, sélectionnez la clé de hello et appuyez sur ctrl + C](./media/app-insights-sharepoint/01-new.png)

panneau Hello qui s’ouvre est place hello où vous pouvez afficher des données d’utilisation et performances sur votre application. tooit de retour tooget prochaine que connexion tooAzure, vous devez rechercher une vignette pour qu’il sur l’écran d’accueil hello. Vous pouvez également cliquez sur Parcourir toofind il.

## <a name="add-our-script-tooyour-web-pages"></a>Ajouter notre script tooyour des pages web
Dans le démarrage rapide, obtenir le script de hello pour les pages web :

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Insérer un script hello juste avant hello &lt;/head&gt; balise de chaque page, vous souhaitez tootrack. Si votre site Web dispose d’une page maître, vous pouvez placer les script hello il. Par exemple, dans un projet ASP.NET MVC, vous placeriez le script dans View\Shared\_Layout.cshtml

script de Hello contient la clé d’instrumentation hello qui dirige la ressource d’Application Insights hello télémétrie tooyour.

### <a name="add-hello-code-tooyour-site-pages"></a>Ajouter les pages du site hello code tooyour
#### <a name="on-hello-master-page"></a>Sur la page maître de hello
Si vous pouvez modifier la page maître du site hello, qui permettront aucune analyse pour chaque page dans le site de hello.

Extraire la page maître de hello et modifier à l’aide de SharePoint Designer ou un autre éditeur.

![](./media/app-insights-sharepoint/03-master.png)

Ajoutez le code hello juste avant hello </head> balise. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>Ou sur des pages individuelles
toomonitor un ensemble limité de pages, ajouter un script de hello séparément tooeach page. 

Insérer un composant WebPart et incorporer l’extrait de code hello qu’elle contient.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Affichage des données relatives à votre application
Redéployez votre application.

Panneau des applications tooyour retour Bonjour [portail Azure](https://portal.azure.com).

événements de première Hello s’affichent dans la recherche. 

![](./media/app-insights-sharepoint/09-search.png)

Après quelques secondes, cliquez sur Actualiser pour obtenir des données supplémentaires.

Dans le panneau de vue d’ensemble de hello, cliquez sur **analytique de l’utilisation** toocharts toosee d’utilisateurs, les sessions et les vues de page :

![](./media/app-insights-sharepoint/06-usage.png)

Cliquez sur n’importe quel toosee graphique plus de détails - par exemple les vues de Page :

![](./media/app-insights-sharepoint/07-pages.png)

Ou bien Utilisateurs :

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Capture des ID d’utilisateur
extrait de code de page web standard Hello ne capture pas le nom d’utilisateur hello à partir de SharePoint, mais vous pouvez le faire avec une petite modification.

1. Copiez hello Essentials liste déroulante dans Application Insights clé d’instrumentation de votre application. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Remplacez par clé d’instrumentation hello « XXXX » dans l’extrait de code hello ci-dessous. 
2. Incorporez un script de hello dans votre application SharePoint au lieu de l’extrait de code hello que vous obtenez à partir du portail de hello.

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a>Étapes suivantes
* [Tests Web](app-insights-monitor-web-app-availability.md) disponibilité de hello toomonitor de votre site.
* [Application Insights](app-insights-overview.md) pour les autres types d'applications.

<!--Link references-->


