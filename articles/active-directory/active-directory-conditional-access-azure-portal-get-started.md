---
title: "aaaGet a démarré avec un accès conditionnel dans Azure Active Directory | Documents Microsoft"
description: "Testez l’accès conditionnel à l’aide d’une condition d’emplacement."
services: active-directory
keywords: "tooapps d’accès conditionnel, l’accès conditionnel avec Azure AD, sécuriser l’accès aux ressources toocompany, les stratégies d’accès conditionnel"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Bien démarrer avec l’accès conditionnel dans Azure Active Directory

Accès conditionnel est une fonctionnalité d’Azure Active Directory qui permet des conditions toodefine vous sous lequel les utilisateurs autorisés peuvent accéder à vos applications. 

Cette rubrique fournit des instructions pour tester un accès conditionnel en fonction d’une condition d’emplacement dans votre environnement.  


## <a name="scenario-description"></a>Description du scénario

Une condition courante dans de nombreuses organisations est tooonly exiger l’authentification multifacteur pour tooapps d’accès qui n’est pas effectuée à partir de l’intranet d’entreprise de hello. Azure Active Directory vous permet d’atteindre cet objectif facilement grâce à une stratégie d’accès conditionnel basée sur l’emplacement. Cette rubrique fournit des instructions détaillées pour configurer une stratégie de ce type. Hello tire parti de la stratégie [des adresses IP approuvées](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish entre les tentatives d’accès effectuées à partir de hello d’entreprise de l’intranet et tous les autres emplacements.


## <a name="prerequisites"></a>Composants requis

Hello scénario décrit dans cette rubrique part du principe que vous êtes familiarisé avec les concepts de hello décrites dans [accès conditionnel Azure Active Directory](active-directory-conditional-access-azure-portal.md).

tootest ce scénario, vous devez :

- Créer un utilisateur de test 

- Attribuer un utilisateur de test de toohello licence Azure AD Premium

- Configurer une application gérée et affecter votre tooit d’utilisateur de test

- Configurer les adresses IP approuvées

Pour plus d’informations sur les adresses IP approuvées, consultez [Adresses IP approuvées](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="policy-configuration-steps"></a>Configuration de la stratégie

**tooconfigure votre stratégie d’accès conditionnel, faire :**

1. Bonjour portail Azure, sur hello barre de navigation gauche, cliquez sur **Azure Active Directory**. 

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. Sur hello **Azure Active Directory** panneau, Bonjour **gérer** , cliquez sur **accès conditionnel**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. Sur hello **accès conditionnel** panneau, tooopen hello **nouveau** lame, dans la barre d’outils hello en haut de hello, cliquez sur **ajouter**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. Sur hello **nouveau** panneau, Bonjour **nom** zone de texte, tapez un nom pour votre stratégie.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. Bonjour **affectation** , cliquez sur **utilisateurs et groupes**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. Sur hello **utilisateurs et groupes** panneau, effectuer hello comme suit :

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. Cliquez sur **Sélectionner des utilisateurs et des groupes**.

    b. Cliquez sur **Sélectionner**.

    c. Sur hello **sélectionnez** panneau, sélectionnez votre utilisateur test, puis cliquez sur **sélectionnez**.

    d. Sur hello **utilisateurs et groupes** panneau, cliquez sur **fait**.

7. Sur hello **nouveau** panneau, tooopen hello **applications Cloud** panneau, Bonjour **affectation** , cliquez sur **applications Cloud**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. Sur hello **applications Cloud** panneau, effectuer hello comme suit :

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. Cliquez sur **Sélectionner les applications**.

    b. Cliquez sur **Sélectionner**.

    c. Sur hello **sélectionnez** panneau, sélectionnez votre application cloud, puis cliquez sur **sélectionnez**.

    d. Sur hello **applications Cloud** panneau, cliquez sur **fait**.

9. Sur hello **nouveau** panneau, tooopen hello **Conditions** panneau, Bonjour **affectation** , cliquez sur **Conditions**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. Sur hello **Conditions** panneau, tooopen hello **emplacements** panneau, cliquez sur **emplacements**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. Sur hello **emplacements** panneau, effectuer hello comme suit :

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. Sous **Configurer**, cliquez sur **Oui**.

    b. Sous **Inclure**, cliquez sur **All locations (Tous les emplacements)**.

    c. Cliquez sur **Exclure**, puis sur **All trusted IPs (Toutes les adresses IP approuvées)**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. Cliquez sur **Done**.

12. Sur hello **Conditions** panneau, cliquez sur **fait**.

13. Sur hello **nouveau** panneau, tooopen hello **Grant** panneau, Bonjour **contrôles** , cliquez sur **Grant**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. Sur hello **Grant** panneau, effectuer hello comme suit :

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. Sélectionnez **Exiger une authentification multifacteur**.

    b. Cliquez sur **Sélectionner**.

15. Sur hello **nouveau** panneau, sous **activer la stratégie**, cliquez sur **sur**.

    ![Accès conditionnel](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. Sur hello **nouveau** panneau, cliquez sur **créer**.


## <a name="testing-hello-policy"></a>Test de la stratégie de hello

tootest votre stratégie, vous devez accéder à votre application à partir d’un appareil qui : 

1. dont l’adresse IP figure parmi les adresses IP approuvées que vous avez configurées ; 

1. dont l’adresse IP ne figure pas parmi les adresses IP approuvées que vous avez configurées.

L’authentification multifacteur ne doit être requise que si la tentative de connexion émane d’un appareil qui ne figure pas parmi les adresses IP approuvées que vous avez configurées. 


## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez que toolearn plus d’informations sur l’accès conditionnel, consultez [accès conditionnel Azure Active Directory](active-directory-conditional-access-azure-portal.md).

