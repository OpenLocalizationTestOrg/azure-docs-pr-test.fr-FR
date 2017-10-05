---
title: "Prise en main d’Azure AD dans les projets Visual Studio WebApi | Microsoft Docs"
description: "Comment prendre en main Azure Active Directory dans les projets WebApi après s’être connecté à un annuaire Azure AD ou avoir créé un annuaire Azure AD à l’aide des services connectés de Visual Studio"
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
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="9b655-103">Prendre en main Azure Active Directory et les services connectés de Visual Studio (projets WebApi)</span><span class="sxs-lookup"><span data-stu-id="9b655-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b655-104">Prise en main</span><span class="sxs-lookup"><span data-stu-id="9b655-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="9b655-105">Que s'est-il passé ?</span><span class="sxs-lookup"><span data-stu-id="9b655-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="9b655-106">Demander une authentification pour l'accès aux contrôleurs</span><span class="sxs-lookup"><span data-stu-id="9b655-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="9b655-107">Tous les contrôleurs de votre projet ont été dotés de l'attribut **Authorize** .</span><span class="sxs-lookup"><span data-stu-id="9b655-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="9b655-108">Cet attribut permet de demander à l’utilisateur de s’authentifier avant d’accéder aux API définies par ces contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="9b655-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="9b655-109">Pour autoriser un accès anonyme au contrôleur, cet attribut doit être supprimé du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="9b655-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="9b655-110">Pour définir plus précisément les autorisations, appliquez cet attribut à chaque méthode nécessitant une autorisation, au lieu de l’appliquer à la classe de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="9b655-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b655-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b655-111">Next steps</span></span>
[<span data-ttu-id="9b655-112">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b655-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

