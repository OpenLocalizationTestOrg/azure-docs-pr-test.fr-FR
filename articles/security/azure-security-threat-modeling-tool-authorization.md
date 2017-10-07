---
title: "aaaAuthorization - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
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
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>Infrastructure de sécurité : Autorisation | Mesures de correction 
| Produit/service | Article |
| --------------- | ------- |
| **Délimitation d’approbation machine** | <ul><li>[Assurez-vous que les ACL appropriées sont toodata d’accès configuré toorestrict non autorisé sur l’appareil de hello](#acl-restricted-access)</li><li>[Vérifier que le contenu sensible d’application spécifique à l’utilisateur est stocké dans le répertoire du profil utilisateur](#sensitive-directory)</li><li>[Assurez-vous que les applications hello déployé sont exécutées avec des privilèges minimum](#deployed-privileges)</li></ul> |
| **Application web** | <ul><li>[Appliquer l’ordre d’étapes séquentiel pendant le traitement du flux de logique d’entreprise](#sequential-logic)</li><li>[Implémenter l’énumération tooprevent de mécanisme de limitation du débit](#rate-enumeration)</li><li>[Vérifier que l’autorisation appropriée est en place et que le principe de privilèges minimum est respecté](#principle-least-privilege)</li><li>[Les décisions de logique d’entreprise et d’autorisation d’accès aux ressources ne doivent pas être basées sur les paramètres de demande entrante](#logic-request-parameters)</li><li>[Vérifier que le contenu et les ressources ne sont pas énumérables ou accessibles via la navigation forcée](#enumerable-browsing)</li></ul> |
| **Base de données** | <ul><li>[Assurez-vous que les comptes les moins privilégiés sont utilisés tooconnect tooDatabase server](#privileged-server)</li><li>[Implémenter des locataires tooprevent de sécurité de niveau de lignes à partir de l’accès aux données de l’autre](#rls-tenants)</li><li>[Le rôle Administrateur système doit comporter uniquement des utilisateurs valides nécessaires](#sysadmin-users)</li></ul> |
| **Passerelle de cloud IoT** | <ul><li>[Se connecter tooCloud passerelle à l’aide de jetons de privilège minimum](#cloud-least-privileged)</li></ul> |
| **Azure Event Hub** | <ul><li>[Utiliser une clé SAP d’autorisations d’envoi seulement pour générer des jetons d’appareil](#sendonly-sas)</li><li>[N’utilisez pas de jetons d’accès qui fournissent un accès direct toohello concentrateur d’événements](#access-tokens-hub)</li><li>[Se connecter tooEvent concentrateur à l’aide des associations de sécurité clés qu’aient hello autorisations minimales nécessaires](#sas-minimum-permissions)</li></ul> |
| **Azure Document DB** | <ul><li>[Utilisez les ressources jetons tooconnect tooDocumentDB chaque fois que possible](#resource-docdb)</li></ul> |
| **Délimitation d’approbation Azure** | <ul><li>[Activer l’accès affinée gestion tooAzure abonnement à l’aide de RBAC](#grained-rbac)</li></ul> |
| **Délimitation d’approbation Service Fabric** | <ul><li>[Limiter les opérations de toocluster d’accès du client à l’aide de RBAC](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[Effectuer la modélisation de sécurité et utiliser la sécurité au niveau des champs si nécessaire](#modeling-field)</li></ul> |
| **Portail Dynamics CRM** | <ul><li>[Effectuez la modélisation de sécurité des comptes portails en n’oubliant pas ce modèle de sécurité hello pour le portail de hello diffère de rest hello de CRM](#portal-security)</li></ul> |
| **Azure Storage** | <ul><li>[Accorder une autorisation précise sur un ensemble d’entités dans Azure Table Storage](#permission-entities)</li><li>[Activer le compte de stockage tooAzure de contrôle d’accès en fonction du rôle (RBAC) à l’aide du Gestionnaire de ressources Azure](#rbac-azure-manager)</li></ul> |
| **Client mobile** | <ul><li>[Implémenter la libération implicite ou la détection du rootage](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[Référence de classe faible dans WCF](#weak-class-wcf)</li><li>[WCF - Implémenter le contrôle de l’autorisation](#wcf-authz)</li></ul> |
| **API Web** | <ul><li>[Implémenter le mécanisme d’autorisation approprié dans l’API web ASP.NET](#authz-aspnet)</li></ul> |
| **Appareil IoT** | <ul><li>[Effectuer des vérifications d’autorisation dans l’appareil de hello si elle prend en charge diverses actions qui nécessitent des différents niveaux d’autorisation](#device-permission)</li></ul> |
| **Passerelle de champ IoT** | <ul><li>[Effectuer des vérifications d’autorisation dans le champ passerelle de hello si elle prend en charge diverses actions qui nécessitent des différents niveaux d’autorisation](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>Assurez-vous que les ACL appropriées sont toodata d’accès configuré toorestrict non autorisé sur l’appareil de hello

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Assurez-vous que les ACL appropriées sont toodata d’accès configuré toorestrict non autorisé sur l’appareil de hello|

## <a id="sensitive-directory"></a>Vérifier que le contenu sensible d’application spécifique à l’utilisateur est stocké dans le répertoire du profil utilisateur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Vérifiez que le contenu sensible d’application spécifique à l’utilisateur est stocké dans le répertoire du profil utilisateur. Il s’agit de tooprevent plusieurs utilisateurs de hello de l’ordinateur d’accéder aux données de l’autre.|

## <a id="deployed-privileges"></a>Assurez-vous que les applications hello déployé sont exécutées avec des privilèges minimum

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation machine | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Assurez-vous que l’application hello déployé est exécutée avec les privilèges minimaux. |

## <a id="sequential-logic"></a>Appliquer l’ordre d’étapes séquentiel pendant le traitement du flux de logique d’entreprise

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Dans l’ordre tooverify cette étape a été exécutée par le biais par un utilisateur authentique vous le souhaitez tooenforce hello tooonly processus métier logique des flux d’applications dans l’ordre de l’étape, avec toutes les étapes en cours de traitement dans le temps humaine réalistes et ne traite pas de manière désordonnée, ignoré certaines étapes, traité comme suit à partir d’un autre utilisateur ou soumise trop rapidement les transactions.|

## <a id="rate-enumeration"></a>Implémenter l’énumération tooprevent de mécanisme de limitation du débit

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
| **Étapes** | <p>principe de Hello signifie l’octroi à un compte d’utilisateur les privilèges qui sont essentielles toothat aux utilisateurs de travailler. Par exemple, un utilisateur de sauvegarde n’a pas besoin de logiciel de tooinstall : par conséquent, utilisateur de sauvegarde hello a des applications de sauvegarde et de sauvegarde de toorun uniquement des droits. Tous les autres privilèges, comme l’installation de nouveaux logiciels, sont bloqués. Hello principe s’applique également tooa ordinateur personnel utilisateur généralement ne fonctionne pas dans un compte d’utilisateur normal, ouvre un compte privilégié, de la protection mot de passe (autrement dit, un superutilisateur) uniquement lorsque les cas de hello absolument l’exige. </p><p>Ce principe peut également être appliqué tooyour applications web. Au lieu d’uniquement selon les méthodes de l’authentification basée sur le rôle à l’aide de sessions, nous souhaitons plutôt que tooassign privilèges toousers au moyen d’un système d’authentification basée sur la base de données. Nous utilisons toujours des sessions dans l’ordre tooidentify si hello utilisateur était connecté correctement, uniquement présent au lieu d’affecter à cet utilisateur à un rôle spécifique, que nous affectons lui avec des privilèges tooverify les actions qu’il est privilégié tooperform sur le système de hello. En outre un grand pro de cette méthode est, chaque fois qu’un utilisateur a toobe affecté vos modifications seront appliquées volée hello comme hello affectation ne dépend pas session hello qui avait tooexpire tout d’abord moins de privilèges.</p>|

## <a id="logic-request-parameters"></a>Les décisions de logique d’entreprise et d’autorisation d’accès aux ressources ne doivent pas être basées sur les paramètres de demande entrante

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Chaque fois que vous êtes en train de si un utilisateur est limitée tooreview certaines données, accès hello restrictions doivent être traitées côté serveur. Hello userID doit être stockée à l’intérieur d’une variable de session sur la connexion et doit être utilisé tooretrieve de données utilisateur à partir de la base de données hello |

### <a name="example"></a>Exemple
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
Maintenant un agresseur potentiel ne peut pas altérer et modifier l’opération d’application hello étant donné que hello identificateur pour la récupération de hello, les données sont gérées côté serveur.

## <a id="enumerable-browsing"></a>Vérifier que le contenu et les ressources ne sont pas énumérables ou accessibles via la navigation forcée

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Les fichiers sensibles statique et de configuration n’a pas doivent être conservées dans hello web racine. Pour le contenu toobe non requis public, accès contrôles doivent être appliqués ou la suppression de hello contenu lui-même.</p><p>En outre, navigation forcée est généralement combiné avec toogather plus d’informations techniques en Force Brute en tentant de tooaccess URL autant que possible tooenumerate répertoires et fichiers sur un serveur. Les personnes malveillantes peuvent vérifier toutes les variantes des fichiers existants généralement. Par exemple, la recherche de fichiers de mot de passe peut englober des fichiers tels que psswd.txt, password.htm, password.dat et d’autres variations.</p><p>toomitigate cela, les fonctions de détection de force brute tentatives doit être inclus.</p>|

## <a id="privileged-server"></a>Assurez-vous que les comptes les moins privilégiés sont utilisés tooconnect tooDatabase server

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Hiérarchie des autorisations de base de données SQL](https://msdn.microsoft.com/library/ms191465), [éléments sécurisables de base de données SQL](https://msdn.microsoft.com/library/ms190401) |
| **Étapes** | Comptes les moins privilégiés doivent être utilisé tooconnect toohello base de données. Connexion de l’application doit être limitée dans la base de données hello et devez uniquement exécuter les procédures stockées sélectionnées. La connexion de l’application ne doit pas disposer d’un accès direct à la table. |

## <a id="rls-tenants"></a>Implémenter des locataires tooprevent de sécurité de niveau de lignes à partir de l’accès aux données de l’autre

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure, local |
| **Attributs**              | Version SQL - V12, Version SQL - MsSQL2016 |
| **Informations de référence**              | [SQL Server - Sécurité au niveau des lignes (RLS)](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **Étapes** | <p>La sécurité au niveau des lignes permet de clients toocontrol accès toorows dans une table de base de données en fonction des caractéristiques de hello d’utilisateur hello l’exécution d’une requête (par exemple, groupe d’appartenance ou contexte d’exécution).</p><p>Sécurité au niveau des lignes (RLS) simplifie la conception de hello et codage de sécurité dans votre application. Elle vous permet de tooimplement des restrictions sur l’accès aux lignes de données. Par exemple, s’assurer que les employés peuvent accéder uniquement aux lignes de données qui sont pertinentes tootheir service ou restreindre données tooonly hello données tootheir pertinentes du fournisseur d’accès d’un client.</p><p>logique de restriction d’accès Hello est située dans la couche de base de données hello plutôt que loin des données hello dans une autre couche application. système de base de données Hello applique des restrictions d’accès de hello chaque fois que cet accès aux données est tenté à partir de n’importe quel niveau. Cela permet de système de sécurité hello plus fiable et plus robuste en réduisant la surface d’exposition de hello hello du système de sécurité.</p><p>|

Notez que les lignes qu’une fonctionnalité de base de données out of box sont tooSQL uniquement applicable Server à partir de 2016 et base de données SQL Azure. Si la fonctionnalité de hello out of box RLS n’est pas implémentée, il doit s’assurer que l’accès aux données est limitée à l’aide de vues et procédures

## <a id="sysadmin-users"></a>Le rôle Administrateur système doit comporter uniquement des utilisateurs valides nécessaires

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Hiérarchie des autorisations de base de données SQL](https://msdn.microsoft.com/library/ms191465), [éléments sécurisables de base de données SQL](https://msdn.microsoft.com/library/ms190401) |
| **Étapes** | Les membres du rôle serveur fixé SysAdmin de hello doivent être très limitée et ne contiennent jamais de comptes utilisés par les applications.  Vérifiez la liste de hello des utilisateurs dans le rôle de hello et supprimer les comptes inutiles|

## <a id="cloud-least-privileged"></a>Se connecter tooCloud passerelle à l’aide de jetons de privilège minimum

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Choix de passerelle - Azure IoT Hub |
| **Informations de référence**              | [Contrôle d’accès IOT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **Étapes** | Fournissent des privilèges minimum composants toovarious autorisations qui se connectent tooCloud passerelle (IoT Hub). Un exemple typique est le composant de gestion des appareils/d’approvisionnement qui utilise registryread/write et Event Processor (ASA) qui utilise Service Connect. Les appareils individuels se connectent à l’aide d’informations d’identification d’appareil|

## <a id="sendonly-sas"></a>Utiliser une clé SAP d’autorisations d’envoi seulement pour générer des jetons d’appareil

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Event Hub | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du modèle de sécurité et de l’authentification Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Étapes** | Une clé SAS est utilisé toogenerate de jetons de chaque périphérique. Utiliser une clé SAS d’autorisations envoi uniquement lors de la génération jeton du périphérique hello pour un serveur de publication donné|

## <a id="access-tokens-hub"></a>N’utilisez pas de jetons d’accès qui fournissent un accès direct toohello concentrateur d’événements

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Event Hub | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du modèle de sécurité et de l’authentification Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Étapes** | Un jeton qui accorde le concentrateur d’événements toohello un accès direct ne convient pas toohello appareil. À l’aide d’un jeton moins privilégié pour appareil hello offrant un accès tooa uniquement le serveur de publication peut vous aider à identifier et il blocage si trouvé toobe non fiable ou compromis d’appareil.|

## <a id="sas-minimum-permissions"></a>Se connecter tooEvent concentrateur à l’aide des associations de sécurité clés qu’aient hello autorisations minimales nécessaires

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Event Hub | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Présentation du modèle de sécurité et de l’authentification Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Étapes** | Fournissent des privilèges minimum les applications principales autorisations toovarious qui se connectent toohello concentrateur d’événements. Générer des clés SAP distincts pour chaque application back-end et fournir uniquement des autorisations de hello requis - toothem envoi, réception ou gérer.|

## <a id="resource-docdb"></a>Utilisez les ressources jetons tooconnect tooCosmos base de données chaque fois que possible

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Document DB | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Un jeton de ressource est associé à une ressource d’autorisation DocumentDB et captures hello relation entre utilisateur hello d’une autorisation de base de données et hello dont dispose cet utilisateur pour une ressource d’application DocumentDB spécifique (par exemple, la collection, le document). Utilisez toujours un Bonjour tooaccess de jeton de ressource DocumentDB si le client de hello ne peut pas être fiable avec la gestion des clés de master ou en lecture seule - comme une application de l’utilisateur final comme un client mobile ou de bureau. Utiliser la clé principale ou des clés en lecture seule à partir d’applications principales qui peuvent stocker ces clés en toute sécurité.|

## <a id="grained-rbac"></a>Activer l’accès affinée gestion tooAzure abonnement à l’aide de RBAC

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Azure | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **Étapes** | Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour Azure. À l’aide de RBAC, vous pouvez accorder uniquement les quantité hello d’accès que les utilisateurs doivent tooperform leur travail.|

## <a id="cluster-rbac"></a>Limiter les opérations de toocluster d’accès du client à l’aide de RBAC

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Délimitation d’approbation Service Fabric | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | Environnement - Azure |
| **Informations de référence**              | [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **Étapes** | <p>Azure Service Fabric prend en charge deux types de contrôle d’accès différents pour les clients qui sont connectés tooa Service Fabric clusters : administrateur et utilisateur. Contrôle d’accès permet de cluster administrateur toolimit toocertain cluster opérations d’accès pour différents groupes d’utilisateurs, la sécurisation de cluster de hello hello.</p><p>Les administrateurs disposent de fonctionnalités de toomanagement d’un accès complet (y compris les fonctionnalités en lecture/écriture). Les utilisateurs, par défaut, ont uniquement un accès en lecture toomanagement fonctionnalités (par exemple, les fonctions de requête), hello capacité tooresolve applications et services.</p><p>Vous spécifiez les rôles de client hello deux (administrateur et client) lors de la création du cluster hello en fournissant des certificats pour chacun.</p>|

## <a id="modeling-field"></a>Effectuer la modélisation de sécurité et utiliser la sécurité au niveau des champs si nécessaire

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Effectuer la modélisation de sécurité et utiliser la sécurité au niveau des champs si nécessaire|

## <a id="portal-security"></a>Effectuez la modélisation de sécurité des comptes portails en n’oubliant pas ce modèle de sécurité hello pour le portail de hello diffère de rest hello de CRM

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Portail Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Effectuez la modélisation de sécurité des comptes portails en n’oubliant pas ce modèle de sécurité hello pour le portail de hello diffère de rest hello de CRM|

## <a id="permission-entities"></a>Accorder une autorisation précise sur un ensemble d’entités dans Azure Table Storage

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | StorageType - Table |
| **Informations de référence**              | [Comment toodelegate aux tooobjects dans votre compte de stockage Azure à l’aide de SAP](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **Étapes** | Dans certains scénarios d’entreprise, le stockage Azure Table peut être requis toostore des données sensibles qui gère la toodifferent parties. Par exemple, les données sensibles se rapportant toodifferent pays. Dans ce cas, les signatures de SAP peuvent être construits en spécifiant hello partition et ligne plages de clés, telles qu’un utilisateur peut accéder à des pays particulier tooa spécifique de données.| 

## <a id="rbac-azure-manager"></a>Activer le compte de stockage tooAzure de contrôle d’accès en fonction du rôle (RBAC) à l’aide du Gestionnaire de ressources Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Comment toosecure votre compte de stockage avec le contrôle d’accès en fonction du rôle (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **Étapes** | <p>Lorsque vous créez un compte de stockage, vous sélectionnez un modèle de déploiement Classique ou Azure Resource Manager. modèle classique de Hello de création de ressources dans Azure permet uniquement d’abonnement de toohello accès tout ou rien et à son tour, hello compte de stockage.</p><p>Avec le modèle de gestionnaire de ressources Azure hello, vous placez le compte de stockage hello dans une ressource groupe et contrôle d’accès toohello Gestion plan de ce compte de stockage spécifique à l’aide d’Azure Active Directory. Vous pouvez par exemple, donner à des utilisateurs spécifiques hello capacité tooaccess hello clés compte de stockage, tandis que d’autres utilisateurs peuvent afficher les informations de compte de stockage hello, mais ne peut pas accéder aux clés de compte de stockage hello.</p>|

## <a id="rooting-detection"></a>Implémenter la libération implicite ou la détection du rootage

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Client mobile | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>L’application doit protéger sa propre configuration et les données utilisateur au cas où le téléphone serait rooté ou libéré. Le rootage/la libération implique un accès non autorisé, ce que les utilisateurs normaux ne feront pas sur leurs téléphones. Application doit-elle donc logique de détection implicite au démarrage de l’application, toodetect si le téléphone de hello a été associé à une racine.</p><p>logique de détection Hello peut être simplement l’accès aux fichiers utilisateur racine normalement uniquement accessible, par exemple :</p><ul><li>/system/app/Superuser.apk</li><li>/sbin/su</li><li>/system/bin/su</li><li>/system/xbin/su</li><li>/data/local/xbin/su</li><li>/data/local/bin/su</li><li>/system/sd/xbin/su</li><li>/system/bin/failsafe/su</li><li>/data/local/su</li></ul><p>Si l’application hello peut accéder à ces fichiers, cela signifie que l’application hello s’exécute en tant qu’utilisateur racine.</p>|

## <a id="weak-class-wcf"></a>Référence de classe faible dans WCF

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | <p>système de Hello utilise une référence de classe faible, ce qui peut permettre à un attaquant de code de tooexecute non autorisé. programme de Hello fait référence à une classe définie par l’utilisateur qui n’est pas identifiée de manière unique. Lorsque .NET charge cette classe faiblement identifiée, recherche hello CLR type chargeur classe hello Bonjour emplacements Bonjour suivants spécifié ordre :</p><ol><li>Si l’assembly hello du type de hello est connu, hello chargeur recherche hello de redirection emplacements, GAC, hello assembly actuel du fichier de configuration à l’aide des informations de configuration et hello du répertoire de base d’application</li><li>Si l’assembly hello est inconnu, hello chargeur recherche hello assembly actuel, mscorlib et l’emplacement de hello retourné par le Gestionnaire d’événements TypeResolve hello</li><li>Cet ordre de recherche CLR peut être modifié avec les raccordements tels que hello mécanisme de transfert de Type et événement AppDomain.TypeResolve de hello</li></ol><p>Si un utilisateur malveillant exploite l’ordre de recherche CLR hello en créant une autre classe avec hello le même nom et le placer dans un autre emplacement que hello CLR chargera tout d’abord, hello CLR exécutera involontairement le code fourni par une personne malveillante de hello</p>|

### <a name="example"></a>Exemple
Hello `<behaviorExtensions/>` WCF tooadd une extension de WCF particulier comportement personnalisé classe tooa indique à l’élément du fichier de configuration WCF hello ci-dessous.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
L’utilisation de noms complets (forts) identifie de manière unique un type et renforce considérablement la sécurité de votre système. Utilisez des noms complets des assemblys lors de l’inscription des types dans les fichiers machine.config et app.config hello.

### <a name="example"></a>Exemple
Hello `<behaviorExtensions/>` tooadd référencé fortement personnalisés classe tooa particulier WCF extension de comportement WCF indique à l’élément du fichier de configuration WCF hello ci-dessous.
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
| **Étapes** | <p>Ce service n’utilise pas un contrôle d’autorisation. Lorsqu’un client appelle un service WCF particulier, WCF fournit différents schémas d’autorisation qui permettent de vérifier que l’appelant hello a méthode de service d’autorisation tooexecute hello sur le serveur de hello. Si les contrôles d’autorisation ne sont pas activés pour les services WCF, un utilisateur authentifié peut obtenir une élévation des privilèges.</p>|

### <a name="example"></a>Exemple
Hello configuration suivante fait en sorte que WCF toonot cocher hello d’autorisation au niveau du client de hello lors de l’exécution du service de hello :
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
Par conséquent, l’utilisation un tooverify de schéma d’autorisation service qui hello appelant de la méthode de service hello est toodo autorisé. WCF fournit deux modes et permet la hello définition d’un schéma d’autorisation personnalisé. le mode de UseWindowsGroups Hello utilise les utilisateurs et rôles Windows et le mode de UseAspNetRoles hello utilise un fournisseur de rôle ASP.NET, tels que SQL Server, tooauthenticate.

### <a name="example"></a>Exemple
Hello de configuration suivant indique toomake WCF que ce client hello fait partie du groupe d’administrateurs hello avant l’exécution du service d’ajouter hello :
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
service de Hello est déclaré comme suit de hello :
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
| **Étapes** | <p>Informations sur les rôles pour les utilisateurs de l’application hello peuvent être dérivées d’Azure AD ou fournie de revendications AD FS si l’application hello s’appuie sur ces derniers en tant que fournisseur d’identité ou l’application hello lui-même peut. Dans tous ces cas, implémentation de l’autorisation personnalisée hello doit valider les informations de rôle d’utilisateur hello.</p><p>Informations sur les rôles pour les utilisateurs de l’application hello peuvent être dérivées d’Azure AD ou fournie de revendications AD FS si l’application hello s’appuie sur ces derniers en tant que fournisseur d’identité ou l’application hello lui-même peut. Dans tous ces cas, implémentation de l’autorisation personnalisée hello doit valider les informations de rôle d’utilisateur hello.</p>

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
Tous les hello contrôleurs et méthodes d’action qui doit tooprotected doivent être décorées avec ci-dessus attribut.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>Effectuer des vérifications d’autorisation dans l’appareil de hello si elle prend en charge diverses actions qui nécessitent des différents niveaux d’autorisation

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Appareil IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Hello appareil doit autoriser hello appelant toocheck si l’appelant de hello n’a hello requis autorisations tooperform hello action demandée. Pour permet par exemple, par exemple hello périphérique est un verrou porte active qui peut être analysé à partir de cloud de hello, ainsi qu’il fournit des fonctionnalités telles que le verrouillage à distance de la porte de hello.</p><p>Hello Smart Lock porte fournit les fonctionnalités de déverrouillage uniquement quand un utilisateur est physiquement près de la porte de hello avec une carte. Dans ce cas, hello implémentation de la commande à distance hello et le contrôle doit être effectuée de manière à ce qu’il ne fournit pas une fonctionnalité toounlock hello des portes comme passerelle de cloud hello n’est pas autorisé toosend une porte de la commande toounlock hello.</p>|

## <a id="field-permission"></a>Effectuer des vérifications d’autorisation dans le champ passerelle de hello si elle prend en charge diverses actions qui nécessitent des différents niveaux d’autorisation

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de champ IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Hello passerelle de champ doit autoriser hello appelant toocheck si l’appelant de hello n’a hello requis autorisations tooperform hello action demandée. Pour, par exemple, il doit y avoir des autorisations différentes pour un utilisateur admin interface/API utilisée tooconfigure un champ v/s passerelles qui se connectent tooit.|
