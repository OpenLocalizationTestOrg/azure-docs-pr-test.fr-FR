---
title: "Test du débit du réseau des machines virtuelles | Microsoft Docs"
description: "Découvrez comment tester le débit du réseau des machines virtuelles Azure."
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
ms.openlocfilehash: ccebc722386a19014674d7a59757a3685bd50793
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Test de bande passante/débit (NTTTCP)

Lorsque vous testez les performances du débit réseau dans Azure, il est préférable d’utiliser un outil qui cible le réseau pour le test et réduit l’utilisation d’autres ressources qui peuvent affecter les performances. NTTTCP est recommandé.

Copiez l’outil sur deux machines virtuelles Azure de la même taille. Une machine virtuelle fonctionne comme expéditeur et l’autre comme récepteur.

#### <a name="deploying-vms-for-testing"></a>Déploiement de machines virtuelles pour le test
Dans le cadre de ce test, les deux machines virtuelles doivent être dans le même service cloud ou le même groupe à haute disponibilité afin de pouvoir utiliser leurs adresses IP internes et exclure les équilibrages de charge du test. Il est possible de tester avec l’adresse IP virtuelle, mais ce type de test n’est pas couvert par ce document.
 
Prenez note de l’adresse IP du récepteur. Appelons cette IP « a.b.c.r »

Notez le nombre de cœurs de la machine virtuelle. Nous l’appelons «\#num\_cores »
 
Exécutez le test NTTTCP pendant 300 secondes (5 minutes) les machines virtuelles d’expédition et de réception.

Conseil : Lorsque vous configurez ce test pour la première fois, vous pouvez essayer une période d’essai plus courte pour obtenir des résultats plus tôt. Une fois que l’outil fonctionne comme prévu, étendez la période d’essai à 300 secondes pour des résultats plus précis.

> [!NOTE]
> L’expéditeur **et** le récepteur doivent spécifier **le même** paramètre de durée de test (-t).

Pour tester un seul flux TCP pendant 10 secondes :

Paramètres du récepteur : ntttcp - r -t 10 - P 1

Paramètres de l’expéditeur : ntttcp-s10.27.33.7 -t 10 - n 1 -P 1

> [!NOTE]
> L’exemple précédent doit uniquement être utilisé pour confirmer votre configuration. Des exemples valides de tests sont proposés plus loin dans ce document.

## <a name="testing-vms-running-windows"></a>Test de machines virtuelles exécutant WINDOWS :

#### <a name="get-ntttcp-onto-the-vms"></a>Préparez NTTTCP sur les machines virtuelles.

Téléchargez la version la plus récente : <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Ou cherchez-la si elle a été déplacée : <https://www.bing.com/search?q=ntttcp+download> \< -- le premier résultat devrait être le bon

Envisagez de placer NTTTCP dans un dossier distinct, comme c:\\tools

#### <a name="allow-ntttcp-through-the-windows-firewall"></a>Autoriser NTTTCP via le pare-feu Windows
Sur le RÉCEPTEUR, créez une règle d’autorisation sur le pare-feu Windows pour autoriser l’entrée du trafic NTTTCP. Il est plus facile d’autoriser la totalité du programme NTTTCP par nom que d’autoriser des ports entrants TCP spécifiques.

Autorisez ntttcp via le pare-feu Windows en utilisant ce qui suit :

netsh advfirewall firewall add rule program=\<CHEMIN\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

Par exemple, si vous avez copié ntttcp.exe dans le dossier « c:\\tools », voici la commande : 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>Exécution de tests NTTTCP

Pour démarrer NTTTCP sur le RÉCEPTEUR (**exécuter à partir de CMD** et non à partir de PowerShell) :

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

Si la machine virtuelle possède quatre cœurs et une adresse IP de 10.0.0.4, la commande ressemblerait à ceci :

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Pour démarrer NTTTCP sur l’EXPÉDITEUR (**exécuter à partir de CMD** et non à partir de PowerShell) :

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Attendez les résultats.


## <a name="testing-vms-running-linux"></a>Test de machines virtuelles exécutant LINUX :

Utilisez nttcp-for-linux. Vous pouvez l’obtenir ici : <https://github.com/Microsoft/ntttcp-for-linux>

Sur les machines virtuelles Linux (EXPÉDITEUR et RÉCEPTEUR), exécutez les commandes suivantes pour préparer ntttcp-for-linux sur vos machines virtuelles :

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

Comme dans l’exemple pour Windows, nous partons du principe que l’IP du récepteur Linux est 10.0.0.4

Démarrez NTTTCP-for-Linux sur le récepteur :

``` bash
ntttcp -r -t 300
```

Et sur l’EXPÉDITEUR, exécutez :

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
La longueur de test par défaut est de 60 secondes si aucun paramètre de temps n’est défini

## <a name="testing-between-vms-running-windows-and-linux"></a>Test entre les machines virtuelles exécutant Windows et LINUX :

Dans ce scénario, nous devons activer le mode sans synchronisation pour permettre l’exécution du test. Pour ce faire, utilisez l’**indicateur -N** pour Linux, et l’**indicateur -ns** pour Windows.

#### <a name="from-linux-to-windows"></a>De Linux vers Windows :

Récepteur <Windows> :

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Expéditeur <Linux>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-to-linux"></a>De Windows vers Linux :

Récepteur <Linux> :

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Expéditeur <Windows> :

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Étapes suivantes
* En fonction des résultats, vous pourriez être en mesure [d’optimiser le de débit réseau](virtual-network-optimize-network-bandwidth.md) pour votre scénario.
* Découvrez-en davantage avec la [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)
