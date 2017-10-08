---
title: emplacements aaaNamed dans Azure Active Directory | Documents Microsoft
description: "En configurant les emplacements nommés, vous pouvez éviter d’avoir des IP adresses qui sont détenus par votre organisation générant des faux positifs pour les emplacements de tooatypical hello voyage Impossible du type d’événement risque."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Emplacements nommés dans Azure Active Directory

Avec hello nommé fonctionnalité emplacements d’Azure Active Directory, vous pouvez étiqueter des plages d’adresses IP approuvées dans votre organisation. Dans votre environnement, vous pouvez utiliser les emplacements nommés dans le contexte de hello de détection hello de [risque d’événements](active-directory-reporting-risk-events.md). fonctionnalité de Hello contribue à réduire hello de fausses signalés pour hello *emplacements de voyage Impossible tooatypical* risque de type d’événement. 

## <a name="configuration"></a>Configuration

tooconfigure un emplacement nommé :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur global.

2. Dans le volet gauche de hello, cliquez sur **Azure Active Directory**.

    ![lien d’Azure Active Directory Hello dans le volet gauche de hello](./media/active-directory-named-locations/01.png)

3. Sur hello **Azure Active Directory** panneau, Bonjour **sécurité** , cliquez sur **accès conditionnel**.

    ![Hello, la commande d’accès conditionnel](./media/active-directory-named-locations/05.png)


4. Sur hello **accès conditionnel** panneau, Bonjour **gérer** , cliquez sur **emplacements nommés**.

    ![Hello nommé emplacements commande](./media/active-directory-named-locations/06.png)


5. Sur hello **emplacements nommés** panneau, cliquez sur **nouvel emplacement**.

    ![Hello nouvelle commande de l’emplacement](./media/active-directory-named-locations/07.png)


6. Sur hello **nouveau** panneau, hello suivant :

    ![Nouveau panneau de Hello](./media/active-directory-named-locations/08.png)

    a. Bonjour **nom** , tapez un nom pour votre emplacement nommé.

    b. Bonjour **plages IP** , tapez une plage IP. plage d’adresses IP Hello doit toobe Bonjour *inter-Domain Routing* format (CIDR).  

    c. Cliquez sur **Create**.



## <a name="what-you-should-know"></a>Ce que vous devez savoir

**Les mises à jour en bloc de**: lorsque vous créez ou mettez à jour les emplacements nommés, pour les mises à jour en bloc, vous pouvez télécharger ou télécharger un fichier CSV avec des plages IP hello. Un téléchargement ajoute des plages d’adresses IP hello dans la liste toohello des fichiers hello au lieu de remplacer la liste de hello.

![Hello télécharger des liens](./media/active-directory-named-locations/09.png)


**Limitations**: vous pouvez définir un maximum de 60 emplacements nommés, avec un tooeach de plage affectée IP d'entre eux. Si vous avez qu’un seul emplacement nommé configuré, vous pouvez définir des plages d’adresses IP too500 pour celle-ci.


## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les événements à risque, consultez [événements à risque Azure Active Directory](active-directory-reporting-risk-events.md).

