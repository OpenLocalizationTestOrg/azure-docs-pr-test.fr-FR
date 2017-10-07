---
title: "aaaGet main d’Azure AD Privileged Identity Management | Documents Microsoft"
description: "Découvrez comment toomanage privilégié identités avec application d’Azure Active Directory Privileged Identity Management hello dans le portail Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Commencer à utiliser Azure AD Privileged Identity Management
Avec Azure Active Directory (AD) Privileged Identity Management, vous pouvez gérer, contrôler et surveiller l’accès au sein de votre organisation. Cette étendue inclut tooresources d’accès dans Azure AD et d’autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.

Cet article vous indique comment tooadd hello tooyour d’application Azure AD PIM tableau de bord de portail Azure.

## <a name="add-hello-privileged-identity-management-application"></a>Ajouter une application de Privileged Identity Management hello
Avant d’utiliser Azure AD Privileged Identity Management, vous devez tooadd hello application tooyour tableau de bord de portail Azure.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) en tant qu’administrateur général de votre annuaire.
2. Si votre organisation a plusieurs répertoires, sélectionnez votre nom d’utilisateur dans le coin supérieur droit hello Hello portail Azure. Sélectionnez le répertoire hello où vous souhaitez toouse PIM.
3. Sélectionnez **davantage de services** et utiliser toosearch de zone de texte de filtre hello pour **Azure AD Privileged Identity Management**.
4. Vérifiez **code confidentiel toodashboard** puis cliquez sur **créer**. Hello application de Privileged Identity Management s’ouvre.

Si vous êtes hello première personne toouse Azure AD Privileged Identity Management dans votre annuaire, vous êtes automatiquement affecté hello **administrateur de sécurité** et **administrateur du rôle privilégié** rôles dans le répertoire de hello. Seuls les administrateurs de rôle privilégié peuvent gérer les attributions de rôles d’utilisateurs. En outre, vous pouvez choisir toorun hello [Assistant de sécurité.](active-directory-privileged-identity-management-security-wizard.md) qui vous guide à travers hello initiale détection et affectation.

## <a name="navigate-tooyour-tasks"></a>Accédez tooyour tâches
Une fois Azure AD Privileged Identity Management est configuré, vous voyez Panneau de navigation hello lorsque vous ouvrez l’application hello. Utilisez cette tooaccomplish panneau vos tâches de gestion d’identité.

![Tâches de niveau supérieur pour PIM - capture d’écran](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **Mes rôles** vous amène tooa la liste des rôles qui sont attribués tooyou. C’est dans cette section que vous activez tous les rôles auxquels vous êtes éligible.
* **Approuver des demandes (préversion)** affiche la liste des demandes d’activation en attente effectuées par les utilisateurs dans votre annuaire. [En savoir plus.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **En attente de demandes (version préliminaire)** affiche tout tooactivate toohave apportée de demandes en cours.
* **Examinez l’accès** prend vous tooany en attente d’accès révisions que vous avez besoin de toocomplete, si vous relisez des accès pour vous-même ou quelqu'un d’autre.
* **Les rôles d’annuaire Azure AD** situé sous hello 'Gérer' section est de tableau de bord hello pour les attributions de rôle privilégié administrateurs toomanage, modifier les paramètres de l’activation de rôle, début accès révisions et bien plus encore. options de Hello dans ce tableau de bord sont désactivées pour toute personne qui n’est pas un administrateur de rôle privilégié.

## <a name="next-steps"></a>Étapes suivantes
Hello [vue d’ensemble d’Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) inclut plus d’informations sur comment vous pouvez gérer l’accès d’administration dans votre organisation.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
