---
title: "inspection d’aaaPacket avec l’Observateur de réseau Azure | Documents Microsoft"
description: "Cet article décrit la façon dont les toouse inspection approfondie des paquets de tooperform Observateur réseau collectées à partir d’une machine virtuelle"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a>Inspection de paquets avec Azure Network Watcher

À l’aide de la fonctionnalité de capture de paquets hello de l’Observateur réseau, vous pouvez lancer et gérer les sessions de capture sur vos machines virtuelles Azure, à partir du portail de hello, PowerShell CLI et par programme via le Kit de développement logiciel de hello et l’API REST. Capture des paquets vous permet de tooaddress les scénarios qui requièrent des données au niveau du paquet en fournissant des informations hello dans un format facilement utilisable. Tirant parti de données de salutation tooinspect d’outils, vous pouvez examiner les communications envoyées tooand à partir de vos machines virtuelles et obtenir des informations détaillées sur votre trafic réseau. Exemples d’utilisation des données de capture de paquets : étude des problèmes de réseau ou d’application, détection des tentatives d’utilisation abusive et d’intrusion sur le réseau ou maintien de la conformité aux réglementations. Dans cet article, nous montrons comment tooopen un fichier de capture de paquet fourni par l’Observateur réseau à l’aide d’un outil open source populaires. Elle fournit également des exemples montrant comment identifier le trafic anormal toocalculate une latence de la connexion et examiner les statistiques de mise en réseau.

## <a name="before-you-begin"></a>Avant de commencer

Cet article aborde certains scénarios préconfigurés dans une capture de paquets exécutée précédemment. Ces scénarios illustrent les fonctionnalités qui sont accessibles en consultant une capture de paquets. Ce scénario utilise [WireShark](https://www.wireshark.org/) tooinspect capture des paquets hello.

Ce scénario part du principe que vous avez déjà exécuté une capture de paquets sur une machine virtuelle. toolearn comment toocreate une capture de paquets visitez [capture des paquets de gérer avec le portail de hello](network-watcher-packet-capture-manage-portal.md) ou reste en vous rendant sur [la gestion des Captures de paquets d’API REST](network-watcher-packet-capture-manage-rest.md).

## <a name="scenario"></a>Scénario

Dans ce scénario, vous allez :

* Examiner une capture de paquets

## <a name="calculate-network-latency"></a>Calculer la latence du réseau

Dans ce scénario, nous montrons comment tooview hello heure aller-retour initiale (RTT) d’une conversation de protocole TCP (Transmission Control) qui se produit entre deux points de terminaison.

Lorsqu’une connexion TCP est établie, hello trois premiers paquets envoyés dans la connexion de hello suivent un modèle communément tooas hello tridirectionnel. En examinant les paquets hello deux premières envoyés dans ce protocole de transfert, une demande initiale à partir du client de hello et une réponse du serveur de hello, nous permet de calculer la latence hello lorsque cette connexion a été établie. Cette latence soit référencé tooas hello temps d’aller-retour (RTT). Pour plus d’informations sur le protocole TCP hello et tridirectionnel hello reportez-vous toohello suivant des ressources. https://support.microsoft.com/fr-fr/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip

### <a name="step-1"></a>Étape 1 :

Lancez WireShark.

### <a name="step-2"></a>Étape 2

Hello de charge **.cap** fichier à partir de la capture des paquets. Ce fichier se trouve dans l’objet blob de hello il a été enregistré dans notre machine virtuelle hello localement sur, en fonction de leur configuration.

### <a name="step-3"></a>Étape 3 :

tooview hello heure aller-retour initiale (RTT) dans les conversations TCP, nous sera être examine uniquement les deux premières paquets hello impliquées dans la négociation TCP hello. Nous allons utiliser des deux premières les paquets hello dans hello tridirectionnel, qui sont hello [SYN], [SYN, ACK] paquets. Ils sont nommés pour les indicateurs définis dans l’en-tête TCP hello. Hello dernier paquet dans la négociation hello, les paquets hello [l’accusé de réception], servira pas dans ce scénario. les paquets Hello [SYN] sont envoyé par le client de hello. Après sa réception server de hello envoie les paquets hello [ACK] sous la forme d’un accusé de réception hello SYN à partir du client de hello. Grâce à des faits hello que réponse du serveur hello nécessite très peu de surcharge, nous calculons hello RTT en soustrayant l’heure hello les paquets hello [SYN, ACK] a été reçu par le client de hello par paquet de temps [SYN] hello a été envoyé par le client de hello.

Si vous utilisez WireShark, cette valeur est calculée automatiquement.

toomore afficher facilement les deux premières les paquets hello dans hello TCP tridirectionnel, nous allons utiliser hello fonctionnalité fournie par WireShark de filtrage.

filtre de hello tooapply dans WireShark, développez hello Segment « Transmission Control Protocol » d’un paquet [SYN] dans la capture et examiner les indicateurs hello définies dans l’en-tête TCP hello.

Étant donné que nous recherchons toofilter sur tous les [SYN] et [SYN, ACK] cofirm de paquets, sous indicateurs que hello Syn bit a la valeur too1, puis cliquez à droite sur les bits de Syn hello -> appliquer comme filtre -> sélectionnés.

![figure 7][7]

### <a name="step-4"></a>Étape 4

Maintenant que vous avez filtré les paquets de voir hello fenêtre tooonly avec hello [SYN] bit défini, vous pouvez facilement sélectionner conversations vous intéressez tooview hello RTT initial. Un Bonjour de tooview facilement RTT dans WireShark cliquez simplement sur déroulante hello marqué l’analyse de « SEQ / l’accusé de réception ». Vous verrez ensuite hello que RTT affiché. Dans ce cas, hello RTT a été 0.0022114 secondes ou 2.211 ms.

![figure 8][8]

## <a name="unwanted-protocols"></a>Protocoles indésirables

De nombreuses applications peuvent être exécutées sur une instance de machine virtuelle que vous avez déployée dans Azure. Plusieurs de ces applications communiquent via le réseau de hello, éventuellement sans votre autorisation explicite. À l’aide de la communication réseau de paquet capture toostore, nous pouvons étudier comment application s’adressent sur le réseau de hello et recherchez les problèmes.

Dans cet exemple, nous allons examiner une capture de paquets précédemment exécutée afin d’identifier les protocoles indésirables susceptibles d’indiquer une communication non autorisée à partir d’une application en cours d’exécution sur votre ordinateur.

### <a name="step-1"></a>Étape 1

À l’aide de hello même capture dans hello précédente scénario, cliquez sur **statistiques** > **hiérarchie de protocole**

![menu Hiérarchie des protocoles][2]

fenêtre hiérarchie de protocole Hello s’affiche. Cette vue fournit une liste de tous les protocoles hello qui étaient en cours d’utilisation pendant la session de capture hello et nombre de hello de paquets transmis et reçus à l’aide de protocoles de hello. Cette vue peut être utile pour détecter le trafic réseau indésirable sur vos machines virtuelles ou sur le réseau.

![hiérarchie des protocoles développée][3]

Comme vous pouvez le voir dans hello suivant capture d’écran, il a été le trafic à l’aide du protocole BitTorrent hello, qui est utilisé pour le partage de fichiers homologue toopeer. En tant qu’administrateur, vous ne prévoyez pas le trafic de BitTorrent toosee sur cet notamment les ordinateurs virtuels. Maintenant vous prenant en charge de ce trafic, vous pouvez supprimer hello homologue toopeer logiciel installés sur cet ordinateur virtuel, ou hello du bloc à l’aide d’un pare-feu ou des groupes de sécurité réseau du trafic. En outre, vous pouvez choisir les captures de paquets toorun selon une planification, afin que vous pouvez vérifier régulièrement utilisation du protocole hello sur vos ordinateurs virtuels. Pour obtenir un exemple sur des tâches de tooautomate réseau dans azure visite [surveiller les ressources réseau avec azure automation](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>Identification des principaux ports et destinations

Présentation des types de trafic hello, hello des points de terminaison et ports hello communiquées via est un important lors de l’analyse ou la résolution des problèmes des applications et des ressources sur votre réseau. En utilisant un fichier de capture de paquet ci-dessus, nous pouvons apprendre rapidement hello premières destinations notre machine virtuelle avec lequel communique et hello ports utilisés.

### <a name="step-1"></a>Étape 1

À l’aide de hello même capture dans hello précédente scénario, cliquez sur **statistiques** > **statistiques IPv4** > **Destinations et les Ports**

![fenêtre de capture de paquets][4]

### <a name="step-2"></a>Étape 2

Comme nous Examinez les résultats de hello est une ligne, a été plusieurs connexions sur le port 111. port de Hello plus utilisé a été 3389, qui est le Bureau à distance et hello restants sont des ports dynamiques RPC.

Alors que ce trafic peut signifier nothing, il s’agit d’un port qui a été utilisé pour un grand nombre de connexions et est inconnu toohello administrateur.

![figure 5][5]

### <a name="step-3"></a>Étape 3 :

Maintenant que nous avons déterminé une hors du port de la place, nous pouvons filtrer notre capture basée sur le port hello.

filtre Hello dans ce scénario serait :

```
tcp.port == 111
```

Nous permet d’entrer le texte du filtre hello ci-dessus dans la zone de texte de filtre hello et appuyez sur ENTRÉE.

![figure 6][6]

À partir des résultats de hello, nous pouvons voir tout le trafic de hello provient d’un ordinateur virtuel local sur hello même sous-réseau. Si nous ne pas toujours comprendre pourquoi ce trafic se produit, nous pouvons examiner plus toodetermine de paquets hello pourquoi il effectue ces appels sur le port 111. Avec ces informations nous pouvons effectuer l’action appropriée de hello.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur hello autres fonctionnalités de diagnostic de l’Observateur réseau en vous rendant sur [réseau Azure la présentation des moniteurs](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













