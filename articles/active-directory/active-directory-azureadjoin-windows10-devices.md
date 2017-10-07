---
title: appareils aaaUsing Windows 10 dans votre espace de travail | Documents Microsoft
description: "Fournit un instantané des fonctionnalités pour les utilisateurs et de l’informatique, opposant hello différentes façons un périphérique peut être configuré et utilisé dans une entreprise avec Windows 10."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Utilisation d’appareils Windows 10 sur votre lieu de travail
S’applique à : PC Windows 10

Windows 10 offre trois modèles pour les organisations qui permettent aux utilisateurs tooaccess ressources de travail de manière sécurisée et pratique.

* **Azure Active Directory Join** (Azure AD Join), pour des employés qui accèdent aux ressources telles qu’Office 365 principalement dans le cloud de hello. Azure AD Join est un nouveau service Windows 10 qui offre une expérience d’approvisionnement de ressources de travail en libre-service.
* La **jonction de domaine**, pour les organisations qui ont investi dans des applications et des ressources en local. Jonction de domaine offre une expérience améliorée dans Windows 10 connecté tooAzure AD.
* **Simplifié d’une nouvelle expérience de BYOD**, pour les utilisateurs qui souhaitent tooadd un travail de compte ou scolaire tooWindows et accéder facilement aux ressources sur les appareils personnels.

Hello tableau suivant présente une capture instantanée de fonctionnalités pour les utilisateurs et les administrateurs informatiques, opposant hello différentes façons un périphérique peut être configuré et utilisé dans une entreprise avec Windows 10 :

|  | jonction de domaine | Azure AD Join | Appareil personnel |
| --- | --- | --- | --- |
| Connexion d’appareils Windows pour les comptes professionnels ou scolaires. |Oui |Oui |Non |
| Utilisateur-authentification unique (SSO) tooOffice 365 et des applications Azure AD. L’authentification unique est toosign de capacité hello dans une seule fois tooaccess ressources de l’organisation. |Oui |Oui |Oui |
| Applications utilisateur SSO tooKerberos/NTLM. |Oui |Limité |Oui, via VPN |
| Authentification forte et connexion pratique pour les comptes professionnels ou scolaires avec Microsoft Passport et Windows Hello. |Oui |Oui |Oui |
| Accéder à tooenterprise Windows Store avec un compte professionnel ou scolaire (et non un compte Microsoft). |Oui |Oui |Oui |
| Itinérance des paramètres utilisateur compatible pour l’entreprise sur tous les appareils en utilisant un compte professionnel ou scolaire. |Oui |Oui |Oui |
| Hello capacité toorestrict accès tooorganizational applications toodevices qui sont conformes aux stratégies de l’unité d’organisation. |Oui |Oui |Oui |
| Approvisionnement d’appareils en libre-service par l’utilisateur « pour travailler n’importe où ». |Non |Oui |Oui |
| Appareils toomanage de capacité. |Oui, via la stratégie de groupe/SCCM |Oui |Oui |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Utilisation d’appareils professionnels avec Azure AD Join et la jonction de domaine dans Windows 10
Windows 10 offre des ressources de travail tooaccess travail des appareils de deux façons :

* Azure AD Join
* Jonction de domaine
  
  Ces deux options peuvent être pertinentes en fonction des besoins et exigences de l’organisation. Dans certains cas, les entreprises peuvent trouver pertinent de mettre en place ces deux méthodes de déploiement.

## <a name="when-toouse-azure-active-directory-join"></a>Quand toouse joignez Azure Active Directory
Azure AD Join est une nouvelle expérience d’approvisionnement de ressources de travail en libre-service dans Windows 10.  Il est ciblé sur les employés qui accèdent aux ressources de travail telles qu’Office 365 principalement dans le cloud de hello. Il est une solution légère de tooconfigure, tablettes, les ordinateurs et les téléphones d’entreprise de hello. Les appareils sont gérés via la gestion des périphériques mobiles (GPM), avec des contrôles homogènes entre les différentes plateformes Windows.

**Voici plusieurs raisons d’utiliser Azure AD Join**:

* Vous souhaitez tooenable hello approvisionnement en libre-service de périphériques pour des employés hello accédez.
* Vous fournissez aux utilisateurs des appareils professionnels, comme des tablettes et téléphones.
* Vous souhaitez toomanage un ensemble d’utilisateurs dans Azure AD et non dans Active Directory, telles que saisonniers, prestataires ou étudiants.
* Vous souhaitez tooprovide jointure tooworkers de fonctionnalités dans les succursales distantes avec l’infrastructure locale limitée.
* Vous ne disposez pas d’instance Active Directory en local.

Certaines organisations utilise Azure AD Join comme hello principal moyen toodeploy travail des appareils, en particulier quand elles migrer tout ou partie de leur cloud toohello de ressources. Organisations hybride avec Active Directory et Azure AD peuvent également choisir toodeploy une méthode ou à une autre selon hello utilisateur ou un service.

Les circonscriptions scolaires et les universités, par exemple, peuvent utiliser Active Directory pour la gestion du personnel et Azure AD pour la gestion des étudiants. Certaines entreprises pourriez toomanage les bureaux distants et les départements des ventes dans Azure AD. Les deux méthodes (Azure AD Join et jonction de domaine) peuvent être utilisées au sein d’une organisation hybride. Azure AD jointure peuvent être des jointures toodomain complément idéal pour le déploiement de périphériques dans un environnement de travail.

**Si hello plus accès tooenterprise ressources habituels est via le cloud de hello, votre organisation peut tirer parti des avantages supplémentaires si**:

* vous pouvez supprimer des dépendances sur une infrastructure d’identité locale ;
* vous pouvez simplifier votre modèle de déploiement d’appareils en remplaçant les solutions de création d’images par une configuration en libre-service ;
* Vous pouvez utiliser toomanage de gestion des appareils mobiles tous vos appareils sur différentes plateformes.

Pour plus d’informations sur Azure AD Join, consultez [extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="when-toouse-domain-join-or-keep-using-it"></a>Lorsque toouse joignez (ou conserver à l’aide)
Pourquoi 15 dernières années, de nombreuses organisations ont utilisées domaine jointure tooconnect travail des appareils. Il permet aux utilisateurs toosign de travail dans les appareils tootheir avec leur annuaire Active Directory ou d’établissement scolaire. Jonction de domaine permet également d’informatique toocentrally et gérer entièrement ces appareils. Les organisations reposent généralement sur les appareils tooprovision méthodes de création d’images et souvent utiliser System Center Configuration Manager (SCCM) ou la stratégie de groupe (GP) toomanage les.

**Les raisons suivantes peuvent vous encourager à utiliser (ou continuer d’utiliser) la jonction de domaine dans votre entreprise**:

* Vous avez Win32 applications déployées toothese périphériques qui utilisent NTLM/Kerberos.
* Vous avez besoin des périphériques toomanage GP ou SCCM/DCM.
* Vous souhaitez que les appareils de la tooconfigure toocontinue toouse de solutions d’acquisition d’images pour vos employés.

**Jonction de domaine dans Windows 10 vous donne également suivant de hello avantages lorsque connecté tooAzure AD**:

* authentification forte liée à l’appareil et connexion pratique pour les comptes professionnels ou scolaires avec Microsoft Passport et Windows Hello ;
* Accéder à toohello enterprise du Windows Store pour les appareils qui utilisent le travail ou d’établissement scolaire (aucun compte Microsoft requis).
* itinérance des paramètres utilisateur compatible pour l’entreprise sur tous les appareils qui utilisent un compte professionnel ou scolaire (aucun compte Microsoft requis) ;
* Hello capacité toorestrict accès tooorganizational applications toodevices qui sont conformes aux stratégies de l’unité d’organisation.

Pour plus d’informations sur Azure AD Join, consultez [extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Activation de la jonction d’appareils personnels pour un usage professionnel ou scolaire
toosupport BYOD dans enterprise hello, Windows 10 offre hello utilisateur hello capacité tooadd un travail scolaire compte tootheir ordinateur, une tablette ou téléphone. Après avoir hello utilisateur ajoute un travail ou compte scolaire, appareil de hello est inscrit auprès d’Azure AD et éventuellement inscrits dans le système de gestion de périphérique mobile hello hello organisation a configuré. répertoire de Hello sera 'Inscrit' vs ces appareils. « Joints à Azure AD ». Les administrateurs peuvent appliquer différentes stratégies en fonction de ces informations, en allégeant éventuellement les stratégies appliquées à un appareil personnel, par rapport à celles appliquées à un appareil professionnel.

Les utilisateurs peuvent ajouter un travail ou scolaire appareil personnel de compte tootheir très facilement. Il peut le faire lorsque l’accès à une application de travail pour hello première fois, ou ils peuvent le faire manuellement via le menu Paramètres de hello. Ce compte fournit l’authentification unique tooorganizational ressources.

Pour plus d’informations sur Azure AD Join, consultez [connecter tooAzure de périphériques joints au domaine Active Directory pour Windows 10 rencontre](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Activation de la jonction de domaine ou d’Azure AD Join
Toutes les méthodes décrites précédemment (jonction de domaine, Azure AD Join et ajouter compte professionnel ou scolaire) ont des points d’entrée dans l’expérience utilisateur hello Windows 10. Toutefois, l’ensemble, une fonctionnalité informatique administrateur tooenable hello dans l’infrastructure de hello avant de l’expérience de hello fonctionnera.

## <a name="requirements-for-deploying-azure-ad-join"></a>Configuration requise pour le déploiement d’Azure AD Join
toodeploy Azure AD Join pour n’importe quel ensemble d’utilisateurs, vous devez hello suivant :

* Un abonnement Azure AD
* Pour accéder à davantage de fonctionnalités, vous avez besoin d’un abonnement Azure AD Premium, par exemple l’inscription automatique au système de gestion des appareils mobiles.
* Gestion des appareils mobiles--par exemple, un abonnement Microsoft Intune, gestion des appareils mobiles pour Office 365 ou un des fournisseurs de gestion de périphérique mobile de partenaire de hello intégrant à Azure AD. (Consultez hello [section Forum aux questions](#frequently-asked-questions) près de fin hello de cet article pour plus d’informations).

Si vos sites sont hybride, il est vivement recommandé que vous déployez Azure AD Connect tooextend hello local active tooAzure Active Directory.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Configuration requise pour l’utilisation de la jonction de domaine avec Azure AD
Jonction de domaine poursuit toowork car elle a toujours. Toutefois, avantages d’Azure AD de hello tooget vous devrez hello suivant :

* Un abonnement Azure AD
* Un déploiement d’Azure AD Connect tooextend hello local active tooAzure Active Directory.
* Une stratégie qui autorise des périphériques joints au domaine toohave accès conditionnel tooAzure AD.
* Une stratégie qui autorise l’accès trop » joint au domaine » de périphériques si vous souhaitez accéder toorestrict en mesure de toobe pour certains périphériques.
* System Center Configuration Manager version 1509 pour Technical Preview, les règles tooenable obliger les appareils conformes. (Voir hello documentation TechNet et le billet de blog).

Pour plus d’informations sur la jonction de domaine dans Windows 10, consultez [connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Conditions requises pour l’utilisation du BYOD et pour « l’ajout d’un compte professionnel ou scolaire »
tooenable « apportez votre propre appareil » (BYOD) avec des comptes professionnels ou scolaires, les éléments suivants de hello sont nécessaires :

* Un abonnement Azure AD
* Pour accéder à davantage de fonctionnalités, vous avez besoin d’un abonnement Azure AD Premium, par exemple l’inscription automatique au système de gestion des appareils mobiles.

## <a name="requirements-for-using-microsoft-passport"></a>Conditions d’utilisation de Microsoft Passport
tooenable Microsoft Passport, vous devez suivant de hello :

* Une infrastructure à clés publiques (PKI) pour la prise en charge de l’authentification basée sur le certificat à l’aide de Microsoft Passport.
* Un abonnement Intune pour la prise en charge de l’authentification basée sur le certificat à l’aide de Microsoft Passport pour Azure AD Join et les comptes professionnels ou scolaires.
* System Center Configuration Manager version 1509 pour Technical Preview (voir hello documentation TechNet et le billet de blog) pour la prise en charge de l’authentification basée sur les certificats qui utilise Microsoft Passport pour la jonction de domaine.
* Une stratégie d’activation de Microsoft Passport dans l’organisation de hello.

Comme un toousing autre une infrastructure à clé publique, vous pouvez activer basée sur clé Microsoft Passport de manière hello suivante :

* Déployez des contrôleurs de domaine Windows Server 2016 « Production Preview 1 » (pas besoin de niveau fonctionnel de domaine ou forêt ; deux contrôleurs de domaine pour la redondance desservant chaque site Active Directory suffisent).
* Définir la stratégie tooenable Microsoft Passport dans l’organisation de hello.

Pour plus d’informations sur Microsoft Passport et Windows Hello dans Windows 10, consultez <lien vers le document sur MS Passport et Windows Hello>.

## <a name="frequently-asked-questions"></a>Forum Aux Questions
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Quels sont les produits de gestion de périphériques mobiles partenaires intégrés à Azure AD ?
Hello produits des fournisseurs suivants s’intègrent avec Azure AD pour l’inscription unifiée et l’accès conditionnel dans Windows 10 :

* AirWatch par VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* Gestion en local des périphériques mobiles SOTI
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Qu’en est-il de la jonction d’espace de travail dans Windows 10 ?
Jonction d’espace a été utilisée dans Windows 8.1 tooenable BYOD. Dans Windows 10, le BYOD est activé via l’ajout d’un compte professionnel ou scolaire, comme expliqué précédemment dans ce document. Pour les organisations qui ne s’intègrent leur gestion des appareils mobiles avec Azure AD, les utilisateurs peuvent inscrire des appareils de hello dans la gestion manuellement via **paramètres** > **comptes**  >  **Accès Professionnel**.

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>Les utilisateurs peuvent se connecter leur compte de domaine tootheir compte Microsoft dans Windows 10 ?
Pas dans Windows 10. Dans Windows 8.1, les utilisateurs de périphériques joints au domaine Impossible « se connecter » leur tooenable de compte de domaine Microsoft compte (par exemple, Hotmail, Live, Outlook, Xbox, etc.) tootheir certaines expériences comme SSO tooLive services, l’utilisation de hello du Windows Store et itinérance de paramètres utilisateur pour les appareils. Dans Windows 10, hello compte Microsoft « se connecter » fonctionnalité a été retirée. utilisateur de Hello pouvez ajouter un ou plusieurs comptes Microsoft en tant que services de tooconsumer des comptes supplémentaires tooenable SSO comme hello du Windows Store. Cette opération est effectuée dans **Paramètres** > **Comptes** > **Votre compte**.

Les utilisateurs qui sont la mise à niveau à partir d’appareils appartenant à un domaine de Windows 8.1, et qui était connectés son compte Microsoft, automatiquement ont leur compte connecté à Microsoft ajoutera toohello la liste des comptes supplémentaires qu’ils utilisent.

## <a name="additional-information"></a>Informations supplémentaires
* [Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

