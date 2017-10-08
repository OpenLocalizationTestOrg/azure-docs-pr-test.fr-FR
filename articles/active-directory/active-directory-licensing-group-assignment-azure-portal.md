---
title: groupe de tooa aaaAssign licences dans Azure Active Directory | Documents Microsoft
description: Comment tooassign licences toousers au moyen de la licence de groupe Azure Active Directory
services: active-directory
keywords: Gestion des licences Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Affecter des toousers de licences par l’appartenance au groupe dans Azure Active Directory

Cet article présente l’affectation d’un produit licences tooa groupe d’utilisateurs dans Azure Active Directory (Azure AD) et vérifiez qu’ils sont sous licence correctement.

Dans cet exemple, le client de hello contient un groupe de sécurité appelé **service ressources humaines**. Ce groupe inclut tous les membres du département des ressources humaines hello (environ 1 000 utilisateurs). Vous souhaitez que le département toohello de licences tooassign Office 365 entreprise E3. Hello service Yammer une entreprise qui est incluse dans hello produit doit être temporairement désactivée jusqu'à ce que le service de hello est toostart prêt à l’utiliser. Vous souhaitez également toodeploy Enterprise Mobility + Security licences toohello même groupe d’utilisateurs.

> [!NOTE]
> Certains services Microsoft ne sont pas disponibles dans tous les emplacements. Avant de tooa utilisateur peut être affectée à une licence, administrateur de hello a propriété d’emplacement d’utilisation toospecify hello sur utilisateur de hello.

> Pour l’attribution de licence de groupe, tous les utilisateurs sans un emplacement d’utilisation spécifié héritera emplacement hello du répertoire de hello. Si vous avez des utilisateurs dans plusieurs emplacements, nous vous recommandons de toujours activer l’emplacement d’utilisation dans le cadre de votre flux de création d’utilisateur dans Azure AD (par exemple, via la configuration AAD Connect) - qui garantira hello résultat d’attribution de licence est toujours correct et que les utilisateurs ne reçoivent pas services dans les emplacements qui ne sont pas autorisés.

## <a name="step-1-assign-hello-required-licenses"></a>Étape 1 : Attribuer des licences de hello requis

1. Connectez-vous à toohello [ **portail Azure** ](https://portal.azure.com) avec un compte d’administrateur. licences toomanage, compte de hello doivent être un administrateur de compte utilisateur ou un rôle Administrateur général.

2. Sélectionnez **davantage de services** dans hello du volet de navigation gauche, puis sélectionnez **Azure Active Directory**. Vous pouvez ajouter cette tooFavorites panneau ou épingler le tableau de bord de portail toohello.

3. Sur hello **Azure Active Directory** panneau, sélectionnez **licences**. Cette opération ouvre un panneau où vous pouvez consulter et gérer tous les produits sous licence dans le locataire de hello.

4. Sous **tous les produits**, sélectionnez à la fois Office 365 entreprise E3 et Enterprise Mobility + Security en sélectionnant les noms de produits hello. affectation de hello toostart, sélectionnez **affecter** haut hello du Panneau de hello.

   ![Tous les produits, affecter des licences](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. Sur hello **affecter licence** panneau, cliquez sur **utilisateurs et groupes** tooopen hello **utilisateurs et groupes** panneau. Recherchez le nom du groupe hello *service ressources humaines*, sélectionnez le groupe de hello, alors que tooconfirm en cliquant sur **sélectionnez** bas hello du Panneau de hello.

   ![Sélectionner un groupe](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. Sur hello **affecter licence** panneau, cliquez sur **options d’affectation (facultatives)**, qui affiche tous les plans de service inclus dans hello deux produits qui nous précédemment sélectionnées. Rechercher **Yammer une entreprise** et mettez-le **hors** toodisable le service de licence de produit hello. Confirmez en cliquant sur **OK** bas hello **options d’attribution**.

   ![Options d’affectation](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. affectation de hello toocomplete, sur hello **affecter licence** panneau, cliquez sur **affecter** bas hello du Panneau de hello.

8. Une notification s’affiche dans le coin supérieur droit hello qui affiche l’état de hello et le résultat du processus de hello. Si le groupe de toohello hello affectation n’a pas pu être effectuée (par exemple, en raison de licences existants dans le groupe de hello), cliquez sur Détails de tooview hello notification d’échec de hello.

Nous avons spécifié maintenant d’un modèle de licence pour le groupe de ressources humaines hello. Un processus en arrière-plan dans Azure AD a été démarrée tooprocess tous les membres existants de ce groupe. Cette opération initiale peut prendre un certain temps, en fonction de la taille actuelle de hello du groupe de hello. Dans l’étape suivante de hello, nous décrivent comment tooverify ce hello est terminée et déterminer si une attention supplémentaire est requise tooresolve problèmes.

> [!NOTE]
> Vous pouvez démarrer hello même assignation à partir d’un autre emplacement : **utilisateurs et groupes** dans Azure AD. Accédez trop**Azure Active Directory** > **utilisateurs et groupes** > **tous les groupes**. Puis recherchez le groupe de hello, sélectionnez-le, puis accédez toohello **licences** hello d’onglet **affecter** bouton sur le panneau de hello ouvre le panneau de l’attribution de licence hello.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>Étape 2 : Vérifier que l’attribution initiale hello est terminé.

1. Accédez trop**Azure Active Directory** > **utilisateurs et groupes** > **tous les groupes**. Recherchez hello **service ressources humaines** licences ont été attribués au groupe.

2. Sur hello **service ressources humaines** Panneau de groupe, sélectionnez **licences**. Cela vous permet de rapidement confirmer si les licences ont été assignées entièrement toousers et s’il existe des erreurs que vous devez toolook dans. Hello informations suivantes est disponible :

   - Liste de licences du produit qui sont actuellement affectées toohello groupe. Sélectionnez une entrée tooshow hello services spécifiques qui ont été activées et toomake change.

   - État de hello licence modifications les plus récentes apportées toohello groupe (si des modifications de hello sont en cours de traitement ou si le traitement est terminé pour tous les membres de l’utilisateur).

   - Informations sur les utilisateurs qui se trouvent dans un état d’erreur, car il est impossible d’affecter les licences toothem.

   ![Options d’affectation](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Pour des informations plus détaillées sur le traitement des licences, consultez **Azure Active Directory** > **Utilisateurs et groupes** > *nom du groupe* > **Journaux d’audit**. Notez hello suivant des activités :

   - Activité : **commencer à appliquer les groupe basé licence toousers**. Cette opération est enregistrée lorsque le système de hello récupère de la modification d’attribution de licence hello sur le groupe de hello et démarre son application tooall membres d’un utilisateur. Il contient des informations sur la modification de hello a été effectuée.

   - Activité : **finissez groupe basé licence toousers**. Cette opération est enregistrée lorsque le système de hello termine le traitement de tous les utilisateurs dans le groupe de hello. Elle contient un résumé du nombre d’utilisateurs qui ont été traités avec succès et du nombre d’utilisateurs auxquels les licences du groupe n’ont pas pu être affectées.

   [Lisez cette section](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn plus en détail comment les journaux d’audit peuvent être apportées aux tooanalyze utilisé par basée sur le groupe de licences.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Étape 3 : Rechercher des problèmes de licences et les résoudre

1. Accédez trop**Azure Active Directory** > **utilisateurs et groupes** > **tous les groupes de**et recherche hello **ressources humaines**groupe de licences attribuées à.
2. Sur hello **service ressources humaines** Panneau de groupe, sélectionnez **licences**. notification Hello sur Panneau de hello montre qu’il n’y a 10 utilisateurs licences n’a pas pu être assignés à. En cliquant sur cette notification, vous accédez à une liste de tous les utilisateurs associés à une erreur de licence pour ce groupe.
3. Hello **échec affectations** colonne nous indique que les deux licences n’a pas pu être assignés toohello utilisateurs. Hello **premiers raison de l’échec** colonne contient la cause de hello de défaillance de hello. Dans ce cas, il s’agit de **Plans de service en conflit**.

   ![Échec d’affectations](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Sélectionnez un Bonjour de tooopen utilisateur **licences** panneau. Ce panneau affiche toutes les licences qui sont actuellement attribuées toohello utilisateur. Dans cet exemple, utilisateur de hello a licence hello Office 365 entreprise E1 qui a été héritée de hello **les utilisateurs Kiosk** groupe. Il est en conflit avec licence hello E3 hello tooapply système a tenté de hello **service ressources humaines** groupe. Par conséquent, aucune des licences hello à partir de ce groupe a été affecté toohello utilisateur.

   ![Afficher les licences pour un utilisateur](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve ce conflit, supprimez hello utilisateur hello **les utilisateurs Kiosk** groupe. Une fois Azure AD traite les modifications de hello, hello **service ressources humaines** licences sont attribuées correctement.

   ![Licence affectée correctement](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Étapes suivantes

toolearn plus d’informations sur la fonctionnalité de hello définie pour la gestion des licences via les groupes, consultez hello suivant des articles :

* [What is group-based licensing in Azure Active Directory? (Présentation des licences basées sur le groupe dans Azure Active Directory)](active-directory-licensing-whatis-azure-portal.md)
* [Identification et résolution des problèmes de licence pour un groupe dans Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Comment toomigrate individuels titulaires d’une licence dans Azure Active Directory en fonction des toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios (Autres scénarios de licence basée sur le groupe Azure Active Directory)](active-directory-licensing-group-advanced.md)
