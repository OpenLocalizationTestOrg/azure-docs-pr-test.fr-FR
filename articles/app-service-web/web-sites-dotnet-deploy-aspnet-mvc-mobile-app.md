---
title: "application web mobile d’aaaDeploy un ASP.NET MVC 5 dans Azure App Service"
description: "Un didacticiel vous apprend comment toodeploy un tooAzure d’application web du Service d’applications à l’aide de mobile fonctionnalités dans ASP.NET MVC 5 application web."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Déployer une application web mobile ASP.NET MVC 5 dans Azure App Service
Ce didacticiel vous hello notions de base de comment toobuild un ASP.NET MVC 5 web application adaptés aux appareils mobiles et le déployer tooAzure du Service d’applications. Pour ce didacticiel, vous devez [Visual Studio Express 2013 pour le Web] [ Visual Studio Express 2013] hello éditions ou professional de Visual Studio si vous l’avez déjà. Vous pouvez utiliser [Visual Studio 2015] mais captures d’écran hello sera différentes, et vous devez utiliser des modèles de hello ASP.NET 4.x.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>Contenu
Pour ce didacticiel, vous allez ajouter des fonctionnalités mobiles toohello annonce de conférence application simple qui est fournie dans hello [projet de démarrage][StarterProject]. Hello capture d’écran suivante montre les sessions ASP.NET hello dans hello terminée application, comme indiqué dans l’émulateur de navigateur hello dans les outils de développement Internet Explorer 11 F12.

![][FixedSessionsByTag]

Vous pouvez utiliser les outils de développement hello Internet Explorer 11 F12 et hello [outil Fiddler] [ Fiddler] toohelp déboguer votre application. 

## <a name="skills-youll-learn"></a>Compétences
Vous apprendrez les compétences suivantes :

* Comment toouse Visual Studio 2013 toopublish votre application web directement tooa web application dans Azure App Service.
* Utilisent des modèles de hello ASP.NET MVC 5 framework du programme d’amorçage CSS hello pour améliorer l’affichage sur les périphériques mobiles
* Comment toocreate mobiles spécifiques vues tootarget certains navigateurs mobiles, tels que les iPhone hello et Android
* Comment toocreate les vues réactive (vues qui répondent toodifferent navigateurs pour les appareils)

## <a name="set-up-hello-development-environment"></a>Configuration d’environnement de développement hello
Configurer votre environnement de développement en installant hello Azure SDK pour .NET 2.5.1 ou version ultérieure. 

1. tooinstall hello Azure SDK pour .NET, cliquez sur lien hello ci-dessous. Si vous n’avez pas encore installé de Visual Studio 2013, il sera installé par un lien de hello. Ce didacticiel requiert Visual Studio 2013. [Kit de développement logiciel (SDK) Azure pour Visual Studio 2013][AzureSDKVs2013]
2. Dans la fenêtre de Web Platform Installer hello, cliquez sur **installer** et poursuivre l’installation de hello.

Vous aurez également besoin d'un émulateur de navigateur mobile. Hello suivantes ne fonctionnent pas :

* Émulateur de navigateur dans les [outils de développement F12 d’Internet Explorer 11][EmulatorIE11] (utilisés dans toutes les captures d’écran de navigateurs mobiles). Il dispose de présélections de chaîne d'agent utilisateur pour Windows Phone 8, Windows Phone 7 et l'iPad d'Apple.
* Émulateur de navigateur de [Google Chrome DevTools][EmulatorChrome]. Il inclut des présélections pour de nombreux périphériques Android, ainsi que pour l'iPhone d'Apple, l'iPad d'Apple et le Kindle Fire d'Amazon. Il émule également des événements tactiles.
* [Émulateur mobile Opera][EmulatorOpera]

Les projets Visual Studio avec C\# code source est disponible tooaccompany cette rubrique :

* [Téléchargement du projet de départ][StarterProject]
* [Téléchargement du projet terminé][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Déployer le projet hello starter tooan l’application web Azure
1. Télécharger l’application de liste de conférence hello [projet de démarrage][StarterProject].
2. Dans l’Explorateur Windows, fichier ZIP de hello téléchargé avec le bouton droit, puis choisissez *propriétés*.
3. Bonjour **propriétés** boîte de dialogue, choisissez hello **Unblock** bouton. (Le déblocage empêche un avertissement de sécurité qui se produit lorsque vous essayez de toouse un *.zip* fichier que vous avez téléchargé à partir du web de hello.)
4. Cliquez sur le fichier ZIP de hello et sélectionnez **extraire tout** afin de décompresser le fichier de hello. 
5. Dans Visual Studio, ouvrez hello *C#\Mvc5Mobile.sln* fichier.
6. Dans l’Explorateur de solutions, cliquez sur projet de hello, sur **publier**.
   
   ![][DeployClickPublish]
7. Dans Publier le site web, cliquez sur **Microsoft Azure App Service**.
   
   ![][DeployClickWebSites]
8. Si vous n’êtes pas déjà connecté à Azure, cliquez sur **Ajouter un compte**.
   
   ![][DeploySignIn]
9. Suivez hello invites toolog à votre compte Azure.
10. Hello, boîte de dialogue du Service d’applications doit maintenant afficher comme connecté. Cliquez sur **Nouveau**.
    
    ![][DeployNewWebsite]  
11. Bonjour **nom de l’application Web** Indiquez un préfixe de nom d’application unique. Le nom complet de votre application web est *&lt;prefix>*.azurewebsites.net. Par ailleurs, sélectionnez ou spécifiez un nouveau nom de groupe de ressources dans **Groupe de ressources**. Ensuite, cliquez sur **nouveau** toocreate un nouveau plan de Service d’applications.
    
    ![][DeploySiteSettings]
12. Configurez le nouveau plan de Service de l’application hello, cliquez sur **OK**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. Dans la boîte de dialogue Créer un Service application hello, cliquez sur **créer**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Une fois hello ressources Azure sont créés, boîte de dialogue Publier le site Web hello est rempli avec des paramètres pour votre nouvelle application hello. Cliquez sur **Publier**.
    
    ![][DeployPublishSite]
    
    Une fois que Visual Studio a terminé l’application de publication toohello hello starter projet web Azure, navigateur de bureau hello ouvre toodisplay hello dynamique web app.
15. Démarrer l’émulateur de votre navigateur mobile, de copier l’URL de hello pour l’application de conférence hello (*<prefix>*. azurewebsites.net) dans l’émulateur de hello, puis cliquez sur le bouton droit et sélectionnez **Parcourir par balise**. Si vous utilisez Internet Explorer 11 comme navigateur par défaut de hello, vous devez simplement tootype `F12`, puis `Ctrl+8`, puis modifiez profil de navigateur hello trop**Windows Phone**. L’image ci-dessous montre hello *AllTags* affichage en mode portrait (choisisse **Parcourir par balise**).
    
    ![][AllTags]

> [!TIP]
> Pendant que vous pouvez déboguer votre application MVC 5 à partir de Visual Studio, vous pouvez publier votre tooAzure d’application web à nouveau tooverify hello web dynamique application directement à partir de votre navigateur mobile ou un émulateur de navigateur.
> 
> 

affichage de Hello est très lisible sur un appareil mobile. Vous pouvez également déjà voir certains des effets visuels de hello appliqués par le framework d’amorçage CSS hello.
Cliquez sur hello **ASP.NET** lien.

![][SessionsByTagASP.NET]

Hello vue des balises ASP.NET est ajusté de zoom de toohello écran, ce programme d’amorçage fait automatiquement pour vous. Toutefois, vous pouvez améliorer ce navigateur mobile vue toobetter couleur hello. Par exemple, hello **Date** colonne est difficile à lire. Plus loin dans le didacticiel de hello, vous allez modifier hello *AllTags* afficher toomake il adaptés aux appareils mobiles.

## <a name="bkmk_bootstrap"></a> Infrastructure CSS Bootstrap
Nouveauté de hello MVC 5 modèle est prise en charge d’amorçage intégrée. Vous avez déjà vu comment il améliore immédiatement hello différentes vues de votre application. Par exemple, barre de navigation hello haut hello est réductible automatiquement lors de la largeur du navigateur hello est plus petite. Sur le navigateur de bureau hello, essayez de redimensionner la fenêtre du navigateur hello et voir comment la barre de navigation hello modifie son apparence. Il s’agit de conception web réactive hello qui est intégrée à l’amorçage.

toosee comment hello Web app ressemble sans amorçage, ouvrez *application\_Démarrer\\BundleConfig.cs* et commentez les lignes hello contenant *bootstrap.js* et *bootstrap.css*. Hello de code suivant montre hello deux dernières instructions Hello `RegisterBundles` méthode après modification de hello :

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Appuyez sur `Ctrl+F5` application hello de toorun.

Observez que la barre de navigation réductible hello est maintenant simplement une liste non triée ordinaire. Cliquez sur **Parcourir par balise** une nouvelle fois, puis cliquez sur **ASP.NET**.
Dans la vue d’émulateur mobile hello, vous pouvez voir maintenant qu’il n’est plus monté de zoom de toohello écran, et vous devez faire défiler vers le côté en ordre toosee hello à droite de la table de hello.

![][SessionsByTagASP.NETNoBootstrap]

Annuler vos modifications et actualiser hello navigateur mobile tooverify qui hello adaptés aux appareils mobiles affichage a été restaurée.

Programme d’amorçage n’est pas spécifique tooASP.NET MVC 5, et vous pouvez tirer parti de ces fonctionnalités dans les applications web. Désormais, Bootstrap est intégré au modèle de projet ASP.NET MVC 5. Votre application web MVC 5 peut donc tirer parti de Bootstrap par défaut.

Pour plus d’informations sur les données d’amorçage, consultez toothe [Bootstrap] [ BootstrapSite] site.

Dans la section suivante de hello, vous verrez comment tooprovide des vues spécifiques du navigateur mobile.

## <a name="bkmk_overrideviews"></a>Remplacer les vues hello, dispositions et les vues partielles
Vous pouvez remplacer toutes les vues (y compris les dispositions et les vues partielles) des navigateurs mobiles en général, mais aussi d’un navigateur mobile particulier ou encore d’un navigateur spécifique. afficher les tooprovide mobiles spécifiques, vous pouvez copier un fichier de vue et ajouter *. Mobile* toohello nom du fichier. Par exemple, toocreate un mobile *Index* vue, vous pouvez copier *vues\\accueil\\Index.cshtml* à *vues\\accueil\\ Index.Mobile.cshtml*.

Dans cette section, vous allez créer un fichier de disposition mobile.

toostart, copie *vues\\Shared\\\_Layout.cshtml* à *vues\\Shared\\\_Layout.Mobile.cshtml* . Ouvrez  *\_Layout.Mobile.cshtml* et remplacez titre hello de **MVC5 Application** trop**MVC5 Application (Mobile)**.

Dans chaque `Html.ActionLink` l’appel pour la barre de navigation hello, supprimez « Parcourir par » dans chaque lien *ActionLink*. Hello de code suivant montre hello terminée `<ul class="nav navbar-nav">` balise du fichier de mise en page mobile hello.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Hello de copie *vues\\accueil\\AllTags.cshtml* le fichier *vues\\accueil\\AllTags.Mobile.cshtml*. Ouvrir le nouveau fichier de hello et modifier le `<h2>` élément à partir de « Balises » trop « balises (M) » :

    <h2>Tags (M)</h2>

Parcourir la page de balises toohello à l’aide d’un navigateur de bureau et à l’aide d’émulateur de navigateur mobile. émulateur de navigateur mobile Hello affiche hello deux modifications (hello titre à partir de  *\_Layout.Mobile.cshtml* et titre hello à partir de *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

En revanche, affichage du bureau hello n’a pas changé (avec un titre de  *\_Layout.cshtml* et *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a> Création de vues spécifiques du navigateur
En outre toomobile-bureau spécifiques et des vues, vous pouvez créer des vues pour un navigateur individuel. Par exemple, vous pouvez créer des vues qui sont spécifiquement conçus pour hello iPhone ou un navigateur d’Android hello. Dans cette section, vous allez créer une disposition pour le navigateur iPhone qui hello et une version iPhone Hello *AllTags* vue.

Ouvrez hello *Global.asax* et ajoutez hello suivant en bas de toohello de code de la `Application_Start` (méthode).

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Ce code définit un nouveau mode d’affichage appelé « iPhone », qui répondra à chaque demande entrante. Si la demande entrante de hello correspond à la condition que vous avez défini (autrement dit, si l’agent utilisateur de hello contient la chaîne de hello « iPhone »), ASP.NET MVC recherche pour les vues dont le nom contient le suffixe « iPhone ».

> [!NOTE]
> Lorsque Ajouter spécifiques au navigateur mobile modes d’affichage, telles que pour iPhone et Android, occuper que tooset hello du premier argument trop`0` toomake (insert haut hello de liste de hello) que ce mode de navigateur spécifiques hello est prioritaire sur modèle mobile de hello (*. Mobile.cshtml). Si le modèle mobile de hello est haut hello de liste de hello au lieu de cela, il sera sélectionné sur votre mode d’affichage souhaité (hello première correspondance wins et modèle de mobile hello correspond à tous les navigateurs mobiles). 
> 
> 

Dans le code hello, avec le bouton droit `DefaultDisplayMode`, choisissez **résoudre**, puis choisissez `using System.Web.WebPages;`. Cette opération ajoute une référence toothe `System.Web.WebPages` espace de noms qui est l’emplacement où le `DisplayModeProvider` et `DefaultDisplayMode` les types sont définis.

![][ResolveDefaultDisplayMode]

Vous pouvez également ajouter simplement manuellement hello suivant ligne toothe `using` section du fichier de hello.

    using System.Web.WebPages;

Enregistrer les modifications de hello. Copiez le fichier *Views\\Shared\\\_Layout.Mobile.cshtml* vers *Views\\Shared\\\_Layout.iPhone.cshtml*. Ouvrez le nouveau fichier de hello et modifiez titre hello à partir de `MVC5 Application (Mobile)` à `MVC5 Application (iPhone)`.

Hello de copie *vues\\accueil\\AllTags.Mobile.cshtml* le fichier *vues\\accueil\\AllTags.iPhone.cshtml*. Dans le nouveau fichier de hello, modifiez hello `<h2>` élément à partir de « balises (M) » » des balises (iPhone) ».

Exécutez l’application hello. Exécuter un émulateur navigateur mobile, assurez-vous que l’agent utilisateur qui lui est défini trop « iPhone », puis accédez toohello *AllTags* vue. Si vous utilisez un émulateur de hello dans les outils de développement Internet Explorer 11 F12, configurez les éléments suivants de toohello de l’émulation :

* Profil du navigateur = **Windows Phone**
* Chaîne d’agent utilisateur = **Custom**
* Chaîne personnalisée = **Apple-iPhone5C1/1001.525**

capture d’écran suivante Hello affiche hello *AllTags* vue dans l’émulateur dans les outils de développement Internet Explorer 11 F12 avec la chaîne d’agent utilisateur hello (il s’agit d’une chaîne d’agent utilisateur iPhone 5 C).

![][AllTagsIPhone_LayoutIPhone]

Dans le navigateur d’appareil mobile hello, sélectionnez hello **haut-parleurs** lien. Car il n’est pas un affichage mobile (*AllSpeakers.Mobile.cshtml*), afficher des haut-parleurs par défaut hello (*AllSpeakers.cshtml*) est restitué à l’aide du mode mobile hello ( *\_ Layout.Mobile.cshtml*). Comme indiqué ci-dessous, titre de hello **MVC5 Application (Mobile)** est défini dans  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

Vous pouvez désactiver globalement d’une vue de (non mobile) par défaut à partir de rendu à l’intérieur d’une disposition mobile en définissant `RequireConsistentDisplayMode` à `true` Bonjour *vues\\\_ViewStart.cshtml* fichier, comme suit :

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Lorsque `RequireConsistentDisplayMode` est défini trop`true`, disposition mobile de hello (*\_Layout.Mobile.cshtml*) est utilisé uniquement pour les périphériques mobiles (par exemple, lorsque le fichier est sous forme de hello  ***ViewName** . Mobile.cshtml*). Vous souhaiterez peut-être tooset `RequireConsistentDisplayMode` trop`true` si votre mise en page mobile ne fonctionne pas correctement avec les vues non mobiles. Hello capture d’écran ci-dessous montre comment hello *haut-parleurs* page restitue lorsque `RequireConsistentDisplayMode` est défini trop`true` (sans la chaîne hello « (Mobile) » Bonjour navigation barre haut hello).

![][AllSpeakers_LayoutMobileOverridden]

Vous pouvez désactiver le mode d’affichage cohérent dans une vue spécifique en définissant `RequireConsistentDisplayMode` trop`false` dans le fichier de vue hello. Le balisage suivant Bonjour *vues\\accueil\\AllSpeakers.cshtml* fichier définit `RequireConsistentDisplayMode` trop`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

Dans cette section, nous avons vu comment toocreate dispositions mobiles, des vues et comment toocreate dispositions et les vues pour des périphériques spécifiques tels que hello iPhone.
Toutefois, hello principal avantage du framework du programme d’amorçage CSS hello est la présentation interactive, ce qui signifie qu’une seule feuille de style peut être appliqué sur le bureau, téléphone et tablette navigateurs toocreate une apparence et convivialité cohérentes. Dans la section suivante de hello, vous verrez comment tooleverage amorcer toocreate adaptés aux appareils mobiles des vues.

## <a name="bkmk_Improvespeakerslist"></a>Améliorer hello haut-parleurs liste
Comme vous venez de voir, hello *haut-parleurs* vue est accessible en lecture, mais les liens hello sont petits et sont difficile tootap sur un appareil mobile. Dans cette section, vous allez apporter hello *AllSpeakers* affichage adaptés aux appareils mobiles, qui affiche des liens volumineux, facile à tap et qui contient un tooquickly de zone de recherche trouvé haut-parleurs.

Vous pouvez utiliser hello Bootstrap [groupe de liste liée] [ linked list group] style afin d’améliorer hello *haut-parleurs* vue. Dans *vues\\accueil\\AllSpeakers.cshtml*, remplacez le contenu hello du fichier de Razor hello avec code hello ci-dessous.

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

Hello `class="list-group"` attribut Bonjour `<div>` balise s’applique le style de la liste d’amorçage et hello `class="input-group-item"` lien tooeach style d’élément de liste d’amorçage s’applique l’attribut.

Actualiser le navigateur d’appareil mobile hello. Hello mis à jour la vue ressemble :

![][AllSpeakersFixed]

Hello Bootstrap [groupe de liste liée] [ linked list group] style rend hello entier d’une zone pour chaque lien interactif, ce qui constitue une bien meilleure expérience utilisateur. Basculer l’affichage du bureau toothe et observer hello apparence et convivialité cohérentes.

![][AllSpeakersFixedDesktop]

Bien que la vue du navigateur mobile hello a été améliorée, il est difficile de naviguer hello longue liste de haut-parleurs. Bootstrap est dépourvu d'une fonction de filtre de recherche en natif. Il est possible d'en ajouter une à l'aide de quelques lignes de code. Vous allez tout d’abord ajouter une vue de toohello de zone de recherche, puis raccorder avec hello du code JavaScript pour la fonction de filtre hello. Dans *vues\\accueil\\AllSpeakers.cshtml*, ajoutez un \<formulaire\> balise juste après hello \<h2\> de balise, comme indiqué ci-dessous :

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

Notez que hello `<form>` et `<input>` à la fois les balises ont hello amorçage styles appliqués toothem. Hello `<span>` élément ajoute un démarrage [glyphicon] [ glyphicon] zone de recherche toothe.

Bonjour *Scripts* dossier, ajoutez un fichier JavaScript nommé *filter.js*. Ouvrir le fichier de hello et collez hello après le code dans celui-ci :

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

Vous devez également tooinclude filter.js dans vos regroupements inscrits. Ouvrez *application\_Démarrer\\BundleConfig.cs* et modifier des groupes de première hello. Modifier la première `bundles.Add` instruction (pour hello **jquery** offre groupée) tooinclude *Scripts\\filter.js*, comme suit :

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

Hello **jquery** offre groupée est déjà rendue par défaut de hello  *\_disposition* vue. Une version ultérieure, vous pouvez utiliser hello du code JavaScript même tooapply les affichages de liste de filtre fonctionnalité tooother.

Actualiser le navigateur d’appareil mobile hello et accédez toohello *AllSpeakers* vue. Dans la zone de recherche, entrez « sc ». liste de haut-parleurs Hello doit maintenant être filtrée en fonction de chaîne de recherche tooyour.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Améliorer hello liste de balises
Comme hello *haut-parleurs* afficher, hello *balises* vue est accessible en lecture, mais les liens de hello sont petite et difficile tootap sur un appareil mobile. Vous pouvez corriger hello *balises* vue hello même moyen vous corrigez hello *haut-parleurs* afficher, si vous utilisez des modifications de code hello décrites précédemment, mais avec les éléments suivants de hello `Html.ActionLink` syntaxe de méthode dans  *Vues\\accueil\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Hello actualiser la recherche du navigateur de bureau comme suit :

![][AllTagsFixedDesktop]

Et hello actualisé navigateur mobile présente comme suit : 

![][AllTagsFixed]

> [!NOTE]
> Si vous remarquez que cette mise en forme de liste d’origine hello est toujours présent dans hello navigateur mobile et vous demander quels styles d’amorçage nice tooyour s’est produit, il s’agit d’un artefact de votre antérieures action toocreate mobile des vues spécifiques. Toutefois, maintenant que vous utilisez hello Bootstrap CSS framework toocreate une conception réactive web, accédez de tête et supprimer ces affichages mobiles spécifiques et des vues de mise en page spécifiques à mobile hello. Une fois que vous l’avez fait, hello de navigateur mobile actualisées affichera les styles d’amorçage hello.
> 
> 

## <a name="bkmk_improvedates"></a>Améliorer hello liste de Dates
Vous pouvez améliorer hello *Dates* afficher comme amélioré de hello *haut-parleurs* et *balises* affiche si vous utilisez hello les modifications du code décrites précédemment, mais avec hello suivant `Html.ActionLink` syntaxe de méthode dans *vues\\accueil\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

La vue du navigateur mobile actualisé se présente ainsi :

![][AllDatesFixed]

Vous pouvez encore améliorer hello *Dates* vue en organisant les valeurs de date-heure hello par date. Cela est possible avec hello Bootstrap [panneaux] [ panels] styles. Remplacez le contenu hello Hello *vues\\accueil\\AllDates.cshtml* fichier avec le code suivant :

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

Ce code crée un distinct `<div class="panel panel-primary">` balise pour chaque date distincte dans la liste de hello et utilise hello [groupe de liste liée] [ linked list group] pour différents liens comme avant. Voici un navigateur mobile hello il semble que lorsque ce code s’exécute :

![][AllDatesFixed2]

Navigateur de bureau toohello commutateur. Là encore, notez hello cohérent.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Améliorer hello SessionsTable vue
Dans cette section, vous allez apporter hello *SessionsTable* afficher plus d’adaptés aux appareils mobiles. Cette modification n’est plus étendu hello dernières modifications apportées.

Dans le navigateur d’appareil mobile hello, appuyez sur hello **balise** bouton, puis entrez `asp` dans la zone de recherche.

![][AllTagsFixedSearchByASP]

Appuyez sur hello **ASP.NET** lien.

![][SessionsTableTagASP.NET]

Comme vous pouvez le voir, affichage de hello est mise en forme en tant que table, qui est actuellement conçu toobe affichée dans le navigateur de bureau hello. Toutefois, il est un peu difficile tooread sur un navigateur mobile. toofix, ouvrez *vues\\accueil\\SessionsTable.cshtml* puis remplacez le contenu hello du fichier par hello suivant de code :

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

code de Hello effectue les 3 tâches :

* utilise hello Bootstrap [groupe de liste liée personnalisé] [ custom linked list group] tooformat hello verticalement, les informations de session afin que toutes ces informations sont accessibles en lecture sur un navigateur mobile (à l’aide de classes telles que liste groupe-élément-texte)
* s’applique hello [système de grille] [ grid system] toothe disposition, par conséquent, cette session hello les éléments de flux horizontalement dans le navigateur de bureau hello et verticalement dans un navigateur mobile de hello (à l’aide de la classe de hello col-md-4)
* utilise hello [utilitaires réactives] [ responsive utilities] pour masquer les balises de session hello lorsqu’ils sont affichés dans un navigateur mobile de hello (à l’aide de la classe de xs masqué hello)

Vous pouvez aussi appuyer sur une session titre lien toogo toohello respectifs. image Hello ci-dessous reflète les modifications de code hello.

![][FixedSessionsByTag]

système de grille d’amorçage Hello que vous avez appliqués automatiquement organise les sessions verticalement dans le navigateur d’appareil mobile hello. Notez également que les balises de hello ne sont pas affichées. Navigateur de bureau toohello commutateur.

![][SessionsTableFixedTagASP.NETDesktop]

Dans le navigateur de bureau hello, notez que les balises hello sont maintenant affichées. En outre, vous pouvez voir que système de grille d’amorçage hello que vous appliqué organise les éléments de session de hello dans deux colonnes. Si vous agrandissez le navigateur, vous verrez que le dispositif de hello change toothree colonnes.

## <a name="bkmk_improvesessionbycode"></a>Améliorer hello SessionByCode vue
Enfin, vous allez résoudre hello *SessionByCode* afficher toomake il adaptés aux appareils mobiles.

Dans le navigateur d’appareil mobile hello, appuyez sur hello **balise** bouton, puis entrez `asp` dans la zone de recherche.

![][AllTagsFixedSearchByASP]

Appuyez sur hello **ASP.NET** lien. Les sessions de balise ASP.NET hello sont affichées.

![][FixedSessionsByTag]

Choisissez hello **création d’une Application à Page unique avec ASP.NET et AngularJS** lien.

![][SessionByCode3-644]

affichage du bureau Hello par défaut convient, mais vous pouvez améliorer hello aspect facilement à l’aide de certains composants de l’interface utilisateur graphique du programme d’amorçage.

Ouvrez *vues\\accueil\\SessionByCode.cshtml* et remplacez les contenu hello hello suivant de balisage :

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

balisage de nouveau Hello utilise des panneaux d’amorçage styles d’affichage mobile de tooimprove hello. 

Actualiser le navigateur d’appareil mobile hello. Hello illustration suivante reflète les modifications de code hello que vous venez d’apporter :

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Conclusion
Ce didacticiel vous a montré comment les applications Web toouse ASP.NET MVC 5 toodevelop adaptés aux appareils mobiles. Vous avez notamment vu les points suivants :

* Déployer un tooan d’application ASP.NET MVC 5 application web App Service
* Utiliser la mise en page de démarrage toocreate web réactive dans votre application MVC 5
* Remplacer la disposition, les vues, les vues partielles, de façon globale ou pour une vue spécifique
* Contrôler la disposition et l’application de remplacement partiel à l’aide de la propriété `RequireConsistentDisplayMode`
* Créer des vues qui ciblent des navigateurs spécifiques, tels que navigateur iPhone qui hello
* Appliquer des styles Bootstrap dans le code Razor

## <a name="see-also"></a>Voir aussi
* [9 principes de base de la conception web réactive (en anglais)](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Bootstrap][BootstrapSite]
* [Blog Bootstrap officiel (en anglais)][Official Bootstrap Blog]
* [Tutoriel Bootstrap Twitter de Tutorial Republic (en anglais)][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Hello amorçage de laboratoire][hello Bootstrap Playground]
* [Bonnes pratiques pour les applications web mobiles des recommandations W3C (en anglais)][W3C Recommendation Mobile Web Application Best Practices]
* [Candidat à la recommandation du W3C concernant les requêtes de média (en anglais)][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

