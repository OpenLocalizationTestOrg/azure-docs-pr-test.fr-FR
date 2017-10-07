---
title: "problèmes d’activation aaaTroubleshoot Windows machine virtuelle dans Azure | Documents Microsoft"
description: "Fournit des hello résoudre les étapes de résolution des problèmes d’activation de machine virtuelle Windows dans Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Résoudre des problèmes liés à l’activation de machines virtuelles Windows Azure

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Si vous rencontrez des problèmes lors de l’activation d’Azure Windows virtual machine (VM) qui est créé à partir d’une image personnalisée, vous pouvez utiliser les informations de hello fournies dans ce problème de hello tootroubleshoot document. 

## <a name="symptom"></a>Symptôme

Lorsque vous essayez de tooactivate une machine virtuelle de Windows Azure, vous recevez une erreur hello suivant l’exemple est semblable à :

**Erreur : 0xC004F074 hello LicensingService de logiciels a signalé que cet ordinateur hello n’a pas pu être activé. Aucun service de gestion des clés (KMS) n’a pu être contacté. Consultez hello journal des événements pour plus d’informations.**

## <a name="cause"></a>Cause :
En général, Azure VM activation rencontrer des problèmes si hello machine virtuelle Windows n’est pas configurée par à l’aide de hello clé KMS client le programme d’installation ou hello machine virtuelle Windows possède un toohello de problème de connectivité service Azure KMS (kms.core.windows.net, port 1668). 

## <a name="solution"></a>Solution

>[!NOTE]
>Si vous utilisez un VPN de site à site et forcé de tunneling, consultez [utilisez Azure personnalisée achemine l’activation KMS tooenable avec le tunneling forcé](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx). 
>
>Si vous utilisez ExpressRoute et que vous avez publiée d’un itinéraire par défaut, consultez [machine virtuelle Azure peut basculer tooactivate ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>Étape 1 configurer hello client le programme d’installation clé KMS (pour Windows Server 2016 et Windows Server 2012 R2)

Pour hello machine virtuelle qui est créé à partir d’une image personnalisée de Windows Server 2016 ou Windows Server 2012 R2, vous devez configurer hello client le programme d’installation clé KMS pour hello machine virtuelle.

Cette étape ne s’applique pas tooWindows 2012 ou Windows 2008 R2. Il utilise la fonctionnalité de l’Activation d’ordinateur virtuel (AVMA) Automation hello, qui est pris en charge uniquement par Windows Server 2016 et Windows Server 2012 R2.

1. Exécutez **slmgr.vbs /dlv** dans une invite de commandes avec élévation de privilèges. Vérifiez hello valeur de Description dans la sortie de hello et déterminer si elle a été créée à partir de la vente au détail (canal de vente au détail) ou le support de licence en volume (VOLUME_KMSCLIENT) :
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Si **slmgr.vbs /dlv** montre le canal de vente au détail, exécutez hello suivant hello tooset de commandes [clé le programme d’installation du client KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) utilisée pour la version de hello de Windows Server et forcer l’activation de tooretry : 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Par exemple, pour Windows Server Datacenter 2016, vous exécuteriez hello de commande suivante :

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>Étape 2 hello Vérifiez la connectivité entre hello machine virtuelle et le service KMS de Azure

1. Téléchargez et extrayez hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) dossier local de tooa outil Bonjour machine virtuelle qui n’est pas activé. 

2. Accédez tooStart, effectuez une recherche sur Windows PowerShell, avec le bouton droit de Windows PowerShell, puis sélectionnez Exécuter en tant qu’administrateur.

3. Assurez-vous que ce hello que machine virtuelle est configurée toouse hello correcte Azure KMS du serveur. toodo cela, exécutez la commande suivante :
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    commande Hello doit retourner : nom d’ordinateur de Service de gestion de clés défini tookms.core.windows.net:1688 avec succès.

4. Vérifier à l’aide de Psping que vous avez connectivité toohello KMS serveur. Basculez le dossier toohello où vous avez extrait le téléchargement de Pstools.zip hello et puis exécutez hello qui suit :
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  Dans la ligne de la dernière seconde hello de sortie de hello, assurez-vous que vous voyez : envoyés = 4, reçus = 4, perdus = 0 (perte 0 %).

  Si la perte est supérieure à 0 (zéro), hello machine virtuelle n’a pas de serveur de connectivité toohello KMS. Dans ce cas, si hello machine virtuelle est dans un réseau virtuel et spécifié a un serveur DNS personnalisé, vous devez vous assurer que serveur DNS est en mesure de tooresolve kms.core.windows.net. Ou bien, modifiez hello DNS server tooone qui se résout kms.core.windows.net.

  Notez que si vous supprimez l’ensemble des serveurs DNS du réseau virtuel, les machines virtuelles utiliseront le service DNS interne d’Azure. Ce service peut résoudre kms.core.windows.net.
  
Vérifiez également que le pare-feu hello invité n’a pas été configuré de manière susceptibles de bloquer les tentatives d’activation.

5. Après avoir vérifié tookms.core.windows.net de connectivité, exécutez hello suivant de commande à l’invite Windows PowerShell avec élévation de privilèges. Cette commande tente plusieurs fois l’activation.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

Une activation réussie retourne des informations semblables hello suivantes :

**Activation de Windows(R), édition ServerDatacenter (12345678-1234-1234-1234-12345678)... Le produit a été activé.**

## <a name="faq"></a>Forum Aux Questions 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>J’ai créé hello Windows Server 2016 à partir d’Azure Marketplace. Dois-je tooconfigure clés d’activation hello Windows Server 2016 ? 
 
Non. image Hello dans Azure Marketplace a hello client le programme d’installation clé KMS déjà configuré. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>Travail d’activation de Windows hello même façon quel que soit si hello machine virtuelle utilise Azure hybride utilisez avantage (HUB) ou non ? 
 
Oui. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>Que se passe-t-il en cas d’expiration de la période d’activation de Windows ? 
 
Lorsque hello la période de grâce a expiré et si Windows n’est pas encore activé, Windows Server 2008 R2 et versions ultérieures de Windows affichera des notifications supplémentaires sur l’activation. peint Hello reste noir et mise à jour Windows installera la sécurité et des mises à jour critiques uniquement, mais pas facultatifs mises à jour. Consultez les Notifications de hello section bas hello hello [Conditions de licence](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.   

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
