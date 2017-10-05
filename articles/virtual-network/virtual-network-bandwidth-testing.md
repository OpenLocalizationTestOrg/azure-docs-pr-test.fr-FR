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
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="3cf96-103">Test de bande passante/débit (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="3cf96-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="3cf96-104">Lorsque vous testez les performances du débit réseau dans Azure, il est préférable d’utiliser un outil qui cible le réseau pour le test et réduit l’utilisation d’autres ressources qui peuvent affecter les performances.</span><span class="sxs-lookup"><span data-stu-id="3cf96-104">When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance.</span></span> <span data-ttu-id="3cf96-105">NTTTCP est recommandé.</span><span class="sxs-lookup"><span data-stu-id="3cf96-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="3cf96-106">Copiez l’outil sur deux machines virtuelles Azure de la même taille.</span><span class="sxs-lookup"><span data-stu-id="3cf96-106">Copy the tool to two Azure VMs of the same size.</span></span> <span data-ttu-id="3cf96-107">Une machine virtuelle fonctionne comme expéditeur et l’autre comme récepteur.</span><span class="sxs-lookup"><span data-stu-id="3cf96-107">One VM functions as SENDER and the other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="3cf96-108">Déploiement de machines virtuelles pour le test</span><span class="sxs-lookup"><span data-stu-id="3cf96-108">Deploying VMs for testing</span></span>
<span data-ttu-id="3cf96-109">Dans le cadre de ce test, les deux machines virtuelles doivent être dans le même service cloud ou le même groupe à haute disponibilité afin de pouvoir utiliser leurs adresses IP internes et exclure les équilibrages de charge du test.</span><span class="sxs-lookup"><span data-stu-id="3cf96-109">For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test.</span></span> <span data-ttu-id="3cf96-110">Il est possible de tester avec l’adresse IP virtuelle, mais ce type de test n’est pas couvert par ce document.</span><span class="sxs-lookup"><span data-stu-id="3cf96-110">It is possible to test with the VIP but this kind of testing is outside the scope of this document.</span></span>
 
<span data-ttu-id="3cf96-111">Prenez note de l’adresse IP du récepteur.</span><span class="sxs-lookup"><span data-stu-id="3cf96-111">Make a note of the RECEIVER's IP address.</span></span> <span data-ttu-id="3cf96-112">Appelons cette IP « a.b.c.r »</span><span class="sxs-lookup"><span data-stu-id="3cf96-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="3cf96-113">Notez le nombre de cœurs de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3cf96-113">Make a note of the number of cores on the VM.</span></span> <span data-ttu-id="3cf96-114">Nous l’appelons «\#num\_cores »</span><span class="sxs-lookup"><span data-stu-id="3cf96-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="3cf96-115">Exécutez le test NTTTCP pendant 300 secondes (5 minutes) les machines virtuelles d’expédition et de réception.</span><span class="sxs-lookup"><span data-stu-id="3cf96-115">Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.</span></span>

<span data-ttu-id="3cf96-116">Conseil : Lorsque vous configurez ce test pour la première fois, vous pouvez essayer une période d’essai plus courte pour obtenir des résultats plus tôt.</span><span class="sxs-lookup"><span data-stu-id="3cf96-116">Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner.</span></span> <span data-ttu-id="3cf96-117">Une fois que l’outil fonctionne comme prévu, étendez la période d’essai à 300 secondes pour des résultats plus précis.</span><span class="sxs-lookup"><span data-stu-id="3cf96-117">Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="3cf96-118">L’expéditeur **et** le récepteur doivent spécifier **le même** paramètre de durée de test (-t).</span><span class="sxs-lookup"><span data-stu-id="3cf96-118">The sender **and** receiver must specify **the same** test duration parameter (-t).</span></span>

<span data-ttu-id="3cf96-119">Pour tester un seul flux TCP pendant 10 secondes :</span><span class="sxs-lookup"><span data-stu-id="3cf96-119">To test a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="3cf96-120">Paramètres du récepteur : ntttcp - r -t 10 - P 1</span><span class="sxs-lookup"><span data-stu-id="3cf96-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="3cf96-121">Paramètres de l’expéditeur : ntttcp-s10.27.33.7 -t 10 - n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="3cf96-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="3cf96-122">L’exemple précédent doit uniquement être utilisé pour confirmer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="3cf96-122">The preceding sample should only be used to confirm your configuration.</span></span> <span data-ttu-id="3cf96-123">Des exemples valides de tests sont proposés plus loin dans ce document.</span><span class="sxs-lookup"><span data-stu-id="3cf96-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="3cf96-124">Test de machines virtuelles exécutant WINDOWS :</span><span class="sxs-lookup"><span data-stu-id="3cf96-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-the-vms"></a><span data-ttu-id="3cf96-125">Préparez NTTTCP sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3cf96-125">Get NTTTCP onto the VMs.</span></span>

<span data-ttu-id="3cf96-126">Téléchargez la version la plus récente : <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="3cf96-126">Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="3cf96-127">Ou cherchez-la si elle a été déplacée : <https://www.bing.com/search?q=ntttcp+download> \< -- le premier résultat devrait être le bon</span><span class="sxs-lookup"><span data-stu-id="3cf96-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="3cf96-128">Envisagez de placer NTTTCP dans un dossier distinct, comme c:\\tools</span><span class="sxs-lookup"><span data-stu-id="3cf96-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-the-windows-firewall"></a><span data-ttu-id="3cf96-129">Autoriser NTTTCP via le pare-feu Windows</span><span class="sxs-lookup"><span data-stu-id="3cf96-129">Allow NTTTCP through the Windows firewall</span></span>
<span data-ttu-id="3cf96-130">Sur le RÉCEPTEUR, créez une règle d’autorisation sur le pare-feu Windows pour autoriser l’entrée du trafic NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="3cf96-130">On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive.</span></span> <span data-ttu-id="3cf96-131">Il est plus facile d’autoriser la totalité du programme NTTTCP par nom que d’autoriser des ports entrants TCP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3cf96-131">It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.</span></span>

<span data-ttu-id="3cf96-132">Autorisez ntttcp via le pare-feu Windows en utilisant ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="3cf96-132">Allow ntttcp through the Windows Firewall like this:</span></span>

<span data-ttu-id="3cf96-133">netsh advfirewall firewall add rule program=\<CHEMIN\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="3cf96-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="3cf96-134">Par exemple, si vous avez copié ntttcp.exe dans le dossier « c:\\tools », voici la commande :</span><span class="sxs-lookup"><span data-stu-id="3cf96-134">For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command:</span></span> 

<span data-ttu-id="3cf96-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="3cf96-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="3cf96-136">Exécution de tests NTTTCP</span><span class="sxs-lookup"><span data-stu-id="3cf96-136">Running NTTTCP tests</span></span>

<span data-ttu-id="3cf96-137">Pour démarrer NTTTCP sur le RÉCEPTEUR (**exécuter à partir de CMD** et non à partir de PowerShell) :</span><span class="sxs-lookup"><span data-stu-id="3cf96-137">Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="3cf96-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="3cf96-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="3cf96-139">Si la machine virtuelle possède quatre cœurs et une adresse IP de 10.0.0.4, la commande ressemblerait à ceci :</span><span class="sxs-lookup"><span data-stu-id="3cf96-139">If the VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="3cf96-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="3cf96-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="3cf96-141">Pour démarrer NTTTCP sur l’EXPÉDITEUR (**exécuter à partir de CMD** et non à partir de PowerShell) :</span><span class="sxs-lookup"><span data-stu-id="3cf96-141">Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="3cf96-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="3cf96-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="3cf96-143">Attendez les résultats.</span><span class="sxs-lookup"><span data-stu-id="3cf96-143">Wait for the results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="3cf96-144">Test de machines virtuelles exécutant LINUX :</span><span class="sxs-lookup"><span data-stu-id="3cf96-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="3cf96-145">Utilisez nttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="3cf96-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="3cf96-146">Vous pouvez l’obtenir ici : <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="3cf96-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="3cf96-147">Sur les machines virtuelles Linux (EXPÉDITEUR et RÉCEPTEUR), exécutez les commandes suivantes pour préparer ntttcp-for-linux sur vos machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="3cf96-147">On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="3cf96-148">CentOS - Installer Git :</span><span class="sxs-lookup"><span data-stu-id="3cf96-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="3cf96-149">Ubuntu - Installer Git :</span><span class="sxs-lookup"><span data-stu-id="3cf96-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="3cf96-150">Compilez et installez sur les deux :</span><span class="sxs-lookup"><span data-stu-id="3cf96-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="3cf96-151">Comme dans l’exemple pour Windows, nous partons du principe que l’IP du récepteur Linux est 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="3cf96-151">As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="3cf96-152">Démarrez NTTTCP-for-Linux sur le récepteur :</span><span class="sxs-lookup"><span data-stu-id="3cf96-152">Start NTTTCP-for-Linux on the RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="3cf96-153">Et sur l’EXPÉDITEUR, exécutez :</span><span class="sxs-lookup"><span data-stu-id="3cf96-153">And on the SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="3cf96-154">La longueur de test par défaut est de 60 secondes si aucun paramètre de temps n’est défini</span><span class="sxs-lookup"><span data-stu-id="3cf96-154">Test length defaults to 60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="3cf96-155">Test entre les machines virtuelles exécutant Windows et LINUX :</span><span class="sxs-lookup"><span data-stu-id="3cf96-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="3cf96-156">Dans ce scénario, nous devons activer le mode sans synchronisation pour permettre l’exécution du test.</span><span class="sxs-lookup"><span data-stu-id="3cf96-156">On this scenarios we should enable the no-sync mode so the test can run.</span></span> <span data-ttu-id="3cf96-157">Pour ce faire, utilisez l’**indicateur -N** pour Linux, et l’**indicateur -ns** pour Windows.</span><span class="sxs-lookup"><span data-stu-id="3cf96-157">This is done by using the **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-to-windows"></a><span data-ttu-id="3cf96-158">De Linux vers Windows :</span><span class="sxs-lookup"><span data-stu-id="3cf96-158">From Linux to Windows:</span></span>

<span data-ttu-id="3cf96-159">Récepteur <Windows> :</span><span class="sxs-lookup"><span data-stu-id="3cf96-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="3cf96-160">Expéditeur <Linux>:</span><span class="sxs-lookup"><span data-stu-id="3cf96-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-to-linux"></a><span data-ttu-id="3cf96-161">De Windows vers Linux :</span><span class="sxs-lookup"><span data-stu-id="3cf96-161">From Windows to Linux:</span></span>

<span data-ttu-id="3cf96-162">Récepteur <Linux> :</span><span class="sxs-lookup"><span data-stu-id="3cf96-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="3cf96-163">Expéditeur <Windows> :</span><span class="sxs-lookup"><span data-stu-id="3cf96-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="3cf96-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3cf96-164">Next steps</span></span>
* <span data-ttu-id="3cf96-165">En fonction des résultats, vous pourriez être en mesure [d’optimiser le de débit réseau](virtual-network-optimize-network-bandwidth.md) pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="3cf96-165">Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="3cf96-166">Découvrez-en davantage avec la [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3cf96-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
