---
title: "Version préliminaire des services de domaine Azure Active Directory : synchronisation sur des domaines gérés | Microsoft Docs"
description: "Synchronisation pour un domaine géré par les services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Synchronisation sur un domaine géré par les services de domaine Azure Active Directory
Hello diagramme suivant illustre comment fonctionne la synchronisation dans les Services de domaine Active Directory de Azure domaines gérés.

![Topologie de synchronisation pour les services de domaine Azure AD](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>Synchronisation du locataire tooyour Azure AD de votre répertoire local
Synchronisation Azure AD Connect est toosynchronize utilisé des comptes d’utilisateur, appartenance aux groupes et client de tooyour Azure AD de hachages d’informations d’identification. Attributs d’utilisateur comptes tels que hello UPN et le SID (identificateur de sécurité) sont synchronisés en local. Si vous utilisez les Services de domaine Active Directory de Azure, les hachages hérité d’informations d’identification requises pour l’authentification NTLM et Kerberos sont également locataire d’Azure AD tooyour synchronisés.

Si vous configurez en écriture différée, les modifications qui se produisent dans votre annuaire Azure AD sont synchronisées tooyour arrière locale Active Directory. Par exemple, si vous modifiez votre mot de passe à l’aide des fonctionnalités de modification de mot de passe libre-service d’Azure AD, mot de passe modifié hello est mise à jour dans votre site domaine Active Directory.

> [!NOTE]
> Utilisez toujours la version la plus récente hello de Azure AD Connect tooensure vous avez des correctifs pour tous les bogues.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>Synchronisation à partir de votre tooyour de locataire Azure AD gérée de domaine
Comptes d’utilisateur, les appartenances au groupe et les hachages des informations d’identification sont synchronisés à partir de votre tooyour de locataire Azure AD domaine géré des Services de domaine Active Directory de Azure. Ce processus de synchronisation est automatique. Vous n’avez pas besoin de tooconfigure, analyser ou gérer le processus de synchronisation. Après que la synchronisation initiale de hello à usage unique de votre annuaire est terminée, elle généralement prend environ 20 minutes sur les modifications effectuées dans Azure AD toobe répercutées dans votre domaine géré. Cet intervalle de synchronisation s’applique les modifications toopassword ou modifie des tooattributes effectuées dans Azure AD.

le processus de synchronisation Hello est également unique-way/unidirectionnel par nature. Votre domaine géré est en grande partie en lecture seule sauf pour les unités d’organisation personnalisées que vous créez. Par conséquent, vous ne pouvez apporter toouser modifie les attributs, les mots de passe utilisateur ou les appartenances au sein du domaine géré de hello. Par conséquent, il n’existe aucune synchronisation inverse des modifications à partir de votre client Azure AD du domaine géré précédent tooyour.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Synchronisation d’un environnement local à plusieurs forêts
De nombreuses organisations possèdent une infrastructure d’identité locale relativement complexe composée de plusieurs forêts de comptes. Azure AD Connect prend en charge la synchronisation des utilisateurs, les groupes et les hachages d’informations d’identification de client de tooyour Azure AD d’environnements à plusieurs forêts.

En revanche, votre client Azure AD est un espace de noms beaucoup plus simple et plat. applications d’accès aux tooenable utilisateurs tooreliably sécurisées par Azure AD, résolvez les conflits de nom UPN entre comptes d’utilisateurs dans des forêts différentes. Votre domaine géré des Services de domaine Active Directory de Azure par rapport ferme locataire Azure AD de tooyour ressemblance. Par conséquent, vous voyez une structure d’unité d’organisation plate dans votre domaine géré. Tous les utilisateurs et groupes sont stockées conteneur hello « AADDC utilisateurs », quel que soit le domaine local de hello ou d’une forêt à partir de laquelle ils ont été synchronisées dans. Vous pouvez avoir configuré une structure d’unité d’organisation hiérarchique en local. Toutefois, votre domaine géré a toujours une structure d’unité d’organisation plate simple.

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>Exclusions - ce qui n’est pas synchronisé domaine géré de tooyour
Hello des objets ou des attributs suivants ne sont pas locataire d’Azure AD tooyour synchronisé ou domaine géré de tooyour :

* **Exclure des attributs :** vous pouvez choisir certains attributs tooexclude à partir de la synchronisation client tooyour Azure AD de votre domaine local à l’aide d’Azure AD Connect. Ces attributs exclus ne sont pas disponibles dans votre domaine géré.
* **Stratégies de groupe :** des stratégies de groupe configurés dans votre domaine local ne sont pas synchronisés tooyour les domaine géré.
* **Partage SYSVOL :** de même, contenu hello Hello partage SYSVOL sur votre domaine local n’est pas synchronisés tooyour les domaine géré.
* **Objets ordinateur :** les objets ordinateur pour le domaine local de tooyour jointes ordinateurs ne sont pas synchronisés tooyour les domaine géré. Ces ordinateurs n’ont une relation d’approbation avec votre domaine géré et appartiennent tooyour un domaine local uniquement. Votre domaine géré, vous trouverez des objets ordinateur uniquement pour les ordinateurs que vous avez explicitement à un domaine de toohello gérés domaine.
* **Attributs de SidHistory pour les utilisateurs et groupes :** utilisateur principal de hello principal SID de groupe et de votre domaine local sont tooyour synchronisé les domaine géré. Toutefois, les attributs SidHistory existants pour les utilisateurs et les groupes ne sont pas synchronisés à partir de votre domaine local tooyour managé domaine.
* **Structures d’unités d’organisation organisation :** domaine géré de tooyour ne sont pas synchronisées sur les unités d’organisation défini dans votre domaine local. Il existe deux unités d’organisation intégrées dans votre domaine géré. Par défaut, votre domaine géré a une structure d’unité d’organisation plate. Vous pouvez toutefois choisir de trop[créer une unité d’organisation personnalisée dans votre domaine géré](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>Comment les attributs spécifiques sont synchronisés tooyour les domaine géré
Hello tableau suivant répertorie certains des attributs communs et décrit comment elles sont synchronisés tooyour les domaine géré.

| Attribut dans votre domaine géré | Source | Remarques |
|:--- |:--- |:--- |
| UPN |Attribut UPN de l’utilisateur dans votre client Azure AD |l’attribut UPN Hello à partir de votre client Azure AD est synchronisé étant tooyour géré domaine. Par conséquent, hello toosign de manière plus fiable dans le domaine géré de tooyour est à l’aide de votre UPN. |
| SAMAccountName |Attribut mailNickname de l’utilisateur, dans votre client Azure AD ou généré automatiquement |l’attribut SAMAccountName Hello en provenance d’attribut de mailNickname hello dans votre locataire Azure AD. Si plusieurs comptes d’utilisateur ont hello même attribut mailNickname, hello SAMAccountName est généré automatiquement. Si hello mailNickname ou le préfixe de nom UPN de l’utilisateur n’est plu de 20 caractères, hello SAMAccountName est généré automatiquement le toosatisfy hello 20 caractères sur les attributs SAMAccountName. |
| Mot de passe |Mot de passe utilisateur de votre client Azure AD |Les hachages d’informations d’identification requis pour l’authentification NTLM ou Kerberos (également appelés informations d’identification supplémentaires) sont synchronisés à partir de votre client Azure AD. Si votre client Azure AD est un client synchronisé, ces informations d’identification proviennent de votre domaine local. |
| SID groupe/utilisateur principal |Généré automatiquement |SID principal de Hello pour les comptes de groupe d’utilisateurs est généré automatiquement dans votre domaine géré. Cet attribut ne correspond pas à hello utilisateur/SID de groupe principal de l’objet hello dans votre site domaine Active Directory. Cette incompatibilité est, car le domaine géré de hello a un espace de noms SID différent que votre domaine local. |
| Historique des SID des utilisateurs et groupes |SID d’utilisateur et de groupe principal local |attribut de SidHistory Hello pour les utilisateurs et groupes dans votre domaine géré a la valeur toomatch hello correspondant primaire de l’utilisateur ou le SID de groupe dans votre domaine local. Cette fonctionnalité permet de rendre courbes d’élévation-et-MAJ de locaux applications toohello domaine géré plus facile, car vous n’avez pas besoin de listes ACL toore des ressources. |

> [!NOTE]
> **Connectez-vous au domaine géré de toohello à l’aide du format UPN de hello :** l’attribut SAMAccountName hello peut être générée automatiquement pour certains comptes d’utilisateurs dans votre domaine géré. Si plusieurs utilisateurs ont hello même attribut mailNickname ou utilisateurs d’avoir trop longue des préfixes de nom UPN, hello SAMAccountName pour ces utilisateurs peut-être être générées automatiquement. Par conséquent, hello SAMAccountName format (par exemple, ' CONTOSO100\joeuser') n’est pas toujours un toosign de manière fiable dans le domaine de toohello. La valeur de SAMAccountName générée automatiquement pour l’utilisateur peut différer du préfixe UPN de ce dernier. Utilisez le format UPN hello (par exemple, 'joeuser@contoso100.com') toosign dans toohello gérés domaine de manière fiable.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Mappage d’attributs pour les comptes d’utilisateur
Hello tableau suivant illustre la façon dont certains attributs pour les objets utilisateur dans votre locataire Azure AD sont des attributs synchronisés toocorresponding dans votre domaine géré.

| Attribut d’utilisateur dans votre client Azure AD | Attribut d’utilisateur dans votre domaine géré |
|:--- |:--- |
| accountEnabled |userAccountControl (Active ou désactive le hello ACCOUNT_DISABLED bit) |
| city |l |
| country |co |
| department |department |
| displayName |displayName |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| givenName |givenName |
| jobTitle |title |
| mail |mail |
| mailNickName |msDS-AzureADMailNickname |
| mailNickName |SAMAccountName (peut parfois être généré automatiquement) |
| mobile |mobile |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| passwordPolicies |userAccountControl (Active ou désactive le hello DONT_EXPIRE_PASSWORD bit) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| postalCode |postalCode |
| preferredLanguage |preferredLanguage |
| state |st |
| streetAddress |streetAddress |
| surname |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Mappage d’attributs pour les groupes
Hello tableau suivant illustre la façon dont certains attributs pour les objets de groupe dans votre locataire Azure AD sont des attributs synchronisés toocorresponding dans votre domaine géré.

| Attribut de groupe dans votre client Azure AD | Attribut de groupe dans votre domaine géré |
|:--- |:--- |
| displayName |displayName |
| displayName |SAMAccountName (peut parfois être généré automatiquement) |
| mail |mail |
| mailNickName |msDS-AzureADMailNickname |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>Les objets qui ne sont pas synchronisés locataire d’Azure AD tooyour à partir de votre domaine géré
Comme décrit dans la section précédente de cet article, il n’existe aucune synchronisation à partir de votre client Azure AD du domaine géré précédent tooyour. Vous pouvez choisir trop[créer une unité d’organisation personnalisé (OU)](active-directory-ds-admin-guide-create-ou.md) dans votre domaine géré. En outre, vous pouvez créer d’autres unités d’organisation, utilisateurs, groupes ou comptes de service au sein de ces unités d’organisation personnalisées. Aucun des objets hello créés dans des unités d’organisation personnalisées sont synchronisés locataire d’Azure AD tooyour précédent. Ces objets sont disponibles uniquement dans votre domaine géré. Par conséquent, ces objets ne sont pas visibles à l’aide des applets de commande PowerShell Azure AD, l’API Azure AD Graph ou à l’aide d’interface utilisateur de gestion hello Azure AD.

## <a name="related-content"></a>Contenu connexe
* [Fonctionnalités - Services de domaine Azure AD](active-directory-ds-features.md)
* [Scénarios de déploiement - Services de domaine Azure AD](active-directory-ds-scenarios.md)
* [Considérations relatives à la mise en réseau pour les services de domaine Azure AD](active-directory-ds-networking.md)
* [Prise en main des services de domaine Azure AD](active-directory-ds-getting-started.md)
