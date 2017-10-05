---
title: "Connexions depuis plusieurs zones géographiques"
description: "Un rapport qui indique les utilisateurs lorsque deux connexions semblent être issues de régions différentes, alors que le laps de temps constaté entre ces connexions ne permet pas à l'utilisateur de se rendre d'une région à une autre."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a><span data-ttu-id="08cd2-103">Connexions depuis plusieurs zones géographiques</span><span class="sxs-lookup"><span data-stu-id="08cd2-103">Sign-ins from multiple geographies</span></span>
<span data-ttu-id="08cd2-104">Ce rapport inclut les connexions réussies d’un utilisateur durant lesquelles deux connexions semblent être issues de régions différentes, mais dont le laps de temps constaté entre ces connexions ne permet pas à l’utilisateur de se rendre d’une région à une autre.</span><span class="sxs-lookup"><span data-stu-id="08cd2-104">This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions.</span></span> <span data-ttu-id="08cd2-105">Les causes possibles sont :</span><span class="sxs-lookup"><span data-stu-id="08cd2-105">Possible causes include:</span></span>

* <span data-ttu-id="08cd2-106">L’utilisateur partage son mot de passe avec d’autres utilisateurs</span><span class="sxs-lookup"><span data-stu-id="08cd2-106">User is sharing their password with other users</span></span>
* <span data-ttu-id="08cd2-107">L’utilisateur utilise un bureau à distance pour lancer un navigateur web pour la connexion</span><span class="sxs-lookup"><span data-stu-id="08cd2-107">User is using a remote desktop to launch a web browser for sign-in</span></span>
* <span data-ttu-id="08cd2-108">Un pirate s’est connecté au compte d’un utilisateur à partir d’un autre pays</span><span class="sxs-lookup"><span data-stu-id="08cd2-108">A hacker has signed in to the account of a user from a different country</span></span>
* <span data-ttu-id="08cd2-109">L’utilisateur utilise une connexion VPN ou proxy</span><span class="sxs-lookup"><span data-stu-id="08cd2-109">User is using a VPN or proxy</span></span>
* <span data-ttu-id="08cd2-110">L’utilisateur est connecté à partir de plusieurs appareils en même temps, par exemple un ordinateur de bureau et un téléphone mobile, et l’adresse IP du téléphone mobile est inhabituelle.</span><span class="sxs-lookup"><span data-stu-id="08cd2-110">User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.</span></span>

<span data-ttu-id="08cd2-111">Les résultats de ce rapport vous indiqueront les événements de connexion réussie, ainsi que le laps de temps entre les connexions, les régions d’où les connexions semblent être issues et le temps de trajet estimé entre ces régions.</span><span class="sxs-lookup"><span data-stu-id="08cd2-111">Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions.</span></span> <span data-ttu-id="08cd2-112">Le temps de trajet indiqué n’est qu’une estimation et peut être différent de la durée de voyage réelle entre les emplacements.</span><span class="sxs-lookup"><span data-stu-id="08cd2-112">The travel time shown is only an estimate and may be different from the actual travel time between the locations.</span></span>

![Connexions depuis plusieurs zones géographiques](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

