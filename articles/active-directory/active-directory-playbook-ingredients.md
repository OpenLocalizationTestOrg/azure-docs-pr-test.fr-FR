---
title: "aaaAzure Active Directory preuve de concept manuel d’ingrédients | Documents Microsoft"
description: "Explorer et implémenter rapidement des scénarios de gestion des identités et des accès"
services: active-directory
keywords: azure active directory, manuel, preuve de concept, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Ingrédients du manuel de preuve de concept Azure Active Directory 

## <a name="theme"></a>Thème
Azure AD fournit des solutions d’identité et accès dans plusieurs domaines d’entreprise de hello. Nous allons classifier scénarios hello Bonjour suivant de zones : 

* [Un grand nombre d’applications, une seule identité](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [Augmenter la sécurité](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [Mettre à l’échelle avec le libre-service](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

Définissez un Bonjour de tooframe de thème que preuve de concept vous aide aux efforts de hello toofocus correspond aux attentes des objectifs de l’entreprise, qui sont souvent déclencheurs hello intérêt hello dans une preuve de concept dans le premier emplacement dans hello. 

## <a name="environment"></a>Environnement

Il est important toodetermine hello des informations sur hello environnement où vous fournira hello preuve de concept. Dans l’idéal, vous pouvez générer lui après hello que preuve de concept est terminée. environnement cible de Hello est primordial et que vous devez rechercher hello juste équilibre entre effectuer il réel que possible et surcharge hello des contraintes ou des considérations supplémentaires. environnements de type Hello pour la validation des conceptions sont :
* **Production :** les scénarios hello sera implémentés dans votre environnement d’exploitation et déjà déployé les services de Cloud Microsoft (solution de production AD, Office 365, Azure AD client / l’authentification unique). 
* **Test d’acceptation utilisateur (UAT)/Environnement de développement :** Vous disposez d’une infrastructure de test (Active Directory et éventuellement une solution SSO/client Azure AD en parallèle) avec des données de test qui ressemblent à celles de production. En général, environnement de test hello est partagé entre plusieurs projets dans l’entreprise de hello.

La plupart des scénarios de ce guide sont additifs par nature. Par conséquent, ils peuvent être déployés dans le client de production hello sans affecter les utilisateurs en dehors de la preuve de concept de hello. Dans ce document, nous évoquerons les scénarios qui auraient un impact sur l’ensemble du client. Dans ce cas, vous pourriez tooconsider un environnement hors production. 


## <a name="target-users"></a>Utilisateurs cible

Il est le jeu de cibles hello toodetermine important d’utilisateurs qui vérifient les scénarios de hello, en particulier lorsque l’environnement de hello est production ou test. Hello des catégories d’utilisateurs cibles de preuve de concept sont :
* **Utilisateurs du pilote :** fonctions de travail des utilisateurs réels dans l’environnement hello qui utilisent des solutions de hello avec compte hello qu’ils utilisent pour leur tooday jour
* **Les utilisateurs de test :** comptes créés dans hello environnement de Test 

La plupart des scénarios de ce guide peuvent être réalisés par des utilisateurs du pilote. Dans ce document, nous évoquerons les considérations relatives aux utilisateurs cible si nécessaire.


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]