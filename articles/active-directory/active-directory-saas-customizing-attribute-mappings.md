---
title: "aaaCustomizing des mappages d’attributs Active Directory de Azure | Documents Microsoft"
description: "Découvrez lesquels mappages d’attributs pour les applications SaaS dans Azure Active Directory sont comment vous pouvez modifier les tooaddress votre entreprise a besoin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Personnalisation des mappages d’attributs d’approvisionnement d’utilisateurs pour les applications SaaS dans Azure Active Directory
Microsoft Azure AD prend en charge les applications SaaS tierces toothird tels que Salesforce, Google Apps et d’autres de configuration de l’utilisateur. Si vous disposez de configuration pour une application de SaaS tiers activée de l’utilisateur, hello portail de gestion Azure contrôle ses valeurs d’attribut dans le cadre d’une configuration appelée « mappage d’attribut ».

Il existe un ensemble préconfiguré de mappages d’attributs entre les objets utilisateur Azure AD et les objets utilisateur de chaque application SaaS. Certaines applications gèrent d’autres types d’objets, tels que des groupes ou des contacts. <br> 
 Vous pouvez personnaliser les mappages d’attributs par défaut hello selon les besoins de tooyour. Cela signifie que vous pouvez modifier ou supprimer des mappages d’attributs existants ou en créer de nouveaux.

Dans le portail hello Azure AD, vous pouvez accéder à cette fonctionnalité en cliquant sur un **mappages** configuration sous **Provisioning** Bonjour **gérer** section d’un  **Application d’entreprise**.


![Salesforce][5] 

En cliquant sur un **mappages** configuration, ouvre hello liée **un mappage d’attribut** panneau.  
Il existe des mappages d’attributs qui sont requis par une toofunction d’application SaaS correctement. Pour les attributs requis, hello **supprimer** fonctionnalité n’est pas disponible.


![Salesforce][6]  

Dans l’exemple hello ci-dessus, vous pouvez voir que hello **nom d’utilisateur** attribut d’un objet géré dans Salesforce est rempli avec hello **userPrincipalName** valeur Hello liée objet Azure Active Directory.

Vous pouvez personnaliser des **mappages d’attributs** existants en cliquant sur un mappage. Cette opération ouvre hello **modifier l’attribut** panneau.

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>Présentation des types de mappage d’attributs
Avec les mappages d’attributs, vous contrôlez la façon dont les attributs sont renseignés dans une application SaaS tierce. Quatre différents types de mappages sont pris en charge :

* **Direct** – attribut de hello cible est rempli avec la valeur hello d’un attribut de l’objet lié de hello dans Azure AD.
* **Constante** – attribut de cible de hello est rempli par une chaîne spécifique que vous avez spécifié.
* **Expression** -attribut de hello cible est rempli en fonction de résultats d’une expression de type script hello. 
  Pour plus d’informations, consultez l’article [Écriture d’expressions pour les mappages d’attributs dans Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).
* **Aucun** -attribut cible de hello reste inchangée. Toutefois, si l’attribut cible de hello est toujours vide, il est rempli avec la valeur par défaut hello que vous spécifiez.

Dans types de mappage addition toothese quatre attributs de base, prend en charge les mappages d’attributs personnalisés concept hello de facultatif **par défaut** assignation de valeur. assignation de la valeur par défaut Hello garantit qu’un attribut cible est rempli avec une valeur si elle existe aucune valeur dans Azure AD ou sur l’objet cible de hello. configuration la plus courante Hello est tooleave ce vide.


## <a name="understanding-attribute-mapping-properties"></a>Présentation des propriétés de mappage d’attributs

Dans la section précédente de hello, vous avez déjà été introduites toohello attribut mappage type propriété.
Dans la propriété toothis de plus, des mappages d’attributs prennent en charge également les hello suivant d’attributs :

- **Attribut source** -attribut utilisateur hello système source de hello (par exemple : Azure Active Directory).
- **Attribut cible** : attribut d’utilisateur hello dans le système cible de hello (par exemple : ServiceNow).
- **Correspond à des objets à l’aide de cet attribut** : ce mappage doit être utilisé ou non toouniquely identifier les utilisateurs entre les systèmes source et cible hello. Cela est généralement définie sur hello userPrincipalName ou attribut de messagerie dans Azure AD, qui est généralement mappé tooa des champs de nom d’utilisateur dans une application cible.
- **Priorité des correspondances** : plusieurs attributs de correspondance peuvent être définis. S’il existe plusieurs, ils sont évalués dans l’ordre de hello défini par ce champ. Dès qu’une correspondance est trouvée, aucun autre attribut correspondant n’est évalué.
- **Appliquer ce mappage**
    - **Toujours** : applique ce mappage à la création de l’utilisateur et des actions de mise à jour.
    - **Lors de la création uniquement** : applique ce mappage uniquement aux actions de création d’utilisateur.


## <a name="what-you-should-know"></a>Ce que vous devez savoir

Microsoft Azure AD fournit une implémentation efficace d’un processus de synchronisation. Dans un environnement initialisé, seuls les objets nécessitant des mises à jour sont traités pendant un cycle de synchronisation. Mise à jour des mappages d’attributs d’a un impact sur les performances de hello d’un cycle de synchronisation. Une configuration de mappage de mise à jour toohello attribut nécessite tous les objets managés toobe réévaluées. Il est un meilleure pratique tookeep hello nombre de mappages d’attributs tooyour modifications consécutives au minimum.

## <a name="next-steps"></a>Étapes suivantes

* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Automatiser la configuration d’utilisateur/Deprovisioning tooSaaS applications](active-directory-saas-app-provisioning.md)
* [Écriture d’expressions pour les mappages d’attributs](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtres d’étendue pour l’approvisionnement des utilisateurs](active-directory-saas-scoping-filters.md)
* [SCIM tooenable la configuration automatique des utilisateurs et groupes à partir d’Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notifications d’approvisionnement de comptes](active-directory-saas-account-provisioning-notifications.md)
* [Liste des didacticiels sur la façon de tooIntegrate applications SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

