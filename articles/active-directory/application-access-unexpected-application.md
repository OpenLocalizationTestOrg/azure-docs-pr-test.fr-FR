---
title: "application aaaUnexpected dans la liste d’applications | Documents Microsoft"
description: "Comment toosee toutes les applications dans votre client et de comprendre comment les applications s’affichent dans la liste de toutes les Applications dans les Applications d’entreprise"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>Application inattendue dans ma liste d’applications

Cet article vous a-t-il toounderstand l’apparence des applications dans votre **toutes les Applications** liste sous **des Applications d’entreprise**. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>Comment toosee toutes les applications dans votre client

toosee tous hello des applications dans votre client, vous devez toouse hello **filtre** contrôler tooshow **toutes les Applications** sous hello **toutes les Applications** liste. toodo, suit hello suivantes :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

6.  Cliquez sur Bonjour utilisez Bonjour **filtre** contrôle haut hello hello **liste de toutes les Applications**.

7.  Sur hello **filtre** panneau, jeu hello **afficher** option trop**toutes les Applications.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>Pourquoi une application spécifique apparaît-elle dans ma liste de toutes les applications ?

Lors du filtrage trop**toutes les Applications**, hello **toutes les Applications** **liste** montre tous les objets Principal du Service dans votre client. Les objets Principal de service peuvent apparaître dans cette liste de différentes façons :

1.  Lorsque vous ajoutez une application à partir de la galerie d’applications hello, y compris :

   1. **Applications de la galerie Azure AD** : applications pré-intégrées pour l’authentification unique avec Azure AD.

   2. **Applications du Proxy d’application** : une application en cours d’exécution dans votre environnement local que vous souhaitez tooprovide sécurisé l’authentification unique sur tooexternally.

   3. **Applications personnalisées** : une application de votre organisation souhaite toodevelop sur hello Azure plateforme de développement d’Application Active Directory, mais qui n’existe pas encore.

   4. **Applications hors galerie** : créez vos propres applications ! N’importe quel lien web ou toute application qui affiche un champ de nom d’utilisateur et mot de passe, prend en charge les protocoles SAML ou OpenID Connect, ou prend en charge SCIM sur laquelle vous souhaitez toointegrate pour l’authentification unique avec Azure AD.

2.  Lors de l’inscription ou de l’ouverture d’une session, une application <sup>tierce</sup> intégrée à Azure Active Directory. Exemple : [Smartsheet](https://app.smartsheet.com/b/home) ou [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).

3.  Lors de l’inscription ou l’ajout d’un utilisateur tooa de licence ou d’une groupe tooa première application de, telles que [Microsoft Office 365](http://products.office.com/).

4.  Lorsque vous ajoutez une nouvelle inscription de l’application en créant une application personnalisée à l’aide de hello [Registre de l’Application](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

5.  Lorsque vous ajoutez une nouvelle inscription de l’application en créant une application personnalisée à l’aide de hello [portail de l’enregistrement d’Application V2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).

6.  Lorsque vous ajoutez une application que vous développez à l’aide des [méthodes d’authentification ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) ou des [Services connectés](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) de Visual Studio.

7.  Lorsque vous créez un objet principal de service à l’aide de hello [Module PowerShell Azure AD](/powershell/azure/install-adv2?view=azureadps-2.0).

8.  Lorsque vous [consentement tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) comme un données toouse de l’administrateur de votre client.

9.  Lorsqu’un [utilisateur y consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse les données dans votre client.

10. Lorsque vous activez certains services qui stockent des données dans votre client. Un exemple est de réinitialiser un mot de passe, qui est modelée comme un toostore principal de service de votre mot de passe réinitialisation stratégie en toute sécurité.

lire de plus d’informations sur comment les applications sont ajoutées tooyour active, tooget [comment et pourquoi les applications sont ajoutées tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Je veux tooremove un utilisateur spécifique ou du groupe affectation tooan une application

tooremove une application utilisateur ou groupe affectation tooan, suivez les étapes de hello répertoriées dans hello [supprimer une attribution de l’utilisateur ou un groupe à partir d’une application d’entreprise dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) l’article.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>Je veux toodisable tous les accès tooan d’applications pour chaque utilisateur

toodisable toutes les applications de la tooan de connexions utilisateur, suivez les étapes de hello répertoriés dans hello [désactiver des connexions utilisateur pour une application d’entreprise dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) l’article.

## <a name="i-want-toodelete-an-application-entirely"></a>Je veux toodelete une application entièrement

trop**supprimer une application**, suivez les instructions de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello toodelete.

7.  Une fois le charge de l’application hello, cliquez sur **supprimer** icône à partir de l’application hello supérieur **vue d’ensemble** panneau.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Je veux toodisable tooany application de tous les futurs utilisateur consentement opérations

La désactivation de consentement de l’utilisateur pour éviter que les utilisateurs finaux d’application de tooany terme autorisation tout le répertoire. Les administrateurs peuvent toujours donner leur consentement au nom de l’utilisateur. toolearn en savoir plus sur l’application de consentement, et pourquoi vous pouvez ou pas souhaitiez toodo, lecture [utilisateur de présentation et de consentement de l’administrateur](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

trop**désactiver toutes les opérations de consentement d’utilisateur futures dans tout le répertoire**, suivez les instructions de hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.

5.  Cliquez sur **Paramètres utilisateur**.

6.  Désactiver toutes les opérations de consentement d’utilisateur futures en définissant un hello **les utilisateurs peuvent autoriser des applications tooaccess leurs données** basculer trop**non** et cliquez sur hello **enregistrer** bouton.

## <a name="next-steps"></a>Étapes suivantes
[Gestion des applications avec Azure Active Directory](active-directory-enable-sso-scenario.md)
