---
title: "aaaHow toodetermine les toouse de la méthode d’authentification unique | Documents Microsoft"
description: "Comprendre hello unique authentification modes pris en charge par Azure AD et comment toopick l’un toochoose pour hello application vous intéressent."
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
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>Comment toodetermine les toouse de la méthode d’authentification unique

Cet article vous a-t-il toounderstand hello unique authentification modes pris en charge par Azure AD et comment toopick l’un toochoose pour hello application vous intéressent.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Modes d’authentification unique et d’approvisionnement pris en charge par des types d’applications spécifiques

tableau Hello ci-dessous décrit hello différent de l’authentification unique et la configuration des modes pris en charge par chacun des hello au-dessus de types d’applications. Vous pouvez utiliser cette toohelp table toounderstand quelle application, vous devez tooadd toosupport un objectif spécifique.

  ![Tableau des types d’applications](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Comment toochoose un mode d’authentification unique

prise en charge de Hello **l’authentification unique** modes pour les applications Azure AD sont répertoriés ci-dessous.

-   **Azure AD l’authentification unique sur désactivé** – choisissez Azure AD l’authentification unique sur désactivé **mode d’authentification unique** si vous n’est pas encore prêt toointegrate cette application avec l’authentification unique avec Azure AD, ou testez simplement son évolution horizontale

-   **Lié à l’ouverture de session** – choisissez hello [lié Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **mode d’authentification unique** si vous avez une application qui est déjà connectée avec une seule session solution existante, ou si vous souhaitez simplement toopublish simple de liens pour vos utilisateurs dans leurs [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou [Lanceur d’applications Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Mot de passe de session** – choisissez hello [mot de passe de session](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **mode d’authentification unique** si votre application s’affiche un champ de nom d’utilisateur et mot de passe HTML et que vous souhaitez toostore qui nom d’utilisateur et mot de passe en toute sécurité toobe relus application toohello plus tard

-   **SAML-authentification** – choisissez hello [SAML-authentification](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) en fonction de rôles d’application toospecific d’authentification unique mode si votre application prend en charge les protocoles SAML ou OpenID Connect hello ou si vous souhaitez les utilisateurs en mesure de toomap de toobe dans les règles que vous définissez dans votre SAML revendications *(**Remarque :** cette option n’est pas disponible lorsque le proxy d’application hello est configuré pour une application) *

-   **En-tête-authentification** – choisissez cette option [basée sur l’en-tête de l’authentification](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) seul mode d’authentification si vous avez une application à l’aide de PingAccess qui prend en charge d’en-tête HTTP en fonction d’authentification que vous souhaitez tooperform l’authentification unique sur trop *(**Remarque :** cette option est disponible uniquement lorsque le proxy d’application hello et PingAccess est configuré pour une application) *

-   **L’authentification intégrée Windows** – choisissez hello [l’authentification Windows intégrée](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) l’authentification unique sur mode lors de l’exposition d’une application WIA local que vous souhaitez tooperform l’authentification unique sur trop*()*  *Remarque :** cette option est disponible uniquement lorsque le proxy d’application hello est configuré pour une application) *

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

6.  Sélectionnez application hello tooconfigure l’authentification unique

7.  Une fois le charge de l’application hello, cliquez sur **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)

