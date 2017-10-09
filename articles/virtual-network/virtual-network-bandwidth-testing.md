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
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="d6171-103">Test de bande passante/débit (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="d6171-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="d6171-104">Lorsque vous testez les performances de débit du réseau dans Azure, il est meilleure toouse un outil qui cible le réseau hello pour les tests et réduit l’utilisation de hello d’autres ressources qui peut impacter les performances.</span><span class="sxs-lookup"><span data-stu-id="d6171-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="d6171-105">NTTTCP est recommandé.</span><span class="sxs-lookup"><span data-stu-id="d6171-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="d6171-106">Copiez hello outil tootwo machines virtuelles de Azure Hello même taille.</span><span class="sxs-lookup"><span data-stu-id="d6171-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="d6171-107">Une machine virtuelle fonctionne comme expéditeur et hello autre en tant que récepteur.</span><span class="sxs-lookup"><span data-stu-id="d6171-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="d6171-108">Déploiement de machines virtuelles pour le test</span><span class="sxs-lookup"><span data-stu-id="d6171-108">Deploying VMs for testing</span></span>
<span data-ttu-id="d6171-109">Pour des raisons de hello de ce test, hello deux machines virtuelles doivent être dans hello même Service Cloud ou hello même groupe à haute disponibilité afin que nous pouvons utiliser leur adresses IP internes et exclure les équilibreurs de charge hello de test de hello.</span><span class="sxs-lookup"><span data-stu-id="d6171-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="d6171-110">Il est possible tootest avec hello VIP, mais ce type de test est en dehors de la portée de hello de ce document.</span><span class="sxs-lookup"><span data-stu-id="d6171-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="d6171-111">Prenez note de l’adresse IP du destinataire hello.</span><span class="sxs-lookup"><span data-stu-id="d6171-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="d6171-112">Appelons cette IP « a.b.c.r »</span><span class="sxs-lookup"><span data-stu-id="d6171-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="d6171-113">Prenez note du nombre de hello de cœurs sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d6171-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="d6171-114">Nous l’appelons «\#num\_cores »</span><span class="sxs-lookup"><span data-stu-id="d6171-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="d6171-115">Exécutez hello NTTTCP tester des 300 secondes (5 minutes) sur l’expéditeur hello machine virtuelle et du récepteur machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d6171-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="d6171-116">Conseil : Lorsque vous configurez ce test pour hello le première fois, vous pouvez essayer un test d’évaluation tooget période plus court plus tôt.</span><span class="sxs-lookup"><span data-stu-id="d6171-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="d6171-117">Une fois que l’outil de hello fonctionne comme prévu, étendre des secondes de période too300 hello test pour des résultats plus précis hello.</span><span class="sxs-lookup"><span data-stu-id="d6171-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="d6171-118">expéditeur de Hello **et** récepteur doit spécifier **hello même** paramètre de durée de test (-t).</span><span class="sxs-lookup"><span data-stu-id="d6171-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="d6171-119">tootest un seul flux TCP pendant 10 secondes :</span><span class="sxs-lookup"><span data-stu-id="d6171-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="d6171-120">Paramètres du récepteur : ntttcp - r -t 10 - P 1</span><span class="sxs-lookup"><span data-stu-id="d6171-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="d6171-121">Paramètres de l’expéditeur : ntttcp-s10.27.33.7 -t 10 - n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="d6171-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="d6171-122">Hello précédent exemple doit être uniquement utilisé tooconfirm votre configuration.</span><span class="sxs-lookup"><span data-stu-id="d6171-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="d6171-123">Des exemples valides de tests sont proposés plus loin dans ce document.</span><span class="sxs-lookup"><span data-stu-id="d6171-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="d6171-124">Test de machines virtuelles exécutant WINDOWS :</span><span class="sxs-lookup"><span data-stu-id="d6171-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="d6171-125">Obtenir NTTTCP sur hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d6171-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="d6171-126">Télécharger la version la plus récente hello : <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="d6171-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="d6171-127">Ou cherchez-la si elle a été déplacée : <https://www.bing.com/search?q=ntttcp+download> \< -- le premier résultat devrait être le bon</span><span class="sxs-lookup"><span data-stu-id="d6171-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="d6171-128">Envisagez de placer NTTTCP dans un dossier distinct, comme c:\\tools</span><span class="sxs-lookup"><span data-stu-id="d6171-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="d6171-129">Autoriser NTTTCP via le pare-feu Windows hello</span><span class="sxs-lookup"><span data-stu-id="d6171-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="d6171-130">Sur hello récepteur, créez une règle d’autorisation sur tooallow du pare-feu Windows hello le tooarrive trafic NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="d6171-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="d6171-131">Il est plus simple tooallow hello NTTTCP programme entier par nom plutôt que des ports TCP spécifiques tooallow entrant.</span><span class="sxs-lookup"><span data-stu-id="d6171-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="d6171-132">Autoriser ntttcp via hello pare-feu Windows comme suit :</span><span class="sxs-lookup"><span data-stu-id="d6171-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="d6171-133">netsh advfirewall firewall add rule program=\<CHEMIN\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="d6171-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="d6171-134">Par exemple, si vous avez copié ntttcp.exe toohello « c:\\outils « dossier, cela serait commande hello :</span><span class="sxs-lookup"><span data-stu-id="d6171-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="d6171-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="d6171-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="d6171-136">Exécution de tests NTTTCP</span><span class="sxs-lookup"><span data-stu-id="d6171-136">Running NTTTCP tests</span></span>

<span data-ttu-id="d6171-137">Démarrer NTTTCP sur hello récepteur (**exécuter à partir de CMD**, pas à partir de PowerShell) :</span><span class="sxs-lookup"><span data-stu-id="d6171-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="d6171-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="d6171-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="d6171-139">Si hello machine virtuelle a quatre cœurs et une adresse IP de 10.0.0.4, il ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="d6171-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="d6171-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="d6171-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="d6171-141">Démarrer NTTTCP sur hello expéditeur (**exécuter à partir de CMD**, pas à partir de PowerShell) :</span><span class="sxs-lookup"><span data-stu-id="d6171-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="d6171-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="d6171-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="d6171-143">Attend les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="d6171-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="d6171-144">Test de machines virtuelles exécutant LINUX :</span><span class="sxs-lookup"><span data-stu-id="d6171-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="d6171-145">Utilisez nttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="d6171-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="d6171-146">Vous pouvez l’obtenir ici : <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="d6171-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="d6171-147">Sur les machines virtuelles Linux (expéditeur et récepteur) de hello, exécutez ces commandes pour préparer ntttcp pour linux sur vos machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="d6171-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="d6171-148">CentOS - Installer Git :</span><span class="sxs-lookup"><span data-stu-id="d6171-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="d6171-149">Ubuntu - Installer Git :</span><span class="sxs-lookup"><span data-stu-id="d6171-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="d6171-150">Compilez et installez sur les deux :</span><span class="sxs-lookup"><span data-stu-id="d6171-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="d6171-151">Comme exemple de Windows hello, nous partons du principe QU'IP du récepteur hello Linux est 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="d6171-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="d6171-152">Démarrer-NTTTCP pour Linux sur hello récepteur :</span><span class="sxs-lookup"><span data-stu-id="d6171-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="d6171-153">Et sur l’expéditeur de hello, exécutez :</span><span class="sxs-lookup"><span data-stu-id="d6171-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="d6171-154">Too60 secondes si aucun paramètre de durée de test longueur par défaut est donnée.</span><span class="sxs-lookup"><span data-stu-id="d6171-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="d6171-155">Test entre les machines virtuelles exécutant Windows et LINUX :</span><span class="sxs-lookup"><span data-stu-id="d6171-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="d6171-156">Sur les scénarios de cette nous devons activer le mode de sans synchronisation hello permettant d’exécuter les tests hello.</span><span class="sxs-lookup"><span data-stu-id="d6171-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="d6171-157">Il incombe à l’aide de hello **indicateur -N** pour Linux et **indicateur de -ns** pour Windows.</span><span class="sxs-lookup"><span data-stu-id="d6171-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="d6171-158">À partir de Linux tooWindows :</span><span class="sxs-lookup"><span data-stu-id="d6171-158">From Linux tooWindows:</span></span>

<span data-ttu-id="d6171-159">Récepteur <Windows> :</span><span class="sxs-lookup"><span data-stu-id="d6171-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="d6171-160">Expéditeur <Linux>:</span><span class="sxs-lookup"><span data-stu-id="d6171-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="d6171-161">À partir de Windows tooLinux :</span><span class="sxs-lookup"><span data-stu-id="d6171-161">From Windows tooLinux:</span></span>

<span data-ttu-id="d6171-162">Récepteur <Linux> :</span><span class="sxs-lookup"><span data-stu-id="d6171-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="d6171-163">Expéditeur <Windows> :</span><span class="sxs-lookup"><span data-stu-id="d6171-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="d6171-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6171-164">Next steps</span></span>
* <span data-ttu-id="d6171-165">En fonction des résultats, il peut y avoir salle trop[optimiser les ordinateurs du débit réseau](virtual-network-optimize-network-bandwidth.md) pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="d6171-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="d6171-166">Découvrez-en davantage avec la [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="d6171-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
