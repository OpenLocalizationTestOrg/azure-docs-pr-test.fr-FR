---
title: "captures de paquets d’aaaManage d’observateur de réseau Azure - portail Azure | Documents Microsoft"
description: "Cette page explique comment toomanage hello la fonctionnalité de capture de paquet de l’Observateur réseau à l’aide du portail Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>Gérer des captures de paquets avec l’Observateur réseau de Azure à l’aide du portail de hello

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API REST Azure](network-watcher-packet-capture-manage-rest.md)

Capture de paquets de l’Observateur réseau vous permet de toocreate capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel. Les filtres sont fournies pour tooensure de session de capture hello que vous capturer le trafic hello seulement que vous le souhaitez. Capture des paquets permet des anomalies de réseau toodiagnose proactive et réactive. Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore. En étant en mesure de tooremotely déclencheur paquet captures, cette fonctionnalité facilite hello de l’exécution d’une capture de paquets sur l’ordinateur souhaité hello, qui permet d’économiser un temps précieux et manuellement.

Cet article passe en revue hello différentes tâches de gestion qui sont actuellement disponibles pour la capture des paquets.

- [**Démarrer une capture de paquets**](#start-a-packet-capture)
- [**Arrêter une capture de paquets**](#stop-a-packet-capture)
- [**Supprimer une capture de paquets**](#delete-a-packet-capture)
- [**Télécharger une capture de paquets**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Avant de commencer

Cet article suppose que vous avez hello suivant des ressources :

- Une instance de l’Observateur réseau dans la région de hello souhaité toocreate une capture de paquets
- Une machine virtuelle avec les paquets hello capturer extension activée.

> [!IMPORTANT]
> La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`. Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>Extension de l’agent de Capture de paquets via le portail de hello

capture des paquets hello tooinstall agent de machine virtuelle via le portail de hello, accédez tooyour virtual machine, cliquez sur **Extensions** > **ajouter** et recherchez **Agent de l’Observateur réseau pour Windows**

![vue de l’agent][agent]

## <a name="packet-capture-overview"></a>Vue d’ensemble des captures de paquets

Accédez toohello [portail Azure](https://portal.azure.com) et cliquez sur **réseau** > **Observateur réseau** > **de Capture de paquets**

page Vue d’ensemble de Hello affiche qu'une liste de tous les paquets capture qui existent, quel que soit l’état de hello.

> [!NOTE]
> Capture des paquets nécessite un compte de stockage toohello de connectivité sur le port 443.

![Écran Vue d’ensemble des captures de paquets][1]

## <a name="start-a-packet-capture"></a>Démarrer une capture de paquets

Cliquez sur **ajouter** toocreate une capture de paquets.

propriétés de Hello qui peuvent être définies sur une capture de paquets sont :

**Paramètres principaux**

- **Abonnement** -cette valeur est abonnement hello qui est utilisé, une instance de l’Observateur réseau est nécessaire dans chaque abonnement.
- **Groupe de ressources** -groupe de ressources hello de machine virtuelle hello ciblé.
- **Cibler la machine virtuelle** -machine virtuelle hello qui capture des paquets hello est en cours d’exécution
- **Nom de capture de paquet** -cette valeur est le nom de hello de capture de paquets hello.

**Configuration de la capture**

- **Compte de stockage** : détermine si la capture de paquets est enregistrée dans un compte de stockage.
- **Fichier** -détermine si une capture de paquets est enregistrée localement sur l’ordinateur virtuel de hello.
- **Comptes de stockage** -hello sélectionnée de capture de paquets hello stockage compte toosave dans. Emplacement par défaut : https://{nom du compte de stockage}.blob.core.windows.net/network-watcher-logs/subscriptions/{ID d’abonnement}/resourcegroups/{nom du groupe de ressources}/providers/microsoft.compute/virtualmachines/{nom de la machine virtuelle}/{AA}/{MM}/{JJ}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap. (Activé uniquement si **Stockage** est sélectionné.)
- **Chemin d’accès local** -chemin d’accès local de hello sur une capture de paquets hello toosave machine virtuelle. (Activé uniquement si **Fichier** est sélectionné.) Un chemin d’accès valide doit être fourni.
- **Nombre maximal d’octets par paquet** -hello du nombre d’octets à partir de chaque paquet sont capturées, tous les octets sont capturées, si ce champ est vide.
- **Nombre maximal d’octets par session** - Total nombre d’octets qui sont capturées, une fois la valeur de hello atteinte cesse de capture de paquets hello.
- **Délai (secondes)** -définit une limite de temps pour toostop de capture de paquets hello. La valeur par défaut est de 18 000 secondes.

> [!NOTE]
> Les comptes de stockage Premium ne sont actuellement pas pris en charge pour le stockage des captures de paquets.

**Filtrage (facultatif)**

- **Protocole** -hello toofilter de protocole pour la capture des paquets hello. les valeurs disponibles Hello sont TCP, UDP et toutes.
- **Adresse IP locale** -cette valeur filtres toopackets de capture de paquets hello où l’adresse IP locale hello correspond à cette valeur de filtre.
- **Port local** -cette valeur filtres toopackets de capture de paquets hello où port local de hello correspond à cette valeur de filtre.
- **Adresse IP distante** -cette valeur filtres toopackets de capture de paquets hello où adresse IP distante de hello correspond à cette valeur de filtre.
- **Port distant** -cette valeur filtres toopackets de capture de paquets hello où port distant de hello correspond à cette valeur de filtre.

> [!NOTE]
> Les valeurs d’adresse IP et de port peuvent être une valeur unique, une plage de valeurs ou un ensemble (c’est-à-dire, 80-1024 pour le port). Vous pouvez définir autant de filtres que vous le souhaitez.

Une fois que les valeurs hello sont remplis, cliquez sur **OK** toocreate capture des paquets hello.

![créer une capture de paquets][2]

Après que hello délai défini sur capture des paquets hello a expiré, la capture des paquets hello s’arrête et peut être vérifiée. Vous pouvez également arrêter manuellement des sessions de captures de paquets hello.

## <a name="delete-a-packet-capture"></a>Supprimer une capture de paquets

Dans les paquets hello capturer vue, cliquez sur hello **menu contextuel** (...) ou avec le bouton droit, puis cliquez sur **supprimer** capture des paquets hello toostop

![supprimer une capture de paquets][3]

> [!NOTE]
> Suppression d’une capture de paquets ne supprime pas le fichier hello hello compte de stockage.

Vous êtes invité tooconfirm vous souhaitez que la capture des paquets hello toodelete, cliquez sur **Oui**

![confirmation][4]

## <a name="stop-a-packet-capture"></a>Arrêter une capture de paquets

Dans les paquets hello capturer vue, cliquez sur hello **menu contextuel** (...) ou avec le bouton droit, puis cliquez sur **arrêter** capture des paquets hello toostop

## <a name="download-a-packet-capture"></a>Télécharger une capture de paquets

Une fois terminé, votre session de capture de paquets hello capture fichier est téléchargé tooblob tooa ou stockage local sur hello machine virtuelle. emplacement de stockage Hello de capture de paquets hello est définie lors de la création de la session de hello. Un outil pratique de tooaccess ces fichiers de capture de compte de stockage tooa enregistré est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/

Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)

Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













