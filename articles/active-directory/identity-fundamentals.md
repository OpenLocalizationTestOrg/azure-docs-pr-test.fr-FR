---
title: "aaaFundamentals de gestion des identités de Azure | Documents Microsoft"
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Principes de base de la gestion des identités Azure
Sous la forme des ressources numériques d’entreprise actives en dehors du réseau d’entreprise hello, dans le cloud de hello et sur les appareils, une grande nuage identité et accès solution de gestion devient une nécessité. Identités basées sur le cloud sont désormais meilleur contrôle de toomaintain moyen hello over et visibilité, comment et quand les utilisateurs accéder aux applications d’entreprise et des données.

Microsoft a été sécurisation des identités basée sur le cloud pour plus de dix ans et maintenant, avec [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), ces mêmes systèmes de protection sont tooyou disponible. Avec Azure AD, les administrateurs d’entreprise peuvent facilement responsabiliser les utilisateurs et les administrateurs et leur garantir une sécurité et une gouvernance sans égales.

Azure AD Premium est un nuage identité et accès solution de gestion avec les fonctionnalités de protection avancée qui permet une identité de sécurité pour toutes les applications, la protection d’identité (améliorée par hello [graphique Microsoft intelligence de la sécurité](https://www.microsoft.com/en-us/security/intelligence)) et la gestion d’identité privilégié. Pas simplement une autre analyse ou outil de création de rapports Azure AD Premium peut protéger les identités des utilisateurs en temps réel et activer des données de votre organisation vous toocreate accès basé sur les risques adaptive stratégies tooprotect.

Regardez cette vidéo pour un aperçu rapide de la protection et de la gestion des identités Azure AD :
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Microsoft fournit non seulement une identité qui accepte everywhere, mais également un ensemble d’outils tooautomate, sécuriser et gérer informatique au sein de votre organisation. Même après l’apparition de hello du cloud computing, il est toujours demander toomanage et contrôler les tâches de l’informatique comme support technique appelle tooreset des mots de passe utilisateur, utilisateur gestion des groupes et les demandes d’application. Ce qui complique les choses encore davantage, employés maintenant apportent toowork de leurs appareils personnels et à l’aide des applications SaaS rapidement disponibles. À ce titre, garder le contrôle sur leurs applications dans les centres de données de l’entreprise et sur les plateformes de cloud public représente un défi de taille.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Se connecter à Active Directory en local avec Azure AD et Office 365
Les organisations qui ont investi volumineux dans Active Directory local peuvent étendre ces cloud de toohello investissements en intégrant leurs répertoires locaux avec Azure AD dans [gestion des identités hybrides](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Ce faisant, elles augmentent la productivité des utilisateurs en leur fournissant une identité commune pour accéder aux ressources, où qu’ils se trouvent. Les utilisateurs et les organisations peuvent ensuite utiliser l’authentification unique (SSO) tooaccess les ressources locales et cloud services tels qu’Office 365.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) est hello seul outil vous avez besoin d’intégration de hello tooget terminée. Azure AD Connect fournit des fonctionnalités toosupport votre synchronisation d’identité a besoin et remplace les anciennes versions des outils d’intégration d’identité tels que DirSync et Azure AD Sync. Avec Azure AD Connect, la gestion des identités et la synchronisation entre les ressources en local et Azure AD sont possibles grâce à :

- Synchronisation : ce composant est chargé de créer des utilisateurs, des groupes et autres objets. Il est également chargé de s’assurer que les informations d’identité pour vos utilisateurs locaux et les groupes sont mise en correspondance cloud de hello. Écriture différée de mot de passe peut également être tookeep activé dans les annuaires locaux synchronisés quand un utilisateur met à jour son mot de passe dans Azure AD.
- Est une fonctionnalité facultative fournie par Azure AD Connect qui peut être utilisé tooconfigure un environnement hybride à l’aide d’un site local AD FS - infrastructure AD FS. Fédération peut être utilisée par les organisations tooaddress déploiements complexes, telles que l’authentification unique, la mise en œuvre de la stratégie d’authentification Active Directory et des cartes à puce ou des tiers l’authentification Multifacteur.
- Analyse de contrôle d’intégrité - [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) peut fournir une analyse robuste et fournir un emplacement central Bonjour Azure tooview portail cette activité.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Augmenter la productivité et réduire les coûts du support technique avec des expériences en libre-service et d’authentification unique

Les employés sont plus productifs lorsqu’ils disposent d’un seul tooremember de nom d’utilisateur et mot de passe et une expérience cohérente à partir de chaque appareil. Ils font gagner du temps quand ils peuvent réaliser libre-service des tâches telles que [la réinitialisation d’un mot de passe oublié](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) ou la demande d’accès tooan application sans attendre que l’assistance à partir du support technique hello.

Azure AD [s’étend sur site Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) dans le cloud de hello, l’activation toouse d’utilisateurs de leur compte professionnel principal pour les leurs appareils joints à un domaine, ressources d’entreprise et l’ensemble des applications SaaS et de site web de hello ils devez toouse tooget leur travail. En outre toonot ayant tooremember plusieurs ensembles de noms d’utilisateur et mots de passe, l’accès des utilisateurs à l’application peuvent également être automatiquement mis en service (ou annuler la mise en service) basé sur leurs appartenances de l’organisation et leur état en tant qu’employé. Et vous pouvez contrôler que l’accès pour les applications de la galerie, ou pour vos propres applications locales que vous avez développées et publiées par le biais hello [Proxy d’Application Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-toocorporate-resources"></a>Gérer et contrôler l’accès aux ressources de toocorporate
Identité et accès management solutions aide Microsoft IT protéger tooapplications d’accès et les ressources sur le centre de données d’entreprise hello et dans le cloud de hello, permettant ainsi des niveaux de validation supplémentaires tels que [l’authentificationmultifacteur](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) et [stratégies d’accès conditionnel](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). En surveillant les activités suspectes via les fonctions avancées de reporting, d’audit et d’alertes de sécurité, vous êtes en mesure de limiter les problèmes de sécurité potentiels.

Stratégies d’accès conditionnel dans Azure AD Premium vous permettent, hello administrateur d’entreprise, hello des règles d’accès basé sur la stratégie de capacité toocreate pour n’importe quelle application connectée AD Azure (applications SaaS, les applications personnalisées qui s’exécutent dans hello cloud ou localement des applications web). Azure AD évalue ces stratégies en temps réel et les applique chaque fois qu’un utilisateur tente de tooaccess une application. Stratégies de protection d’identité Azure permettent de prendre les mesures tooautomatically si une activité suspecte est détectée. Ces actions peuvent inclure le blocage toousers d’accès à haut risque, en appliquant l’authentification multifacteur, et mots de passe utilisateur réinitialisation s’il semble que les informations d’identification ont été compromises.


## <a name="azure-active-directory-privileged-identity-management"></a>Azure Active Directory Privileged Identity Management

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), inclus avec hello Azure Active Directory Premium P2 offre, vous permet de toodiscover, restreindre et surveiller les comptes d’administration et leurs tooresources d’accès dans votre Azure Active Directory et d’autres Services Microsoft online services. Il permet également d’administrer un accès administratif à la demande pour hello exacte période que vous avez besoin.

Privileged Identity Management peut appliquer des droits d’administrateur de la demande afin que les administrateurs puissent demander multifacteur authentifiée, temporaire une élévation de leurs privilèges de préconfiguré périodes de temps avant que leurs comptes renvoyer tooa normal état de l’utilisateur.

## <a name="benefits-of-azure-identity"></a>Avantages de la gestion des identités Azure

Avec la gestion des identités Azure, vous pouvez :

-   créer et gérer une identité unique pour chaque utilisateur de votre entreprise en préservant la synchronisation des utilisateurs, des groupes et des appareils avec [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) ;

-   Fournir des applications tooyour, y compris des milliers d’applications SaaS pré-intégrées accès avec authentification unique ou sécuriser l’accès à distance les applications SaaS tooon local à l’aide de hello [Proxy d’Application Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   sécuriser l’accès aux applications en appliquant [l’authentification multifacteur](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) basée sur des règles aussi bien aux applications en local qu’aux applications dans le cloud ;

-   Améliorer la productivité des utilisateurs avec [réinitialisation de mot de passe libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords)et le groupe et application à l’aide de hello des demandes d’accès [MyApps portal](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help).

-   Tirer parti de hello [haute disponibilité et fiabilité](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) d’une entreprise dans le monde, solution de gestion identités et des accès basée sur le cloud.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur les solutions d’identité Azure](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)