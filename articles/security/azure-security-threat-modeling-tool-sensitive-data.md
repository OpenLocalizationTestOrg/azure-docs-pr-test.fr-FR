---
title: "Données sensibles - Outil Microsoft de modélisation des menaces - Azure | Microsoft Docs"
description: "Mesures de correction des menaces exposées dans l’outil de modélisation des menaces"
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
ms.openlocfilehash: 8d7189ea4b01d43cea709e3300d8ed71d266f5c9
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2018
---
# <a name="security-frame-sensitive-data--mitigations"></a>Infrastructure de sécurité : Données sensibles | Mesures de correction 
| Produit/Service | Article |
| --------------- | ------- |
| **Délimitation d’approbation machine** | <ul><li>[S’assurer que les fichiers binaires sont masqués s’ils contiennent des informations sensibles](#binaries-info)</li><li>[Utiliser le système de fichiers EFS pour protéger les données confidentielles spécifiques de l’utilisateur](#efs-user)</li><li>[S’assurer que les données sensibles stockées par l’application sur le système de fichiers sont chiffrées](#filesystem)</li></ul> | 
| **Application Web** | <ul><li>[S’assurer que le contenu sensible n’est pas mis en cache dans le navigateur](#cache-browser)</li><li>[Chiffrer les sections des fichiers de configuration de l’application web qui contiennent des données sensibles](#encrypt-data)</li><li>[Désactiver explicitement l’attribut HTML de saisie semi-automatique dans les formulaires et les entrées sensibles](#autocomplete-input)</li><li>[S’assurer que les données sensibles affichées sur l’écran de l’utilisateur sont masquées](#data-mask)</li></ul> | 
| **Base de données** | <ul><li>[Implémenter le masquage des données dynamiques pour limiter l’exposition de données sensibles aux utilisateurs non privilégiés](#dynamic-users)</li><li>[S’assurer que les mots de passe sont stockés dans un format de hachage salé](#salted-hash)</li><li>[S’assurer que les données sensibles des colonnes de la base de données sont chiffrées](#db-encrypted)</li><li>[S’assurer que le chiffrement au niveau de la base de données est activé](#tde-enabled)</li><li>[S’assurer que les sauvegardes de base de données sont chiffrées](#backup)</li></ul> | 
| **API Web** | <ul><li>[S’assurer que les données sensibles concernant l’API Web ne sont pas stockées dans le navigateur](#api-browser)</li></ul> | 
| Azure Document DB | <ul><li>[Chiffrer les données sensibles stockées dans Azure Cosmos DB](#encrypt-docdb)</li></ul> | 
| **Délimitation d’approbation de machine virtuelle Azure IaaS** | <ul><li>[Utiliser Azure Disk Encryption pour chiffrer les disques utilisés par les machines virtuelles](#disk-vm)</li></ul> | 
| **Délimitation d’approbation Service Fabric** | <ul><li>[Chiffrer les secrets dans les applications Service Fabric](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[Effectuer la modélisation de sécurité et utiliser les divisions/équipes si nécessaire](#modeling-teams)</li><li>[Réduire l’accès pour partager la fonctionnalité sur les entités critiques](#entities)</li><li>[Former les utilisateurs aux risques liés à la fonctionnalité de partage Dynamics CRM et aux bonnes pratiques de sécurité](#good-practices)</li><li>[Inclure une règle de normes de développement interdisant l’affichage des détails de configuration dans la gestion des exceptions](#exception-mgmt)</li></ul> | 
| **Stockage Azure** | <ul><li>[Utiliser Azure Storage Service Encryption pour les données au repos (version préliminaire)](#sse-preview)</li><li>[Utiliser le chiffrement côté client pour stocker les données sensibles dans le stockage Azure](#client-storage)</li></ul> | 
| **Client mobile** | <ul><li>[Chiffrer les données sensibles ou personnelles écrites dans le stockage local des téléphones](#pii-phones)</li><li>[Masquer les fichiers binaires générés avant la diffusion auprès des utilisateurs finaux](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[Définir la valeur clientCredentialType sur Certificat ou Windows](#cert)</li><li>[Le mode de sécurité WCF n’est pas activé](#security)</li></ul> | 

## <a id="binaries-info"></a>S’assurer que les fichiers binaires sont masqués s’ils contiennent des informations sensibles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Assurez-vous que les fichiers binaires sont masqués s’ils contiennent des informations sensibles, comme des secrets industriels ou une logique métier sensible et irréversible. Cela permet d’arrêter l’ingénierie à rebours des assemblys. Les outils du type `CryptoObfuscator` peuvent être utilisés à cet effet. |

## <a id="efs-user"></a>Utiliser le système de fichiers EFS pour protéger les données confidentielles spécifiques de l’utilisateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Utilisez le système de fichiers EFS pour protéger les données confidentielles spécifiques de l’utilisateur des pirates disposant d’un accès physique à l’ordinateur. |

## <a id="filesystem"></a>S’assurer que les données sensibles stockées par l’application sur le système de fichiers sont chiffrées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Assurez-vous que les données sensibles stockées par l’application sur le système de fichiers sont chiffrées (par exemple, en vous servant de DPAPI), si le système EFS ne peut pas être appliqué |

## <a id="cache-browser"></a>S’assurer que le contenu sensible n’est pas mis en cache dans le navigateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, Web Forms, MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Les navigateurs peuvent stocker des informations à des fins de mise en cache et d’historique. Ces fichiers mis en cache sont stockés dans un dossier, comme le dossier Fichiers Internet temporaires d’Internet Explorer. Lorsque ces pages sont de nouveau consultées, le navigateur les affiche à partir du cache. Si l’utilisateur peut voir des informations sensibles (par exemple, adresse, numéro de carte de crédit, numéro de sécurité sociale ou nom d’utilisateur), ces informations sont peut-être stockées dans le cache du navigateur et elles peuvent par conséquent être récupérées lors de l’examen du cache du navigateur ou en appuyant simplement sur le bouton Précédent du navigateur. Définissez la valeur d’en-tête de réponse cache-control sur « no-store » pour toutes les pages. |

### <a name="example"></a>exemples
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

### <a name="example"></a>exemples
Il est possible d’utiliser un filtre. L’exemple suivant illustre ce cas de figure : 
```csharp
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
| **Informations de référence**              | [How To: Encrypt Configuration Sections in ASP.NET 2.0 Using DPAPI (Chiffrement des sections de configuration dans ASP.NET 2.0 à l’aide de DPAPI)](https://msdn.microsoft.com/library/ff647398.aspx), [Spécification d’un fournisseur de configuration protégée](https://msdn.microsoft.com/library/68ze1hb2.aspx), [Using Azure Key Vault to protect application secrets (Utilisation d’Azure Key Vault pour protéger la confidentialité de l’application)](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Étapes** | Les fichiers de configuration tels que web.config et appsettings.json sont souvent utilisés pour stocker des informations sensibles, comme les noms d’utilisateur, les mots de passe, les chaînes de connexion de base de données et les clés de chiffrement. Si vous ne protégez pas ces informations, votre application est vulnérable aux attaquants ou aux personnes malveillantes qui veulent obtenir des informations sensibles, comme les noms d’utilisateur et les mots de passe de comptes, les noms de bases de données et les noms de serveurs. Selon le type de déploiement (azure/local), chiffrez les sections sensibles des fichiers de configuration à l’aide de DPAPI ou de services tels qu’Azure Key Vault. |

## <a id="autocomplete-input"></a>Désactiver explicitement l’attribut HTML de saisie semi-automatique dans les formulaires et les entrées sensibles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN: autocomplete attribute (MSDN : attribut autocomplete)](http://msdn.microsoft.com/library/ms533486(VS.85).aspx), [Using AutoComplete in HTML (Utilisation de la saisie semi-automatique dans HTML)](http://msdn.microsoft.com/library/ms533032.aspx), [Vulnérabilité liée au nettoyage HTML](http://technet.microsoft.com/security/bulletin/MS10-071), [Autocomplete.,again?! (Encore la saisie semi-automatique ?)](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) |
| **Étapes** | L’attribut autocomplete spécifie si la saisie semi-automatique doit être activée ou non sur un formulaire. Lorsque la saisie semi-automatique est activée, le navigateur complète automatiquement les valeurs en fonction des valeurs que l’utilisateur a déjà entrées. Par exemple, lorsqu’un nouveau nom et un nouveau mot de passe sont entrés dans un formulaire et que le formulaire est envoyé, le navigateur vous demande si le mot de passe doit être enregistré. Par la suite, lorsque le formulaire est affiché, le nom et le mot de passe sont automatiquement renseignés ou ils sont complétés au moment de la saisie du nom. Une personne malveillante disposant d’un accès local peut obtenir le mot de passe en texte clair à partir du cache du navigateur. La saisie semi-automatique est activée par défaut et elle doit être explicitement désactivée. |

### <a name="example"></a>exemples
```csharp
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>S’assurer que les données sensibles affichées sur l’écran de l’utilisateur sont masquées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Les données sensibles telles que les mots de passe, les numéros de carte de crédit, les numéros de sécurité sociale, etc. doivent être masquées à l’écran. Cela empêche les personnes non autorisées d’accéder aux données (par exemple, en épiant les mots de passe saisis, ou lorsque le support technique affiche le numéro de sécurité sociale de l’utilisateur). Assurez-vous que ces éléments de données ne sont pas visibles en texte brut et qu’ils sont masqués de manière appropriée. Cette opération doit être effectuée lorsque les éléments sont acceptés en entrée (par exemple, type d’entrée = « mot de passe ») et lors de l’affichage sur l’écran (par exemple, affichage des 4 derniers chiffres de la carte de crédit uniquement). |

## <a id="dynamic-users"></a>Implémenter le masquage des données dynamiques pour limiter l’exposition de données sensibles aux utilisateurs non privilégiés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure, local |
| **Attributs**              | Version SQL - V12, Version SQL - MsSQL2016 |
| **Informations de référence**              | [Dynamic Data Masking (masquage des données dynamiques)](https://msdn.microsoft.com/library/mt130841) |
| **Étapes** | Le masquage des données dynamiques vise à limiter l’exposition des données sensibles, empêchant ainsi les utilisateurs non autorisés d’afficher les données. Le masquage des données dynamiques ne vise pas à empêcher les utilisateurs de la base de données de se connecter directement à la base de données ni d’exécuter des requêtes exhaustives qui exposent partiellement les données sensibles. Le masquage des données dynamiques est complémentaire d’autres fonctionnalités de sécurité SQL Server (audit, chiffrement, sécurité au niveau des lignes, etc.) et il est fortement recommandé d’utiliser cette fonctionnalité en conjonction avec ces dernières afin d’optimiser la protection des données sensibles de la base de données. Cette fonctionnalité est prise en charge uniquement par SQL Server à partir de la version 2016 et par Azure SQL Database. |

## <a id="salted-hash"></a>S’assurer que les mots de passe sont stockés dans un format de hachage salé

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Password Hashing using .NET Crypto APIs (Hachage de mots de passe à l’aide des API de chiffrement .NET)](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **Étapes** | Les mots de passe ne doivent pas être stockés dans les bases de données de magasin d’utilisateurs personnalisés. Au lieu de cela, les hachages de mot de passe doivent être stockés avec des valeurs salt. Assurez-vous que la valeur salt de l’utilisateur est toujours unique et que vous appliquez b-crypt, s-crypt ou PBKDF2 avant de stocker le mot de passe, avec un nombre d’itérations de facteur de travail minimal de 150 000 boucles afin d’éliminer tout risque d’attaque par force brute.| 

## <a id="db-encrypted"></a>S’assurer que les données sensibles des colonnes de la base de données sont chiffrées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Version SQL - Toutes |
| **Informations de référence**              | [Liste de vérification : chiffrement des données sensibles](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [Chiffrer une colonne de données](https://msdn.microsoft.com/library/ms179331), [ENCRYPTBYCERT (Transact-SQL)](https://msdn.microsoft.com/library/ms188061) |
| **Étapes** | Les données sensibles, comme les numéros de carte de crédit, doivent être chiffrées dans la base de données. Les données peuvent être chiffrées par le biais du chiffrement au niveau colonne ou par une fonction de l’application utilisant les fonctions de chiffrement. |

## <a id="tde-enabled"></a>S’assurer que le chiffrement au niveau de la base de données est activé

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du chiffrement transparent des données (TDE)](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **Étapes** | La fonction Transparent Data Encryption (TDE) de SQL Server permet de chiffrer les données sensibles dans une base de données et de protéger les clés utilisées pour chiffrer les données avec un certificat. Cela empêche toute personne ne disposant pas des clés d’utiliser les données. TDE protège les données au repos, ce qui signifie les données et les fichiers journaux. Cette fonctionnalité permet de se conformer aux nombreuses lois, réglementations et directives établies dans de nombreux secteurs. |

## <a id="backup"></a>S’assurer que les sauvegardes de base de données sont chiffrées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure, OnPrem |
| **Attributs**              | Version SQL - V12, Version SQL - MsSQL2014 |
| **Informations de référence**              | [Chiffrement de sauvegarde](https://msdn.microsoft.com/library/dn449489) |
| **Étapes** | SQL Server peut chiffrer les données lors de la création d’une sauvegarde. En spécifiant l’algorithme de chiffrement et le chiffreur (certificat ou clé asymétrique) lors de la création d’une sauvegarde, il est possible de créer un fichier de sauvegarde chiffré. |

## <a id="api-browser"></a>S’assurer que les données sensibles concernant l’API Web ne sont pas stockées dans le navigateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC 5, MVC 6 |
| **Attributs**              | Fournisseur d’identité - ADFS, Fournisseur d’identité - Azure AD |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Dans certaines implémentations, des artefacts sensibles concernant l’authentification de l’API Web sont stockés en local dans le navigateur. C’est notamment le cas des artefacts d’authentification Azure AD comme adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key, etc.</p><p>Tous ces artefacts sont disponibles même après la déconnexion ou la fermeture du navigateur. Si un pirate obtient l’accès à ces artefacts, il peut le réutiliser pour accéder aux ressources protégées (API). Assurez-vous que tous les artefacts sensibles concernant l’API Web ne sont pas stockés dans le navigateur. Si le stockage côté client est inévitable (par exemple, les applications à page unique qui tirent parti des flux implicites OpenIdConnect/OAuth doivent stocker les jetons d’accès au niveau local), utilisez des options de stockage sans persistance. Par exemple, préférez SessionStorage à LocalStorage.</p>| 

### <a name="example"></a>exemples
L’extrait de code JavaScript ci-dessous provient d’une bibliothèque d’authentification personnalisée qui stocke les artefacts d’authentification en local. Ce type d’implémentation doit être évité. 
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

## <a id="disk-vm"></a>Utiliser Azure Disk Encryption pour chiffrer les disques utilisés par les machines virtuelles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation de machine virtuelle Azure IaaS | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Utilisation de la fonctionnalité Azure Disk Encryption pour chiffrer les disques utilisés par vos machines virtuelles](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **Étapes** | <p>Azure Disk Encryption est une nouvelle fonctionnalité qui est actuellement disponible en version préliminaire. Cette fonctionnalité vous permet de chiffrer les disques de données et de système d’exploitation utilisés par une machine virtuelle IaaS. Sur Windows, les disques sont chiffrés à l’aide de la technologie de chiffrement BitLocker standard. Sur Linux, les disques sont chiffrés à l’aide de la technologie DM-Crypt. La fonctionnalité est intégrée à Azure Key Vault pour vous permettre de contrôler et gérer les clés de chiffrement de disque. Azure Disk Encryption convient pour les trois scénarios de chiffrement client suivants :</p><ul><li>Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir des fichiers VHD chiffrés par le client et des clés de chiffrement fournies par le client, qui sont stockées dans Azure Key Vault.</li><li>Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir d’Azure Marketplace.</li><li>Activation du chiffrement sur des machines virtuelles IaaS existantes et fonctionnant déjà dans Azure.</li></ul>| 

## <a id="fabric-apps"></a>Chiffrer les secrets dans les applications Service Fabric

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Service Fabric | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Environnement - Azure |
| **Informations de référence**              | [Gestion des secrets dans des applications Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **Étapes** | Les secrets peuvent être des informations sensibles quelconques, notamment des chaînes de connexion de stockage, des mots de passe ou d’autres valeurs qui ne doivent pas être traitées en texte brut. Utilisez Azure Key Vault pour gérer les clés et les secrets dans les applications Service Fabric. |

## <a id="modeling-teams"></a>Effectuer la modélisation de sécurité et utiliser les divisions/équipes si nécessaire

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Effectuez la modélisation de sécurité et utilisez les divisions/équipes si nécessaire |

## <a id="entities"></a>Réduire l’accès pour partager la fonctionnalité sur les entités critiques

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Réduisez l’accès pour partager la fonctionnalité sur les entités critiques |

## <a id="good-practices"></a>Former les utilisateurs aux risques liés à la fonctionnalité de partage Dynamics CRM et aux bonnes pratiques de sécurité

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Formez les utilisateurs aux risques liés à la fonctionnalité de partage Dynamics CRM et aux bonnes pratiques de sécurité |

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
| **Composant**               | Stockage Azure | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | StorageType - Blob |
| **Informations de référence**              | [Azure Storage Service Encryption pour les données au repos (version préliminaire)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **Étapes** | <p>Azure Storage Service Encryption pour les données au repos vous aide à protéger vos données pour répondre aux engagements de votre organisation en matière de sécurité et de conformité. Avec cette fonctionnalité, Azure Storage chiffre automatiquement vos données avant de les rendre persistantes dans le stockage et les déchiffre avant la récupération. La gestion du chiffrement, du déchiffrement et des clés est totalement transparente pour les utilisateurs. SSE s’applique uniquement aux objets blob de blocs, aux objets blob de pages et aux objets blob d’ajout. Les autres types de données, y compris les tables, les files d’attente et les fichiers, ne sont pas chiffrés.</p><p>Flux de travail de chiffrement et de déchiffrement :</p><ul><li>Le client active le chiffrement sur le compte de stockage</li><li>Lorsque le client écrit de nouvelles données (PUT Blob, PUT Block, PUT Page, etc.) pour le stockage Blob, chaque écriture est chiffrée à l’aide du chiffrement AES 256 bits, l’un des algorithmes de chiffrement par blocs les plus puissants disponibles</li><li>Lorsque le client a besoin d’accéder aux données (GET Blob, etc.), ces dernières sont automatiquement déchiffrées avant d’être renvoyées à l’utilisateur</li><li>Si le chiffrement est désactivé, les nouvelles écritures ne sont plus chiffrées et les données chiffrées existantes restent chiffrées jusqu’à ce qu’elles soient réécrites par l’utilisateur. Lorsque le chiffrement est activé, les écritures dans Blob Storage sont chiffrées. L’état des données ne change pas lorsque l’utilisateur bascule entre l’activation et la désactivation du chiffrement pour le compte de stockage</li><li>Toutes les clés de chiffrement sont stockées, chiffrées et gérées par Microsoft</li></ul><p>Actuellement, les clés utilisées pour le chiffrement sont gérées par Microsoft. Microsoft crée initialement les clés, puis gère le stockage sécurisé des clés ainsi que leur rotation régulière, conformément à la politique interne de Microsoft en la matière. À l’avenir, les clients pourront gérer leurs propres clés de chiffrement et fournir un chemin de migration des clés gérées par Microsoft en clés gérées par le client.</p>| 

## <a id="client-storage"></a>Utiliser le chiffrement côté client pour stocker les données sensibles dans le stockage Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Stockage Azure | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l’aide d’Azure Key Vault](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [Storing Data Securely in Azure Blob Storage with Azure Encryption Extensions (Stockage sécurisé des données dans le stockage Blob Azure avec les extensions de chiffrement Azure)](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) |
| **Étapes** | <p>La bibliothèque cliente de stockage Azure pour le package NuGet .NET prend en charge le chiffrement des données au sein des applications clientes avant le chargement vers le stockage Azure, et le déchiffrement des données pendant leur téléchargement vers le client. La bibliothèque prend également en charge l’intégration à Azure Key Vault pour la gestion des clés de compte de stockage. Voici une brève description du fonctionnement du chiffrement côté client :</p><ul><li>Le Kit de développement logiciel (SDK) client de stockage Azure génère une clé de chiffrement de contenu (CEK) qui est une clé symétrique à usage unique</li><li>Les données du client sont chiffrées à l’aide de cette clé de chiffrement de contenu</li><li>La clé de chiffrement de contenu est ensuite encapsulée (chiffrée) à l’aide de la clé de chiffrement de clés (KEK). La clé de chiffrement de clés est identifiée par un identificateur de clé et peut être une paire de clés asymétriques ou une clé symétrique pouvant être gérée localement ou stockée dans Azure Key Vault. Le client Storage n’a jamais accès à la clé de chiffrement de clés. Il appelle simplement l'algorithme d’encapsulage de clés fourni par Key Vault. Si besoin est, les clients peuvent choisir d’utiliser des fournisseurs personnalisés pour l’encapsulage/le désencapsulage de clés</li><li>Les données chiffrées sont ensuite téléchargées sur le service Azure Storage. Vérifiez les liens dans la section Références pour en savoir plus sur l’implémentation de bas niveau.</li></ul>|

## <a id="pii-phones"></a>Chiffrer les données sensibles ou personnelles écrites dans le stockage local des téléphones

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client mobile | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, Xamarin  |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Gérer des paramètres et des fonctionnalités sur vos appareils avec des stratégies Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [Keychain Valet (Trousseau valet)](https://components.xamarin.com/view/square.valet) |
| **Étapes** | <p>Si l’application écrit des informations sensibles, comme les informations personnelles de l’utilisateur (adresse e-mail, numéro de téléphone, prénom, nom, préférences, etc.) sur le système de fichiers mobile, ces dernières doivent être chiffrées avant leur écriture sur le système de fichiers local. Si l’application est une application d’entreprise, envisagez la publication de l’application à l’aide de Windows Intune.</p>|

### <a name="example"></a>exemples
Intune peut être configuré conformément aux stratégies de sécurité suivantes pour sauvegarder les données sensibles : 
```csharp
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>exemples
Si l’application n’est pas une application d’entreprise, utilisez le keystore fourni par la plateforme et les trousseaux pour stocker les clés de chiffrement, grâce auxquels l’opération de chiffrement peut être effectuée sur le système de fichiers. L’extrait de code suivant explique comment accéder à une clé du trousseau à l’aide de Xamarin : 
```csharp
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

## <a id="binaries-end"></a>Masquer les fichiers binaires générés avant la diffusion auprès des utilisateurs finaux

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client mobile | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Crypto Obfuscation For .Net](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **Étapes** | Les fichiers binaires générés (assemblys dans fichiers apk) doivent être masqués pour arrêter l’ingénierie à rebours des assemblys. Des outils tels que `CryptoObfuscator` peuvent être utilisés à cet effet. |

## <a id="cert"></a>Définir la valeur clientCredentialType sur Certificat ou Windows

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | L’utilisation d’un UsernameToken avec mot de passe en texte brut sur un canal non chiffré expose le mot de passe aux personnes malveillantes qui sont alors en mesure d’intercepter les messages SOAP. Les fournisseurs de services qui utilisent UsernameToken peuvent accepter l’envoi de mots de passe en texte brut. L’envoi de mots de passe en texte brut sur un canal non chiffré peut exposer les informations d’identification à des personnes malveillantes susceptibles d’intercepter le message SOAP. | 

### <a name="example"></a>exemples
La configuration du fournisseur de services WCF suivante utilise un UsernameToken : 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
Définissez la valeur clientCredentialType sur Certificat ou Windows. 

## <a id="security"></a>Le mode de sécurité WCF n’est pas activé

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, .NET Framework 3 |
| **Attributs**              | Mode de sécurité - Transport, Mode de sécurité - Messages |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html), [Fundamentals of WCF Security CoDe Magazine (Notions de base de sécurité WCF dans CoDe Magazine)](http://www.codemag.com/article/0611051) |
| **Étapes** | Aucune sécurité liée au transport ou aux messages n’a été définie. Les applications qui transmettent des messages sans sécurité liée au transport ou aux messages ne peuvent pas garantir l’intégrité ou la confidentialité des messages. Lorsqu’une liaison de sécurité WCF est définie sur Aucune, la sécurité liée au transport et aux messages est désactivée. |

### <a name="example"></a>exemples
La configuration suivante définit le mode de sécurité sur Aucun. 
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

### <a name="example"></a>exemples
Mode de sécurité - L’ensemble des liaisons de service offre cinq modes de sécurité : 
* Aucune. Sécurité désactivée. 
* Transport. Utilise la sécurité liée au transport pour la protection des messages et l’authentification mutuelle. 
* Message. Utilise la sécurité liée aux messages pour la protection des messages et l’authentification mutuelle. 
* Les deux. Vous permet de fournir des paramètres de sécurité au niveau du transport et des messages (seul MSMQ prend en charge cette fonctionnalité). 
* TransportWithMessageCredential. Les informations d’identification sont transmises avec les messages, et la protection des messages et l’authentification du serveur sont fournies par la couche de transport. 
* TransportCredentialOnly. Les informations d’identification du client sont transmises avec la couche de transport, et aucune protection n’est appliquée aux messages. Utilisez la sécurité liée au transport et aux messages pour protéger l’intégrité et la confidentialité des messages. La configuration ci-dessous indique au service d’utiliser la sécurité liée au transport avec les informations d’identification du message.
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
