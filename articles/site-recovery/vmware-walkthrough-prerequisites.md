---
title: "aaaPrerequisites pour la réplication tooAzure VMware à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Résume les conditions préalables de hello pour répliquer les charges de travail en cours d’exécution sur les ordinateurs virtuels VMware tooAzure, à l’aide du service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 14f8e9713b42a1d8da71223fbbb7a6b7c4303adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-vmware-tooazure-replication"></a>Étape 2 : Passez en revue les conditions préalables de hello pour la réplication tooAzure VMware

Lisez les conditions préalables de hello résumées dans hello tableau suivant.

**Configuration requise** | **Détails**
--- | ---
**Microsoft Azure** | En savoir plus sur la [configuration requise pour Azure](site-recovery-prereq.md#azure-requirements)
**Serveur de configuration local** | Vous devez disposer d’une machine virtuelle VMware Windows Server 2012 R2 ou une version ultérieure. Configurez ce serveur au cours du déploiement de Site Recovery.<br/><br/> Par le processus de hello par défaut serveur et le serveur cible maître sont également installés sur cet ordinateur virtuel. Lors de la montée en puissance, vous devrez peut-être un serveur de processus distinct, et il a hello mêmes exigences que le serveur de configuration hello.<br/><br/> Vous trouverez de plus amples informations sur ces composants [ici](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Serveurs VMware locaux** | Un ou plusieurs serveurs VMware vSphere exécutant la version 6.5, 6.0, 5.5, 5.1 avec les dernières mises à jour. Les serveurs doivent se trouver dans le même réseau que le serveur de configuration hello (ou un serveur de processus distinct) de hello.<br/><br/> Nous vous recommandons un serveur vCenter toomanage hôtes, en cours d’exécution 6.5, 6.0 ou 5.5 avec les dernières mises à jour de hello.
**Machines virtuelles locales** | Machines virtuelles que vous souhaitez tooreplicate doit être en cours d’exécution un [prise en charge du système d’exploitation](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)et être conformes avec [conditions préalables Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). La machine virtuelle doit exécuter des outils VMware.
**URLs** | serveur de configuration Hello doit accéder aux URL de toothese :<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si vous avez des règles de pare-feu basé sur l’adresse IP, assurez-vous qu’ils autorisent un tooAzure de communication.<br/></br> Autoriser hello [plages d’adresses IP Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653)et hello port HTTPS (443).<br/></br> Autoriser les plages d’adresses IP pour hello région Azure de votre abonnement et ouest des États-Unis (utilisé pour la gestion d’identité et contrôle d’accès).<br/><br/> Autoriser cette URL pour le téléchargement de MySQL hello : http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Service de mobilité** | Installé sur chaque machine virtuelle répliquée.




## <a name="limitations"></a>Limites

Assurez-vous que vous comprenez les limitations hello résumées dans le tableau de hello avant de déployer.

**Limite** | **Détails**
--- | ---
**Microsoft Azure** | Les comptes de stockage et réseau doivent être Bonjour même région que le coffre de hello<br/><br/> Si vous utilisez un compte de stockage premium, vous devez également une norme de stocker les journaux de compte de réplication toostore<br/><br/> Vous ne peut pas répliquer toopremium des comptes dans le centre et de l’Inde du Sud.
**Serveur de configuration local** | Le type d’adaptateur de machine virtuelle VMware doit être VMXNET3. Dans le cas contraire, [installez cette mise à jour](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> vSphere PowerCLI 6.0 doit être installé.<br/><br> machine de Hello ne doivent pas être un contrôleur de domaine. machine de Hello doit avoir une adresse IP statique.<br/><br/> nom d’hôte Hello doit être de 15 caractères ou moins, et le système d’exploitation doit être en anglais.
**VMware** | Site Recovery ne prend pas en charge les nouvelles fonctionnalités de vCenter et vSphere 6.5 et 6.0 telles que Cross vCenter vMotion, les volumes virtuels et le DRS de stockage.
**Machines virtuelles** | Vérifier les [limitations de la machine virtuelle Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> Vous ne pouvez pas répliquer de machines virtuelles comportant des disques chiffrés, ou des machines virtuelles avec le démarrage UEFI/EFI.<br/><br> Les clusters à disque partagé ne sont pas pris en charge. Si l’ordinateur virtuel source de hello a association de cartes réseau, il est converti tooa une seule carte réseau après le basculement.<br/><br/> Si les ordinateurs virtuels disposent d’un disque iSCSI, Site Recovery convertit fichier de disque dur virtuel tooa après le basculement. Si la cible iSCSI de hello peut être atteint par hello machine virtuelle Azure, il connecte tooit et voit il et hello disque dur virtuel. Si cela se produit, vous déconnecter de cible iSCSI hello.<br/><br/> Si vous souhaitez que la cohérence multimachine virtuelle tooenable, ce qui permet aux ordinateurs virtuels en cours d’exécution hello récupérée de la même charge de travail toobe tooa ensemble des données cohérentes point, ouvrir le port 20004 sur hello machine virtuelle.<br/><br/> Windows doit être installé sur le lecteur de hello C. disque de système d’exploitation Hello doit être de base et non dynamique. disque de données Hello peut être dynamique.<br/><br/> Les fichiers Linux/etc/hosts sur des machines virtuelles doivent contenir des entrées qui mappent des adresses de tooIP du nom d’hôte local hello associés à toutes les cartes réseau. Hello nom d’hôte, des points de montage, nom du périphérique, chemins d’accès système et noms de fichiers (/ etc. ; /usr) doit être en anglais uniquement.<br/><br/> Les types spécifiques de [stockage Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) sont pris en charge.<br/><br/>Créer ou définir **disk.enableUUID=true** dans les paramètres de machine virtuelle hello. Cela fournit un toohello UUID cohérent VMDK, afin qu’il monte correctement et garantit que les modifications delta uniquement sont transférées local tooon arrière lors du retour arrière, sans réplication complète.


## <a name="next-steps"></a>Étapes suivantes

- Si vous effectuez un déploiement complet, passez trop[étape 3 : planifier la capacité](vmware-walkthrough-capacity.md)
- Si vous effectuez un déploiement de test simple, passez trop[étape 4 : planifier la mise en réseau](vmware-walkthrough-network.md).
