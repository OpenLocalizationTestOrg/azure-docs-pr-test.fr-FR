---
title: "applications aaaProvisioning avec des filtres d’étendue | Documents Microsoft"
description: "Découvrez comment toouse étendue filtre les objets tooprevent dans les applications qui prennent en charge l’approvisionnement automatique des utilisateurs d’être réellement configuré si un objet n’est pas conforme à vos besoins."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Approvisionnement d’applications basé sur les attributs avec filtres d’étendue
objectif Hello de cette section est tooexplain toouse étendue comment les filtres toodefine basée sur les attributs des règles qui déterminent quels utilisateurs sont mis en service toohello application.

## <a name="clauses-and-scope-groups"></a>Clauses et groupes d’étendue
![Filtre d’étendue][1] 

Les filtres d’étendue sont définis par un ou plusieurs **groupes d’étendue**, chacun contenant une ou plusieurs **clauses**. clauses de hello toosee pour un groupe d’étendue particulier, développez-le en cliquant sur hello flèche toohello gauche du nom du groupe hello.

A **clause** détermine quels utilisateurs sont autorisés à toopass via hello filtre d’étendue en évaluant les attributs de chaque utilisateur. Par exemple, vous pouvez avoir une clause qui impose que « état » attribut égal New York l’utilisateur, donc seuls les utilisateurs de New York sont configurés dans l’application hello.

![Nom du groupe d’étendue][2] 

Chaque **groupe d’étendue** commence par un obligatoire **clause**, comme illustré dans la capture d’écran hello ci-dessus. Cette clause déclare simplement que l’utilisateur hello doit d’abord être affecté toohello application avant son évaluation par vos filtres d’étendue. Cette clause ne peut pas être supprimée ou modifiée.

Vous pouvez ajouter de nouvelles clauses ou nouveaux groupes d’étendue en appuyant sur le bouton approprié de hello. Vous pouvez attribuer un nom à chaque groupe d’étendue en modifiant sa propriété **Nom du groupe d’étendue** .

## <a name="how-scoping-filters-are-evaluated"></a>Évaluation des filtres d’étendue
Lors de la configuration, nous testons chaque utilisateur affecté par rapport à votre portée toodetermine de filtres si cet utilisateur mérite accès toohello application. Vous pouvez considérer chaque clause comme un test qui doive être passé dans l’ordre pour hello utilisateur tooavoid est rejeté. 

Si vous avez plusieurs groupes d’étendue définies, chaque utilisateur doit au moins un d'entre eux tooaccess passer application hello. Au sein de chaque groupe d’étendue, toutefois, hello utilisateur doit passer chaque toopass clause ce groupe d’étendue spécifique. 

En d’autres termes, vous pouvez considérer les groupes d’étendue comme étant ou liés, et vous pouvez considérer clauses hello comme en cours et liés. Par exemple, considérez hello ci-dessous de filtre d’étendue :

![Nom du groupe d’étendue][3]  

En fonction de filtre d’étendue de toothis, les utilisateurs doivent satisfaire suivant de hello critères, toobe configuré :

1. Ils doivent avoir toohello application.
2. Ils doivent travailler dans le service d’ingénierie hello
3. Ils doivent travailler à San Francisco ou au Canada.

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications](active-directory-saas-app-provisioning.md)
* [Personnalisation des mappages d’attributs pour l’approvisionnement des utilisateurs](active-directory-saas-customizing-attribute-mappings.md)
* [Écriture d’expressions pour les mappages d’attributs](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Notifications d’approvisionnement de comptes](active-directory-saas-account-provisioning-notifications.md)
* [SCIM tooenable la configuration automatique des utilisateurs et groupes à partir d’Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Liste des didacticiels sur la façon de tooIntegrate applications SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
