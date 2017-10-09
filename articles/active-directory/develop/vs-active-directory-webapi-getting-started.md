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
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="72859-103">Prendre en main Azure Active Directory et les services connectés de Visual Studio (projets WebApi)</span><span class="sxs-lookup"><span data-stu-id="72859-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72859-104">Prise en main</span><span class="sxs-lookup"><span data-stu-id="72859-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="72859-105">Que s'est-il passé ?</span><span class="sxs-lookup"><span data-stu-id="72859-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a><span data-ttu-id="72859-106">Contrôleurs de tooaccess nécessitant une authentification</span><span class="sxs-lookup"><span data-stu-id="72859-106">Requiring authentication tooaccess controllers</span></span>
<span data-ttu-id="72859-107">Tous les contrôleurs dans votre projet ont été dotées de hello **Authorize** attribut.</span><span class="sxs-lookup"><span data-stu-id="72859-107">All controllers in your project were adorned with hello **Authorize** attribute.</span></span> <span data-ttu-id="72859-108">Cet attribut requiert hello toobe d’utilisateur authentifié avant que l’accès aux API de hello définies par ces contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="72859-108">This attribute requires hello user toobe authenticated before accessing hello APIs defined by these controllers.</span></span> <span data-ttu-id="72859-109">tooallow hello contrôleur toobe accessible de manière anonyme, supprimez cet attribut à partir du contrôleur de hello.</span><span class="sxs-lookup"><span data-stu-id="72859-109">tooallow hello controller toobe accessed anonymously, remove this attribute from hello controller.</span></span> <span data-ttu-id="72859-110">Si vous souhaitez que les autorisations de hello tooset à un niveau plus granulaire, appliquer hello attribut tooeach méthode qui nécessite une autorisation au lieu de la classe de contrôleur toohello son application.</span><span class="sxs-lookup"><span data-stu-id="72859-110">If you want tooset hello permissions at a more granular level, apply hello attribute tooeach method that requires authorization instead of applying it toohello controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72859-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72859-111">Next steps</span></span>
[<span data-ttu-id="72859-112">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72859-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

