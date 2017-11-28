---
title: aaaArticle Index pour la gestion des applications dans Azure Active Directory | Microsoft Azure
description: "Découvrez comment celle toocustomize hello pour vos certificats de fédération et utilisation des certificats toorenew qui expire sous peu."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Index d’articles pour la gestion des applications dans Azure Active Directory
Cette page fournit une liste complète de tous les documents écrits sur hello diverses fonctionnalités liées à l’application dans Azure Active Directory (Azure AD).

Il existe une zone de fonctionnalité majeure tooeach brève introduction, ainsi que des conseils sur le tooread articles selon les informations que vous recherchez.

## <a name="overview-articles"></a>Articles généraux
articles Hello ci-dessous sont de bons points de départ pour ceux qui souhaitent simplement une brève explication de fonctionnalités de gestion des applications Azure AD.

| Guide des articles |  |
|:---:| --- |
| Une introduction toohello application Gestion des problèmes qui répond à Azure AD |[Gestion des applications avec Azure Active Directory (AD)](active-directory-enable-sso-scenario.md) |
| Une vue d’ensemble de hello diverses fonctionnalités dans Azure AD liées tooenabling l’authentification unique, qui comporte tooapps, et comment les utilisateurs lancent les applications d’accès |[Accès aux applications et authentification unique dans Azure Active Directory](active-directory-appssoaccess-whatis.md) |
| Regardez hello différentes étapes lors de l’intégration des applications dans votre annuaire Azure AD |[Intégration d’applications dans Azure Active Directory](active-directory-integrating-applications-getting-started.md)<br /><br />[L’activation de l’authentification unique sur tooSaaS applications](active-directory-sso-integrate-saas-apps.md)<br /><br />[Gestion des accès tooApps](active-directory-managing-access-to-apps.md) |
| Explication technique de la représentation des applications dans Azure AD |[Comment et pourquoi les Applications sont ajoutées tooAzure AD](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>Articles de résolution des problèmes
Cette section fournit un accès rapide toorelevant des guides de dépannage. Vous trouverez plus d’informations sur chaque zone de fonctionnalité sur rest hello de cette page.

| Domaine de fonctionnalités |  |
|:---:| --- |
| Authentification unique fédérée |[Dépannage de l’authentification unique basée sur SAML](active-directory-saml-debugging.md) |
| Authentification unique par mot de passe |[Résolution des problèmes de hello Extension volet d’accès pour Internet Explorer](active-directory-saas-ie-troubleshooting.md) |
| Proxy d’application |[Guide de résolution des problèmes pour le proxy d’application](active-directory-application-proxy-troubleshoot.md) |
| Authentification unique entre AD en local et Azure AD |[Dépannage de la synchronisation du mot de passe](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[Résolution des problèmes d’écriture différée du mot de passe](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Appartenances au groupe dynamique |[Résolution des problèmes liés à l’appartenance au groupe dynamique](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>Authentification unique (SSO)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>Authentification unique fédérée : se connecter à plusieurs applications à l’aide d’une seule identité
L’authentification unique autorise tooaccess d’utilisateurs des applications et des services à l’aide de qu’un seul ensemble d’informations d’identification. La fédération est une méthode par le biais de laquelle vous pouvez activer l’authentification unique. Lorsque les utilisateurs tentent de toosign dans des applications fédérées, qu’ils obtiendront officielle-page de connexion tootheir redirigé de l’organisation restitué par Azure Active Directory et sont ensuite application toohello arrière redirigé après une authentification réussie.

| Guide des articles |  |
|:---:| --- |
| Une toofederation de présentation et d’autres types d’authentification |[Authentification unique avec Azure AD](active-directory-appssoaccess-whatis.md) |
| Des milliers d’applications SaaS pré-intégrées à Azure AD avec des étapes de configuration de l’authentification unique simplifiées |[Prise en main de la galerie d’applications Azure AD hello](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Liste complète des applications pré-intégrées qui prennent en charge la fédération](http://aka.ms/aadfederatedapps)<br /><br />[Comment votre application de tooAdd toohello Galerie d’applications Azure AD](active-directory-app-gallery-listing.md) |
| Plus de 150 didacticiels d’application sur la façon dont tooconfigure sur l’authentification unique pour les applications telles que [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [Google Apps](active-directory-saas-google-apps-tutorial.md), [Workday](active-directory-saas-workday-tutorial.md)et bien plus encore |[Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md) |
| Comment toomanually configurer et personnaliser votre configuration de l’authentification unique |[Comment tooConfigure fédéré Single Sign-On tooApps qui ne sont pas Bonjour Galerie d’applications Azure Active Directory](active-directory-saas-custom-apps.md)<br /><br />[Comment tooCustomize les revendications émises dans hello du jeton SAML pour les applications Pre-Integrated](active-directory-saml-claims-customization.md) |
| Guide de dépannage pour les applications fédérées qui utilisent le protocole SAML de hello |[Dépannage de l’authentification unique basée sur SAML](active-directory-saml-debugging.md) |
| Comment tooconfigure date d’expiration du certificat de votre application et comment toorenew vos certificats |[Gestion des certificats pour l’authentification unique fédérée sur Azure Active Directory](active-directory-sso-certs.md) |

Seule l’authentification fédérée est disponible pour toutes les éditions d’Azure AD pour les applications tooten par utilisateur. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) prend en charge un nombre illimité d’applications. Si votre organisation a [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) ou [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), vous pouvez [utilisez regroupe les applications toofederated tooassign accès](#managing-access-to-applications).

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>Authentification unique par mot de passe : partage de compte et authentification unique pour les applications non fédérées
tooenable unique authentification tooapplications qui ne prennent en charge la fédération, fonctionnalités de gestion Azure AD offre un mot de passe qui peuvent stocker en toute sécurité les applications tooSaaS les mots de passe et se connecter automatiquement les utilisateurs dans ces applications. Vous pouvez facilement distribuer des informations d’identification pour les comptes créés et partager des comptes d’équipe avec plusieurs personnes. Les utilisateurs ne doivent nécessairement tooknow hello informations d’identification toohello comptes d’accès aux donnés.

| Guide des articles |  |
|:---:| --- |
| Un fonctionnement du SSO introduction toohow basée sur mot de passe et une brève vue d’ensemble technique |[Authentification unique par mot de passe avec Azure AD](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Un résumé du partage de hello scénarios tooaccount connexe et comment ces problèmes sont résolus par Azure AD |[Partage de comptes avec Azure AD](active-directory-sharing-accounts.md) |
| Modifier automatiquement le mot de passe hello pour certaines applications à intervalles réguliers |[Substitution de mot de passe automatique (version préliminaire)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Déploiement de guides et de dépannage pour la version d’Internet Explorer hello Hello extension de gestion de mot de passe Azure AD |[Comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](active-directory-saas-ie-group-policy.md)<br /><br />[Résolution des problèmes de hello Extension volet d’accès pour Internet Explorer](active-directory-saas-ie-troubleshooting.md) |

Mot de passe de session unique est disponible pour toutes les éditions d’Azure AD pour les applications tooten par utilisateur. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) prend en charge un nombre illimité d’applications. Si votre organisation a [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) ou [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), vous pouvez [utilisez groupes tooassign accès tooapplications](#managing-access-to-applications). La substitution de mot de passe automatique est une fonctionnalité [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>Proxy d’application : Applications de tooon site seule l’authentification et accès à distance
Si vous avez des applications dans votre réseau privé qui doivent toobe accessible par les utilisateurs et appareils à l’extérieur hello réseau, vous pouvez utiliser le Proxy d’Application Azure AD tooenable accès à distance sécurisé toothose applications.

| Guide des articles |  |
|:---:| --- |
| Vue d’ensemble du proxy d’application Azure AD et présentation de son fonctionnement |[En fournissant un accès à distance sécurisé applications tooon locales](active-directory-application-proxy-get-started.md) |
| Didacticiels sur la façon de tooconfigure le Proxy d’Application et comment toopublish votre première application |[Comment tooSet des Proxy d’application Azure AD](active-directory-application-proxy-enable.md)<br /><br />[Comment installer des tooSilently hello connecteur Proxy d’application](active-directory-application-proxy-silent-installation.md)<br /><br />[Comment tooPublish Applications à l’aide du Proxy d’application](active-directory-application-proxy-publish.md)<br /><br />[Comment tooUse votre propre nom de domaine](active-directory-application-proxy-custom-domains.md) |
| Comment tooenable un seul conditionnel et de l’authentification d’accès pour les applications publiées avec le Proxy d’application |[Authentification unique avec le proxy d’application](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[Accès conditionnel et proxy d’Application](active-directory-application-proxy-conditional-access.md) |
| Des conseils sur la façon de toouse le Proxy d’Application pour les scénarios suivants de hello |[Comment tooSupport les Applications clientes natives](active-directory-application-proxy-native-client.md)<br /><br />[Comment tooSupport Applications prenant en charge les revendications](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[Comment les Applications de tooSupport publiées sur des réseaux distincts et emplacements](active-directory-application-proxy-connectors.md) |
| Guide de résolution des problèmes pour le proxy d’application |[Guide de résolution des problèmes pour le proxy d’application](active-directory-application-proxy-troubleshoot.md) |

Le Proxy d’application est disponible pour toutes les éditions d’Azure AD pour les applications tooten par utilisateur. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) prend en charge un nombre illimité d’applications. Si votre organisation a [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) ou [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), vous pouvez [utilisez groupes tooassign accès tooapplications](#managing-access-to-applications).

Vous pouvez également être intéressé [les Services de domaine Active Directory de Azure](../active-directory-domain-services/active-directory-ds-overview.md), qui vous permet de toomigrate votre tooAzure d’applications local tout en répondant toujours les identités de hello a besoin de ces applications.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Activation de l’authentification unique entre Azure AD et AD en local
Si votre organisation gère un Active Directory Windows Server local avec Azure Active Directory dans le cloud de hello, vous pouvez probablement tooenable l’authentification unique entre ces deux systèmes. Azure AD Connect (outil hello qui intègre ces deux systèmes ensemble) fournit plusieurs options pour configurer l’authentification unique : établir une fédération avec AD FS ou un autre fournisseur de fédération ou activer la synchronisation de mot de passe.

| Guide des articles |  |
|:---:| --- |
| Une vue d’ensemble sur les options d’authentification unique hello proposé dans Azure AD Connect, ainsi que des informations sur la gestion des environnements hybrides |[Options d’authentification de l’utilisateur dans Azure AD Connect](active-directory-aadconnect-user-signin.md) |
| Conseils généraux sur la gestion des environnements comportant à la fois Active Directory en local et Azure Active Directory |[Considérations relatives à la conception d'identités hybrides Azure AD](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Intégration de vos identités locales à Azure Active Directory](active-directory-aadconnect.md) |
| Aide sur l’utilisation de synchronisation de mot de passe tooenable SSO |[Implémenter la synchronisation de mot de passe avec Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Résoudre les problèmes de synchronisation de mot de passe](https://support.microsoft.com/en-us/kb/2855271) |
| Aide sur l’utilisation de l’écriture différée de mot de passe tooenable SSO |[Prise en main de la gestion de mot de passe dans Azure AD](active-directory-passwords-getting-started.md)<br /><br />[Résoudre les problèmes d’écriture différée du mot de passe](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Aide sur l’utilisation de tooenable de fournisseurs d’identité tiers SSO |[Liste des Compatible tiers identité fournisseurs que peuvent être utilisés de tooEnable Single Sign-On](https://aka.ms/ssoproviders) |
| Comment les utilisateurs de Windows 10 peuvent profiter des avantages de hello de l’authentification unique via Azure AD Join |[Extension des capacités du Cloud tooWindows 10 appareils via Azure Active Directory Join](active-directory-azureadjoin-overview.md) |

Azure AD Connect est disponible pour [toutes les éditions d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/). La réinitialisation du mot de passe libre-service Azure AD est disponible pour [Azure AD Standard](https://azure.microsoft.com/pricing/details/active-directory/) et [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Tooon local de l’écriture différée de mot de passe Active Directory est un [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) fonctionnalité.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>Accès conditionnel : appliquer des exigences de sécurité supplémentaires pour les applications à haut risque
Une fois la configuration des ressources et les applications de tooyour de l’authentification unique, vous pouvez sécuriser puis davantage les applications sensibles en appliquant des exigences de sécurité spécifiques sur chaque connexion toothat d’application. Par exemple, vous pouvez utiliser toodemand Azure AD que tous les accès tooa application nécessitent toujours l’authentification multifacteur, indépendamment de si cette application intrinsèquement prend en charge cette fonctionnalité. Un autre exemple courant de l’accès conditionnel est toorequire que les utilisateurs soient connectés toohello organisation approuvé réseau dans l’ordre tooaccess une application particulièrement sensible.

| Guide des articles |  |
|:---:| --- |
| Fonctionnalités d’un accès conditionnel toohello introduction offertes dans Azure AD, Office 365 et Intune |[Gestion des risques avec accès conditionnel](active-directory-conditional-access.md) |
| Comment accéder à la tooenable conditionnelle pour hello suivant les types de ressources |[Accès conditionnel pour les applications SaaS](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Accès conditionnel pour les services Office 365](active-directory-conditional-access-device-policies.md)<br /><br />[Accès conditionnel pour des applications locales](active-directory-conditional-access.md)<br /><br />[Accès conditionnel pour les applications locales publiées par le biais du proxy d’application Azure AD](active-directory-application-proxy-conditional-access.md) |

| Comment les appareils tooregister avec Azure Active Directory dans commander tooenable stratégies d’accès conditionnel périphérique | [Vue d’ensemble de l’inscription Azure Active Directory](active-directory-conditional-access-device-registration-overview.md)<br /><br />[Comment tooEnable l’inscription automatique pour les appareils Windows joints à un domaine](active-directory-conditional-access-automatic-device-registration.md)<br />— [Étapes pour les appareils Windows 8.1](active-directory-conditional-access-automatic-device-registration-setup.md)<br />— [Étapes pour les appareils Windows 7](active-directory-conditional-access-automatic-device-registration-setup.md) |

| Comment toouse hello application Authenticator de Microsoft pour vérification en deux étapes | [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

L’accès conditionnel est une fonctionnalité [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

## <a name="apps--azure-ad"></a>Applications et Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Cloud App Discovery : recherchez les applications SaaS en cours d’utilisation dans votre organisation
Cloud App Discovery permet de savoir quelles applications SaaS sont utilisées dans l’organisation de hello informatiques. Il est possible de mesurer l’utilisation des applications et de popularité, pour qu’il puisse déterminer quelles applications bénéficieront hello plus d’être soumis au contrôle de l’informatique et qui est intégrée à Azure AD.

| Guide des articles |  |
|:---:| --- |
| Vue d’ensemble de son fonctionnement |[Détection des applications cloud non approuvées avec Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md) |
| Approfondir son fonctionnement avec tooquestions réponses sur la confidentialité |[Considérations relatives à la confidentialité et à la sécurité](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| Forum Aux Questions (FAQ) |[Forum Aux Questions consacré à Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Didacticiels de déploiement de Cloud App Discovery |[Guide de déploiement de stratégie de groupe](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[Guide de déploiement de System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[Installation sur les serveurs proxy avec ports personnalisés](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| journal de l’agent de découverte d’application Cloud toohello mises à jour des modifications de Hello |[Journal des modifications](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Cloud App Discovery est une fonctionnalité [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>Approvisionnement automatique des comptes d’utilisateur dans les applications SaaS et annulation de l’approvisionnement
Automatiser la création de hello, la maintenance et la suppression des identités des utilisateurs dans les applications SaaS telles que l’échange, Salesforce, ServiceNow et bien plus encore. Correspond à la synchronisation et des identités existantes entre Azure AD et vos applications SaaS et contrôler l’accès en désactivant les comptes lorsque les utilisateurs quittent l’organisation de hello.

| Guide des articles |  |
|:---:| --- |
| En savoir plus sur son fonctionnement et de trouver les réponses aux questions de toocommon |[Automatiser la configuration de l’utilisateur & Deprovisioning tooSaaS applications](active-directory-saas-app-provisioning.md) |
| Configurer le mappage des informations entre Azure AD et votre application SaaS |[Personnalisation des mappages d’attributs](active-directory-saas-customizing-attribute-mappings.md)<br><br>[Écriture d’expressions pour les mappages d’attributs](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Comment tooenable automatisé configuration application tooany qui prend en charge le protocole SCIM hello |[Configurer l’approvisionnement des utilisateurs automatisée tooany SCIM-Enabled application](active-directory-scim-provisioning.md) |
| Comment tooreport sur et résoudre les problèmes de configuration de l’utilisateur |[Création de rapports sur l’approvisionnement d’utilisateurs automatique](active-directory-saas-provisioning-reporting.md)<br><br>[Notifications d’approvisionnement](active-directory-saas-account-provisioning-notifications.md)<br><br>[Résolution des problèmes d’approvisionnement d’utilisateurs](active-directory-application-provisioning-content-map.md) |
| Limiter les personnes qui obtient application tooan mis en service en fonction de leurs valeurs d’attribut |[Filtres d’étendue](active-directory-saas-scoping-filters.md) |

Approvisionnement automatique des utilisateurs est disponible pour toutes les éditions d’Azure AD pour les applications tooten par utilisateur. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) prend en charge un nombre illimité d’applications. Si votre organisation a [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) ou [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), vous pouvez [utiliser toomanage groupes quels utilisateurs obtient configurés](#managing-access-to-applications).

### <a name="building-applications-that-integrate-with-azure-ad"></a>Création d’applications qui s’intègrent à Azure AD
Si votre organisation développe ou gérer les applications de line-of-business (LoB), ou si vous êtes un développeur d’application avec les clients qui utilisent Azure Active Directory, hello suivant didacticiels vous aideront à intégrer vos applications avec Azure AD.

| Guide des articles |  |
|:---:| --- |
| Conseils pour les professionnels de l’informatique et les développeurs d’applications sur l’intégration d’applications à Azure AD |[Guide Hello professionnel de l’informatique pour développer des Applications pour Azure AD](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Guide du développeur Hello pour Azure Active Directory](active-directory-developers-guide.md) |
| Comment tooapplication fournisseurs peuvent ajouter leur toohello applications Galerie d’applications Azure AD |[Affichage de votre Application Bonjour Galerie d’applications Azure Active Directory](active-directory-app-gallery-listing.md) |
| Comment toomanage accéder aux applications toodeveloped à l’aide d’Azure Active Directory |[Comment tooEnable affectation d’utilisateurs pour les Applications développées](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[Affectation d’utilisateurs tooyour application](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[Groupe d’affectation tooyour application](active-directory-applications-guiding-developers-assigning-groups.md) |

Si vous développez des applications orientées consommateur, peut vous intéresser à l’aide de [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) afin que vous n’avez pas votre propre toomanage de système d’identité toodevelop vos utilisateurs. [En savoir plus](../active-directory-b2c/active-directory-b2c-overview.md).

## <a name="managing-access-tooapplications"></a>Gestion des accès tooApplications
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>À l’aide de groupes et toomanage libre service qui a accès toowhich applications
vous gérez des utilisateurs autorisés à accéder aux ressources de toowhich toohelp, Azure Active Directory vous permet de tooset affectations et les autorisations à l’échelle à l’aide de groupes. Service informatique peut choisir les tooenable libre-service fonctionnalités afin que les utilisateurs peuvent simplement demander l’autorisation quand ils en ont besoin.

| Guide des articles |  |
|:---:| --- |
| Vue d’ensemble des fonctionnalités de gestion d’accès Azure AD |[Introduction tooManaging tooApps d’accès](active-directory-managing-access-to-apps.md)<br /><br />[Fonctionnement de la gestion des accès dans Azure AD](active-directory-manage-groups.md)<br /><br />[Comment tooUse groupes tooManage tooSaaS d’accès aux Applications](active-directory-accessmanagement-group-saasapps.md) |
| Activer la gestion des applications et groupes en libre-service |[Gestion des applications en libre-service](active-directory-self-service-application-access.md)<br /><br />[Gestion des groupes en libre-service](active-directory-accessmanagement-self-service-group-management.md) |
| Instructions pour configurer vos groupes dans Azure AD |[Comment tooCreate groupes de sécurité](active-directory-accessmanagement-manage-groups.md)<br /><br />[Comment tooDesignate les propriétaires d’un groupe](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[Comment tooUse hello « tous les utilisateurs » du groupe](active-directory-accessmanagement-dedicated-groups.md) |
| Utilisez des groupes dynamiques tooautomatically remplir l’appartenance au groupe à l’aide de règles d’adhésion basées sur un attribut |[Appartenance au groupe dynamique  : règles avancées](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[Résolution des problèmes liés à l’appartenance au groupe dynamique](active-directory-accessmanagement-troubleshooting.md) |

La gestion de l’accès aux applications basée sur un groupe est disponible pour [Azure AD Standard](https://azure.microsoft.com/pricing/details/active-directory/) et [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). La gestion des groupes en libre-service, la gestion des applications en libre-service et les groupes dynamiques sont des fonctionnalités [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>B2B Collaboration : Activer le partenaire accès tooapplications
Si votre entreprise a conclu un partenariat avec d’autres sociétés, il est probable que vous avez besoin d’applications d’entreprise de tooyour toomanage partenaire access. Azure Collaboration B2B d’Active Directory fournit un tooshare de manière simple et sécurisée de vos applications avec des partenaires.

| Guide des articles |  |
|:---:| --- |
| Vue d’ensemble des différentes fonctionnalités Azure AD qui vous aident à gérer des utilisateurs externes tels que des partenaires ou des clients. |[Comparaison des capacités de gestion des identités externes dans Azure AD](active-directory-b2b-compare-external-identities.md) |
| Un tooB2B introduction de Collaboration et de mode de démarrage tooget |[Intégration de partenaires cloud simple et sécurisée avec Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Azure Active Directory B2B Collaboration](active-directory-b2b-collaboration-overview.md) |
| Approfondir Azure AD B2B Collaboration et la manière dont toouse il |[Collaboration B2B : Fonctionnement](active-directory-b2b-how-it-works.md)<br /><br />[Limites actuelles d’Azure AD B2B Collaboration](active-directory-b2b-current-limitations.md)<br /><br />[Procédure pas à pas détaillée de l’utilisation d’Azure AD B2B Collaboration](active-directory-b2b-detailed-walkthrough.md) |
| Articles de référence contenant des détails techniques sur le fonctionnement d’Azure AD B2B Collaboration |[Format de fichier CSV pour l’ajout d’utilisateurs partenaires](active-directory-b2b-references-csv-file-format.md)<br /><br />[Attributs de l’utilisateur affectés par Azure AD B2B Collaboration](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[Format de jeton utilisateur pour les utilisateurs partenaires](active-directory-b2b-references-external-user-token-format.md) |

B2B Collaboration est actuellement disponible pour [toutes les éditions d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>Volet d’accès : portail pour accéder aux applications et fonctionnalités de libre-service
Hello d’accès Azure AD est où les utilisateurs finaux peuvent lancer leurs applications et les fonctionnalités de libre-service accès hello qui leur permettent de toomanage leurs applications et les appartenances aux groupes. En outre toohello autres options pour l’accès à des applications compatibles avec l’authentification unique, volet d’accès sont inclus dans la liste hello ci-dessous.

| Guide des articles |  |
|:---:| --- |
| Une comparaison de hello différentes options disponibles pour le déploiement d’applications avec authentification unique toousers |[Déploiement d’Applications intégré de Azure AD tooUsers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Une vue d’ensemble de hello volet d’accès et son MyApps équivalent mobile |[Introduction tooAccess Panneau de configuration et MyApps](active-directory-saas-access-panel-introduction.md)<br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Comment les applications tooaccess Azure AD à partir de hello du site Web Office 365 |[À l’aide de hello Lanceur d’applications Office 365](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| Comment les applications tooaccess Azure AD à partir de hello application mobile Intune Managed Browser |[Intune Managed Browser](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Comment les applications tooaccess Azure AD à l’aide des liens profonds tooinitiate l’authentification unique |[Obtention de l’authentification sur des liens directs tooYour applications](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

Le volet d’accès est disponible pour [toutes les éditions d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>Rapports : Facilement auditer les modifications de l’accès d’application et surveiller les connexions tooapps
Azure Active Directory fournit plusieurs rapports et alertes toohelp vous surveillez tooapplications d’accès de votre organisation. Vous pouvez recevoir des alertes pour les applications tooyour-connexions anormales, et vous pouvez suivre quand et pourquoi l’application de tooan un utilisateur d’accès a changé.

| Guide des articles |  |
|:---:| --- |
| Une vue d’ensemble de hello dans Azure Active Directory, les fonctions de rapport |[Prise en main de la création de rapports Azure AD](active-directory-reporting-getting-started.md) |
| Comment toomonitor hello connexions et l’utilisation de l’application de vos utilisateurs |[Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md) |
| Suivi des modifications apportées toowho peuvent accéder à une application particulière |[Événements de rapport d'audit d'Azure Active Directory](active-directory-reporting-audit-events.md) |
| Exporter des données de ces outils tooyour préféré de rapports à l’aide de hello hello API de création de rapports |[Prise en main de hello API de création de rapports AD Azure](active-directory-reporting-api-getting-started.md) |

les rapports qui sont inclus dans les différentes éditions d’Azure Active Directory, de toosee [cliquez ici](active-directory-view-access-usage-reports.md).

## <a name="see-also"></a>Voir aussi
[Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Services de domaine Azure Active Directory](https://azure.microsoft.com/services/active-directory-ds/)

[Azure Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/)
