---
title: "Azure AD Connect : Étapes suivantes et comment toomanage Azure AD Connect | Documents Microsoft"
description: "Découvrez comment tooextend hello configuration par défaut et les tâches opérationnelles pour Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>Étapes suivantes et comment toomanage Azure AD Connect
Procédez hello opérationnels dans cette toomeet de Connect de Azure Active Directory (Azure AD) de l’article toocustomize besoins et exigences de votre organisation.  

## <a name="add-additional-sync-admins"></a>Ajout d’administrateurs de synchronisation supplémentaires
Par défaut, le seul utilisateur hello hello installation et les administrateurs locaux sont moteur de synchronisation en mesure de toomanage hello installé. Pour tooaccess de personnes supplémentaires toobe en mesure de gérer le moteur de synchronisation hello, recherchez le groupe hello nommé ADSyncAdmins sur le serveur local de hello et ajoutez-les toothis groupe.

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>Affecter des utilisateurs Active Directory Premium et Enterprise Mobility Suite tooAzure de licences
Maintenant que vos utilisateurs ont été synchronisés toohello cloud, vous devez tooassign les une licence afin qu’ils peuvent commencer avec les applications de cloud telles qu’Office 365.

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>tooassign une Azure AD Premium ou la licence de la Suite Enterprise Mobility

1. Se connecter toohello portail Azure en tant qu’administrateur.
2. Sur hello gauche, sélectionnez **Active Directory**.
3. Sur hello **Active Directory** page, double-cliquez sur le répertoire hello ayant hello utilisateurs tooset des.
4. En hello haut hello active, sélectionnez **licences**.
5. Sur hello **licences** page, sélectionnez **Active Directory Premium** ou **Enterprise Mobility Suite**, puis cliquez sur **affecter**.
6. Dans la boîte de dialogue hello, sélectionnez les utilisateurs de hello vous souhaitez tooassign licences, puis cliquez sur hello coche icône toosave hello change.

## <a name="verify-hello-scheduled-synchronization-task"></a>Vérifier la tâche de synchronisation planifiée hello
Utilisez hello toocheck portail Azure hello statut d’une synchronisation.

### <a name="tooverify-hello-scheduled-synchronization-task"></a>tâche de synchronisation planifiée hello tooverify
1. Se connecter toohello portail Azure en tant qu’administrateur.
2. Sur hello gauche, sélectionnez **Active Directory**.
3. Sur hello **Active Directory** page, double-cliquez sur le répertoire hello ayant hello utilisateurs tooset des.
4. En hello haut hello active, sélectionnez **intégration d’annuaire**.
5. Sous **intégration avec Active Directory local**, hello de Remarque dernière heure de synchronisation.

<center>![Heure de synchronisation d’annuaires](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>Lancement d’une tâche de synchronisation planifiée
Si vous avez besoin d’une tâche de synchronisation de toorun, faire cela en réexécutant via l’Assistant d’Azure AD Connect hello.  Vous devez tooprovide vos informations d’identification Azure AD.  Dans l’Assistant de hello, sélectionnez hello **personnaliser les options de synchronisation** de tâches, puis cliquez sur **suivant** toomove via l’Assistant de hello. À la fin de hello, assurez-vous que hello **démarrer le processus de synchronisation hello dès la fin de la configuration initiale de hello** est activée.

<center>![Démarrage de la synchronisation](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

Pour plus d’informations sur la synchronisation de Connect hello Azure AD du planificateur, consultez [Azure Scheduler de connexion AD](active-directory-aadconnectsync-feature-scheduler.md).

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Tâches supplémentaires disponibles dans Azure AD Connect
Après l’installation initiale d’Azure AD Connect, vous pouvez toujours démarrer hello Assistant à nouveau à partir de hello Azure AD Connect start page ou bureau d’un raccourci.  Vous remarquerez que via l’Assistant de hello redevenir fournit de nouvelles options sous forme de hello des tâches supplémentaires.  

Hello tableau suivant fournit un résumé de ces tâches et une brève description de chaque tâche.

![Liste des tâches supplémentaires](./media/active-directory-aadconnect-whats-next/addtasks.png)

| Tâche supplémentaire | Description |
| --- | --- |
| **Scénario de vue hello sélectionné** |Afficher votre solution Azure AD Connect actuelle.  Cela inclut les paramètres généraux, les répertoires synchronisés et les paramètres de synchronisation. |
| **Personnalisation des options de synchronisation** |Modifier la configuration actuelle du hello comme l’ajout de la configuration de toohello de forêts Active Directory supplémentaire ou l’activation des options de synchronisation tels que l’utilisateur, groupe, appareil ou écriture différée de mot de passe. |
| **Activation du mode intermédiaire** |Informations sur la phase qui ne sont pas synchronisées immédiatement et ne sont pas exporté tooAzure AD ou sur site Active Directory.  Avec cette fonctionnalité, vous pouvez afficher un aperçu des synchronisations hello avant qu’ils surviennent. |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [l’intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
