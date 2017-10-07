---
title: tooIntegrate aaaHow avec Azure Active Directory | Documents Microsoft
description: "Un toobenefits guide d’et de ressources pour l’intégration avec Azure Active Directory."
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>Intégration avec Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory offre aux organisations la gestion des identités professionnelles pour les applications cloud.  Intégration d’Azure AD permet à vos utilisateurs une expérience de connexion simplifiée et permet à votre application est conforme à la stratégie de tooIT.

## <a name="how-toointegrate"></a>Comment tooIntegrate
Il existe plusieurs façons pour toointegrate de votre application auprès d’Azure AD.  Bénéficiez d’autant de ces scénarios nécessaires à votre application.

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>Prise en charge Azure AD comme un moyen tooSign dans tooYour Application
**Réduction des problèmes de connexion et réduction des coûts de prise en charge.** À l’aide de Azure AD toosign dans tooyour application, vos utilisateurs n’auront pas un tooremember plus de nom et mot de passe.  En tant que développeur, vous avez un moins toostore de mot de passe et protéger.  N’ayant ne pas de réinitialisations de mot de passe oublié de toohandle peut être un seul des économies significatives.  Azure AD optimise la connexion pour certaines des applications de cloud les plus populaires hello au monde, y compris Office 365 et Microsoft Azure.  Avec des centaines de millions utilisateurs issus de millions d’organisations, sans doute votre utilisateur est déjà connecté tooAzure AD.  En savoir plus sur [l’ajout de la prise en charge pour la connexion Azure AD](active-directory-authentication-scenarios.md).

**Simplifiez l’inscription à votre application.**  Lors de l'inscription de votre application, Azure AD peut envoyer des informations essentielles sur un utilisateur pour vous permettre de remplir au préalable votre formulaire d'inscription ou de le supprimer complètement.  Les utilisateurs peuvent souscrire pour votre application à l’aide de leur compte Azure AD via un consentement familiers expérience similaire toothose trouvé dans les médias sociaux et des applications mobiles.  Tout utilisateur peut inscrire et connectez-vous à application tooan qui est intégrée à Azure AD sans nécessiter d’intervention de l’informatique.  En savoir plus sur [l’inscription de votre application pour la connexion d’un compte Azure AD](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) .

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>Rechercher des utilisateurs, gérer l’approvisionnement des utilisateurs et contrôler l’accès tooYour Application
**Rechercher des utilisateurs dans le répertoire de hello.**  Utiliser hello API Graph toohelp aux utilisateurs de rechercher et Parcourir pour d’autres personnes dans leur organisation lors de l’invitation à d’autres utilisateurs ou adresses de messagerie de l’octroi d’accès, au lieu de demander les tootype.  Les utilisateurs peuvent rechercher à l’aide d’une interface de style livre adresse familiers, notamment l’affichage des détails de hello de la hiérarchie d’organisation hello.  En savoir plus sur hello [API Graph](active-directory-graph-api.md).

**Réutilisation des groupes Active Directory et des listes de distribution déjà gérées par votre client.**  Azure Active Directory contient des groupes de hello que votre client est déjà à l’aide de la distribution du courrier électronique et gestion de l’accès.  À l’aide de hello API Graph, réutiliser ces groupes au lieu de toocreate de votre client de demander et gérer un ensemble distinct de groupes dans votre application.  Informations sur les groupes peuvent également être envoyées tooyour application dans les jetons de connexion.  En savoir plus sur hello [API Graph](active-directory-graph-api.md).

**Utilisez toocontrol Azure AD qui a accès tooyour application.**  Les administrateurs et les propriétaires d’applications dans Azure AD peuvent affecter l’accès tooapplications toospecific utilisateurs et groupes.  À l’aide de hello API Graph, vous pouvez lire cette liste et utilisez-la toocontrol mise en service et l’annulation du déploiement de ressources et accéder au sein de votre application.

**Utilisation d’Azure AD pour les rôles en fonction d’Access Control.**  Les administrateurs et les propriétaires d’applications peuvent affecter les utilisateurs et groupes tooroles que vous définissez lorsque vous inscrivez votre application dans Azure AD.  Informations sur les rôles sont envoyées tooyour application dans les jetons de connexion et peuvent également être lue à l’aide de l’API Graph de hello.  En savoir plus sur l’ [utilisation d'Azure AD pour les autorisations](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx).

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>Obtenir les profils d’accès tooUser, calendrier, messagerie, Contacts, fichiers et bien plus encore
**Azure AD est le serveur d’autorisation de hello pour Office 365 et d’autres services professionnels de Microsoft.**  Si vous prenez en charge Azure AD pour l’authentification dans une application de tooyour ou de la prise en charge de la liaison de vos comptes tooAzure AD utilisateur comptes d’utilisateur actuels à l’aide d’OAuth 2.0, vous pouvez demander la lecture et l’utilisateur un accès en écriture tooa profil, calendrier, messagerie, contacts, fichiers et autres informations.  Vous pouvez accéder en toute transparence écrire le calendrier d’événements toouser et lire ou écrire des fichiers tootheir OneDrive.  En savoir plus sur [l’accès à hello API Office 365](https://msdn.microsoft.com/office/office365/howto/platform-development-overview).

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>Promouvoir votre Application Bonjour Azure et Office 365 Marketplaces
**Promouvoir votre toohello application millions d’organisations qui utilisent déjà Azure AD.**  Les utilisateurs qui recherchent ces marketplace utilisent déjà un ou plusieurs services cloud, ce qui les définit en tant que clients de service cloud.  En savoir plus sur la promotion de votre application dans [hello Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/).

**Lorsque des utilisateurs s’inscrivent à votre application, cela apparaîtra dans leur panneau d'accès Azure AD et le lanceur d'applications Office 365.**  Les utilisateurs seront tooquickly en mesure d’et application tooyour retour facilement une version ultérieure, amélioration de l’intérêt des utilisateurs.  En savoir plus sur hello [volet d’accès Azure AD](../active-directory-saas-access-panel-introduction.md).

### <a name="secure-device-to-service-and-service-to-service-communication"></a>Sécurisation de la communication de périphérique à service et de service à service
**À l’aide d’Azure AD pour la gestion des identités des appareils et services réduit le code hello vous devez toowrite et permet un accès informatique toomanage.**  Appareils et services peuvent obtenir des jetons d’Azure AD à l’aide d’OAuth et utiliser ces API de jetons tooaccess web.  Grâce à Azure AD, vous pouvez éviter d'écrire du code d'authentification complexe.  Étant donné que les identités de hello des appareils et services de hello sont stockées dans Azure AD, informatique peut gérer les clés et révocation dans un endroit unique au lieu d’avoir toodo cela séparément dans votre application.

## <a name="benefits-of-integration"></a>Avantages de l'intégration
Intégration à Azure AD est fourni avec les avantages que vous n’avez pas besoin de code supplémentaire toowrite.

### <a name="integration-with-enterprise-identity-management"></a>Intégration avec la gestion des identités d'entreprise
**Aidez votre application à se conformer aux stratégies informatiques.**  Les organisations intégrant leurs systèmes de gestion des identités avec Azure AD, donc lorsqu’une personne quitte une organisation, ils sont automatiquement perdues application tooyour d’accès sans tootake nécessitant d’informatique des étapes supplémentaires.  Service informatique peut gérer qui peut accéder à votre application et déterminer les stratégies d’accès sont requises - exemple multi-factor Authentication - réduire votre toocomply de code toowrite nécessaire avec des stratégies d’entreprise complexes.  Azure AD fournit avec un journal d’audit détaillés de qui a signé dans tooyour application, par conséquent, les administrateurs informatiques peuvent suivre l’utilisation.

**Azure AD étend cloud toohello de Active Directory afin que votre application peut s’intégrer à Active Directory.**  De nombreuses organisations monde hello utilisent Active Directory comme leurs connectez-vous principal et le système de gestion des identités et nécessitent leur toowork applications avec Active Directory.  L’intégration avec Azure AD permet d’intégrer votre application à Active Directory.

### <a name="advanced-security-features"></a>Fonctionnalités de sécurité avancées
**Authentification multifacteur**  Azure AD fournit une authentification multifacteur native.  Les administrateurs informatiques peuvent demander l’authentification multifacteur tooaccess votre application, afin que vous n’avez pas toocode cette prise en charge vous-même.  En savoir plus sur l’ [authentification multifacteur](https://azure.microsoft.com/documentation/services/multi-factor-authentication/).

**Détection de connexion anormale**  Azure AD traite des connexions plus d’un milliard de jour, lors de l’utilisation d’ordinateur une activité suspecte toodetect algorithmes d’apprentissage et de notifier les administrateurs informatiques d’identifier les problèmes éventuels.  Prend en charge l’authentification dans Azure AD, votre application obtienne des avantages hello cette protection. En savoir plus sur [l’affichage des rapports d'accès Azure Active Directory](../active-directory-view-access-usage-reports.md).

**Accès conditionnel.**  En outre toomulti--Factor authentication, les administrateurs peuvent exiger des conditions spécifiques être respectées avant que les utilisateurs peuvent se connecter au tooyour application.  Conditions qui peuvent être définies incluent la plage d’adresses IP hello de périphériques clients, l’appartenance dans les groupes spécifiés et l’état de hello du périphérique hello utilisé pour l’accès.  En savoir plus sur [l’accès conditionnel d’Azure Active Directory](../active-directory-conditional-access.md).

### <a name="easy-development"></a>Développement facile :
**Protocoles standard de l’industrie.**  Microsoft est validée toosupporting des normes industrielles.  Azure AD prend en charge les protocoles d’authentification SAML 2.0, OpenID Connect 1.0, OAuth 2.0 et WS-Federation 1.2 hello.  Hello API Graph est conforme à OData 4.0.  Si votre application a déjà prend en charge hello SAML 2.0 ou OpenID Connect 1.0 protocoles pour la connexion fédérée, l’ajout d’un support pour Azure AD peut être simple.  En savoir plus sur les [protocoles d'authentification pris en charge par Azure AD](active-directory-authentication-protocols.md).

**Bibliothèques open source.**  Microsoft fournit des bibliothèques entièrement prise en charge open source pour le développement de toospeed langues et plateformes populaires.  code source de Hello est sous licence Apache 2.0 et sont toofork libre et de contribuer toohello arrière projets.  En savoir plus sur les [bibliothèques d'authentification Azure AD](active-directory-authentication-libraries.md).

### <a name="worldwide-presence-and-high-availability"></a>Présence dans le monde entier et haute disponibilité
**Azure AD est déployé dans les centres de données monde hello et géré et surveillé autour de l’horloge hello.**  Azure AD est le système de gestion d’identité hello pour Microsoft Azure et Office 365 et est déployé dans des centres de 28 données monde hello.  Données d’annuaire sont garanties toobe répliquée tooat au moins trois des centres de données.  Équilibreurs de charge global Assurez-vous que les utilisateurs accèdent à la copie la plus proche d’Azure AD contenant leurs données hello, réacheminer demande automatiquement tooother des centres de données si un problème est détecté.

## <a name="next-steps"></a>Étapes suivantes
[Commencer à écrire du code](active-directory-developers-guide.md#get-started).

[Connexion des utilisateurs à l'aide d'Azure AD](active-directory-authentication-scenarios.md)

