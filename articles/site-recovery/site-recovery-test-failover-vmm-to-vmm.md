---
title: basculement aaaTest (tooVMM VMM) dans Azure Site Recovery | Documents Microsoft
description: "Azure Site Recovery coordonne la réplication hello, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. En savoir plus sur tooAzure de basculement ou un centre de données secondaire."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: pratshar
ms.openlocfilehash: 6b4f65ab692cbb0665102c4f51ea0694151cd3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-failover-vmm-toovmm-in-site-recovery"></a>Test de basculement (tooVMM VMM) en mode de récupération de Site


Cet article fournit des informations et des instructions relatives à l’exécution d’un test de basculement ou d’un test de récupération d’urgence de machines virtuelles et de serveurs physiques protégés par Azure Site Recovery. Vous utiliserez un site géré par System Center Virtual Machine Manager VMM local en tant que site de récupération hello.

Vous exécutez un toovalidate de basculement de test de votre stratégie de réplication ou effectuez un exercice de récupération d’urgence sans temps mort ni perte de données. Un test de basculement n’a aucune incidence sur la réplication en cours de hello ou sur votre environnement de production. Vous pouvez l’exécuter sur une machine virtuelle ou sur un [plan de récupération](site-recovery-create-recovery-plans.md). Lorsque vous êtes déclenchement d’un test de basculement, vous devez réseau hello toospecify auquel les machines virtuelles de test hello se connecteront. Vous pouvez suivre la progression de hello hello du basculement de test sur hello **travaux** page.  

Si vous avez des commentaires ou des questions, faites-nous part bas hello de cet article ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hello-infrastructure-for-test-failover"></a>Préparer l’infrastructure de hello pour test de basculement
Si vous voulez toorun un test de basculement à l’aide d’un réseau existant, vous devez préparer Active Directory, DHCP et DNS dans ce réseau.

Si vous voulez toorun un test de basculement à l’aide de réseaux d’ordinateurs virtuels hello option toocreate automatiquement, ajoutez une étape manuelle avant groupe 1 hello plan de récupération que vous allez toouse pour test de basculement hello. Ajoutez ensuite toohello de ressources d’infrastructure hello automatiquement créé réseau avant d’exécuter le test de basculement hello.

### <a name="things-toonote"></a>Éléments toonote
Lorsque vous effectuez une réplication tooa du site secondaire, type hello du réseau que hello réplica ordinateur utilise n’a pas besoin de type hello de toomatch de réseau logique utilisé pour le test de basculement, mais certaines combinaisons peut ne pas fonctionnent. Si le réplica de hello utilise DHCP et isolation basés sur le réseau local virtuel, réseau d’ordinateurs virtuels hello pour les réplicas hello n’a pas besoin d’un pool d’adresses IP statiques. À l’aide de la virtualisation de réseau Windows pour le basculement de test hello ne fonctionne pas, car aucun pool d’adresses n’est disponibles. 

En outre, test de basculement hello ne fonctionne pas si le réseau de réplica hello utilise sans isolation et réseau de test hello utilise la virtualisation de réseau Windows. Il s’agit car réseau sans isolation de hello n’a pas toocreate requis de sous-réseaux hello un réseau de virtualisation de réseau Windows.

Comment les machines virtuelles de réplication sont toomapped connecté les réseaux de machines virtuelles après que basculement dépend de la configuration de réseau d’ordinateurs virtuels hello dans la console VMM hello.

#### <a name="vm-network-configured-with-no-isolation-or-vlan-isolation"></a>Réseau de machines virtuelles configuré sans isolation ou avec isolation du VLAN
Si DHCP est défini pour le réseau d’ordinateurs virtuels hello, hello ordinateur virtuel est connecté toohello ID de VLAN via les paramètres de hello sont spécifiés pour le site de réseau hello dans le réseau logique associé soient hello. machine virtuelle de Hello reçoit son adresse IP à partir du serveur DHCP disponible de hello. 

Vous n’avez pas besoin toodefine un pool d’adresses IP statiques pour le réseau d’ordinateurs virtuels hello cible. Si un pool d’adresses IP statiques est utilisé pour le réseau d’ordinateurs virtuels hello, hello ordinateur virtuel est connecté toohello ID de VLAN via les paramètres de hello sont spécifiés pour le site de réseau hello dans le réseau logique associé soient hello.

machine virtuelle de Hello reçoit son adresse IP hello pool de qui est défini pour le réseau d’ordinateurs virtuels hello. Si un pool d’adresses IP statiques n’est pas défini sur le réseau d’ordinateurs virtuels hello cible, l’allocation d’adresse IP échoue. Créer un pool d’adresses IP hello sur les deux hello serveurs source et cible VMM que vous allez utiliser pour la protection et de récupération.

#### <a name="vm-network-with-windows-network-virtualization"></a>Réseau de machines virtuelles avec virtualisation de réseau Windows
Si un réseau d’ordinateurs virtuels est configuré avec la virtualisation de réseau Windows, vous devez définir un pool statique hello cible réseau de machines virtuelles, indépendamment de si le réseau d’ordinateurs virtuels source hello est configuré toouse DHCP ou un pool d’adresses IP statiques. 

Si vous définissez DHCP, serveur VMM de hello cible agit comme un serveur DHCP et fournit une adresse IP à partir du pool de hello est défini pour le réseau d’ordinateurs virtuels hello cible. Si l’utilisation d’un pool d’adresses IP statiques est définie pour le serveur de source de hello, le serveur VMM de hello cible alloue une adresse IP à partir du pool de hello. Dans les deux cas, le processus d’allocation d’une adresse IP échoue si aucun pool d’adresses IP statiques n’est défini.


### <a name="prepare-dhcp"></a>Préparer le service DHCP
Si les ordinateurs virtuels hello impliqué dans test de basculement utilisent DHCP, créez un serveur DHCP de test dans un réseau isolé de hello à des fins de hello du test de basculement.

### <a name="prepare-active-directory"></a>Préparation du système Active Directory
toorun un test de basculement pour tester l’application, vous avez besoin une copie de l’environnement Active Directory de production hello dans votre environnement de test. Pour plus d’informations, consultez hello [considérations relatives au basculement pour Active Directory de test](site-recovery-active-directory.md#test-failover-considerations).

### <a name="prepare-dns"></a>Préparer le service DNS
Préparez un serveur DNS pour le basculement de test hello comme suit :

* **DHCP**: si les machines virtuelles utilisent DHCP, hello adresseIP du test de hello DNS doit être mis à jour sur le serveur DHCP de test hello. Si vous utilisez un type de réseau de virtualisation de réseau Windows, serveur VMM de hello joue le rôle de serveur DHCP de hello. Par conséquent, adresse IP de hello du serveur DNS doit être à jour dans le réseau de basculement de test hello. Dans ce cas, les ordinateurs virtuels hello inscrire toohello serveur DNS.
* **Adresse statique**: si les ordinateurs virtuels utilisent une adresse IP statique, hello adresse IP du serveur DNS doit être mis à jour dans le réseau de test de basculement de test de hello. Vous devrez peut-être tooupdate DNS avec l’adresse IP de hello hello virtuels des ordinateurs de test. Vous pouvez utiliser hello suivant l’exemple de script à cet effet :

        Param(
        [string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="run-a-test-failover"></a>Exécution d’un test de basculement
Cette procédure décrit comment toorun un test de basculement pour la récupération d’un plan. Vous pouvez également exécuter basculement hello pour une seule machine virtuelle sur hello **virtuels** onglet.

![Panneau Test de basculement](./media/site-recovery-test-failover-vmm-to-vmm/TestFailover.png)

1. Sélectionnez **Plans de récupération** > *nom_planrécupération*. Cliquez sur **Type de basculement** > **Test Type de basculement**.
1. Sur hello **le Test de basculement** panneau, spécifiez comment les machines virtuelles doivent être connectés toonetworks après le basculement de test hello. Pour plus d’informations, consultez hello [options réseau](#network-options-in-site-recovery).
1. Suivre la progression du basculement sur hello **travaux** onglet.
1. Une fois le basculement terminé, vérifiez que les ordinateurs virtuels hello démarrent.
1. Lorsque vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello. Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello. Cette étape supprime hello ordinateurs virtuels et des réseaux qui ont été créés pendant le test de basculement.


## <a name="network-options-in-site-recovery"></a>Options réseau de Site Recovery

Lorsque vous exécutez un test de basculement, vous êtes invité tooselect des paramètres de réseau pour les ordinateurs de réplica de test. Plusieurs options s’offrent à vous.  

| **Option de test de basculement** | **Description** | **Vérification du basculement** | **Détails** |
| --- | --- | --- | --- |
| **Basculer tooa site VMM secondaire--sans réseau** |Ne sélectionnez aucun réseau de machines virtuelles. |Vérifie que les machines de test sont créées.<br/><br/>machine virtuelle de test Hello est créé sur l’ordinateur hôte de hello où la machine virtuelle de réplication hello existe. Il n’est pas ajouté cloud toohello où se trouve la machine virtuelle de réplication hello. |<p>machine de basculé Hello n’est pas connecté tooany réseau.<br/><br/>machine de Hello peut être connecté tooa réseau d’ordinateurs virtuels après que qu’elle a été créée. |
| **Basculer tooa site VMM secondaire--avec le réseau** |Sélectionnez un réseau de machines virtuelles existant. |Vérifie la création des machines virtuelles. |machine virtuelle de test Hello est créé sur l’ordinateur hôte de hello où la machine virtuelle de réplication hello existe. Il n’est pas ajouté cloud toohello où se trouve la machine virtuelle de réplication hello.<br/><br/>Créez un réseau de machines virtuelles isolé de votre réseau de production.<br/><br/>Si vous utilisez un réseau basé sur un réseau VLAN, nous vous recommandons de créer un réseau logique distinct (non utilisé en production) dans VMM, à cet effet. Ce réseau logique est utilisé toocreate réseaux d’ordinateurs virtuels pour les tests de basculement.<br/><br/>réseau logique de Hello doit être associé au moins une des cartes réseau de hello de tous les serveurs Hyper-V hello hébergeant des ordinateurs virtuels.<br/><br/>Pour les réseaux logiques de réseau local virtuel, hello sites réseau que vous ajoutez le réseau logique de toohello doivent être isolés.<br/><br/>Si vous utilisez un réseau logique basé sur la fonction de virtualisation réseau Windows, Azure Site Recovery crée automatiquement des réseaux de machines virtuelles isolés. |
| **Échec sur le site VMM secondaire tooa--créer un réseau** |Un réseau de test temporaire est créé automatiquement en fonction de paramètre hello que vous spécifiez dans **réseau logique** et ses sites réseau associés. |Vérifie la création des machines virtuelles. |Utilisez cette option si le plan de récupération hello utilise plus d’un réseau d’ordinateurs virtuels. Si vous utilisez des réseaux de virtualisation de réseau Windows, cette option peut automatiquement créer des réseaux d’ordinateurs virtuels avec hello mêmes paramètres (sous-réseaux et pools d’adresses IP) dans le réseau hello de machine virtuelle de réplication hello. Ces réseaux de machines virtuelles est automatiquement supprimés une fois le test de basculement hello est terminée.</p><p>machine virtuelle de test Hello est créé sur l’ordinateur hôte de hello où la machine virtuelle de réplication hello existe. Il n’est pas ajouté cloud toohello où se trouve la machine virtuelle de réplication hello. |

> [!TIP]
> adresse IP donnée à ordinateur virtuel de tooa pendant le test de basculement Hello est hello recevrait la même adresse IP que hello d’ordinateur virtuel pour un basculement planifié ou non planifié (en supposant qu’adresse hello est disponible dans le réseau de basculement de test hello). Hello même adresse IP n’est pas disponible dans le réseau de basculement de test hello, ordinateur virtuel de hello reçoit une autre adresse IP qui est disponible dans le réseau de basculement de test hello.
>
>


## <a name="test-failover-tooa-production-network-on-a-recovery-site"></a>Réseau de production de tooa de basculement de test sur un site de récupération
Lorsque vous effectuez un test de basculement, nous vous conseillons de choisir un réseau différent de celui du site de récupération de production que vous avez indiqué dans [Mappage réseau](https://docs.microsoft.com/azure/site-recovery/site-recovery-network-mapping). Toutefois, si vous voulez vraiment de connectivité de réseau de bout en bout toovalidate dans une machine virtuelle d’ayant basculé, notez hello les points suivants :

* Vérifiez que hello l’ordinateur virtuel principal est arrêté lorsque vous effectuez un test de basculement hello. Si vous ne le faites pas, les deux ordinateurs virtuels avec hello même identité sera exécuté dans hello même réseau à hello même temps. Cette situation peut entraîner des conséquences tooundesired.
* Les modifications que vous apportez toohello basculer des machines virtuelles de test sont perdues lors du nettoyage hello test basculer des machines virtuelles. Ces modifications ne sont pas répliquées toohello précédent l’ordinateur virtuel principal.
* Cette méthode de tests conduit toodowntime pour votre application de production. Demandez aux utilisateurs de l’application hello toouse pas à l’application hello lors de la récupération d’urgence de hello permet d’accéder est en cours d’exécution.  


## <a name="next-steps"></a>Étapes suivantes
Une fois que votre test de basculement a réussi, vous pouvez essayer d’effectuer un [basculement](site-recovery-failover.md).
