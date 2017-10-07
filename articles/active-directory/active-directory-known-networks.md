---
title: "Réseaux aaaKnown Bonjour portail classique Azure | Documents Microsoft"
description: "En configurant les réseaux connus, vous évite d’avoir des adresses IP appartenant à votre organisation incluse dans hello connexions depuis plusieurs zones géographiques et des connexions à partir d’adresses IP avec les rapports d’activité suspecte."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>Réseaux connus

> [!div class="op_single_selector"]
> * [portail Azure Classic](active-directory-known-networks.md)
> * [Portail Azure](active-directory-known-networks-azure-portal.md)
> 
> 


Vous pouvez utiliser l’accès Azure Active Directory et l’utilisation des rapports toogain visibilité intégrité de hello et la sécurité de répertoire de votre organisation. Avec cette information, un administrateur d’annuaire peut déterminer plus précisément où peut se trouver des risques de sécurité afin qu’ils peuvent planifier en conséquence toomitigate ces risques.

Il est possible que hello »*connexions depuis plusieurs zones géographiques*« et »*connexions à partir d’adresses IP avec une activité suspecte*« rapports signaler de manière incorrecte les adresses IP qui sont en réalité détenus par votre organisation. 

Cela peut, par exemple, se produire dans les cas suivants : 

* Un utilisateur de votre bureau de Boston s’est connecté à distance tooyour centre de données dans les déclencheurs de San Francisco hello les rapports « Connexions depuis plusieurs zones géographiques » 
* Un utilisateur de votre organisation tente toosign sur plusieurs fois avec un hello de déclencheurs de mot de passe incorrect les rapports « Connexions à partir d’adresses IP avec une activité suspecte » 

tooprevent ces cas de sécurité trompeuse générant des rapports, vous devez ajouter les connus adresse toohello liste des plages IP de l’adresse IP publique de votre organisation.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>plages d’adresse IP publique de votre organisation tooadd, effectuer hello comme suit :

1. Authentification toohello [portail de gestion Azure](https://manage.windowsazure.com).

2. Dans le volet gauche de hello, cliquez sur **Active Directory**. 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-01.png)

3. Bonjour **répertoire** , sélectionnez votre annuaire.

4. Dans le menu hello haut de hello, cliquez sur **configurer**. 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-02.png)

5. Sur l’onglet configurer de hello, accédez trop**vos plages d’adresses IP publiques organisations** 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-03.png)

6. Cliquez sur **Ajouter des plages d'adresses IP connues**.

7. Ajoutez vos plages d’adresses dans la boîte de dialogue hello qui s’affiche, puis cliquez sur la coche hello lorsque vous avez terminé. 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-04.png)

**Ressources supplémentaires :**

* [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md)
* [Connexions à partir d’adresses IP affichant une activité suspecte](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Connexions depuis plusieurs zones géographiques](active-directory-reporting-sign-ins-from-multiple-geographies.md)

