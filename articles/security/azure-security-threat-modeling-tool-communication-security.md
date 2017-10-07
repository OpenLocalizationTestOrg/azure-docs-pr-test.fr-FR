---
title: "aaaCommunication sécurité - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
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
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>Infrastructure de sécurité : sécurité des communications | Mesures de correction 
| Produit/Service | Article |
| --------------- | ------- |
| **Azure Event Hub** | <ul><li>[Une communication sécurisée tooEvent concentrateur à l’aide de SSL/TLS](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[Vérifiez le compte de service des privilèges et vérifiez que hello personnalisés des Services ou des Pages ASP.NET respectent la sécurité de CRM](#priv-aspnet)</li></ul> |
| **Azure Data Factory** | <ul><li>[Utiliser la passerelle de gestion des données lors de la connexion sur le serveur SQL local tooAzure Data Factory](#sqlserver-factory)</li></ul> |
| **IdentityServer** | <ul><li>[Vérifiez que tout le trafic tooIdentity serveur via une connexion HTTPS](#identity-https)</li></ul> |
| **Application web** | <ul><li>[Vérifiez que les certificats X.509 utilisé tooauthenticate des connexions SSL, TLS et DTLS](#x509-ssltls)</li><li>[Configurer le certificat SSL pour le domaine personnalisé dans Azure App Service](#ssl-appservice)</li><li>[Forcer tous les tooAzure de trafic du Service d’applications via une connexion HTTPS](#appservice-https)</li><li>[Activer le protocole HTTP Strict Transport Security (HSTS)](#http-hsts)</li></ul> |
| **Base de données** | <ul><li>[Assurer le chiffrement de la connexion SQL Server et la validation des certificats](#sqlserver-validation)</li><li>[Forcer le chiffrement communication tooSQL serveur](#encrypted-sqlserver)</li></ul> |
| **Azure Storage** | <ul><li>[Assurez-vous que tooAzure communication que stockage est effectuée via HTTPS](#comm-storage)</li><li>[Valider le hachage MD5 après le téléchargement de blobs si le protocole HTTPS ne peut pas être activé](#md5-https)</li><li>[Utiliser SMB 3.0 client compatible tooensure en transit tooAzure de chiffrement de données des partages de fichiers](#smb-shares)</li></ul> |
| **Client mobile** | <ul><li>[Implémenter l’épinglage de certificat](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[Activer le protocole HTTPS - Sécuriser le canal de transport](#https-transport)</li><li>[WCF : TooEncryptAndSign au niveau du Protection sécurité ensemble Message](#message-protection)</li><li>[WCF : Utiliser un compte le moins privilégié de toorun votre service WCF](#least-account-wcf)</li></ul> |
| **API Web** | <ul><li>[Forcer tooWeb trafic toutes les API via une connexion HTTPS](#webapi-https)</li></ul> |
| **Cache Redis Azure** | <ul><li>[Assurez-vous que tooAzure communication que cache Redis est via le protocole SSL](#redis-ssl)</li></ul> |
| **Passerelle de champ IoT** | <ul><li>[APPAREIL tooField passerelle communication sécurisée](#device-field)</li></ul> |
| **Passerelle de cloud IoT** | <ul><li>[Sécuriser l’appareil tooCloud communication de passerelle à l’aide de SSL/TLS](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>Une communication sécurisée tooEvent concentrateur à l’aide de SSL/TLS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Event Hub | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du modèle de sécurité et de l’authentification Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Étapes** | Sécuriser les connexions du protocole AMQP ou HTTP tooEvent concentrateur à l’aide de SSL/TLS |

## <a id="priv-aspnet"></a>Vérifiez le compte de service des privilèges et vérifiez que hello personnalisés des Services ou des Pages ASP.NET respectent la sécurité de CRM

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Vérifiez le compte de service des privilèges et vérifiez que hello personnalisés des Services ou des Pages ASP.NET respectent la sécurité de CRM |

## <a id="sqlserver-factory"></a>Utiliser la passerelle de gestion des données lors de la connexion sur le serveur SQL local tooAzure Data Factory

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Data Factory | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Types de services liés - Azure et local |
| **Informations de référence**              |[Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway), [Passerelle de gestion de données](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **Étapes** | <p>outil de passerelle de gestion des données (DMG) Hello est tooconnect requis toodata sources sont protégés derrière un pare-feu ou un réseau d’entreprise.</p><ol><li>Verrouillage de la machine de hello isole l’outil DMG hello et empêche les programmes ne fonctionnant pas correctement d’endommager ou de surveillance sur l’ordinateur de source de données hello. (Par exemple, les dernières mises à jour doivent être installées, activer le nombre minimal de ports requis, approvisionnement des comptes contrôlés, audit activé, chiffrement activé, etc.).</li><li>Clé de passerelle de données doit faire pivoter à intervalles fréquents ou chaque fois que le mot de passe du compte hello DMG service renouvelle</li><li>Les transits de données via le service lié doivent être chiffrés.</li></ol> |

## <a id="identity-https"></a>Vérifiez que tout le trafic tooIdentity serveur via une connexion HTTPS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | IdentityServer | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [IdentityServer3 - Keys, Signatures and Cryptography](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) (IdentityServer3 - Clés, signatures et chiffrement), [IdentityServer3 - Deployment](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) (IdentityServer3 - Déploiement) |
| **Étapes** | Par défaut, IdentityServer requiert tous les toocome les connexions entrantes via le protocole HTTPS. Il est absolument indispensable que les communications avec IdentityServer s’effectuent sur les transports sécurisés uniquement. Il existe certains scénarios de déploiement (p. ex. déchargement SSL) dans lesquels cette exigence peut être assouplie. Consultez la page de déploiement de serveur d’identités hello dans les références de hello pour plus d’informations. |

## <a id="x509-ssltls"></a>Vérifiez que les certificats X.509 utilisé tooauthenticate des connexions SSL, TLS et DTLS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Les applications qui utilisent le protocole SSL, TLS et DTLS doivent vérifier les certificats X.509 hello d’entités hello à qu'ils se connectent. Cela inclut la vérification des certificats hello pour :</p><ul><li>Nom de domaine</li><li>Dates de validité (dates de début et dates d’échéance).</li><li>État de révocation.</li><li>Utilisation (par exemple, authentification serveur pour les serveurs, authentification client pour les clients).</li><li>Chaîne d’approbation. Certificats doivent être associés tooa autorité de certification (CA) qui est approuvée par la plateforme de hello ou configurée de manière explicite par l’administrateur de hello</li><li>La longueur de clé de la clé publique du certificat doit être supérieure à 2 048 bits.</li><li>L’algorithme de hachage doit être SHA256 et supérieur. |

## <a id="ssl-appservice"></a>Configurer le certificat SSL pour le domaine personnalisé dans Azure App Service

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | EnvironmentType - Azure |
| **Informations de référence**              | [Activer le protocole HTTPS pour une application dans Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **Étapes** | Par défaut, Azure permet déjà de HTTPS pour chaque application avec un certificat générique pour hello *. domaine azurewebsites.net. Comme tous les domaines génériques, il n’est cependant pas aussi sécurisé qu’un domaine personnalisé avec votre propre certificat. [Consultez cet article](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/). Il est recommandé de tooenable SSL pour le domaine personnalisé de hello application hello déployé est accessible via|

## <a id="appservice-https"></a>Forcer tous les tooAzure de trafic du Service d’applications via une connexion HTTPS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | EnvironmentType - Azure |
| **Informations de référence**              | [Exécution de SSL sur votre application] https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app) |
| **Étapes** | <p>Bien que Azure permet déjà de HTTPS pour les services d’application Azure avec un certificat générique pour le domaine de hello *. azurewebsites.net, il n’appliquent pas HTTPS. Les visiteurs peuvent toujours accéder à application hello à l’aide de HTTP, ce qui peut compromettre la sécurité de l’application hello et par conséquent HTTPS a toobe appliquée de manière explicite. Les applications ASP.NET MVC doivent utiliser hello [RequireHttps filtre](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) qui force une toobe de demande HTTP non sécurisée via HTTPS.</p><p>Module de réécriture d’URL hello, qui est inclus avec le Service d’application Azure peut également être utilisé tooenforce HTTPS. Module de réécriture d’URL permet aux développeurs toodefine les règles appliquées tooincoming demandes avant que les demandes de hello sont remis tooyour application. Règles de réécriture d’URL sont définies dans un fichier web.config stocké dans l’application hello racine hello</p>|

### <a name="example"></a>Exemple
exemple Hello contient une règle de réécriture d’URL base qui force tout trafic entrant toouse le trafic HTTPS
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
Cette règle s’applique en retournant un code d’état HTTP de 301 (redirection permanente) lorsque les utilisateur hello demande une page à l’aide de HTTP. Hello effectue une redirection 301 hello demande toohello même URL en tant que visiteur de hello demandé, mais remplace hello HTTP partie de requête hello avec HTTPS. Par exemple, HTTP://contoso.com serait tooHTTPS://contoso.com redirigé. 

## <a id="http-hsts"></a>Activer le protocole HTTP Strict Transport Security (HSTS)

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [OWASP HTTP Strict Transport Security Cheat Sheet](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) (Aide-mémoire sur HTTP Strict Transport Security par l’OWASP) |
| **Étapes** | <p>Sécurité HTTP du Transport Strict (HSTS) est une amélioration de l’inclusion de sécurité qui est spécifiée par une application web via l’utilisation de hello d’un en-tête de réponse particulière. Une fois qu’un navigateur pris en charge reçoit cet en-tête ce navigateur empêche les communications provenant envoyées sur le domaine spécifié de toohello HTTP et l’envoie à la place toutes les communications via le protocole HTTPS. Il empêche également les invites HTTPS sur lesquelles cliquer sur les navigateurs.</p><p>tooimplement HSTS, hello suivant l’en-tête de réponse a toobe configuré globalement, pour un site Web dans le code ou dans la configuration. Strict-Transport-Security : max-age = 300 ; includeSubDomains HSTS adresses hello suivant des menaces :</p><ul><li>Utilisateur insère les signets ou manuellement types http://example.com et qui est la personne malveillante de sujet tooa man-in-the-middle : HSTS redirige automatiquement tooHTTPS de requêtes HTTP pour le domaine cible de hello</li><li>Application qui est prévu toobe purement HTTPS contient des liens HTTP par inadvertance ou fait Office de contenu sur HTTP Web : HSTS redirige automatiquement tooHTTPS de requêtes HTTP pour le domaine cible de hello</li><li>Un intrus de man-in-the-middle tente de trafic toointercept à partir d’un utilisateur cible à l’aide d’un certificat non valide et espère utilisateur de hello acceptera certificat incorrect de hello : HSTS n’autorise pas un message de certificat non valide de hello toooverride utilisateur</li></ul>|

## <a id="sqlserver-validation"></a>Assurer le chiffrement de la connexion SQL Server et la validation des certificats

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure  |
| **Attributs**              | Version SQL - V12 |
| **Informations de référence**              | [Best Practices on Writing Secure Connection Strings for SQL Database](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) (Bonnes pratiques sur l’écriture de chaînes de connexion sécurisées pour SQL Database) |
| **Étapes** | <p>Toutes les communications entre SQL Database et une application cliente sont chiffrées en permanence à l’aide du protocole Secure Sockets Layer (SSL). SQL Database ne prend pas en charge les connexions non chiffrées. certificats toovalidate avec le code d’application ou les outils, demander une connexion chiffrée et ne faites pas confiance à des certificats de serveur hello explicitement. Si le code ou les outils de votre application ne demandent pas une connexion chiffrée, ils recevront pourtant des connexions chiffrées.</p><p>Cependant, ils peuvent ne pas valider les certificats de serveur hello et seront donc vulnérables trop au milieu de hello attaques « ». certificats toovalidate avec le code d’application ADO.NET, `Encrypt=True` et `TrustServerCertificate=False` dans la chaîne de connexion de base de données hello. certificats toovalidate via SQL Server Management Studio, ouvrez la boîte de dialogue de tooServer de se connecter hello. Cliquez sur l’onglet des propriétés de connexion hello chiffrer la connexion</p>|

## <a id="encrypted-sqlserver"></a>Forcer le chiffrement communication tooSQL serveur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Local |
| **Attributs**              | Version SQL - MsSQL2016, Version SQL - MsSQL2012, Version SQL - MsSQL2014 |
| **Informations de référence**              | [Activer les connexions chiffrées toohello du moteur de base de données](https://msdn.microsoft.com/library/ms191192)  |
| **Étapes** | L’activation de SSL chiffrement accroît la sécurité de hello des données transmises sur des réseaux entre des instances de SQL Server et des applications. |

## <a id="comm-storage"></a>Assurez-vous que tooAzure communication que stockage est effectuée via HTTPS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Chiffrement au niveau du transport – Utilisation de HTTPS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **Étapes** | sécurité de hello tooensure de stockage Azure données en transit, utilisez toujours le protocole HTTPS hello lors de l’appel d’API REST de hello ou l’accès à des objets dans le stockage. En outre, les Signatures d’accès partagé, qui peut être utilisé toodelegate accéder aux objets de stockage tooAzure, incluent une option toospecify que hello uniquement le protocole HTTPS peut être utilisé lors de l’utilisation de Signatures d’accès partagé, garantissant que toute personne envoyant des liens avec des jetons SAS sera Utilisez le protocole approprié de hello.|

## <a id="md5-https"></a>Valider le hachage MD5 après le téléchargement de blobs si le protocole HTTPS ne peut pas être activé

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | StorageType - Blob |
| **Informations de référence**              | [Windows Azure Blob MD5 Overview](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/) (Vue d’ensemble de la vérification MD5 du service Blob Windows Azure) |
| **Étapes** | <p>Service d’objets Blob Windows Azure fournit des mécanismes tooensure l’intégrité des données à la fois à l’application hello et les couches de transport. Si pour une raison quelconque, vous devez toouse HTTP au lieu de HTTPS et que vous travaillez avec des objets BLOB de blocs, vous pouvez utiliser la vérification de MD5 toohelp vérifier l’intégrité de hello d’objets BLOB de hello en cours de transfert</p><p>Ceci contribuera à la protection contre les erreurs au niveau du réseau/transport, mais pas nécessairement contre les attaques intermédiaires. Si vous pouvez utiliser le protocole HTTPS, qui fournit une sécurité au niveau du transport, alors l’utilisation de la vérification MD5 est redondant et inutile.</p>|

## <a id="smb-shares"></a>Utilisez les partages de fichiers SMB 3.0 client compatible tooensure les données en transit chiffrement tooAzure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client mobile | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | StorageType - Fichier |
| **Informations de référence**              | [Azure File Storage, now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931) (Le stockage de fichiers Azure est désormais disponible de manière générale), [Prise en main du stockage de fichiers Azure sur Windows](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **Étapes** | Stockage de fichier Azure prend en charge HTTPS lors de l’utilisation des API REST de hello, mais il est plus couramment utilisé comme un partage de fichiers SMB attaché tooa machine virtuelle. SMB 2.1 ne prend pas en charge le chiffrement, les connexions sont uniquement autorisées au sein de hello même région dans Azure. Toutefois, SMB 3.0 prend en charge le chiffrement et peut être utilisé avec Windows Server 2012 R2, Windows 8, Windows 8.1 et Windows 10, ce qui permet d’entre régions accéder et même des accès sur le bureau de hello. |

## <a id="cert-pinning"></a>Implémenter l’épinglage de certificat

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, Windows Phone |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Certificate and Public Key Pinning](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net) (Épinglage de clé publique et de certificat) |
| **Étapes** | <p>L’épinglage de certificat assure une protection contre les interceptions. L’épinglage est processus hello d’association d’un ordinateur hôte à leurs X509 attendu certificat ou clé publique. Une fois qu’un certificat ou la clé publique est altérée ou affichée pour un ordinateur hôte, certificat de hello ou clé publique est associé ou 'épinglé' toohello hôte. </p><p>Par conséquent, lorsqu’un adversaire tente toodo attaque MITM de SSL de, au cours de la clé de hello la négociation SSL de serveur sera différente de hello épinglé clé du certificat et demande de hello est ignorée, empêchant le certificat de l’intercepteur épinglage peut être obtenue en implémentation de ServicePointManager `ServerCertificateValidationCallback` déléguer.</p>|

### <a name="example"></a>Exemple
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>Activer le protocole HTTPS - Sécuriser le canal de transport

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | configuration de l’application Hello doit garantir que HTTPS est utilisé pour toutes les informations de toosensitive d’accès.<ul><li>**Explication :** si une application gère les informations sensibles et n’utilise pas le chiffrement au niveau du message, il doit uniquement pouvoir toocommunicate sur un canal de transport chiffrées.</li><li>**RECOMMANDATIONS :** assurez-vous que le transport HTTP est désactivé et activez le transport HTTPS à la place. Par exemple, remplacez hello `<httpTransport/>` avec `<httpsTransport/>` balise. Ne comptez pas sur un tooguarantee (pare-feu) de configuration de réseau qu’application hello uniquement accessibles via un canal sécurisé. À partir d’un point de vue philosophique, application hello ne doit pas dépendre réseau hello pour sa sécurité.</li></ul><p>À partir d’un point de vue pratique, hello responsables de la sécurisation de hello réseau ne suivent pas les toujours les exigences de sécurité hello de l’application hello lorsqu’elles évoluent.</p>|

## <a id="message-protection"></a>WCF : TooEncryptAndSign au niveau du Protection sécurité ensemble Message

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **Étapes** | <ul><li>**Explication :** lorsque le niveau de Protection a la valeur « none » sera désactivée protection des messages trop. La confidentialité et l’intégrité sont obtenues grâce à un niveau approprié de paramétrage.</li><li>**RECOMMANDATIONS :**<ul><li>Quand `Mode=None`, la protection des messages est désactivée.</li><li>Lorsque `Mode=Sign` -signes mais ne chiffre pas de message de type hello ; doit être utilisées lors de l’intégrité des données sont important</li><li>Lorsque `Mode=EncryptAndSign` -signe et chiffre le message de type hello</li></ul></li></ul><p>Envisagez de désactiver le chiffrement et la signature uniquement votre message lorsque vous devez simplement l’intégrité de hello toovalidate d’informations hello sans problèmes de confidentialité. Cela peut être utile pour les opérations ou les contrats de service dans lequel vous avez besoin de l’expéditeur d’origine de toovalidate hello mais aucune donnée sensible n’est transmise. Lors de la réduction de niveau de protection hello, veillez à que ce message de type hello ne contient pas toutes les informations d’identification personnelle (PII).</p>|

### <a name="example"></a>Exemple
Configuration de service de hello et message de type hello signe tooonly opération hello est illustrée dans hello exemple suivant. Exemple de contrat de service de `ProtectionLevel.Sign`: hello Voici un exemple d’utilisation de ProtectionLevel.Sign au niveau du contrat de Service hello : 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>Exemple
Exemple de contrat d’opération de `ProtectionLevel.Sign` (pour un contrôle granulaire) : hello Voici un exemple d’utilisation `ProtectionLevel.Sign` à hello OperationContract niveau :

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>WCF : Utiliser un compte le moins privilégié de toorun votre service WCF

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **Étapes** | <ul><li>**EXPLICATION :** n’exécutez pas de services WCF sous un compte administrateur ou avec des privilèges élevés. En cas de compromission des services, l’impact sera important.</li><li>**RECOMMANDATIONS :** utiliser un toohost compte le moins privilégié votre WCF du service, car elle réduit la surface d’attaque de votre application et réduire les dommages potentiels hello si vous sont d’une attaque. Si le compte de service hello requiert des droits d’accès supplémentaires sur les ressources d’infrastructure, tels que MSMQ, hello autorisations appropriées de journal des événements et compteurs de performances système de fichiers hello, il convient les ressources toothese afin que le service WCF de hello peut s’exécuter avec succès.</li></ul><p>Si votre service doit tooaccess des ressources spécifiques pour le compte de l’appelant initial hello, utilisez l’emprunt d’identité et l’identité de l’appelant de délégation tooflow hello pour une vérification d’autorisation en aval. Dans un scénario de développement, utilisez le compte de service de réseau local hello, qui est un compte spécial intégré qui dispose de privilèges réduits. Dans un scénario de production, créez un compte de service de domaine personnalisé avec des privilèges minimum.</p>|

## <a id="webapi-https"></a>Forcer tooWeb trafic toutes les API via une connexion HTTPS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Enforcing SSL in a Web API Controller](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) (Application de SSL dans un contrôleur d’API Web) |
| **Étapes** | Si une application possède à la fois une liaison HTTP et HTTPS, les clients peuvent toujours utiliser site hello de tooaccess HTTP. tooprevent cela, utilisez un tooensure de filtre d’action qui demande tooprotected API sont toujours via HTTPS.|

### <a name="example"></a>Exemple 
Hello de code suivant montre un filtre API Web d’authentification qui vérifie si SSL : 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
Ajouter ce filtre tooany des actions API Web nécessitant SSL : 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>Assurez-vous que tooAzure communication que cache Redis est via le protocole SSL

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Cache Redis Azure | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Forum aux questions sur le Cache Redis Azure](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **Étapes** | Redis serveur ne prend pas en charge SSL en dehors de la zone de hello, contrairement à un Cache Redis Azure. Si vous vous connectez tooAzure Cache Redis et que votre client prend en charge SSL, comme StackExchange.Redis, vous devez utiliser SSL. Par défaut, le port non SSL est désactivé pour les nouvelles instances Cache Redis Azure. Assurez-vous que les paramètres par défaut sécurisés hello ne sont pas modifiés sauf s’il existe une dépendance sur la prise en charge SSL pour les clients redis. |

Notez que Redis est conçue toobe accessible par les clients approuvés dans les environnements approuvés. Cela signifie que généralement il n’est pas une bonne idée tooexpose hello Redis instance directement toohello internet ou, en général, environnement tooan où les clients non approuvés peuvent accéder directement à hello le port TCP de Redis ou un socket d’UNIX. 

## <a id="device-field"></a>APPAREIL tooField passerelle communication sécurisée

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de champ IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Pour les appareils basé sur IP, le protocole de communication hello peut généralement être encapsulé dans un SSL/TLS canal tooprotect transfert de données. Pour les autres protocoles qui ne prennent pas en charge SSL/TLS, vérifiez s’il existe des versions sécurisées de protocole de hello qui offrent une sécurité au niveau de la couche de transport ou du message. |

## <a id="device-cloud"></a>Sécuriser l’appareil tooCloud communication de passerelle à l’aide de SSL/TLS

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Guide du développeur Azure IoT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **Étapes** | Sécuriser les protocoles HTTP/AMQP ou MQTT à l’aide du protocole SSL/TLS. |
