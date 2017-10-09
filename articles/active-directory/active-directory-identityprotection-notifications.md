---
title: "notifications de la Protection d’identité Active Directory aaaAzure | Documents Microsoft"
description: "Découvrez comment les notifications prennent en charge vos activités d’examen."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a>Notifications d’Azure Active Directory Identity Protection
Azure AD Identity Protection envoie deux types de notification automatisé des e-mails toohelp que vous gérez risque d’utilisateur et les événements à risque :

* E-mail d’alerte en cas d’utilisateur compromis
* E-mail de synthèse hebdomadaire

## <a name="user-compromised-alert-email"></a>E-mail d’alerte en cas d’utilisateur compromis
Un e-mail d’alerte en cas d’utilisateur compromis est généré lorsqu’Azure AD Identity Protection identifie un compte compromis. messagerie de Hello inclut un toohello lien Qu'utilisateurs marqués en vue d’état risque dans le tableau de bord hello Identity Protection. Nous vous recommandons d’examiner immédiatement les notifications des comptes compromis.

## <a name="weekly-digest-email"></a>E-mail de synthèse hebdomadaire
e-mail de résumé hebdomadaire Hello contient un résumé des nouveaux événements de risque.<br>
Il inclut :

* Les utilisateurs à risque
* Activités suspectes
* Les vulnérabilités détectées
* Liens toohello liées dans la Protection de l’identité des rapports

<br>
![Mise à jour](./media/active-directory-identityprotection-notifications/400.png "mise à jour")
<br>

Vous pouvez désactiver l’envoi de l’e-mail de synthèse hebdomadaire.
<br><br>
![Risques pour l’utilisateur](./media/active-directory-identityprotection-notifications/62.png "risques pour l’utilisateur")
<br>

**boîte de dialogue configuration associés tooopen hello**:

1. Sur hello **Azure AD Identity Protection** panneau, cliquez sur **paramètres**.
   <br><br>
   ![Stratégie des risques utilisateur](./media/active-directory-identityprotection-notifications/401.png "stratégie risque de l’utilisateur")
   <br>
2. Bonjour **général** , cliquez sur **Notifications**.
   <br><br>
   ![Stratégie des risques utilisateur](./media/active-directory-identityprotection-notifications/405.png "stratégie risque de l’utilisateur")
   <br>

## <a name="see-also"></a>Voir aussi
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
