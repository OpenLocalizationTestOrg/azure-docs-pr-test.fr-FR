---
title: "Bien démarrer avec Azure Active Directory Domain Services | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)


## <a name="task-3-configure-administrative-group"></a>Tâche 3 : configurer le groupe d’administration
Dans cette tâche de configuration, vous allez créer un groupe d’administration dans votre répertoire Azure AD. Ce groupe d’administration spécial est appelé *AAD DC Administrators*. Membres de ce groupe ont des autorisations d’administration sur les ordinateurs qui appartiennent à un domaine géré de toohello de domaine. Sur les ordinateurs joints à un domaine, ce groupe est ajouté toohello groupe d’administrateurs. En outre, les membres de ce groupe peuvent utiliser Bureau à distance tooconnect à distance toodomain-ordinateurs joints à un.

> [!NOTE]
> Il est inutile des autorisations administrateur de domaine ou administrateur d’entreprise sur un domaine géré hello que vous avez créé à l’aide d’Azure Active Directory Domain Services. Dans des domaines gérés, ces autorisations sont réservées par le service de hello et ne sont pas apportées toousers disponibles au sein de client de hello. Toutefois, vous pouvez utiliser hello spéciaux groupe d’administration créés dans cette tooperform de tâche de configuration certaines opérations privilégiées. Ces opérations comprennent la jonction de domaine toohello des ordinateurs, appartenant toohello groupe d’administration sur les ordinateurs joints au domaine et stratégie de groupe.
>

Assistant de Hello crée automatiquement le groupe d’administration hello dans votre annuaire Azure AD. Ce groupe est appelé « Administrateurs AAD DC ». Si vous disposez d’un groupe portant ce nom dans votre annuaire Azure AD, Assistant de hello sélectionne ce groupe. Vous pouvez configurer l’appartenance au groupe à l’aide de hello **groupe administrateur** page de l’Assistant.

1. appartenance au groupe de tooconfigure, cliquez sur **administrateurs du contrôleur de domaine AAD**.

    ![Configurer l’appartenance au groupe](./media/getting-started/domain-services-blade-admingroup.png)

2. Cliquez sur hello **ajouter des membres** bouton tooadd les utilisateurs de votre groupe d’administrateur Azure AD directory toohello.

3. Lorsque vous avez terminé, cliquez sur **OK** toomove sur toohello **Résumé** page d’Assistant de hello.

4. Sur hello **Résumé** page d’Assistant hello, vérifier les paramètres de configuration hello pour le domaine géré de hello. Vous pouvez revenir en arrière étape tooany des modifications de toomake Assistant hello, si nécessaire. Lorsque vous avez terminé, cliquez sur **OK** toocreate hello gérés nouveau domaine.

    ![Résumé](./media/getting-started/domain-services-blade-summary.png)

5. Vous voyez une notification qui affiche la progression de hello de votre déploiement de Services de domaine Active Directory de Azure. Cliquez sur la notification de hello toosee détaillées de progression pour le déploiement de hello.

    ![Notification - Déploiement en cours](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Approvisionner votre domaine managé
processus de Hello de configuration de votre domaine géré peut prendre tooan heure.

1. Pendant que votre déploiement est en cours d’exécution, vous pouvez rechercher des services de domaine Bonjour **recherche les ressources** zone de recherche. Sélectionnez **les Services de domaine Active Directory de Azure** à partir du résultat de recherche hello. Hello **les Services de domaine Active Directory de Azure** panneau répertorie hello domaine géré qui est en cours d’approvisionnement.

    ![Rechercher le domaine managé en cours d’approvisionnement](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Cliquez sur nom hello hello géré (par exemple, « contoso100.com ») de domaine toosee plus de détails sur le domaine de hello.

    ![Domain Services - État d’approvisionnement](./media/getting-started/domain-services-provisioning-state.png)

3. Hello **vue d’ensemble** onglet affiche ce domaine hello est actuellement en cours d’approvisionnement. Vous ne pouvez pas configurer le domaine géré de hello jusqu'à ce qu’il est entièrement configuré. Cela peut prendre jusqu'à l’heure tooan pour votre toobe domaine géré entièrement configuré.

    ![Services de domaine - onglet vue d’ensemble au cours de l’état d’approvisionnement de hello ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Lorsque le domaine géré de hello est entièrement configuré, hello **vue d’ensemble** onglet affiche l’état domaine hello **en cours d’exécution**.

    ![Domain Services - Onglet Vue d’ensemble une fois la configuration terminée](./media/getting-started/domain-services-provisioned.png)

5. Sur hello **propriétés** onglet, vous voyez deux adresses IP pour le domaine contrôleurs sont disponibles pour les réseaux virtuels hello.

    ![Domain Services - Onglet Propriétés après un approvisionnement complet](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Étape suivante
[Tâche 4 : mettre à jour les paramètres DNS hello hello réseau virtuel Azure](active-directory-ds-getting-started-dns.md)
