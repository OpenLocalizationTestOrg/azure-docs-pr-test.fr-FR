---
title: "la bande passante de réseau aaaAzure RemoteApp - recommandations générales | Documents Microsoft"
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
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="ab651-103">Bande passante réseau Azure RemoteApp : instructions générales (si vous ne pouvez pas tester votre propre bande passante)</span><span class="sxs-lookup"><span data-stu-id="ab651-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ab651-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="ab651-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ab651-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ab651-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ab651-106">Si vous n’avez pas hello de hello heure ou la fonctionnalité de toorun [les tests de la bande passante du réseau](remoteapp-bandwidthtests.md) pour Azure RemoteApp, voici quelques indications assez génériques qui peuvent vous aider à estimer la bande passante réseau par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ab651-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="ab651-107">Si vous avez un mélange de ces scénarios, nous ne recommandons pas quoi que ce soit inférieur (ou égal à) 10 Mo/s comme hello la bande passante du réseau au MINIMUM pour les applications modernes connecté à Internet dans un environnement distant.</span><span class="sxs-lookup"><span data-stu-id="ab651-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="ab651-108">(Bien que, comme indiqué, cela ne garantit pas une expérience utilisateur supérieure à la moyenne.)</span><span class="sxs-lookup"><span data-stu-id="ab651-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="ab651-109">PowerPoint complexe, PowerPoint simple</span><span class="sxs-lookup"><span data-stu-id="ab651-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="ab651-110">Les performances d’Azure RemoteApp sont optimales sur un réseau local de 100 Mo.</span><span class="sxs-lookup"><span data-stu-id="ab651-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="ab651-111">À hello 10 Mo/profil de réseau s, lorsque l’instabilité ci-dessus 120 ms est plus de 5 %, utilisateur de hello verront une expérience moyenne.</span><span class="sxs-lookup"><span data-stu-id="ab651-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="ab651-112">À 1 hello de Mo/s différente est éblouissants - par exemple, dans un diaporama, utilisateur de hello ne soient pas visibles des transitions animées du tout, car les images sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="ab651-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="ab651-113">Internet Explorer, PDF mixte, PDF, texte</span><span class="sxs-lookup"><span data-stu-id="ab651-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="ab651-114">Profil de réseau 10 Mo/s est tooLAN Fermer dans la plupart des aspects.</span><span class="sxs-lookup"><span data-stu-id="ab651-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="ab651-115">1 Mo/s fournit une expérience OK, bien qu’il peut y avoir une instabilité dans le cas lorsqu’un utilisateur fait défiler bien qu’il existe des images sur l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="ab651-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="ab651-116">Vidéo flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="ab651-116">Flash video (YouTube)</span></span>
<span data-ttu-id="ab651-117">100 Mo/s LAN fournit hello meilleure expérience utilisateur, alors que 10 Mo/s est acceptable (c'est-à-dire nous suivre la cadence hello mais instabilité augmente).</span><span class="sxs-lookup"><span data-stu-id="ab651-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="ab651-118">À 1 Mbit/s, l’instabilité est très élevée et se remarque.</span><span class="sxs-lookup"><span data-stu-id="ab651-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="ab651-119">Frappe dans Word (saisie à distance dans Word)</span><span class="sxs-lookup"><span data-stu-id="ab651-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="ab651-120">Il s’agit d’un scénario d’utilisation à bande passante faible.</span><span class="sxs-lookup"><span data-stu-id="ab651-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="ab651-121">À 256 Kbits/s, l’expérience est aussi bonne que sur un réseau local.</span><span class="sxs-lookup"><span data-stu-id="ab651-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="ab651-122">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="ab651-122">Learn more</span></span>
* [<span data-ttu-id="ab651-123">Estimation de l’utilisation de la bande passante réseau Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ab651-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="ab651-124">Azure RemoteApp : quelle est la corrélation entre la bande passante réseau et la qualité de l’expérience d’utilisation ?</span><span class="sxs-lookup"><span data-stu-id="ab651-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="ab651-125">Azure RemoteApp : test de votre bande passante réseau avec quelques scénarios courants</span><span class="sxs-lookup"><span data-stu-id="ab651-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

