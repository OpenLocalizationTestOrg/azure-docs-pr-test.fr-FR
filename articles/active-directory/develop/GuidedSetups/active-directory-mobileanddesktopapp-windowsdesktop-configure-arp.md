---
title: "Prise en main d’Azure AD v2 avec les applications de bureau Windows - Configuration | Microsoft Docs"
description: "Cet article explique comment une application de bureau Windows .NET (XAML) peut obtenir un jeton d’accès et appeler une API protégée par un point de terminaison Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 5e83171846517496e221f0a84565cdf7b77514df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="948a1-103">Ajouter les informations d’inscription de l’application à votre application</span><span class="sxs-lookup"><span data-stu-id="948a1-103">Add the application’s registration information to your app</span></span>
<span data-ttu-id="948a1-104">Dans cette étape, vous devez ajouter l’ID d’application à votre projet.</span><span class="sxs-lookup"><span data-stu-id="948a1-104">In this step, you need to add the Application Id to your project.</span></span>

1.  <span data-ttu-id="948a1-105">Ouvrez `App.xaml.cs` et remplacez la ligne contenant `ClientId` par :</span><span class="sxs-lookup"><span data-stu-id="948a1-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="948a1-106">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="948a1-106">What is Next</span></span>

[<span data-ttu-id="948a1-107">Test et validation</span><span class="sxs-lookup"><span data-stu-id="948a1-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
