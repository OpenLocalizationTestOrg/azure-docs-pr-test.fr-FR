---
title: aaaCreate une application Azure line-of-business avec authentification AD FS | Documents Microsoft
description: "Découvrez comment une application métier-dans Azure App Service s’authentifie auprès de toocreate local STS. Ce didacticiel cible AD FS comme hello STS local."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>Créer une application cœur de métier Azure avec authentification AD FS
Cet article vous explique comment toocreate un ASP.NET MVC line-of-business application [Azure App Service](../app-service/app-service-value-prop-what-is.md) à l’aide d’un site local [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) en tant que fournisseur d’identité hello. Ce scénario peut fonctionner lorsque vous voulez les applications line-of-business toocreate dans Azure App Service votre organisation nécessite Active toobe de données stockée sur site.

> [!NOTE]
> Pour une vue d’ensemble des options de l’authentification et l’autorisation d’enterprise différents pour le Service d’applications Azure hello, consultez [authentifier avec Active Directory locale dans votre application Azure](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Ce que vous allez créer
Vous allez générer une application ASP.NET de base dans Azure App Service Web Apps avec hello suivant de fonctionnalités :

* Authentification des utilisateurs auprès d’AD FS
* Utilise `[Authorize]` utilisateurs tooauthorize pour différentes actions
* Configuration statique pour le débogage dans Visual Studio et de publication d’applications Web de Service tooApp (configurer qu’une seule fois, déboguer et publier à tout moment)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Ce dont vous avez besoin
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Vous devez hello suivant toocomplete ce didacticiel :

* Un site local déploiement AD FS (pour une procédure de bout en bout hello de laboratoire de test utilisé dans ce didacticiel, consultez [du laboratoire de Test : STS autonome avec AD FS dans une machine virtuelle Azure (pour le test)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* Approbations de partie de confiance autorisations toocreate dans Gestion AD FS
* Visual Studio 2013 Update 4 (ou version ultérieure)
* [Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) ou version ultérieure

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Utiliser l’exemple d’application pour le modèle métier
Hello exemple d’application dans ce didacticiel, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), est créé par l’équipe d’Azure Active Directory hello. Étant donné que AD FS prend en charge WS-Federation, vous pouvez l’utiliser comme un toocreate modèles d’applications line-of-business en toute simplicité. Il a hello suivant de fonctionnalités :

* Utilise [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate avec un site local déploiement AD FS
* Fonctionnalités de connexion et de déconnexion
* Utilise [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (au lieu de Windows Identity Foundation), qui est hello ultérieure d’ASP.NET et tooset beaucoup plus simple pour l’authentification et d’autorisation à WIF

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Installer l’application d’exemple hello
1. Cloner ou télécharger l’exemple de solution hello à [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) répertoire local de tooyour.
   
   > [!NOTE]
   > Hello les instructions de la section [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) vous montrent comment tooset application hello avec Azure Active Directory. Mais dans ce didacticiel, vous configurer avec AD FS, par conséquent, suivez les étapes de hello ici à la place.
   > 
   > 
2. Ouvrez la solution de hello, puis ouvrez Controllers\AccountController.cs Bonjour **l’Explorateur de solutions**.
   
   Vous verrez que les code hello émet simplement un authentification stimulation tooauthenticate hello utilisateur à l’aide de WS-Federation. Toute l’authentification est configurée dans App_Start\Startup.Auth.cs.
3. Ouvrez App_Start\Startup.Auth.cs. Bonjour `ConfigureAuth` (méthode), ligne de hello Remarque :
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   Dans le monde OWIN hello, cet extrait de code est réellement hello strict que minimum, vous devez le tooconfigure l’authentification WS-Federation. Il est beaucoup plus simple et plus élégante à WIF, où Web.config est injecté avec XML partout dans l’emplacement de hello. Hello uniquement les informations dont vous avez besoin sont hello partie de confiance (RP) identificateur et hello l’URL du fichier de métadonnées de votre service AD FS. Voici un exemple :
   
   * Identificateur de la partie de confiance : `https://contoso.com/MyLOBApp`
   * Adresse des métadonnées : `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. Dans App_Start\Startup.Auth.cs, modifiez hello suivant des définitions de type chaîne statique :  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Maintenant, modifiez hello correspondant dans le fichier Web.config. Ouvrez hello Web.config et modifier hello suivant les paramètres de l’application :  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   Renseignez les valeurs de clé hello en fonction de votre environnement respectif.
6. Toomake d’application hello qu’il n’y a aucune erreur de build.

Vous avez terminé. Exemple d’application hello est à présent prêt toowork avec AD FS. Vous devez toujours tooconfigure une approbation de partie de confiance avec cette application dans AD FS plus tard.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Déployer hello exemple application tooAzure App Service Web Apps
Ici, vous publiez hello application tooa l’application web dans les applications Web App Service tout en conservant les environnement de débogage hello. Notez que vous prévoyez d’application de hello toopublish avant qu’il ait une relation d’approbation RP avec AD FS, donc l’authentification ne fonctionne toujours pas encore. Toutefois, si vous le faites maintenant vous pouvez avoir URL de l’application web hello que vous pouvez utiliser d’approbation de partie de confiance tooconfigure hello plus tard.

1. Cliquez avec le bouton droit sur votre projet et sélectionnez **Publier**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Cliquez sur **Microsoft Azure App Service**.
3. Si vous n’avez pas encore connecté tooAzure, cliquez sur **connexion** et utiliser un compte Microsoft de hello pour toosign de votre abonnement Azure dans.
4. Une fois connecté, cliquez sur **nouveau** toocreate une application web.
5. Renseignez tous les champs obligatoires. Vous allez tooconnect tooon locale, les données plus tard, donc vous ne pouvez pas créer une base de données pour cette application web.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. Cliquez sur **Créer**. Une fois l’application hello web est créée, la boîte de dialogue Publier le site Web hello est ouvert.
7. Dans **URL de Destination**, modifiez **http** trop**https**. Copiez hello entière URL tooa éditeur de texte pour une utilisation ultérieure. Cliquez ensuite sur **Publier**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. Dans Visual Studio, ouvrez **Web.Release.config** dans votre projet. Insérer hello XML suivant dans hello `<configuration>` balise et remplacez la valeur de clé hello avec l’URL de l’application web de votre publication.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

Lorsque vous avez terminé, vous avez deux identificateurs RP configurés dans votre projet, une pour votre environnement de débogage dans Visual Studio, et l’autre pour hello publié l’application web dans Azure. Vous allez configurer une approbation de partie de confiance pour chacun des deux environnements de hello dans AD FS. Pendant le débogage, les paramètres dans le fichier Web.config de l’application hello sont toomake utilisé votre **déboguer** travail de configuration avec AD FS. Lorsqu’elle est publiée (par défaut, hello **version** configuration est publiée), un fichier Web.config transformé qui intègre les modifications du paramètre d’application hello dans Web.Release.config téléchargé.

Si vous souhaitez l’application web publiée de hello tooattach dans Azure toohello débogueur (autrement dit, vous devez télécharger les symboles de débogage de votre code dans l’application web publiée de hello), vous pouvez créer un clone de hello déboguer la configuration de débogage Azure, mais avec son propre fichier Web.config personnalisé transformer) par exemple, Web.AzureDebug.config) qui utilise les paramètres de l’application à partir de Web.Release.config hello. Ainsi, vous toomaintain une configuration statique dans différents environnements de hello.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Configuration d’approbations de partie de confiance dans Gestion AD FS
Vous devez maintenant tooconfigure une approbation de partie de confiance dans Gestion AD FS avant de pouvoir utiliser votre exemple d’application et en fait s’authentifier avec AD FS. Vous devez tooset les deux approbations de partie de confiance distinctes, une pour votre environnement de débogage et un pour votre application web publiée.

> [!NOTE]
> Assurez-vous que vous répétez hello comme suit pour les deux de vos environnements.
> 
> 

1. Sur votre serveur AD FS, connectez-vous avec les informations d’identification disposant des droits de gestion tooAD FS.
2. Ouvrez Gestion AD FS. Cliquez avec le bouton droit sur **AD FS\Relations de confiance\Approbations de partie de confiance** et sélectionnez **Ajouter une approbation de partie de confiance**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. Bonjour **sélectionner une Source de données** , sélectionnez **entrer manuellement les données sur la partie de confiance hello**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. Bonjour **indiquer le nom complet** page, tapez un nom complet pour l’application hello et cliquez sur **suivant**.
5. Bonjour **choisissez un protocole** , cliquez sur **suivant**.
6. Bonjour **configurer le certificat** , cliquez sur **suivant**.
   
   > [!NOTE]
   > Étant donné que vous utilisez déjà HTTPS, les jetons chiffrés sont facultatifs. Si vous voulez vraiment tooencrypt des jetons à partir d’AD FS sur cette page, vous devez également ajouter la logique de déchiffrement de jeton dans votre code. Pour plus d’informations, consultez la page [Configuration manuelle de l’intergiciel (middleware) OWIN WS-Federation et acceptation des jetons chiffrés](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Avant de passer à l’étape suivante de hello, vous devez une information de votre projet Visual Studio. Dans Propriétés du projet hello, notez hello **URL SSL** de l’application hello. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. Dans Gestion AD FS, Bonjour **configurer l’URL** page Hello **Assistant Ajouter une partie confiance**, sélectionnez **activer la prise en charge de protocole WS-Federation passif de hello** et tapez Bonjour URL SSL de votre projet Visual Studio que vous avez noté à l’étape précédente de hello. Cliquez ensuite sur **Suivant**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL spécifie où le client de hello toosend après l’authentification réussit. Pour un environnement de débogage hello, il doit être <code>https://localhost:&lt;port&gt;/</code>. Pour l’application web publiée de hello, elle doit être hello URL de l’application web.
   > 
   > 
9. Bonjour **configurer les identificateurs** page, vérifiez que votre projet URL SSL est déjà répertorié, cliquez sur **suivant**. Cliquez sur **suivant** tous hello fin toohello de moyen de l’Assistant hello avec les sélections par défaut.
   
   > [!NOTE]
   > Dans App_Start\Startup.Auth.cs de votre projet Visual Studio, cet identificateur est mis en correspondance par rapport à la valeur hello <code>WsFederationAuthenticationOptions.Wtrealm</code> lors de l’authentification fédérée. Par défaut, les URL de l’application hello à partir de l’étape précédente de hello est ajouté comme un identificateur de partie de confiance.
   > 
   > 
10. Vous avez terminé de configurer hello application de partie de confiance pour votre projet dans AD FS. Ensuite, vous configurez ce toosend application hello revendications requises par votre application. Hello **modifier les règles de revendication** boîte de dialogue est ouverte par défaut pour vous à fin hello d’Assistant de hello afin que vous pouvez démarrer immédiatement. Permet de configurer au moins hello après les revendications (avec les schémas entre parenthèses) :
    
    * Nom (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - utilisé par ASP.NET toohydrate `User.Identity.Name`.
    * Utilisateur nom principal (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - utilisé toouniquely identifier les utilisateurs de l’organisation de hello.
    * Appartenances aux groupes en tant que rôles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - peut être utilisé avec `[Authorize(Roles="role1, role2,...")]` décoration tooauthorize contrôleurs/actions. En réalité, cette approche ne peut pas être hello plus performantes pour l’autorisation de rôle. Si vos utilisateurs AD appartiennent toohundreds des groupes de sécurité, ils deviennent des centaines de revendications de rôle dans le jeton SAML de hello. Une autre approche consiste à toosend un seul rôle de revendication conditionnellement en fonction de l’appartenance de l’utilisateur hello dans un groupe particulier. Toutefois, pour ce didacticiel, nous allons procéder plus simplement.
    * ID de nom (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - peut être utilisé pour la validation anti-contrefaçon. Pour plus d’informations sur la façon dont toomake il anti-contrefaçon validation, consultez hello **ajouter des fonctionnalités métier-** section de [créer une application Azure line-of-business avec authentification Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Hello revendication types que vous avez besoin de tooconfigure pour votre application est déterminée par les besoins de votre application. Pour la liste hello de revendications pris en charge par les applications Azure Active Directory (autrement dit, des approbations de partie de confiance), par exemple, consultez [prise en charge du jeton et Types de revendications](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. Dans la boîte de dialogue Modifier les règles de revendication hello, cliquez sur **ajouter une règle**.
12. Configurer des revendications de nom UPN et rôle hello comme indiqué dans la capture d’écran de hello et cliquez sur **Terminer**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Ensuite, créez un nom temporaire ID de revendication à l’aide des étapes de hello illustrées dans [les identificateurs de nom dans les assertions SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Cliquez de nouveau sur **Ajouter une règle** .
14. Sélectionnez **Envoyer les revendications en utilisant une règle personnalisée**, puis cliquez sur **Suivant**.
15. Langage de règle suivante hello de coller dans hello **règle personnalisée** zone, une règle de hello nom **par l’identificateur de Session** et cliquez sur **Terminer**.  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    Votre règle personnalisée doit ressembler à cette capture d’écran :
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. Cliquez de nouveau sur **Ajouter une règle** .
17. Sélectionnez **Transformer une revendication entrante** et cliquez sur **Suivant**.
18. Configurer la règle de hello comme indiqué dans la capture d’écran hello (à l’aide du type de revendication hello vous avez créé dans une règle personnalisée de hello) et cliquez sur **Terminer**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Pour plus d’informations sur les étapes de hello pour la revendication de nom ID hello temporaire, consultez [les identificateurs de nom dans les assertions SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Cliquez sur **appliquer** Bonjour **modifier les règles de revendication** boîte de dialogue. Il doit maintenant ressembler à hello suivant capture d’écran :
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Là encore, assurez-vous que vous répétez ces étapes pour votre environnement de débogage et l’application web publiée.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Tester l’authentification fédérée pour votre application
Vous est tootest prêt logique d’authentification de votre application par rapport à ADFS. Dans mon environnement de laboratoire AD FS, j’ai un utilisateur de test auquel appartient le groupe de test tooa dans Active Directory (AD).

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

authentification tootest dans le débogueur hello, il vous suffit de toodo maintenant est de type `F5`. Si vous souhaitez que l’authentification de tootest dans l’application web publiée de hello, accédez toohello URL.

Une fois le charge de l’application web de hello, cliquez sur **connexion**. Soit une boîte de dialogue ou hello login page de connexion pris en charge par AD FS, en fonction de la méthode d’authentification hello choisi par AD FS doit maintenant s’afficher. Voici ce que nous obtenons dans Internet Explorer 11.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

Une fois que vous vous connectez avec un utilisateur de domaine hello AD du déploiement de hello AD FS, vous devez maintenant voir la page d’accueil de hello avec **Hello, <User Name>!** dans l’angle de hello. Voici ce que nous obtenons.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

Jusqu'à présent, vous avez réussi Bonjour suivant façons :

* Votre application a atteint l’AD FS et un identificateur de partie de confiance correspondant est trouvé dans la base de données AD FS de hello
* AD FS a été authentifié un utilisateur Active Directory et rediriger la page d’accueil de l’application toohello
* AD FS en tant que nom de hello envoyé avec succès de revendication (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, comme indiqué par le fait de hello cet utilisateur hello nom s’affiche dans l’angle de hello. 

Si la revendication de nom hello est manquante, vous auriez vu **Bonjour !**. Si vous examinez Views\Shared\_LoginPartial.cshtml, vous trouvez qu’il utilise `User.Identity.Name` nom d’utilisateur toodisplay hello. Comme mentionné précédemment, si le nom de hello revendication Hello authentifié l’utilisateur n’est disponible dans le jeton SAML de hello, ASP.NET hydrates de cette propriété avec lui. toosee que tous hello des revendications qui sont envoyés par AD FS, placez un point d’arrêt dans Controllers\HomeController.cs, Bonjour de méthode d’action Index. Une fois hello utilisateur est authentifié, inspecter hello `System.Security.Claims.Current.Claims` collection.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Autorisation des utilisateurs pour des contrôleurs ou des actions spécifiques
Étant donné que vous avez inclus les appartenances aux groupes en tant que revendications de rôle dans votre configuration d’approbation de partie de confiance, vous pouvez désormais les utiliser directement dans hello `[Authorize(Roles="...")]` décoration pour les contrôleurs et les actions. Dans une application métier-avec modèle de création-lire-mise à jour-suppression (CRUD) hello, vous pouvez autoriser des rôles spécifiques tooaccess chaque action. Pour l’instant, vous allez simplement essayer cette fonctionnalité sur le contrôleur Home existant de hello.

1. Ouvrez Controllers\HomeController.cs.
2. Décorer hello `About` et `Contact` toohello similaire action méthodes suivante de code, à l’aide des appartenances de sécurité de l’utilisateur authentifié.  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    Étant donné que j’ai ajouté **utilisateur Test** trop**groupe Test** dans mon environnement de laboratoire AD FS, je vais utiliser d’autorisation de groupe Test tootest sur `About`. Pour `Contact`, de tester cas négatif de hello de **Admins du domaine**, toowhich **utilisateur de Test** n’appartient pas.
3. Démarrez le débogueur de hello en tapant `F5` et connectez-vous, puis cliquez sur **sur**. Vous devriez maintenant afficher hello `~/About/Index` page avec succès, si votre utilisateur authentifié est autorisé pour cette action.
4. Maintenant, cliquez sur **Contact**, dans mon cas ne doivent pas autoriser **utilisateur Test** pour l’action de hello. Toutefois, le navigateur de hello est redirigé tooAD FS, ce qui est finalement affiche ce message :
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Si vous examinez cette erreur dans l’Observateur d’événements sur hello serveur AD FS, vous consultez le message d’exception :  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    Hello pour corriger cette erreur parce que par défaut, MVC retourne un 401 non autorisé lorsque les rôles d’un utilisateur ne sont pas autorisés. Cela déclenche un fournisseur d’identité de la réauthentification demande tooyour (AD FS). Étant donné que hello utilisateur est déjà authentifié, AD FS retourne toohello même page, qui émet alors un autre 401, création d’une boucle de redirection. Vous substituez d’AuthorizeAttribute `HandleUnauthorizedRequest` méthode avec une logique simple tooshow quelque chose qui soit parlante au lieu de la boucle de redirection hello poursuite de l’opération.
5. Créez un fichier de projet hello appelé AuthorizeAttribute.cs et hello Coller après le code dans celui-ci.
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    Hello remplacer le code envoie un HTTP 403 (interdit) au lieu de HTTP 401 (non autorisé) dans les cas authentifiés mais non autorisés.
6. Exécuter le débogueur hello avec `F5`. Lorsque vous cliquez sur **Contact** , un message d’erreur plus explicite s’affiche à présent :
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Publiez de nouveau hello application tooAzure App Service Web Apps et tester le comportement de hello d’application en temps réel de hello.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Se connecter aux données local tooon
Une raison que vous souhaiteriez tooimplement votre application métier-avec AD FS au lieu d’Azure Active Directory est problèmes de conformité avec la conservation des données organisation désactivé en local. Cela signifie également que votre application web dans Azure doive accéder aux bases de données locales, étant donné que vous n’êtes pas autorisé toouse [base de données SQL](/services/sql-database/) comme couche de données hello pour vos applications web.

Azure App Service Web Apps prend en charge l’accès aux bases de données locales avec deux approches : [Connexions hybrides](../biztalk-services/integration-hybrid-connection-overview.md) et [Réseaux virtuels](web-sites-integrate-with-vnet.md). Pour plus d’informations, consultez la rubrique [Utilisation de l’intégration VNET et des connexions hybrides avec Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Ressources supplémentaires
* [Authentification avec Active Directory en local dans votre application Azure](web-sites-authentication-authorization.md)
* [Créer une application Azure cœur de métier avec authentification Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md)
* [Utilisez hello Option d’authentification d’organisation locale (ADFS) avec ASP.NET dans Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Migrer un tooKatana VS2013 projet Web à partir de WIF](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Vue d’ensemble des services AD FS](http://technet.microsoft.com/library/hh831502.aspx)
* [Spécification WS-Federation 1.1](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

