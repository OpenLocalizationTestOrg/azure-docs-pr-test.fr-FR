---
title: "aaaSensitive données - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
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
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>Infrastructure de sécurité : Données sensibles | Mesures de correction 
| Produit/Service | Article |
| --------------- | ------- |
| **Délimitation d’approbation machine** | <ul><li>[S’assurer que les fichiers binaires sont masqués s’ils contiennent des informations sensibles](#binaries-info)</li><li>[Pensez à l’aide du système EFS (Encrypted File System) est utilisé tooprotect des données confidentielles spécifiques à l’utilisateur](#efs-user)</li><li>[Assurez-vous que les données sensibles stockées par l’application hello sur le système de fichiers hello sont chiffrées.](#filesystem)</li></ul> | 
| **Application web** | <ul><li>[Assurez-vous que le contenu sensible n’est pas mis en cache sur le navigateur de hello](#cache-browser)</li><li>[Chiffrer les sections des fichiers de configuration de l’application web qui contiennent des données sensibles](#encrypt-data)</li><li>[Désactiver explicitement les attributs HTML hello la saisie semi-automatique dans les formulaires sensibles et les entrées](#autocomplete-input)</li><li>[Assurez-vous que les données sensibles affichées sur l’écran hello utilisateur sont masquées](#data-mask)</li></ul> | 
| **Base de données** | <ul><li>[Implémenter des utilisateurs de masquage exposition des données sensibles toolimit non privilégié de données dynamiques](#dynamic-users)</li><li>[S’assurer que les mots de passe sont stockés dans un format de hachage salé](#salted-hash)</li><li>[S’assurer que les données sensibles des colonnes de la base de données sont chiffrées](#db-encrypted)</li><li>[S’assurer que le chiffrement au niveau de la base de données est activé](#tde-enabled)</li><li>[S’assurer que les sauvegardes de base de données sont chiffrées](#backup)</li></ul> | 
| **API Web** | <ul><li>[Assurez-vous que tooWeb pertinentes des données sensibles QU'API ne sont pas stockée dans le stockage du navigateur](#api-browser)</li></ul> | 
| Azure Document DB | <ul><li>[Chiffrer les données sensibles stockées dans DocumentDB](#encrypt-docdb)</li></ul> | 
| **Délimitation d’approbation de machine virtuelle Azure IaaS** | <ul><li>[Utiliser des disques tooencrypt de chiffrement de disque Azure utilisés par les ordinateurs virtuels](#disk-vm)</li></ul> | 
| **Délimitation d’approbation Service Fabric** | <ul><li>[Chiffrer les secrets dans les applications Service Fabric](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[Effectuer la modélisation de sécurité et utiliser les divisions/équipes si nécessaire](#modeling-teams)</li><li>[Réduire la fonctionnalité d’accès tooshare sur les entités critiques](#entities)</li><li>[Formation des utilisateurs sur les risques de hello associés à la fonctionnalité de Dynamics CRM partage hello et les bonnes pratiques de sécurité](#good-practices)</li><li>[Inclure une règle de normes de développement interdisant l’affichage des détails de configuration dans la gestion des exceptions](#exception-mgmt)</li></ul> | 
| **Azure Storage** | <ul><li>[Utiliser Azure Storage Service Encryption pour les données au repos (version préliminaire)](#sse-preview)</li><li>[Utiliser des données sensibles toostore de chiffrement côté Client dans le stockage Azure](#client-storage)</li></ul> | 
| **Client mobile** | <ul><li>[Chiffrer les données sensibles ou personnelles écrites le stockage local des toophones](#pii-phones)</li><li>[Obscurcir les fichiers binaires générés avant de les distribuer aux utilisateurs de tooend](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[Ensemble clientCredentialType tooCertificate ou Windows](#cert)</li><li>[Le mode de sécurité WCF n’est pas activé](#security)</li></ul> | 

## <a id="binaries-info"></a>S’assurer que les fichiers binaires sont masqués s’ils contiennent des informations sensibles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Assurez-vous que les fichiers binaires sont masqués s’ils contiennent des informations sensibles, comme des secrets industriels ou une logique métier sensible et irréversible. Il s’agit de toostop inverse l’ingénierie des assemblys. Les outils du type `CryptoObfuscator` peuvent être utilisés à cet effet. |

## <a id="efs-user"></a>Pensez à l’aide du système EFS (Encrypted File System) est utilisé tooprotect des données confidentielles spécifiques à l’utilisateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Pensez à l’aide du système EFS (Encrypted File System) est spécifique à l’utilisateur des données confidentielles tooprotect utilisé à partir de rivaux avec l’ordinateur de toohello d’accès physique. |

## <a id="filesystem"></a>Assurez-vous que les données sensibles stockées par l’application hello sur le système de fichiers hello sont chiffrées.

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Assurez-vous que les données sensibles stockées par l’application hello sur le système de fichiers hello sont chiffrées (par exemple, à l’aide de DPAPI), si le système EFS ne peut pas être appliqué. |

## <a id="cache-browser"></a>Assurez-vous que le contenu sensible n’est pas mis en cache sur le navigateur de hello

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, Web Forms, MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Les navigateurs peuvent stocker des informations à des fins de mise en cache et d’historique. Ces fichiers mis en cache sont stockés dans un dossier, comme le dossier des fichiers Internet temporaires hello dans les cas de hello d’Internet Explorer. Ces pages sont visées à nouveau, navigateur de hello les affiche dans son cache. Si des informations sensibles sont utilisateur toohello affiché (par exemple, son adresse, carte de crédit, numéro de sécurité sociale ou nom d’utilisateur), cette information peut être stockée dans le cache du navigateur et par conséquent récupérables examiner la mémoire cache du navigateur hello ou en appuyant simplement sur le bouton de navigateur hello « Précédent ». Définir de valeur d’en-tête cache-control réponse trop « no-store » pour toutes les pages. |

### <a name="example"></a>Exemple
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>Exemple
Il est possible d’utiliser un filtre. L’exemple suivant illustre ce cas de figure : 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>Chiffrer les sections des fichiers de configuration de l’application web qui contiennent des données sensibles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Comment : Chiffrer des Sections de Configuration dans ASP.NET 2.0 à l’aide de DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [en spécifiant un fournisseur de Configuration protégée](https://msdn.microsoft.com/library/68ze1hb2.aspx), [secrets d’application à l’aide d’Azure Key Vault tooprotect](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Étapes** | Fichiers de configuration tels que hello Web.config, appsettings.json sont souvent utilisées toohold des informations sensibles, notamment des noms d’utilisateur, les mots de passe, des chaînes de connexion de base de données et des clés de chiffrement. Si vous ne protégez pas ces informations, votre application est vulnérable tooattackers ou obtenir des informations sensibles telles que les noms d’utilisateur de compte et les mots de passe, les noms de base de données et les noms de serveur des utilisateurs malveillants. Selon le type de déploiement hello (azure/localement), chiffrer les sections de sensibles hello de fichiers de configuration à l’aide de DPAPI ou des services tels que le coffre de clés Azure. |

## <a id="autocomplete-input"></a>Désactiver explicitement les attributs HTML hello la saisie semi-automatique dans les formulaires sensibles et les entrées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN: autocomplete attribute (MSDN : attribut autocomplete)](http://msdn.microsoft.com/library/ms533486(VS.85).aspx), [Using AutoComplete in HTML (Utilisation de la saisie semi-automatique dans HTML)](http://msdn.microsoft.com/library/ms533032.aspx), [Vulnérabilité liée au nettoyage HTML](http://technet.microsoft.com/security/bulletin/MS10-071), [Autocomplete.,again?! (Encore la saisie semi-automatique ?)](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) |
| **Étapes** | attribut de la saisie semi-automatique Hello Spécifie si un formulaire doit avoir la saisie semi-automatique ou désactiver. Lorsque la saisie semi-automatique est activée, les valeurs complète automatiquement navigateur hello basées sur cet utilisateur hello a entré. Par exemple, lorsqu’un nouveau nom et mot de passe est entré dans un formulaire et hello formulaire est envoyé, navigateur de hello demande si le mot de passe hello doit être enregistré. Par la suite lorsque hello formulaire est affiché, mot de passe et nom de hello sont automatiquement renseignés ou sont effectuées comme nom de hello est entré. Un pirate ayant accès local peut obtenir le mot de passe de texte en clair hello du cache du navigateur hello. La saisie semi-automatique est activée par défaut et elle doit être explicitement désactivée. |

### <a name="example"></a>Exemple
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>Assurez-vous que les données sensibles affichées sur l’écran hello utilisateur sont masquées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Données sensibles telles que les mots de passe, numéros de carte de crédit, etc. de SSN doivent être masquées lorsque affiché sur l’écran hello. Il s’agit de personnel tooprevent non autorisé d’accéder aux données de hello (par exemple, épaule-navigation des mots de passe, affichage des numéros de SSN d’utilisateurs de support technique). Assurez-vous que ces éléments de données ne sont pas visibles en texte brut et qu’ils sont masqués de manière appropriée. Cela a toobe pris en charge lors de les accepter comme entrée (par ex.. type d’entrée = « password »), ainsi que l’affichage sur l’écran hello (par exemple, affichage uniquement hello 4 derniers chiffres du numéro de carte de crédit hello). |

## <a id="dynamic-users"></a>Implémenter des utilisateurs de masquage exposition des données sensibles toolimit non privilégié de données dynamiques

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure, local |
| **Attributs**              | Version SQL - V12, Version SQL - MsSQL2016 |
| **Informations de référence**              | [Dynamic Data Masking (masquage des données dynamiques)](https://msdn.microsoft.com/library/mt130841) |
| **Étapes** | Hello masquage dynamique des données vise exposition toolimit des données sensibles, empêchant les utilisateurs qui ne dispose pas d’accéder aux données de toohello de les consulter. Masquage dynamique des données ne visent pas les utilisateurs de base de données tooprevent de se connecter directement toohello de base de données et exécuter des requêtes exhaustives qui exposent des données sensibles de hello. Masquage dynamique des données sont complémentaire tooother fonctionnalités de sécurité SQL Server (l’audit, chiffrement, sécurité au niveau des lignes...) et il est vivement recommandé toouse cette fonctionnalité conjointement avec celles-ci par ailleurs dans l’ordre toobetter protéger les données sensibles hello Bonjour base de données. Cette fonctionnalité est prise en charge uniquement par SQL Server à partir de la version 2016 et par Azure SQL Database. |

## <a id="salted-hash"></a>S’assurer que les mots de passe sont stockés dans un format de hachage salé

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Password Hashing using .NET Crypto APIs (Hachage de mots de passe à l’aide des API de chiffrement .NET)](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **Étapes** | Les mots de passe ne doivent pas être stockés dans les bases de données de magasin d’utilisateurs personnalisés. Au lieu de cela, les hachages de mot de passe doivent être stockés avec des valeurs salt. Assurez-vous que salt hello pour l’utilisateur de hello est toujours unique et que vous appliquez b-crypt, s-crypt ou PBKDF2 avant de stocker le mot de passe hello, avec un nombre d’itérations facteur travail minimal de 150 000 boucles possibilité de hello tooeliminate de force.| 

## <a id="db-encrypted"></a>S’assurer que les données sensibles des colonnes de la base de données sont chiffrées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Version SQL - Toutes |
| **Informations de référence**              | [Liste de vérification : chiffrement des données sensibles](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [Chiffrer une colonne de données](https://msdn.microsoft.com/library/ms179331), [ENCRYPTBYCERT (Transact-SQL)](https://msdn.microsoft.com/library/ms188061) |
| **Étapes** | Les données sensibles telles que des numéros de carte de crédit ont toobe chiffrée dans la base de données hello. Les données peuvent être chiffrées à l’aide du chiffrement au niveau colonne ou par une fonction de l’application à l’aide des fonctions de chiffrement hello. |

## <a id="tde-enabled"></a>S’assurer que le chiffrement au niveau de la base de données est activé

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du chiffrement transparent des données (TDE)](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **Étapes** | Chiffrement transparent des données (TDE) dans SQL server permet le chiffrement des données sensibles dans une base de données de fonctionnalité et à protéger les clés hello qui sont des données de hello tooencrypt utilisé avec un certificat. Cela empêche toute personne sans les clés hello d’utiliser les données de hello. Chiffrement transparent des données protège les données « au repos », ce qui signifie que les fichiers journaux et de données hello. Hello capacité toocomply il offre de nombreuses lois, réglementations et instructions établies dans différents secteurs professionnels. |

## <a id="backup"></a>S’assurer que les sauvegardes de base de données sont chiffrées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure, OnPrem |
| **Attributs**              | Version SQL - V12, Version SQL - MsSQL2014 |
| **Informations de référence**              | [Chiffrement de sauvegarde](https://msdn.microsoft.com/library/dn449489) |
| **Étapes** | SQL Server dispose des données de salutation hello capacité tooencrypt lors de la création d’une sauvegarde. En spécifiant l’algorithme de chiffrement hello et chiffreur hello (un certificat ou clé asymétrique) lors de la création d’une sauvegarde, un peut créer un fichier de sauvegarde chiffré. |

## <a id="api-browser"></a>Assurez-vous que tooWeb pertinentes des données sensibles QU'API ne sont pas stockée dans le stockage du navigateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC 5, MVC 6 |
| **Attributs**              | Fournisseur d’identité - ADFS, Fournisseur d’identité - Azure AD |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Dans certaines implémentations, tooWeb pertinentes d’artefacts sensibles des API l’authentification sont stockées dans le stockage local du navigateur. C’est notamment le cas des artefacts d’authentification Azure AD comme adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key, etc.</p><p>Tous ces artefacts sont disponibles même après la déconnexion ou la fermeture du navigateur. Si un adversaire Obtient des artefacts de toothese d’accès, il peut les réutiliser ressources de hello protégé tooaccess (API). Assurez-vous que tous les artefacts sensibles de tooWeb connexes API n’est pas stockée dans le stockage du navigateur. Dans les cas où le stockage côté client est inévitable (par exemple, seul Page Applications (SPA) qui tirent parti des flux implicite OpenIdConnect/OAuth besoin toostore localement les jetons d’accès), utilisez les options de stockage avec n’ont pas de persistance. par exemple, préférez SessionStorage tooLocalStorage.</p>| 

### <a name="example"></a>Exemple
Hello extrait de code JavaScript suivant provient d’une bibliothèque d’authentification personnalisé qui stocke les artefacts de l’authentification dans le stockage local. Ce type d’implémentation doit être évité. 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>Chiffrer les données sensibles stockées dans Cosmos DB

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Document DB | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Chiffrez les données sensibles au niveau de l’application avant de les stocker dans la base de données de document ou de stocker toute donnée sensible dans d’autres solutions de stockage, comme le stockage Azure ou Azure SQL| 

## <a id="disk-vm"></a>Utiliser des disques tooencrypt de chiffrement de disque Azure utilisés par les ordinateurs virtuels

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation de machine virtuelle Azure IaaS | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [À l’aide du chiffrement de disque Azure tooencrypt disques utilisés par vos ordinateurs virtuels](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **Étapes** | <p>Azure Disk Encryption est une nouvelle fonctionnalité qui est actuellement disponible en version préliminaire. Cette fonctionnalité vous permet de disques de système d’exploitation tooencrypt hello et des disques de données utilisées par une Machine virtuelle de IaaS. Pour Windows, les lecteurs de hello sont chiffrés à l’aide de la technologie de chiffrement BitLocker standard. Pour Linux, les disques de hello sont chiffrées à l’aide de la technologie de hello DM-Crypt. Il est intégré à Azure Key Vault tooallow vous toocontrol et gérer des clés de chiffrement de disque hello. Hello solutions de chiffrement de disque Azure prend en charge hello trois scénarios de chiffrement client suivants :</p><ul><li>Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir des fichiers VHD chiffrés par le client et des clés de chiffrement fournies par le client, qui sont stockées dans Azure Key Vault.</li><li>Activer le chiffrement sur les nouvelles machines virtuelles IaaS de créés à partir de hello Azure Marketplace.</li><li>Activation du chiffrement sur des machines virtuelles IaaS existantes et fonctionnant déjà dans Azure.</li></ul>| 

## <a id="fabric-apps"></a>Chiffrer les secrets dans les applications Service Fabric

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Service Fabric | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Environnement - Azure |
| **Informations de référence**              | [Gestion des secrets dans des applications Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **Étapes** | Les secrets peuvent être des informations sensibles quelconques, notamment des chaînes de connexion de stockage, des mots de passe ou d’autres valeurs qui ne doivent pas être traitées en texte brut. Utilisez le coffre de clés Azure toomanage clés et les secrets dans les applications de l’infrastructure de service. |

## <a id="modeling-teams"></a>Effectuer la modélisation de sécurité et utiliser les divisions/équipes si nécessaire

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Effectuez la modélisation de sécurité et utilisez les divisions/équipes si nécessaire |

## <a id="entities"></a>Réduire la fonctionnalité d’accès tooshare sur les entités critiques

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Réduire la fonctionnalité d’accès tooshare sur les entités critiques |

## <a id="good-practices"></a>Formation des utilisateurs sur les risques de hello associés à la fonctionnalité de Dynamics CRM partage hello et les bonnes pratiques de sécurité

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Formation des utilisateurs sur les risques de hello associés à la fonctionnalité de Dynamics CRM partage hello et les bonnes pratiques de sécurité |

## <a id="exception-mgmt"></a>Inclure une règle de normes de développement interdisant l’affichage des détails de configuration dans la gestion des exceptions

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Incluez une règle de normes de développement interdisant l’affichage des détails de configuration dans la gestion des exceptions en dehors du développement. Testez cette procédure lors de vérifications de code ou d’un contrôle périodique.|

## <a id="sse-preview"></a>Utiliser Azure Storage Service Encryption pour les données au repos (version préliminaire)

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | StorageType - Blob |
| **Informations de référence**              | [Azure Storage Service Encryption pour les données au repos (version préliminaire)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **Étapes** | <p>Azure Storage Service de chiffrement (SSE) pour les données au repos vous permet de protéger et de protéger vos données toomeet votre engagements de conformité et de sécurité de l’organisation. Avec cette fonctionnalité, Azure Storage chiffre vos toostorage toopersisting préalable de données et déchiffre tooretrieval préalable automatiquement. Hello de chiffrement, le déchiffrement et gestion de clés est totalement transparent toousers. SSE s’applique uniquement les tooblock objets BLOB, les objets BLOB de pages et ajouter des objets BLOB. Hello autres types de données, y compris les tables, les files d’attente et les fichiers ne seront pas chiffrées.</p><p>Flux de travail de chiffrement et de déchiffrement :</p><ul><li>client de Hello Active le chiffrement sur le compte de stockage hello</li><li>Lorsque les clients hello écrit le nouveau stockage tooBlob de données (PUT Blob, placez le bloc, placer la Page, etc.) ; chaque écriture est chiffrée à l’aide du chiffrement AES 256 bits, un des hello les plus forts les chiffrements par bloc disponibles</li><li>Lorsque le client de hello a besoin de données tooaccess (GET Blob, etc.), les données sont automatiquement déchiffrées avant de retourner toohello utilisateur</li><li>Si le chiffrement est désactivé, nouvelle écriture n’est plus chiffrés et les données chiffrées existantes restent chiffrées jusqu'à ce que réécrit par l’utilisateur de hello. Alors que le chiffrement est activé, les écritures tooBlob stockage sera chiffrée. état Hello des données ne change pas avec utilisateur hello basculer entre l’activation/désactivation du chiffrement pour le compte de stockage hello</li><li>Toutes les clés de chiffrement sont stockées, chiffrées et gérées par Microsoft</li></ul><p>Notez que pour l’instant, clés hello utilisés pour le chiffrement de hello sont gérés par Microsoft. Microsoft génère des clés de hello à l’origine et gérer le stockage sécurisé de clés de hello ainsi qu’une rotation régulière de hello hello tel que défini par la stratégie interne de Microsoft. Bonjour future, clients obtiendront hello capacité toomanage leurs propres > clés de chiffrement et fournir un chemin de migration à partir des clés de centres de données gérés par toocustomer de clés.</p>| 

## <a id="client-storage"></a>Utiliser des données sensibles toostore de chiffrement côté Client dans le stockage Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l’aide d’Azure Key Vault](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [Storing Data Securely in Azure Blob Storage with Azure Encryption Extensions (Stockage sécurisé des données dans le stockage Blob Azure avec les extensions de chiffrement Azure)](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) |
| **Étapes** | <p>Hello bibliothèque cliente de stockage Azure pour .NET Nuget package prend en charge le chiffrement des données dans les applications clientes avant chargement tooAzure stockage et le déchiffrement des données lors du téléchargement de toohello client. bibliothèque de Hello prend également en charge l’intégration avec le coffre de clés Azure pour la gestion de clés de compte de stockage. Voici une brève description du fonctionnement du chiffrement côté client :</p><ul><li>client de stockage Azure Hello SDK génère une clé de chiffrement de contenu (CEK), qui est une clé symétrique usage unique</li><li>Les données du client sont chiffrées à l’aide de cette clé de chiffrement de contenu</li><li>Hello CEK est ensuite encapsulée (chiffré) à l’aide de la clé de chiffrement à clé hello (KEK). Hello veillent est identifié par un identificateur de clé et peut être une paire de clés asymétriques ou une clé symétrique et peut être géré localement ou stockée dans Azure Key Vault. client de stockage Hello lui-même n’a jamais accès toohello de clés. Il appelle simplement algorithme hello encapsulage de clé fourni par le coffre de clés. Les clients peuvent choisir toouse des fournisseurs personnalisés pour la clé d’habillage/Désencapsulation s’ils veulent</li><li>Hello données chiffrées seront ensuite téléchargé toohello le service Azure Storage. Vérifiez les liens hello dans la section des références hello pour les détails d’implémentation de bas niveau.</li></ul>|

## <a id="pii-phones"></a>Chiffrer les données sensibles ou personnelles écrites le stockage local des toophones

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client mobile | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, Xamarin  |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Gérer des paramètres et des fonctionnalités sur vos appareils avec des stratégies Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [Keychain Valet (Trousseau valet)](https://components.xamarin.com/view/square.valet) |
| **Étapes** | <p>Si l’application hello écrit des informations sensibles telles que PII l’utilisateur (courrier électronique, numéro de téléphone, prénom, nom, préférences, etc.). -sur le système de fichiers mobile, puis il doit être chiffré avant d’écrire le système de fichiers local toohello. Si l’application hello est une application d’entreprise, puis Explorez possibilité hello de l’application de publication à l’aide de Windows Intune.</p>|

### <a name="example"></a>Exemple
Intune peut être configuré avec la sécurité Stratégies toosafeguard sensibles données suivantes : 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>Exemple
Si l’application hello n’est pas une application d’entreprise, puis utiliser l’appel fourni le magasin de clés, les clés de chiffrement de trousseau toostore, à l’aide de l’opération de chiffrement peuvent être effectués sur le système de fichiers hello. Code suivant montre comment la clé tooaccess de trousseau à l’aide de xamarin : 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>Obscurcir les fichiers binaires générés avant de les distribuer aux utilisateurs de tooend

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client mobile | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Crypto Obfuscation For .Net](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **Étapes** | Fichiers binaires générés (assemblys dans apk) doivent être obscurci toostop inverse l’ingénierie des assemblys. Outils tels que `CryptoObfuscator` peut être utilisé à cet effet. |

## <a id="cert"></a>Ensemble clientCredentialType tooCertificate ou Windows

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | À l’aide d’un UsernameToken avec un mot de passe en texte clair sur un canal non chiffré expose tooattackers de mot de passe hello qui peuvent intercepter des messages SOAP de type hello. Les fournisseurs de services qui utilisent hello UsernameToken peut accepter des mots de passe envoyés en texte clair. Envoi des mots de passe en texte clair sur un canal non chiffré peut exposer tooattackers d’informations d’identification hello qui espionne message SOAP de type hello. | 

### <a name="example"></a>Exemple
Hello configuration de fournisseur de service WCF suivante utilise hello UsernameToken : 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
Ensemble clientCredentialType tooCertificate ou Windows. 

## <a id="security"></a>Le mode de sécurité WCF n’est pas activé

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, .NET Framework 3 |
| **Attributs**              | Mode de sécurité - Transport, Mode de sécurité - Messages |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html), [Fundamentals of WCF Security CoDe Magazine (Notions de base de sécurité WCF dans CoDe Magazine)](http://www.codemag.com/article/0611051) |
| **Étapes** | Aucune sécurité liée au transport ou aux messages n’a été définie. Applications qui transmettent des messages sans transport ou message de sécurité ne peut pas garantir l’intégrité de hello ou la confidentialité des messages de type hello. Lorsque la valeur de tooNone est une liaison de sécurité WCF, sécurité de transport et de message sont désactivées. |

### <a name="example"></a>Exemple
Hello de configuration suivant définit tooNone de mode de sécurité hello. 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>Exemple
Mode de sécurité - L’ensemble des liaisons de service offre cinq modes de sécurité : 
* Aucune. Sécurité désactivée. 
* Transport. Utilise la sécurité liée au transport pour la protection des messages et l’authentification mutuelle. 
* Message. Utilise la sécurité liée aux messages pour la protection des messages et l’authentification mutuelle. 
* Les deux. Vous permet de toosupply paramètres pour le transport et la sécurité au niveau du message (que MSMQ prend en charge). 
* TransportWithMessageCredential. Informations d’identification sont transmises avec le message de type hello et protection des messages et l’authentification du serveur sont fournies par la couche de transport hello. 
* TransportCredentialOnly. Informations d’identification du client sont renvoyées avec la couche de transport hello et aucune protection des messages n’est appliquée. Utilisez le transport et le message d’intégrité de hello tooprotect de sécurité et confidentialité des messages. configuration de Hello ci-dessous indique la sécurité du transport hello service toouse avec les informations d’identification de message.
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
