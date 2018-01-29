---
title: "Didacticiel : Configuration de LinkedIn Learning pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner et déprovisionner automatiquement des comptes d’utilisateur sur LinkedIn Learning."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: mtillman
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 9b07417fbb094cdc285e00be3c48f9af0a38601d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-configuring-linkedin-learning-for-automatic-user-provisioning"></a>Didacticiel : Configuration de LinkedIn Learning pour l’approvisionnement automatique d’utilisateurs


L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans LinkedIn Learning et Azure AD pour approvisionner et déprovisionner automatiquement des comptes d’utilisateur d’Azure AD sur LinkedIn Learning. 

## <a name="prerequisites"></a>Composants requis

Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :

*   Un client Azure Active Directory
*   Un locataire LinkedIn Learning 
*   Un compte d’administrateur dans LinkedIn Learning ayant accès au Centre des comptes LinkedIn

> [!NOTE]
> Azure Active Directory s’intègre à LinkedIn Learning à l’aide du protocole [SCIM](http://www.simplecloud.info/).

## <a name="assigning-users-to-linkedin-learning"></a>Assignation d’utilisateurs à LinkedIn Learning

Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées. Dans le cadre de l’approvisionnement automatique de comptes d’utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés. 

Avant de configurer et d’activer le service d’approvisionnement, vous devrez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à LinkedIn Learning. Une fois que vous avez choisi, vous pouvez assigner ces utilisateurs à LinkedIn Learning en suivant les instructions fournies ici :

[Affecter un utilisateur ou un groupe à une application d’entreprise](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-learning"></a>Conseils importants pour l’assignation d’utilisateurs à LinkedIn Learning

*   Il est recommandé d’assigner un seul utilisateur Azure AD à LinkedIn Learning pour tester la configuration de l’approvisionnement. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Quand vous assignez un utilisateur à LinkedIn Learning, vous devez sélectionner le rôle **Utilisateur** dans la boîte de dialogue d’assignation. Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.


## <a name="configuring-user-provisioning-to-linkedin-learning"></a>Configuration de l’approvisionnement des utilisateurs sur LinkedIn Learning

Cette section vous guide pour connecter votre instance d’Azure AD à l’API d’approvisionnement de comptes d’utilisateur SCIM de LinkedIn Learning et configurer le service d’approvisionnement pour créer, mettre à jour et désactiver des comptes d’utilisateur assignés dans LinkedIn Learning en fonction des assignations d’utilisateurs et de groupes dans Azure AD.

> [!TIP]
> Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour LinkedIn Learning en suivant les instructions fournies dans le [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent.


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-learning-in-azure-ad"></a>Pour configurer l’approvisionnement automatique de comptes d’utilisateur sur LinkedIn Learning dans Azure AD :


La première étape consiste à récupérer votre jeton d’accès LinkedIn. Si vous êtes administrateur d’entreprise, vous pouvez approvisionner vous-même un jeton d’accès. Dans le Centre des comptes, accédez à **Paramètres &gt; Paramètres globaux**, puis ouvrez le panneau de configuration **SCIM**.

> [!NOTE]
> Si vous ouvrez le Centre des comptes directement plutôt qu’en passant par un lien, vous pouvez y accéder en effectuant les étapes suivantes.

1)  Connectez-vous au Centre des comptes.

2)  Sélectionnez **Administrateur &gt; Paramètres d’administration**.

3)  Cliquez sur **Intégrations avancées** dans la barre latérale gauche. Vous êtes redirigé vers le Centre des comptes.

4)  Cliquez sur **+ Ajouter une nouvelle configuration SCIM**, puis suivez la procédure en remplissant chaque champ.

> Si l’affectation automatique de licences n’est pas activée, cela signifie que seules les données utilisateur sont synchronisées.

![Approvisionnement LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_1.PNG)

> Quand l’affectation automatique de licences est activée, vous devez noter l’instance d’application et le type de licence. Les licences sont toutes affectées sur le principe du « premier arrivé, premier servi ».

![Approvisionnement LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_2.PNG)

5)  Cliquez sur **Générer un jeton**. Un jeton d’accès doit s’afficher sous le champ **Jeton d’accès**.

6)  Enregistrez votre jeton d’accès dans votre Presse-papiers ou votre ordinateur avant de quitter la page.

7) Ensuite, connectez-vous au [portail Azure](https://portal.azure.com), puis accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.

8) Si vous avez déjà configuré LinkedIn Learning pour l’authentification unique, recherchez votre instance de LinkedIn Learning à l’aide du champ de recherche. Sinon, sélectionnez **Ajouter**, puis recherchez **LinkedIn Learning** dans la galerie d’applications. Sélectionnez LinkedIn Learning dans les résultats de la recherche, puis ajoutez-le à votre liste d’applications.

9)  Sélectionnez votre instance de LinkedIn Learning, puis sélectionnez l’onglet **Approvisionnement**.

10) Définissez le **Mode d’approvisionnement** sur **Automatique**.

![Approvisionnement LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_3.PNG)

11)  Renseignez les champs suivants sous **Informations d’identification de l’administrateur** :

* Dans l’**URL de locataire**, entrez https://api.linkedin.com.

* Dans le champ **Jeton secret**, entrez le jeton d’accès que vous avez généré à l’étape 1, puis cliquez sur **Tester la connexion**.

* Une notification de réussite doit s’afficher en haut à droite de votre portail.

12) Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case se trouvant en dessous.

13) Cliquez sur **Save**. 

14) Dans la section **Mappages d’attributs**, passez en revue les attributs d’utilisateur et de groupe qui seront synchronisés d’Azure AD vers LinkedIn Learning. Notez que les attributs sélectionnés comme propriétés **Correspondance** seront utilisés pour faire correspondre les comptes d’utilisateur et les groupes dans LinkedIn Learning pour les opérations de mise à jour. Cliquez sur le bouton Enregistrer pour valider les modifications.

![Approvisionnement LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_4.PNG)

15) Pour activer le service d’approvisionnement Azure AD pour LinkedIn Learning, définissez **l’État d’approvisionnement** sur **Activé** dans la section **Paramètres**.

16) Cliquez sur **Save**. 

Cette commande lance la synchronisation initiale des utilisateurs et/ou groupes assignés à LinkedIn Learning dans la section Utilisateurs et groupes. Notez que la synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que le service est en cours d’exécution. Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement dans votre application LinkedIn Learning.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-enterprise-apps-manage-provisioning.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
