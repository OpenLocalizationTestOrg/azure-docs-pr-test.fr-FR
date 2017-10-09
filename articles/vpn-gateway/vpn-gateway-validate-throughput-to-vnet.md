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
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>Comment réseau virtuel de toovalidate VPN débit tooa

Une connexion de passerelle VPN vous permet de tooestablish sécurisée, la connectivité intersite entre votre réseau virtuel dans Azure et votre service informatique.

Cet article explique comment toovalidate débit du réseau à partir de hello local ressources tooan machine virtuelle Azure. Il fournit également des instructions de dépannage.

>[!NOTE]
>Cet article vise toohelp diagnostiquer et résoudre les problèmes courants. En cas de problème de hello toosolve impossible à l’aide de hello suivant d’informations, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Vue d'ensemble

Hello connexion à la passerelle VPN implique hello suivant des composants :

- Appareils VPN sur site (afficher la liste des [appareils VPN validés)](vpn-gateway-about-vpn-devices.md#devicetable).
- Internet public
- Passerelle VPN Azure
- Machine virtuelle Azure

Hello suivant schéma montre la connectivité logique de hello d’un tooan de réseau sur site réseau virtuel Azure via VPN.

![Logique tooMSFT de connectivité de réseau de client réseau à l’aide de VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Calculer hello maximale attendue entrées/sorties

1.  Déterminez les exigences de débit de base de votre application.
2.  Déterminez les limites de débit de votre passerelle VPN Azure. Pour obtenir l’aide, voir section hello « débit par type de VPN et de référence (SKU) » [planification et conception pour la passerelle VPN](vpn-gateway-plan-design.md).
3.  Déterminer hello [des conseils de débit de machine virtuelle Azure](../virtual-machines/virtual-machines-windows-sizes.md) pour la taille de votre machine virtuelle.
4.  Déterminez la bande passante de votre fournisseur d’accès à Internet (FAI).
5.  Calculez le débit prévu - Bande passante la plus basse entre machine virtuelle et passerelle FAI * 0,8.

Si votre débit calculé ne répond pas aux exigences de débit de base de votre application, vous devez la bande passante de hello tooincrease de ressource hello que vous avez identifié comme goulot d’étranglement hello. tooresize une passerelle VPN Azure, consultez [la modification d’une référence (SKU) de la passerelle](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). tooresize une machine virtuelle, consultez [redimensionner une machine virtuelle](../virtual-machines/virtual-machines-windows-resize-vm.md). Si vous ne rencontrez pas de bande passante Internet attendue, vous pouvez également toocontact votre fournisseur de services Internet.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Validation du débit réseau à l’aide d’outils de performances

Cette validation doit être effectuée pendant les heures creuses, car la saturation de débit de tunnel VPN pendant le test empêche les résultats précis.

outil de Hello que nous utilisons pour ce test est iPerf, qui fonctionne sur Windows et Linux et possède des modes de client et le serveur. Il est limité too3 Gbits/s pour les machines virtuelles Windows.

Cet outil n’effectue pas de n’importe quel toodisk d’opérations de lecture/écriture. Il génère uniquement le trafic TCP généré automatiquement à partir d’une fin toohello autres. Il généré des statistiques basées sur une expérimentation qui mesure hello de bande passante disponible entre les nœuds de client et le serveur. Lorsque vous testez entre deux nœuds, une joue le serveur de hello et hello sous la forme d’un client. Une fois ce test est terminé, nous vous recommandons d’inverser hello rôles tootest à la fois téléchargement des débit sur les deux nœuds.

### <a name="download-iperf"></a>Télécharger iPerf
Téléchargez [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Pour plus d’informations, consultez la [Documentation d’iPerf](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >Hello des produits tiers dont traite cet article sont fabriqués par des sociétés indépendantes de Microsoft. Microsoft exclut toute garantie, expresse ou implicite, concernant les performances de hello ou la fiabilité de ces produits.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Exécutez iPerf (iperf3.exe)
1. Activer une règle de groupe de sécurité réseau/ACL autorisant le trafic de hello (pour l’adresse IP publique de test sur une machine virtuelle Azure).

2. Sur les deux nœuds, activez une exception de pare-feu pour le port 5001.

    **Windows :** suivant de hello exécuter de commandes en tant qu’administrateur :

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    règle de hello tooremove lors du test est terminée, exécutez la commande :

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Linux Azure :** les images Linux Azure sont dotées de pare-feu permissifs. S’il existe une application qui écoute sur un port, le trafic de hello est autorisé par le biais. Les images personnalisées qui sont sécurisées peuvent nécessiter l’ouverture explicite des ports. Les pare-feu de couche système courants pour Linux comprennent `iptables`, `ufw` et `firewalld`.

3. Sur le nœud du serveur hello, basculez toohello où iperf3.exe est extrait. Puis exécutez iPerf en mode serveur et définissez-le toolisten sur le port 5001 comme hello suivant de commandes :

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. Sur le nœud de client hello, basculez toohello où iperf outil est extrait et puis exécutez hello de commande suivante :

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    client de Hello est INDUISANT le trafic sur le serveur à port 5001 toohello pendant 30 secondes. Hello indicateur '-P ' qui indique que nous utilisons le nœud du serveur toohello 32 connexions simultanées.

    Hello d’écran suivante montre la sortie de cet exemple hello :

    ![Sortie](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. Hello toopreserve (facultatif) test des résultats, exécutez la commande suivante :

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Après avoir effectué les étapes précédentes hello, exécutez hello inversé de la même procédure avec les rôles de hello, afin que hello nœud du serveur seront désormais client de hello et vice versa.

## <a name="address-slow-file-copy-issues"></a>Résolution des problèmes de copie lente des fichiers
Vous pouvez rencontrer des problèmes de copie trop lente de fichiers lorsque vous utilisez l’Explorateur Windows ou le glisser-déplacer via une session RDP. Ce problème est normalement dû tooone ou les deux de hello suivant facteurs :

- Les applications de copie de fichiers, comme l’Explorateur Windows et le protocole RDP, n’utilisent pas plusieurs threads lors de la copie des fichiers. Pour de meilleures performances, utilisez une application de copie de fichier multithread comme [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy des fichiers à l’aide de 16 ou 32 threads. Cliquez sur le numéro de thread toochange hello pour la copie des fichiers dans Richcopy, **Action** > **options de copie** > **copie d’un fichier**.<br><br>
![Problèmes de copie lente de fichiers](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- La vitesse en lecture/écriture du disque de la machine virtuelle est insuffisante. Pour plus d'informations, consultez [Dépannage Azure Storage](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Interface externe avec appareil local
Si hello localement le périphérique VPN adresse IP du côté Internet est inclus dans hello [réseau local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) définition dans Azure, vous pouvez rencontrer toobring incapacité hello VPN, sporadique se déconnecte, ou des problèmes de performances.

## <a name="checking-latency"></a>Vérification de la latence
Utiliser tracert tootrace tooMicrosoft Azure bord périphérique toodetermine s’il existe des retards supérieure à 100 ms entre sauts.

Hello sur un réseau local, exécutez *tracert* toohello VIP de hello passerelle Azure ou la machine virtuelle. Une fois que vous voyez uniquement * retourné, vous savez hello bord Azure a été atteinte. Lorsque vous voyez les noms DNS qui incluent « MSN » est retournée, vous savez que vous avez atteint la dorsale principale de Microsoft hello.<br><br>
![Vérification de la latence](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations ou de l’aide, consultez hello suivant liens :

- [Optimiser le débit du réseau des machines virtuelles Azure](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Support Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
