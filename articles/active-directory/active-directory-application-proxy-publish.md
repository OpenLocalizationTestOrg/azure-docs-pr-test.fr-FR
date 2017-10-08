---
title: "les applications avec Proxy d’Application Azure AD aaaPublish | Documents Microsoft"
description: "Publier le cloud de toohello d’applications local avec le Proxy d’Application Azure AD dans le portail classique de hello."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publier des applications avec le Proxy d’application Azure AD

> [!div class="op_single_selector"]
> * [Portail Azure](application-proxy-publish-azure-portal.md)
> * [portail Azure Classic](active-directory-application-proxy-publish.md)

Proxy d’Application Azure AD vous permet de prendre en charge des travailleurs à distance en publiant toobe d’applications local accédé via hello internet. À ce stade, vous devez déjà avoir [activé le Proxy d’Application Bonjour portail Azure classic](active-directory-application-proxy-enable.md). Cet article vous guide tout au long de hello étapes toopublish applications qui s’exécutent sur votre réseau local et fournir un accès sécurisé à distance à partir de votre réseau. Après avoir terminé cet article, vous serez prêt tooconfigure hello porte des informations personnalisées ou des exigences de sécurité.

> [!NOTE]
> Le Proxy d’application est une fonctionnalité qui est disponible uniquement si la mise à niveau toohello Premium ou édition de base d’Azure Active Directory. Pour plus d’informations, consultez la page [Éditions d’Azure Active Directory](active-directory-editions.md). Si vous souhaitez toouse Proxy d’Application, vous pouvez [publier des applications Bonjour Azure portal](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Publier une application à l’aide d’Assistant de hello
1. Connectez-vous en tant qu’administrateur Bonjour [portail Azure classic](https://manage.windowsazure.com/).
2. TooActive active, sélectionnez le répertoire hello où vous avez activé le Proxy d’Application.
   
    ![Active Directory - icône](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Cliquez sur hello **Applications** onglet, puis cliquez sur hello **ajouter** bouton bas hello écran hello
   
    ![Ajouter une application](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Sélectionnez **Publier une application qui sera accessible depuis l’extérieur de votre réseau**.
   
    ![Publier une application qui sera accessible depuis l’extérieur de votre réseau](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Fournir hello suit les informations de votre application :
   
   * **Nom**: nom convivial de hello pour votre application. Il doit être unique au sein de votre annuaire.
   * **URL interne**: adresse hello hello connecteur Proxy d’Application utilise l’application hello tooaccess à partir de votre réseau privé. Vous pouvez fournir un chemin d’accès spécifique sur hello toopublish de serveur principal, tandis que le reste de hello du serveur de hello n’est pas publiée. De cette façon, vous pouvez publier des sites différents hello même serveur et chacune d’elles donnent ses propres règles d’accès et le nom.
     
     > [!TIP]
     > Si vous publiez un chemin d’accès, assurez-vous qu’il inclut toutes les images nécessaires de hello, des scripts et des feuilles de style pour votre application. Par exemple, si votre application est à https://yourapp/app et utilise des images à https://yourapp/media, vous devez publier https://yourapp/ comme chemin d’accès hello.
     > 
     > 
   * **Méthode de pré-authentification**: comment le Proxy d’Application vérifie les utilisateurs avant d’en leur donnant accès tooyour application. Choisissez une des options de hello hello liste déroulante.
     
     * Azure Active Directory : Le Proxy d’Application redirige toosign utilisateurs avec Azure AD, qui authentifie leurs autorisations pour le répertoire de hello et application.
     * Passthrough : Les utilisateurs n’ont d’application de tooauthenticate tooaccess hello.
     
     ![Propriétés de l’application](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. Assistant de hello toofinish, cliquez sur la case à cocher hello bas hello écran hello. application Hello est maintenant définie dans Azure AD.

## <a name="assign-users-and-groups-toohello-application"></a>Affecter des utilisateurs et groupes toohello application
Dans commande pour vos utilisateurs tooaccess votre application publiée, vous devez tooassign les individuellement ou en groupes. (N’oubliez pas de tooassign trop vous-même accéder.) Chaque utilisateur assigné doit posséder une licence pour la version De base d’Azure ou versions ultérieures. Vous pouvez attribuer des licences individuellement ou toogroups. Pour plus d’informations, consultez [affectation d’utilisateurs tooan application](active-directory-applications-guiding-developers-assigning-users.md). 

Pour les applications qui nécessitent la pré-authentification, affectation d’un utilisateur accorde à autorisation toouse hello application. Pour les applications qui ne nécessitent pas la pré-authentification, affectation d’un utilisateur signifie que l’utilisateur hello peut accéder à application hello via le volet d’accès hello.

1. Après l’Assistant Ajouter une application hello vous connectez, vous voyez hello démarrage rapide de page de votre application. toomanage qui a accès toohello application, sélectionnez **utilisateurs et groupes**.
   
    ![Affectation des utilisateurs dans l’écran de démarrage rapide du proxy d’application - capture d’écran](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Recherchez des groupes spécifiques dans votre annuaire, ou affichez tous les utilisateurs. résultats de recherche toodisplay hello, cliquez sur la case à cocher hello.
   
      ![Recherche de groupes ou d’utilisateurs - capture d’écran](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Sélectionnez chaque utilisateur ou groupe tooassign toothis application et cliquez sur **affecter**. Vous êtes invité à tooconfirm cette action.

> [!NOTE]
> Pour les applications avec authentification Windows intégrée, vous pouvez affecter uniquement les utilisateurs et les groupes qui ont été synchronisés à partir de votre Active Directory local. Il n’est pas possible d’affecter les utilisateurs qui se connectent à l’aide d’un compte Microsoft et les invités aux applications publiées avec le proxy d’application Azure Active Directory. Assurez-vous que vos utilisateurs se connecter avec des informations d’identification qui font partie de hello même domaine que l’application hello que vous publiez.
> 
> 

## <a name="test-your-published-application"></a>Tester votre application publiée
Une fois que vous avez publié votre application, vous pouvez tester son évolution horizontale en naviguant toohello URL que vous avez publiée. Vérifiez que vous pouvez accéder à l’application, qu’elle s’affiche correctement et que tout fonctionne comme prévu. Si vous rencontrez un problème ou obtenez un message d’erreur, essayez de hello [guide de dépannage](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Configuration de votre application
Vous pouvez modifier les applications publiées ou configurer des options avancées sur la page Configurer hello. Dans cette page, vous pouvez personnaliser votre application en modifiant le nom de hello ou téléchargez un logo. Vous pouvez également gérer les règles d’accès comme hello méthode de pré-authentification ou l’authentification multifacteur.

![Configuration avancée](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Une fois que vous publiez des applications à l’aide du Proxy d’Application Azure Active Directory, ils apparaissent dans la liste des Applications hello dans Azure AD, et vous pouvez les gérer.

Si vous désactivez les services de Proxy d’Application après avoir publié des applications, les applications hello ne sont plus accessibles en dehors de votre réseau privé. Vos utilisateurs peuvent toujours accès hello applications locale comme d’habitude.

tooview une application et vérifiez que qu’il est accessible, double-cliquez sur nom hello de l’application hello. Si hello service Proxy d’Application est désactivée et l’application hello n’est pas disponible, un message d’avertissement s’affiche en haut de hello d’écran hello.

toodelete une application, sélectionnez une application dans la liste de hello puis **supprimer**.

## <a name="next-steps"></a>Étapes suivantes
* [Publier des applications avec votre propre nom de domaine](active-directory-application-proxy-custom-domains.md)
* [Activer l’authentification unique](active-directory-application-proxy-sso-using-kcd.md)
* [Activer l’accès conditionnel](active-directory-application-proxy-conditional-access.md)
* [Utiliser des applications utilisant les revendications](active-directory-application-proxy-claims-aware-apps.md)

Pour les informations les plus récentes hello et mises à jour, consultez hello [blog de Proxy d’Application](http://blogs.technet.com/b/applicationproxyblog/)

