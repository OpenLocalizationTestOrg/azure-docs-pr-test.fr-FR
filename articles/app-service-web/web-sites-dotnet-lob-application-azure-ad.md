---
title: aaaCreate une application Azure line-of-business avec authentification Azure Active Directory | Documents Microsoft
description: "Découvrez comment application toocreate un ASP.NET MVC-métier dans Azure App Service qui authentifie avec Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Créer une application Azure cœur de métier avec authentification Azure Active Directory
Cet article vous explique comment toocreate un .NET line-of-business application [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) à l’aide de hello [l’authentification / autorisation](../app-service/app-service-authentication-overview.md) fonctionnalité. Il montre également comment toouse hello [API Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery les données d’annuaire dans une application hello.

client Azure Active Directory Hello que vous utilisez peut être un répertoire Azure uniquement. Ou bien, il peut être [synchronisés avec votre Active Directory local](../active-directory/active-directory-aadconnect.md) toocreate une expérience d’authentification unique pour les travailleurs sont locaux et distants. Cet article utilise le répertoire par défaut de hello pour votre compte Azure.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Ce que vous allez créer
Vous allez générer une application de création-lire-mise à jour-suppression (CRUD) line-of-business simple dans une application de Service Web Apps qu’assure le suivi des éléments de travail avec hello suivant de fonctionnalités :

* Authentification des utilisateurs à l’aide d’Azure Active Directory
* Interrogation des utilisateurs et des groupes de répertoires à l’aide de l’ [API Graph Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Utilisez hello ASP.NET MVC *aucune authentification* modèle

Si vous avez besoin de contrôle d’accès en fonction du rôle (RBAC) pour votre application cœur de métier dans Azure, consultez l’ [étape suivante](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Ce dont vous avez besoin
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Vous devez hello suivant toocomplete ce didacticiel :

* Un locataire Azure Active Directory avec les utilisateurs de différents groupes
* Autorisations des applications toocreate sur le client d’Azure Active Directory hello
* Visual Studio 2013 Update 4 (ou version ultérieure)
* [Kit de développement logiciel (SDK) Azure 2.8.1 ou version ultérieure](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>Créer et déployer un tooAzure d’application web
1. Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.
2. Sélectionnez **Application web ASP.NET**, nommez votre projet, puis cliquez sur **OK**.
3. Sélectionnez hello **MVC** modèle, puis modifier l’authentification hello trop**aucune authentification**. Assurez-vous que **hôte Bonjour Cloud** est sélectionné, cliquez sur **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. Bonjour **créer un Service application** boîte de dialogue, cliquez sur **ajouter un compte** (puis **ajouter un compte** dans la liste déroulante de hello) toolog dans tooyour compte Azure.
5. Une fois connecté, configurez votre application web. Créer un groupe de ressources et d’un nouveau plan de Service de l’application en cliquant sur hello respectif **nouveau** bouton. Cliquez sur **Explorer d’autres services Azure** toocontinue.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. Bonjour **Services** , cliquez sur  **+**  tooadd une base de données SQL pour votre application. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. Dans **configurer la base de données SQL**, cliquez sur **nouveau** toocreate une instance de SQL Server.
8. Dans **Configurer SQL Server**, configurez votre instance SQL Server. Ensuite, cliquez sur **OK**, **OK**, et **créer** tookick hors tension de la création d’application hello dans Azure.
9. Dans **Azure App Service activité**, vous pouvez voir quand la création d’application hello est terminée. Cliquez sur  **publier &lt;* appname*> toothis application Web maintenant **, puis cliquez sur **publier**. 
   
    Une fois que Visual Studio se termine, il ouvre hello publier l’application dans le navigateur de hello. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Configurer l’authentification et l’accès à l’annuaire
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu de gauche hello, cliquez sur **des Services d’application** > **&lt;*appname*> ** > **l’authentification / autorisation**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Activez l’authentification Azure Active Directory en cliquant sur **Activé** > **Azure Active Directory** > **Express** > **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Cliquez sur **enregistrer** dans la barre de commandes hello.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Une fois que les paramètres d’authentification hello ont été enregistrés correctement, essayez d’application tooyour à nouveau dans le navigateur de hello. Les paramètres par défaut assurent une authentification sur l’application entière hello. Si vous n’êtes pas déjà connecté, vous êtes écran de connexion tooa redirigé. Une fois connecté, vous constatez que votre application est sécurisée via HTTPS. Ensuite, vous devez le toodirectory tooenable accéder aux données. 
5. Accédez toohello [portail classic](https://manage.windowsazure.com).
6. Dans le menu de gauche hello, cliquez sur **Active Directory** > **répertoire par défaut** > **Applications**  >   **&lt;* appname*> **.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Il s’agit d’application Azure Active Directory hello créés pour vous tooenable hello d’autorisation du Service d’applications / fonctionnalité d’authentification.
7. Cliquez sur **utilisateurs** et **groupes** toomake assurer que vous disposez de certains utilisateurs et groupes dans le répertoire de hello. Dans le cas contraire, créez plusieurs utilisateurs et groupes de test.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Cliquez sur **configurer** tooconfigure cette application.
9. Faites défiler vers le bas toohello **clés** section et ajouter une clé en sélectionnant une durée. Ensuite, cliquez sur **Autorisations déléguées** et sélectionnez **Lire les données de l’annuaire**. 
   Cliquez sur **Enregistrer**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Une fois que vos paramètres sont enregistrés, faites défiler sauvegarder toohello **clés** et cliquez sur hello **copie** clé de client bouton toocopy hello. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Si vous quittez cette page maintenant, vous ne serez pas en mesure de tooaccess jamais la clé de ce client.
    > 
    > 
11. Ensuite, vous devez tooconfigure votre application web avec cette clé. Connectez-vous à toohello [Explorateur de ressources Azure](https://resources.azure.com) avec votre compte Azure.
12. En hello haut hello, cliquez sur **en lecture/écriture** modifications toomake Bonjour Explorateur de ressources Azure.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Recherche des paramètres d’authentification pour votre application, situé dans les abonnements hello >  **&lt;* subscriptionname*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **fournisseurs** > **Microsoft.Web**  >  **sites** > **&lt;*appname*> ** > **config**  >  **authsettings**.
14. Cliquez sur **Modifier**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. Dans le volet de modification de hello, définissez hello `clientSecret` et `additionalLoginParams` propriétés comme suit.
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Cliquez sur **Put** à hello toosubmit supérieur vos modifications.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Tootest maintenant, si vous avez l’autorisation de hello jeton tooaccess hello API Graph Azure Active Directory, accédez simplement à  **https://&lt;*appname*>.azurewebsites.net/.auth/me** dans votre Navigateur. Si vous avez configuré tous les éléments correctement, vous devez voir hello `access_token` propriété Bonjour réponse JSON.
    
    Hello `~/.auth/me` chemin d’accès de l’URL est géré par l’authentification du Service application / toogive d’autorisation vous toutes les informations de hello liées tooyour authentifié session. Pour plus d’informations, consultez la page [Authentification et autorisation dans Azure App Service](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > Hello `access_token` a une période d’expiration. Toutefois, l’authentification/autorisation App Service fournit des fonctionnalités d’actualisation du jeton grâce à `~/.auth/refresh`. Pour plus d’informations sur la façon de toouse, consultez [App Store de jeton de Service](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

Ensuite, vous ferez quelque chose d’utile avec les données d’annuaire.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>Ajouter des fonctionnalités métier-tooyour application
Nous allons maintenant créer un outil de suivi simple des éléments de travail CRUD.  

1. Dans le dossier de ~\Models hello, créez un fichier de classe appelé WorkItem.cs et remplacez `public class WorkItem {...}` par hello suivant de code :
   
     using System.ComponentModel.DataAnnotations;
   
     public class WorkItem   {
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     public enum WorkItemStatus   {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Générez hello projet toomake votre logique de génération de modèles automatique toohello accessible à nouveau modèle dans Visual Studio.
3. Ajouter un nouvel élément de modèle généré automatiquement `WorkItemsController` toohello ~\Controllers dossier (avec le bouton droit **contrôleurs**, pointez trop**ajouter**, puis sélectionnez **nouvel élément structuré**). 
4. Sélectionnez **Contrôleur MVC 5 avec vues, en utilisant Entity Framework**, puis cliquez sur **Ajouter**.
5. Modèle hello SELECT que vous avez créé, puis cliquez sur  **+**  , puis **ajouter** tooadd un contexte de données, puis cliquez sur **ajouter**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. Dans ~\Views\WorkItems\Create.cshtml (un élément de modèle généré automatiquement automatiquement), recherchez hello `Html.BeginForm` méthode d’assistance et hello en surbrillance des modifications suivantes :  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Notez que `token` et `tenant` sont utilisés par hello `AadPicker` toomake objet appelle des API Azure Active Directory Graph. Vous allez ajouter `AadPicker` ultérieurement.     
   
   > [!NOTE]
   > Vous pouvez également obtenir `token` et `tenant` côté client de hello avec `~/.auth/me`, mais ce serait un appel de serveur supplémentaire. Par exemple :
   > 
   > $.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });
   > 
   > 
7. Apporter des modifications mêmes avec hello ~ \Views\WorkItems\Edit.cshtml.
8. Hello `AadPicker` objet est défini dans un script que vous avez besoin de tooadd tooyour projet. Cliquez sur hello ~\Scripts dossier, pointez trop**ajouter**, puis cliquez sur **fichier JavaScript**. Type `AadPickerLibrary` pour le nom de fichier hello et cliquez sur **OK**.
9. Copier le contenu hello [ici](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) dans ~ \Scripts\AadPickerLibrary.js.
   
   Dans le script de hello, hello `AadPicker` les appels de l’objet [API Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch pour les utilisateurs et groupes qui correspondent à des entrées de hello.  
10. ~\Scripts\AadPickerLibrary.js utilise également hello [widget de la saisie semi-automatique de l’interface utilisateur jQuery](https://jqueryui.com/autocomplete/). Vous devez donc projet tooyour de tooadd jQuery UI. Cliquez avec le bouton droit sur votre projet et cliquez sur **Gérer les packages NuGet**.
11. Dans le Gestionnaire de Package NuGet de hello, cliquez sur Parcourir, type **-jquery ui** dans hello barre de recherche, puis cliquez sur **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. Dans le volet droit de hello, cliquez sur **installer**, puis cliquez sur **OK** tooproceed.
13. Ouvrez ~\App_Start\BundleConfig.cs et rendre hello en surbrillance des modifications suivantes :  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Il existe plus performant de façons toomanage JavaScript et des fichiers CSS dans votre application. Toutefois, par souci de simplicité vous allez juste toopiggyback sur les groupes de hello qui sont chargées avec chaque vue.
14. Enfin, dans ~ \Global.asax, ajouter hello suivant la ligne de code hello `Application_Start()` (méthode). `Ctrl`+`.`sur chaque erreur de résolution de noms trop résoudre ce problème.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > Vous avez besoin de cette ligne de code, car le modèle MVC par défaut hello utilise <code>[ValidateAntiForgeryToken]</code> décoration sur certaines des actions de hello. En raison du comportement toohello décrite par [Brock Allen](https://twitter.com/BrockLAllen) à [MVC 4, AntiForgeryToken et revendications](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) votre HTTP POST peut échouer la validation du jeton anti-contrefaçon car :
    > 
    > * Azure Active Directory n’envoie pas http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, qui est requis par défaut par jeton anti-contrefaçon de hello.
    > * Si Azure Active Directory est répertoire synchronisé avec AD FS, approbation hello AD FS par défaut n’envoie pas de revendication de http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, bien que vous pouvez configurer manuellement les services AD FS toosend cette revendication.
    > 
    > `ClaimTypes.NameIdentifies`Spécifie la revendication de hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, lequel Azure Active Directory ne fournit pas.  
    > 
    > 
15. Maintenant, publiez vos modifications. Cliquez avec le bouton droit sur votre projet et cliquez sur **Publier**.
16. Cliquez sur **paramètres**, qu’il reste un tooyour de chaîne de connexion de base de données SQL, sélectionnez **mise à jour de la base de données** toomake hello des modifications de schéma pour votre modèle, puis cliquez sur **publier** .
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. Dans le navigateur de hello, accédez toohttps : / /&lt;*appname*>.azurewebsites.net/workitems et cliquez sur **créer un nouveau**.
18. Cliquez sur Bonjour **AssignedToName** boîte. Les utilisateurs et les groupes issus de votre client Azure Active Directory s’affichent désormais dans une liste déroulante. Vous pouvez taper toofilter, ou utilisez hello `Up` ou `Down` de clé, ou cliquez sur tooselect hello utilisateur ou un groupe. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Cliquez sur **créer** modifications de hello toosave. Ensuite, cliquez sur **modifier** sur le travail de hello créé élément tooobserve hello même comportement.

Félicitations, vous exécutez à présent une application cœur de métier dans Azure avec accès aux annuaires ! Il est beaucoup plus, que vous pouvez faire avec hello API Graph. Reportez-vous à la documentation de [référence sur l’API Graph Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).

<a name="next"></a>

## <a name="next-step"></a>Étape suivante
Si vous avez besoin de contrôle d’accès basé sur un rôle (RBAC) pour votre application line-of-business dans azure, consultez [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) pour obtenir un exemple à partir de l’équipe d’Azure Active Directory hello. Il vous montre comment les rôles tooenable pour votre application Azure Active Directory et autoriser les utilisateurs avec hello `[Authorize]` décoration.

Si votre application line-of-business doit accéder aux données locales tooon, consultez [accès aux ressources locales à l’aide de connexions hybrides dans Azure App Service](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Ressources supplémentaires
* [Authentification et autorisation dans Azure App Service](../app-service/app-service-authentication-overview.md)
* [Authentification avec Active Directory en local dans votre application Azure](web-sites-authentication-authorization.md)
* [Création d’une application cœur de métier dans Azure avec authentification AD FS](web-sites-dotnet-lob-application-adfs.md)
* [Authentification de Service d’application et hello API Azure AD Graph](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Documentation et exemples Microsoft Azure Active Directory](https://github.com/AzureADSamples)
* [Types de jeton et de revendication pris en charge par Azure Active Directory](http://msdn.microsoft.com/library/azure/dn195587.aspx)
