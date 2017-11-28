---
title: "Connexions après plusieurs échecs"
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
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="a9416-103">Connexions après plusieurs échecs</span><span class="sxs-lookup"><span data-stu-id="a9416-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="a9416-104">Ce rapport indique les utilisateurs qui sont parvenus à se connecter, mais après plusieurs tentatives de connexion infructueuses.</span><span class="sxs-lookup"><span data-stu-id="a9416-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="a9416-105">Les causes possibles sont :</span><span class="sxs-lookup"><span data-stu-id="a9416-105">Possible causes include:</span></span>

* <span data-ttu-id="a9416-106">L’utilisateur a oublié son mot de passe</span><span class="sxs-lookup"><span data-stu-id="a9416-106">User had forgotten their password</span></span></li><li><span data-ttu-id="a9416-107">Son mot de passe lui a été dérobé</span><span class="sxs-lookup"><span data-stu-id="a9416-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="a9416-108">Les résultats de ce rapport vous indiqueront le nombre de tentatives consécutives effectuées par l’utilisateur avant de parvenir à se connecter et l’horodatage associé à la première connexion réussie.</span><span class="sxs-lookup"><span data-stu-id="a9416-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="a9416-109">**Paramètres de rapport**: vous pouvez configurer le nombre minimal de tentatives de connexion infructueuses qui doivent être effectuées consécutivement avant d’apparaître dans le rapport.</span><span class="sxs-lookup"><span data-stu-id="a9416-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="a9416-110">Lorsque vous modifiez ce paramètre, il est important de savoir que ces modifications ne seront pas appliquées aux échecs de connexion existants qui sont déjà mentionnés dans un rapport existant.</span><span class="sxs-lookup"><span data-stu-id="a9416-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="a9416-111">Elles seront toutefois appliquées à toutes les connexions futures.</span><span class="sxs-lookup"><span data-stu-id="a9416-111">However, they will be applied to all future sign-ins.</span></span> <span data-ttu-id="a9416-112">Cependant, seuls les administrateurs titulaires d’une licence peuvent effectuer ces modifications.</span><span class="sxs-lookup"><span data-stu-id="a9416-112">Changes to this report can only be made by licensed admins.</span></span>

![Connexions après plusieurs échecs](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

