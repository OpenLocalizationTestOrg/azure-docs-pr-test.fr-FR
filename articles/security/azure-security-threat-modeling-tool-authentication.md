---
title: "aaaAuthentication - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
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
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>Infrastructure de sécurité : Authentification | Mesures de correction 
| Produit/Service | Article |
| --------------- | ------- |
| **Application web**    | <ul><li>[Envisagez d’utiliser un tooWeb tooauthenticate du mécanisme d’authentification standard Application](#standard-authn-web-app)</li><li>[Les applications doivent gérer les scénarios d’authentification ayant échoué en toute sécurité ](#handle-failed-authn)</li><li>[Activer l’authentification adaptative ou avancée](#step-up-adaptive-authn)</li><li>[Garantir que les interfaces d’administration sont correctement verrouillées](#admin-interface-lockdown)</li><li>[Implémenter des fonctionnalités de mot de passe oublié en toute sécurité](#forgot-pword-fxn)</li><li>[Garantir que la stratégie de compte et de mot de passe est implémentée](#pword-account-policy)</li><li>[Énumération de mettre en œuvre des contrôles tooprevent nom d’utilisateur](#controls-username-enum)</li></ul> |
| **Base de données** | <ul><li>[Si possible, utilisez l’authentification Windows pour la connexion tooSQL Server](#win-authn-sql)</li><li>[Lorsque cela est possible utiliser l’authentification Azure Active Directory pour tooSQL de connexion de base de données](#aad-authn-sql)</li><li>[Lorsque le mode d’authentification SQL est utilisé, garantir que la stratégie de compte et de mot de passe est appliquée sur SQL Server](#authn-account-pword)</li><li>[Ne pas utiliser l’authentification SQL dans des bases de données à relation contenant-contenu](#autn-contained-db)</li></ul> |
| **Azure Event Hub** | <ul><li>[Utiliser les informations d’authentification par appareil à l’aide des jetons SAP](#authn-sas-tokens)</li></ul> |
| **Délimitation d’approbation Azure** | <ul><li>[Activer Azure Multi-Factor Authentication pour les administrateurs Azure](#multi-factor-azure-admin)</li></ul> |
| **Délimitation d’approbation Service Fabric** | <ul><li>[Restreindre l’accès anonyme tooService Cluster Fabric](#anon-access-cluster)</li><li>[Garantir que le certificat client à nœud Service Fabric est différent du certificat nœud à nœud](#fabric-cn-nn)</li><li>[Utilisez des clusters de l’ensemble fibre optique tooservice AAD tooauthenticate clients](#aad-client-fabric)</li><li>[Garantir que les certificats Service Fabric proviennent d’une autorité de certification approuvée](#fabric-cert-ca)</li></ul> |
| **IdentityServer** | <ul><li>[Utiliser des scénarios d’authentification standard pris en charge par IdentityServer](#standard-authn-id)</li><li>[Remplacer hello par défaut Identity Server cache de jeton avec une solution évolutive](#override-token)</li></ul> |
| **Délimitation d’approbation machine** | <ul><li>[Garantir que les fichiers binaires de l’application déployée sont signés numériquement](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[Activer l’authentification lors de la connexion tooMSMQ les files d’attente dans WCF](#msmq-queues)</li><li>[WCF-ne définissez pas de Message clientCredentialType toonone](#message-none)</li><li>[WCF-ne définissez pas le Transport clientCredentialType toonone](#transport-none)</li></ul> |
| **API Web** | <ul><li>[Assurez-vous que les techniques d’authentification standard sont utilisée toosecure API Web](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[Utiliser des scénarios d’authentification standard pris en charge par Azure Active Directory](#authn-aad)</li><li>[Remplacer hello par défaut ADAL cache de jeton avec une solution évolutive](#adal-scalable)</li><li>[Assurez-vous que TokenReplayCache est la relecture de hello tooprevent utilisé des jetons d’authentification ADAL](#tokenreplaycache-adal)</li><li>[Utiliser des bibliothèques ADAL toomanage jeton demande OAuth2 clients tooAAD (ou AD local)](#adal-oauth2)</li></ul> |
| **Passerelle de champ IoT** | <ul><li>[Authentifier les appareils toohello champ passerelle de connexion](#authn-devices-field)</li></ul> |
| **Passerelle de cloud IoT** | <ul><li>[Assurez-vous que les périphériques se connectant tooCloud passerelle sont authentifiés](#authn-devices-cloud)</li><li>[Utiliser les informations d’authentification par appareil](#authn-cred)</li></ul> |
| **Azure Storage** | <ul><li>[Assurez-vous que seul hello requise conteneurs et objets BLOB obtiennent un accès en lecture anonyme](#req-containers-anon)</li><li>[Accorder tooobjects un accès limité dans le stockage Azure à l’aide de disques SAS ou SAP](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>Envisagez d’utiliser un tooWeb tooauthenticate du mécanisme d’authentification standard Application

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| Détails | <p>L’authentification est le processus hello dans lequel une entité prouve son identité, généralement par le biais d’informations d’identification, telles qu’un nom d’utilisateur et un mot de passe. Il existe plusieurs protocoles d’authentification disponibles qui peuvent vous être utiles. Certains d’entre eux sont répertoriés ci-dessous :</p><ul><li>Certificats clients</li><li>Basé sur Windows</li><li>Basé sur des formulaires</li><li>Fédération - ADFS</li><li>Fédération - Azure AD</li><li>Fédération - IdentityServer</li></ul><p>Envisagez d’utiliser un processus de l’authentification standard mécanisme tooidentify hello source</p>|

## <a id="handle-failed-authn"></a>Les applications doivent gérer les scénarios d’authentification ayant échoué en toute sécurité 

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| Détails | <p>Les applications qui authentifient des utilisateurs explicitement doivent gérer les scénarios d’échec d’authentification securely.hello le mécanisme d’authentification doit :</p><ul><li>Refuser l’accès des ressources de tooprivileged lorsque l’authentification échoue</li><li>Afficher un message d’erreur générique après l’échec d’authentification et le refus de l’accès.</li></ul><p>Test des éléments suivants :</p><ul><li>Protection des ressources avec des privilèges après les échecs de connexion.</li><li>Un message d’erreur générique est affiché après les événements d’échec d’authentification et de refus de l’accès.</li><li>Les comptes sont désactivés après un nombre excessif d’échecs.</li><ul>|

## <a id="step-up-adaptive-authn"></a>Activer l’authentification adaptative ou avancée

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| Détails | <p>Vérifiez l’application hello a une autorisation supplémentaire (telle qu’intensifier ou authentification adaptative, via l’authentification multifacteur par exemple envoyer OTP dans SMS, etc. de courrier électronique ou demande une nouvelle authentification) afin de l’utilisateur de hello est un défi avant l’octroi d’accès informations de toosensitive. Cette règle s’applique également visant à rendre compte tooan de modifications critiques ou action</p><p>Cela signifie également qu’adaptation hello d’authentification a toobe implémenté de telle manière qu’application hello applique correctement contextuelle d’autorisation Autoriser ainsi en toonot manipulations non autorisées par le biais de dans l’exemple, falsification du paramètre</p>|

## <a id="admin-interface-lockdown"></a>Garantir que les interfaces d’administration sont correctement verrouillées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| Détails | Hello première solution est toogrant l’accès uniquement à partir d’une certaine source IP plage toohello interface d’administration. Si cette solution ne sera possible qu’il est toujours recommandé tooenforce une authentification Step-Up ou adaptative pour la connexion dans l’interface d’administration de hello |

## <a id="forgot-pword-fxn"></a>Implémenter des fonctionnalités de mot de passe oublié en toute sécurité

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| Détails | <p>Hello est première tooverify que vous avez oublié le mot de passe et d’autres chemins de récupération envoient un lien, y compris une durée limitée activation jeton au lieu de hello mot de passe. L’authentification supplémentaire sur soft-jetons (par exemple, les applications mobiles SMS jeton, natives, etc.) peut être nécessaire ainsi avant de lien de hello est envoyé via. En second lieu, vous ne devez pas verrouiller hello utilisateurs compte tout en hello d’obtention d’un nouveau mot de passe est en cours.</p><p>Cela peut entraîner des tooa par déni de service chaque fois qu’une personne malveillante décide toointentionally utilisateurs hello avec une attaque automatisée de verrouillage. Troisièmement, chaque fois que la nouvelle demande de mot de passe hello a été défini en cours d’exécution, vous affichez de message de salutation doit être généralisé dans l’énumération de commande tooprevent nom d’utilisateur. Quatrième, toujours interdire l’utilisation de hello d’anciens mots de passe et implémenter une stratégie de mot de passe fort.</p> |

## <a id="pword-account-policy"></a>Garantir que la stratégie de compte et de mot de passe est implémentée

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| Détails | <p>Une stratégie de compte et de mot de passe conforme à la stratégie et aux bonnes pratiques de l’organisation doit être implémentée.</p><p>toodefend contre les attaques en force et dictionnaire en fonction d’estimation : stratégie de mot de passe fort doit être implémenté tooensure que les utilisateurs créent le mot de passe complexe (par exemple, longueur minimale de 12 caractères, caractères spéciaux et alphanumériques).</p><p>Stratégies de verrouillage de compte peuvent être implémentées dans hello suivant de manière :</p><ul><li>**Verrouillage léger :** il peut s’agir d’une bonne option pour protéger vos utilisateurs des attaques en force brute. Par exemple, chaque fois que l’utilisateur de hello entre une application hello de trois fois de mot de passe incorrect pu verrouiller les compte hello une minute dans tooslow de commande du processus hello d’attaque en rendant moins rentables pour hello intrus tooproceed son mot de passe. Si vous étiez tooimplement dur contre-mesures de verrouillage pour cet exemple, vous devez obtenir un « Dos » par définitivement verrouillage des comptes. Vous pouvez également application peut générer un secret à usage unique (un mot de passe) et envoyez-la hors-bande (par courrier électronique, sms, etc.) toohello utilisateur. Une autre approche peut être tooimplement CAPTCHA après qu’un nombre de tentatives ayant échoué est atteint.</li><li>**Verrouillage de disque dur :** ce type de verrouillage doit être appliqué à chaque fois que vous détectez un utilisateur attaquer votre application et que vous lui compteur au moyen de verrouillage définitivement son compte jusqu'à ce qu’une équipe de réponse avait temps toodo leurs légales. Après ce processus, vous pouvez décider d’utilisateur hello toogive son compte ou prendre davantage de poursuites contre lui. Ce type d’approche empêche les intrus hello de pénétrer davantage de votre application et infrastructure.</li></ul><p>toodefend contre les attaques par défaut et les comptes prévisibles, vérifiez que toutes les clés et les mots de passe peut être remplacé et sont générés ou remplacés après l’heure de l’installation.</p><p>Si l’application hello a tooauto-générer des mots de passe, assurez-vous que les mots de passe hello généré sont aléatoires et disposer de forte entropie.</p>|

## <a id="controls-username-enum"></a>Énumération de mettre en œuvre des contrôles tooprevent nom d’utilisateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Tous les messages d’erreur doivent être généralisées dans l’énumération de commande tooprevent nom d’utilisateur. En outre, parfois vous ne pouvez pas éviter une fuite d’informations dans des fonctionnalités comme une page d’enregistrement. Ici, vous devez toouse débit maximal de méthodes comme CAPTCHA tooprevent une attaque automatisée par une personne malveillante. |

## <a id="win-authn-sql"></a>Si possible, utilisez l’authentification Windows pour la connexion tooSQL Server

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Local |
| **Attributs**              | Version SQL - Toutes |
| **Informations de référence**              | [SQL Server - Choisir un mode d’authentification](https://msdn.microsoft.com/library/ms144284.aspx) |
| **Étapes** | L’authentification Windows utilise le protocole de sécurité Kerberos, fournit une application de stratégie de mot de passe avec la validation de toocomplexity se soucier des mots de passe forts, prend en charge le verrouillage de compte et prend en charge d’expiration du mot de passe.|

## <a id="aad-authn-sql"></a>Lorsque cela est possible utiliser l’authentification Azure Active Directory pour tooSQL de connexion de base de données

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure |
| **Attributs**              | Version SQL - V12 |
| **Informations de référence**              | [TooSQL de connexion de base de données en utilisant authentification Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **Étapes** | **Version minimale :** V12 de base de données SQL Azure requis toouse de base de données SQL Azure tooallow l’authentification AAD contre hello Microsoft Directory |

## <a id="authn-account-pword"></a>Lorsque le mode d’authentification SQL est utilisé, garantir que la stratégie de compte et de mot de passe est appliquée sur SQL Server

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Stratégie de mot de passe SQL Server](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **Étapes** | Lorsque vous utilisez l’authentification SQL Server, les connexions sont créées dans SQL Server et ne sont pas basées sur les comptes d’utilisateur Windows. Hello nom d’utilisateur et mot de passe hello sont créées à l’aide de SQL Server et stockées dans SQL Server. SQL Server peut utiliser des mécanismes de stratégie de mot de passe Windows. Il peut appliquer hello mêmes stratégies de complexité et d’expiration utilisés dans toopasswords Windows utilisés à l’intérieur de SQL Server. |

## <a id="autn-contained-db"></a>Ne pas utiliser l’authentification SQL dans des bases de données à relation contenant-contenu

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Local, SQL Azure |
| **Attributs**              | Version SQL - MSSQL2012, Version SQL - V12 |
| **Informations de référence**              | [Meilleures pratiques de sécurité recommandées avec les bases de données à relation contenant-contenu](http://msdn.microsoft.com/library/ff929055.aspx) |
| **Étapes** | absence de Hello d’une stratégie de mot de passe appliquée peut augmenter la probabilité hello d’informations d’identification faible établie dans une base de données. Utilisez l’authentification Windows. |

## <a id="authn-sas-tokens"></a>Utiliser les informations d’authentification par appareil à l’aide des jetons SAP

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Event Hub | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du modèle de sécurité et de l’authentification Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Étapes** | <p>modèle de sécurité de concentrateurs d’événements Hello est basé sur une combinaison de jetons de Signature d’accès partagé (SAP) et d’éditeurs d’événements. nom du serveur de publication Hello représente hello DeviceID qui reçoit le jeton de hello. Cela permet d’associer des jetons hello générés avec les appareils hello respectifs.</p><p>Tous les messages sont marqués avec le donneur d’ordre côté service autorisant la détection de tentatives d’usurpation d’origine en charge utile. Lors de l’authentification des appareils, générer une par appareil SaS tooa étendue jeton unique de l’éditeur.</p>|

## <a id="multi-factor-azure-admin"></a>Activer Azure Multi-Factor Authentication pour les administrateurs Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Azure | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation d'Azure Multi-Factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **Étapes** | <p>L’authentification multifacteur (MFA) est une méthode d’authentification qui nécessite plus d’une méthode de vérification et ajoute une seconde couche critique de sécurité toouser connexions et transactions. Elle fonctionne avec deux ou plusieurs de hello les méthodes de vérification suivantes :</p><ul><li>Un élément que vous connaissez (généralement un mot de passe)</li><li>Un élément que vous possédez (un appareil de confiance qui n'est pas facilement dupliqué, comme un téléphone)</li><li>Un élément vous concernant particulièrement (biométrie)</li><ul>|

## <a id="anon-access-cluster"></a>Restreindre l’accès anonyme tooService Cluster Fabric

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Service Fabric | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Environnement - Azure  |
| **Informations de référence**              | [Scénarios de sécurité d’un cluster Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **Étapes** | <p>Clusters doivent toujours être tooprevent sécurisé non autorisé les utilisateurs de se connecter tooyour cluster, surtout quand les charges de production en cours d’exécution sur ce dernier.</p><p>Lors de la création d’un cluster service fabric, assurez-vous que le mode sécurité hello est défini trop « sécurisé » et configurer le certificat de serveur X.509 hello requis. Création d’un cluster « sécurisé » autorise tout tooit de tooconnect utilisateur anonyme si elle expose toohello de points de terminaison de gestion Internet public.</p>|

## <a id="fabric-cn-nn"></a>Garantir que le certificat client à nœud Service Fabric est différent du certificat nœud à nœud

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Service Fabric | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Environnement - Azure, environnement - Autonome |
| **Informations de référence**              | [Sécurité de certificat Client à un autre service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security), [cluster sécurisée du tooa se connecter à l’aide du certificat client](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **Étapes** | <p>Sécurité du certificat du client à ce nœud est configurée lors de la création de cluster de hello via hello portail Azure, modèles du Gestionnaire de ressources ou un modèle JSON autonome en spécifiant un certificat de client d’administration et/ou d’un certificat client utilisateur.</p><p>Hello administrateur client et l’utilisateur les certificats clients que vous spécifiez doivent être différentes de celle des certificats primaires et secondaires hello, que vous spécifiez pour la sécurité du nœud à l’autre.</p>|

## <a id="aad-client-fabric"></a>Utilisez des clusters de l’ensemble fibre optique tooservice AAD tooauthenticate clients

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Service Fabric | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Environnement - Azure |
| **Informations de référence**              | [Scénarios de sécurité d’un cluster - Recommandations en matière de sécurité](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **Étapes** | Les clusters en cours d’exécution sur Azure peuvent également sécuriser l’accès aux points de terminaison de gestion toohello à l’aide d’Azure Active Directory (AAD), indépendamment des certificats clients. Pour les clusters Azure, il est recommandé d’utiliser AAD sécurité tooauthenticate clients et les certificats pour la sécurité du nœud à l’autre.|

## <a id="fabric-cert-ca"></a>Garantir que les certificats Service Fabric proviennent d’une autorité de certification approuvée

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Service Fabric | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Environnement - Azure |
| **Informations de référence**              | [Certificats X.509 et Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **Étapes** | <p>Service Fabric utilise des certificats de serveur X.509 pour l’authentification des clients et des nœuds.</p><p>Tooconsider de certains points importants lors de l’utilisation de certificats dans les infrastructures de service :</p><ul><li>Les certificats utilisés dans les clusters qui exécutent des charges de travail de production doivent être créés en utilisant un service de certificats Windows Server correctement configuré ou obtenus auprès d’une autorité de certification approuvée. Hello autorité de certification peut être une autorité de certification externe approuvée ou un correctement géré Infrastructure à clé publique (PKI) interne</li><li>En production, n’utilisez jamais de certificats temporaires ou de test créés avec des outils comme MakeCert.exe.</li><li>Vous pouvez utiliser un certificat auto-signé, mais seulement pour les clusters de test et non en production.</li></ul>|

## <a id="standard-authn-id"></a>Utiliser des scénarios d’authentification standard pris en charge par IdentityServer

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | IdentityServer | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [IdentityServer3 - hello vue d’ensemble](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **Étapes** | <p>Voici des interactions standard pris en charge par le serveur d’identités hello :</p><ul><li>Les navigateurs communiquent avec les applications web.</li><li>Les applications web communiquent avec les API web (parfois pour elles-mêmes, parfois pour le compte d’un utilisateur).</li><li>Les applications basées sur un navigateur communiquent avec les API web.</li><li>Les applications natives communiquent avec les API web.</li><li>Les applications basées sur un serveur communiquent avec les API web.</li><li>Les API web communiquent avec les API web (parfois pour elles-mêmes, parfois pour le compte d’un utilisateur).</li></ul>|

## <a id="override-token"></a>Remplacer hello par défaut Identity Server cache de jeton avec une solution évolutive

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | IdentityServer | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Identity Server Deployment - Caching](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) (Déploiement d’IdentityServer - Mise en cache) |
| **Étapes** | <p>IdentityServer a un cache en mémoire intégré simple. Lorsque cela est approprié pour les applications natives à petite échelle, il n’est pas adaptée pour les applications de niveau et principaux mid pour hello suivant raisons :</p><ul><li>Ces applications sont accessibles par plusieurs utilisateurs simultanément. L’enregistrement de tous les jetons d’accès Bonjour même magasin crée des problèmes d’isolation et présente des problèmes lors du fonctionnement à l’échelle : de nombreux utilisateurs, chacun avec autant de jetons comme ressources de hello hello accède à des applications de leur part, peut signifier un nombre très élevé et très coûteux recherche opérations</li><li>Ces applications sont généralement déployées sur les topologies distribuées, où plusieurs nœuds doivent avoir accès toohello même cache</li><li>Les jetons mis en cache doivent survivre aux désactivations et recyclages de processus.</li><li>Pour tous les hello au-dessus de raisons, lors de l’implémentation des applications web, il est recommandé de cache de jeton du serveur identité toooverride hello par défaut avec une solution évolutive telles que le cache Azure Redis</li></ul>|

## <a id="binaries-signed"></a>Garantir que les fichiers binaires de l’application déployée sont signés numériquement

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Vérifiez que les fichiers binaires de l’application déployée sont signés numériquement afin que l’intégrité de hello des fichiers binaires de hello peut être vérifiée|

## <a id="msmq-queues"></a>Activer l’authentification lors de la connexion tooMSMQ les files d’attente dans WCF

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, NET Framework 3 |
| **Attributs**              | N/A |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **Étapes** | Programme échoue tooenable authentification lors de la connexion tooMSMQ les files d’attente, une personne malveillante peut soumettre file d’attente de messages toohello pour le traitement de façon anonyme. Si l’authentification n’est pas utilisé tooconnect tooan MSMQ file d’attente utilisée toodeliver un programme tooanother de message, un attaquant pourrait envoyer un message malveillant anonyme.|

### <a name="example"></a>Exemple
Hello `<netMsmqBinding/>` élément du fichier de configuration WCF hello ci-dessous fait en sorte que l’authentification de WCF toodisable lors de la connexion de file d’attente MSMQ tooan pour la remise du message.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
Configurer l’authentification de domaine Windows ou le certificat du toorequire MSMQ en permanence pour les messages entrants ou sortants.

### <a name="example"></a>Exemple
Hello `<netMsmqBinding/>` élément du fichier de configuration WCF hello ci-dessous indique à l’authentification du certificat tooenable WCF lors de la file d’attente MSMQ de tooan de connexion. client de Hello est authentifié à l’aide de certificats X.509. certificat de client Hello doit être présent dans le magasin de certificats hello du serveur de hello.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>WCF-ne définissez pas de Message clientCredentialType toonone

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework 3 |
| **Attributs**              | Type d’informations d’identification client - Aucun |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | absence de Hello d’authentification signifie que tout le monde est en mesure de tooaccess ce service. Un service qui n’authentifie pas ses clients autorise l’accès aux utilisateurs de tooall. Configurer tooauthenticate d’application hello par rapport aux informations d’identification du client. Cela est possible en définissant hello message clientCredentialType tooWindows ou certificat. |

### <a name="example"></a>Exemple
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>WCF-ne définissez pas le Transport clientCredentialType toonone

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, .NET Framework 3 |
| **Attributs**              | Type d’informations d’identification client - Aucun |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | absence de Hello d’authentification signifie que tout le monde est en mesure de tooaccess ce service. Un service qui n’authentifie pas ses clients permet à tous les utilisateurs tooaccess ses fonctionnalités. Configurer tooauthenticate d’application hello par rapport aux informations d’identification du client. Cela est possible en définissant hello transport clientCredentialType tooWindows ou certificat. |

### <a name="example"></a>Exemple
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>Assurez-vous que les techniques d’authentification standard sont utilisée toosecure API Web

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Authentication and Authorization in ASP.NET Web API](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) (Authentification et autorisation dans l’API web ASP.NET), [External Authentication Services with ASP.NET Web API (C#)](http://www.asp.net/web-api/overview/security/external-authentication-services) (Services d’authentification externe avec l’API web ASP.NET (C#)) |
| **Étapes** | <p>L’authentification est le processus hello dans lequel une entité prouve son identité, généralement par le biais d’informations d’identification, telles qu’un nom d’utilisateur et un mot de passe. Il existe plusieurs protocoles d’authentification disponibles qui peuvent vous être utiles. Certains d’entre eux sont répertoriés ci-dessous :</p><ul><li>Certificats clients</li><li>Basé sur Windows</li><li>Basé sur des formulaires</li><li>Fédération - ADFS</li><li>Fédération - Azure AD</li><li>Fédération - IdentityServer</li></ul><p>Dans la section des références hello fournissent des détails de bas niveau sur la façon dont chacun des schémas d’authentification hello peut être implémentée toosecure une API Web.</p>|

## <a id="authn-aad"></a>Utiliser des scénarios d’authentification standard pris en charge par Azure Active Directory

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure AD | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Scénarios d’authentification pour Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/), [Exemples de code Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/), [Guide du développeur Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **Étapes** | <p>Azure Active Directory (Azure AD) simplifie l’authentification pour les développeurs en fournissant l’identité en tant que service, avec la prise en charge des protocoles standard tels que OAuth 2.0 et OpenID Connect. Voici hello cinq principaux scénarios d’application pris en charge par Azure AD :</p><ul><li>Web Browser tooWeb Application : un utilisateur doit toosign dans l’application web tooa sécurisée par Azure AD</li><li>Application à Page unique (SPA) : Un utilisateur doit toosign dans tooa application à page unique sécurisée par Azure AD</li><li>Native tooWeb Application API : une application native qui s’exécute sur un téléphone, tablette ou un PC besoins tooauthenticate un tooget utilisateur ressources à partir d’une API web sécurisée par Azure AD</li><li>Web Application tooWeb API : tooget des ressources à partir d’une API web sécurisée par Azure AD a besoin d’une application web</li><li>Application démon ou serveur tooWeb API : tooget des ressources à partir d’une API web sécurisée par Azure AD a besoin d’une application démon ou une application serveur sans aucune interface utilisateur web</li></ul><p>Pour les détails d’implémentation de bas niveau, consultez toohello les liens dans la section des références hello</p>|

## <a id="adal-scalable"></a>Remplacer hello par défaut ADAL cache de jeton avec une solution évolutive

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure AD | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Modern Authentication with Azure Active Directory for Web Applications](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) (Authentification moderne avec Azure Active Directory pour les applications web), [Using Redis as ADAL token cache](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/) (Utilisation de Redis en tant que cache de jeton ADAL)  |
| **Étapes** | <p>cache par défaut Hello qui utilise de la bibliothèque ADAL (Active Directory Authentication Library) est un cache en mémoire qui s’appuie sur un magasin statique, disponible au niveau du processus. Bien que cela fonctionne pour les applications natives, il n’est pas adaptée pour les applications de niveau et principaux mid pour hello suivant raisons :</p><ul><li>Ces applications sont accessibles par plusieurs utilisateurs simultanément. L’enregistrement de tous les jetons d’accès Bonjour même magasin crée des problèmes d’isolation et présente des problèmes lors du fonctionnement à l’échelle : de nombreux utilisateurs, chacun avec autant de jetons comme ressources de hello hello accède à des applications de leur part, peut signifier un nombre très élevé et très coûteux recherche opérations</li><li>Ces applications sont généralement déployées sur les topologies distribuées, où plusieurs nœuds doivent avoir accès toohello même cache</li><li>Les jetons mis en cache doivent survivre aux désactivations et recyclages de processus.</li></ul><p>Pour tous les hello au-dessus de raisons, lors de l’implémentation des applications web, il est recommandé de cache jeton ADAL par défaut toooverride hello avec une solution évolutive telles que le cache Azure Redis.</p>|

## <a id="tokenreplaycache-adal"></a>Assurez-vous que TokenReplayCache est la relecture de hello tooprevent utilisé des jetons d’authentification ADAL

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure AD | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Modern Authentication with Azure Active Directory for Web Applications](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) (Authentification moderne avec Azure Active Directory pour les applications web) |
| **Étapes** | <p>propriété TokenReplayCache de Hello autorise les développeurs toodefine un cache de relecture de jetons, un magasin qui peut être utilisé pour l’enregistrement à des fins de hello permettant de vérifier que les jetons aucun jeton peut être utilisé plusieurs fois.</p><p>Il s’agit d’une mesure par rapport à une attaque courante, hello invoque appelé attaque de relecture de jetons : un attaquant intercepte le jeton hello envoyé à la connexion peut tenter de toosend il application toohello à nouveau (« relire ») pour l’établissement d’une nouvelle session. Par exemple, dans OIDC-octroi d’un code flux, après une authentification réussie de l’utilisateur, une demande trop « / signin-oidc « point de terminaison de la partie de confiance hello est effectuée avec « id_token », « code » et « état » paramètres.</p><p>Hello de confiance valide cette demande et établit une nouvelle session. Si un adversaire capture cette demande et il relit, il peut établir une session réussie et un utilisateur de hello d’usurpation d’identité. présence de Hello de nonce hello dans OpenID Connect peut limiter mais pas complètement éliminer les circonstances hello dans lequel les attaques hello peuvent être mises en œuvre avec succès. tooprotect leurs applications, les développeurs peuvent fournir une implémentation de ITokenReplayCache et affecter une instance tooTokenReplayCache.</p>|

### <a name="example"></a>Exemple
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>Exemple
Voici un exemple d’implémentation de l’interface de ITokenReplayCache hello. (Veuillez personnaliser et mettre en œuvre votre infrastructure de mise en cache spécifique au projet)
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
Hello implémentée en cache a toobe référencé dans options OIDC via hello « TokenValidationParameters » propriété comme suit.
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

Notez qu’efficacité de hello tootest de cette configuration, la connexion dans votre application protégée OIDC locale et capturer les demande hello trop`"/signin-oidc"` point de terminaison dans fiddler. Lors de la protection de hello n’est pas en place, la relecture de cette demande dans fiddler définit un nouveau cookie de session. Lors de la demande de hello est relu après avoir ajouté hello TokenReplayCache protection, application hello lève une exception comme suit :`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>Utiliser des bibliothèques ADAL toomanage jeton demande OAuth2 clients tooAAD (ou AD local)

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure AD | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **Étapes** | <p>Hello Azure AD authentication Library (ADAL) permet de client application développeurs tooeasily authentifier les utilisateurs toocloud ou Active Directory (AD) local et ainsi profiter des jetons d’accès pour sécuriser les appels d’API.</p><p>ADAL possède de nombreuses fonctionnalités qui facilitent l'authentification aux développeurs, notamment la prise en charge asynchrone, un cache de jeton configurable qui stocke les jetons d'accès et les jetons d'actualisation, l'actualisation automatique des jetons lorsqu'un jeton d'accès expire et qu’un jeton d'actualisation est disponible, et bien plus encore.</p><p>En gérant la plupart de complexité de hello, la bibliothèque ADAL peut aider le développeur de se concentrer sur la logique métier dans leur application et sécuriser facilement les ressources sans être un expert en sécurité. Des bibliothèques distinctes sont disponibles pour .NET, JavaScript (client et Node.js), iOS, Android et Java.</p>|

## <a id="authn-devices-field"></a>Authentifier les appareils toohello champ passerelle de connexion

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de champ IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Assurez-vous que chaque appareil est authentifié par le champ passerelle de hello avant d’accepter des données et de faciliter les communications en amont avec hello passerelle de Cloud. En outre, assurez-vous que les appareils se connectent avec des informations d’identification par appareil, afin que chaque appareil puisse être identifié de manière unique.|

## <a id="authn-devices-cloud"></a>Assurez-vous que les périphériques se connectant tooCloud passerelle sont authentifiés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, C#, Node.JS  |
| **Attributs**              | N/A, choix de passerelle - Azure IoT Hub |
| **Informations de référence**              | N/A, [Mise en route d’Azure IoT Hub (.NET)](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/), [Mise en route d’Azure IoT Hub (Node)](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted), [Contrôler l’accès à IoT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/), [référentiel Git](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **Étapes** | <ul><li>**Générique :** appareil de hello authentifier à l’aide de la sécurité TLS (Transport Layer) ou IPSec. L’infrastructure doit prendre en charge l’utilisation d’une clé prépartagée (PSK) sur les périphériques qui ne peuvent pas gérer le chiffrement asymétrique complet. Utilisez Azure AD, OAuth.</li><li>**C# :** lors de la création d’une instance DeviceClient, par défaut, hello méthode Create crée une instance de DeviceClient qui utilise toocommunicate de protocole AMQP hello avec IoT Hub. toouse hello le protocole HTTPS, utilisez remplacement hello de méthode Create hello qui vous permet de protocole de hello toospecify. Si vous utilisez le protocole HTTPS hello, vous devez également ajouter hello `Microsoft.AspNet.WebApi.Client` hello de NuGet package tooyour projet tooinclude `System.Net.Http.Formatting` espace de noms.</li></ul>|

### <a name="example"></a>Exemple
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>Exemple
**Node.JS : authentification**
#### <a name="symmetric-key"></a>Clé symétrique
* Créez un IoT Hub sur Azure.
* Créer une entrée dans le Registre des identités hello appareil
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* Créez un appareil simulé.
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>Jeton SAP
* Généré en interne lors de l’utilisation de la clé symétrique, mais nous pouvons le générer et l’utiliser explicitement également.
* Définissez un protocole : `var Http = require('azure-iot-device-http').Http;`.
* Créez un jeton SAP :
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* Connectez-vous à l’aide du jeton SAP : 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>Certificats
* Générer un personnel X509 signé certificat à l’aide d’un outil tel que OpenSSL toogenerate une .cert .key fichiers toostore hello hello et certificat de clé et respectivement
* Approvisionnez un appareil qui accepte une connexion sécurisée à l’aide de certificats.
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* Connectez un appareil à l’aide d’un certificat.
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>Utiliser les informations d’authentification par appareil

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT  | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | Choix de passerelle - Azure IoT Hub |
| **Informations de référence**              | [Contrôler l’accès à IoT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **Étapes** | Utilisez des informations d’authentification par appareil à l’aide des jetons SAP en fonction de la clé d’appareil ou du certificat de client plutôt que des stratégies d’accès partagé au niveau d’IoT Hub. Cela empêche la réutilisation de hello des jetons d’authentification d’une passerelle de périphérique ou un champ par un autre |

## <a id="req-containers-anon"></a>Assurez-vous que seul hello requise conteneurs et objets BLOB obtiennent un accès en lecture anonyme

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | StorageType - Blob |
| **Informations de référence**              | [Gérer l’accès en lecture anonyme toocontainers et les objets BLOB](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/), [Signatures d’accès partagé, partie 1 : modèle de présentation hello SAP](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **Étapes** | <p>Par défaut, un conteneur et tous les objets BLOB qu’il contient sont accessibles uniquement par le propriétaire de hello hello du compte de stockage. conteneur de tooa toogive les utilisateurs anonymes des autorisations en lecture et ses objets BLOB, une peut définir un accès public tooallow hello conteneur des autorisations. Utilisateurs anonymes peuvent lire des objets BLOB dans un conteneur accessible publiquement sans authentifier la demande de hello.</p><p>Les conteneurs fournissent hello options pour la gestion des accès au conteneur suivantes :</p><ul><li>Accès public en lecture : les données de conteneur et de blob peuvent être lues via une demande anonyme. Les clients peuvent énumérer des objets BLOB dans le conteneur hello via une demande anonyme, mais ne peut pas énumérer des conteneurs dans le compte de stockage hello.</li><li>Accès public en lecture pour les blobs uniquement : les données de blobs à l’intérieur de ce conteneur peuvent être lues via une demande anonyme, mais les données du conteneur ne sont pas disponibles. Les clients ne peuvent pas énumérer les objets BLOB conteneur hello via une demande anonyme</li><li>Accès en lecture sans public : données de conteneur et les objets blob peuvent être lues par le propriétaire du compte hello</li></ul><p>L’accès anonyme est idéal dans les situations où certains blobs doivent toujours être disponibles pour l’accès en lecture anonyme. Pour un contrôle plus précise, un peut créer une signature d’accès partagé, ce qui permet un accès toodelegate restreint à l’aide des autorisations différentes et sur un intervalle de temps spécifié. Garantissez que les conteneurs et les blobs, qui peuvent éventuellement contenir des données sensibles, ne bénéficient pas d’un accès anonyme accidentellement.</p>|

## <a id="limited-access-sas"></a>Accorder tooobjects un accès limité dans le stockage Azure à l’aide de disques SAS ou SAP

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A |
| **Informations de référence**              | [Signatures d’accès partagé, partie 1 : Modèle de SAP de hello présentation](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/), [Signatures d’accès partagé, partie 2 : créer et utiliser une SAP de stockage d’objets Blob](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/), [comment toodelegate aux tooobjects dans votre compte à l’aide Les stratégies d’accès stockée et les Signatures d’accès partagé](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **Étapes** | <p>À l’aide d’une signature d’accès partagé (SAS) est un tooobjects d’accès toogrant limitée efficace dans un compte tooother les clients de stockage, sans avoir de clé d’accès tooexpose compte. Hello SAS est un URI qui englobe dans ses paramètres de requête toutes les informations de hello nécessaires pour l’authentification d’accès tooa des ressources de stockage. tooaccess des ressources de stockage avec hello SAS, hello client a uniquement besoin toopass dans le constructeur approprié de hello SAS toohello ou la méthode.</p><p>Vous pouvez utiliser une SAP lorsque vous souhaitez tooprovide accès tooresources dans votre client de tooa de compte de stockage ne peut pas être approuvée par la clé de compte hello. Vos clés de compte de stockage incluent à la fois une clé primaire et secondaire, les deux accorder un accès administratif tooyour compte et toutes les ressources qu’il hello. Exposition de vos clés de compte s’ouvre votre possibilité de toohello compte d’utilisation malveillante ou involontaire. Signatures d’accès partagé offrent une solution sécurisée qui permet aux autres clients tooread, écriture et suppression des données dans votre compte de stockage selon que vous avez accordé des autorisations toohello et sans avoir besoin de la clé de compte hello.</p><p>Si vous avez un ensemble logique de paramètres qui sont chaque fois similaires, il est plus judicieux d’utiliser une stratégie d’accès stockée. À l’aide d’un SAS dérivé d’une stratégie d’accès stockée vous donne en effet toorevoke de capacité hello que SAS immédiatement, il est hello recommandé de meilleure pratique tooalways utiliser des stratégies d’accès stockées lorsque cela est possible.</p>|
