---
title: "Bande passante réseau Azure RemoteApp : instructions générales | Microsoft Docs"
description: "Comprendre des instructions de base en matière de bande passante réseau pour vos applications et collections Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="22345-103">Bande passante réseau Azure RemoteApp : instructions générales (si vous ne pouvez pas tester votre propre bande passante)</span><span class="sxs-lookup"><span data-stu-id="22345-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="22345-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="22345-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="22345-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="22345-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="22345-106">Si vous n’avez pas le temps ou la possibilité d’exécuter les [tests de la bande passante réseau](remoteapp-bandwidthtests.md) pour Azure RemoteApp, voici quelques instructions relativement génériques qui peuvent vous aider à estimer la bande passante réseau par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22345-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="22345-107">Si vous avez une combinaison de ces scénarios, nous recommandons une bande passante réseau de 10 Mbits/s MINIMUM pour les applications modernes connectées à Internet dans un environnement à distance.</span><span class="sxs-lookup"><span data-stu-id="22345-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="22345-108">(Bien que, comme indiqué, cela ne garantit pas une expérience utilisateur supérieure à la moyenne.)</span><span class="sxs-lookup"><span data-stu-id="22345-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="22345-109">PowerPoint complexe, PowerPoint simple</span><span class="sxs-lookup"><span data-stu-id="22345-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="22345-110">Les performances d’Azure RemoteApp sont optimales sur un réseau local de 100 Mo.</span><span class="sxs-lookup"><span data-stu-id="22345-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="22345-111">Avec un profil réseau de 10 Mbits/s, lorsque l’instabilité supérieure à 120 ms est de plus de 5 %, l’expérience utilisateur sera moyenne.</span><span class="sxs-lookup"><span data-stu-id="22345-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="22345-112">À 1 Mbit/s, la différence est incontestable. Par exemple, dans un diaporama, l’utilisateur peut ne pas voir les transitions animées, car les images sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="22345-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="22345-113">Internet Explorer, PDF mixte, PDF, texte</span><span class="sxs-lookup"><span data-stu-id="22345-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="22345-114">Un profil réseau de 10 Mbits/s est similaire d’un réseau local sous bien des aspects.</span><span class="sxs-lookup"><span data-stu-id="22345-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="22345-115">1 Mbit/s offre une expérience acceptable, bien qu’une instabilité soit possible lorsqu’un utilisateur fait défiler du contenu alors que des images sont présentes à l’écran.</span><span class="sxs-lookup"><span data-stu-id="22345-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="22345-116">Vidéo flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="22345-116">Flash video (YouTube)</span></span>
<span data-ttu-id="22345-117">Un réseau local de 100 Mbits/s offre la meilleure expérience, alors qu’un réseau de 10 Mbits/s est acceptable (c’est-à-dire que le réseau peut suivre la fréquence des images mais l’instabilité augmente).</span><span class="sxs-lookup"><span data-stu-id="22345-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="22345-118">À 1 Mbit/s, l’instabilité est très élevée et se remarque.</span><span class="sxs-lookup"><span data-stu-id="22345-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="22345-119">Frappe dans Word (saisie à distance dans Word)</span><span class="sxs-lookup"><span data-stu-id="22345-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="22345-120">Il s’agit d’un scénario d’utilisation à bande passante faible.</span><span class="sxs-lookup"><span data-stu-id="22345-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="22345-121">À 256 Kbits/s, l’expérience est aussi bonne que sur un réseau local.</span><span class="sxs-lookup"><span data-stu-id="22345-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="22345-122">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="22345-122">Learn more</span></span>
* [<span data-ttu-id="22345-123">Estimation de l’utilisation de la bande passante réseau Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="22345-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="22345-124">Azure RemoteApp : quelle est la corrélation entre la bande passante réseau et la qualité de l’expérience d’utilisation ?</span><span class="sxs-lookup"><span data-stu-id="22345-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="22345-125">Azure RemoteApp : test de votre bande passante réseau avec quelques scénarios courants</span><span class="sxs-lookup"><span data-stu-id="22345-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

