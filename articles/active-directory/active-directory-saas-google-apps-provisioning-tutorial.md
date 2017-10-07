---
title: "Didacticiel : configuration de Google Apps pour l’approvisionnement automatique d’utilisateurs dans Azure | Documents Microsoft"
description: "Découvrez comment tooautomatically approvisionner et configurer des comptes d’utilisateurs Azure AD tooGoogle applications."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Didacticiel : configuration de Google Apps pour approvisionner automatiquement des utilisateurs

objectif Hello de ce didacticiel est tooshow que vous hello étapes, vous devez tooperform dans Google Apps et Azure AD fourniture de tooautomatically et annuler la configuration des comptes d’utilisateur à partir d’Azure AD tooGoogle applications.

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory.
*   Vous devez avoir un client valide pour Google Apps pour Travailler ou Google Apps pour l’Éducation. Vous pouvez utiliser un compte d’essai gratuit pour chaque service.
*   Un compte utilisateur dans Google Apps avec les autorisations d’administrateur d’équipe.

## <a name="assigning-users-toogoogle-apps"></a>Affectation d’utilisateurs tooGoogle applications

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD qui représentent des utilisateurs qui doivent accéder aux applications de Google Apps tooyour hello. Une fois choisi, vous pouvez attribuer ces applications de Google Apps tooyour les utilisateurs en suivant les instructions hello ici : [affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   Il est recommandé qu’un seul utilisateur Azure AD avoir hello de tootest tooGoogle applications service de la configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.
>*   Lorsque vous affectez un tooGoogle utilisateur applications, vous devez sélectionner hello utilisateur ou rôle de « Groupe » dans la boîte de dialogue attribution hello. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.

## <a name="enable-automated-user-provisioning"></a>Activer l’approvisionnement automatique des utilisateurs

Cette section vous guide à travers de la connexion du compte d’utilisateur de vos applications Azure AD tooGoogle API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Google Apps, en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD .

>[!Tip]
>Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Google Apps, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="configure-automatic-user-account-provisioning"></a>Configurer l’approvisionnement automatique d’un compte utilisateur

> [!NOTE]
> Une autre option viable pour automatiser la configuration des applications de tooGoogle de l’utilisateur est toouse [Google Apps Active Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) qui configure votre ordinateur local Active Directory identités tooGoogle applications. En revanche, la solution hello dans ce didacticiel configure vos utilisateurs Active Directory de Azure (cloud) et les groupes à extension messagerie tooGoogle applications. 

1. L’authentification à hello [Google Apps Admin Console](http://admin.google.com/) à l’aide de votre compte d’administrateur, puis cliquez sur **sécurité**. Si vous ne voyez pas le lien de hello, il peut être masquée sous hello **plus de contrôles** menu bas hello écran hello.
   
    ![Cliquez sur Sécurité.][10]

2. Sur hello **sécurité** , cliquez sur **référence de l’API**.
   
    ![Cliquez sur Référence d’API.][15]

3. Sélectionnez **Activer l'accès à l'API**.
   
    ![Cliquez sur Référence d’API.][16]

    > [!IMPORTANT]
    > Pour chaque utilisateur que vous avez l’intention tooprovision tooGoogle applications, leur nom d’utilisateur dans Azure Active Directory *doit* être liée tooa des domaines personnalisés. Par exemple, les noms d'utilisateur qui ressemblent à bob@contoso.onmicrosoft.com ne sont pas acceptés par Google Apps, tandis que ceux ressemblant à bob@contoso.com sont acceptés. Vous pouvez modifier le domaine d’un utilisateur existant en modifiant ses propriétés dans Azure AD. Instructions pour la tooset un domaine personnalisé pour Azure Active Directory et Google Apps sont inclus dans comme suit.
      
4. Si vous n’avez pas encore ajouté un tooyour de nom de domaine personnalisé Azure Active Directory, puis suivez hello comme suit :
  
    a. Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**. Dans la liste de répertoires hello, sélectionnez votre annuaire. 

    b. Cliquez sur **nom de domaine** sur hello du volet de navigation gauche, puis cliquez sur **ajouter**.
     
     ![domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![ajout de domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Tapez votre nom de domaine dans hello **nom de domaine** champ. Ce nom de domaine doit être hello même nom de domaine que vous avez l’intention de toouse pour Google Apps. Lorsque vous êtes prêt, cliquez sur hello **ajouter un domaine** bouton.
     
     ![nom de domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Cliquez sur **suivant** page de vérification toogo toohello. tooverify que vous possédez ce domaine, vous devez modifier les enregistrements DNS du domaine hello selon les valeurs toohello fournis sur cette page. Vous pouvez choisir tooverify à l’aide **les enregistrements MX** ou **enregistrements TXT**, selon ce que vous sélectionnez pour hello **Type d’enregistrement** option. Pour obtenir des instructions plus complètes sur le mode de nom de domaine de tooverify avec Azure AD, consultez [ajouter vos propres tooAzure de nom de domaine Active Directory](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Répétez hello étapes pour tous les domaines hello que vous avez l’intention de tooadd tooyour répertoire précédentes.

5. Maintenant que vous avez vérifié tous vos domaines avec Azure AD, vous devez maintenant les vérifier à nouveau avec Google Apps. Pour chaque domaine qui n’est pas déjà inscrit avec Google Apps, procédez hello comme suit :
   
    a. Bonjour [Google Apps Admin Console](http://admin.google.com/), cliquez sur **domaines**.
     
     ![Cliquer sur Domaines][20]

    b. Cliquez sur **Ajouter un domaine ou un alias de domaine**.
     
     ![Ajouter un nouveau domaine][21]

    c. Sélectionnez **ajouter un autre domaine**et tapez Bonjour nom de domaine hello que vous aimeriez tooadd.
     
     ![Entrer votre nom de domaine][22]

    d. Cliquez sur **Continuer et vérifier la propriété du domaine**. Suivez ensuite tooverify d’étapes hello que vous possédez le nom de domaine hello. Pour obtenir des instructions complètes sur tooverify votre domaine avec Google Apps, voir. [Vérifiez que le propriétaire de votre site avec Google Apps](https://support.google.com/webmasters/answer/35179).

    e. Répétez hello étapes pour tous les domaines supplémentaires que vous avez l’intention de tooadd tooGoogle applications précédentes.
     
     > [!WARNING]
     > Si vous modifiez le domaine principal de hello pour votre client Google Apps, et si vous avez déjà configuré l’authentification unique avec Azure AD, puis vous avez toorepeat étape #3 sous [deuxième étape : activer l’authentification unique sur](#step-two-enable-single-sign-on).
       
6. Bonjour [Google Apps Admin Console](http://admin.google.com/), cliquez sur **rôles d’administrateur**.
   
     ![Cliquer sur Google Apps][26]

7. Déterminer quels admin compte toouse toomanage de la configuration de l’utilisateur. Pourquoi **rôle admin** de ce compte, modifier hello **des privilèges** pour ce rôle. Vérifiez qu’elle a hello tous les **des privilèges d’administration API** activée afin que ce compte peut être utilisé pour la configuration.
   
     ![Cliquer sur Google Apps][27]
   
    > [!NOTE]
    > Si vous configurez un environnement de production, il est recommandé de hello est toocreate un compte d’administrateur dans Google Apps spécifiquement pour cette étape. Ces comptes doivent disposer d’un rôle d’administrateur associé qui possède les privilèges API nécessaires hello.
     
8. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

9. Si vous avez déjà configuré Google Apps pour l’authentification unique, recherchez votre instance de Google Apps à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Google Apps** dans la galerie d’applications hello. Sélectionnez Google Apps à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

10. Sélectionnez votre instance de Google Apps, puis hello **Provisioning** onglet.

11. Ensemble hello **Mode d’approvisionnement** trop**automatique**. 

     ![approvisionnement](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. Sous hello **informations d’identification administrateur** , cliquez sur **Authorize**. Une boîte de dialogue d’autorisation Google Apps s’ouvre dans une nouvelle fenêtre du navigateur.

13. Confirmez que vous souhaitez que les modifications de toomake autorisations Azure Active Directory toogive que tooyour Google Apps locataire. Cliquez sur **Accepter**.
    
     ![Confirmez les autorisations.][28]

14. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Google Apps application. Si hello connexion échoue, assurez-vous que votre compte Google Apps a des autorisations d’administrateur d’équipe et essayez hello **« Autoriser »** pas à pas.

15. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.

16. Cliquez sur **Enregistrer.**

17. Sous la section des mappages de hello, sélectionnez **tooGoogle de synchronisation Azure Active Directory Users applications.**

18. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooGoogle applications. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Google Apps pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

19. tooenable hello service de configuration d’Azure AD pour Google Apps, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres

20. Cliquez sur **Enregistrer.**

Il démarre la synchronisation initiale de hello de tous les utilisateurs et/ou groupes affectés tooGoogle des applications dans la section utilisateurs et groupes de hello. la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre application Google Apps.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png