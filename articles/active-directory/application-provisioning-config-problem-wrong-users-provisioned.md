---
title: "ensemble aaaWrong d’utilisateurs sont en cours d’application de la galerie tooan mis en service Azure AD | Documents Microsoft"
description: "Découvrez comment toofind les pourquoi un ensemble différent d’utilisateurs sont mis en service application tooan que ceux attendus"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Mauvais groupe d’utilisateurs sont en cours d’application de la galerie tooan mis en service Azure AD

Les utilisateurs qui sont approvisionnés toohello application est basée sur les utilisateurs et les groupes auxquels ont été **affecté** toohello application.

Utilisez les ressources hello ci-dessous toolearn comment toocheck les utilisateurs et les groupes auxquels ont été attribué des application tooan dans Azure Active Directory.

## <a name="assign-a-user-directly-as-an-administrator"></a>Affecter un utilisateur directement en tant qu’administrateur

tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.

7.  Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.

9.  Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.

10. Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.

11. Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**. Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.

12. **Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.

13. Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.

14. **Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.

15. Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.

Si cette configuration est configuré et en cours d’exécution pour une application, les nouveaux utilisateurs doivent être application tooan approvisionnés dans 10 minutes environ. Vérifiez hello **les journaux d’Audit** pour plus d’informations.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Assigner un groupe directement tooan application en tant qu’administrateur

tooassign un ou plusieurs groupes tooan application directement, hello suivez les étapes ci-dessous :

1.  Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**

2.  Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.

3.  Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.

4.  Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.

5.  Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.

  * Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**

6.  Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.

7.  Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.

8.  Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.

9.  Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.

10. Type Bonjour **nom de groupe complète** groupe hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.

11. Placez le curseur sur hello **groupe** dans hello liste tooreveal un **case à cocher**. Cliquez sur tooadd de photo ou le logo de profil de hello case à cocher toohello groupe suivant votre toohello utilisateur **sélectionnés** liste.

12. **Facultatif :** si vous souhaitez que trop**ajouter plusieurs groupes**, type dans un autre **nom de groupe complète** dans hello **recherche par nom ou adresse de messagerie** zone de recherche, Cliquez sur tooadd de case à cocher hello toohello de ce groupe **sélectionnés** liste.

13. Lorsque vous avez fini de sélectionner les groupes, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.

14. **Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un toohello de tooassign rôle groupes que vous avez sélectionné.

15. Cliquez sur hello **affecter** bouton tooassign hello application toohello les groupes sélectionnés.

Si cette configuration est configuré et en cours d’exécution pour une application, les nouveaux utilisateurs contenus dans le groupe de hello doivent être application tooan approvisionnés dans 10 minutes environ. Vérifiez hello **les journaux d’Audit** pour plus d’informations.

>[!IMPORTANT]
>Hello nom du groupe de configuration d’et de groupe plus d’informations, dans les membres de toohello de plus, si la prise en charge pour certaines applications. Vous pouvez activer ou désactiver cette fonctionnalité en activant ou désactivant hello **mappage** pour les objets de groupe affichés dans hello **Provisioning** onglet. 
>
>

Si la configuration des groupes est activée, veillez à tooreview hello attribut mappages tooensure un champ approprié est utilisé pour hello « correspondant ID ». Cela peut être le nom d’affichage hello ou par courrier électronique à l’alias, que hello groupe et ses membres ne pas être configurés si hello correspondant est vide ou non remplie pour un groupe dans Azure AD.

## <a name="next-steps"></a>Étapes suivantes
[Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications avec Azure Active Directory](active-directory-saas-app-provisioning.md)
