---
title: "aaaHow toouse mots de passe d’application dans Azure MFA ? | Microsoft Docs"
description: "Cette page sera aider les utilisateurs à comprendre quelles sont les mots de passe d’application et ce qu’ils sont utilisés pour avec respect tooAzure l’authentification Multifacteur."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: bf2c11edc0ca81f2950eff0f7a3a24c8a5b34623
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Que sont les mots de passe d’application dans Azure Multi-Factor Authentication ?
Actuellement, certaines des applications non-Web, tels que hello Apple messagerie native client qui utilise Exchange Active Sync, ne prennent pas en charge l’authentification multifacteur. L’authentification multifacteur est activée par l’utilisateur. Cela signifie que si un utilisateur a été activé pour l’authentification multifacteur et ils essaient de toouse des applications non-Web, elles seront toodo Impossible donc. Un mot de passe permet cette toooccur.

Une fois que vous disposez d’un mot de passe d’application, vous l’utilisez à la place de votre mot de passe d’origine avec ces applications sans navigateur. Il s’agit, car lorsque vous inscrivez pour la vérification en deux étapes, vous indiquez à Microsoft pas les toolet tout le monde vous connecter avec votre mot de passe si elles ne peut pas également effectuer la vérification de second hello. client de messagerie native Apple Hello sur votre téléphone ne peut pas se connecter en tant que vous, car il ne peut pas demander de vérification en deux étapes. Pour résoudre ce Hello est toocreate un mot de passe d’application plus sécurisée que vous n’utilisez pas quotidiennes, mais uniquement pour les applications qui ne prennent pas en charge vérification en deux étapes. Utilisez un mot de passe application hello afin que les applications qui peuvent contourner l’authentification multifacteur et continuer toowork.

> [!NOTE]
> Les clients Office 2013 (y compris Outlook) prennent en charge de nouveaux protocoles d’authentification et peuvent être utilisés dans le cadre de la vérification en deux étapes.  Ainsi, une fois activés, les mots de passe d’application ne sont pas obligatoires avec les clients Office 2013.  Pour plus d’informations, consultez [Version préliminaire publique de l’authentification moderne Office 2013 annoncée](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-toouse-app-passwords"></a>Comment les mots de passe toouse application
Hello Voici certains tooremember de choses sur la façon de mots de passe d’application toouse.

* Vous ne pouvez pas créer vos propres mots de passe d’application. En effet, ils sont générés automatiquement. Étant donné que vous n’avez tooenter hello mot de passe une fois par application, il est plus sûr toouse un mot de passe plus complexe, générée automatiquement plutôt que d’effectuer une que vous pouvez mémoriser.
* À l’heure actuelle, un utilisateur peut posséder jusqu’à 40 mots de passe. Si vous essayez de toocreate un fois que vous avez atteint la limite de hello, vous serez toodelete invité à un de vos mots de passe d’application existant avant de créer un nouveau.
* Il est recommandé d’utiliser un mot de passe d’application par appareil, et non par application. Par exemple, vous pouvez créer un mot de passe d’application pour votre ordinateur portable et utiliser ce mot de passe pour toutes vos applications sur cet ordinateur. Ensuite, créez une deuxième toouse de mot de passe d’application pour toutes vos applications sur votre bureau. 
* Première fois que vous inscrivez pour la vérification en deux étapes, vous pouvez soit un hello de mot de passe d’application.  Si vous avez besoin d’autres mots de passe, vous pouvez les créer.



## <a name="creating-and-deleting-app-passwords"></a>Création et suppression des mots de passe d’application
À la première connexion, vous obtenez un mot de passe d’application que vous pouvez utiliser.  En outre, vous pouvez également créer et supprimer des mots de passe d’application par la suite.  La procédure à suivre dépend de l’utilisation de l’authentification multifacteur. Toodetermine où vous devez adresser des mots de passe d’application toomanage de questions hello de réponse suivant : 

1. Utilisez-vous la vérification en deux étapes pour votre compte Microsoft personnel ? Si Oui, vous devez faire référence toohello [mots de passe d’application et de la vérification en deux étapes](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article d’aide. Si non, continuer tooquestion deux.

2. Vous utilisez la vérification en deux étapes pour votre compte professionnel ou scolaire. Vous l’utilisez toosign dans les applications tooOffice 365 ? Si Oui, vous devez faire référence trop[créer un mot de passe d’application pour Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) de l’aide. Si non, continuer tooquestion trois. 

3. Utilisez-vous la vérification en deux étapes avec Microsoft Azure ? Si Oui, continuer toohello [gérer les mots de passe d’application Bonjour Azure portal](#manage-app-passwords-in-the-Azure-portal) section de cet article. Si non, continuer tooquestion quatre.

4. Vous ne savez pas exactement dans quels cas vous utilisez la vérification en deux étapes ? Continuer toohello [gérer les mots de passe d’application avec le portail de MyApps hello](#manage-app-passwords-with-the-myapps-portal) section de cet article. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>Gérer les mots de passe d’application Bonjour portail Azure
Si vous utilisez la vérification en deux étapes avec Azure, vous souhaitez que les mots de passe application toocreate via hello portail Azure.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>mots de passe toocreate application Bonjour portail Azure
1. Se connecter toohello portail Azure classic.
2. En haut de hello, avec le bouton droit de votre nom d’utilisateur, puis sélectionnez Vérification de sécurité supplémentaire.
3. Sur la page Vérification hello, en haut hello, sélectionnez les mots de passe d’application
4. Cliquez sur **Créer**.
5. Entrez un nom pour le mot de passe hello et cliquez sur **suivant**
6. Copier le Presse-papiers toohello du mot de passe d’application hello et collez-le dans votre application.
   
   ![Cloud](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>mots de passe toodelete application Bonjour portail Azure
1. Se connecter toohello portail Azure classic.
2. En haut de hello, avec le bouton droit de votre nom d’utilisateur, puis sélectionnez Vérification de sécurité supplémentaire.
3. En haut hello, une vérification de sécurité tooadditional suivante, sélectionnez **mots de passe d’application.**
4. Suivant toohello application un mot de passe toodelete, sélectionnez **supprimer**.
5. Confirmez la suppression de hello en cliquant sur **Oui**.
6. Une fois que le mot de passe hello est supprimé, vous pouvez cliquer sur **fermer**.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>Gérer les mots de passe d’application avec le portail de MyApps hello.
Si vous n’êtes pas sûr de la façon dont vous utilisez l’authentification multifacteur, vous pouvez toujours créer et supprimer des mots de passe d’application via le portail de myapps hello.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>un mot de passe d’application à l’aide de toocreate hello Myapps portail
1. Connectez-vous trop[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Cliquez sur votre nom en haut de hello à droite, puis choisissez **profil**.
3. Sélectionnez **Vérification de sécurité supplémentaire**.
   ![Capture d’écran : Vérification de sécurité supplémentaire](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Sélectionnez **Mots de passe d’application**.
   ![Capture d’écran : sélection de Mots de passe d’application](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Cliquez sur **Créer**.
6. Entrez un nom pour le mot de passe hello et cliquez sur **suivant**.
7. Copier le Presse-papiers toohello du mot de passe d’application hello et collez-le dans votre application.
   ![Créer un mot de passe d’application](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>un mot de passe d’application à l’aide de toodelete hello Myapps portail
1. Connectez-vous trop[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. En haut de hello, sélectionnez le profil.
3. Sélectionnez **Vérification de sécurité supplémentaire**.

   ![Capture d’écran : Vérification de sécurité supplémentaire](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Sélectionnez **Mots de passe d’application**.

   ![Capture d’écran : sélection de Mots de passe d’application](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Suivant toohello application un mot de passe toodelete, cliquez sur **supprimer**.

   ![Supprimer un mot de passe d’application](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Confirmer que vous souhaitez toodelete ce mot de passe en cliquant sur **Oui**.
7. Une fois que le mot de passe hello est supprimé, vous pouvez cliquer sur **fermer**.

## <a name="next-steps"></a>Étapes suivantes

- [Gérer les paramètres de la vérification en deux étapes](multi-factor-authentication-end-user-manage-settings.md)

- Essayer hello [application Authenticator de Microsoft](microsoft-authenticator-app-how-to.md) tooverify vos connexions avec les notifications de l’application, au lieu de recevoir des appels ou textes. 
