---
title: aaaOverview des Services de domaine Active Directory Azure | Documents Microsoft
description: "Présentation des services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Services de domaine Azure AD
## <a name="overview"></a>Vue d'ensemble
Services d’Infrastructure Azure permettent de toodeploy une large gamme de solutions informatiques de façon flexible. Avec des Machines virtuelles Azure, vous pouvez déployer presque instantanément et vous payez uniquement par minute de hello. Grâce à la prise en charge de Windows, Linux, SQL Server, Oracle, IBM, SAP et BizTalk, vous pouvez déployer n’importe quelle charge de travail et toutes les langues sur quasiment tous les systèmes d’exploitation. Ces avantages permettent de toomigrate tooAzure de localement les applications héritées déployées, toosave sur les frais de fonctionnement.

Un aspect clé de la migration des locaux tooAzure d’applications est la gestion des besoins d’identité hello de ces applications. Applications prenant en charge l’annuaire peuvent s’appuient sur le protocole LDAP pour l’accès en lecture ou écriture toohello d’annuaire d’entreprise ou s’appuient sur les utilisateurs finaux de tooauthenticate de l’authentification intégrée Windows (authentification Kerberos ou NTLM). Les applications métier (Line-of-business, LOB) s’exécutant sous Windows Server sont généralement déployées sur les ordinateurs appartenant au domaine, et peuvent être gérées en toute sécurité grâce à la stratégie de groupe. décalage too'lift et « cloud de toohello applications sur site, ces dépendances sur l’infrastructure d’identité d’entreprise hello doivent toobe résolu.

Souvent, les administrateurs d’activer tooone Hello suivant les besoins d’identité solutions toosatisfy hello de leurs applications déployées dans Azure :

* Déployer une connexion VPN de site à site entre les charges de travail en cours d’exécution dans les Services d’Infrastructure Azure et d’annuaire d’entreprise hello en local.
* Étendre l’infrastructure de domaine/forêt hello Active Directory d’entreprise en configurant des contrôleurs de domaine répliqués à l’aide de machines virtuelles.
* le déploiement d’un domaine autonome dans Azure à l’aide de contrôleurs de domaine déployés en tant que machines virtuelles Azure.

Toutes ces approches pèchent par leur coût élevé et la surcharge administrative. Les administrateurs sont des contrôleurs de domaine toodeploy requis à l’aide de machines virtuelles dans Azure. En outre, ils ont besoin toomanage, sécurisé, patch, analyse, sauvegarde et résoudre les problèmes de ces machines virtuelles. envers les Hello toohello des connexions VPN sur site répertoire entraîne des charges de travail déployées dans les pannes ou problèmes de réseau Azure toobe tootransient vulnérable. qui réduisent les temps d’activité et affectent quelque peu la fiabilité de ces applications.

Nous avons conçu des Services de domaine Active Directory de Azure tooprovide une alternative plus simple.

## <a name="introducing-azure-ad-domain-services"></a>Présentation des services de domaine Azure AD
Les Services de domaine Active Directory Azure fournissent des services de domaine gérés tels que la jonction de domaine, la stratégie de groupe, le protocole LDAP, l’authentification Kerberos/NTLM, etc. totalement compatibles avec Windows Server Active Directory. Vous pouvez utiliser ces services de domaine sans avoir besoin de hello pour vous toodeploy, gérer et de correctif logiciel des contrôleurs de domaine dans le cloud de hello. Les Services de domaine Active Directory Azure s’intègre à votre client Azure AD existant, ce qui rend possible pour les utilisateurs toolog à l’aide de leurs informations d’identification d’entreprise. Plus, vous pouvez utiliser des groupes existants et utilisateur comptes toosecure accès tooresources, garantissant ainsi plus lisse 'finesse-et-déplacer les' tooAzure de ressources sur site des Services d’Infrastructure.

La fonctionnalité des services de domaine Azure AD fonctionne de façon transparente, que votre locataire Azure AD soit situé uniquement dans le cloud ou synchronisé avec votre annuaire Active Directory local.

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>Services de domaine Azure AD pour les entreprises exclusivement dans le cloud
Une publicité Azure uniquement dans le cloud de locataire (souvent désignée tooas ' managé locataires') n’a pas de n’importe quel empreinte d’identité locale. En d’autres termes, les comptes d’utilisateur, leurs mots de passe et les appartenances aux groupes sont tous les toohello natif cloud - c'est-à-dire, créés et gérés dans Azure AD. Imaginons un instant que Contoso est un locataire Azure AD uniquement dans le cloud. Comme indiqué dans hello après l’illustration, l’administrateur de Contoso a configuré un réseau virtuel dans les Services d’Infrastructure Azure. Les applications et les charges de travail de serveur sont déployées dans ce réseau virtuel sur des machines virtuelles Azure. Contoso étant un locataire exclusivement dans le cloud, toutes les identités des utilisateurs, leurs informations d’identification et les appartenances aux groupes sont créées et gérées dans Azure AD.

![Vue d’ensemble des services de domaine Azure AD](./media/active-directory-domain-services-overview/aadds-overview.png)

Contoso administrateur informatique peut activer les Services de domaine Active Directory de Azure pour son locataire Azure AD et choisissez toomake des services de domaine disponibles dans ce réseau virtuel. Par la suite, les Services de domaine Active Directory Azure configure un domaine géré et le rend disponible dans le réseau virtuel de hello. Tous les comptes utilisateur, les appartenances au groupe et les informations d’identification utilisateur disponibles dans le locataire Azure AD de Contoso sont également disponibles dans ce domaine nouvellement créé. Cette fonctionnalité permet aux utilisateurs de toosign d’organisation hello dans le domaine de toohello à l’aide de leurs informations d’identification - par exemple, lors de la connexion à distance toodomain-ordinateurs joints à un via le Bureau à distance. Les administrateurs peuvent configurer tooresources d’accès dans le domaine hello à l’aide des appartenances aux groupes existants. Les applications déployées sur les ordinateurs virtuels sur le réseau virtuel de hello peuvent utiliser des fonctionnalités telles que la jonction de domaine, le lecture LDAP, liaison LDAP, l’authentification NTLM et Kerberos et stratégie de groupe.

Quelques aspects marquants de hello domaine géré qui est configurée par les Services de domaine Active Directory de Azure sont les suivantes :

* Contoso administrateur informatique n’a pas besoin toomanage, patch ou analyser ce domaine ou des contrôleurs de domaine pour ce domaine géré.
* Il n’a pas besoin de réplication toomanage Active Directory pour ce domaine. Les comptes utilisateur, les appartenances aux groupes et les informations d’identification du locataire Azure AD de Contoso sont automatiquement disponibles dans ce domaine géré.
* Étant donné que le domaine de hello est géré par Azure AD Services de domaine, Contoso administrateur informatique ne dispose pas des privilèges d’administrateur de domaine ou administrateur d’entreprise sur ce domaine.

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>Services de domaine Azure AD pour les entreprises hybrides
Les entreprises dotées d’une infrastructure informatique hybride consomment à la fois des ressources de cloud et des ressources locales. Ces organisations synchronisent les informations d’identité à partir de son locataire d’Azure AD local active tootheir. Les organisations hybride regarder toomigrate plus de leur cloud toohello applications local, en particulier les applications héritées de répertoire prenant en charge, les Services de domaine Active Directory de Azure peuvent être toothem utile.

Litware Corporation a déployé [Azure AD Connect](../active-directory/active-directory-aadconnect.md), toosynchronize les informations d’identité à partir de leur locataire tootheir Azure AD du répertoire local. les informations d’identité Hello sont synchronisées incluent des comptes d’utilisateur, leurs hachages d’informations d’identification pour l’authentification (synchronisation de mot de passe) et les appartenances aux groupes.

> [!NOTE]
> **Synchronisation de mot de passe est obligatoire pour hybride organisations toouse des Services de domaine Active Directory Azure**. Cette exigence est, car les informations d’identification des utilisateurs sont nécessaires dans hello géré domaine fourni par les Services de domaine Active Directory de Azure, tooauthenticate ces utilisateurs via les méthodes d’authentification NTLM ou Kerberos.
>
>

![Services de domaine Azure AD pour Litware Corporation](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

Hello illustration ci-dessus montre comment les organisations avec une infrastructure informatique, tels que Corporation Litware hybride peuvent utiliser les Services de domaine Active Directory de Azure. Les applications et charges de travail de serveurs de Litware nécessitant des services de domaine sont déployées dans un réseau virtuel dans les services d’infrastructure Azure. Litware administrateur informatique peut activer les Services de domaine Active Directory de Azure pour son locataire Azure AD et choisissez toomake un domaine géré disponible dans ce réseau virtuel. Litware étant une organisation avec une infrastructure informatique hybride, informations d’identification, des groupes et comptes d’utilisateur sont locataire tootheir synchronisé Azure AD à partir de leur répertoire local. Cette fonctionnalité permet aux toosign d’utilisateurs dans le domaine de toohello à l’aide de leurs informations d’identification d’entreprise - par exemple, lors de la connexion à distance toomachines joints à un domaine toohello via le Bureau à distance. Les administrateurs peuvent configurer tooresources d’accès dans le domaine hello à l’aide des appartenances aux groupes existants. Les applications déployées sur les ordinateurs virtuels sur le réseau virtuel de hello peuvent utiliser des fonctionnalités telles que la jonction de domaine, le lecture LDAP, liaison LDAP, l’authentification NTLM et Kerberos et stratégie de groupe.

Quelques aspects marquants de hello domaine géré qui est configurée par les Services de domaine Active Directory de Azure sont les suivantes :

* domaine géré de Hello est un domaine autonome. et non une extension du domaine local de Litware.
* Litware administrateur informatique n’a pas besoin de toomanage, patch ou surveiller les contrôleurs de domaine pour ce domaine géré.
* Domaine n’existe pas besoin de toomanage AD réplication toothis. Comptes d’utilisateur, les appartenances aux groupes et les informations d’identification à partir de l’annuaire de Litware local sont synchronisée tooAzure AD via Azure AD Connect. Ces comptes d’utilisateur, les appartenances aux groupes et les informations d’identification sont automatiquement disponibles dans le domaine géré de hello.
* Étant donné que le domaine de hello est géré par Azure AD Services de domaine, Litware administrateur informatique ne dispose pas des privilèges d’administrateur de domaine ou administrateur d’entreprise sur ce domaine.

## <a name="benefits"></a>Avantages
Avec les Services de domaine Active Directory de Azure, vous pouvez tirer parti hello avantages suivants :

* **Simple** – vous pouvez répondre aux besoins d’identité hello d’ordinateurs virtuels déploiement des services d’Infrastructure tooAzure en quelques clics simples. Vous ne devez toodeploy et gérer l’infrastructure d’identité dans Azure ou le programme d’installation connectivité tooyour back-identité l’infrastructure locale.
* **Intégré** : les services de domaine Azure AD s’intègrent parfaitement à votre locataire Azure AD. Vous pouvez maintenant utiliser Azure AD en tant qu’un annuaire d’entreprise de nuage intégré qui gère la toohello les besoins de vos applications modernes et les applications prenant en charge Active traditionnelles.
* **Compatible** – les Services de domaine Active Directory Azure repose sur l’infrastructure de niveau entreprise ayant fait leurs preuves hello de Windows Server Active Directory. Ainsi, vos applications peuvent bénéficier d’une plus grande compatibilité avec les fonctionnalités de Windows Server Active Directory. Les fonctionnalités disponibles dans Windows Server Active Directory ne sont actuellement pas toutes disponibles pour les Services de domaine Azure AD. Toutefois, les fonctionnalités disponibles sont compatibles avec des fonctionnalités Windows Server Active Directory correspondantes hello que dépendent de votre infrastructure locale. Hello LDAP, les fonctionnalités de jointure Kerberos, NTLM, la stratégie de groupe et domaine constituent une offre mature qui a été testée et affinée de différentes versions de Windows Server.
* **Économique** – avec les Services de domaine Active Directory Azure, vous pouvez éviter la charge hello infrastructure et de gestion qui est associé à la gestion de l’identité infrastructure toosupport répertoire prenant en charge les applications traditionnelles. Vous pouvez déplacer ces tooAzure d’applications des Services d’Infrastructure et tirer parti des économies substantielles sur les frais de fonctionnement.
