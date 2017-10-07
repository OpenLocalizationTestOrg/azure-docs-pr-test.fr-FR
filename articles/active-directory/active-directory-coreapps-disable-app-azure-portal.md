---
title: "aaaDisable connexions utilisateur pour une application d’entreprise dans Active Directory de Azure | Documents Microsoft"
description: "Comment toodisable une application d’entreprise afin qu’aucun utilisateur ne peut se connecter tooit dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Désactiver les connexions utilisateur pour une application d’entreprise dans Azure Active Directory
Il est facile toodisable une application d’entreprise afin qu’aucun utilisateur ne peut se connecter tooit dans Azure Active Directory (Azure AD). Vous devez disposer des applications d’entreprise hello toomanage hello les autorisations appropriées, et vous devez être administrateur général pour le répertoire de hello.

## <a name="how-do-i-disable-user-sign-ins"></a>Comment désactiver les connexions des utilisateurs ?
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **Azure Active Directory** dans hello de zone de texte, puis sélectionnez **entrée**.
3. Sur hello **Azure Active Directory** -  ***nom_répertoire*** blade (autrement dit, hello Azure AD panneau pour le répertoire hello vous gérez), sélectionnez **desapplicationsd’entreprise**.

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. Sur hello **des applications d’entreprise** panneau, sélectionnez **toutes les applications**. Vous consultez une liste d’applications hello que vous pouvez gérer.
5. Sur hello **des applications d’entreprise - toutes les applications** panneau, sélectionnez une application.
6. Sur hello ***appname*** blade (autrement dit, hello blade avec nom hello d’application sélectionné hello dans le titre de hello), sélectionnez **propriétés**.

    ![En sélectionnant hello toutes les commandes d’applications](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. Sur hello ***appname*** - **propriétés** panneau, sélectionnez **non** pour **activée pour les utilisateurs de toosign ?**.
8. Sélectionnez hello **enregistrer** commande.

## <a name="next-steps"></a>Étapes suivantes
* [Voir tous mes groupes](active-directory-groups-view-azure-portal.md)
* [Affecter une application d’entreprise tooan utilisateur ou un groupe](active-directory-coreapps-assign-user-azure-portal.md)
* [Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans la version préliminaire d’Azure Active Directory](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Modifier le nom hello ou un logo d’une application d’entreprise](active-directory-coreapps-change-app-logo-user-azure-portal.md)
