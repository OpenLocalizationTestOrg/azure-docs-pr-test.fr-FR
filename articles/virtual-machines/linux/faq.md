---
title: aaaFrequently aux questions sur les machines virtuelles Linux dans Azure | Documents Microsoft
description: "Fournit des toosome réponses hello fréquemment posées sur les ordinateurs virtuels Linux créés avec le modèle de gestionnaire de ressources hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Forum aux questions sur les machines virtuelles Linux
Cet article traite des questions courantes sur les ordinateurs virtuels Linux créés dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello. Pour la version de Windows hello de cette rubrique, consultez [Forum aux questions sur les Machines virtuelles Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Qu’est-il possible d’exécuter sur une machine virtuelle Azure ?
Tous les abonnés peuvent exécuter des logiciels serveur sur une machine virtuelle Azure. Pour plus d’informations, consultez [Linux dans des distributions prises en charge par Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quelle quantité de stockage puis-je utiliser avec une machine virtuelle ?
Chaque disque de données peut être jusqu'à too1 to. nombre de Hello de disques de données que vous pouvez utiliser dépend de la taille de hello de machine virtuelle de hello. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Un compte de stockage Azure fournit le stockage de disque de système d’exploitation hello et les disques de données. Chaque disque est un fichier .vhd stocké sous la forme d’un objet blob de pages. Pour plus d’informations sur la tarification, voir [Tarification – Stockage](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Comment puis-je accéder à ma machine virtuelle ?
Établir une toolog de connexion à distance sur l’ordinateur virtuel de toohello, à l’aide de Secure Shell (SSH). Consultez les instructions de hello sur la façon de tooconnect [à partir de Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [de Linux et Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Par défaut, SSH autorise un maximum de 10 connexions simultanées. Vous pouvez augmenter ce nombre en modifiant le fichier de configuration hello.

Si vous rencontrez des problèmes, consultez [Dépanner les connexions Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>Puis-je utiliser des données de toostore hello disque temporaire (/ dev/sdb1) ?
N’utilisez pas les données de toostore salutation disque temporaire (/ dev/sdb1). Il s’agit uniquement d’un stockage temporaire. Vous risquez de perdre des données qui ne pourront pas être récupérées.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Puis-je copier ou cloner une machine virtuelle Azure ?
Oui. Pour obtenir des instructions, consultez [comment toocreate une copie de la machine virtuelle Linux dans hello modèle de déploiement de gestionnaire de ressources](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Pourquoi ne vois-je pas les régions Centre et Est du Canada dans Azure Resource Manager ?
Hello deux nouvelles régions du Canada Central et est du Canada ne sont pas automatiquement inscrits pour la création de la machine virtuelle pour les abonnements Azure existants. Cette inscription s’effectue automatiquement lorsqu’un ordinateur virtuel est déployé par le biais hello tooany portail Azure autre région à l’aide du Gestionnaire de ressources Azure. Après un ordinateur virtuel est déployé tooany autre région Azure, les régions de nouveau hello doivent être disponibles pour les ordinateurs virtuels suivants.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Puis-je ajouter un toomy de carte réseau virtuelle après sa création ?
Oui, c’est maintenant possible. Hello VM première besoins toobe arrêtée désallouée. Vous pouvez ajouter ou supprimer une carte réseau (sauf s’il est hello dernière NIC sur hello machine virtuelle). 

## <a name="are-there-any-computer-name-requirements"></a>Existe-t-il des exigences en matière de nom d’ordinateur ?
Oui. nom de l’ordinateur Hello peut être un maximum de 64 caractères. Consultez l’article [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Restrictions et règles de conventions d’affectation de noms) pour en savoir plus sur la dénomination de vos ressources.

## <a name="are-there-any-resource-group-name-requirements"></a>Existe-t-il des exigences pour le nom du groupe de ressources ?
Oui. nom de groupe de ressources Hello peut être un maximum de 90 caractères. Consultez l’article [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Restrictions et règles de conventions d’affectation de noms) pour en savoir plus sur les groupes de ressources.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Quelles sont les exigences de nom d’utilisateur hello lors de la création d’une machine virtuelle ?
Les noms d’utilisateur doivent avoir une longueur de 1 à 64 caractères.

Hello suivant des noms d’utilisateur n’est pas autorisé :

<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>
    <tr>
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
Les mots de passe doivent comporter 6-72 caractères et répondre aux 3 hors hello suivant les exigences de complexité 4 :

* Avoir des minuscules
* Avoir des majuscules
* Avoir un chiffre
* Avoir un caractère spécial (correspondances Regex [\W_])

Hello après les mots de passe n’est pas autorisé :

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$$word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Password!</td>
        <td style="text-align:center">Password1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">iloveyou!</td>
    </tr>
</table>
