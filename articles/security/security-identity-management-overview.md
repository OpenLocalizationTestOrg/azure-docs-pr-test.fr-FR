---
title: "aaaAzure sécurité des fonctionnalités qui permettent à la gestion d’identité | Documents Microsoft"
description: " Cet article fournit une vue d’ensemble de fonctionnalités de sécurité Azure hello principales qui aide à la gestion d’identité. Identité et accès management solutions aide Microsoft IT protéger tooapplications d’accès et les ressources sur le centre de données d’entreprise hello et dans le cloud de hello, l’activation des niveaux supplémentaires de validation, telles que l’authentification multifacteur et conditionnel stratégies d’accès. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Vue d’ensemble de la sécurité et de la gestion des identités Azure
Identité et accès management solutions aide Microsoft IT protéger tooapplications d’accès et les ressources sur le centre de données d’entreprise hello et dans le cloud de hello, l’activation des niveaux supplémentaires de validation, telles que l’authentification multifacteur et conditionnel stratégies d’accès. En surveillant les activités suspectes via les fonctions avancées de reporting, d’audit et d’alertes de sécurité, vous êtes en mesure de limiter les problèmes de sécurité potentiels. [Azure Active Directory Premium](../active-directory/active-directory-editions.md) fournit toothousands d’authentification unique des applications de cloud (SaaS) et les applications de tooweb d’accès vous exécutez localement.

Avantages de sécurité d’Azure Active Directory (AD) incluent la possibilité de hello :

* Création et gestion d’une identité unique pour chaque utilisateur de l’entreprise hybride, ce qui favorise la synchronisation des utilisateurs, des groupes et des appareils
* Fournir des applications tooyour, y compris des milliers d’applications SaaS pré-intégrées accès avec authentification unique
* Activation de la sécurité d’accès aux applications en appliquant l’authentification multi-facteur basée sur des règles aussi bien pour les applications locales que pour les applications cloud
* Configurer un accès à distance sécurisé tooon local web applications via le Proxy d’Application Azure AD

Hello cet article vise tooprovide une vue d’ensemble de fonctionnalités de sécurité Azure hello principales qui aide à la gestion d’identité. Nous fournissons également des liens tooarticles qui fournissent des détails de chaque fonctionnalité afin d’en savoir plus.  

article de Hello se concentre sur hello suivant des capacités de gestion d’identité Azure :

* Authentification unique
* Proxy inversé
* Authentification multifacteur
* Surveillance de la sécurité, alertes et rapports Machine Learning
* Gestion des identités et des accès des consommateurs
* Inscription des appareils
* Privileged Identity Management
* Identity Protection
* Gestion des identités hybrides

## <a name="single-sign-on"></a>Authentification unique
L’authentification unique (SSO) signifie être en mesure de tooaccess toutes les applications de hello et les ressources que vous avez besoin de toodo entreprise, en vous connectant une seule fois à l’aide d’un compte d’utilisateur. Une fois connecté, vous pouvez accéder à toutes les applications hello vous devez sans être tooauthenticate requis (par exemple, tapez un mot de passe) une deuxième fois.

De nombreuses entreprises s’appuient sur des applications SaaS comme Office 365, Box et Salesforce pour accroître la productivité des utilisateurs finaux. Historiquement, tooindividually du personnel informatique créer et mettre à jour des comptes d’utilisateur de chaque application SaaS, et les utilisateurs devaient tooremember un mot de passe pour chaque application SaaS.

Azure AD étend localement les environnements Active Directory dans le cloud de hello, l’activation des utilisateurs toouse leur compte professionnel principal toonot uniquement de connexion tootheir les appareils joints à un domaine et des ressources d’entreprise, mais également tous les hello web et les applications SaaS nécessaire pour leur travail.

Non seulement les utilisateurs aient toomanage plusieurs ensembles de noms d’utilisateur et mots de passe, l’accès de l’application peut être automatiquement mis en service ou déprovisionnés en fonction des groupes de l’organisation et leur état en tant qu’employé. Azure AD présente la sécurité et les contrôles de gouvernance d’accès qui permettent de vous toocentrally gérer l’accès des utilisateurs entre les applications SaaS.

En savoir plus :

* [Présentation de l’authentification unique](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../active-directory/active-directory-appssoaccess-whatis.md)
* [Intégrer l’authentification unique Azure Active Directory aux applications SaaS](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>Proxy inversé
Proxy d’Application Azure AD vous permet de publier des applications locales, telles que [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) sites, [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), et [IIS](http://www.iis.net/)-en fonction des applications à l’intérieur de votre réseau privé et fournit des toousers un accès sécurisé à l’extérieur de votre réseau. Proxy d’application fournit l’accès à distance et -session unique (SSO) pour de nombreux types d’applications sur site web avec des milliers de hello d’applications SaaS Azure AD prend en charge. Employés peuvent se connecter dans les applications de tooyour d’accueil sur leurs propres appareils et de s’authentifier via ce proxy basé sur le cloud.

En savoir plus :

* [Activation du proxy d’application Azure AD](../active-directory/active-directory-application-proxy-enable.md)
* [Publier des applications avec le Proxy d’application Azure AD](../active-directory/active-directory-application-proxy-publish.md)
* [Authentification unique avec le proxy d’application](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [Utilisation de l’accès conditionnel](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Authentification multifacteur
Azure multi-Factor authentication (MFA) est une méthode d’authentification qui nécessite l’utilisation de hello de plusieurs méthodes de vérification et ajoute une seconde couche critique de sécurité toouser connexions et transactions. L’authentification Multifacteur permet toodata d’accès de sauvegarde et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Elle fournit une authentification forte par le biais de diverses options de vérification : appel téléphonique, SMS, notification par application mobile ou code de vérification et jetons OAuth tiers.

En savoir plus :

* [Authentification multifacteur](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Présentation d'Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure Multi-Factor Authentication : fonctionnement](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Surveillance de la sécurité, alertes et rapports Machine Learning
Vous pouvez protéger votre entreprise grâce à la surveillance de la sécurité, aux alertes et aux rapports Machine Learning qui identifient les comportements d’accès incohérents. Vous pouvez utiliser l’accès Azure Active Directory et l’utilisation des rapports toogain visibilité intégrité de hello et la sécurité de répertoire de votre organisation. Avec cette information, un administrateur d’annuaire peut déterminer plus précisément où peut se trouver des risques de sécurité afin qu’ils peuvent planifier en conséquence toomitigate ces risques.

Bonjour portail Azure classic, les rapports sont classés dans hello suivant façons :

* D’anomalies – ces rapports contiennent des événements que nous avons trouvé toobe anormale de connexion. Notre objectif est toomake vous prenant en charge de cette activité et vous toobe toomake en mesure de déterminer si un événement est suspect.
* Rapports d’application intégrée : fournissent des indications sur l’utilisation des applications du cloud au sein de votre société. Azure Active Directory permet d’intégrer des milliers d'applications du cloud.
* Erreur – ces rapports indiquent des erreurs qui peuvent se produire lors de la configuration des applications tooexternal de comptes.
* Rapports spécifiques à l’utilisateur : affichent les données d’activité relatives aux appareils/connexions d’un utilisateur spécifique.
* Journaux d’activité – contiennent un enregistrement de tous les événements audités dans hello des dernières 24 heures, 7 jours, ou 30 derniers jours et les modifications d’activité de groupe et activité d’inscription et de réinitialisation de mot de passe de la dernière.

En savoir plus :

* [Affichage de vos rapports d’accès et d’utilisation](../active-directory/active-directory-view-access-usage-reports.md)
* [Prise en main de la création de rapports Azure Active Directory](../active-directory/active-directory-reporting-getting-started.md)
* [Guide Azure Active Directory Reporting Guide](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>Gestion des identités et des accès des consommateurs
Azure B2C Active Directory est un service de gestion des identités hautement disponible, et globaux, pour les applications consommateur qui s’adapte toohundreds de millions d’identités. Le service peut être intégré sur l’ensemble des plateformes web et mobiles. Vos consommateurs peuvent session tooall vos applications par le biais des expériences personnalisables à l’aide de leurs comptes sociaux existants ou en créant de nouvelles informations d’identification.

Bonjour précédentes, les développeurs d’applications qui voulaient toosign haut et vous connecter aux consommateurs dans leurs applications seraient ont écrits leur propre code. Et ils aurait utilisé localement bases de données ou des systèmes toostore noms d’utilisateur et mots de passe. Azure B2C Active Directory offre une meilleur moyen toointegrate consommateur gestion des identités dans les applications à l’aide de hello de plate-forme sécurisée basée sur des normes et un grand ensemble de stratégies extensibles à votre organisation.

Lorsque vous utilisez Azure Active Directory B2C, vos consommateurs peuvent s’inscrire auprès de vos applications à l’aide de leurs comptes sociaux existants (Facebook, Google, Amazon, LinkedIn) ou en créant des informations d’identification (adresse de messagerie et mot de passe, ou nom d’utilisateur et mot de passe).

En savoir plus :

* [Qu’est-ce qu’Azure Active Directory B2C ?](https://azure.microsoft.com/services/active-directory-b2c/)
* [Azure Active Directory B2C en version préliminaire : Inscription et connexion de consommateurs à vos applications](../active-directory-b2c/active-directory-b2c-overview.md)
* [Version préliminaire d’Azure Active Directory B2C : types d’applications](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>Enregistrement de l’appareil
L’inscription de périphérique Azure AD est foundation hello pour des périphériques [accès conditionnel](../active-directory/active-directory-conditional-access-device-registration-overview.md) scénarios. Lorsqu’un appareil est inscrit, Azure Active Directory Device Registration fournit appareil hello avec une identité qui est le périphérique de hello tooauthenticate utilisé lors de la hello utilisateur se connecte. Hello authentifié dispositif et attributs hello du périphérique de hello, peuvent ensuite être des stratégies d’accès conditionnel tooenforce utilisé pour les applications qui sont hébergées dans le cloud de hello et sur site.

Lorsqu’il est associé à une solution de gestion des appareils mobiles comme Intune, les attributs d’appareil hello dans Azure Active Directory sont mis à jour avec des informations supplémentaires sur l’appareil de hello. Cela vous permet des règles d’accès conditionnel toocreate qui permettent d’accéder à partir d’appareils toomeet vos normes de conformité et de sécurité.

En savoir plus :

* [Prise en main du service Azure Active Directory Device Registration](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Azure Active Directory (AD) Privileged Identity Management vous permet de gérer, contrôler et surveiller vos identités privilégiées et tooresources d’accès dans Azure AD et d’autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.

Parfois, les utilisateurs doivent toocarry opérations nécessitant des privilèges dans les ressources Azure ou Office 365 ou d’autres applications SaaS. Cela signifie souvent que les organisations ont toogive les privilèges permanentes d’accès dans Azure AD. C’est un risque de sécurité croissant pour les ressources hébergées dans le cloud, car les entreprises ne peuvent pas suffisamment surveiller ce que ces utilisateurs font avec leurs privilèges d'administrateur. En outre, si un compte d’utilisateur disposant d’un accès privilégié est compromis, cette seule faille peut affecter sa sécurité globale sur le cloud. Azure AD Privileged Identity Management permet tooresolve ce risque.

Grâce à Azure AD Privileged Identity Management, vous pouvez :

* Identifier les utilisateurs qui ont un rôle d’administrateur dans Azure AD
* Activer à la demande « juste à temps » d’un accès administratif tooMicrosoft Online Services comme Office 365 et Intune
* Obtenir des rapports sur l'historique des accès administrateur et sur les modifications apportées aux affectations de l'administrateur
* Recevoir des alertes sur le rôle privilégié de tooa d’accès

En savoir plus :

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Rôles dans Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure AD Privileged Identity Management : Comment tooadd ou supprimer un rôle d’utilisateur](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>Identity Protection
Azure AD Identity Protection est un service de sécurité offrant une vue consolidée des événements à risque et des vulnérabilités potentielles qui affectent les identités de votre organisation. Identity Protection tire parti des fonctionnalités existantes de détection des anomalies d’Azure Active Directory (disponibles via les rapports d’activités anormales d’Azure AD) et introduit de nouveaux types d’événements à risque capables de détecter les anomalies en temps réel.

En savoir plus :

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Channel 9 : Azure AD and Identity Show: Identity Protection Preview (Émission sur Azure AD et l’identité : présentation d’Identity Protection)](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>Gestion des identités hybrides
Approche tooidentity étendues locaux Microsoft et cloud hello, création d’une identité d’utilisateur unique pour l’authentification et d’autorisation des ressources tooall, indépendamment de l’emplacement.

En savoir plus :

* [Livre blanc sur les identités hybrides](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Blog de l’équipe Active Directory](https://blogs.technet.microsoft.com/ad/)
