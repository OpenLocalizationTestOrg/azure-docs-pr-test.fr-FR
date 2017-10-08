---
title: "Services de domaine Azure Active Directory : caractéristiques | Microsoft Docs"
description: "Caractéristiques des services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Services de domaine Azure AD
## <a name="features"></a>Caractéristiques
Hello suivant les fonctionnalités est disponible dans les domaines des Services de domaine Active Directory de Azure gérés.

* **Expérience de déploiement simple :** vous pouvez activer les services de domaine Azure AD pour votre client Azure AD en quelques clics. Que votre client Azure AD soit un client cloud ou qu’il soit synchronisé avec votre annuaire local, votre domaine géré peut être configuré rapidement.
* **Prise en charge de la jonction de domaine :** , vous pouvez facilement les ordinateurs de jonction de domaine dans votre domaine géré est disponible dans le réseau virtuel Azure de hello. expérience de jonction de domaine Hello sur le fonctionnement des systèmes d’exploitation serveur en toute transparence par rapport à des domaines pris en charge par les Services de domaine Active Directory de Azure et les clients Windows. Vous pouvez également recourir aux outils de jonction de domaine automatisée par rapport à ces domaines.
* **Une instance de domaine par annuaire Azure AD :** vous pouvez créer un seul domaine Active Directory par annuaire Azure AD.
* **Création de domaines avec des noms personnalisés :** vous pouvez créer des domaines avec des noms personnalisés (par exemple, « contoso100.com ») à l’aide des services de domaine Azure AD. Vous pouvez utiliser des noms de domaine vérifiés ou non vérifiés. Si vous le souhaitez, vous pouvez également créer un domaine avec le suffixe de domaine intégré hello (autrement dit, ' *. onmicrosoft.com') proposé par votre annuaire Azure AD.
* **Intégrée à Azure AD :** vous n’avez besoin de tooconfigure ou gérer la réplication des Services de domaine Active Directory de tooAzure. Les comptes d’utilisateur, les appartenances aux groupes et les informations d’identification (mots de passe) issus de votre annuaire Azure AD sont automatiquement disponibles dans les services de domaine Azure AD. Nouveaux utilisateurs, groupes ou tooattributes de modifications à partir de votre client Azure AD ou votre annuaire local sont automatiquement synchronisée tooAzure AD les Services de domaine.
* **Authentification NTLM et Kerberos :** grâce à la prise en charge de l’authentification NTLM et Kerberos, vous pouvez déployer des applications qui reposent sur l’authentification intégrée de Windows.
* **Utilisation de vos informations d’identification/mots de passe d’entreprise :** les mots de passe des utilisateurs dans votre client Azure AD fonctionnent avec les services de domaine Azure AD. Les utilisateurs peuvent utiliser leurs toodomain joindre l’ordinateur à des informations d’identification d’entreprise, connectez-vous de façon interactive ou via le Bureau à distance et s’authentifier sur le domaine géré de hello.
* **Prise en charge de lecture de liaison LDAP et LDAP :** vous pouvez utiliser les applications qui reposent sur les liaisons LDAP tooauthenticate des utilisateurs dans des domaines pris en charge par les Services de domaine Active Directory de Azure. En outre, les applications qui utilisent le protocole LDAP les attributs d’utilisateur/ordinateur tooquery à partir du répertoire de hello peuvent également fonctionner auprès des Services de domaine Active Directory de Azure des opérations de lecture.
* **LDAP sécurisé (LDAPS) :** vous pouvez activer accès toohello directory via LDAP sécurisé (LDAPS). Accès LDAP sécurisé est disponible dans le réseau virtuel hello par défaut. Toutefois, vous pouvez également activer accès LDAP sécurisé sur hello internet.
* **Stratégie de groupe :** vous pouvez utiliser un seul objet GPO intégré chaque pour hello utilisateurs et ordinateurs conteneurs tooenforce respect des stratégies de sécurité requis pour les comptes d’utilisateurs et les ordinateurs joints au domaine. Vous pouvez également créer votre propre stratégie de groupe personnalisé et attribuer les unités d’organisation toocustom trop[gérer la stratégie de groupe](active-directory-ds-admin-guide-administer-group-policy.md).
* **Gérer le système DNS :** membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent gérer le système DNS pour votre domaine géré à l’aide de l’administration DNS familier des outils tels que hello le composant logiciel enfichable MMC d’Administration DNS.
* **Créer des unités d’organisation (UO) personnalisé :** membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent créer des unités d’organisation personnalisées dans le domaine géré de hello. Ces utilisateurs bénéficient de privilèges administratifs complets sur les unités organisationnelles personnalisées et peuvent donc ajouter/supprimer des comptes de service, des ordinateurs, des groupes, etc. au sein de ces unités organisationnelles personnalisées.
* **Disponible dans plusieurs régions Azure :** voir hello [des services Azure par région](https://azure.microsoft.com/regions/#services/) page tooknow hello régions Azure dans lequel les Services de domaine Active Directory de Azure est disponible.
* **Haute disponibilité :** les services de domaine Azure AD offrent une haute disponibilité pour votre domaine. Cette fonctionnalité offre la garantie que hello supérieur toofailures de temps d’activité et de résilience de service. Intégrées de contrôle d’état offre une mise à jour automatisée des échecs par la rotation des nouvelles instances tooreplace échoué instances tooprovide suite service pour votre domaine.
* **Utiliser les outils de gestion familiers :** vous pouvez utiliser les outils de gestion Active Directory Windows Server familiers tels que des domaines du tooadminister géré hello centre d’administration Active Directory ou Active Directory PowerShell.
