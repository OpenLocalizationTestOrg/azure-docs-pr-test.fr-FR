---
title: "aaaSession de gestion - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "mesures d’atténuation des menaces exposé Bonjour outil de modélisation des menaces"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>Infrastructure de sécurité : gestion des sessions | Articles 
| Produit/service | Article |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[Implémenter une déconnexion appropriée à l’aide de méthodes ADAL lors de l’utilisation d’Azure AD](#logout-adal)</li></ul> |
| Appareil IoT | <ul><li>[Utiliser des durées de vie limitées pour les jetons SaS générés](#finite-tokens)</li></ul> |
| **Azure Document DB** | <ul><li>[Utiliser des durées de vie de jeton minimales pour les jetons de ressource générés](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[Implémenter une déconnexion appropriée à l’aide de méthodes WsFederation lors de l’utilisation d’ADFS](#wsfederation-logout)</li></ul> |
| **IdentityServer** | <ul><li>[Implémenter une déconnexion appropriée lors de l’utilisation d’IdentityServer](#proper-logout)</li></ul> |
| **Application web** | <ul><li>[Utilisation requise de cookies sécurisés par les applications disponibles par le biais de HTTPS](#https-secure-cookies)</li><li>[Élément httpOnly requis dans la définition des cookies pour toutes les applications basées sur HTTP](#cookie-definition)</li><li>[Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les pages web ASP.NET](#csrf-asp)</li><li>[Configurer la durée de vie d’inactivité d’une session](#inactivity-lifetime)</li><li>[Implémenter la déconnexion appropriée à partir de l’application hello](#proper-app-logout)</li></ul> |
| **API Web** | <ul><li>[Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les API Web ASP.NET](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>Implémenter une déconnexion appropriée à l’aide de méthodes ADAL lors de l’utilisation d’Azure AD

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure AD | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Si l’application hello s’appuie sur le jeton d’accès émis par Azure AD, le Gestionnaire d’événements déconnexion hello doit appeler |

### <a name="example"></a>Exemple
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>Exemple
Il est également nécessaire de détruire la session de l’utilisateur en appelant la méthode Session.Abandon(). La méthode ci-après présente une implémentation sécurisée de la déconnexion d’un utilisateur :
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>Utiliser des durées de vie limitées pour les jetons SaS générés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Appareil IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Jetons SAP générés pour l’authentification tooAzure IoT Hub doivent avoir une période d’expiration finie. Conserver hello SaS durées de vie de jeton tooa toolimit minimale hello durée qu’ils peuvent être relues dans le cas où les jetons hello sont compromis.|

## <a id="resource-tokens"></a>Utiliser des durées de vie de jeton minimales pour les jetons de ressource générés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Document DB | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Réduire timespan hello de valeur minimale du jeton tooa ressource requise. Les jetons de ressource ont une durée de validité par défaut d'une heure.|

## <a id="wsfederation-logout"></a>Implémenter une déconnexion appropriée à l’aide de méthodes WsFederation lors de l’utilisation d’ADFS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | ADFS | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Si l’application hello s’appuie sur le jeton STS émis par ADFS, le Gestionnaire d’événements déconnexion hello doit appeler toolog de méthode WSFederationAuthenticationModule.FederatedSignOut() utilisateur de hello. Également hello session en cours doit être détruit, et la valeur du jeton de session hello doit être réinitialisé et annulé.|

### <a name="example"></a>Exemple
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>Implémenter une déconnexion appropriée lors de l’utilisation d’IdentityServer

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | IdentityServer | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [IdentityServer3-Federated sign out](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **Étapes** | IdentityServer prend en charge toofederate de capacité hello aux fournisseurs d’identité externe. Quand un utilisateur se déconnecte un fournisseur d’identité en amont, en fonction de protocole hello utilisé, il peut être possible tooreceive une notification lorsque hello utilisateur se déconnecte. Il permet de toonotify IdentityServer ses clients afin qu’ils peuvent également se connecter hello utilisateur out. Consultez la documentation de hello dans la section des références hello pour les détails d’implémentation hello.|

## <a id="https-secure-cookies"></a>Utilisation requise de cookies sécurisés par les applications disponibles par le biais de HTTPS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | EnvironmentType - OnPrem |
| **Informations de référence**              | [httpCookies, élément (Schéma des paramètres ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property (Propriété HttpCookie.Secure)](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **Étapes** | Les cookies sont normalement uniquement accessible toohello domaine pour lequel ils ont été limités. Malheureusement, définition hello de « domaine » n’inclut pas de protocole de hello les cookies qui sont créés via le protocole HTTPS sont accessibles via HTTP. attribut de « sécurisées » Hello indique navigateur toohello hello cookie doit uniquement être rendue disponible via le protocole HTTPS. Assurez-vous que tous les cookies définis sur HTTPS utilisent hello **sécurisé** attribut. spécification de Hello peut être appliquée dans le fichier web.config de hello en définissant hello requireSSL attribut tootrue. Il s’agit de hello préféré approche, car il appliquera hello **sécurisé** d’attribut pour tous les cookies actuels et futurs sans hello besoin toomake toutes les modifications de code supplémentaire.|

### <a name="example"></a>Exemple
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
paramètre de Hello est appliquée même si HTTP est utilisé tooaccess hello application. Si le protocole HTTP est utilisé tooaccess hello application, de hello sauts paramètre application hello parce que les cookies de hello sont définies avec le navigateur hello attribut et hello sécurisé n’envoie pas les toohello application.

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Web Forms, MVC5 |
| **Attributs**              | EnvironmentType - OnPrem |
| **Informations de référence**              | N/A  |
| **Étapes** | Lorsque hello web application hello partie de confiance, et hello IdP est le serveur AD FS, attribut de sécurité du jeton hello FedAuth peut être configuré en définissant le tooTrue requireSSL dans `system.identityModel.services` section du fichier web.config :|

### <a name="example"></a>Exemple
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>Élément httpOnly requis dans la définition des cookies pour toutes les applications basées sur HTTP

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Secure Cookie Attribute (Attribut de cookie sécurisé)](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **Étapes** | toomitigate hello risque de divulgation avec une attaque de l’écriture de scripts entre sites (XSS), un nouvel attribut - httpOnly - a été introduite toocookies et est pris en charge par tous les principaux navigateurs. attribut de Hello Spécifie qu’un cookie n’est pas accessible via un script. À l’aide de cookies HttpOnly, une application web réduit les risques de hello volées via un script et d’envoyés du site Web de l’attaquant tooan les informations sensibles contenues dans le cookie de hello. |

### <a name="example"></a>Exemple
Toutes les applications HTTP qui utilisent des cookies doivent spécifier HttpOnly dans la définition de cookie hello en implémentant après la configuration dans le fichier web.config :
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Web Forms |
| **Attributs**              | N/A  |
| **Informations de référence**              | [FormsAuthentication.RequireSSL Property (Propriété FormsAuthentication.RequireSSL)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **Étapes** | Hello RequireSSL valeur de la propriété est définie dans le fichier de configuration hello pour une application ASP.NET à l’aide de l’attribut requireSSL de hello d’élément de configuration hello. Vous pouvez spécifier dans le fichier Web.config de hello pour votre application ASP.NET si SSL (Secure Sockets Layer) est le serveur toohello de cookies d’authentification par formulaire hello tooreturn requis par attribut de paramètre hello requireSSL.|

### <a name="example"></a>Exemple 
Hello exemple de code suivant définit hello requireSSL attribut dans le fichier Web.config de hello.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC5 |
| **Attributs**              | EnvironmentType - OnPrem |
| **Informations de référence**              | [Windows Identity Foundation (WIF) Configuration – Part II (Configuration de Windows Identity Foundation (WIF) - Partie II)](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| **Étapes** | attribut httpOnly tooset pour les cookies FedAuth hideFromCsript attribut doit être la valeur tooTrue. |

### <a name="example"></a>Exemple
Configuration suivante montre la configuration correcte de hello :
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les pages web ASP.NET

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Falsification de requête (CSRF ou XSRF) est un type d’attaque dans lequel une personne malveillante peut exécuter des actions dans le contexte de sécurité hello de session établie d’un autre utilisateur sur un site web. objectif de Hello est toomodify ou supprimer le contenu, si le site web ciblé de hello s’appuie exclusivement sur session cookies tooauthenticate réception d’une requête. Un pirate peut exploiter cette vulnérabilité en obtenant tooload du navigateur d’un autre utilisateur d’une URL avec une commande d’un site vulnérable sur lequel hello utilisateur est déjà connecté. Il existe de nombreuses façons pour un toodo attaquant, telles que par un autre site web d’hébergement qui charge une ressource de serveur vulnérable de hello ou tooclick d’utilisateur lors de l’obtention hello un lien. attaque de Hello peut être évitée si le serveur de hello envoie un client toohello de jeton supplémentaires, requiert hello client tooinclude ce jeton dans toutes les demandes futures et vérifie que toutes les demandes futures incluent un jeton qui se rapporte toohello la session active, comme par à l’aide de hello ASP.NET AntiForgeryToken ou ViewState. |

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [XSRF/CSRF Prevention in ASP.NET MVC and Web Pages (Prévention des attaques XSRF/CSRF dans les pages MVC et Web ASP.NET)](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| **Étapes** | Formulaires anti-CSRF et ASP.NET MVC - hello d’utilisation `AntiForgeryToken` méthode d’assistance sur les vues ; mettez un `Html.AntiForgeryToken()` dans l’écran hello, par exemple,|

### <a name="example"></a>Exemple
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>Exemple
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Exemple
À hello même moment, visiteur de hello Html.AntiForgeryToken() donne un cookie appelé __RequestVerificationToken, avec hello même valeur que la valeur aléatoire masqué hello indiqué ci-dessus. Toovalidate une publication de formulaire entrantes, ajoutez ensuite la méthode d’action hello [ValidateAntiForgeryToken] filtre toohello cible. Par exemple :
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Un filtre d’autorisation qui vérifie les éléments suivants :
* demande entrante de Hello dispose d’un cookie appelé __RequestVerificationToken
* Hello demande entrante a un `Request.Form` entrée appelée __RequestVerificationToken
* Ces cookies et `Request.Form` correspondance des valeurs en supposant que toutes les est bien, hello demande passe par normalement. Dans le cas contraire, un échec d’autorisation survient avec le message « Un jeton anti-contrefaçon requis n’a pas été fourni ou n’est pas valide ». 

### <a name="example"></a>Exemple
AJAX et anti-CSRF : jeton de formulaire hello peut poser un problème pour les requêtes AJAX, car une requête AJAX peut envoyer des données JSON, pas les données de formulaire HTML. Une solution consiste aux jetons hello toosend dans un en-tête HTTP personnalisé. Hello de code suivant utilise des jetons de Razor syntaxe toogenerate hello, puis ajoute hello jetons tooan AJAX demande. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Exemple
Lorsque vous traitez la demande de hello, extrayez les jetons hello à partir de l’en-tête de demande hello. Puis l’appel hello AntiForgery.Validate méthode toovalidate des jetons hello. Hello méthode Validate lève une exception si les jetons hello ne sont pas valides.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Web Forms |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Tirer parti des fonctionnalités intégrées ASP.NET tooFend Off Web des attaques](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **Étapes** | Attaques CSRF dans WebForm en fonction des applications peuvent être atténuées en définissant la chaîne aléatoire ViewStateUserKey tooa qui varie pour chaque utilisateur - ID utilisateur ou, mieux encore, ID de session. Pour un certain nombre de raisons techniques et sociales, l’identifiant de session constitue un bien meilleur choix, car ce type d’identifiant est imprévisible, arrive à expiration et varie selon chaque utilisateur.|

### <a name="example"></a>Exemple
Voici le code hello vous devez toohave dans toutes les pages :
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>Configurer la durée de vie d’inactivité d’une session

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [HttpSessionState.Timeout Property (Propriété HttpSessionState.Timeout)](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **Étapes** | Délai d’expiration de session représente hello événement qui se produit quand un utilisateur ne n’exécute aucune action sur un site web pendant un intervalle (défini par le serveur web). Hello d’événement, côté serveur, de modifier le statut de hello de too'invalid de session utilisateur hello » (par exemple « non utilisé plus ») et lui demander de hello web server toodestroy (la suppression de toutes les données contenues dans celui-ci). Hello exemple de code suivant définit hello délai d’expiration session attribut too15 minutes dans le fichier Web.config de hello.|

### <a name="example"></a>Exemple
```Code XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Web Forms |
| **Attributs**              | N/A  |
| **Informations de référence**              | [forms, élément de authentication (Schéma des paramètres ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Étapes** | Définir les minutes hello too15 de délai d’attente de cookie de Ticket d’authentification de formulaires|

### <a name="example"></a>Exemple
```Code XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>Exemple
Également hello ADFS émis la durée de vie du jeton SAML revendication doit être défini à too15 minutes, en exécutant hello commande powershell sur un serveur AD FS hello suivante :
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Implémenter la déconnexion appropriée à partir de l’application hello

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Effectuer déconnexion approprié à partir de l’application hello, lorsque l’utilisateur appuie sur déconnecter de bouton. Lors de la déconnexion, l’application doit détruire la session de l’utilisateur et également réinitialiser et annuler la valeur du cookie de session, ainsi que la valeur du cookie d’authentification. En outre, lorsque plusieurs sessions identité d’utilisateur unique tooa liés, ils doivent être collectivement terminées côté hello serveur au délai d’attente ou de déconnexion. Enfin, assurez-vous que la fonctionnalité de déconnexion est accessible sur chaque page. |

## <a id="csrf-api"></a>Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les API Web ASP.NET

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Falsification de requête (CSRF ou XSRF) est un type d’attaque dans lequel une personne malveillante peut exécuter des actions dans le contexte de sécurité hello de session établie d’un autre utilisateur sur un site web. objectif de Hello est toomodify ou supprimer le contenu, si le site web ciblé de hello s’appuie exclusivement sur session cookies tooauthenticate réception d’une requête. Un pirate peut exploiter cette vulnérabilité en obtenant tooload du navigateur d’un autre utilisateur d’une URL avec une commande d’un site vulnérable sur lequel hello utilisateur est déjà connecté. Il existe de nombreuses façons pour un toodo attaquant, telles que par un autre site web d’hébergement qui charge une ressource de serveur vulnérable de hello ou tooclick d’utilisateur lors de l’obtention hello un lien. attaque de Hello peut être évitée si le serveur de hello envoie un client toohello de jeton supplémentaires, requiert hello client tooinclude ce jeton dans toutes les demandes futures et vérifie que toutes les demandes futures incluent un jeton qui se rapporte toohello la session active, comme par à l’aide de hello ASP.NET AntiForgeryToken ou ViewState. |

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API (Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) dans les API Web ASP.NET)](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| **Étapes** | AJAX et anti-CSRF : jeton de formulaire hello peut poser un problème pour les requêtes AJAX, car une requête AJAX peut envoyer des données JSON, pas les données de formulaire HTML. Une solution consiste aux jetons hello toosend dans un en-tête HTTP personnalisé. Hello de code suivant utilise des jetons de Razor syntaxe toogenerate hello, puis ajoute hello jetons tooan AJAX demande. |

### <a name="example"></a>Exemple
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Exemple
Lorsque vous traitez la demande de hello, extrayez les jetons hello à partir de l’en-tête de demande hello. Puis l’appel hello AntiForgery.Validate méthode toovalidate des jetons hello. Hello méthode Validate lève une exception si les jetons hello ne sont pas valides.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>Exemple
Anti-CSRF et formulaires ASP.NET MVC - hello d’utilisation méthode d’assistance de AntiForgeryToken sur les vues ; Placez un Html.AntiForgeryToken() sous forme de hello, par exemple,
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>Exemple
exemple Hello ci-dessus produira hello suivant :
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Exemple
À hello même moment, visiteur de hello Html.AntiForgeryToken() donne un cookie appelé __RequestVerificationToken, avec hello même valeur que la valeur aléatoire masqué hello indiqué ci-dessus. Toovalidate une publication de formulaire entrantes, ajoutez ensuite la méthode d’action hello [ValidateAntiForgeryToken] filtre toohello cible. Par exemple :
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Un filtre d’autorisation qui vérifie les éléments suivants :
* demande entrante de Hello dispose d’un cookie appelé __RequestVerificationToken
* Hello demande entrante a un `Request.Form` entrée appelée __RequestVerificationToken
* Ces cookies et `Request.Form` correspondance des valeurs en supposant que toutes les est bien, hello demande passe par normalement. Dans le cas contraire, un échec d’autorisation survient avec le message « Un jeton anti-contrefaçon requis n’a pas été fourni ou n’est pas valide ».

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC5, MVC6 |
| **Attributs**              | Fournisseur d’identité - ADFS, Fournisseur d’identité - Azure AD |
| **Informations de référence**              | [Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2 (Sécuriser une API Web avec des comptes individuels et une connexion locale dans API Web ASP.NET 2.2)](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| **Étapes** | Si hello API Web est sécurisé à l’aide d’OAuth 2.0, puis il attend un jeton de support dans l’autorisation demande en-tête et accorde l’accès toohello la demande uniquement si le jeton de hello est valide. Contrairement à l’authentification basé sur les cookies, les navigateurs n’attachement pas toorequests de jetons de porteur hello. Hello demande client doit tooexplicitly d’attacher le jeton de support hello dans l’en-tête de demande hello. Par conséquent, dans le cas des API Web ASP.NET protégées à l’aide d’OAuth 2.0, les jetons du porteur sont considérés comme un moyen de défense contre les attaques CSRF. Notez que si la partie MVC hello de l’application hello utilise l’authentification par formulaire (par exemple, utilise les cookies), les jetons anti-contrefaçon ont toobe utilisé par l’application web MVC est hello. |

### <a name="example"></a>Exemple
Hello API Web a toobe informé toorely uniquement sur les jetons de support et non sur les cookies. Il est possible en hello suivant la configuration dans `WebApiConfig.Register` méthode : ''' config du code C-Sharp. SuppressDefaultHostAuthentication() ; configuration. Filters.Add (nouvelle HostAuthenticationFilter(OAuthDefaults.AuthenticationType)) ;
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
