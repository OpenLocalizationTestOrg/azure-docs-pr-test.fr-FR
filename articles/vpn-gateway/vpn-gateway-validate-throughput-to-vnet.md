---
title: "Valider les VPN débit tooa réseau virtuel Microsoft Azure | Documents Microsoft"
description: "objectif de ce document Hello est toohelp un utilisateur de valider le débit du réseau à partir de leur tooan de ressources local machine virtuelle Azure hello."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="0a96b-103">Comment réseau virtuel de toovalidate VPN débit tooa</span><span class="sxs-lookup"><span data-stu-id="0a96b-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="0a96b-104">Une connexion de passerelle VPN vous permet de tooestablish sécurisée, la connectivité intersite entre votre réseau virtuel dans Azure et votre service informatique.</span><span class="sxs-lookup"><span data-stu-id="0a96b-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="0a96b-105">Cet article explique comment toovalidate débit du réseau à partir de hello local ressources tooan machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="0a96b-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="0a96b-106">Il fournit également des instructions de dépannage.</span><span class="sxs-lookup"><span data-stu-id="0a96b-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="0a96b-107">Cet article vise toohelp diagnostiquer et résoudre les problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="0a96b-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="0a96b-108">En cas de problème de hello toosolve impossible à l’aide de hello suivant d’informations, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="0a96b-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="0a96b-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0a96b-109">Overview</span></span>

<span data-ttu-id="0a96b-110">Hello connexion à la passerelle VPN implique hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="0a96b-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="0a96b-111">Appareils VPN sur site (afficher la liste des [appareils VPN validés)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="0a96b-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="0a96b-112">Internet public</span><span class="sxs-lookup"><span data-stu-id="0a96b-112">Public Internet</span></span>
- <span data-ttu-id="0a96b-113">Passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="0a96b-113">Azure VPN gateway</span></span>
- <span data-ttu-id="0a96b-114">Machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="0a96b-114">Azure virtual machine</span></span>

<span data-ttu-id="0a96b-115">Hello suivant schéma montre la connectivité logique de hello d’un tooan de réseau sur site réseau virtuel Azure via VPN.</span><span class="sxs-lookup"><span data-stu-id="0a96b-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![Logique tooMSFT de connectivité de réseau de client réseau à l’aide de VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="0a96b-117">Calculer hello maximale attendue entrées/sorties</span><span class="sxs-lookup"><span data-stu-id="0a96b-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="0a96b-118">Déterminez les exigences de débit de base de votre application.</span><span class="sxs-lookup"><span data-stu-id="0a96b-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="0a96b-119">Déterminez les limites de débit de votre passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="0a96b-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="0a96b-120">Pour obtenir l’aide, voir section hello « débit par type de VPN et de référence (SKU) » [planification et conception pour la passerelle VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="0a96b-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="0a96b-121">Déterminer hello [des conseils de débit de machine virtuelle Azure](../virtual-machines/virtual-machines-windows-sizes.md) pour la taille de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0a96b-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="0a96b-122">Déterminez la bande passante de votre fournisseur d’accès à Internet (FAI).</span><span class="sxs-lookup"><span data-stu-id="0a96b-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="0a96b-123">Calculez le débit prévu - Bande passante la plus basse entre machine virtuelle et passerelle FAI * 0,8.</span><span class="sxs-lookup"><span data-stu-id="0a96b-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="0a96b-124">Si votre débit calculé ne répond pas aux exigences de débit de base de votre application, vous devez la bande passante de hello tooincrease de ressource hello que vous avez identifié comme goulot d’étranglement hello.</span><span class="sxs-lookup"><span data-stu-id="0a96b-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="0a96b-125">tooresize une passerelle VPN Azure, consultez [la modification d’une référence (SKU) de la passerelle](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="0a96b-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="0a96b-126">tooresize une machine virtuelle, consultez [redimensionner une machine virtuelle](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="0a96b-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="0a96b-127">Si vous ne rencontrez pas de bande passante Internet attendue, vous pouvez également toocontact votre fournisseur de services Internet.</span><span class="sxs-lookup"><span data-stu-id="0a96b-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="0a96b-128">Validation du débit réseau à l’aide d’outils de performances</span><span class="sxs-lookup"><span data-stu-id="0a96b-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="0a96b-129">Cette validation doit être effectuée pendant les heures creuses, car la saturation de débit de tunnel VPN pendant le test empêche les résultats précis.</span><span class="sxs-lookup"><span data-stu-id="0a96b-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="0a96b-130">outil de Hello que nous utilisons pour ce test est iPerf, qui fonctionne sur Windows et Linux et possède des modes de client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="0a96b-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="0a96b-131">Il est limité too3 Gbits/s pour les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="0a96b-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="0a96b-132">Cet outil n’effectue pas de n’importe quel toodisk d’opérations de lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="0a96b-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="0a96b-133">Il génère uniquement le trafic TCP généré automatiquement à partir d’une fin toohello autres.</span><span class="sxs-lookup"><span data-stu-id="0a96b-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="0a96b-134">Il généré des statistiques basées sur une expérimentation qui mesure hello de bande passante disponible entre les nœuds de client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="0a96b-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="0a96b-135">Lorsque vous testez entre deux nœuds, une joue le serveur de hello et hello sous la forme d’un client.</span><span class="sxs-lookup"><span data-stu-id="0a96b-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="0a96b-136">Une fois ce test est terminé, nous vous recommandons d’inverser hello rôles tootest à la fois téléchargement des débit sur les deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="0a96b-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="0a96b-137">Télécharger iPerf</span><span class="sxs-lookup"><span data-stu-id="0a96b-137">Download iPerf</span></span>
<span data-ttu-id="0a96b-138">Téléchargez [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="0a96b-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="0a96b-139">Pour plus d’informations, consultez la [Documentation d’iPerf](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="0a96b-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="0a96b-140">Hello des produits tiers dont traite cet article sont fabriqués par des sociétés indépendantes de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a96b-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="0a96b-141">Microsoft exclut toute garantie, expresse ou implicite, concernant les performances de hello ou la fiabilité de ces produits.</span><span class="sxs-lookup"><span data-stu-id="0a96b-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="0a96b-142">Exécutez iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="0a96b-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="0a96b-143">Activer une règle de groupe de sécurité réseau/ACL autorisant le trafic de hello (pour l’adresse IP publique de test sur une machine virtuelle Azure).</span><span class="sxs-lookup"><span data-stu-id="0a96b-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="0a96b-144">Sur les deux nœuds, activez une exception de pare-feu pour le port 5001.</span><span class="sxs-lookup"><span data-stu-id="0a96b-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="0a96b-145">**Windows :** suivant de hello exécuter de commandes en tant qu’administrateur :</span><span class="sxs-lookup"><span data-stu-id="0a96b-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="0a96b-146">règle de hello tooremove lors du test est terminée, exécutez la commande :</span><span class="sxs-lookup"><span data-stu-id="0a96b-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="0a96b-147">**Linux Azure :** les images Linux Azure sont dotées de pare-feu permissifs.</span><span class="sxs-lookup"><span data-stu-id="0a96b-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="0a96b-148">S’il existe une application qui écoute sur un port, le trafic de hello est autorisé par le biais.</span><span class="sxs-lookup"><span data-stu-id="0a96b-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="0a96b-149">Les images personnalisées qui sont sécurisées peuvent nécessiter l’ouverture explicite des ports.</span><span class="sxs-lookup"><span data-stu-id="0a96b-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="0a96b-150">Les pare-feu de couche système courants pour Linux comprennent `iptables`, `ufw` et `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="0a96b-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="0a96b-151">Sur le nœud du serveur hello, basculez toohello où iperf3.exe est extrait.</span><span class="sxs-lookup"><span data-stu-id="0a96b-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="0a96b-152">Puis exécutez iPerf en mode serveur et définissez-le toolisten sur le port 5001 comme hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="0a96b-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="0a96b-153">Sur le nœud de client hello, basculez toohello où iperf outil est extrait et puis exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0a96b-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="0a96b-154">client de Hello est INDUISANT le trafic sur le serveur à port 5001 toohello pendant 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="0a96b-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="0a96b-155">Hello indicateur '-P ' qui indique que nous utilisons le nœud du serveur toohello 32 connexions simultanées.</span><span class="sxs-lookup"><span data-stu-id="0a96b-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="0a96b-156">Hello d’écran suivante montre la sortie de cet exemple hello :</span><span class="sxs-lookup"><span data-stu-id="0a96b-156">hello following screen shows hello output from this example:</span></span>

    ![Sortie](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="0a96b-158">Hello toopreserve (facultatif) test des résultats, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0a96b-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="0a96b-159">Après avoir effectué les étapes précédentes hello, exécutez hello inversé de la même procédure avec les rôles de hello, afin que hello nœud du serveur seront désormais client de hello et vice versa.</span><span class="sxs-lookup"><span data-stu-id="0a96b-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="0a96b-160">Résolution des problèmes de copie lente des fichiers</span><span class="sxs-lookup"><span data-stu-id="0a96b-160">Address slow file copy issues</span></span>
<span data-ttu-id="0a96b-161">Vous pouvez rencontrer des problèmes de copie trop lente de fichiers lorsque vous utilisez l’Explorateur Windows ou le glisser-déplacer via une session RDP.</span><span class="sxs-lookup"><span data-stu-id="0a96b-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="0a96b-162">Ce problème est normalement dû tooone ou les deux de hello suivant facteurs :</span><span class="sxs-lookup"><span data-stu-id="0a96b-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="0a96b-163">Les applications de copie de fichiers, comme l’Explorateur Windows et le protocole RDP, n’utilisent pas plusieurs threads lors de la copie des fichiers.</span><span class="sxs-lookup"><span data-stu-id="0a96b-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="0a96b-164">Pour de meilleures performances, utilisez une application de copie de fichier multithread comme [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy des fichiers à l’aide de 16 ou 32 threads.</span><span class="sxs-lookup"><span data-stu-id="0a96b-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="0a96b-165">Cliquez sur le numéro de thread toochange hello pour la copie des fichiers dans Richcopy, **Action** > **options de copie** > **copie d’un fichier**.</span><span class="sxs-lookup"><span data-stu-id="0a96b-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="0a96b-166">
![Problèmes de copie lente de fichiers](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="0a96b-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="0a96b-167">La vitesse en lecture/écriture du disque de la machine virtuelle est insuffisante.</span><span class="sxs-lookup"><span data-stu-id="0a96b-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="0a96b-168">Pour plus d'informations, consultez [Dépannage Azure Storage](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0a96b-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="0a96b-169">Interface externe avec appareil local</span><span class="sxs-lookup"><span data-stu-id="0a96b-169">On-premises device external facing interface</span></span>
<span data-ttu-id="0a96b-170">Si hello localement le périphérique VPN adresse IP du côté Internet est inclus dans hello [réseau local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) définition dans Azure, vous pouvez rencontrer toobring incapacité hello VPN, sporadique se déconnecte, ou des problèmes de performances.</span><span class="sxs-lookup"><span data-stu-id="0a96b-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="0a96b-171">Vérification de la latence</span><span class="sxs-lookup"><span data-stu-id="0a96b-171">Checking latency</span></span>
<span data-ttu-id="0a96b-172">Utiliser tracert tootrace tooMicrosoft Azure bord périphérique toodetermine s’il existe des retards supérieure à 100 ms entre sauts.</span><span class="sxs-lookup"><span data-stu-id="0a96b-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="0a96b-173">Hello sur un réseau local, exécutez *tracert* toohello VIP de hello passerelle Azure ou la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0a96b-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="0a96b-174">Une fois que vous voyez uniquement * retourné, vous savez hello bord Azure a été atteinte.</span><span class="sxs-lookup"><span data-stu-id="0a96b-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="0a96b-175">Lorsque vous voyez les noms DNS qui incluent « MSN » est retournée, vous savez que vous avez atteint la dorsale principale de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="0a96b-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="0a96b-176">
![Vérification de la latence](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="0a96b-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a96b-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0a96b-177">Next steps</span></span>
<span data-ttu-id="0a96b-178">Pour plus d’informations ou de l’aide, consultez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="0a96b-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="0a96b-179">Optimiser le débit du réseau des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="0a96b-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="0a96b-180">Support Microsoft</span><span class="sxs-lookup"><span data-stu-id="0a96b-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
