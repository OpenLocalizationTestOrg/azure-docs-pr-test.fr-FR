---
title: "aaaHow tooperform une vérification de l’accès | Documents Microsoft"
description: "Découvrez comment tooperform un réexamen avec hello application d’Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a>Comment tooperform un accès passez en revue dans Azure AD Privileged Identity Management
Azure Active Directory (AD) Privileged Identity Management simplifie comment gérer les entreprises tooresources accès privilégié dans Azure AD et autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.  

Si vous êtes affecté le rôle d’administrateur de tooan, l’administrateur de votre organisation rôle privilégié peut vous demander de tooregularly confirmer que vous devez toujours ce rôle pour votre travail. Vous pouvez obtenir un message électronique contenant un lien, ou vous pouvez accéder droite toohello [portail Azure](https://portal.azure.com). Suivez les étapes de hello dans cette tooperform article automatique examiner vos rôles sont affectés.

Si vous êtes un administrateur de rôle privilégié intéressé par accès révisions, obtenir plus de détails à [façon toostart examiner un accès](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-hello-privileged-identity-management-application"></a>Ajouter une application de Privileged Identity Management hello
Vous pouvez utiliser l’application de gestion d’identité privilégié (PIM) hello Azure AD Bonjour [portail Azure](https://portal.azure.com/) tooperform les examiner.  Si vous n’avez application Azure AD Privileged Identity Management de hello sur votre portail, suivez ces tooget étapes a démarré.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez votre nom d’utilisateur dans hello coin supérieur droit de hello portail Azure et répertoire hello sélectionnez où vous allez être fonctionne.
3. Sélectionnez **davantage de services** et utiliser toosearch de zone de texte de filtre hello pour **Azure AD Privileged Identity Management**.
4. Vérifiez **code confidentiel toodashboard** puis cliquez sur **créer**. Hello application de Privileged Identity Management s’ouvre.

## <a name="approve-or-deny-access"></a>Approuver ou refuser l'accès
Lorsque vous approuvez ou refusez l’accès, vous indiquez simplement réviseur de hello si vous utilisez toujours ce rôle ou non. Choisissez **approuver** si vous souhaitez que toostay dans le rôle de hello, ou **Deny** si vous ne devez hello accès plus. Votre état ne changera pas tout de suite, jusqu'à ce que le réviseur de hello applique les résultats hello.
Suivez ces étapes toofind et terminer la vérification de l’accès hello :

1. Bonjour application PIM, sélectionnez **révision d’un accès privilégié**. Si vous disposez de toutes les révisions en attente d’accès, ils apparaissent Bonjour Qu'azure AD Access passe en revue le panneau.
2. Sélectionnez la révision hello souhaité toocomplete.
3. Sauf si vous avez créé la révision de hello, vous apparaissez comme hello uniquement l’utilisateur en cours de révision de hello. Sélectionnez le nom de tooyour suivant hello case à cocher.
4. Choisissez **Approuver** ou **Refuser**. Vous devrez peut-être tooinclude raison de votre décision Bonjour **fournir une raison** zone de texte.  
5. Fermer hello **rôles Azure AD** panneau.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
