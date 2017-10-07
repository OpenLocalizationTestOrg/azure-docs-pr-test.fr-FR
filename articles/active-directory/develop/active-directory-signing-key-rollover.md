---
title: "Substitution des clés dans Azure AD d’aaaSigning | Documents Microsoft"
description: "Cet article traite des meilleures pratiques de la substitution de la clé de signature pour Azure Active Directory de hello"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Substitution de la clé de signature dans Azure Active Directory
Cette rubrique explique ce que vous devez tooknow sur les clés publiques hello sont utilisées dans les jetons de sécurité Azure Active Directory (Azure AD) toosign. Il est important toonote que ces clés sont remplacées régulièrement et, en cas d’urgence, peut être déployée sur immédiatement. Toutes les applications qui utilisent Azure AD doivent être en mesure de tooprogrammatically handle hello substitution de clé processus ou établir un processus de substitution manuelle périodique. Continuer à lire toounderstand comment les clés hello fonctionnent, comment tooassess hello impact de l’application de tooyour substitution hello et tooupdate votre application ou une substitution de clé de substitution manuelle périodique processus toohandle à établir si nécessaire.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Vue d’ensemble des clés de signature dans Azure AD
Azure AD utilise le chiffrement de clé publique générée sur secteur normes tooestablish approbation entre lui-même et hello applications qui l’utilisent. En pratique, cela fonctionne dans hello suivant : Azure AD utilise une clé de signature qui se compose d’une paire de clés publique et privée. Lorsqu’un utilisateur se connecte tooan application qui utilise Azure AD pour l’authentification, Azure AD crée un jeton de sécurité qui contient des informations sur l’utilisateur de hello. Ce jeton est signé par Azure AD à l’aide de sa clé privée avant son envoi différé toohello application. tooverify hello jeton est valide et provient bien d’Azure AD, l’application hello doit valider la signature du jeton hello à l’aide de la clé publique de hello exposé par Azure AD, qui est contenue dans le locataire hello [document de découverte OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) ou SAML/WS-Fed [document de métadonnées de fédération](active-directory-federation-metadata.md).

Pour des raisons de sécurité clé restaure de manière périodique et, dans les cas de hello d’urgence, la signature d’Azure AD peut être annulés immédiatement. Toute application qui s’intègre à Azure AD doit être préparée toohandle un événement de substitution de clé quel que soit la fréquence à laquelle il peut se produire. Si ce n’est pas et que votre application tente de toouse une signature de hello tooverify clés ayant expiré sur un jeton, la demande de connexion hello échoue.

Plus d’une clé valide est toujours disponible dans le document de découverte OpenID Connect hello et le document de métadonnées de fédération hello. Votre application doit être préparée toouse toutes les clés de hello spécifié dans le document de hello, car une clé peut être changée rapidement, un autre peut être son remplacement et ainsi de suite.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>Comment tooassess si votre application est affectée et le toodo concernant
Comment votre application gère la substitution de clé dépend de variables telles que de type hello d’application ou le protocole d’identité et de la bibliothèque a été utilisée. les sections Hello ci-dessous évaluer si les types courants de hello d’applications sont affectées par la substitution de clé hello et fournissent des conseils sur la façon dont tooupdate hello la substitution automatique des applications toosupport ou mettre à jour manuellement la clé de hello.

* [Applications clientes natives ayant accès aux ressources](#nativeclient)
* [Applications web/API ayant accès aux ressources](#webclient)
* [Applications web/API protégeant les ressources et créées à l’aide d’Azure App Services](#appservices)
* [Applications web/API protégeant les ressources à l’aide du middleware .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication](#owin)
* [Applications web/API protégeant les ressources à l’aide du middleware .NET Core OpenID Connect ou JwtBearerAuthentication](#owincore)
* [Applications web/API protégeant les ressources à l’aide du module passport-azure-ad Node.js](#passport)
* [Applications web/API protégeant les ressources et créées avec Visual Studio 2015 ou Visual Studio 2017](#vs2015)
* [Applications web protégeant les ressources et créées avec Visual Studio 2013](#vs2013)
* [API web protégeant les ressources et créées avec Visual Studio 2013](#vs2013_webapi)
* [Applications web protégeant les ressources et créées avec Visual Studio 2012](#vs2012)
* [Applications web protégeant les ressources et créées avec Visual Studio 2010, 2008 ou avec Windows Identity Foundation](#vs2010)
* [Applications Web / API de protection des ressources à l’aide d’un autres bibliothèques ou implémenter manuellement hello protocoles pris en charge](#other)

Ce guide n’est **pas** applicable aux :

* Les applications ajoutées à partir de la galerie d’applications Azure AD (y compris personnalisé) ont des directives spécifiques avec des clés de toosigning ce qui concerne les. [Plus d’informations.](../active-directory-sso-certs.md)
* Les applications publiées via le proxy d’application n’ont pas tooworry sur les clés de signature sur site.

### <a name="nativeclient"></a>Applications clientes natives ayant accès aux ressources
En général, les applications qui ont uniquement accès aux ressources (par exemple, Microsoft Graph, KeyVault, API d’Outlook et d’autres APIs Microsoft) en général uniquement obtenir un jeton et transmettre toohello propriétaire de la ressource. Étant donné qu’ils ne protègent pas toutes les ressources, ils n’inspectent pas de jeton de hello et est donc inutile de tooensure qu’il est correctement signé.

Si l’ordinateur de bureau ou mobile, les applications clientes natives, appartiennent à cette catégorie et ne sont donc pas affectées par la substitution de hello.

### <a name="webclient"></a>Applications web/API ayant accès aux ressources
En général, les applications qui ont uniquement accès aux ressources (par exemple, Microsoft Graph, KeyVault, API d’Outlook et d’autres APIs Microsoft) en général uniquement obtenir un jeton et transmettre toohello propriétaire de la ressource. Étant donné qu’ils ne protègent pas toutes les ressources, ils n’inspectent pas de jeton de hello et est donc inutile de tooensure qu’il est correctement signé.

Applications et web API qui est à l’aide de flux d’application uniquement hello (informations d’identification de client / certificat client), appartiennent à cette catégorie et ne sont donc pas affectées par la substitution de hello.

### <a name="appservices"></a>Applications web/API protégeant les ressources et créées à l’aide d’Azure App Services
L’authentification des Services App Azure / de la fonctionnalité d’autorisation (EasyAuth) a déjà substitution de la logique nécessaire hello toohandle clé automatiquement.

### <a name="owin"></a>Applications web/API protégeant les ressources à l’aide du middleware .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication
Si votre application utilise hello .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication intergiciel (middleware), il est déjà substitution de la logique nécessaire hello toohandle clé automatiquement.

Vous pouvez vérifier que votre application utilise l’un de ces éléments en recherchant les Hello suivant des extraits de code dans votre application Startup.cs ou Startup.Auth.cs

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>Applications web/API protégeant les ressources à l’aide du middleware .NET Core OpenID Connect ou JwtBearerAuthentication
Si votre application utilise hello .NET Core OWIN OpenID Connect ou JwtBearerAuthentication intergiciel (middleware), il est déjà substitution de la logique nécessaire hello toohandle clé automatiquement.

Vous pouvez vérifier que votre application utilise l’un de ces éléments en recherchant les Hello suivant des extraits de code dans votre application Startup.cs ou Startup.Auth.cs

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>Applications web/API protégeant les ressources à l’aide du module passport-azure-ad Node.js
Si votre application utilise le module de passport-ad Node.js hello, il est déjà substitution de la logique nécessaire hello toohandle clé automatiquement.

Vous pouvez vous assurer que votre application passport-ad en recherchant des hello suivant extrait de code dans votre application app.js

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>Applications web/API protégeant les ressources et créées avec Visual Studio 2015 ou Visual Studio 2017
Si vous avez sélectionné et que votre application a été créée à l’aide d’un modèle d’application web dans Visual Studio 2015 ou Visual Studio 2017 **travail et les comptes d’établissement scolaire** de hello **modifier l’authentification** menu, il déjà a la substitution de la logique nécessaire hello toohandle clé automatiquement. Cette logique, incorporée dans le middleware OWIN OpenID Connect de hello, récupère et met en cache les clés hello à partir du document de découverte OpenID Connect hello et actualise régulièrement les.

Si vous avez ajouté manuellement solution tooyour d’authentification, votre application ne peut pas avoir logique de substitution de clé nécessaire hello. Vous devez toowrite il vous-même ou hello de suivre les étapes [applications Web API à l’aide de toutes les autres bibliothèques ou implémenter manuellement hello pris en charge les protocoles.](#other).

### <a name="vs2013"></a>Applications web protégeant les ressources et créées avec Visual Studio 2013
Si votre application a été créée à l’aide d’un modèle d’application web dans Visual Studio 2013 et que vous avez sélectionné **comptes professionnels** de hello **modifier l’authentification** menu, il a déjà hello nécessaire logique toohandle automatiquement de substitution de clé. Cette logique stocke l’identificateur unique de votre organisation et hello dans deux tables de base de données associés hello projet des informations de clé de signature. Vous trouverez des chaîne de connexion hello pour la base de données hello dans le fichier Web.config du projet hello.

Si vous avez ajouté manuellement solution tooyour d’authentification, votre application ne peut pas avoir logique de substitution de clé nécessaire hello. Vous devez toowrite il vous-même ou hello de suivre les étapes [applications Web API à l’aide de toutes les autres bibliothèques ou implémenter manuellement hello pris en charge les protocoles.](#other).

Hello suit vous permet de vérifier que la logique hello fonctionne correctement dans votre application.

1. Dans Visual Studio 2013, ouvrez la solution de hello, puis sur hello **l’Explorateur de serveurs** onglet hello fenêtre de droite.
2. Développez **Connexions de données**, **DefaultConnection**, puis **Tables**. Recherchez hello **IssuingAuthorityKeys** table, faites un clic droit, puis cliquez sur **afficher les données de Table**.
3. Bonjour **IssuingAuthorityKeys** table, il y aura au moins une ligne, ce qui correspond la valeur d’empreinte numérique toohello pour la clé de hello. Supprimer des lignes dans la table de hello.
4. Avec le bouton hello **locataires** de table, puis cliquez sur **afficher les données de Table**.
5. Bonjour **locataires** table, il y aura au moins une ligne, laquelle correspond l’identificateur du locataire tooa répertoire unique. Supprimer des lignes dans la table de hello. Si vous ne supprimez pas les lignes hello dans les deux hello **locataires** table et **IssuingAuthorityKeys** table, vous obtiendrez une erreur lors de l’exécution.
6. Générez et exécutez l’application hello. Une fois que vous êtes connecté tooyour compte, vous pouvez arrêter l’application hello.
7. Retourner toohello **l’Explorateur de serveurs** et observer les valeurs hello Bonjour **IssuingAuthorityKeys** et **locataires** table. Vous remarquerez qu’ils ont été complétées automatiquement avec les informations appropriées hello à partir du document de métadonnées de fédération hello.

### <a name="vs2013"></a>API web protégeant les ressources et créées avec Visual Studio 2013
Si vous créé une application de l’API web dans Visual Studio 2013 à l’aide du modèle d’API Web hello, puis sélectionné **comptes professionnels** de hello **modifier l’authentification** menu, déjà hello logique nécessaire dans votre application.

Si vous avez configuré manuellement l’authentification, suivez les instructions de hello sous toolearn comment tooconfigure tooautomatically de votre API Web mettre à jour ses informations de clé.

Hello extrait de code suivant montre comment tooget hello dernières clés à partir du document de métadonnées de fédération hello et ensuite utiliser hello [Gestionnaire de jetons JWT](https://msdn.microsoft.com/library/dn205065.aspx) jeton de hello toovalidate. extrait de code Hello part du principe que vous allez utiliser votre propre mécanisme de persistance toovalidate clé de hello future de la mise en cache des jetons d’Azure AD, que ce soit dans une base de données, le fichier de configuration ou ailleurs.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Applications web protégeant les ressources et créées avec Visual Studio 2012
Si votre application a été créée dans Visual Studio 2012, vous avez probablement utilisé hello identité et outil d’accès aux tooconfigure votre application. Il est également probable que vous utilisez hello [validation émetteur de nom de Registre (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Hello VINR est chargé de gérer les informations sur les fournisseurs d’identité approuvés (Azure AD) et les clés de hello utilisées toovalidate les jetons émis par eux. Hello VINR rend également facile tooautomatically mise à jour hello informations de clé stockées dans un fichier Web.config en téléchargeant hello dernier fédération document de métadonnées associé à votre annuaire, en vérifiant si la configuration de hello est obsolète par hello plus récentes document et mise à jour hello toouse hello nouvelle clé d’application si nécessaire.

Si vous avez créé votre application à l’aide d’un des exemples de code hello ou de la documentation détaillée fournis par Microsoft, la logique de substitution de clé hello est déjà incluse dans votre projet. Vous remarquerez que code hello ci-dessous existe déjà dans votre projet. Si votre application n’a pas déjà cette logique, suivez les étapes de hello ci-dessous tooadd et tooverify fonctionne correctement.

1. Dans **l’Explorateur de solutions**, ajoutez une référence toohello **System.IdentityModel** assembly pour le projet approprié de hello.
2. Ouvrez hello **Global.asax.cs** de fichier et ajoutez hello qui suit à l’aide de directives :
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Ajouter hello suivant de méthode toohello **Global.asax.cs** fichier :
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Appeler hello **RefreshValidationSettings()** méthode Bonjour **Application_Start()** méthode dans **Global.asax.cs** comme indiqué :
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

Une fois que vous avez suivi ces étapes, le fichier Web.config de votre application sera mis à jour avec hello dernières informations du document de métadonnées de fédération hello, y compris les dernières clés de hello. Cette mise à jour se produit chaque fois que votre pool d’applications est recyclé dans IIS. par défaut IIS a la valeur toorecycle applications toutes les 29 heures.

Suivez les étapes de hello ci-dessous tooverify fonctionnement de la logique de substitution de clé hello.

1. Après avoir vérifié que votre application à l’aide de code hello ci-dessus, ouvrez hello **Web.config** de fichiers et accédez toohello  **<issuerNameRegistry>**  bloc, spécifiquement pour hello quelques lignes suivantes :
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. Bonjour  **<add thumbprint=””>**  définir, modifier valeur d’empreinte numérique hello en remplaçant les caractères à une autre. Enregistrer hello **Web.config** fichier.
3. Générez l’application hello et exécutez-le. Si vous pouvez terminer le processus de connexion hello, votre application est correctement mise à jour de clé de hello en téléchargeant les informations hello requis à partir du document de métadonnées de fédération de votre annuaire. Si vous rencontrez des problèmes de connexion, vérifiez les modifications de hello dans votre application sont correctes en lisant hello [tooYour Ajout de l’authentification à l’aide d’applications Web Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) rubrique, ou de télécharger et en inspectant hello suivant l’exemple de code : [ Une Application Cloud mutualisée pour Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Applications web protégeant les ressources et créées avec Visual Studio 2008 ou 2010 et avec Windows Identity Foundation (WIF) version 1.0 pour .NET 3.5
Si vous avez créé une application sur WIF v1.0, il n’est aucune actualisation de tooautomatically mécanisme toouse de configuration de votre application une nouvelle clé.

* *Moyen le plus simple* utiliser les outils de FedUtil hello inclus dans hello WIF SDK, qui peut récupérer le dernier document de métadonnées hello et mettre à jour votre configuration.
* Mettre à jour votre too.NET application 4.5, qui inclut la version la plus récente de WIF dans l’espace de noms système hello hello. Vous pouvez ensuite utiliser hello [validation émetteur de nom de Registre (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform les mises à jour automatiques de la configuration de l’application hello.
* Effectuer une restauration manuelle conformément aux instructions hello à fin hello de ce guide.

Instructions toouse hello FedUtil tooupdate votre configuration :

1. Vérifiez que vous avez hello WIF v1.0 SDK installé sur votre ordinateur de développement pour Visual Studio 2008 ou 2010. Dans le cas contraire, vous pouvez [le télécharger ici](https://www.microsoft.com/en-us/download/details.aspx?id=4451).
2. Dans Visual Studio, ouvrez la solution de hello, puis cliquez sur le projet applicable de hello et sélectionnez **mettre à jour des métadonnées de fédération**. Si cette option n’est pas disponible, FedUtil et/ou hello WIF v1.0 SDK n’a pas été installé.
3. À partir de l’invite de commandes hello, sélectionnez **mise à jour** toobegin mise à jour les métadonnées de fédération. Si vous avez accès toohello server environnement où l’application hello est hébergée, vous pouvez éventuellement utiliser FedUtil [Planificateur de mise à jour automatique des métadonnées](https://msdn.microsoft.com/library/ee517272.aspx).
4. Cliquez sur **Terminer** processus de mise à jour toocomplete hello.

### <a name="other"></a>Applications Web / API de protection des ressources à l’aide d’un autres bibliothèques ou implémenter manuellement hello protocoles pris en charge
Si vous utilisez une autre bibliothèque ou implémentée manuellement un des protocoles de hello pris en charge, vous aurez besoin de bibliothèque de hello tooreview ou tooensure votre implémentation qui hello clé est récupérée sur le document de découverte OpenID Connect hello ou hello document de métadonnées de fédération. Une façon toocheck pour ce est toodo une recherche dans votre code ou de la bibliothèque hello pour les appels de n’importe quel document de découverte OpenID tooeither hello ou le document de métadonnées de fédération hello.

Si la clé est stocké ailleurs ou codé en dur dans votre application, vous pouvez manuellement récupérer la clé de hello et mise à jour il en conséquence effectuer une restauration manuelle conformément aux instructions hello à fin hello de ce guide. **Il est fortement recommandé que vous améliorez la substitution automatique des toosupport votre application** à l’aide de hello est proche de plan dans cette surcharge et les interruptions de futures tooavoid article si Azure AD augmente sa cadence de substitution ou a une substitution d’out-of-band d’urgence.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Comment tootest votre toodetermine application si elle est affectée
Vous pouvez vérifier si votre application prend en charge la substitution automatique de la clé en téléchargeant les scripts de hello et en suivant les instructions de hello dans [ce référentiel GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>Comment tooperform une restauration manuelle si votre application ne prend pas en charge la substitution automatique
Si votre application ne **pas** prend en charge la substitution automatique, vous devez tooestablish un processus qui régulièrement moniteurs Azure AD de signature des clés et effectue une restauration manuelle en conséquence. [Ce référentiel GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contient des scripts et des instructions sur la façon de toodo cela.

