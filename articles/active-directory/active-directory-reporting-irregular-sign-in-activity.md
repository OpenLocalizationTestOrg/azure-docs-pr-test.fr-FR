---
title: "Activité de connexion anormale"
description: "Un rapport qui inclut des connexions qui ont été identifiées comme « anormales » par nos algorithmes d'apprentissage automatique (Machine Learning)."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a><span data-ttu-id="e2b48-103">Activité de connexion anormale</span><span class="sxs-lookup"><span data-stu-id="e2b48-103">Irregular sign-in activity</span></span>
<span data-ttu-id="e2b48-104">Les connexions irrégulières sont celles qui ont été identifiées par nos algorithmes d’apprentissage automatique, sur la base d'une condition de « déplacement impossible » associée à un emplacement et un périphérique de connexion anormaux.</span><span class="sxs-lookup"><span data-stu-id="e2b48-104">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign in location and device.</span></span> <span data-ttu-id="e2b48-105">Cela peut signifier qu'un pirate est parvenu à se connecter à l'aide de ce compte.</span><span class="sxs-lookup"><span data-stu-id="e2b48-105">This may indicate that a hacker has successfully signed in using this account.</span></span>
<span data-ttu-id="e2b48-106">Nous envoyons une notification par courrier électronique aux administrateurs globaux si nous trouvons au moins 10 événements de connexion anormaux dans un intervalle de moins de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="e2b48-106">We will send an email notification to the global admins if we encounter 10 or more anomalous sign-in events within a span of 30 days or less.</span></span> <span data-ttu-id="e2b48-107">Veillez à inclure aad-alerts-noreply@mail.windowsazure.com dans votre liste d'expéditeurs approuvés.</span><span class="sxs-lookup"><span data-stu-id="e2b48-107">Please be sure to include aad-alerts-noreply@mail.windowsazure.com in your safe senders list.</span></span>

