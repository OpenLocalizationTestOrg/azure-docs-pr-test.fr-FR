---
title: aaaConfigure Azure AD Privileged Identity Management | Documents Microsoft
description: "Une rubrique qui explique ce qu’est Azure AD Privileged Identity Management et comment toouse PIM tooimprove la sécurité de votre cloud."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Qu’est-ce qu’Azure AD Privileged Identity Management ?
Avec Azure Active Directory (AD) Privileged Identity Management, vous pouvez gérer, contrôler et surveiller l’accès au sein de votre organisation. Cela inclut tooresources d’accès dans Azure AD et d’autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.  

> [!NOTE]
> Privileged Identity Management est disponible tooyour toute organisation lors de la licence de vos administrateurs avec l’édition hello Premium P2 d’Azure Active Directory. Pour plus d’informations, consultez la page [Éditions d’Azure Active Directory](active-directory-editions.md).

Organisations souhaitent plusieurs hello toominimize personnes ont accès toosecure informations ou des ressources, car qui réduit le risque de hello d’un utilisateur malveillant que l’accès de mise en route. Toutefois, les utilisateurs doivent toujours toocarry opérations nécessitant des privilèges dans les applications Azure, Office 365 ou SaaS. Les organisations doivent offrir un accès privilégié aux utilisateurs dans Azure AD sans avoir à surveiller ce que font les utilisateurs avec leurs privilèges d’administrateur. Azure AD Privileged Identity Management permet tooresolve ce risque.  

Azure AD Privileged Identity Management vous aide à :  

* Identifier les utilisateurs qui ont un rôle d’administrateur dans Azure AD
* Activer à la demande « juste à temps » d’un accès administratif tooMicrosoft Online Services comme Office 365 et Intune
* Obtenir des rapports sur l'historique des accès administrateur et sur les modifications apportées aux affectations de l'administrateur
* Recevoir des alertes sur le rôle privilégié de tooa d’accès
* Exiger l’approbation tooactivate (version préliminaire)

Azure AD Privileged Identity Management peut gérer les rôles d’organisation de hello intégrée Azure AD, notamment (liste non exhaustive) :  

* Administrateur général
* Administrateur de facturation
* Administrateur de services  
* Administrateur d'utilisateurs
* Administrateur de mots de passe

## <a name="just-in-time-administrator-access"></a>Administrateur des accès immédiats
Historiquement, vous pouvez affecter un rôle d’administrateur tooan utilisateur via le portail Azure classic de hello ou Windows PowerShell. Par conséquent, cet utilisateur devient un **administrateur permanent**, toujours active dans le rôle de hello attribué. Azure AD Privileged Identity Management introduit le concept de hello d’un **admin éligible**. Les administrateurs éligibles doivent être des utilisateurs qui nécessitent un accès privilégié de temps à autres, mais pas tous les jours. rôle de Hello est inactif jusqu'à ce que l’utilisateur de hello requiert un accès, puis de terminer un processus d’activation et qu’il devienne un administrateur actif d’une période prédéterminée.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Activer Privileged Identity Management pour votre répertoire
Vous pouvez démarrer à l’aide d’Azure AD Privileged Identity Management Bonjour [portail Azure](https://portal.azure.com/).

> [!NOTE]
> Vous devez être un administrateur global avec un compte professionnel (par exemple, @yourdomain.com), pas un compte Microsoft (par exemple, @outlook.com), tooenable Azure AD Privileged Identity Management pour un répertoire.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) en tant qu’administrateur général de votre annuaire.
2. Si votre organisation a plusieurs répertoires, sélectionnez votre nom d’utilisateur dans le coin supérieur droit hello Hello portail Azure. Sélectionnez le répertoire hello où vous allez utiliser Azure AD Privileged Identity Management.
3. Sélectionnez **davantage de services** et utiliser toosearch de zone de texte de filtre hello pour **Azure AD Privileged Identity Management**.
4. Vérifiez **code confidentiel toodashboard** puis cliquez sur **créer**. Hello application de Privileged Identity Management s’ouvre.

Si vous êtes hello première personne toouse Azure AD Privileged Identity Management dans votre annuaire, puis hello [Assistant sécurité](active-directory-privileged-identity-management-security-wizard.md) vous guide à travers hello attribution initiale. Une fois que vous devenez automatiquement hello tout d’abord **administrateur de sécurité** et **administrateur du rôle privilégié** du répertoire de hello.

Seul un administrateur de rôle privilégié peut gérer l’accès des autres administrateurs. Vous pouvez [donnent autres toomanage de capacité hello utilisateurs PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Tableau de bord d’administration de Privileged Identity Management
Azure AD Privileged Identity Manager fournit un tableau de bord d’administration qui contient des informations importantes telles que :

* Alertes qui désignent la sécurité de tooimprove d’opportunités
* nombre de Hello d’utilisateurs ayant le rôle de privilège tooeach  
* nombre de Hello d’administrateurs éligibles et permanents
* Un graphique des activations de rôle privilégié dans votre annuaire

![Capture d’écran du tableau de bord PIM][2]

## <a name="privileged-role-management"></a>Gestion des rôles privilégiés
Avec Azure AD Privileged Identity Management, vous pouvez gérer les administrateurs de hello en ajoutant ou supprimant le rôle de tooeach administrateurs permanents ou éligibles.

![Capture d’écran d’ajout et de suppression d’administrateurs dans PIM][3]

## <a name="configure-hello-role-activation-settings"></a>Configurer les paramètres de l’activation de rôle hello
À l’aide de hello [paramètres de rôle](active-directory-privileged-identity-management-how-to-change-default-settings.md) vous pouvez configurer les propriétés de d’activation de rôle éligibles hello, y compris :

* Durée Hello de période d’activation de rôle hello
* notification de l’activation du rôle Hello
* informations de Hello un utilisateur doivent tooprovide pendant le processus d’activation de rôle hello
* Un numéro d’incident ou ticket de service
* [Exigences relatives au flux de travail d’approbation - préversion](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![Capture d’écran de l’activation d’administrateur dans les paramètres PIM][4]

Notez que dans l’image de hello, hello boutons pour **multi-Factor Authentication** sont désactivés. Avec certains rôles dotés de privilèges élevés, l’authentification multifacteur est requise pour garantir une protection renforcée.

## <a name="role-activation"></a>Activation d’un rôle
trop[activer un rôle](active-directory-privileged-identity-management-how-to-activate-role.md), un administrateur éligible demande un temps « activation » pour le rôle de hello. l’activation de Hello peut être demandée à l’aide de hello **activer mon rôle** option dans Azure AD Privileged Identity Management.

Un administrateur qui veut tooactivate un rôle doit tooinitialize Azure AD Privileged Identity Management Bonjour portail Azure.

L’activation de rôles est personnalisable. Dans les paramètres de PIM hello, vous pouvez déterminer la longueur de l’activation de hello et quelles informations hello a besoin rôle de hello tooprovide tooactivate hello.

![Capture d’écran de demande d’activation de rôle d’administrateur dans PIM][5]

## <a name="review-role-activity"></a>Passer en revue les activités de rôle
Il existe deux façons tootrack comment vos employés et les administrateurs utilisent privilégié des rôles. à l’aide de la première option à Hello [historique d’audit des rôles d’annuaire](active-directory-privileged-identity-management-how-to-use-audit-log.md). historique des audits Hello consigne le suivi des modifications dans les attributions de rôle privilégié et l’historique de l’activation de rôle.

![Capture d’écran de l’historique d’activation dans PIM][6]

deuxième option Hello est tooset des regular [accès révisions](active-directory-privileged-identity-management-how-to-start-security-review.md). Ces évaluations d’accès peuvent être effectuées par et attribuées réviseur (par exemple, un gestionnaire de l’équipe) ou les employés hello trouverez eux-mêmes. Il s’agit de hello meilleure manière toomonitor qui doit toujours avoir accès, et qui n’effectue plus.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Azure AD PIM à l’expiration de l’abonnement
Tooreaching préalable général disponibilité Azure AD PIM était en version préliminaire et il n’y avait aucune licence vérifie un toopreview locataire Azure AD PIM.  Maintenant que Azure AD PIM a atteint la disponibilité générale, les licences d’évaluation ou payants doivent être assignés administrateurs toohello de hello toocontinue de client à l’aide de PIM.  Si votre organisation ne pas acheté d’Azure AD Premium P2 ou votre version d’évaluation expire, principalement toutes les fonctionnalités d’Azure AD PIM hello ne seront plus disponibles dans votre client.  Vous pouvez en savoir plus Bonjour [conditions requises des abonnements Azure AD PIM](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
