---
title: "stratégies de rétention de rapport Active Directory aaaAzure | Documents Microsoft"
description: "Stratégies de rétention des données de rapport dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Stratégies de rétention des rapports Azure Active Directory


Cette rubrique fournit des réponses toohello des questions courantes conjointement avec conservation des données hello pour les rapports d’activité différente hello dans Azure Active Directory. 

**Q : comment obtenir collection hello de données d’activité a démarré ?**

**R :**

| Édition d’Azure AD | Début de la collection |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | Lorsque vous vous inscrivez pour un abonnement |
| Azure AD Gratuit | Hello la première fois que vous ouvrez hello [panneau d’Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) ou utilisez hello [API de création de rapports](https://aka.ms/aadreports)  |

---
**Q : quand vos données d’activité est disponible dans hello portail Azure ?**

**R :**

- **Immédiatement** : Si vous avez déjà travaillé avec des rapports Bonjour portail Azure classic
- **Dans les 2 heures** : Si vous n’avez pas activé la création de rapports Bonjour portail Azure classic

---
**Q : comment obtenir collection hello de signaux de sécurité a démarré ?**  

**R :** pour les signaux de sécurité, le processus de collecte hello démarre lorsque vous choisissez de participer toouse hello identité Protection Center. 


---
**Q : combien de temps est hello stockées les données collectées ?**

**R :**

**Rapports d’activité**    

| Rapport                 | Azure AD Gratuit | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Audit de répertoire        | 7 jours        | 30 jours             | 30 jours             |
| Activité de connexion       | 7 jours        | 30 jours             | 30 jours             |

**Signaux de sécurité**

| Rapport         | Azure AD Gratuit | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| Les utilisateurs à risque  | 7 jours        | 30 jours             | 90 jours             |
| Connexions risquées | 7 jours        | 30 jours             | 90 jours             |

---