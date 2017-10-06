---
title: aaaAzure Active Directory B2B collaboration API et la personnalisation | Documents Microsoft
description: "Azure Active Directory B2B collaboration prend en charge les relations de votre société croisée en activant tooselectively partenaires commerciaux un accès à vos applications d’entreprise"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>API et personnalisation d’Azure Active Directory B2B Collaboration

Nous avons eu de nombreux clients nous dire qu’ils veulent des processus d’invitation hello toocustomize d’une manière qui convient le mieux à leur organisation. Avec notre API, cela est possible. [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Fonctionnalités de l’invitation hello API
Hello API offre hello suivant de fonctionnalités :

1. Invitez un utilisateur externe avec *n’importe quelle* adresse e-mail.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. Personnaliser votre tooland utilisateurs où vous souhaitez une fois qu’ils acceptent leur invitation.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Choisissez toosend hello invitation standard courrier par nous

    ```
    "sendInvitationMessage": true
    ```

  avec un destinataire toohello message que vous pouvez personnaliser

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. Choisissez toocc : personnes tookeep Bonjour boucle sur votre invitation ce collaborateur.

5. Ou de personnaliser entièrement votre invitation et l’intégration de flux de travail en choisissant pas toosend notifications via Azure AD.

    ```
    "sendInvitationMessage": false
    ```

  Dans ce cas, vous récupérez une URL de remboursement des hello API que vous pouvez incorporer dans un modèle de courrier électronique, messagerie instantanée ou autre méthode de distribution de votre choix.

6. Enfin, si vous êtes un administrateur, vous pouvez choisir utilisateur de hello tooinvite en tant que membre.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>Modèle d’autorisation
Hello API peut être exécuté dans hello suivant les modes d’autorisation :

### <a name="app--user-mode"></a>Mode Application + Utilisateur
Dans ce mode, la personne qui utilise les besoins de hello API toohave hello autorisations toobe créer des invitations à participer à B2B.

### <a name="app-only-mode"></a>Mode Application uniquement
Dans le contexte uniquement d’application, application hello doit hello User.ReadWrite.All ou Directory.ReadWrite.All étendues pour hello invitation toosucceed.

Pour plus d’informations, consultez : https://graph.microsoft.io/docs/authorization/permission_scopes


## <a name="powershell"></a>PowerShell
Il est maintenant possible toouse PowerShell tooadd et inviter des utilisateurs externes tooan organisation facilement. Créer une invitation à l’aide d’applet de commande hello :

```
New-AzureADMSInvitation
```

Vous pouvez utiliser hello options suivantes :

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

Vous pouvez également extraire référence des API d’invitation hello dans [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-admin-add-users.md)
* [Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?](active-directory-b2b-iw-add-users.md)
* [éléments Hello Hello e-mail d’invitation B2B collaboration](active-directory-b2b-invitation-email.md)
* [Utilisation d’une invitation B2B Collaboration](active-directory-b2b-redemption-experience.md)
* [Attribution de licences Azure AD B2B Collaboration](active-directory-b2b-licensing.md)
* [Résolution des problèmes d’Azure Active Directory B2B Collaboration](active-directory-b2b-troubleshooting.md)
* [Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration](active-directory-b2b-faq.md)
* [Authentification multifacteur pour les utilisateurs B2B Collaboration](active-directory-b2b-mfa-instructions.md)
* [Ajouter des utilisateurs B2B Collaboration sans invitation](active-directory-b2b-add-user-without-invite.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
