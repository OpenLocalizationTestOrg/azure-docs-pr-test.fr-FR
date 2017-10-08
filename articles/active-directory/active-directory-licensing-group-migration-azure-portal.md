---
title: toomigrate aaaHow votre tooa des utilisateurs individuels sous licence de groupe dans Azure Active Directory | Documents Microsoft
description: "Comment tooswitch à partir de l’utilisateur individuel licences toogroup concession de licence à l’aide d’Azure Active Directory"
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Comment tooadd concédé sous licence tooa groupe d’utilisateurs pour le Gestionnaire de licences dans Azure Active Directory

Vous avez peut-être existant toousers de licences déployées dans des organisations de hello via « assignation directe ; » Autrement dit, à l’aide de scripts PowerShell ou autres outils tooassign individuels de licences utilisateur. Si vous souhaitez que toostart à l’aide basée sur le groupe de licences licences de toomanage dans votre organisation, vous devez une migration plan tooseamlessly remplacer des solutions existantes avec basée sur le groupe de licences.

Hello plus importantes chose tookeep à l’esprit est que vous devez éviter une situation où migration toogroup concession de licence entraîne utilisateurs temporairement perdent leurs licences actuellement attribués. Tout processus qui peut entraîner la suppression des licences doit être évitée risque de hello tooremove d’utilisateurs perdre l’accès tooservices et leurs données.

## <a name="recommended-migration-process"></a>Processus de migration recommandé

1. Votre gestion de l’attribution et de la suppression des licences utilisateur est actuellement automatisée (par exemple, avec PowerShell). Conservez ce paramétrage.

2. Créer un nouveau groupe de licences (ou décider quels existant groupes toouse) et vérifiez que tous les utilisateurs sont ajoutés en tant que membres.

3. Affecter des licences de hello requis toothose ; votre objectif doit être tooreflect hello même état de licence votre automatisation existante (par exemple, PowerShell) applique toothose utilisateurs.

4. Vérifiez que les licences ont été appliqués tooall les utilisateurs de ces groupes. Cela est possible en vérifiant l’état de traitement hello sur chaque groupe et en vérifiant les journaux d’Audit.

  - Vous pouvez vérifier ponctuellement certains utilisateurs individuels en examinant les détails de leur licence. Vous verrez qu’ils ont hello même licences attribuées « directement » et « hérité » à partir de groupes.

  - Vous pouvez exécuter un script PowerShell trop[vérifier comment les licences sont attribuées toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - Lorsque hello même licence de produit est assignée toohello utilisateur à la fois directement et via un groupe, seule une licence est consommée par l’utilisateur de hello. Par conséquent, aucune des licences supplémentaires ne sont requis tooperform migration.

5. Assurez-vous qu’aucune attribution de licence n’a échoué en vérifiant les utilisateurs en état d’erreur dans chaque groupe. Pour plus d’informations, consultez [Identification et résolution des problèmes de licence pour un groupe](active-directory-licensing-group-problem-resolution-azure-portal.md).

6. Envisagez de supprimer des attributions de direct hello d’origine ; Vous souhaiterez peut-être toodo progressivement, dans « ondes », toomonitor hello résultat sur un sous-ensemble d’utilisateurs tout d’abord.

  Vous pouvez laisser les assignations directes d’origine hello sur les utilisateurs, mais lorsque les utilisateurs de hello laissent leurs groupes sous licence qu’ils conserveront licence d’origine hello, qui n’est peut-être pas que vous souhaitez.

## <a name="an-example"></a>exemple

Une organisation compte 1 000 utilisateurs. Tous les utilisateurs ont besoin d’une licence Enterprise Mobility + Security (EMS). 200 utilisateurs sont Bonjour service Finance et nécessitent des licences d’Office 365 entreprise E3. Un script PowerShell s’exécute en local afin d’ajouter et de supprimer les licences des utilisateurs qui arrivent ou s’en vont. Il convient de script de hello tooreplace avec basée sur le groupe de licences pour les licences sont gérées automatiquement par Azure AD.

Voici le processus de migration hello pourrait ressembler :

1. À l’aide de hello assign portail Azure hello EMS licence toohello **tous les utilisateurs** groupe dans Azure AD. Affecter hello E3 licence toohello **service financier** groupe qui contient tous les utilisateurs de hello requis.

2. Dans chaque groupe, vérifiez que l’attribution de licence est effectuée pour tous les utilisateurs. Panneau accédez toohello pour chaque groupe, sélectionnez **licences**et vérifier l’état de traitement hello haut hello hello **licences** panneau.

  - Rechercher pour tooconfirm de « dernières modifications de licence ont été appliqués tooall utilisateurs », le traitement est terminé.

  - Recherchez une notification en haut de la page, indiquant les utilisateurs pour lesquels des licences n’ont peut-être pas été correctement attribuées. Avons-nous manqué de licences pour certains utilisateurs ? Certains utilisateurs présentent-ils des références de licence en conflit qui les empêchent d’hériter des licences de groupe ?

3. Vérifiez tooverify certains utilisateurs qu’ils ont hello direct et licences de groupe appliqués. Panneau accédez toohello pour un utilisateur, sélectionnez **licences**et examiner l’état de hello de licences.

  - Voici l’état utilisateur hello attendu pendant la migration :

      ![État utilisateur attendu](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  Cela confirme que l’utilisateur hello possède des licences, directs et héritées. Il apparaît que des licences **EMS** et **E3** sont attribuées.

  - Sélectionnez chaque licence tooshow plus d’informations sur les services hello activée. Cela peut être utilisé toocheck si hello direct et activer les licences de groupe exactement hello même plans de service pour l’utilisateur de hello.

      ![Vérification des plans de service](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. Après avoir confirmé l’équivalence des licences directes et des licences de groupe, vous pouvez commencer à supprimer les licences directes des utilisateurs. Vous pouvez tester cela en les supprimant pour les utilisateurs individuels dans le portail de hello, puis exécutez toohave de scripts d’automatisation que les supprimer en bloc. Voici un exemple de hello même utilisateur avec les licences direct hello supprimé via le portail de hello. Notez qu’état de la licence hello reste inchangé, mais nous ne voyez plus les assignations directes.

  ![Licences directes supprimées](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les autres scénarios de gestion des licences via les groupes, lire

* [Affectation d’un groupe de tooa de licences dans Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [What is group-based licensing in Azure Active Directory? (Présentation des licences basées sur le groupe dans Azure Active Directory)](active-directory-licensing-whatis-azure-portal.md)
* [Identification et résolution des problèmes de licence pour un groupe dans Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios (Autres scénarios de licence basée sur le groupe Azure Active Directory)](active-directory-licensing-group-advanced.md)
