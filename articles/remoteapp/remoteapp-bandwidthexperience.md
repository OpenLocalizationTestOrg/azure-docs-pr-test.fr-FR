---
title: "aaaAzure RemoteApp - comment la bande passante réseau et la qualité de profiter de travail ensemble ? | Microsoft Docs"
description: "Découvrez l’impact de la bande passante réseau dans Azure RemoteApp sur la qualité de l’expérience utilisateur."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp : quelle est la corrélation entre la bande passante réseau et la qualité de l’expérience d’utilisation ?
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Lorsque vous examinez hello [la bande passante de réseau global](remoteapp-bandwidth.md) requis pour Azure RemoteApp, conserver Bonjour esprit suivant facteurs - il s’agit de tous les font partie d’un système dynamique qu’impacts hello l’expérience utilisateur globale. 

* **Bande passante réseau disponible et les conditions réseau actuelles** -un ensemble de paramètres (perte, la latence, instabilité) sur le même réseau à un moment donné de hello peut affecter l’application hello expérience de diffusion en continu, ce qui signifie une expérience utilisateur globale garantie. la bande passante de Hello disponible dans votre réseau est une fonction de la congestion, perte aléatoire, la latence, car tous les paramètres suivants affectent mécanisme de contrôle de congestion hello, qui, dans les contrôles de l’activer, hello collisions de tooavoid de vitesse de transmission.  Par exemple, un réseau avec perte de données ou un réseau avec une latence élevée fera hello utilisateur expérience incorrecte même sur un réseau avec la bande passante de 1 000 Mo. perte de Hello et la latence varient en fonction de nombre de hello d’utilisateurs qui se trouvent sur hello même réseau et ce que font les utilisateurs (par exemple, visionner des vidéos, télécharger ou transférer des fichiers volumineux, impression).
* **Scénario d’utilisation** -expérience de hello dépend de quelles hello font les utilisateurs en tant qu’individus et en tant que groupe sur hello même réseau. Par exemple, la lecture d’une diapositive requiert uniquement un toobe frame unique mis à jour ; Si l’utilisateur de hello skims et fait défiler sur le contenu d’un document texte hello, ils ont besoin d’un nombre élevé de toobe frames mis à jour par seconde. Hello communication de retour et les deux sens serveur toohello dans ce scénario finira par consommer davantage de bande passante réseau. Envisagez également un exemple extrême : plusieurs utilisateurs visionnent des vidéos haute définition (résolution 4K, par exemple), organisent des téléconférences HD, jouent à des jeux vidéo 3D ou utilisent des systèmes de CAO. Tous ces éléments peuvent rendre même un réseau à bande passante réellement élevée pratiquement inutilisable.
* **Écran hello et la résolution nombre d’écrans** -davantage de bande passante réseau est requis toofull mise à jour des écrans plus grandes que les petits écrans. la technologie sous-jacente Hello élabore une assez bonne d’encodage et de transmettre uniquement les régions hello d’écrans hello qui ont été mis à jour, mais de temps, la totalité de l’écran hello doit toobe mis à jour. Lorsque l’utilisateur de hello a un écran de résolution plus élevé (par exemple résolution de 4 Ko), cette mise à jour nécessite davantage de bande passante réseau à un écran avec une résolution inférieure (par exemple, 1024x768px). Cette même logique s’applique si vous utilisez plusieurs écrans pour la redirection. Besoins en bande passante tooincrease avec nombre hello d’écrans.
* **La redirection du Presse-papiers et appareil** - il s’agit d’un problème de pas très évident, mais dans de nombreux cas si un utilisateur stocke une grande partie du Presse-papiers toohello de données, il faut un peu de temps pour cette tootransfer plus d’informations à partir du client de bureau à distance hello toohello server. expérience de Hello en aval peut être touché par expérience hello d’envoyer le contenu du Presse-papiers hello en amont. Hello valable pour la redirection du périphérique - si un analyseur webcam génère une grande quantité de données qui doit utiliser serveur en amont toohello toobe envoyé, ou tooreceive un document volumineux a besoin d’une imprimante ou application disponibles tooan toobe dans hello cloud toocopy nécessaire au stockage local un un fichier volumineux, les utilisateurs peuvent remarquer une perte d’images ou temporairement vidéo de « figé », car les données hello nécessaires pour la redirection du périphérique hello augmente la bande passante du réseau hello a besoin. 

Lorsque vous évaluez vos besoins en bande passante réseau, assurez-vous que tooconsider tous ces facteurs fonctionne comme un système.

Revenez maintenant, toohello [l’article de la bande passante réseau principal](remoteapp-bandwidth.md), ou déplacez tootesting votre [la bande passante réseau](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>En savoir plus
* [Estimation de l’utilisation de la bande passante réseau Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp : test de votre bande passante réseau avec quelques scénarios courants](remoteapp-bandwidthtests.md)
* [Bande passante réseau Azure RemoteApp : instructions générales (si vous ne pouvez pas tester votre propre bande passante)](remoteapp-bandwidthguidelines.md)

