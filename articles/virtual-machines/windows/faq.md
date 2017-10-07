---
title: aaaFAQ sur les machines virtuelles Windows dans Azure | Documents Microsoft
description: "Fournit des toosome réponses hello fréquemment posées sur des machines virtuelles Windows créés avec le modèle de gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Questions fréquentes sur les machines virtuelles Azure
Cet article traite des questions courantes sur des machines virtuelles Windows créés dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello. Pour la version de Linux hello de cette rubrique, consultez [Forum aux questions sur les Machines virtuelles Linux](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Qu’est-il possible d’exécuter sur une machine virtuelle Azure ?
Tous les abonnés peuvent exécuter des logiciels serveur sur une machine virtuelle Azure. Pour plus d’informations sur la stratégie de prise en charge hello pour les logiciels de serveurs Microsoft en cours d’exécution dans Azure, consultez [prise en charge des logiciels serveur Microsoft pour les Machines virtuelles Azure](https://support.microsoft.com/kb/2721672)

Certaines versions de Windows 7, Windows 8.1 et Windows 10 sont les abonnés Azure tooMSDN disponibles et les abonnés MSDN développement et de paiement à l’utilisation de Test, pour les tâches de développement et de test. Pour plus d’informations, notamment des instructions et des limitations, voir [Images de client Windows pour les abonnés MSDN](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/). 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quelle quantité de stockage puis-je utiliser avec une machine virtuelle ?
Chaque disque de données peut être jusqu'à too1 to. nombre de Hello de disques de données que vous pouvez utiliser dépend de la taille de hello de machine virtuelle de hello. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Les disques Azure gérés sont hello disque nouvelle et recommandée offres de stockage pour une utilisation avec des Machines virtuelles Azure pour le stockage persistant des données. Vous pouvez utiliser plusieurs disques managés avec chaque machine virtuelle. Ces disques offrent deux types d’options de stockage durable : les disques managés Premium et les disques managés Standard. Pour obtenir des informations sur la tarification, consultez [Tarification des disques gérés](https://azure.microsoft.com/pricing/details/managed-disks).

Comptes de stockage Azure peuvent également fournir un stockage pour les disques de données et de disque de système d’exploitation hello. Chaque disque est un fichier .vhd stocké sous la forme d’un objet blob de pages. Pour plus d’informations sur la tarification, voir [Tarification – Stockage](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Comment puis-je accéder à ma machine virtuelle ?
Établissez une connexion à distance à l’aide du protocole RDP (Remote Desktop Protocol) pour une machine virtuelle Windows. Pour obtenir des instructions, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Un maximum de deux connexions simultanées sont prises en charge, sauf si le serveur de hello est configuré comme un hôte de session des Services Bureau à distance.  

Si vous rencontrez des problèmes avec le Bureau à distance, consultez [tooa de connexions de résoudre les problèmes de bureau à distance basé sur Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Si vous êtes familiarisé avec Hyper-V, vous risquez de rechercher les un tooVMConnect similaire d’outil. Azure n’offre pas un outil similaire car l’ordinateur virtuel de console accès tooa n’est pas pris en charge.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>Puis-je utiliser des données de toostore hello disque temporaire (hello lecteur D: par défaut) ?
N’utilisez pas les données de toostore salutation disque temporaire. Il ne sert qu’au stockage temporaire. Vous risqueriez donc de perdre des données sans pouvoir les récupérer. Une perte de données peut se produire lors de la machine virtuelle de hello déplace tooa autre ordinateur hôte. Redimensionnement d’un ordinateur virtuel, la mise à jour hello hôte ou une défaillance matérielle sur l’ordinateur hôte de hello est certaines des raisons hello qu'une machine virtuelle peuvent se déplacer.

Si vous avez une application qui doit la lettre de lecteur D: toouse hello, vous pouvez réaffecter les lettres de lecteur afin qu’hello disque temporaire utilise autre chose que D:. Pour obtenir des instructions, consultez [modifier la lettre de lecteur hello du disque temporaire de Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Comment puis-je modifier hello lettre de lecteur hello temporaire disque ?
Vous pouvez modifier la lettre de lecteur hello par déplacement du fichier page hello et en réaffectant les lettres de lecteur, mais vous devez toomake que vous hello étapes dans un ordre spécifique. Pour obtenir des instructions, consultez [modifier la lettre de lecteur hello du disque temporaire de Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>Puis-je ajouter un ensemble de disponibilité tooan machine virtuelle existant ?
Non. Si vous souhaitez que votre partie de toobe de machine virtuelle d’un ensemble de disponibilité, vous devez toocreate hello machine virtuelle dans le jeu de hello. Il n’existe actuellement pas un moyen de tooadd une machine virtuelle tooan disponibilité après que qu’elle a été créée.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>Puis-je télécharger une tooAzure de machine virtuelle ?
Oui. Pour obtenir des instructions, consultez [migration local tooAzure de machines virtuelles](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>Puis-je redimensionner le disque du système d’exploitation hello ?
Oui. Pour obtenir des instructions, consultez [comment tooexpand hello lecteur du système d’exploitation d’un ordinateur virtuel dans un groupe de ressources Azure](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Puis-je copier ou cloner une machine virtuelle Azure ?
Oui. Utilisation d’images gérés, vous pouvez créer une image d’un ordinateur virtuel et ensuite utiliser hello image toobuild plusieurs nouveaux ordinateurs virtuels. Pour obtenir des instructions, consultez [Créer une image personnalisée d’une machine virtuelle](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Pourquoi ne vois-je pas les régions Centre et Est du Canada dans Azure Resource Manager ?

Hello deux nouvelles régions du Canada Central et est du Canada ne sont pas automatiquement inscrits pour la création de la machine virtuelle pour les abonnements Azure existants. Cette inscription s’effectue automatiquement lorsqu’un ordinateur virtuel est déployé par le biais hello tooany portail Azure autre région à l’aide du Gestionnaire de ressources Azure. Après un ordinateur virtuel est déployé tooany autre région Azure, les régions de nouveau hello doivent être disponibles pour les ordinateurs virtuels suivants.

## <a name="does-azure-support-linux-vms"></a>Azure prend-il en charge les machines virtuelles Linux ?
Oui. tooquickly créer un tootry Linux VM out, consultez [créer un VM Linux sur Azure à l’aide du portail de hello](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Puis-je ajouter un toomy de carte réseau virtuelle après sa création ?
Oui, c’est maintenant possible. Hello VM première besoins toobe arrêtée désallouée. Vous pouvez ajouter ou supprimer une carte réseau (sauf s’il est hello dernière NIC sur hello machine virtuelle). 

## <a name="are-there-any-computer-name-requirements"></a>Existe-t-il des exigences en matière de nom d’ordinateur ?
Oui. nom de l’ordinateur Hello peut être un maximum de 15 caractères. Consultez l’article [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Restrictions et règles de conventions d’affectation de noms) pour en savoir plus sur la dénomination de vos ressources.

## <a name="are-there-any-resource-group-name-requirements"></a>Existe-t-il des exigences pour le nom du groupe de ressources ?
Oui. nom de groupe de ressources Hello peut être un maximum de 90 caractères. Consultez l’article [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Restrictions et règles de conventions d’affectation de noms) pour en savoir plus sur les groupes de ressources.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Quelles sont les exigences de nom d’utilisateur hello lors de la création d’une machine virtuelle ?

Les noms d’utilisateur peuvent comporter un maximum de 20 caractères et ne doivent pas se terminer par un point («. »). 


Hello suivant des noms d’utilisateur n’est pas autorisé :
<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> a</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> aspnet</td>
    </tr>
    <tr>
        <td style="text-align:center">backup </td><td style="text-align:center"> console </td><td style="text-align:center"> david </td><td style="text-align:center"> guest</td>
    </tr>
    <tr>
        <td style="text-align:center">john </td><td style="text-align:center"> propriétaire </td><td style="text-align:center"> root </td><td style="text-align:center"> server</td>
    </tr>
    <tr>
        <td style="text-align:center">sql </td><td style="text-align:center"> support </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Quelles sont les exigences de mot de passe hello lors de la création d’une machine virtuelle ?
Les mots de passe doivent être de 12-123 caractères et répondre aux 3 hors hello suivant les exigences de complexité 4 :

* Avoir des minuscules
* Avoir des majuscules
* Avoir un chiffre
* Avoir un caractère spécial (correspondances Regex [\W_])

Hello après les mots de passe n’est pas autorisé :

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$$word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Password! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>iloveyou! </td>
    </tr>
</table>
