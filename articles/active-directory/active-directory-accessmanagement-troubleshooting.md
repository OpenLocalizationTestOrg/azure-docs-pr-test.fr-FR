---
title: aaaTroubleshooting des membres dynamiques pour les groupes | Documents Microsoft
description: "Conseils pour résoudre les problèmes d’appartenance dynamique à des groupes dans Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Résolution des problèmes liés à l’appartenance dynamique à des groupes
**J’ai configuré une règle sur un groupe, mais aucune appartenance mis à jour dans le groupe de hello**<br/>Vérifiez que hello **activer gestion déléguée des groupes** est défini trop**Oui** Bonjour **configurer** onglet. Vous verrez ce paramètre uniquement si vous êtes connecté en tant qu’un toowhom utilisateur une licence Azure Active Directory Premium est attribuée. Vérifiez les valeurs hello pour les attributs d’utilisateur sur une règle hello : existe-t-il des utilisateurs qui répondent aux règles de hello ?

**J’ai configuré une règle, mais maintenant les membres existants de hello de règle de hello sont supprimés**<br/>Ce comportement est normal. Les membres existants du groupe de hello sont supprimés lorsqu’une règle est activée ou modifiée. les utilisateurs de Hello retournés à partir de l’évaluation de la règle de hello sont ajoutés en tant que groupe de membres toohello.     

**Je ne vois pas instantanément de changement d’appartenance quand j’ajoute ou quand je modifie une règle. Pourquoi ?**<br/>L’évaluation de l’appartenance dédiée est effectuée régulièrement dans le cadre d’un processus asynchrone exécuté en arrière-plan. La durée pendant laquelle hello a est déterminé par un nombre d’utilisateurs dans votre répertoire et hello la taille de groupe hello créé suite à la règle de hello hello. En règle générale, les répertoires avec un nombre réduit d’utilisateurs verrez changements d’appartenance au groupe hello en moins de quelques minutes. Répertoires avec un grand nombre d’utilisateurs peuvent prendre 30 minutes ou plu toopopulate.

### <a name="next-steps"></a>Étapes suivantes
Ces articles fournissent des informations supplémentaires sur Azure Active Directory.

* [La gestion des accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md)
* [Intégration des identités locales dans Azure Active Directory](active-directory-aadconnect.md)
