---
title: "aaaException de gestion - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
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
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a>Infrastructure de sécurité : Gestion des exceptions | Corrections 
| Produit/service | Article |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF - Ne pas inclure le nœud serviceDebug dans le fichier de configuration](#servicedebug)</li><li>[WCF - Ne pas inclure le nœud serviceMetadata dans le fichier de configuration](#servicemetadata)</li></ul> |
| **API Web** | <ul><li>[Vérifier que la gestion des exceptions correcte est effectuée dans l’API web ASP.NET](#exception)</li></ul> |
| **Application web** | <ul><li>[Ne pas exposer les détails de sécurité dans les messages d’erreur ](#messages)</li><li>[Implémenter la page de gestion des erreurs par défaut ](#default)</li><li>[Définir la méthode de déploiement tooRetail dans IIS](#deployment)</li><li>[Les exceptions doivent échouer en toute sécurité](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF - Ne pas inclure le nœud serviceDebug dans le fichier de configuration

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | Services Windows Communication Framework (WCF) peuvent être configuré tooexpose les informations de débogage. Les informations de débogage ne doivent pas être utilisées dans les environnements de production. Hello `<serviceDebug>` balise définit si la fonctionnalité d’informations de débogage de hello est activée pour un service WCF. Si a la valeur tootrue hello attribut includeExceptionDetailInFaults, informations sur les exceptions à partir de l’application hello seront affichera tooclients. Les pirates peuvent tirer parti de hello supplémentaires qu’ils des gains d’informations de débogage de sortie toomount les attaques ciblées sur l’infrastructure de hello, base de données ou d’autres ressources utilisées par l’application hello. |

### <a name="example"></a>Exemple
fichier de configuration suivant Hello inclut hello `<serviceDebug>` balise : 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Désactiver les informations de débogage dans le service hello. Cela peut être accompli en supprimant hello `<serviceDebug>` étiquette à partir du fichier de configuration de votre application. 

## <a id="servicemetadata"></a>WCF - Ne pas inclure le nœud serviceMetadata dans le fichier de configuration

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Générique, NET Framework 3 |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | Exposer publiquement des informations sur un service peut fournir aux attaquants précieuses dans comment ils peuvent exploiter les service hello. Hello `<serviceMetadata>` balise active la fonctionnalité de publication de métadonnées hello. Les métadonnées de service peuvent contenir des informations sensibles qui ne doivent pas être accessibles publiquement. Au minimum, autoriser uniquement les utilisateurs approuvés tooaccess hello des métadonnées et vous assurer que les informations inutiles ne sont pas exposées. Mieux encore, de désactiver entièrement hello capacité toopublish métadonnées. Une configuration sécurisée de WCF ne contiendra pas hello `<serviceMetadata>` balise. |

## <a id="exception"></a>Vérifier que la gestion des exceptions correcte est effectuée dans l’API web ASP.NET

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC 5, MVC 6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Gestion des exceptions dans l’API web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Validation de modèle dans l’API web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Étapes** | Par défaut, la plupart des exceptions non interceptées dans l’API web ASP.NET sont converties en réponse HTTP avec le code d’état`500, Internal Server Error`|

### <a name="example"></a>Exemple
code d’état toocontrol hello retourné par hello API, `HttpResponseException` peut être utilisé comme indiqué ci-dessous : 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a>Exemple
Pour contrôler davantage sur la réponse d’exception hello, hello `HttpResponseMessage` classe peut être utilisée comme indiqué ci-dessous : 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
toocatch exceptions non gérées qui ne sont pas du type de hello `HttpResponseException`, les filtres d’Exception peut être utilisés. Filtres d’exception implémentent hello `System.Web.Http.Filters.IExceptionFilter` interface. toowrite de façon la plus simple Hello un filtre d’exception est tooderive de hello `System.Web.Http.Filters.ExceptionFilterAttribute` classe et substituer la méthode OnException de hello. 

### <a name="example"></a>Exemple
Voici un filtre qui convertit des `NotImplementedException` exceptions en code d’état HTTP `501, Not Implemented` : 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

Il existe plusieurs façons tooregister un filtre d’exception API Web :
- Par action
- Par contrôleur
- Globalement

### <a name="example"></a>Exemple
tooapply hello filtre d’action spécifique de tooa, ajouter un filtre de hello en tant qu’attribut toohello action : 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a>Exemple
tooapply hello filtre tooall d’actions hello sur un `controller`, ajouter un filtre de hello comme un attribut toohello `controller` classe : 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Exemple
tooapply hello filtrer les contrôleurs d’API Web tooall globalement, ajoutez une instance du hello filtre toohello `GlobalConfiguration.Configuration.Filters` collection. Filtres d’exception dans cette collection s’appliquent d’action du contrôleur Web API tooany. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Exemple
Pour la validation de modèle, état du modèle hello peut être passé méthode tooCreateErrorResponse comme indiqué ci-dessous : 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

Vérifiez les liens hello dans la section des références pour plus d’informations sur la gestion des exceptionnelles hello et validation de modèle dans l’API Web ASP.Net 

## <a id="messages"></a>Ne pas exposer les détails de sécurité dans les messages d’erreur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Messages d’erreur génériques sont fournies directement toohello utilisateur sans inclure les données d’application sensibles. Voici quelques exemples de données sensibles :</p><ul><li>Noms de serveur</li><li>Chaînes de connexion</li><li>Noms d’utilisateur</li><li>Mot de passe</li><li>Procédures SQL</li><li>Détail des échecs SQL dynamiques</li><li>Arborescence des appels de procédure et lignes de code</li><li>Variables stockées dans la mémoire</li><li>Emplacements de lecteur et de dossier</li><li>Points d’installation d’application</li><li>Paramètres de configuration d’hôte</li><li>Autres détails de l’application internes</li></ul><p>L’interception de toutes les erreurs dans une application, la fourniture de messages d’erreur génériques, ainsi que l’activation des messages d’erreur personnalisés dans IIS permettent d’éviter la divulgation d’informations. Base de données SQL Server et de gestion, entre autre erreur de gestion des architectures, des exceptions .NET sont utilisateur malveillant de tooa particulièrement longue et extrêmement utiles profiler votre application. Faire pas directement hello d’afficher le contenu d’une classe dérivée de la classe d’Exception .NET hello et vérifiez que vous disposez de la gestion des exceptions appropriées afin qu’une exception inattendue n’est pas par inadvertance déclenché directement toohello utilisateur.</p><ul><li>Fournir des messages d’erreur générique directement utilisateur toohello qui résument les détails spécifiques rangements trouvés directement dans le message d’erreur d’exception hello</li><li>Non affichage hello contenu d’une exception .NET classe directement toohello utilisateur</li><li>Intercepter tous les messages d’erreur et le cas échéant informe l’utilisateur hello via un client d’application erreur générique message envoyé toohello</li><li>Ne pas exposer de contenu hello de classe d’Exception hello directement toohello utilisateur, en particulier hello retourner la valeur de `.ToString()`, ou les valeurs des propriétés de Message ou StackTrace hello hello. Se connecter à ces informations et afficher un utilisateur de toohello plus anodin par message en toute sécurité</li></ul>|

## <a id="default"></a>Implémenter la page de gestion des erreurs par défaut

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Modifier la boîte de dialogue des paramètres des pages d’erreur ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Étapes** | <p>Lorsqu’une application ASP.NET échoue et provoque une erreur serveur interne HTTP/1.x 500, ou que la configuration d’une fonctionnalité (comme le filtrage des demandes) empêche l’affichage d’une page, un message d’erreur est généré. Les administrateurs peuvent choisir ou non l’application hello doit afficher un message convivial toohello client, client de toohello message erreur détaillé ou erreur détaillée message toolocalhost uniquement. Hello <customErrors> balise dans le fichier web.config de hello comporte trois modes :</p><ul><li>**On :** spécifie que les erreurs personnalisées sont activées. Si aucun attribut defaultRedirect n’est spécifié, les utilisateurs voient une erreur générique. les erreurs personnalisées Hello figurent toohello des clients distants et l’hôte local de toohello</li><li>**Off :** spécifie que les erreurs personnalisées sont désactivées. Hello erreurs ASP.NET détaillées sont affichées toohello des clients distants et l’hôte local de toohello</li><li>**RemoteOnly :** Spécifie que les erreurs personnalisées sont affichées uniquement des clients distants toohello, et que les erreurs ASP.NET sont affichées les hôte local toohello. Il s’agit par défaut hello</li></ul><p>Ouvrez hello `web.config` de fichiers pour le site/application hello et vérifiez qu’une balise de hello `<customErrors mode="RemoteOnly" />` ou `<customErrors mode="On" />` défini.</p>|

## <a id="deployment"></a>Définir la méthode de déploiement tooRetail dans IIS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Élément de déploiement (schéma des paramètres ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Étapes** | <p>Hello `<deployment retail>` commutateur est destiné aux serveurs IIS de production. Ce commutateur est utilisé toohelp aux applications d’exécuter avec des performances optimales hello et des informations de sécurité minimales fuites en désactivant hello la sortie de trace de l’application capacité toogenerate sur une page, la désactivation de la toodisplay de capacité hello d’erreur détaillés messages tooend utilisateurs et hello pour désactiver le commutateur de débogage.</p><p>Les commutateurs et les options destinés aux développeurs, comme le suivi et le débogage des échecs de demande, sont généralement activés pendant le développement actif. Il est recommandé de définir que la méthode de déploiement hello sur n’importe quel serveur de production tooretail. Ouvrez le fichier machine.config de hello et vérifiez que `<deployment retail="true" />` conserve la valeur tootrue.</p>|

## <a id="fail"></a>Les exceptions doivent échouer en toute sécurité

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Échec en toute sécurité](https://www.owasp.org/index.php/Fail_securely) |
| **Étapes** | L’application doit échouer en toute sécurité. Toute méthode renvoyant une valeur booléenne, en fonction de la décision prise, doit comporter un bloc d’exception créé avec soin. Il existe de nombreuses erreurs logiques en raison de l’escalade de problèmes de sécurité toowhich dans, lorsque le bloc d’exception hello est écrit sans.|

### <a name="example"></a>Exemple
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
Hello au-dessus de la méthode retourne toujours la valeur True, si une exception se produit. Si l’utilisateur final de hello fournit une URL incorrecte, qui hello navigateur égards, mais hello `Uri()` constructeur n’et une exception est levée victime de hello à entreprendre les URL valides mais incorrect toohello. 
