---
title: "fenêtre d’interpréteur de commandes de cloud computing Azure (aperçu) aaaUsing hello | Documents Microsoft"
description: "Fenêtre d’interpréteur de commandes Azure Cloud procédure pas à pas hello."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a>À l’aide de la fenêtre d’interpréteur de commandes Azure Cloud hello

Ce document explique comment toouse hello fenêtre Shell de Cloud.

## <a name="concurrent-sessions"></a>Sessions simultanées
Cloud Shell permet à plusieurs sessions simultanées entre les onglets de navigateur en permettant à chaque tooexist de session en tant que processus séparé Bash.
Si quitter une session, assurez-vous que chaque processus s’exécute indépendamment bien qu’elles s’exécutent sur tooexit à partir de chaque fenêtre de session hello même ordinateur.

## <a name="restart-cloud-shell"></a>Redémarrer Cloud Shell
![](media/recycle.png)
> [!WARNING]
> Le redémarrage de Cloud Shell réinitialise l’état de la machine et tous les fichiers non conservés par votre partage de fichiers sont perdus.

* Cliquez sur icône du redémarrage hello sur la barre d’outils de hello tooreceive un nouvel environnement de Shell du Cloud.

## <a name="minimize--maximize-cloud-shell-window"></a>Réduire et agrandir la fenêtre Cloud Shell
![](media/minmax.png)
* Cliquez sur hello réduire sur hello icône haut à droite de hello fenêtre toohide il. Recliquez sur hello icône Cloud Shell toounhide.
* Cliquez sur hello optimiser la hauteur de toomax icône tooset fenêtre. toorestore fenêtre tooprevious taille, cliquez sur Restaurer.

## <a name="copy-and-paste"></a>Copier et coller
* Windows : `Ctrl-insert` toocopy et `Shift-insert` toopaste. Le menu déroulant accessible par un clic droit permet également de copier/coller.
  * FireFox/IE peuvent ne pas prendre en charge correctement les autorisations de Presse-papiers.
* Mac OS : `Cmd-c` toocopy et `Cmd-v` toopaste. Le menu déroulant accessible par un clic droit permet également de copier/coller.

## <a name="resize-cloud-shell-window"></a>Redimensionner la fenêtre Cloud Shell
* Cliquez et faites glisser de bord supérieur de hello de barre d’outils hello haut ou le bas de la fenêtre de l’interface de Cloud tooresize hello.

## <a name="scrolling-text-display"></a>Défilement du texte
* Défile avec le texte de terminal toomove tactile ou de la souris.

## <a name="exit-command"></a>Commande Quitter
En cours d’exécution `exit` met fin à la session active de hello. Ce comportement se produit par défaut au bout de 20 minutes en l’absence d’interaction.

## <a name="next-steps"></a>Étapes suivantes
[Démarrage rapide de Cloud Shell](quickstart.md)
