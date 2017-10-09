---
title: "Des Services de domaine Active Directory Azure : Contrôleurs de domaine comparer le domaine Azure AD Services tooDIY | Documents Microsoft"
description: "Comparaison des contrôleurs de domaine Azure Active Directory Domain Services tooDIY"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>Comment toodecide si des Services de domaine Active Directory de Azure est adapté à votre cas d’usage
Avec les Services de domaine Active Directory de Azure, vous pouvez déployer vos charges de travail dans les Services d’Infrastructure Azure, sans avoir tooworry sur la gestion de l’infrastructure d’identité dans Azure. Ce service géré est différent d’un déploiement Windows Server Active Directory standard que vous déployez et gérez par vous-même. service de Hello est toodeploy facile et remet le contrôle d’intégrité automatisée et correction. Nous sommes en constante évolution hello service tooadd prise en charge des scénarios de déploiement courants.

toodecide si les Services de domaine Active Directory de Azure toouse nous vous recommandons de hello suivant documentation :

* Consultez la liste des hello [fonctionnalités proposées par les Services de domaine Active Directory de Azure](active-directory-ds-features.md).
* Consultez les [scénarios de déploiement courants pour les services de domaine Azure AD](active-directory-ds-scenarios.md).
* Enfin, [comparer l’option des Services de domaine Active Directory de Azure de tooa AD personnalisables](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Comparer domaine tooDIY AD de Services de domaine Active Directory de Azure dans Azure
Hello tableau suivant vous aide à choisir entre l’utilisation des Services de domaine Active Directory de Azure et gérez votre propre infrastructure Active Directory dans Azure.

| **Fonctionnalité** | **Services de domaine Azure AD** | **Infrastructure AD personnalisée sur des machines virtuelles Azure** |
| --- |:---:|:---:|
| [**Service géré**](active-directory-ds-comparison.md#managed-service) |**&amp;#x2713;** |**&amp;#x2715;** |
| [**Déploiements sécurisés**](active-directory-ds-comparison.md#secure-deployments) |**&amp;#x2713;** |L’administrateur doit le déploiement de hello toosecure. |
| [**Serveur DNS**](active-directory-ds-comparison.md#dns-server) |**&amp;#x2713;** (service géré) |**&amp;#x2713;** |
| [**Domain or Enterprise administrator privileges**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**Jonction de domaine**](active-directory-ds-comparison.md#domain-join) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Authentification de domaine à l’aide de NTLM et Kerberos**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Délégation Kerberos contrainte**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|basée sur la ressource|basée sur la ressource et basée sur le compte|
| [**Structure d’unité d’organisation personnalisée**](active-directory-ds-comparison.md#custom-ou-structure) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Extensions de schéma**](active-directory-ds-comparison.md#schema-extensions) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**Approbations de domaine/forêt AD**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**LDAP read**](active-directory-ds-comparison.md#ldap-read) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**LDAP sécurisé (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**LDAP write**](active-directory-ds-comparison.md#ldap-write) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**Group Policy**](active-directory-ds-comparison.md#group-policy) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Déploiements géolocalisés**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**&amp;#x2715;** |**&amp;#x2713;** |

#### <a name="managed-service"></a>Service géré
Les domaines des services de domaine Azure AD sont gérés par Microsoft. Vous n’avez pas de tooworry sur l’application de correctifs, mises à jour, la surveillance des sauvegardes et garantir la disponibilité de votre domaine. Ces tâches de gestion sont proposées en tant que service par Microsoft Azure pour vos domaines gérés.

#### <a name="secure-deployments"></a>Déploiements sécurisés
domaine géré de Hello est verrouillée en toute sécurité vers le bas conformément aux recommandations de sécurité de Microsoft pour les déploiements d’Active Directory. Ces recommandations proviennent des dizaines d’années de l’équipe de produit hello AD de l’expérience d’ingénierie et prise en charge des déploiements d’Active Directory. Pour les déploiements personnalisables, vous avez besoin d’un déploiement spécifique de tootake étapes toolock bas/votre déploiement sécurisé.

#### <a name="dns-server"></a>Serveur DNS
Un domaine géré des services de domaine Azure AD inclut des services DNS gérés. Membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent gérer DNS sur le domaine de hello géré. Membres de ce groupe reçoivent des privilèges d’Administration DNS complets pour le domaine géré de hello. Gestion du service DNS peut être effectuée à l’aide de hello 'Console d’Administration de DNS » inclus dans le package d’outils d’Administration de serveur distant (RSAT) hello.
[Plus d’informations](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>Privilèges d’administrateur de domaine ou d’entreprise
Ces privilèges élevés ne sont pas proposés sur un domaine géré AAD-DS. Les applications qui nécessitent ces privilèges élevés ne peuvent pas être déployées vers des domaines managés AAD-DS. Un plus petit sous-ensemble des privilèges d’administrateur est toomembers disponibles du groupe d’administration déléguée hello appelé « Administrateurs de contrôleur de domaine AAD ». Ces privilèges incluent des privilèges tooconfigure DNS, configurez la stratégie de groupe, obtenir des privilèges d’administrateur sur les ordinateurs joints au domaine etc..

#### <a name="domain-join"></a>jonction de domaine
Vous pouvez joindre des machines virtuelles toohello gérés toohow similaire de domaine vous joignez le domaine des ordinateurs tooan AD.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>Authentification de domaine à l’aide de NTLM et Kerberos
Avec les Services de domaine Active Directory de Azure, vous pouvez utiliser votre tooauthenticate les informations d’identification d’entreprise avec le domaine géré de hello. Les informations d’identification sont synchronisées avec votre client Azure AD. Pour les clients synchronisés, Azure AD Connect garantit que modifications toocredentials apportées localement est synchronisé tooAzure AD. Avec une configuration d’un domaine personnalisé, vous devrez peut-être tooset d’un domaine Active Directory relation d’approbation avec votre service Active Directory pour tooauthenticate utilisateurs avec leurs informations d’identification d’entreprise. Ou bien, vous devrez peut-être tooset des tooensure de réplication Active Directory que les mots de passe utilisateur synchronisent des machines virtuelles de contrôleur de domaine Azure tooyour.

#### <a name="kerberos-constrained-delegation"></a>Délégation Kerberos contrainte
Sur un domaine managé Azure AD Domain Services, vous n’avez pas les privilèges « Administrateur de domaine ». Par conséquent, vous ne pouvez pas configurer la délégation Kerberos contrainte basée sur le compte (traditionnelle). Toutefois, vous pouvez configurer hello plus sécurisée basée sur la ressource de la délégation contrainte.
[Plus d’informations](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>Structure d’unité d’organisation personnalisée
Membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent créer des unités d’organisation personnalisées hello géré domaine. Les utilisateurs qui créent des unités d’organisation personnalisées bénéficient des privilèges d’administration complets sur l’unité d’organisation de hello.
[Plus d’informations](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>Extensions de schéma
Vous ne pouvez pas étendre le schéma de base hello d’un domaine géré des Services de domaine Active Directory de Azure. Par conséquent, les applications qui reposent sur le schéma de tooAD extensions (par exemple, les nouveaux attributs sous l’objet d’utilisateur hello) ne peut pas être levées et déplacée domaines tooAAD-DS.

#### <a name="ad-domain-or-forest-trusts"></a>Approbations de domaine ou de forêt AD
Domaines gérés ne peut pas être configuré tooset des relations d’approbation (trafic entrant/sortant) avec d’autres domaines. Par conséquent, les scénarios de déploiement de forêt de ressources ne peuvent pas utiliser Azure AD Domain Services. De même, les déploiements où vous ne préférez pas toosynchronize tooAzure de mots de passe Active Directory ne peut pas utiliser les Services de domaine Active Directory de Azure.

#### <a name="ldap-read"></a>Lecture LDAP
Hello gérés domaine prend en charge LDAP lecture les charges de travail. Par conséquent, vous pouvez déployer des applications qui effectuent la lecture des opérations sur un domaine géré de hello LDAP.

#### <a name="secure-ldap"></a>LDAP sécurisé
Vous pouvez configurer les Services de domaine Active Directory de Azure tooprovide sécurisée LDAP accès tooyour géré domaine, y compris sur hello internet.
[Plus d’informations](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>Écriture LDAP
domaine géré de Hello est en lecture seule pour les objets utilisateur. Par conséquent, les applications qui effectuent des opérations d’écriture LDAP sur les attributs d’objet utilisateur de hello ne fonctionnent pas dans un domaine géré. En outre, les mots de passe utilisateur ne peut pas être changés de dans le domaine géré de hello. Un autre exemple consisterait à la modification de l’appartenance aux groupes ou des attributs de groupe dans le domaine géré hello, qui n’est pas autorisé. Toutefois, des modifications toouser attributs ou des mots de passe dans Azure AD (via le portail de PowerShell/Azure) ou Active Directory sont synchronisés en local toohello AAD-DS géré de domaine.

#### <a name="group-policy"></a>Stratégie de groupe
Il existe un objet GPO intégré chaque pour les conteneurs de « Ordinateurs AADDC » et « Utilisateurs AADDC » hello. Vous pouvez personnaliser ces stratégie de groupe GPO tooconfigure intégrés. Les membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent également créer des objets stratégie de groupe personnalisé et les lier des unités d’organisation tooexisting (y compris les unités d’organisation personnalisées).
[Plus d’informations](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>Déploiements géographiquement dispersés
Les domaines gérés des services de domaine Azure AD sont disponibles dans un seul réseau virtuel dans Azure. Pour les scénarios qui requièrent de domaine contrôleurs toobe est disponible dans plusieurs régions Azure sur Bonjour, la configuration de contrôleurs de domaine dans des machines virtuelles Azure IaaS peut être préférable de hello.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>Options de déploiement AD personnalisé
Vous avez peut-être utilisé en cas de déploiement où vous devez certaines des fonctionnalités hello offertes par une installation de Windows Server Active Directory. Dans ce cas, envisagez l’une des hello personnalisables (soi-même) options suivantes :

* **Domaine cloud autonome :** vous pouvez configurer un domaine cloud autonome à l’aide de machines virtuelles Azure qui ont été configurées en tant que contrôleurs de domaine. Cette infrastructure ne s’intègre pas à votre environnement AD local. Cette option nécessite un ensemble différent de « cloud les informations d’identification » toologin/gérer les ordinateurs virtuels dans le cloud de hello.
* **Déploiement de forêt de ressources :** vous pouvez configurer un domaine dans une topologie de forêt de ressources hello, à l’aide de machines virtuelles configurées en tant que contrôleurs de domaine. Ensuite, vous pouvez configurer une relation d’approbation AD avec votre environnement AD local. Vous pouvez la jonction de domaine (machines virtuelles Azure) d’ordinateurs toothis forêt de ressources du cloud de hello. Authentification de l’utilisateur produit sur un à un répertoire local VPN/ExpressRoute connexion tooyour.
* **Étendre votre tooAzure de domaine local :** vous pouvez vous connecter à un réseau local de tooyour de réseau virtuel Azure à l’aide d’une connexion VPN/ExpressRoute. Ce paramétrage permet de machines virtuelles Azure toobe tooyour jointes AD local. Une autre solution consiste toopromote des contrôleurs de domaine répliqués de votre domaine local dans Azure en tant qu’une machine virtuelle. Vous pouvez ensuite configurer il tooreplicate sur un répertoire local VPN/ExpressRoute connexion tooyour. Ce mode de déploiement étend efficacement votre tooAzure de domaine local.

> [!NOTE]
> Vous pouvez décider qu’une option personnalisée est mieux adaptée à vos cas d’utilisation de déploiement. Envisagez de [partage de commentaires](active-directory-ds-contact-us.md) toohelp nous comprendre les fonctionnalités peut vous aider à vous avez choisi de Services de domaine Active Directory de Azure Bonjour futures. Ces commentaires nous aident à faire évoluer à suit toobetter hello service qu'a besoin de votre déploiement et cas d’usage.
>
>

Nous avons publié [des recommandations pour le déploiement de Windows Server Active Directory sur des Machines virtuelles Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp faciliter les installations personnalisées.

## <a name="related-content"></a>Contenu connexe
* [Fonctionnalités - Services de domaine Azure AD](active-directory-ds-features.md)
* [Scénarios de déploiement - Services de domaine Azure AD](active-directory-ds-scenarios.md)
* [Instructions pour le déploiement de Windows Server Active Directory sur Azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj156090.aspx)
