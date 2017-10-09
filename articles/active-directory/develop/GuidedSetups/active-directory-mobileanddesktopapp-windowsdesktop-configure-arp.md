---
title: aaaAzure AD v2 Windows Desktop mise en route - Config | Documents Microsoft
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
ms.openlocfilehash: d96d9eded200824a6f7ee234009dd0bb11b18b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="06048-103">Ajouter une application de l’application hello d’enregistrement d’informations tooyour</span><span class="sxs-lookup"><span data-stu-id="06048-103">Add hello application’s registration information tooyour app</span></span>
<span data-ttu-id="06048-104">Dans cette étape, vous avez besoin d’un projet de tooyour tooadd hello Id d’Application.</span><span class="sxs-lookup"><span data-stu-id="06048-104">In this step, you need tooadd hello Application Id tooyour project.</span></span>

1.  <span data-ttu-id="06048-105">Ouvrez `App.xaml.cs` et remplacez la ligne hello contenant hello `ClientId` avec :</span><span class="sxs-lookup"><span data-stu-id="06048-105">Open `App.xaml.cs` and replace hello line containing hello `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="06048-106">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06048-106">What is Next</span></span>

[<span data-ttu-id="06048-107">Test et validation</span><span class="sxs-lookup"><span data-stu-id="06048-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
