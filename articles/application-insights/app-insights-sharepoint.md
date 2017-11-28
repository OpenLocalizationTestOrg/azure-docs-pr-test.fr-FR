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
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="6594d-103">Surveillance d’un site SharePoint avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="6594d-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="6594d-104">Azure Application Insights hello contrôle la disponibilité, performances et l’utilisation de vos applications.</span><span class="sxs-lookup"><span data-stu-id="6594d-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="6594d-105">Ici, vous allez apprendre comment tooset pour un site SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6594d-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="6594d-106">Création d’une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="6594d-106">Create an Application Insights resource</span></span>
<span data-ttu-id="6594d-107">Bonjour [portail Azure](https://portal.azure.com), créez une ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6594d-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="6594d-108">Choisissez ASP.NET en tant que type de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6594d-108">Choose ASP.NET as hello application type.</span></span>

![Cliquez sur Propriétés, sélectionnez la clé de hello et appuyez sur ctrl + C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="6594d-110">panneau Hello qui s’ouvre est place hello où vous pouvez afficher des données d’utilisation et performances sur votre application.</span><span class="sxs-lookup"><span data-stu-id="6594d-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="6594d-111">tooit de retour tooget prochaine que connexion tooAzure, vous devez rechercher une vignette pour qu’il sur l’écran d’accueil hello.</span><span class="sxs-lookup"><span data-stu-id="6594d-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="6594d-112">Vous pouvez également cliquez sur Parcourir toofind il.</span><span class="sxs-lookup"><span data-stu-id="6594d-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="6594d-113">Ajouter notre script tooyour des pages web</span><span class="sxs-lookup"><span data-stu-id="6594d-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="6594d-114">Dans le démarrage rapide, obtenir le script de hello pour les pages web :</span><span class="sxs-lookup"><span data-stu-id="6594d-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="6594d-115">Insérer un script hello juste avant hello &lt;/head&gt; balise de chaque page, vous souhaitez tootrack.</span><span class="sxs-lookup"><span data-stu-id="6594d-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="6594d-116">Si votre site Web dispose d’une page maître, vous pouvez placer les script hello il.</span><span class="sxs-lookup"><span data-stu-id="6594d-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="6594d-117">Par exemple, dans un projet ASP.NET MVC, vous placeriez le script dans View\Shared\_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="6594d-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="6594d-118">script de Hello contient la clé d’instrumentation hello qui dirige la ressource d’Application Insights hello télémétrie tooyour.</span><span class="sxs-lookup"><span data-stu-id="6594d-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="6594d-119">Ajouter les pages du site hello code tooyour</span><span class="sxs-lookup"><span data-stu-id="6594d-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="6594d-120">Sur la page maître de hello</span><span class="sxs-lookup"><span data-stu-id="6594d-120">On hello master page</span></span>
<span data-ttu-id="6594d-121">Si vous pouvez modifier la page maître du site hello, qui permettront aucune analyse pour chaque page dans le site de hello.</span><span class="sxs-lookup"><span data-stu-id="6594d-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="6594d-122">Extraire la page maître de hello et modifier à l’aide de SharePoint Designer ou un autre éditeur.</span><span class="sxs-lookup"><span data-stu-id="6594d-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="6594d-123">Ajoutez le code hello juste avant hello </head> balise.</span><span class="sxs-lookup"><span data-stu-id="6594d-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="6594d-124">Ou sur des pages individuelles</span><span class="sxs-lookup"><span data-stu-id="6594d-124">Or on individual pages</span></span>
<span data-ttu-id="6594d-125">toomonitor un ensemble limité de pages, ajouter un script de hello séparément tooeach page.</span><span class="sxs-lookup"><span data-stu-id="6594d-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="6594d-126">Insérer un composant WebPart et incorporer l’extrait de code hello qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="6594d-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="6594d-127">Affichage des données relatives à votre application</span><span class="sxs-lookup"><span data-stu-id="6594d-127">View data about your app</span></span>
<span data-ttu-id="6594d-128">Redéployez votre application.</span><span class="sxs-lookup"><span data-stu-id="6594d-128">Redeploy your app.</span></span>

<span data-ttu-id="6594d-129">Panneau des applications tooyour retour Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6594d-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="6594d-130">événements de première Hello s’affichent dans la recherche.</span><span class="sxs-lookup"><span data-stu-id="6594d-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="6594d-131">Après quelques secondes, cliquez sur Actualiser pour obtenir des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6594d-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="6594d-132">Dans le panneau de vue d’ensemble de hello, cliquez sur **analytique de l’utilisation** toocharts toosee d’utilisateurs, les sessions et les vues de page :</span><span class="sxs-lookup"><span data-stu-id="6594d-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="6594d-133">Cliquez sur n’importe quel toosee graphique plus de détails - par exemple les vues de Page :</span><span class="sxs-lookup"><span data-stu-id="6594d-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="6594d-134">Ou bien Utilisateurs :</span><span class="sxs-lookup"><span data-stu-id="6594d-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="6594d-135">Capture des ID d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6594d-135">Capturing User Id</span></span>
<span data-ttu-id="6594d-136">extrait de code de page web standard Hello ne capture pas le nom d’utilisateur hello à partir de SharePoint, mais vous pouvez le faire avec une petite modification.</span><span class="sxs-lookup"><span data-stu-id="6594d-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="6594d-137">Copiez hello Essentials liste déroulante dans Application Insights clé d’instrumentation de votre application.</span><span class="sxs-lookup"><span data-stu-id="6594d-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="6594d-138">Remplacez par clé d’instrumentation hello « XXXX » dans l’extrait de code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6594d-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="6594d-139">Incorporez un script de hello dans votre application SharePoint au lieu de l’extrait de code hello que vous obtenez à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="6594d-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="6594d-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6594d-140">Next Steps</span></span>
* <span data-ttu-id="6594d-141">[Tests Web](app-insights-monitor-web-app-availability.md) disponibilité de hello toomonitor de votre site.</span><span class="sxs-lookup"><span data-stu-id="6594d-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="6594d-142">[Application Insights](app-insights-overview.md) pour les autres types d'applications.</span><span class="sxs-lookup"><span data-stu-id="6594d-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


