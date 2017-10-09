---
title: "débit du réseau Azure VM aaaTesting | Documents Microsoft"
description: "Découvrez comment tootest machine virtuelle Azure débit du réseau."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Test de bande passante/débit (NTTTCP)

Lorsque vous testez les performances de débit du réseau dans Azure, il est meilleure toouse un outil qui cible le réseau hello pour les tests et réduit l’utilisation de hello d’autres ressources qui peut impacter les performances. NTTTCP est recommandé.

Copiez hello outil tootwo machines virtuelles de Azure Hello même taille. Une machine virtuelle fonctionne comme expéditeur et hello autre en tant que récepteur.

#### <a name="deploying-vms-for-testing"></a>Déploiement de machines virtuelles pour le test
Pour des raisons de hello de ce test, hello deux machines virtuelles doivent être dans hello même Service Cloud ou hello même groupe à haute disponibilité afin que nous pouvons utiliser leur adresses IP internes et exclure les équilibreurs de charge hello de test de hello. Il est possible tootest avec hello VIP, mais ce type de test est en dehors de la portée de hello de ce document.
 
Prenez note de l’adresse IP du destinataire hello. Appelons cette IP « a.b.c.r »

Prenez note du nombre de hello de cœurs sur hello machine virtuelle. Nous l’appelons «\#num\_cores »
 
Exécutez hello NTTTCP tester des 300 secondes (5 minutes) sur l’expéditeur hello machine virtuelle et du récepteur machine virtuelle.

Conseil : Lorsque vous configurez ce test pour hello le première fois, vous pouvez essayer un test d’évaluation tooget période plus court plus tôt. Une fois que l’outil de hello fonctionne comme prévu, étendre des secondes de période too300 hello test pour des résultats plus précis hello.

> [!NOTE]
> expéditeur de Hello **et** récepteur doit spécifier **hello même** paramètre de durée de test (-t).

tootest un seul flux TCP pendant 10 secondes :

Paramètres du récepteur : ntttcp - r -t 10 - P 1

Paramètres de l’expéditeur : ntttcp-s10.27.33.7 -t 10 - n 1 -P 1

> [!NOTE]
> Hello précédent exemple doit être uniquement utilisé tooconfirm votre configuration. Des exemples valides de tests sont proposés plus loin dans ce document.

## <a name="testing-vms-running-windows"></a>Test de machines virtuelles exécutant WINDOWS :

#### <a name="get-ntttcp-onto-hello-vms"></a>Obtenir NTTTCP sur hello machines virtuelles.

Télécharger la version la plus récente hello : <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Ou cherchez-la si elle a été déplacée : <https://www.bing.com/search?q=ntttcp+download> \< -- le premier résultat devrait être le bon

Envisagez de placer NTTTCP dans un dossier distinct, comme c:\\tools

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>Autoriser NTTTCP via le pare-feu Windows hello
Sur hello récepteur, créez une règle d’autorisation sur tooallow du pare-feu Windows hello le tooarrive trafic NTTTCP. Il est plus simple tooallow hello NTTTCP programme entier par nom plutôt que des ports TCP spécifiques tooallow entrant.

Autoriser ntttcp via hello pare-feu Windows comme suit :

netsh advfirewall firewall add rule program=\<CHEMIN\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

Par exemple, si vous avez copié ntttcp.exe toohello « c:\\outils « dossier, cela serait commande hello : 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>Exécution de tests NTTTCP

Démarrer NTTTCP sur hello récepteur (**exécuter à partir de CMD**, pas à partir de PowerShell) :

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

Si hello machine virtuelle a quatre cœurs et une adresse IP de 10.0.0.4, il ressemble à ceci :

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Démarrer NTTTCP sur hello expéditeur (**exécuter à partir de CMD**, pas à partir de PowerShell) :

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Attend les résultats de hello.


## <a name="testing-vms-running-linux"></a>Test de machines virtuelles exécutant LINUX :

Utilisez nttcp-for-linux. Vous pouvez l’obtenir ici : <https://github.com/Microsoft/ntttcp-for-linux>

Sur les machines virtuelles Linux (expéditeur et récepteur) de hello, exécutez ces commandes pour préparer ntttcp pour linux sur vos machines virtuelles :

CentOS - Installer Git :
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu - Installer Git :
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Compilez et installez sur les deux :
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Comme exemple de Windows hello, nous partons du principe QU'IP du récepteur hello Linux est 10.0.0.4

Démarrer-NTTTCP pour Linux sur hello récepteur :

``` bash
ntttcp -r -t 300
```

Et sur l’expéditeur de hello, exécutez :

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Too60 secondes si aucun paramètre de durée de test longueur par défaut est donnée.

## <a name="testing-between-vms-running-windows-and-linux"></a>Test entre les machines virtuelles exécutant Windows et LINUX :

Sur les scénarios de cette nous devons activer le mode de sans synchronisation hello permettant d’exécuter les tests hello. Il incombe à l’aide de hello **indicateur -N** pour Linux et **indicateur de -ns** pour Windows.

#### <a name="from-linux-toowindows"></a>À partir de Linux tooWindows :

Récepteur <Windows> :

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Expéditeur <Linux>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>À partir de Windows tooLinux :

Récepteur <Linux> :

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Expéditeur <Windows> :

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Étapes suivantes
* En fonction des résultats, il peut y avoir salle trop[optimiser les ordinateurs du débit réseau](virtual-network-optimize-network-bandwidth.md) pour votre scénario.
* Découvrez-en davantage avec la [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)
