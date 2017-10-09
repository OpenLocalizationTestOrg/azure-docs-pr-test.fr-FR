---
title: "aaaAccessing des Machines virtuelles Azure à partir de l’Explorateur de serveurs | Documents Microsoft"
description: "Obtenir une vue d’ensemble du mode de tooview créer et gérer des machines virtuelles Azure (VM) dans l’Explorateur de serveurs dans Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Accès aux machines virtuelles Azure à partir de l’Explorateur de serveurs
Grâce à l’Explorateur de serveurs dans Visual Studio, vous pouvez afficher des informations concernant vos machines virtuelles hébergées par Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Accès aux machines virtuelles dans l’Explorateur de serveurs
Si vous avez des machines virtuelles hébergées par Azure, vous pouvez y accéder depuis l’Explorateur de serveurs. Vous devez tout d’abord vous connecter tooyour abonnement Azure tooview vos services mobiles. toosign, ouvrez le menu contextuel hello hello nœud Azure dans l’Explorateur de serveurs, puis choisissez **connecter tooMicrosoft Azure**.

### <a name="tooget-information-about-your-virtual-machines"></a>tooget plus d’informations sur vos machines virtuelles
1. Dans l’Explorateur de serveurs, choisissez un ordinateur virtuel, puis tooshow de clé hello F4 sa fenêtre de propriétés.
   
    Hello tableau suivant indique quelles propriétés sont disponibles, mais elles sont en lecture seule. toochange, utilisez hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Propriété | Description |
   | --- | --- |
   | Nom DNS |URL de Hello avec hello adresse Internet de l’ordinateur virtuel de hello. |
   | Environnement |Pour un ordinateur virtuel, hello valeur de cette propriété est toujours Production. |
   | Nom |nom Hello de machine virtuelle de hello. |
   | Taille |taille de Hello de machine virtuelle hello, qui reflète la quantité de hello de mémoire et espace disque disponible. Pour plus d’informations, consultez « Configurer les tailles pour les services cloud ». |
   | État |Les valeurs incluent : Démarrage en cours, Démarré, En cours d’arrêt, Arrêté et Extraction de l’état. Si la récupération de l’état s’affiche, l’état actuel de hello est inconnu. les valeurs Hello pour cette propriété diffèrent des valeurs hello sont utilisées sur hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | SubscriptionID |ID d’abonnement Hello pour votre compte Azure. Vous pouvez afficher ces informations sur hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885) en affichant les propriétés hello pour un abonnement. |
2. Choisissez un nœud de point de terminaison, puis afficher hello **propriétés** fenêtre.
3. Hello tableau suivant décrit hello des propriétés disponibles des points de terminaison, mais ils sont en lecture seule. points de terminaison tooadd ou modifier hello pour un ordinateur virtuel, utilisez hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Propriété | Description |
   | --- | --- |
   | Nom |Identificateur de point de terminaison hello. |
   | Port privé |port Hello pour les applications de tooyour internes d’accès réseau. |
   | Protocole |protocole Hello hello couche de transport pour ce point de terminaison utilise, TCP ou UDP. |
   | Port public |port Hello qui est utilisé pour l’accès public tooyour application. |

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur l’utilisation des rôles Azure dans Visual Studio, consultez [à l’aide de bureau à distance avec des rôles Azure](vs-azure-tools-remote-desktop-roles.md).

