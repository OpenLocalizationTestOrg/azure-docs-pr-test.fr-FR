---
title: "aaaHow tooactivate ou désactiver un rôle | Documents Microsoft"
description: "Découvrez comment tooactivate rôles privilégiés identités avec application d’Azure Privileged Identity Management hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>Comment tooactivate ou désactiver les rôles dans Azure AD Privileged Identity Management
Azure Active Directory (AD) Privileged Identity Management simplifie comment gérer les entreprises tooresources accès privilégié dans Azure AD et autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.  

Si vous avez été éligible pour un rôle d’administrateur, ce qui signifie que vous pouvez activer ce rôle lorsque vous avez besoin d’actions de tooperform privilégié. Par exemple, si vous gérez occasionnellement des fonctionnalités d’Office 365, les administrateurs de rôle privilégié de votre organisation peuvent ne pas vous attribuer le rôle d’administrateur général permanent, étant donné que ce rôle affecte également les autres services. Au lieu de cela, ils peuvent vous attribuer des rôles Azure AD tels qu’administrateur Exchange Online. Vous pouvez demander tooactivate ce rôle lorsque vous avez besoin de leurs privilèges, et vous aurez contrôle d’administration pour une période prédéterminée.

Cet article est pour les administrateurs qui ont besoin de tooactivate leur rôle dans Azure AD Privileged Identity Management (PIM). Il vous guide dans hello étapes tooactivate un rôle lorsque vous devez disposer des autorisations de hello et désactivez le rôle de hello lorsque vous avez terminé. En outre, les administrateurs de rôle privilégié peuvent demander l’approbation tooactivate un rôle (version préliminaire). Pour en savoir plus sur les flux de travail d’approbation PIM, consultez [cet article](./privileged-identity-management/azure-ad-pim-approval-workflow.md).

## <a name="add-hello-privileged-identity-management-application"></a>Ajouter une application de Privileged Identity Management hello
Utiliser l’application de hello Azure AD Privileged Identity Management Bonjour [portail Azure](https://portal.azure.com/) toorequest d’activation de rôle, même si vous allez toooperate dans un autre portail ou de PowerShell. Si vous n’avez pas application Azure AD Privileged Identity Management de hello sur votre portail Azure, suivez ces tooget étapes a démarré.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez votre nom d’utilisateur dans hello coin supérieur droit de hello portail Azure et répertoire hello sélectionnez où vous allez être fonctionne.
3. Sélectionnez **davantage de services** et utiliser toosearch de zone de texte de filtre hello pour **Azure AD Privileged Identity Management**.
4. Vérifiez **code confidentiel toodashboard** puis cliquez sur **créer**. Hello application de Privileged Identity Management s’ouvre.

## <a name="activate-a-role"></a>Activer un rôle
Lorsque vous devez tootake sur un rôle, vous pouvez demander l’activation en sélectionnant hello **mes rôles** option de navigation dans l’application de hello Azure AD Privileged Identity Management d’une colonne de navigation de gauche.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et sélectionnez hello Azure AD Privileged Identity Management mosaïque.
2. Sélectionnez **Mes rôles**. Une liste de vos rôles éligibles affectées apparaissent dans hello en hello haut hello de regroupement.
3. Sélectionnez un rôle tooactivate.
4. Sélectionnez **Activer**. Hello **demander l’activation du rôle** panneau s’affiche.
5. Certains rôles nécessitent l’authentification multifacteur (MFA) avant d’activer le rôle de hello. Vous ne devez tooauthenticate une fois par session.
   
    ![Vérification multifacteur avant activation du rôle : capture d’écran][2]
6. Entrez le motif hello pour la demande d’activation de hello dans le champ de texte hello.  Certains rôles nécessitent toosupply un numéro de ticket d’incident.
7. Sélectionnez **OK**.  Si le rôle de hello ne requiert pas d’approbation, il est activé et rôle de hello s’affiche dans la liste hello des rôles actifs (directement sous la liste hello d’attributions de rôle éligibles). Si hello [rôle requiert une approbation](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, une notification toast s’affiche brièvement dans hello coin supérieur droit de votre navigateur pour vous informer de demande de hello est en attente d’approbation.

    ![Notification de demande en attente - capture d’écran][3]

## <a name="deactivate-a-role"></a>Désactiver un rôle
Une fois qu’un rôle a été activé, il se désactive automatiquement quand sa limite de temps (durée éligible) est atteinte.

Si vous effectuer vos tâches d’administration au début, vous pouvez également désactiver un rôle manuellement dans hello application Azure AD Privileged Identity Management.  Sélectionnez **mes rôles**, choisissez le rôle hello terminé à l’aide de hello **attributions de rôles Active** regroupement, puis sélectionnez **Deactivate**.  

## <a name="cancel-a-pending-request"></a>Annuler une demande en attente
Événement de hello vous n’avez pas besoin d’activation d’un rôle qui nécessite l’approbation, vous pouvez annuler une demande en attente à tout moment. Sélectionnez simplement hello **mes rôles** option de navigation dans l’application de hello Azure AD Privileged Identity Management d’une colonne de navigation de gauche.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et sélectionnez hello Azure AD Privileged Identity Management mosaïque.
2. Sélectionnez **Mes rôles**. Une liste de vos rôles éligibles affectées apparaissent dans hello en hello haut hello de regroupement.
3. Sélectionnez un rôle
4. Sélectionnez hello **l’Activation est en attente d’approbation** bannière sur le panneau de détails de l’activation de rôle hello.
5. Sélectionnez **Annuler** haut hello hello **en attente d’approbation** panneau.

   ![Capture d’écran d’annulation de demande en attente][4]

## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez en savoir plus sur Azure AD Privileged Identity Management, hello liens suivants contiennent plus d’informations.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
