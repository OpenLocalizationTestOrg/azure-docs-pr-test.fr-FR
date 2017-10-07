---
title: "aaaMicrosoft États d’utilisateur Azure multi-Factor Authentication"
description: "En savoir plus sur l’état utilisateur dans Azure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>La vérification en deux étapes de toorequire pour un utilisateur ou un groupe

Il existe deux approches pour exiger une vérification en deux étapes. Hello première option est tooenable chaque utilisateur pour Azure multi-Factor Authentication (MFA). Lorsque les utilisateurs sont activées individuellement, ils effectuent toujours la vérification en deux étapes (à quelques exceptions près, comme lorsqu’ils se connectent à partir d’adresses IP autorisées si hello mémorisés fonctionnalité de périphériques est mis sous tension). deuxième option de Hello est tooset une stratégie d’accès conditionnel qui requiert une vérification en deux étapes sous certaines conditions.

>[!TIP] 
>Choisissez une de ces méthodes toorequire en deux étapes la vérification, pas les deux. L’activation d’un utilisateur pour l’authentification multifacteur Azure remplace toutes les stratégies d’accès conditionnel.

## <a name="which-option-is-right-for-you"></a>Choisir l’option qui vous convient

**L’activation de l’authentification Multifacteur Azure en modifiant des États utilisateur** est l’approche traditionnelle de hello pour exiger une vérification en deux étapes. Elle fonctionne pour les deux Azure MFA dans le cloud de hello et le serveur Azure MFA. Tous les utilisateurs de hello que vous activez ont hello même expérience, qui est une vérification en deux étapes tooperform chaque fois qu’ils se connectent. L’activation d’un utilisateur remplace toutes les stratégies d’accès conditionnel appliquées à cet utilisateur. 

**L’activation de l’authentification multifacteur Azure avec une stratégie d’accès conditionnel** est une approche plus souple pour exiger une vérification en deux étapes. Il fonctionne toutefois, pour l’authentification Multifacteur Azure dans le cloud de hello, et l’accès conditionnel est un [payé la fonctionnalité d’Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features). Vous pouvez créer des stratégies d’accès conditionnel qui s’appliquent toogroups, ainsi que des utilisateurs individuels. Vous pouvez appliquer davantage de restrictions aux groupes à haut risque par rapport aux groupes à faible risque, ou exiger la vérification en deux étapes uniquement pour les applications cloud à haut risque tout en ignorant celles à faible risque. 

Ces deux options invite tooregister utilisateurs pourquoi de l’authentification multifacteur Azure première fois qu’ils se connectent après que les spécifications hello allumé. Les deux options fonctionnent également avec hello configurable [paramètres Azure multi-Factor Authentication](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>Activer Azure MFA en modifiant l’état de l’utilisateur

Comptes d’utilisateur dans Azure multi-Factor Authentication ont hello suivant trois états distincts :

| État | Description | Applications affectées (autres que des navigateurs) |
|:---:|:---:|:---:|
| Désactivé |état par défaut de Hello pour un nouvel utilisateur n'inscrit pas Azure multi-Factor Authentication (MFA). |Non |
| Activé |utilisateur de Hello a été inscrit dans Azure MFA, mais n’a pas été inscrit. Elles seront demandées tooregister hello leur prochaine dans que connexion. |Non.  Ils continuent toowork jusqu'à ce que le processus d’inscription de hello est terminée. |
| Appliquée |utilisateur de Hello a été inscrit et terminée le processus d’inscription de hello pour Azure MFA. |Oui.  Les applications requièrent des mots de passe d'application. |

État de l’utilisateur reflète si un administrateur a les inscrit dans Azure MFA, et si elles s’est terminée de processus d’inscription de hello.

Tous les utilisateurs commencent avec l’état *désactivé*. Lorsque vous inscrivez des utilisateurs dans l’authentification multifacteur Azure, leur état devient *activé*. Lorsque les utilisateurs activés se connectent et terminer le processus d’inscription de hello, leur état change également*appliquée*.  

### <a name="view-hello-status-for-a-user"></a>Afficher l’état hello pour un utilisateur

Hello utilisation suivant étapes tooaccess hello page où vous pouvez afficher et gérer des États utilisateur :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.
2. Accédez trop**Azure Active Directory** > **utilisateurs et groupes** > **tous les utilisateurs**.
3. Sélectionnez **Multi-Factor Authentication**.
   ![Sélectionnez Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Une nouvelle page qui affiche les États utilisateur hello, s’ouvre.
   ![État utilisateur pour l’authentification multifacteur - capture d’écran](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>Modifier l’état hello pour un utilisateur

1. Utilisez hello précédant la page users d’étapes tooget toohello l’authentification multifacteur.
2. Rechercher un utilisateur hello que vous souhaitez tooenable pour Azure MFA. Vous devrez peut-être toochange hello vue haut hello. 
   ![Rechercher un utilisateur - capture d’écran](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Vérifiez le nom de tootheir suivant hello boîte.
4. Sur la droite, sous étapes rapides de hello, choisissez **activer** ou **désactiver**.
   ![Activer l’utilisateur sélectionné - capture d’écran](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*Activé* les utilisateurs basculent automatiquement trop*appliquée* quand ils s’inscrivent pour Azure MFA. Vous ne devez pas modifier manuellement hello utilisateur état tooenforced. 

5. Confirmez votre sélection dans la fenêtre contextuelle hello qui s’ouvre. 

Après avoir activé des utilisateurs, vous devez les en avertir par e-mail. Indiquez-leur qu’ils sont demandées tooregister hello leur prochaine dans que connexion. En outre, si votre organisation utilise des applications non-Web qui ne prennent pas en charge l’authentification moderne, ils devez toocreate mots de passe d’application. Vous pouvez également inclure un lien de tooour [guide de l’utilisateur final de l’authentification Multifacteur Azure](./end-user/multi-factor-authentication-end-user.md) toohelp leur prise en main.

### <a name="use-powershell"></a>Utiliser PowerShell
utilisation de l’état de toochange hello utilisateur état [PowerShell Azure AD](/powershell/azure/overview), modifier `$st.State`. Il existe trois états possibles :

* Activé
* Appliquée
* Désactivé  

Ne déplacez pas les utilisateurs directement toohello *appliqué* état. Applications sans navigateur cessera de fonctionner, car l’utilisateur de hello n'a pas fait l’objet d’inscription de l’authentification Multifacteur et obtenu une [mot de passe](multi-factor-authentication-whats-next.md#app-passwords). 

À l’aide de PowerShell d’est une bonne option lorsque vous avez besoin toobulk permettant aux utilisateurs. Créez un script PowerShell qui effectue une itération sur une liste d’utilisateurs et active ces utilisateurs :

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

Voici un exemple :

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>Activer Azure MFA avec une stratégie d’accès conditionnel

L’accès conditionnel est une fonctionnalité payante d’Azure Active Directory qui offre de nombreuses options de configuration. Ces étapes guident monodirectionnelle toocreate une stratégie. Pour plus d’informations, consultez [Accès conditionnel dans Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.
2. Accédez trop**Azure Active Directory** > **accès conditionnel**.
3. Sélectionnez **Nouvelle stratégie**.
4. Sous **Affectations**, sélectionnez **Utilisateurs et groupes**. Hello d’utilisation **Include** et **exclure** onglets toospecify quels utilisateurs et groupes qui est géré par la stratégie de hello.
5. Sous **Affectations**, sélectionnez **Applications cloud**. Choisissez tooinclude **toutes les applications de cloud**.
6. Sous **Contrôles d’accès**, sélectionnez **Accorder**. Choisissez **Exiger une authentification multifacteur**.
7. Activer **activer la stratégie** trop**sur** , puis sélectionnez **enregistrer**.

Hello autres options dans la stratégie d’accès conditionnel hello permettent toospecify exactement lors de la vérification en deux étapes doit être requise. Par exemple, vous pouvez apporter une stratégie qui stipule : lors de sous-traitants tooaccess notre application d’approvisionnement des réseaux non approuvés sur les appareils qui ne sont pas joints au domaine, nécessitent la vérification en deux étapes. 

## <a name="next-steps"></a>Étapes suivantes

- Obtenir des conseils sur hello [meilleures pratiques pour l’accès conditionnel](../active-directory/active-directory-conditional-access-best-practices.md)

- Gérer les paramètres de l’authentification multifacteur pour [vos utilisateurs et leurs appareils](multi-factor-authentication-manage-users-and-devices.md)