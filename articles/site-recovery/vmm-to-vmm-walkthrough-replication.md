---
title: "aaaSet une stratégie de réplication pour le site secondaire tooa réplication Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment tooset une stratégie pour un ordinateur virtuel Hyper-V réplication tooa VMM secondaire du site avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>Étape 8 : Configurer une stratégie de réplication

Après avoir configuré [le mappage réseau](vmm-to-vmm-walkthrough-network-mapping.md), utilisez cette tooset article d’une stratégie de réplication pour Hyper-V virtual machine (VM) réplication tooa site secondaire, à l’aide de [Azure Site Recovery](site-recovery-overview.md).

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Avant de commencer

- Lorsque vous créez une stratégie de réplication, tous les ordinateurs hôtes à l’aide de la stratégie de hello doit hello même système d’exploitation. Hello cloud VMM peut contenir des hôtes Hyper-V qui exécutent différentes versions de Windows Server, mais dans ce cas, vous avez besoin de plusieurs stratégies de réplication.
- Vous pouvez effectuer la réplication initiale hello hors connexion.

## <a name="configure-replication-settings"></a>Configurer les paramètres de réplication

1. toocreate une stratégie de réplication, cliquez sur **Prepare infrastructure** > **les paramètres de réplication** > **+ créer et associer**.

    ![Réseau](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie. Hello type source et cible doit-elle être **Hyper-V**.
3. Dans **version de l’hôte Hyper-V**, sélectionnez le système d’exploitation est en cours d’exécution sur l’ordinateur hôte de hello.
4. Dans **type d’authentification** et **le port d’authentification**, spécifiez comment le trafic est authentifié entre hello principal et les serveurs hôtes Hyper-V de récupération. Sélectionnez **Certificat** , sauf si vous avez un environnement Kerberos opérationnel. Azure Site Recovery configurera automatiquement des certificats pour l'authentification HTTPS. Vous n’avez pas besoin toodo quoi que ce soit manuellement. Par défaut, les ports 8083 et 8084 (pour les certificats) seront ouverts dans hello le pare-feu Windows sur les serveurs hôtes de Hyper-V hello. Si vous sélectionnez **Kerberos**, un ticket Kerberos sera utilisé pour l’authentification mutuelle des serveurs hôtes de hello. Notez que ce paramètre n'est utile que pour les serveurs hôtes Hyper-V s'exécutant sur Windows Server 2012 R2.
5. Dans **fréquence de copie**, spécifiez la fréquence à laquelle vous souhaitez tooreplicate d’éventuelles données delta après la réplication initiale de hello (toutes les 30 secondes, 5 ou 15 minutes).
6. Dans **rétention du point de récupération**, spécifiez, en heures, la durée de conservation hello sera être pour chaque point de récupération. Les ordinateurs protégés peuvent être récupérées point tooany dans une fenêtre.
7. Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures). Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello. Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello. Si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications exécutées sur des machines virtuelles sources. Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.
8. Dans **Compression du transfert de données**, indiquez si les données répliquées transférées doivent être compressées.
9. Sélectionnez **supprimer le réplica VM**, toospecify qui hello d’ordinateur virtuel de réplication doit être supprimé si vous désactivez la protection de machine virtuelle de la source hello. Si vous activez ce paramètre, quand vous désactivez la protection pour la source de hello VM, il est supprimé de la console de récupération de Site hello, paramètres de Site Recovery pour hello VMM sont supprimés à partir de la console VMM hello et hello réplica est supprimé.
10. Dans **Initial de la méthode de réplication**, si vous effectuez une réplication sur le réseau de hello, spécifiez si toostart hello la réplication initiale ou la planifier. la bande passante du réseau toosave, vous souhaiterez peut-être tooschedule il en dehors des heures occupés. Cliquez ensuite sur **OK**.

     ![Stratégie de réplication](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. Lorsque vous créez une nouvelle stratégie, il est automatiquement associé hello cloud VMM. Dans **Stratégie de réplication**, cliquez sur **OK**. Vous pouvez associer Clouds VMM supplémentaires (et hello machines virtuelles dans les) cette stratégie de réplication dans **réplication** > nom de la stratégie > **associer le Cloud VMM**.

     ![Stratégie de réplication](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a>Préparer la réplication initiale hors connexion

Vous pouvez effectuer une réplication hors connexion pour la copie des données initiales hello. Vous pouvez la préparer comme suit :

* Sur le serveur de source de hello, vous spécifiez un emplacement de chemin d’accès à partir de quels hello exportation de données aura lieu. Affecter un contrôle total pour les autorisations de partage et NTFS, toohello le service VMM sur le chemin d’exportation de hello. Sur le serveur cible de hello, vous spécifiez un emplacement de chemin d’accès à partir de laquelle importent les données de salutation se produira. Affecter des mêmes autorisations sur ce chemin d’accès d’importation hello.
* Si hello importer ou chemin d’exportation est partagé, attribuer l’appartenance au groupe administrateur, utilisateur avec pouvoir, opérateurs d’impression ou opérateur de serveur pour le compte de service VMM hello sur l’ordinateur distant de hello sur quel hello partagé se trouve.
* Si vous utilisez des hôtes exécuter en tant que comptes tooadd, sur hello importer et exporter les chemins d’accès, affecter en lecture et écriture toohello comptes d’identification dans VMM.
* Hello importer et exporter les partages ne doivent pas être situés sur tout ordinateur utilisé comme un serveur hôte Hyper-V, car la configuration de boucle n’est pas pris en charge par Hyper-V.
* Dans Active Directory, sur chaque serveur hôte Hyper-V qui contient les ordinateurs virtuels que vous souhaitez tooprotect, activez et configurez des ordinateurs distants la délégation contrainte tootrust hello exportation et importation de hello chemins d’accès sont situés, comme suit :
  1. Sur le contrôleur de domaine hello, ouvrez **Active Directory Users and Computers**.
  2. Dans l’arborescence de la console hello, cliquez sur **DomainName** > **ordinateurs**.
  3. Nom de serveur hôte hello Hyper-V avec le bouton droit > **propriétés**.
  4. Sur hello **délégation** , cliquez sur **n’approuver cet ordinateur pour les services uniquement de délégation toospecified**.
  5. Cliquez sur **Utiliser tout protocole d’authentification**.
  6. Cliquez sur **Ajouter** > **Utilisateurs et ordinateurs**.
  7. Nom du type hello d’ordinateur hello qui héberge le chemin d’exportation de hello > **OK**. À partir de la liste hello des services disponibles, maintenez la touche CTRL de hello et cliquez sur **cifs** > **OK**. Répétez pour nom hello d’ordinateur de hello ce chemin d’importation de hello hôtes. Répétez cette procédure pour les serveurs hôtes Hyper-V supplémentaires.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 9 : activer la réplication](vmm-to-vmm-walkthrough-enable-replication.md).
