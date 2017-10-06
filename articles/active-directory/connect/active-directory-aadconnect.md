---
title: "Connectez Active Directory à Azure Active Directory. | Microsoft Docs"
description: "Azure AD Connect intègre vos répertoires locaux à Azure Active Directory. Cela vous permet de tooprovide une identité commune pour les applications Office 365, Azure et SaaS intégrée à Azure AD."
keywords: "Introduction tooAzure AD Connect, vue d’ensemble d’Azure AD Connect, nouveautés d’Azure AD Connect, répertoire d’installation active"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Intégrer des répertoires locaux à Azure Active Directory
Azure AD Connect intègre vos répertoires locaux à Azure Active Directory. Cela vous permet de tooprovide une identité commune pour vos utilisateurs pour les applications Office 365, Azure et SaaS intégrée à Azure AD. Cette rubrique va vous guider hello planification, déploiement et les étapes de l’opération. Il est une collection de liens toohello rubriques connexes toothis zone.

> [!IMPORTANT]
> [Azure AD Connect est hello meilleure manière tooconnect votre annuaire local avec Azure AD et Office 365. Il s’agit d’un tooAzure de tooupgrade beaucoup de temps AD Connect à partir de Windows Azure Active Directory Sync (DirSync) ou Azure AD Sync que ces outils sont déconseillées maintenant et fin de la prise en charge sur le 13 avril 2017.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Qu’est-ce qu’Azure AD Connect ?](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Pourquoi utiliser Azure AD Connect
L’intégration de vos annuaires locaux avec Azure AD améliore la productivité de vos utilisateurs en leur fournissant une identité commune pour accéder aux ressources cloud et locales. Les utilisateurs et les organisations peuvent bénéficier de suivant de hello :

* Les utilisateurs peuvent utiliser une identité unique tooaccess des applications locales et cloud services tels qu’Office 365.
* Un seul outil tooprovide une expérience de déploiement simple pour la synchronisation et connectez-vous.
* Fournit les fonctionnalités les plus récents hello pour vos scénarios. Azure AD Connect remplace les versions antérieures des outils d’intégration d’identité tels que DirSync et Azure AD Sync. Pour plus d’informations, consultez [Identité hybride : Comparaison des outils d’intégration d’annuaire](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Fonctionnement d’Azure AD Connect
Azure Active Directory Connect est constitué de trois composants principaux : les services de synchronisation hello, hello facultatif Active Directory Federation Services composant et composant d’analyse hello nommé [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Pile Azure AD Connect](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Synchronisation : ce composant est chargé de créer des utilisateurs, des groupes et autres objets. Il est également chargé de s’assurer que les informations d’identité pour vos utilisateurs locaux et les groupes sont mise en correspondance cloud de hello.
* AD FS - fédération est une partie facultative d’Azure AD Connect et peut être utilisé tooconfigure un environnement hybride à l’aide d’un site local infrastructure AD FS. Peut servir à des organisations tooaddress déploiements complexes, tels que de la jonction de domaine SSO, l’application de la stratégie d’authentification Active Directory et les cartes à puce ou 3e partie de l’authentification Multifacteur.
* Analyse de contrôle d’intégrité - Azure AD Connect Health peuvent fournir des robuste de surveillance et fournir un emplacement central Bonjour Azure tooview portail cette activité. Pour plus d’informations, voir [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Installer Azure AD Connect
Vous pouvez trouver le téléchargement hello pour Azure AD Connect sur [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771).

| Solution | Scénario |
| --- | --- |
| Avant de commencer : [Matériel et conditions préalables](active-directory-aadconnect-prerequisites.md) |<li>Étapes toocomplete avant de commencer tooinstall Azure AD Connect.</li> |
| [Paramètres Express](active-directory-aadconnect-get-started-express.md) |<li>Si vous avez une seule forêt Active Directory puis cela est hello recommandé option toouse.</li> <li>Utilisateur se connecter avec hello même mot de passe à l’aide de la synchronisation de mot de passe.</li> |
| [Paramètres personnalisés](active-directory-aadconnect-get-started-custom.md) |<li>Utilisés lorsque vous disposez de plusieurs forêts. Prise en charge de nombreuses [topologies](active-directory-aadconnect-topologies.md) locales.</li> <li>Personnalisez votre option de connexion, par exemple AD FS pour la fédération, ou utilisez un fournisseur d’identité tiers.</li> <li>Personnalisez les fonctionnalités de synchronisation, telles que le filtrage et l’écriture différée.</li> |
| [Mise à niveau à partir de DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Utilisé lorsque vous disposez d’un serveur DirSync existant déjà en cours d’exécution.</li> |
| [Mise à niveau à partir d’Azure AD Sync ou d’Azure AD Connect](active-directory-aadconnect-upgrade-previous-version.md) |<li>Il existe plusieurs méthodes différentes, en fonction de vos préférences.</li> |

[Après l’installation](active-directory-aadconnect-whats-next.md) vous devez vérifier qu’il est fonctionne comme prévu et attribuer des licences aux utilisateurs de toohello.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Étapes suivantes tooInstall Azure AD Connect
|Rubrique |Lien|  
| --- | --- |
|Téléchargez Azure AD Connect | [Téléchargez Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Installation à l’aide des paramètres Express | [Installation rapide pour Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Installation à l’aide des paramètres personnalisés | [Installation personnalisée d’Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Mise à niveau à partir de DirSync | [Effectuer une mise à niveau à partir de l’outil de synchronisation Azure AD (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Après l’installation | [Vérifier l’installation de hello et attribuer des licences](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>En savoir plus sur l’installation d’Azure AD Connect
Vous souhaitez également tooprepare pour [opérationnelle](active-directory-aadconnectsync-operations.md) problèmes. Vous souhaiterez peut-être toohave un serveur de secours afin de vous facilement pouvez tomber s’il existe un [après sinistre](active-directory-aadconnectsync-operations.md#disaster-recovery). Si vous envisagez de toomake fréquentes modifications de configuration, vous devez prévoir un [mode de préproduction](active-directory-aadconnectsync-operations.md#staging-mode) server.

|Rubrique |Lien|  
| --- | --- |
|Topologies prises en charge | [Topologies pour Azure AD Connect](active-directory-aadconnect-topologies.md)|
|Principes de conception | [Principes de conception Azure AD Connect](active-directory-aadconnect-design-concepts.md)|
|Comptes utilisés pour l’installation | [Autorisations et informations d’identification Azure AD Connect](./active-directory-aadconnect-accounts-permissions.md)|
|Planification opérationnelle | [Azure Connect AD sync : tâches et examen opérationnels](active-directory-aadconnectsync-operations.md)|
|Options de connexion utilisateur | [Options de connexion de l’utilisateur via Azure AD Connect](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Configuration de fonctionnalités de synchronisation
Azure AD Connect est doté de plusieurs fonctionnalités que vous pouvez activer ou qui sont activées par défaut. Certaines fonctionnalités peuvent parfois nécessiter une configuration supplémentaire dans des topologies et scénarios spécifiques.

[Le filtrage](active-directory-aadconnectsync-configure-filtering.md) est utilisée lorsque vous souhaitez toolimit les objets qui sont synchronisés tooAzure AD. Par défaut, tous les utilisateurs, contacts, groupes et ordinateurs Windows 10 sont synchronisés. Vous pouvez modifier hello un filtrage basé sur les domaines, les unités d’organisation ou d’attributs.

[Synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) synchronise le hachage de mot de passe hello dans Active Directory tooAzure AD. l’utilisateur final Hello peut utiliser hello même mot de passe localement et dans le cloud hello mais uniquement gérer dans un seul emplacement. Dans la mesure où il utilise votre annuaire Active Directory local en tant qu’autorité de hello, vous pouvez également utiliser votre propre stratégie de mot de passe.

[L’écriture différée de mot de passe](../active-directory-passwords-getting-started.md) autoriser votre toochange utilisateurs et réinitialiser leurs mots de passe dans le cloud de hello et avoir votre stratégie de mot de passe local appliquée.

[L’écriture différée de l’appareil](active-directory-aadconnect-feature-device-writeback.md) autorise un appareil inscrit dans Azure AD les toobe écrit tooon local Active Directory afin qu’il peut être utilisé pour l’accès conditionnel.

Hello [empêcher des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) fonctionnalité est activée par défaut et protège votre annuaire du cloud à partir de nombreuses suppressions à hello même temps. Par défaut, elle permet 500 suppressions par exécution. Vous pouvez modifier ce paramètre en fonction de la taille de votre organisation.

[Mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) est activée par défaut pour les installations de configuration rapide et permet de garantir votre Azure AD Connect est toujours opérationnel toodate avec la version la plus récente hello.

### <a name="next-steps-tooconfigure-sync-features"></a>Fonctionnalités de synchronisation suivantes étapes tooconfigure
|Rubrique |Lien|  
| --- | --- |
|Configurer le filtrage | [Azure AD Connect Sync : Configurer le filtrage](active-directory-aadconnectsync-configure-filtering.md)|
|synchronisation de mot de passe | [Azure AD Connect Sync : implémenter la synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md)|
|écriture différée du mot de passe | [Prise en main de la gestion de mot de passe](../active-directory-passwords-getting-started.md)|
|L’écriture différée d’appareils | [Activation de l’écriture différée des appareils dans Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md)|
|prévention des suppressions accidentelles | [Azure AD Connect Sync : Prévention des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|Mise à jour automatique | [Azure AD Connect : Mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Personnaliser Azure AD Connect Sync
Synchronisation Azure AD Connect est fourni avec une configuration par défaut est toowork prévue pour la plupart des clients et des topologies. Mais il existe toujours des situations où la configuration par défaut de hello ne fonctionne pas et doit être ajustée. Il est pris en charge toomake modifications documentées dans cette section et les rubriques associées.

Si vous n’avez pas travaillé avec une topologie de synchronisation avant que vous le souhaitez notions de base toostart toounderstand hello et hello termes utilisés comme décrit dans hello [concepts techniques](active-directory-aadconnectsync-technical-concepts.md). Azure AD Connect est évolution hello de MIIS 2003, ILM2007 et FIM 2010. Bien que certains éléments soient identiques, beaucoup de choses ont changé.

Hello [configuration par défaut](active-directory-aadconnectsync-understanding-default-configuration.md) suppose que la configuration de hello peut comporter plusieurs forêts. Dans ces topologies, un objet utilisateur peut être représenté comme un contact dans une autre forêt. Hello utilisateur peut également avoir une boîte aux lettres liée dans une autre forêt de ressources. comportement de Hello de configuration par défaut de hello est décrit dans [les utilisateurs et contacts](active-directory-aadconnectsync-understanding-users-and-contacts.md).

modèle de configuration Hello synchronisée est appelé [approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md). Hello flux d’attributs avancés sont à l’aide de [fonctions](active-directory-aadconnectsync-functions-reference.md) tooexpress attribut transformations. Vous pouvez afficher et examiner hello ensemble de la configuration à l’aide des outils qui est livré avec Azure AD Connect. Si vous avez besoin de modifications de configuration toomake, assurez-vous que vous suivez hello [meilleures pratiques](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) afin qu’il soit plus facile tooadopt nouvelles versions.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>Étapes de synchronisation de toocustomize Azure AD Connect
|Rubrique |Lien|  
| --- | --- |
|Tous les articles sur la synchronisation Azure AD Connect | [Synchronisation d’Azure AD Connect](active-directory-aadconnectsync-whatis.md)|
|concepts techniques | [Azure AD Connect Sync : Concepts techniques](active-directory-aadconnectsync-technical-concepts.md)|
|Présentation de la configuration par défaut hello | [Synchronisation Azure AD Connect : présentation de la configuration par défaut hello](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Présentation des utilisateurs et des contacts | [Azure AD Connect Sync : Présentation des utilisateurs et des contacts](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|Approvisionnement déclaratif | [Azure AD Connect Sync : présentation des expressions d’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Modifier la configuration par défaut hello | [Meilleures pratiques pour la modification de la configuration par défaut de hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Configuration de fonctionnalités de fédération
AD FS peut être configuré toosupport [plusieurs domaines](active-directory-aadconnect-multiple-domains.md). Par exemple, vous pouvez avoir plusieurs premiers domaines que vous avez besoin de toouse pour la fédération.

Si votre serveur AD FS n’a pas été configuré tooautomatically les certificats de mise à jour d’Azure AD ou si vous utilisez une solution non-AD FS, puis vous serez averti lorsque vous avez trop[mettre à jour des certificats](active-directory-aadconnect-o365-certs.md).

### <a name="next-steps-tooconfigure-federation-features"></a>Fonctionnalités de fédération suivantes étapes tooconfigure
|Rubrique |Lien|  
| --- | --- |
|Tous les articles AD FS | [Fédération avec Azure AD Connect](active-directory-aadconnectfed-whatis.md)|
|Configuration d’ADFS avec des sous-domaines | [Prise en charge de plusieurs domaines pour la fédération avec Azure AD](active-directory-aadconnect-multiple-domains.md)|
|Gérer la batterie AD FS | [Gestion AD FS et personnalisation avec Azure AD Connect](active-directory-aadconnect-federation-management.md)|
|Mise à jour manuelle de certificats de fédération | [Renouvellement des certificats de fédération pour Office 365 et Azure AD](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>Plus d’informations et de références
|Rubrique |Lien|  
| --- | --- |
|Historique des versions | [Historique des versions](active-directory-aadconnect-version-history.md)|
|Comparatif DirSync, Azure ADSync et Azure AD Connect | [Comparaison des outils d’intégration de répertoire](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Liste de compatibilité non-ADFS pour Azure AD | [Liste de compatibilité de fédération Azure AD](active-directory-aadconnect-federation-compatibility.md)|
|Configuration d’un IdP SAML 2.0|[Utilisation d’un fournisseur d’identité (IdP) SAML 2.0 pour l’authentification unique](active-directory-aadconnect-federation-saml-idp.md)|
|Attributs synchronisés | [Attributs synchronisés](active-directory-aadconnectsync-attributes-synchronized.md)|
|Surveillance à l’aide d’Azure AD Connect Health | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|Forum Aux Questions (FAQ) | [FAQ Azure AD Connect](active-directory-aadconnect-faq.md)|

**Ressources supplémentaires**

Ignite présentation du 2015 d’étendre votre cloud toohello de répertoires locaux.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

