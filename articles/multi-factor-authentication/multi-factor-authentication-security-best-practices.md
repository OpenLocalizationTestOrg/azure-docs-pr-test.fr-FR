---
title: "méthodes conseillées pour l’authentification Multifacteur aaaSecurity | Documents Microsoft"
description: "Ce document propose de meilleures pratiques à l’aide de l’authentification Multifacteur Azure avec des comptes Azure"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>Meilleures pratiques pour l’utilisation de l’authentification multifacteur Azure avec des comptes Azure AD

Vérification en deux étapes est hello préféré pour la plupart des organisations tooenhance leur processus d’authentification. Azure Multi-Factor Authentication (MFA) aide les entreprises à satisfaire les exigences des sociétés en matière de sécurité et de conformité tout en fournissant une expérience de connexion facile pour leurs utilisateurs. Cet article présente quelques conseils dont vous devez tenir compte lors de la planification pour l’adoption de hello de l’authentification Multifacteur Azure.

## <a name="deploy-azure-mfa-in-hello-cloud"></a>Déployer Azure MFA dans hello cloud

Il existe deux façons tooenable Azure MFA pour tous vos utilisateurs.

* Acheter des licences pour chaque utilisateur (Azure MFA, Azure AD Premium ou Enterprise Mobility + Security)
* Créer un fournisseur d’authentification multifacteur et payer par utilisateur ou par authentification

### <a name="licenses"></a>Licences
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

Si vous avez des licences Azure AD Premium ou Enterprise Mobility + Security, vous disposez déjà de l’authentification MFA. Votre organisation n’a pas besoin les utilisateurs vérification capacité tooall tooextend supplémentaire n’est pas défini hello en deux étapes. Vous ne devez tooassign un utilisateur tooa de licence, puis vous pouvez activer l’authentification Multifacteur.

Lorsque vous configurez l’authentification multifacteur, tenez compte des hello suivant conseils :

* Ne créez pas de fournisseur d’authentification multifacteur par authentification. Si vous procédez ainsi, vous êtes susceptible de payer pour des requêtes de vérification d’utilisateurs qui ont déjà des licences.
* Si vous n’avez suffisamment de licences pour tous vos utilisateurs, vous pouvez créer un reste de hello de toocover de fournisseur d’authentification multifacteur par utilisateur de votre organisation. 
* Azure AD Connect est requis uniquement si vous synchronisez votre environnement Active Directory local avec un annuaire Azure AD. Si vous utilisez un annuaire Azure AD non synchronisé avec une instance locale d’Active Directory, vous n’avez pas besoin d’Azure AD Connect.

### <a name="multi-factor-auth-provider"></a>Fournisseur d’authentification multi facteurs
![Fournisseur d’authentification multi facteurs](./media/multi-factor-authentication-security-best-practices/authprovider.png)

Si vous n’avez pas de licences qui incluent Azure MFA, vous pouvez créer un fournisseur d’authentification MFA. 

Lorsque vous créez hello fournisseur d’authentification, vous devez tooselect un répertoire et envisagez hello les détails suivants :

* Vous n’avez pas besoin d’un toocreate de répertoire Azure AD un fournisseur d’authentification multifacteur, mais que vous obtenez davantage de fonctionnalités avec une. Hello suivant les fonctionnalités est activée lorsque vous associez hello fournisseur d’authentification à un annuaire Azure AD :  
  * Étendre tooall de vérification en deux étapes à vos utilisateurs  
  * Proposer à vos administrateurs généraux des fonctionnalités supplémentaires, telles que le portail de gestion hello, messages de bienvenue personnalisés et des rapports.
* Si vous synchronisez votre environnement Active Directory local avec un annuaire Azure AD, vous avez besoin de DirSync ou d’AAD Sync. Si vous utilisez un annuaire Azure AD qui n’est pas synchronisé avec une instance locale d’Active Directory, DirSync ou AAD Sync est inutile.
* Choisissez le modèle de consommation de hello qui convient le mieux à votre entreprise. Une fois que vous sélectionnez le modèle d’utilisation de hello, vous ne pouvez pas le modifier. Hello deux modèles sont :
  * Par authentification : vous payez pour chaque vérification. Utilisez ce modèle si vous souhaitez la vérification en deux étapes pour toute personne qui accède à une certaine application, et non pour des utilisateurs spécifiques.
  * Par utilisateur activé : vous payez pour chaque utilisateur que vous activez pour Azure MFA. Utilisez ce modèle si une partie seulement des utilisateurs possède des licences Azure AD Premium Enterprise Mobility Suite.

### <a name="supportability"></a>Prise en charge
Étant donné que la plupart des utilisateurs sont habitués toousing uniquement les mots de passe tooauthenticate, il est important que votre entreprise met sensibilisation des utilisateurs de tooall concernant ce processus. Cette détection peut réduire la probabilité hello que les utilisateurs contactez le support technique pour des problèmes mineurs des tooMFA connexes. Toutefois, pour certains scénarios, il est nécessaire de désactiver provisoirement l’authentification Multifacteur. Hello utilisation suivant les instructions toounderstand comment toohandle ces scénarios :

* Formez vos scénarios de toohandle de personnel de support technique où hello utilisateur ne peut pas se connecter, car l’application mobile hello ou téléphone ne reçoit une notification ou un appel téléphonique. Le support technique peut [activer un contournement à usage unique](multi-factor-authentication-whats-next.md#one-time-bypass) tooallow un tooauthenticate utilisateur une seule fois par « contournement « vérification en deux étapes. Hello contournement est temporaire et expire après un nombre de secondes spécifié.
* Envisagez de hello [fonctionnalité d’adresses IP approuvées](multi-factor-authentication-whats-next.md#trusted-ips) dans Azure MFA comme une vérification en deux étapes de toominimize moyen. Avec cette fonctionnalité, les administrateurs d’un locataire géré ou fédéré peuvent ignorer la vérification en deux étapes pour les utilisateurs qui se connectent à partir de l’intranet local de l’entreprise hello. Hello fonctionnalités sont disponibles pour les clients Azure AD disposant de licences Azure AD Premium, Enterprise Mobility Suite ou Azure multi-Factor Authentication.

## <a name="best-practices-for-an-on-premises-deployment"></a>Meilleures pratiques pour un déploiement local
Si votre société a choisi tooleverage sa propre infrastructure de tooenable l’authentification Multifacteur, vous devez toodeploy local sur un serveur Azure multi-Factor Authentication. composants du serveur MFA Hello figurent dans hello suivant schéma :

![Composants du serveur MFA par défaut : console, moteur de synchronisation, portail de gestion, service cloud](./media/multi-factor-authentication-security-best-practices/server.png)\*Non installé par défaut \**Installé, mais non activé par défaut

Le serveur Microsoft Azure Multi-Factor Authentication peut sécuriser les ressources de cloud et les ressources locales par fédération. Vous devez disposer d’AD FS et le fédérer avec votre locataire Azure AD.
Lorsque vous configurez le serveur multi-Factor Authentication, tenez compte des hello les détails suivants :

* Si vous sécurisez les ressources Azure AD à l’aide d’Active Directory Federation Services (AD FS), puis hello première étape de vérification est effectuée en local avec AD FS. Hello deuxième étape est effectué localement en répondant à hello revendication.
* Vous n’avez pas tooinstall hello serveur Azure multi-Factor Authentication votre serveur de fédération AD FS. Toutefois, hello adaptateur de l’authentification multifacteur pour AD FS doit être installé sur un serveur Windows Server 2012 R2 AD FS en cours d’exécution. Vous pouvez installer le serveur de hello sur un autre ordinateur, tant qu’il s’agit d’une version prise en charge et installer l’adaptateur hello AD FS séparément sur votre serveur de fédération AD FS. 
* Assistant installation de l’authentification multifacteur AD FS adaptateur Hello crée un groupe de sécurité appelé PhoneFactor Admins dans Active Directory, puis ajoute le groupe de toothis de compte de service AD FS. Vérifiez que hello groupe PhoneFactor Admins a été créé sur votre contrôleur de domaine, et que ce compte de service hello AD FS est membre de ce groupe. Si nécessaire, ajoutez manuellement toohello de compte de service AD FS de hello groupe PhoneFactor Admins sur votre contrôleur de domaine.

### <a name="user-portal"></a>Portail de l'utilisateur
portail de l’utilisateur Hello permet des fonctionnalités de libre-service et fournit un ensemble complet de fonctionnalités d’administration utilisateur. Il s’exécute sur un site web IIS (Internet Information Server). Utilisez hello suivant les instructions tooconfigure ce composant :

* Utiliser IIS 6 ou version ultérieure
* Installer et inscrire ASP.NET v2.0.507207
* Veiller à ce que ce serveur puisse être déployé dans un réseau de périmètre

### <a name="app-passwords"></a>Mots de passe d'application
Si votre organisation est fédérée pour l’authentification unique avec Azure AD et que vous vous apprêtez toobe à l’aide de l’authentification Multifacteur Azure, puis prenez hello les détails suivants :

* mot de passe Hello est vérifié par Azure AD et par conséquent, contourne la fédération. La fédération n’est utilisée activement que lorsque vous configurez le mot de passe d’application.
* Pour les utilisateurs fédérés (SSO), les mots de passe sont stockés dans l’id d’organisation hello. Si l’utilisateur de hello quitte la société de hello, ces informations possède des id de tooorganizational tooflow à l’aide de DirSync. La désactivation/suppression de compte peut prendre jusqu'à toosync toothree heures, ce qui retarde la désactivation/suppression de mots de passe d’application dans Azure AD.
* Les paramètres de contrôle d'accès client locaux ne sont pas honorés par Mot de passe d’application
* Aucune authentification locale de journalisation/fonctionnalité d’audit n’est disponible pour les mots de passe d’application.
* Certaines conceptions architecturales avancées peuvent nécessiter l’utilisation d’une combinaison de noms d’utilisateur, de mots de passe et de mots de passe d’application durant l’utilisation de la vérification en deux étapes avec les clients, selon l’emplacement où ils s’authentifient. Pour les clients qui s’authentifient auprès d’une infrastructure locale, vous devez utiliser le nom d’utilisateur et le mot de passe d’une organisation. Pour les clients qui s’authentifient auprès d’Azure AD, vous devez utiliser le mot de passe hello.
* Par défaut, les utilisateurs ne peuvent pas créer des mots de passe d'application. Si vous avez besoin de mots de passe de l’application de toocreate tooallow les utilisateurs, sélectionnez hello **autoriser les utilisateurs toocreate application des mots de passe toosign dans des applications sans navigateur** option.

## <a name="additional-considerations"></a>Considérations supplémentaires
Utilisez cette liste afin de connaître certaines considérations supplémentaires et obtenir des conseils pour chaque composant qui sera déployé en local :

- Configurez Azure Multi-Factor Authentication avec les [services AD FS (Active Directory Federation Services)](multi-factor-authentication-get-started-adfs.md).
- Installer et configurer hello du serveur Azure MFA avec [l’authentification RADIUS](multi-factor-authentication-get-started-server-radius.md).
- Installer et configurer hello du serveur Azure MFA avec [l’authentification IIS](multi-factor-authentication-get-started-server-iis.md).
- Installer et configurer hello du serveur Azure MFA avec [l’authentification Windows](multi-factor-authentication-get-started-server-windows.md).
- Installer et configurer hello du serveur Azure MFA avec [l’authentification LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Installer et configurer hello du serveur Azure MFA avec [passerelle Bureau à distance et le serveur Azure multi-Factor Authentication utilisant RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- Installer et configurer la synchronisation entre hello serveur Azure MFA et [Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md).
- [Déployer hello Service Web d’application Azure multi-Factor Authentication Server Mobile](multi-factor-authentication-get-started-server-webservice.md).
- [Configuration de VPN avancée avec Azure Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) pour les équipements VPN Cisco ASA, Citrix Netscaler et Juniper/Pulse Secure à l’aide de LDAP ou RADIUS.

## <a name="next-steps"></a>Étapes suivantes
Bien que cet article mette en évidence quelques-unes des meilleures pratiques de l’authentification Multifacteur Azure, il existe d’autres ressources que vous pouvez également utiliser au moment de la planification de votre déploiement de l’authentification Multifacteur. liste Hello ci-dessous présente certains articles clés qui peuvent vous aider lors de ce processus :

* [Rapports dans Azure Multi-Factor Authentication](multi-factor-authentication-manage-reports.md)
* [expérience d’inscription de Hello en deux étapes vérification](multi-factor-authentication-end-user-first-time.md)
* [Forum Aux Questions d’Azure Multi-Factor Authentication](multi-factor-authentication-faq.md)

