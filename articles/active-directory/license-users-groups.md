---
title: utilisateurs aaaLicense dans Azure Active Directory | Documents Microsoft
description: "Découvrez comment toolicense vous-même et vos utilisateurs dans Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>Guide de démarrage rapide : Utilisateurs sous licence dans Azure Active Directory
Les services Azure AD basés sur des licences reposent sur l’activation d’un abonnement Azure Active Directory (Azure AD) dans votre client Azure. Une fois l’abonnement de hello est actif, des fonctionnalités de service sont gérées par des administrateurs Azure AD et utilisées par les utilisateurs sous licence. Lorsque vous achetez Enterprise Mobility + Security, Azure AD Premium ou Azure AD Basic, votre client est mis à jour avec abonnement hello, y compris sa période de validité et prépayé des licences. Vos informations d’abonnement, y compris nombre hello de licences attribuées ou disponibles, soient disponibles via hello Azure portail sous **Azure Active Directory** en ouvrant le hello **licences** vignette. Hello **licences** lame est également hello meilleures place toomanage les affectations de licence.

Bien qu’obtention d’un abonnement est tous les tooconfigure payé des fonctionnalités, vous devez néanmoins être affectés à des licences utilisateur pour payant Azure AD fonctionnalités payée. Une licence doit être attribuée à tout utilisateur ayant besoin d’accéder à une fonctionnalité Azure AD payante ou géré par le biais de ce type de fonctionnalité. L’attribution de licence est un mappage entre un utilisateur et un service acheté, comme Azure AD Premium, Azure AD Basic ou Enterprise Mobility + Security.

Vous pouvez utiliser [attribution de licence basée sur le groupe](active-directory-licensing-whatis-azure-portal.md) tooset des règles telles que les éléments suivants de hello :
* Tous les utilisateurs de votre annuaire obtiennent automatiquement une licence
* Toute personne avec le titre de travail approprié hello Obtient une licence
* Vous pouvez déléguer des gestionnaires de tooother hello décision dans l’organisation de hello (à l’aide de [groupes en libre-service](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> Pour obtenir une présentation détaillée de toogroups d’attribution de licence, y compris avancé des scénarios et Office 365, les scénarios de gestion de licences voir [attribuer des licences toousers par l’appartenance au groupe dans Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="assign-licenses-toousers-and-groups"></a>Assigner des groupes et des licences toousers
À l’aide d’un abonnement actif, vous devez tout d’abord attribuer une licence tooyourself et actualiser votre tooensure navigateur que vous voyez toutes les fonctionnalités de hello attendu incluses avec votre abonnement. étape suivante de Hello est tooassign licences toohello utilisateurs qui doivent accéder aux fonctionnalités de Azure AD toopaid. Une licence de tooassign facilement est toogroups de licences tooassign d’utilisateurs, plutôt que tooindividuals. Lorsque vous affectez le groupe de licences tooa, tous les membres du groupe sont affectés à une licence. Si les utilisateurs sont ajoutés ou supprimés du groupe de hello, licence hello est automatiquement attribué ou supprimé. 

> [!NOTE]
> Certains services Microsoft ne sont pas disponibles dans tous les emplacements. Tooa utilisateur peut être affectée à une licence, administrateur de hello devez spécifier hello **l’emplacement d’utilisation** propriété pour l’utilisateur de hello. Vous pouvez définir cette propriété sous **utilisateur** &gt; **profil** &gt; **paramètres** Bonjour portail Azure. Lorsque vous utilisez l’affectation du groupe de licences, emplacement hello du répertoire de hello hérite de n’importe quel utilisateur dont l’emplacement d’utilisation n’est pas spécifié.

tooassign une licence, sous **Azure Active Directory** &gt; **licences** &gt; **tous les produits**, sélectionnez un ou plusieurs produits, puis **Affecter** sur la barre de commandes hello.

![Sélectionnez un tooassign de licence](media/license-users-groups/select-license-to-assign.png)

Vous pouvez utiliser hello **utilisateurs et groupes** toochoose panneau plusieurs utilisateurs ou groupes ou toodisable service plans dans le produit de hello. Utiliser zone de recherche hello toosearch supérieur pour les noms d’utilisateur et de groupe.

![Sélectionner un utilisateur ou un groupe pour l’attribution de licences](media/license-users-groups/select-user-for-license-assignment.png)

Lorsque vous affectez le groupe de licences tooa, il peut prendre un certain temps avant que tous les utilisateurs héritent licence hello selon la taille de hello du groupe de hello. Vous pouvez vérifier le statut de traitement hello sur hello **groupe** panneau, sous hello **licences** vignette.

![Statut d’affectation de licence](media/license-users-groups/license-assignment-status.png)

Des erreurs d’affectation peuvent se produire lors de l’affectation des licences Azure AD, mais elles restent relativement rares lors de la gestion des produits Azure AD et Enterprise Mobility + Security. Les erreurs d’attribution se limitent aux problèmes suivants :
- Conflits d’attribution : quand un utilisateur a été affecté précédemment une licence qui n’est pas compatible avec licence en cours de hello. Dans ce cas, l’attribution de licence de nouveau hello requiert hello en cours de suppression.
- Dépassement de licences disponibles : lorsque nombre hello d’utilisateurs dans les groupes assignés dépasse les licences disponibles hello, état d’attribution d’un utilisateur reflète un tooassign échec en raison de toomissing licences.

### <a name="azure-ad-b2b-collaboration-licensing"></a>Affectation de licences Azure Active Directory B2B Collaboration

B2B collaboration vous permet des utilisateurs invités de tooinvite à vos services de Azure AD client tooprovide accès tooAzure AD et les ressources Azure vous rendre disponible.  

Il n’existe aucun frais pour inviter les utilisateurs B2B et de les affecter l’application tooan dans Azure AD. Les applications too10 par invité utilisateur et des rapports de base 3 sont également gratuits pour les utilisateurs de collaboration B2B. Si votre utilisateur invité a aucune licence appropriée dans le locataire d’Azure AD du partenaire hello, ils allez disposer d’une licence dans le vôtre également.

Il n’est pas obligatoire, mais si vous souhaitez que les fonctionnalités de tooprovide accès toopaid Azure AD, les utilisateurs invités de B2B doivent disposer d’une licence avec des licences de Azure AD d’appropriées. Un locataire invitant à une annonce Azure payé licence permettre affecter des droits d’utilisateur B2B collaboration les utilisateurs d’invité tooan cinq supplémentaires invités toohello client. Pour plus d’informations et pour voir des scénarios, consultez le [Guide d’attribution de licences pour Azure Active Directory B2B Collaboration](active-directory-b2b-licensing.md).

## <a name="view-assigned-licenses"></a>Visualiser les licences attribuées

Un récapitulatif des licences attribuées et disponibles est disponible sous **Azure Active Directory** &gt; **Licences** &gt; **Tous les produits**.

![Afficher le récapitulatif des licences](media/license-users-groups/view-license-summary.png)

Une liste détaillée des utilisateurs et groupes attribués est disponible quand vous sélectionnez un produit spécifique. Hello **utilisateurs sous licence** liste affiche tous les utilisateurs actuellement consomme une licence et que la licence de hello a été assignée directement toohello utilisateur ou si elle est héritée d’un groupe.

![Afficher le détail des licences](media/license-users-groups/view-license-detail.png)

De même, hello **concédé sous licence de groupes** liste affiche tous les groupes de licences de toowhich ont été affectés. Sélectionnez un Bonjour tooopen utilisateur ou un groupe **licences** panneau, qui montre toutes les licences affectées toothat objet.

## <a name="remove-a-license"></a>Supprimer une licence

tooremove une licence, accédez toohello utilisateur ou un groupe et ouvrez hello **licences** vignette. Sélectionnez hello licence, puis cliquez sur **supprimer**.

![Supprimer une licence](media/license-users-groups/remove-license.png)

Héritée par utilisateur hello à partir d’un groupe de licences ne peut pas être supprimées directement. Au lieu de cela, supprimez-le hello groupe hello à partir duquel ils héritent des licences de hello.


## <a name="next-steps"></a>Étapes suivantes
Dans ce démarrage rapide, vous avez appris comment tooassign licences toousers et les groupes dans Windows Azure AD. 

Vous pouvez utiliser hello suivant des affectations de licence de lien tooconfigure abonnement dans Azure AD dans hello portail Azure.

> [!div class="nextstepaction"]
> [Attribuer des licences Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 