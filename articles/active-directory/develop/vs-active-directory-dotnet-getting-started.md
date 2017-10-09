---
title: "aaaGet démarré avec Azure AD dans les projets Visual Studio MVC | Documents Microsoft"
description: "Comment tooget démarrer à l’aide d’Azure Active Directory dans les projets MVC après la connexion tooor création d’un répertoire Azure AD à l’aide de Visual Studio services connectés"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 807824dd6e4e57e443f8a7322cf2e5326384316d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a><span data-ttu-id="27cc1-103">Prise en main d’Azure Active Directory et des services connectés de Visual Studio (projets MVC)</span><span class="sxs-lookup"><span data-stu-id="27cc1-103">Getting Started with Azure Active Directory and Visual Studio connected services (MVC Projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27cc1-104">Prise en main</span><span class="sxs-lookup"><span data-stu-id="27cc1-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="27cc1-105">Que s'est-il passé ?</span><span class="sxs-lookup"><span data-stu-id="27cc1-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a><span data-ttu-id="27cc1-106">Contrôleurs de tooaccess nécessitant une authentification</span><span class="sxs-lookup"><span data-stu-id="27cc1-106">Requiring authentication tooaccess controllers</span></span>
<span data-ttu-id="27cc1-107">Tous les contrôleurs dans votre projet ont été dotées de hello **Authorize** attribut.</span><span class="sxs-lookup"><span data-stu-id="27cc1-107">All controllers in your project were adorned with hello **Authorize** attribute.</span></span> <span data-ttu-id="27cc1-108">Cet attribut requiert hello toobe d’utilisateur authentifié avant d’accéder à ces contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="27cc1-108">This attribute requires hello user toobe authenticated before accessing these controllers.</span></span> <span data-ttu-id="27cc1-109">tooallow hello contrôleur toobe accessible de manière anonyme, supprimez cet attribut à partir du contrôleur de hello.</span><span class="sxs-lookup"><span data-stu-id="27cc1-109">tooallow hello controller toobe accessed anonymously, remove this attribute from hello controller.</span></span> <span data-ttu-id="27cc1-110">Si vous souhaitez que les autorisations de hello tooset à un niveau plus granulaire, appliquer hello attribut tooeach méthode qui nécessite une autorisation au lieu de la classe de contrôleur toohello son application.</span><span class="sxs-lookup"><span data-stu-id="27cc1-110">If you want tooset hello permissions at a more granular level, apply hello attribute tooeach method that requires authorization instead of applying it toohello controller class.</span></span>

## <a name="adding-signin--signout-controls"></a><span data-ttu-id="27cc1-111">Ajouter des contrôles SignIn/SignOut</span><span class="sxs-lookup"><span data-stu-id="27cc1-111">Adding SignIn / SignOut Controls</span></span>
<span data-ttu-id="27cc1-112">tooadd hello SignIn/SignOut contrôle tooyour vue, vous pouvez utiliser hello **_LoginPartial.cshtml** vue partielle tooadd hello fonctionnalité tooone de vos affichages.</span><span class="sxs-lookup"><span data-stu-id="27cc1-112">tooadd hello SignIn/SignOut controls tooyour view, you can use hello **_LoginPartial.cshtml** partial view tooadd hello functionality tooone of your views.</span></span> <span data-ttu-id="27cc1-113">Voici un exemple de la norme de hello fonctionnalité ajoutée toohello **_Layout.cshtml** vue.</span><span class="sxs-lookup"><span data-stu-id="27cc1-113">Here is an example of hello functionality added toohello standard **_Layout.cshtml** view.</span></span> <span data-ttu-id="27cc1-114">(Notez hello dernier élément div hello avec barre de navigation de classe / réduction) :</span><span class="sxs-lookup"><span data-stu-id="27cc1-114">(Note hello last element in hello div with class navbar-collapse):</span></span>

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a><span data-ttu-id="27cc1-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27cc1-115">Next steps</span></span>
- [<span data-ttu-id="27cc1-116">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27cc1-116">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/) 

