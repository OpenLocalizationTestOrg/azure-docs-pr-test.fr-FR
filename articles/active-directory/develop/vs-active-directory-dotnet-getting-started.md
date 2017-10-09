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
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a>Prise en main d’Azure Active Directory et des services connectés de Visual Studio (projets MVC)
> [!div class="op_single_selector"]
> * [Prise en main](vs-active-directory-dotnet-getting-started.md)
> * [Que s'est-il passé ?](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>Contrôleurs de tooaccess nécessitant une authentification
Tous les contrôleurs dans votre projet ont été dotées de hello **Authorize** attribut. Cet attribut requiert hello toobe d’utilisateur authentifié avant d’accéder à ces contrôleurs. tooallow hello contrôleur toobe accessible de manière anonyme, supprimez cet attribut à partir du contrôleur de hello. Si vous souhaitez que les autorisations de hello tooset à un niveau plus granulaire, appliquer hello attribut tooeach méthode qui nécessite une autorisation au lieu de la classe de contrôleur toohello son application.

## <a name="adding-signin--signout-controls"></a>Ajouter des contrôles SignIn/SignOut
tooadd hello SignIn/SignOut contrôle tooyour vue, vous pouvez utiliser hello **_LoginPartial.cshtml** vue partielle tooadd hello fonctionnalité tooone de vos affichages. Voici un exemple de la norme de hello fonctionnalité ajoutée toohello **_Layout.cshtml** vue. (Notez hello dernier élément div hello avec barre de navigation de classe / réduction) :

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

## <a name="next-steps"></a>Étapes suivantes
- [En savoir plus sur Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 

