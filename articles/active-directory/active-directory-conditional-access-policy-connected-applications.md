---
title: "stratégies d’accès conditionnel périphérique Azure Active Directory aaaConfigure | Documents Microsoft"
description: "Découvrez comment stratégies d’accès conditionnel de périphérique Azure Active Directory tooconfigure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Configurer les stratégies d’accès conditionnel basé sur les appareils dans Azure Active Directory

Avec l’[accès conditionnel Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), vous pouvez préciser les méthodes d’accès des utilisateurs autorisés aux ressources. Par exemple, vous limitez hello aux toocertain ressources tootrusted appareils. Une stratégie d’accès conditionnel qui requiert un appareil de confiance est aussi appelée stratégie d’accès conditionnel basé sur les appareils.

Cette rubrique fournit des informations sur comment stratégies pour les applications Azure AD connectés d’accès conditionnel basé sur le périphérique de tooconfigure. 


## <a name="before-you-begin"></a>Avant de commencer

L’accès conditionnel basé sur les appareils fait le lien entre l’**accès conditionnel Azure AD** et la **gestion des appareils Azure AD**. Si vous n’êtes pas familiarisé avec une de ces zones, vous devez lire hello suivant rubriques, tout d’abord :

- **[Accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -cette rubrique fournit d’une vue d’ensemble conceptuelle de la condition d’accès et hello la terminologie associée.

- **[Gestion de toodevice introduction dans Azure Active Directory](device-management-introduction.md)**  -cette rubrique fournit une vue d’ensemble de hello différentes options vous disposez de périphériques tooconnect avec Azure AD. 


## <a name="trusted-devices"></a>Appareils de confiance

Dans un monde mobile en premier, privilégie le cloud, Azure Active Directory permet toodevices de l’authentification unique, les applications et services à partir de n’importe quel endroit. Pour certaines ressources dans votre environnement, accorder l’accès aux utilisateurs de droite toohello peut-être pas suffisant. En outre toohello des utilisateurs appropriés, vous pouvez également nécessiter qu'un toobe appareil de confiance utilisé tooaccess une ressource. Dans votre environnement, vous pouvez définir un appareil de confiance qui est basé sur hello suivants des composants :

- Hello [plateformes d’appareils](active-directory-conditional-access-azure-portal.md#device-platforms) sur un appareil
- Si un appareil est conforme ou non
- Si un appareil est joint à un domaine 

Hello [plateformes d’appareils](active-directory-conditional-access-azure-portal.md#device-platforms) se caractérise par le système d’exploitation hello qui s’exécute sur votre appareil. Dans votre stratégie d’accès conditionnel basés sur un appareil, vous pouvez limiter l’accès toocertain ressources toospecific des plateformes d’appareils.



Dans une stratégie d’accès conditionnel basés sur un appareil, vous pouvez exiger toobe appareils de confiance marqué comme conforme.

![Applications cloud](./media/active-directory-conditional-access-policy-connected-applications/24.png)

Les appareils peuvent être marqués comme conformes dans le répertoire hello par :

- Intune 
- Un système de gestion de périphériques mobile tiers qui s’intègre avec Azure AD  

Seuls les appareils qui sont connecté tooAzure AD peuvent être marqués comme conformes. tooconnect un tooAzure périphérique Active Directory, vous avez hello options suivantes : 

- Appareils inscrits sur Azure AD
- Appareil joints Azure AD
- Appareils joints Azure AD hybrides

    ![Applications cloud](./media/active-directory-conditional-access-policy-connected-applications/26.png)

Si vous avez un encombrement de Active Directory (AD) local, vous pouvez envisager d’appareils qui ne sont pas connecté tooAzure AD mais toobe tooyour jointes AD approuvé.

![Applications cloud](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>Étapes suivantes

Avant de configurer une stratégie d’accès conditionnel basés sur l’appareil dans votre environnement, vous devez examiner hello [meilleures pratiques pour l’accès conditionnel dans Azure Active Directory](active-directory-conditional-access-best-practices.md).

