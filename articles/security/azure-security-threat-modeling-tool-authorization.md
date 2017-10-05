---
title: "Autorisation - Outil Microsoft de modélisation des menaces - Azure | Microsoft Docs"
description: "mesures de correction des menaces exposées dans l’outil de modélisation des menaces"
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
ms.openlocfilehash: 312a66544a5e64daa86b4902b57d4050f1f66af5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-authorization--mitigations"></a>Infrastructure de sécurité : Autorisation | Mesures de correction 
| Produit/service | Article |
| --------------- | ------- |
| **Délimitation d’approbation machine** | <ul><li>[Vérifier que les ACL appropriées sont configurées pour limiter l’accès non autorisé aux données sur l’appareil](#acl-restricted-access)</li><li>[Vérifier que le contenu sensible d’application spécifique à l’utilisateur est stocké dans le répertoire du profil utilisateur](#sensitive-directory)</li><li>[Vérifier que les applications déployées sont exécutées avec des privilèges minimum](#deployed-privileges)</li></ul> |
| **Application web** | <ul><li>[Appliquer l’ordre d’étapes séquentiel pendant le traitement du flux de logique d’entreprise](#sequential-logic)</li><li>[Implémenter le mécanisme de limitation du débit pour empêcher une énumération](#rate-enumeration)</li><li>[Vérifier que l’autorisation appropriée est en place et que le principe de privilèges minimum est respecté](#principle-least-privilege)</li><li>[Les décisions de logique d’entreprise et d’autorisation d’accès aux ressources ne doivent pas être basées sur les paramètres de demande entrante](#logic-request-parameters)</li><li>[Vérifier que le contenu et les ressources ne sont pas énumérables ou accessibles via la navigation forcée](#enumerable-browsing)</li></ul> |
| **Base de données** | <ul><li>[Vérifier que des comptes avec des privilèges minimum sont utilisés pour se connecter au serveur de base de données](#privileged-server)</li><li>[Implémenter la sécurité au niveau des lignes (RLS) pour empêcher les locataires d’accéder aux données des autres](#rls-tenants)</li><li>[Le rôle Administrateur système doit comporter uniquement des utilisateurs valides nécessaires](#sysadmin-users)</li></ul> |
| **Passerelle de cloud IoT** | <ul><li>[Se connecter à la passerelle de cloud à l’aide de jetons avec des privilèges minimum](#cloud-least-privileged)</li></ul> |
| **Hub d'événement d'Azure** | <ul><li>[Utiliser une clé SAP d’autorisations d’envoi seulement pour générer des jetons d’appareil](#sendonly-sas)</li><li>[Ne pas utiliser des jetons d’accès qui fournissent un accès direct au concentrateur d’événement](#access-tokens-hub)</li><li>[Se connecter au concentrateur d’événement à l’aide des clés SAP qui disposent des autorisations minimales requises](#sas-minimum-permissions)</li></ul> |
| **Azure Document DB** | <ul><li>[Utiliser autant que possible des jetons de ressource pour se connecter à DocumentDB](#resource-docdb)</li></ul> |
| **Délimitation d’approbation Azure** | <ul><li>[Activer la gestion des accès précis à un abonnement Azure à l’aide de RBAC](#grained-rbac)</li></ul> |
| **Délimitation d’approbation Service Fabric** | <ul><li>[Restreindre l’accès client aux opérations de cluster à l’aide de RBAC](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[Effectuer la modélisation de sécurité et utiliser la sécurité au niveau des champs si nécessaire](#modeling-field)</li></ul> |
| **Portail Dynamics CRM** | <ul><li>[Effectuer la modélisation de sécurité des comptes du portail en gardant à l’esprit que le modèle de sécurité pour le portail est différent du reste de CRM](#portal-security)</li></ul> |
| **Azure Storage** | <ul><li>[Accorder une autorisation précise sur un ensemble d’entités dans Azure Table Storage](#permission-entities)</li><li>[Activer le contrôle d’accès en fonction du rôle (RBAC) sur le compte de stockage Azure à l’aide d’Azure Resource Manager](#rbac-azure-manager)</li></ul> |
| **Client mobile** | <ul><li>[Implémenter la libération implicite ou la détection du rootage](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[Référence de classe faible dans WCF](#weak-class-wcf)</li><li>[WCF - Implémenter le contrôle de l’autorisation](#wcf-authz)</li></ul> |
| **API Web** | <ul><li>[Implémenter le mécanisme d’autorisation approprié dans l’API web ASP.NET](#authz-aspnet)</li></ul> |
| **Appareil IoT** | <ul><li>[Effectuer des vérifications d’autorisation dans l’appareil s’il prend en charge diverses actions nécessitant différents niveaux d’autorisation](#device-permission)</li></ul> |
| **Passerelle de champ IoT** | <ul><li>[Effectuer des vérifications d’autorisation dans la passerelle de champ si elle prend en charge diverses actions nécessitant différents niveaux d’autorisation](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>Vérifier que les ACL appropriées sont configurées pour limiter l’accès non autorisé aux données sur l’appareil

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Vérifier que les ACL appropriées sont configurées pour limiter l’accès non autorisé aux données sur l’appareil|

## <a id="sensitive-directory"></a>Vérifier que le contenu sensible d’application spécifique à l’utilisateur est stocké dans le répertoire du profil utilisateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Vérifiez que le contenu sensible d’application spécifique à l’utilisateur est stocké dans le répertoire du profil utilisateur. Cela vise à empêcher plusieurs utilisateurs de la machine d’accéder aux données des autres.|

## <a id="deployed-privileges"></a>Vérifier que les applications déployées sont exécutées avec des privilèges minimum

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Vérifiez que l’application déployée est exécutée avec des privilèges minimum. |

## <a id="sequential-logic"></a>Appliquer l’ordre d’étapes séquentiel pendant le traitement du flux de logique d’entreprise

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Pour vérifier que cette étape a été exécutée par un utilisateur authentique, vous souhaitez forcer l’application à ne traiter que les flux de logique d’entreprise dans l’ordre séquentiel des étapes, toutes les étapes étant traitées sur une durée humainement réaliste, et à ne pas traiter des étapes ignorées externes à l’ordre, des étapes traitées par un autre utilisateur ou des transactions soumises trop rapidement.|

## <a id="rate-enumeration"></a>Implémenter le mécanisme de limitation du débit pour empêcher une énumération

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Vérifiez que les identificateurs sensibles sont aléatoires. Implémentez le contrôle CAPTCHA sur les pages anonymes. Vérifier que les erreurs et les exceptions ne révèlent pas de données spécifiques|

## <a id="principle-least-privilege"></a>Vérifier que l’autorisation appropriée est en place et que le principe de privilèges minimum est respecté

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Le principe implique de n’accorder à un compte d’utilisateur que les privilèges essentiels pour que les utilisateurs puissent travailler. Par exemple, un utilisateur de sauvegarde n’a pas besoin d’installer de logiciels : l’utilisateur de sauvegarde dispose donc uniquement de droits d’exécution et d’applications liées à la sauvegarde. Tous les autres privilèges, comme l’installation de nouveaux logiciels, sont bloqués. Le principe s’applique également à un utilisateur d’ordinateur personnel qui utilise généralement un compte d’utilisateur normal et ouvre un compte privilégié, protégé par mot de passe (à savoir, un superutilisateur), uniquement lorsque la situation l’exige. </p><p>Ce principe peut également être appliqué à vos applications web. Plutôt que de dépendre uniquement de méthodes d’authentification basées sur le rôle à l’aide de sessions, nous souhaitons affecter des privilèges aux utilisateurs au moyen d’un système d’authentification basé sur la base de données. Nous utilisons toujours des sessions pour déterminer si l’utilisateur s’est connecté correctement. Mais plutôt que d’attribuer à cet utilisateur un rôle spécifique, nous lui accordons maintenant des privilèges pour vérifier les actions qu’il est autorisé à effectuer sur le système. Un avantage considérable de cette méthode est tel que, lorsque des privilèges inférieurs doivent être accordés à un utilisateur, vos modifications sont appliquées à la volée car l’affectation ne dépend pas la session qui arriverait à expiration en premier.</p>|

## <a id="logic-request-parameters"></a>Les décisions de logique d’entreprise et d’autorisation d’accès aux ressources ne doivent pas être basées sur les paramètres de demande entrante

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Chaque fois que vous vérifiez si un utilisateur est limité à la consultation de certaines données, les restrictions d’accès doivent être traitées côté serveur. L’ID utilisateur doit être stocké dans une variable de session au moment de la connexion et doit être utilisé pour récupérer les données utilisateur dans la base de données |

### <a name="example"></a>Exemple
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
Un éventuel intrus ne peut désormais plus altérer ni modifier l’opération de l’application, car l’identificateur de récupération des données est géré côté serveur.

## <a id="enumerable-browsing"></a>Vérifier que le contenu et les ressources ne sont pas énumérables ou accessibles via la navigation forcée

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Les fichiers statiques et de configuration sensibles ne doivent pas être conservés dans le webroot. Pour le contenu ne devant pas être rendu public, des contrôles d’accès appropriés doivent être appliqués ou le contenu lui-même doit être supprimé.</p><p>De plus, la navigation forcée est généralement combinée à des techniques de force brute pour collecter des informations en tentant d’accéder au plus grand nombre d’URL possible afin d’énumérer des répertoires et des fichiers sur un serveur. Les personnes malveillantes peuvent vérifier toutes les variantes des fichiers existants généralement. Par exemple, la recherche de fichiers de mot de passe peut englober des fichiers tels que psswd.txt, password.htm, password.dat et d’autres variations.</p><p>Pour corriger ce problème, des fonctionnalités de tentatives de détection en force brute doivent être incluses.</p>|

## <a id="privileged-server"></a>Vérifier que des comptes avec des privilèges minimum sont utilisés pour se connecter au serveur de base de données

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Hiérarchie des autorisations de base de données SQL](https://msdn.microsoft.com/library/ms191465), [éléments sécurisables de base de données SQL](https://msdn.microsoft.com/library/ms190401) |
| **Étapes** | Des comptes avec des privilèges minimum doivent être utilisés pour se connecter à la base de données. La connexion d’application doit être limitée dans la base de données et ne doit exécuter que des procédures stockées sélectionnées. La connexion de l’application ne doit pas disposer d’un accès direct à la table. |

## <a id="rls-tenants"></a>Implémenter la sécurité au niveau des lignes (RLS) pour empêcher les locataires d’accéder aux données des autres

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure, local |
| **Attributs**              | Version SQL - V12, Version SQL - MsSQL2016 |
| **Informations de référence**              | [SQL Server - Sécurité au niveau des lignes (RLS)](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **Étapes** | <p>La sécurité au niveau des lignes permet aux clients de contrôler l’accès aux lignes d’une table de base de données en fonction des caractéristiques de l’utilisateur qui exécute une requête (par exemple, appartenance à un groupe ou contexte d’exécution).</p><p>La sécurité au niveau des lignes (RLS) simplifie la conception et le codage de la sécurité dans votre application. Elle vous permet d’implémenter des restrictions sur l’accès aux lignes de données. Par exemple, en s’assurant que les employés ne peuvent accéder qu’aux lignes de données utiles à leur service, ou en limitant l’accès aux données d’un client aux données relatives à son entreprise uniquement.</p><p>La logique de restriction d’accès se situe dans la couche de base de données plutôt qu’à l’écart des données d’une autre couche d’application. Le système de base de données applique les restrictions d’accès chaque fois qu’un accès aux données est tenté à partir d’un quelconque niveau. Le système de sécurité est ainsi plus fiable et plus robuste en réduisant la surface d’exposition du système de sécurité.</p><p>|

Veuillez noter que la RLS comme fonctionnalité de base de données prête à l’emploi s’applique uniquement à partir de SQL Server 2016 et à la base de données SQL Azure. Si la fonctionnalité RLS prête à l’emploi n’est pas implémentée, assurez-vous que l’accès aux données est limité à l’aide de vues et de procédures

## <a id="sysadmin-users"></a>Le rôle Administrateur système doit comporter uniquement des utilisateurs valides nécessaires

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Hiérarchie des autorisations de base de données SQL](https://msdn.microsoft.com/library/ms191465), [éléments sécurisables de base de données SQL](https://msdn.microsoft.com/library/ms190401) |
| **Étapes** | Les membres du rôle serveur fixe SysAdmin doivent être très limités et ne doivent jamais contenir des comptes utilisés par des applications.  Veuillez consulter la liste des utilisateurs du rôle et supprimer les comptes inutiles|

## <a id="cloud-least-privileged"></a>Se connecter à la passerelle de cloud à l’aide de jetons avec des privilèges minimum

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Choix de passerelle - Azure IoT Hub |
| **Informations de référence**              | [Contrôle d’accès IOT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **Étapes** | Accordez des autorisations avec des privilèges minimum à divers composants qui se connectent à la passerelle de cloud (IoT Hub). Un exemple typique est le composant de gestion des appareils/d’approvisionnement qui utilise registryread/write et Event Processor (ASA) qui utilise Service Connect. Les appareils individuels se connectent à l’aide d’informations d’identification d’appareil|

## <a id="sendonly-sas"></a>Utiliser une clé SAP d’autorisations d’envoi seulement pour générer des jetons d’appareil

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Event Hub | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du modèle de sécurité et de l’authentification Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Étapes** | Une clé SAP est utilisée pour générer des jetons d’appareils individuels. Utiliser une clé SAP d’autorisations d’envoi seulement pendant la génération du jeton d’appareil pour un éditeur donné|

## <a id="access-tokens-hub"></a>Ne pas utiliser des jetons d’accès qui fournissent un accès direct au concentrateur d’événement

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Event Hub | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du modèle de sécurité et de l’authentification Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Étapes** | Un jeton qui accorde un accès direct au concentrateur d’événement ne doit pas être fourni à l’appareil. L’utilisation d’un jeton avec des privilèges minimum pour l’appareil, qui n’accorde l’accès qu’à un éditeur, permet d’identifier et de bloquer un appareil s’il est jugé non fiable ou compromis.|

## <a id="sas-minimum-permissions"></a>Se connecter au concentrateur d’événement à l’aide des clés SAP qui disposent des autorisations minimales requises

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Event Hub | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du modèle de sécurité et de l’authentification Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Étapes** | Accordez des autorisations avec des privilèges minimum à diverses applications principales qui se connectent au concentrateur d’événement. Générez des clés SAP distinctes pour chaque application principale et n’accordez que les autorisations requises (envoi, réception ou gestion).|

## <a id="resource-docdb"></a>Utiliser des jetons de ressource pour se connecter à Azure Cosmos DB le cas échéant

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Document DB | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Un jeton de ressource est associé à une ressource d'autorisation DocumentDB et capture la relation entre l'utilisateur d'une base de données et l'autorisation dont cet utilisateur dispose pour une ressource d'application DocumentDB spécifique (collection, document, etc.). Utilisez toujours un jeton de ressource pour accéder à DocumentDB si le client ne peut pas être approuvé avec la gestion des clés principales ou en lecture seule, par exemple une application d’utilisateur final comme un client mobile ou de bureau. Utilisez une clé principale ou des clés en lecture seule d’applications principales capables de stocker ces clés en toute sécurité.|

## <a id="grained-rbac"></a>Activer la gestion des accès précis à un abonnement Azure à l’aide de RBAC

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Azure | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Utiliser les attributions de rôle pour gérer l’accès à vos ressources d’abonnement Azure](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **Étapes** | Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour Azure. L’utilisation de RBAC vous permet de n’accorder que les droits d’accès dont les utilisateurs ont besoin pour effectuer leur travail.|

## <a id="cluster-rbac"></a>Restreindre l’accès client aux opérations de cluster à l’aide de RBAC

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Service Fabric | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Environnement - Azure |
| **Informations de référence**              | [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **Étapes** | <p>Azure Service Fabric prend en charge deux types de contrôle d’accès différents pour les clients qui sont connectés à un cluster Service Fabric : administrateur et utilisateur. Le contrôle d'accès permet à l'administrateur du cluster de limiter l'accès à certaines opérations de cluster pour différents groupes d'utilisateurs, renforçant ainsi la sécurité du cluster.</p><p>Les administrateurs ont un accès complet aux fonctions de gestion (y compris les fonctionnalités de lecture/écriture). Les utilisateurs, par défaut, ont uniquement un accès en lecture aux fonctionnalités de gestion (par exemple, aux fonctionnalités de requête) et la capacité à résoudre les applications et les services.</p><p>Vous spécifiez les deux rôles clients (client et administrateur) au moment de la création du cluster en fournissant des certificats séparés pour chacun.</p>|

## <a id="modeling-field"></a>Effectuer la modélisation de sécurité et utiliser la sécurité au niveau des champs si nécessaire

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Effectuer la modélisation de sécurité et utiliser la sécurité au niveau des champs si nécessaire|

## <a id="portal-security"></a>Effectuer la modélisation de sécurité des comptes du portail en gardant à l’esprit que le modèle de sécurité pour le portail est différent du reste de CRM

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Portail Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Effectuer la modélisation de sécurité des comptes du portail en gardant à l’esprit que le modèle de sécurité pour le portail est différent du reste de CRM|

## <a id="permission-entities"></a>Accorder une autorisation précise sur un ensemble d’entités dans Azure Table Storage

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | StorageType - Table |
| **Informations de référence**              | [Comment déléguer l’accès aux objets dans votre compte de stockage Azure à l’aide de SAP](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **Étapes** | Dans certains scénarios d’entreprise, Azure Table Storage peut être nécessaire pour stocker des données sensibles répondant aux besoins des différentes parties. Par exemple, les données sensibles relatives aux différents pays. Dans ce cas, les signatures SAP peuvent être créées en spécifiant les plages de clés de partitions et de lignes, de sorte qu’un utilisateur puisse accéder aux données spécifiques à un pays particulier.| 

## <a id="rbac-azure-manager"></a>Activer le contrôle d’accès en fonction du rôle (RBAC) sur le compte de stockage Azure à l’aide d’Azure Resource Manager

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Comment sécuriser un compte de stockage en utilisant le contrôle d’accès en fonction du rôle (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **Étapes** | <p>Lorsque vous créez un compte de stockage, vous sélectionnez un modèle de déploiement Classique ou Azure Resource Manager. Le modèle classique de création de ressources dans Azure autorise seulement un accès « tout ou rien » à l’abonnement et, à tour de rôle, au compte de stockage.</p><p>Avec le modèle Azure Resource Manager, vous devez placer le compte de stockage dans un groupe de ressources et contrôler l’accès au plan de gestion de ce compte de stockage spécifique à l’aide d’Azure Active Directory. Par exemple, vous pouvez permettre à certains utilisateurs d’accéder aux clés de compte de stockage, pendant que d’autres pourront voir les informations relatives au compte de stockage, mais pas accéder aux clés de compte de stockage.</p>|

## <a id="rooting-detection"></a>Implémenter la libération implicite ou la détection du rootage

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client mobile | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>L’application doit protéger sa propre configuration et les données utilisateur au cas où le téléphone serait rooté ou libéré. Le rootage/la libération implique un accès non autorisé, ce que les utilisateurs normaux ne feront pas sur leurs téléphones. L’application doit donc disposer d’une logique de détection implicite au démarrage de l’application pour détecter si le téléphone a été rooté.</p><p>La logique de détection peut permettre d’accéder à des fichiers qui ne sont normalement accessibles qu’à l’utilisateur racine, par exemple :</p><ul><li>/system/app/Superuser.apk</li><li>/sbin/su</li><li>/system/bin/su</li><li>/system/xbin/su</li><li>/data/local/xbin/su</li><li>/data/local/bin/su</li><li>/system/sd/xbin/su</li><li>/system/bin/failsafe/su</li><li>/data/local/su</li></ul><p>Si l’application peut accéder à l’un de ces fichiers, cela signifie que l’application est exécutée en tant qu’utilisateur racine.</p>|

## <a id="weak-class-wcf"></a>Référence de classe faible dans WCF

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | <p>Le système utilise une référence de classe faible, permettant ainsi à une personne malveillante d’exécuter du code non autorisé. Le programme fait référence à une classe définie par l’utilisateur qui n’est pas identifiée de manière unique. Lorsque .NET charge cette classe identifiée de manière faible, le chargeur de type CLR recherche la classe dans les emplacements suivants, dans l’ordre indiqué :</p><ol><li>Si le type de l’assembly est connu, le chargeur recherche les emplacements de redirection du fichier de configuration, GAC, l’assembly actuel à l’aide d’informations de configuration et le répertoire de base d’application</li><li>Si l’assembly est inconnu, le chargeur recherche l’assembly actuel, mscorlib et l’emplacement renvoyé par le gestionnaire d’événements TypeResolve</li><li>Cet ordre de recherche CLR peut être modifié avec des raccordements tels que le mécanisme de transfert de type et l’événement AppDomain.TypeResolve</li></ol><p>Si une personne malveillante exploite l’ordre de recherche CLR en créant une autre classe portant le même nom et en la plaçant dans un emplacement autre que l’emplacement de chargement CLR initial, le CLR exécutera involontairement le code fourni par la personne malveillante</p>|

### <a name="example"></a>Exemple
L’élément `<behaviorExtensions/>` du fichier de configuration WCF ci-dessous indique à WCF d’ajouter une classe de comportements personnalisée à une extension WCF particulière.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
L’utilisation de noms complets (forts) identifie de manière unique un type et renforce considérablement la sécurité de votre système. Utilisez des noms d’assembly complets lors de l’inscription des types dans les fichiers machine.config et app.config.

### <a name="example"></a>Exemple
L’élément `<behaviorExtensions/>` du fichier de configuration WCF ci-dessous indique à WCF d’ajouter une classe de comportements personnalisée référencée de manière forte à une extension WCF particulière.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>WCF - Implémenter le contrôle de l’autorisation

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | <p>Ce service n’utilise pas un contrôle d’autorisation. Lorsqu’un client appelle un service WCF particulier, WCF fournit divers schémas d’autorisation qui vérifient que l’appelant est autorisé à exécuter la méthode de service sur le serveur. Si les contrôles d’autorisation ne sont pas activés pour les services WCF, un utilisateur authentifié peut obtenir une élévation des privilèges.</p>|

### <a name="example"></a>Exemple
La configuration suivante indique à WCF de ne pas vérifier le niveau d’autorisation du client lors de l’exécution du service :
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Utilisez un schéma d’autorisation de service pour vérifier que l’appelant de la méthode de service est autorisé à le faire. WCF propose deux modes et permet de définir un schéma d’autorisation personnalisé. Le mode UseWindowsGroups utilise des rôles et utilisateurs Windows, et le mode UseAspNetRoles utilise un fournisseur de rôle ASP.NET, tel que SQL Server, pour l’authentification.

### <a name="example"></a>Exemple
La configuration suivante indique à WCF de vérifier que le client fait partie du groupe Administrateurs avant d’exécuter le service Ajouter :
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Le service est ensuite déclaré comme suit :
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>Implémenter le mécanisme d’autorisation approprié dans l’API web ASP.NET

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, MVC5 |
| **Attributs**              | N/A, Fournisseur d’identité - ADFS, Fournisseur d’identité - Azure AD |
| **Informations de référence**              | [Authentification et autorisation dans l’API Web ASP.NET](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) |
| **Étapes** | <p>Des informations de rôle pour les utilisateurs d’applications peuvent être dérivées d’Azure AD ou de revendications ADFS si l’application s’appuie sur ces derniers en tant que fournisseur d’identité ou que l’application elle-même peut lui fournir. Dans tous les cas, l’implémentation d’une autorisation personnalisée doit valider les informations de rôle utilisateur.</p><p>Des informations de rôle pour les utilisateurs d’applications peuvent être dérivées d’Azure AD ou de revendications ADFS si l’application s’appuie sur ces derniers en tant que fournisseur d’identité ou que l’application elle-même peut lui fournir. Dans tous les cas, l’implémentation d’une autorisation personnalisée doit valider les informations de rôle utilisateur.</p>

### <a name="example"></a>Exemple
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
Tous les contrôleurs et toutes les méthodes d’action qui doivent être protégés doivent inclure l’attribut ci-dessus.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>Effectuer des vérifications d’autorisation dans l’appareil s’il prend en charge diverses actions nécessitant différents niveaux d’autorisation

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Appareil IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>L’appareil doit autoriser l’appelant afin de vérifier si l’appelant dispose des autorisations nécessaires pour exécuter l’action demandée. Par exemple, supposons que l’appareil est un verrouillage de porte intelligent qui peut être surveillé à partir du cloud ; il fournit en outre des fonctionnalités telles que le verrouillage à distance de la porte.</p><p>Le verrouillage de porte intelligent fournit des fonctionnalités de déverrouillage uniquement lorsqu’une personne se rapproche physiquement de la porte avec une carte. Dans ce cas, l’implémentation de la commande à distance et du contrôle doit être effectuée de manière à ce que toutes les fonctionnalités pour déverrouiller la porte ne soient pas fournies étant donné que la passerelle de cloud n’est pas autorisée à envoyer une commande de déverrouillage de la porte.</p>|

## <a id="field-permission"></a>Effectuer des vérifications d’autorisation dans la passerelle de champ si elle prend en charge diverses actions nécessitant différents niveaux d’autorisation

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de champ IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | La passerelle de champ doit autoriser l’appelant afin de vérifier si l’appelant dispose des autorisations nécessaires pour exécuter l’action demandée. Par exemple, les autorisations pour une interface/API d’utilisateur administrateur doivent être différentes de celles utilisées pour configurer une passerelle de champ par rapport aux appareils qui s’y connectent.|
