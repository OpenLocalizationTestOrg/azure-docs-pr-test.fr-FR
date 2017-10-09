---
title: "aaaSign connexions après plusieurs échecs"
description: "Un rapport indiquant les utilisateurs qui sont parvenus à se connecter, mais après plusieurs tentatives de connexion infructueuses."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="1ee19-103">Connexions après plusieurs échecs</span><span class="sxs-lookup"><span data-stu-id="1ee19-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="1ee19-104">Ce rapport indique les utilisateurs qui sont parvenus à se connecter, mais après plusieurs tentatives de connexion infructueuses.</span><span class="sxs-lookup"><span data-stu-id="1ee19-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="1ee19-105">Les causes possibles sont :</span><span class="sxs-lookup"><span data-stu-id="1ee19-105">Possible causes include:</span></span>

* <span data-ttu-id="1ee19-106">L’utilisateur a oublié son mot de passe</span><span class="sxs-lookup"><span data-stu-id="1ee19-106">User had forgotten their password</span></span></li><li><span data-ttu-id="1ee19-107">L’utilisateur est victime hello de mot de passe réussie estimation attaque en force brute</span><span class="sxs-lookup"><span data-stu-id="1ee19-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="1ee19-108">Les résultats de ce rapport affiche hello de nombre de consécutives ayant échoué tentatives de connexion effectuées toohello préalable réussie connectez-vous et un horodatage associé hello première réussie connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="1ee19-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="1ee19-109">**Paramètres de rapport**: vous pouvez configurer le nombre minimal de hello d’échecs de connexion consécutifs tentatives qui doit se produire avant d’être affichée dans le rapport de hello.</span><span class="sxs-lookup"><span data-stu-id="1ee19-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="1ee19-110">Lorsque vous apportez des modifications toothis définition est toonote important que ces modifications ne seront pas appliqué tooany existant ayant échoué connexions qui s’affichent actuellement dans votre rapport existant.</span><span class="sxs-lookup"><span data-stu-id="1ee19-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="1ee19-111">Toutefois, ils seront appliqués tooall futures connexions. Rapport sur toothis les modifications ne sont accessibles que par les administrateurs sous licence.</span><span class="sxs-lookup"><span data-stu-id="1ee19-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![Connexions après plusieurs échecs](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

