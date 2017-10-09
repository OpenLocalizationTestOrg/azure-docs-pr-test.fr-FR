---
title: "aaaEstimate l’utilisation de la bande passante du réseau Azure RemoteApp | Documents Microsoft"
description: "En savoir plus sur les besoins en bande passante réseau hello pour vos applications et les collections Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Estimation de l’utilisation de la bande passante réseau Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp utilise toocommunicate du protocole RDP (Remote Desktop) hello entre les applications exécutées dans hello Azure cloud et vos utilisateurs. Cet article fournit des recommandations de base vous permet de tooestimate que l’utilisation du réseau et potentiellement évaluent l’utilisation de la bande passante réseau par l’utilisateur d’Azure RemoteApp.

L’estimation de l’utilisation de la bande passante par utilisateur est très complexe et nécessite l’exécution simultanée de plusieurs applications dans des scénarios multitâche où chaque application peut avoir un impact sur les performances d’une autre, en fonction de leurs besoins en matière de bande passante réseau. Type même hello du client Bureau à distance (par exemple, le client Mac et client HTML5) peut entraîner des résultats de la bande passante toodifferent. toohelp que vous parcourez ces complications, nous allons arrêter des scénarios d’utilisation hello dans plusieurs scénarios du monde réel tooreplicate hello courants catégories. (Où la réalité hello est bien sûr, une combinaison de catégories et diffère par l’utilisateur.)

Avant d’aller plus - Notez que nous partons du principe RDP fournit une expérience tooexcellent correct pour la plupart des scénarios d’utilisation sur les réseaux avec une latence inférieure à 120 ms et la bande passante plus de 5 Mo - basée sur toodynamically de capacité de RDP ajuster à l’aide de réseau disponible de hello la bande passante et hello estimé des besoins en bande passante application. Cet article va au-delà de celles toolook « la plupart des scénarios d’utilisation » sur le périmètre de hello, où toounwind de démarrage des scénarios et l’expérience utilisateur commence toodegrade.

À présent extraire hello suivant des articles pour plus d’informations hello, y compris les facteurs tooconsider, des recommandations de ligne de base et ce que nous n’incluait pas nos estimations.

* [Quelle est la corrélation entre la bande passante réseau et la qualité de l’expérience d’utilisation ?](remoteapp-bandwidthexperience.md)
* [Test de votre bande passante réseau avec quelques scénarios courants](remoteapp-bandwidthtests.md)
* [Instructions rapides si vous n’avez pas tootest de temps ou la possibilité de hello](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>Quels sont les éléments que nous n’avons pas inclus ?
Lorsque vous examinez hello proposé de tests et nos recommandations globales (et il est vrai que génériques), n’oubliez pas qu’il n’y a plusieurs facteurs qui nous n’a pas compte. Par exemple, hello complications d’expérience utilisateur fournies par nature asymétrique de hello du téléchargement et la bande passante de téléchargement. nature asymétrique de Hello de la plupart des réseaux Wi-Fi plus impact sur les performances de hello et la perception d’expérience utilisateur hello. Pour les scénarios interactives le trafic en aval de hello peut-être être hiérarchisé inférieure à hello en amont, ce qui peut augmenter le nombre hello de trames de vidéo ou audio perdues et par conséquent avoir un impact sur perception d’utilisateur hello Hello expérience de diffusion en continu. Vous pouvez exécuter vos propres toosee expériences ce qui est approprié pour le cas d’usage spécifique et le réseau.

Bien que nous évoquer la redirection du périphérique, nous ne prenaient pas en considération hello bande passante du trafic réseau de hello dû à des appareils connectés, tels que le stockage, les imprimantes, les scanneurs, les caméras web et les autres périphériques USB. effet Hello de ces appareils généralement pics temporairement les besoins en bande passante hello et disparaît lors de la tâche hello est terminée. Mais dans le cas d’une utilisation fréquente, la demande en bande passante pourrait être relativement importante.

Nous ne traitent pas comment un utilisateur peut affecter les autres utilisateurs au sein de hello même réseau. Par exemple, un utilisateur consomme vidéo de 4 Ko sur un réseau de Mo/s 100 susceptibles de dégrader considérablement des autres utilisateurs sur le même réseau lors de la tentative toodo hello même tâche. Malheureusement, il obtient impact de hello toodetermine progressivement plus difficile d’utilisation simultanée toogive une recommandation commune ou complète sur le fonctionnement d’un système de hello au niveau de l’agrégat. Nous pouvons dire il suffit que hello protocole technologie sous-jacente rendent hello meilleur parti de la bande passante du réseau disponible hello, mais elle a ses limites.

