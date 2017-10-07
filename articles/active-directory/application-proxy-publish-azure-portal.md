---
title: "les applications avec Proxy d’Application Azure AD aaaPublish | Documents Microsoft"
description: "Bonjour portail Azure, publier cloud de toohello d’applications local avec le Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publier des applications avec le Proxy d’application Azure AD

> [!div class="op_single_selector"]
> * [Portail Azure](application-proxy-publish-azure-portal.md)
> * [portail Azure Classic](active-directory-application-proxy-publish.md)

Proxy d’Application Azure Active Directory (AD) vous permet de prendre en charge des travailleurs à distance en publiant toobe d’applications local accédé via hello internet. Vous pouvez publier ces applications via hello tooprovide portail Azure à distance un accès sécurisé à partir d’à l’extérieur de votre réseau.

Cet article vous guide tout au long des étapes de hello toopublish une application locale avec le Proxy d’Application. Après avoir terminé cet article, vos utilisateurs seront être, tooaccess en mesure de votre application à distance. Et vous serez prêt tooconfigure des fonctionnalités supplémentaires pour l’application hello comme single sign-on, des informations personnalisées et exigences de sécurité.

Si vous êtes tooApplication nouveau Proxy, en savoir plus sur cette fonctionnalité avec l’article hello [comment tooprovide sécuriser l’accès à distance, applications locales tooon](active-directory-application-proxy-get-started.md).


## <a name="publish-an-on-premises-app-for-remote-access"></a>Publier une application locale pour un accès à distance

Suivez ces étapes toopublish vos applications avec Proxy d’Application. Si vous n’avez pas déjà téléchargé et configuré un connecteur pour votre organisation, passez trop[prise en main le Proxy d’Application et d’installer le connecteur de hello](active-directory-application-proxy-enable.md) tout d’abord, puis publier votre application.

> [!TIP]
> Si vous testez des Proxy d’Application pour hello première fois, sélectionnez une application qui est configurée pour l’authentification basée sur mot de passe. Le Proxy d’application prend en charge d’autres types d’authentification, mais les applications basées sur le mot de passe sont tooget plus simple de hello haut et à exécuter rapidement. 

1. Connectez-vous en tant qu’administrateur Bonjour [portail Azure](https://portal.azure.com/).
2. Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Nouvelle application**.

  ![Ajouter une application d’entreprise](./media/application-proxy-publish-azure-portal/add-app.png)

3. Sélectionnez **Tout**, puis **Application locale**.  

  ![Ajout de votre propre application](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Fournir hello suit les informations de votre application :

   - **Nom**: nom hello d’application hello qui apparaîtra dans le volet d’accès hello et Bonjour portail Azure. 

   - **URL interne**: hello URL que vous utilisez l’application de hello tooaccess à partir de votre réseau privé. Vous pouvez fournir un chemin d’accès spécifique sur hello toopublish de serveur principal, tandis que le reste de hello du serveur de hello n’est pas publiée. De cette façon, vous pouvez publier des sites différents sur hello même serveur en tant qu’applications différentes et chacune d’elles fournissent des ses propres règles d’accès et le nom.

     > [!TIP]
     > Si vous publiez un chemin d’accès, assurez-vous qu’il inclut toutes les images nécessaires de hello, des scripts et des feuilles de style pour votre application. Par exemple, si votre application est à https://yourapp/app et utilise des images à https://yourapp/media, vous devez publier https://yourapp/ comme chemin d’accès hello. Page d’accueil hello toobe que vos utilisateurs voient ne dispose pas cette URL interne. Pour plus d’informations, consultez [Définir une page d’accueil personnalisée pour les applications publiées](application-proxy-office365-app-launcher.md).

   - **URL externe**: hello adresse vos utilisateurs passera tooin commande tooaccess hello de l’application en dehors de votre réseau. Si vous ne souhaitez pas domaine de Proxy d’Application par défaut toouse hello, en savoir plus sur [des domaines personnalisés dans le Proxy d’Application Azure AD](active-directory-application-proxy-custom-domains.md).
   - **Pré-authentification**: comment le Proxy d’Application vérifie les utilisateurs avant d’en leur donnant accès tooyour application. 

     - Azure Active Directory : Le Proxy d’Application redirige toosign utilisateurs avec Azure AD, qui authentifie leurs autorisations pour le répertoire de hello et application. Nous vous recommandons de laisser cette option comme valeur par défaut de hello, afin que vous pouvez tirer parti des fonctionnalités de sécurité Azure AD telles que les conditions d’accès et l’authentification multifacteur.
     - Passthrough : Les utilisateurs n’aient tooauthenticate par rapport à l’application de hello tooaccess Azure Active Directory. Vous pouvez toujours configurer les exigences d’authentification sur le back-end hello.
   - **Groupe de connecteurs**: application tooyour de connecteurs processus hello accès à distance et les groupes de connecteur vous aident à organiser les connecteurs et les applications par région, le réseau ou objectif. Si vous n’avez pas les groupes de connecteurs encore créés, votre application est trop affectée**par défaut**.

   ![Configuration de votre application](./media/application-proxy-publish-azure-portal/configure-app.png)
5. Si nécessaire, configurez des paramètres supplémentaires. Pour la plupart des applications, vous devez conserver ces paramètres dans leur état par défaut. 
   - **Délai d’Application principal**: définissez cette valeur trop**Long** uniquement si votre application est lente tooauthenticate et se connecter. 
   - **URL dans les en-têtes**: conserver cette valeur en tant que **Oui** , sauf si votre application requis d’en-tête d’hôte d’origine hello dans la demande d’authentification hello.
   - **URL dans le corps de l’Application**: conserver cette valeur en tant que **non** , sauf si vous avez codé en dur HTML liens tooother des applications locales et que vous n’utilisez pas des domaines personnalisés. Pour plus d’informations, consultez [Rediriger les liens codés en dur pour les applications publiées avec le Proxy d’application Azure AD](application-proxy-link-translation.md).
   
   ![Configuration de votre application](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. Sélectionnez **Ajouter**.


## <a name="add-a-test-user"></a>Ajouter un utilisateur de test 

tootest que votre application a été publiée correctement, ajoutez un compte d’utilisateur de test. Vérifiez que ce compte dispose déjà des autorisations tooaccess hello de l’application à l’intérieur du réseau d’entreprise de hello.

1. Dans le panneau de démarrage rapide de hello, sélectionnez **affecter un utilisateur de test**.

  ![Attribuer un utilisateur à des fins de test](./media/application-proxy-publish-azure-portal/assign-user.png)

2. Sur les utilisateurs de hello et panneau de groupes, sélectionnez **ajouter**.

  ![Ajouter un utilisateur ou groupe](./media/application-proxy-publish-azure-portal/add-user.png)

3. Dans le panneau de devoir ajouter hello, sélectionnez **utilisateurs et groupes** puis choisissez compte hello tooadd. 
4. Sélectionnez **Attribuer**.

## <a name="test-your-published-app"></a>Tester votre application publiée

Dans votre navigateur, accédez à toohello URL externe que vous avez configurés au cours de hello étape de publication. Vous devez normalement voir écran d’accueil hello et être en mesure de toosign avec compte de test hello permet de paramétrer.

![Tester votre application publiée](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>Étapes suivantes
- [Télécharger des connecteurs](active-directory-application-proxy-enable.md) et [créer des groupes de connecteurs](active-directory-application-proxy-connectors-azure-portal.md) toopublish des applications sur des réseaux distincts et emplacements.

- [Configurer l’authentification unique](application-proxy-sso-azure-portal.md) pour votre application récemment publiée
