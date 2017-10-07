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
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Bande passante réseau Azure RemoteApp : instructions générales (si vous ne pouvez pas tester votre propre bande passante)
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Si vous n’avez pas hello de hello heure ou la fonctionnalité de toorun [les tests de la bande passante du réseau](remoteapp-bandwidthtests.md) pour Azure RemoteApp, voici quelques indications assez génériques qui peuvent vous aider à estimer la bande passante réseau par utilisateur.

Si vous avez un mélange de ces scénarios, nous ne recommandons pas quoi que ce soit inférieur (ou égal à) 10 Mo/s comme hello la bande passante du réseau au MINIMUM pour les applications modernes connecté à Internet dans un environnement distant. (Bien que, comme indiqué, cela ne garantit pas une expérience utilisateur supérieure à la moyenne.)

## <a name="complex-powerpoint-simple-powerpoint"></a>PowerPoint complexe, PowerPoint simple
Les performances d’Azure RemoteApp sont optimales sur un réseau local de 100 Mo. À hello 10 Mo/profil de réseau s, lorsque l’instabilité ci-dessus 120 ms est plus de 5 %, utilisateur de hello verront une expérience moyenne. À 1 hello de Mo/s différente est éblouissants - par exemple, dans un diaporama, utilisateur de hello ne soient pas visibles des transitions animées du tout, car les images sont ignorées.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, PDF mixte, PDF, texte
Profil de réseau 10 Mo/s est tooLAN Fermer dans la plupart des aspects. 1 Mo/s fournit une expérience OK, bien qu’il peut y avoir une instabilité dans le cas lorsqu’un utilisateur fait défiler bien qu’il existe des images sur l’écran hello.

## <a name="flash-video-youtube"></a>Vidéo flash (YouTube)
100 Mo/s LAN fournit hello meilleure expérience utilisateur, alors que 10 Mo/s est acceptable (c'est-à-dire nous suivre la cadence hello mais instabilité augmente). À 1 Mbit/s, l’instabilité est très élevée et se remarque.

## <a name="word-typing-word-remote-input"></a>Frappe dans Word (saisie à distance dans Word)
Il s’agit d’un scénario d’utilisation à bande passante faible. À 256 Kbits/s, l’expérience est aussi bonne que sur un réseau local.

## <a name="learn-more"></a>En savoir plus
* [Estimation de l’utilisation de la bande passante réseau Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp : quelle est la corrélation entre la bande passante réseau et la qualité de l’expérience d’utilisation ?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp : test de votre bande passante réseau avec quelques scénarios courants](remoteapp-bandwidthtests.md)

