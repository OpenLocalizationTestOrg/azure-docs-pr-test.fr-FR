---
title: "aaaGet démarré avec Azure AD dans les projets Visual Studio WebApi | Documents Microsoft"
description: "Comment tooget démarrer à l’aide d’Azure Active Directory dans les projets WebApi après la connexion tooor création d’un répertoire Azure AD à l’aide de Visual Studio services connectés"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 21413a71a2fd61f31268bf6d5e4d86b8be5bd16a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a>Prendre en main Azure Active Directory et les services connectés de Visual Studio (projets WebApi)
> [!div class="op_single_selector"]
> * [Prise en main](vs-active-directory-webapi-getting-started.md)
> * [Que s'est-il passé ?](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>Contrôleurs de tooaccess nécessitant une authentification
Tous les contrôleurs dans votre projet ont été dotées de hello **Authorize** attribut. Cet attribut requiert hello toobe d’utilisateur authentifié avant que l’accès aux API de hello définies par ces contrôleurs. tooallow hello contrôleur toobe accessible de manière anonyme, supprimez cet attribut à partir du contrôleur de hello. Si vous souhaitez que les autorisations de hello tooset à un niveau plus granulaire, appliquer hello attribut tooeach méthode qui nécessite une autorisation au lieu de la classe de contrôleur toohello son application.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

