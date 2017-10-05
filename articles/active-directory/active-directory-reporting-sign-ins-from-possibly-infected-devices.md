---
title: "Connexions à partir de périphériques potentiellement infectés"
description: "Un rapport incluant des tentatives de connexion effectuées à partir d’appareils sur lesquels des logiciels malveillants peuvent être exécutés."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: d0361662-d970-4a66-8eb3-72e9f8824dcf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 3809e20937d8d9829675e20f893101cb849dcea2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-possibly-infected-devices"></a><span data-ttu-id="79639-103">Connexions à partir de périphériques potentiellement infectés</span><span class="sxs-lookup"><span data-stu-id="79639-103">Sign ins from possibly infected devices</span></span>
<span data-ttu-id="79639-104">Ce rapport tente d’identifier les appareils des utilisateurs qui ont été infectés et font à présent partie d’un botnet.</span><span class="sxs-lookup"><span data-stu-id="79639-104">This report attempts to identify your users' devices that that have become infected and are now part of a botnet.</span></span> <span data-ttu-id="79639-105">Nous mettons en corrélation les adresses IP des connexions utilisateur et les adresses IP déterminées comme étant en contact avec des serveurs botnet.</span><span class="sxs-lookup"><span data-stu-id="79639-105">We correlate IP addresses of users' sign-ins against IP addresses that we know to be in contact with botnet servers.</span></span>

<span data-ttu-id="79639-106">Recommandation : ce rapport suit les adresses IP et non les appareils des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="79639-106">Recommendation: This report flags IP addresses, not user devices.</span></span> <span data-ttu-id="79639-107">Nous vous recommandons de contacter l'utilisateur et d'analyser tous ses appareils afin d’en acquérir la certitude.</span><span class="sxs-lookup"><span data-stu-id="79639-107">We recommend that you contact the user and scan all the user's devices to be certain.</span></span> <span data-ttu-id="79639-108">Il est également possible que les appareils personnels d'un utilisateur soient infectés, ou qu'une tierce personne utilisant la même adresse IP possède un appareil infecté.</span><span class="sxs-lookup"><span data-stu-id="79639-108">It is also possible that a user's personal device is infected, or that someone other than the user, who was using the same IP address as the user, has an infected device.</span></span>

<span data-ttu-id="79639-109">Pour plus d'informations sur le traitement des infections de logiciels malveillants, consultez le [Centre de protection contre les programmes malveillants](http://go.microsoft.com/fwlink/?linkid=335773).</span><span class="sxs-lookup"><span data-stu-id="79639-109">For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773).</span></span>

![Connexions à partir de périphériques potentiellement infectés](./media/active-directory-reporting-sign-ins-from-possibly-infected-devices/signInsFromPossiblyInfectedDevices.PNG)

