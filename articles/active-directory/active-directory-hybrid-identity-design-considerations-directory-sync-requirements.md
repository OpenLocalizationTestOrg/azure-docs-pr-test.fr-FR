---
title: "aaaAzure considérations de conception hybride identité Active Directory - déterminer les besoins de synchronisation d’annuaire | Documents Microsoft"
description: "Identifier les exigences sont nécessaires pour la synchronisation de tous les utilisateurs de hello entre on = locaux et cloud d’entreprise de hello."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a>Déterminer les exigences de synchronisation de répertoire
Synchronisation consiste à fournir aux utilisateurs une identité de cloud hello basée sur leur identité locale. Ou non qu’ils utiliseront le compte synchronisé pour l’authentification ou l’authentification fédérée, les utilisateurs de hello doivent toujours toohave une identité de cloud de hello.  Cette identité a besoin toobe conservées et mises à jour régulièrement.  mises à jour Hello peuvent prendre différentes formes, des modifications de toopassword de modifications de titre.  

Commencez par évaluer les organisations hello identité utilisateur et la solution contraintes locales. Cette évaluation est important toodefine hello prescriptions comment les identités d’utilisateur seront créées et mis à jour dans le cloud de hello.  Pour la plupart des organisations, Active Directory est local et ne sont hello des services locaux qui sont des utilisateurs par synchronisées de toutefois dans certains cas cela sera pas hello cas.  

Vérifiez que hello tooanswer suivant questions :

* Combien avez-vous de forêts AD: une, plusieurs ou aucune ?
  
  * Vers combien d'annuaires Azure AD allez-vous synchroniser ?
    
    1. Utilisez-vous le filtrage ?
    2. Avez-vous prévu plusieurs serveurs Azure AD Connect ?
* Avez-vous actuellement un outil de synchronisation local ?
  
  * Si oui, vos utilisateurs bénéficient-ils d'un annuaire/d'une intégration virtuels d'identités ?
* Vous disposez de n’importe quel autre répertoire local que vous souhaitez toosynchronize (par exemple, annuaire LDAP, base de données des ressources humaines, etc.) ?
  * Vous allez toobe effectuer n’importe quel GALSync ?
  * Nouveautés d’état de hello actuel de l’UPN de votre organisation ? 
  * Avez-vous un annuaire différent pour l'authentification des utilisateurs ?
  * Votre entreprise utilise-t-elle Microsoft Exchange ?
    * Le déploiement d'Exchange hybride est-il prévu ?

Maintenant que vous avez une idée sur les conditions de synchronisation, vous devez toodetermine outil est un toomeet correct de hello ces exigences.  Microsoft fournit plusieurs intégration d’annuaire tooaccomplish outils et la synchronisation.  Consultez hello [tableau de comparaison des outils identité hybride directory integration](active-directory-hybrid-identity-design-considerations-tools-comparison.md) pour plus d’informations. 

Maintenant que vous avez vos exigences de synchronisation et d’un outil hello pour ce faire, de votre société, vous avez besoin d’applications hello tooevaluate qui utilisent ces services d’annuaire. Cette évaluation est importante toodefine hello spécifications techniques toointegrate ces cloud de toohello d’applications. Vérifiez que hello tooanswer suivant questions :

* Ces applications seront déplacé toohello cloud et utiliser hello directory ?
* Y a-t-il des attributs spéciaux qui doivent toobe synchronisé toohello cloud afin de ces applications peuvent les utiliser avec succès ?
* Ces applications devez toobe réécrite parti tootake d’authentification de cloud ?
* Ces applications continue toolive local tandis que les utilisateurs y accéder à l’aide d’identité de cloud hello ?

Vous devez également toodetermine hello sécurité exigences et contraintes de synchronisation d’annuaires. Cette évaluation est important tooget une liste d’exigences hello qui seront nécessaires dans l’ordre toocreate et conserver l’identité de l’utilisateur dans le cloud de hello. Vérifiez que hello tooanswer suivant questions :

* Où serveur de synchronisation hello se trouver ?
* Sera-t-il lié à un domaine ?
* Serveur de hello se trouvera sur un réseau restreint derrière un pare-feu, par exemple un réseau de périmètre ?
  * Sera synchronisation toosupport des ports pare-feu tooopen en mesure de hello requis ?
* Disposez-vous d’un plan de récupération d’urgence pour le serveur de synchronisation hello ?
* Disposez-vous d’un compte disposant des autorisations correctes de hello pour toutes les forêts que vous souhaitez toosynch avec ?
  * Si votre entreprise ne sait pas réponses hello pour cette question, passez en revue la section hello « Autorisations pour la synchronisation de mot de passe » dans l’article de hello [installation hello Service de synchronisation Azure Active Directory](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) et déterminer si vous disposez déjà d’un compte disposant de ces autorisations ou si vous devez toocreate une.
* Si vous avez synchronisation de multi-forêt est tooget en mesure de tooeach forêt de hello synchronisation server ?

> [!NOTE]
> Notez que tootake de chacune des réponses et comprendre hello sous-tend hello. [Déterminer les besoins de réponse aux incidents](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) passe en revue les options hello disponibles. En répondant à chacune de ces questions, vous sélectionnerez l’option correspondant le mieux à vos besoins métier.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Déterminer les exigences d’authentification multifacteur](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

