---
title: applications aaaUsing App-V avec Azure RemoteApp | Documents Microsoft
description: "Découvrez comment les applications toouse App-V dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Utilisation d'applications App-V dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Vous pouvez utiliser des applications App-V dans une collection hybride Azure RemoteApp, ce qui nécessite la jonction de domaine.

Avant de commencer, assurez-vous que client App-V 5.1 de hello tooinstall avec les dernières mises à jour de hello. Vous devez toocreate une [image personnalisée](remoteapp-create-custom-image.md) qui inclut le client de hello App-V.  

Il est facile toouse votre infrastructure App-V avec Azure RemoteApp. Comme une collection hybride est déployée dans un réseau virtuel Azure qui est contrôleur de domaine de l’accès tooyour et machines virtuelles de hello sont joints à un domaine, vous pouvez exploiter votre existante application App-v infrastructure et de déploiement méthodes tooeasyily hôte App-V dans Azure RemoteApp. Voici quelques considérations que vous devez connaître en fonction de type hello du déploiement d’App-V qu'est actuellement :

| Options de configuration |  | Positive | Negative |
| --- | --- | --- | --- |
| Méthode de remise |Diffusion en continu (à la demande) |Application est toujours hello nouvelle et plus récents |Première latence |
| Montée |Plus rapide ; application est déjà présente sur hello machine virtuelle |Encombrement - occupe de l'espace image (limite 127 Go) | |
| Stockage de l'emplacement d'application |Contenu partagé |L'application est exécutée dans la mémoire de l'instance Azure RemoteApp |Mange mémoire et la bonne connexion du serveur toostreaming (fichier) à l’emplacement de l’application hello |
| Disque (en cache) |Exécution rapide. L'application ne dépend pas de la disponibilité du contenu source |Encombrement - occupe de l'espace image (limite 127 Go) | |
| Ciblage |Utilisateur |Nécessite une infrastructure App-V entièrement autonome | |
| Global (machine) |Pré-publication ou cible avec le serveur de publication |Devez tooupdate votre image Azure si vous souhaitez tooupdate hello application (énorme). Occupe de l'espace sur l'image. | |

 Après avoir créé votre image personnalisée de votre collection hybride, publiez votre application, affecter des utilisateurs et profitez de vos applications App-V existantes hébergées dans Azure RemoteApp remis appareil tooany n’importe où.

