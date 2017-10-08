---
title: "toochoose aaaHow quelle application de type toouse lors de l’ajout d’une application | Documents Microsoft"
description: "Comprendre les types hello pris en charge des applications que vous pouvez intégrer à Azure AD et leurs options de configuration connexes"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>Comment toochoose quelle application de type toouse lors de l’ajout d’une application

Cet article vous a-t-il toounderstand hello quatre principaux types d’applications que vous pouvez intégrer à Azure AD :

* Ce qui est pris en charge par chacun d’eux
* Pourquoi choisir telle ou telle application
* Comment tooconfigure que les propriétés de l’application cœur, comment les utilisateurs sont **configuré**, ou **l’authentification unique** toouse de technologie.

## <a name="supported-application-types-in-azure-ad"></a>Types d’applications pris en charge dans Azure AD

Azure AD prend en charge quatre principaux types d’applications que vous pouvez ajouter à l’aide de hello **ajouter** fonctionnalité situés sous **des Applications d’entreprise**. Vous avez notamment vu les points suivants :

-   **Applications de la galerie Azure AD** : applications pré-intégrées pour l’authentification unique avec Azure AD.

-   **Applications du Proxy d’application** : une application en cours d’exécution dans votre environnement local que vous souhaitez tooprovide sécurisé l’authentification unique sur tooexternally.

-   **Applications personnalisées** : une application de votre organisation souhaite toodevelop sur hello Azure plateforme de développement d’Application Active Directory, mais qui n’existe pas encore.

-   **Applications hors galerie** : créez vos propres applications ! N’importe quel lien web ou toute application qui affiche un champ de nom d’utilisateur et mot de passe, prend en charge les protocoles SAML ou OpenID Connect, ou prend en charge SCIM sur laquelle vous souhaitez toointegrate pour l’authentification unique avec Azure AD.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>Fonctions et fonctionnalités pris en charge par tous les hello au-dessus de types d’applications

Hello fonctionnalités suivantes sont prises en charge par une des hello au-dessus des 4 types d’application dans Azure AD :

-   **Démarrage rapide** : commencez rapidement à utiliser une application en suivant des [étapes de déploiement simple](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started).

-   **Gestion des propriétés générales** : obtenir un [direct via un lien ciblé](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan application, [personnaliser hello marque](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) d’une application, ou [désactiver l’application hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) pour tous les utilisateurs.

-   **Gestion des utilisateurs et de groupe** – [affecter](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) ou [supprimer](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) utilisateurs et groupes tooan application et éventuellement affecter les rôles d’application spécifique hello ces utilisateurs et groupes ont accès à

-   **Accès aux applications de libre-service** – activer votre toorequest utilisateurs [accès à l’application automatique](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan des applications à partir de leur Application l’accès panneaux en ajoutant une application directement ou [ rejoindre un groupe activé libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), vous pouvez éventuellement demander une approbation entreprise le plus long hello moyen

-   **Des journaux de connexions** – consultez [tous hello application tooan de connexions](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), ou toutes vos applications

-   **Journaux d’audit** – consultez [détaillées des journaux d’audit sur l’application de modifications tooan](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), ou tooall vos applications

-   **Accès conditionnel et des risques** – définissez puissants [les règles d’accès basé sur une condition](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) qui sont appliquées lorsque les utilisateurs tentent de toosign dans une application spécifique de tooa

-   **Affichage des autorisations** – afficher hello [OAuth2 autorisations](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) une application a accès tooin votre annuaire à partir d’un emplacement unique

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Modes d’authentification unique et d’approvisionnement pris en charge par des types d’applications spécifiques

tableau Hello ci-dessous décrit hello différent de l’authentification unique et la configuration des modes pris en charge par chacun des hello au-dessus de types d’applications. Vous pouvez utiliser cette toohelp table toounderstand quelle application, vous devez tooadd toosupport un objectif spécifique.

  ![Tableau des types d’applications](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Comment toochoose un mode d’authentification unique

prise en charge de Hello **l’authentification unique** modes pour les applications Azure AD sont répertoriés ci-dessous.

-   **Azure AD l’authentification unique sur désactivé** – choisissez Azure AD l’authentification unique sur désactivé **mode d’authentification unique** si vous n’est pas encore prêt toointegrate cette application avec l’authentification unique avec Azure AD, ou testez simplement son évolution horizontale

-   **Lié à l’ouverture de session** – choisissez hello [lié Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **mode d’authentification unique** si vous avez une application qui est déjà connectée avec une seule session solution existante, ou si vous souhaitez simplement toopublish simple de liens pour vos utilisateurs dans leurs [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou [Lanceur d’applications Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Mot de passe de session** – choisissez hello [mot de passe de session](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **mode d’authentification unique** si votre application s’affiche un champ de nom d’utilisateur et mot de passe HTML et que vous souhaitez toostore qui nom d’utilisateur et mot de passe en toute sécurité toobe relus application toohello plus tard

-   **SAML-authentification** – choisissez hello [SAML-authentification](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) en fonction de rôles d’application toospecific d’authentification unique mode si votre application prend en charge les protocoles SAML ou OpenID Connect hello ou si vous souhaitez les utilisateurs en mesure de toomap de toobe dans les règles que vous définissez dans votre SAML revendications *

   >[!NOTE]
   >Cette option n’est pas disponible lorsque le proxy d’application hello est configuré pour une application.
   >
   >

-   **En-tête-authentification** – choisissez cette option [basée sur l’en-tête de l’authentification](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) seul mode d’authentification si vous avez une application à l’aide de PingAccess qui prend en charge d’en-tête HTTP en fonction d’authentification que vous souhaitez tooperform l’authentification unique sur trop

   >[!NOTE]
   >Cette option est disponible uniquement lorsque le proxy d’application hello et PingAccess est configuré pour une application.
   >
   >

-   **L’authentification intégrée Windows** – choisissez hello [l’authentification Windows intégrée](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) mode lors de l’exposition d’une application WIA local que vous souhaitez trop de tooperform l’authentification unique sur l’authentification unique

   >[!NOTE]
   >Cette option est disponible uniquement lorsque le proxy d’application hello est configuré pour une application.
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Modes d’authentification unique pour les applications personnalisées

Applications que vous avez personnalisé développé par hello [application personnalisée](#_Custom-Developed_Applications) expérience prennent également en charge un seul authentification modes supplémentaires non répertoriées ci-dessus. Vous avez notamment vu les points suivants :

-   Authentification basée sur [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)

-   Authentification basée sur [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)

-   Authentification basée sur [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)

-   Authentification basée sur [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)

Hello de lecture [guide du développeur Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn plus en détail comment une seule application toocreate un personnalisées qui prend en charge ces modes d’authentification.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>Comment tooset une application de mode d’authentification

tooset une application **l’authentification unique** mode, suivez les instructions hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello pour lequel vous souhaitez tooconfigure l’authentification unique.

7.  Une fois le charge de l’application hello, cliquez sur **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

## <a name="how-toochoose-a-provisioning-mode"></a>Comment toochoose un mode d’approvisionnement

-   **Approvisionnement manuel** – choisissez hello [manuel](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) mode de préparation si vous avez des comptes existants, ou que vous souhaitez toomanage les comptes pour cette application en dehors d’Azure AD.

-   **Approvisionnement automatique** – choisissez hello [automatique](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **le mode d’approvisionnement** si vous souhaitez que le service de configuration basée sur l’API tooenable automatique et/ou l’annulation du déploiement de comptes d’utilisateurs toothis application 

   >[!NOTE]
   >Cette option est disponible uniquement pour les applications au sein de hello **proposées** catégorie Hello [Galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **Provisionnement automatique SCIM** – utilisez [provisionnement automatique SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) si votre application prend en charge le protocole SCIM hello pour la détection des modifications toousers et des groupes, qui sont émis automatiquement les modifications tooany application intégrée à Azure AD 

   >[!NOTE]
   >Cette option n’est pas répertoriée comme un mode d’approvisionnement spécifique, mais est activée par défaut pour toutes les applications intégrées à Azure AD.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>Comment tooset une application d’approvisionnement de mode

tooset une application **configuration** mode, suivez les instructions hello ci-dessous :

tooset une application **l’authentification unique** mode, suivez les instructions hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello pour lequel vous souhaitez tooconfigure configuration.

7.  Une fois le charge de l’application hello, cliquez sur **Provisioning** à partir du menu de navigation de gauche de l’application hello.

## <a name="next-steps"></a>Étapes suivantes
[Gestion des applications avec Azure Active Directory](active-directory-enable-sso-scenario.md)
