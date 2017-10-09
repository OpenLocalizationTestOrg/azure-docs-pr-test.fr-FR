---
title: site secondaire du tooa aaaReplicate ordinateurs virtuels Hyper-V avec Azure Site Recovery | Documents Microsoft
description: "Décrit comment tooreplicate ordinateurs virtuels Hyper-V dans VMM clouds tooa secondaire VMM site à l’aide de hello portail Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>Réplication d’ordinateurs virtuels Hyper-V dans VMM clouds tooa secondaire de site VMM à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-vmm-to-vmm.md)
> * [Portail classique](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Cet article décrit comment tooreplicate locaux virtuels Hyper-V gérés dans des clouds System Center Virtual Machine Manager (VMM), à l’aide du site secondaire tooa [Azure Site Recovery](site-recovery-overview.md) Bonjour portail Azure. En savoir plus sur cette [architecture du scénario](site-recovery-components.md).

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Composants requis

**Configuration requise** | **Détails**
--- | ---
**Microsoft Azure** | Vous avez besoin d’un compte [Microsoft Azure](http://azure.microsoft.com/) . Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/). [En savoir plus](https://azure.microsoft.com/pricing/details/site-recovery/) sur la tarification Site Recovery.
**Instances VMM locales** | Nous vous recommandons de qu'avoir deux serveurs VMM, un site principal de hello et un Bonjour secondaire.<br/><br/> Vous pouvez effectuer la réplication entre des clouds sur un seul serveur VMM.<br/><br/> Serveurs VMM doivent exécuter au moins System Center 2012 SP1 avec les dernières mises à jour de hello.<br/><br/> Les serveurs VMM doivent avoir accès à Internet.
**Clouds VMM** | Chaque serveur VMM doit avoir à un ou plusieurs clouds et tous les clouds doivent avoir le profil de capacité de Hyper-V hello. <br/><br/>Les clouds doivent contenir un ou plusieurs groupes hôtes VMM.<br/><br/> Si vous avez uniquement un seul serveur VMM, il doit au moins deux clouds, tooact comme principale et secondaire.
**Hyper-V** | Serveurs Hyper-V doivent être en cours d’exécution au moins Windows Server 2012 avec le rôle de hello Hyper-V, et avoir hello les dernières mises à jour installées.<br/><br/> Un serveur Hyper-V doit contenir au moins une machine virtuelle.<br/><br/>  Les serveurs hôte Hyper-V doivent se trouver dans des groupes hôtes dans des clouds VMM principaux et secondaires hello.<br/><br/> Si vous exécutez Hyper-V dans un cluster sur Windows Server 2012 R2, installez la [mise à jour 2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Si vous exécutez Hyper-V dans un cluster sous Windows Server 2012, notez que le répartiteur de clusters n’est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques. Configurer le service broker de cluster hello manuellement. [En savoir plus](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Les serveurs Hyper-V doivent disposer d’un accès Internet.
**URLs** | Serveurs VMM et des ordinateurs hôtes Hyper-V doivent être en mesure de tooreach ces URL :<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>Étapes du déploiement

Voici la procédure à suivre :

1. Assurez-vous que la configuration requise est respectée.
2. Préparer le serveur VMM de hello et hôtes Hyper-V.
3. Créez un coffre Recovery Services. coffre de Hello contient les paramètres de configuration et orchestre la réplication.
4. Spécifiez les paramètres de la source, de la cible et de réplication.
5. Déploiement de service de mobilité hello sur des machines virtuelles que vous souhaitiez tooreplicate.
6. Préparez la réplication, et activez la réplication pour les machines virtuelles Hyper-V.
7. Exécutez un toomake de basculement de test que tout fonctionne comme prévu.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>Préparer les serveurs VMM et les hôtes Hyper-V

tooprepare pour le déploiement :

1. Assurez-vous que le serveur VMM de hello et hôtes Hyper-V sont conformes aux conditions préalables de hello décrites ci-dessus et peuvent atteindre l’URL de hello requis.
2. Configurez les réseaux VMM de manière à pouvoir définir le [mappage réseau](#network-mapping-overview).

    - Assurez-vous que les ordinateurs virtuels sur la source de hello serveur hôte Hyper-V sont connecté tooa réseau de VMM VM. Ce réseau doit être lié tooa réseau logique associé au cloud de hello.
    Vérifiez qu’un réseau de machines virtuelles correspondant configuré cloud hello secondaire que vous utilisez pour la récupération. Ce réseau d’ordinateurs virtuels doit être lié tooa réseau logique associé avec le cloud secondaire de hello.

3. Préparer un [déploiement de serveur unique](#single-vmm-server-deployment), si vous voulez que les machines virtuelles de tooreplicate entre des clouds sur hello même serveur VMM.

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau** > **Gestion** > **Recovery Services**.
3. Dans **nom**, spécifiez un coffre de hello tooidentify nom convivial. Si vous avez plusieurs abonnements, sélectionnez-en un.
4. [Créez un groupe de ressources](../azure-resource-manager/resource-group-template-deploy-portal.md)ou sélectionnez-en un. Spécifiez une région Azure. Les machines sont répliquées toothis région. les régions toocheck pris en charge consultez disponibilité géographique dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Si vous souhaitez tooquickly accès hello coffre à partir de hello du tableau de bord, cliquez sur **code confidentiel toodashboard** > **créer un archivage**.

    ![Nouveau coffre](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

coffre Hello apparaît sur hello **tableau de bord**, dans **toutes les ressources**et sur hello principal **les coffres de Services de récupération** panneau.


## <a name="choose-a-protection-goal"></a>Choisir un objectif en matière de protection

Sélectionnez ce que vous souhaitez tooreplicate, et où tooreplicate à.

2. Cliquez sur **Site Recovery** > **Étape 1 : Préparez l’infrastructure** > **Objectif de protection**.
3. Sélectionnez **toorecovery site**, puis sélectionnez **Oui, avec Hyper-V**.
4. Sélectionnez **Oui** tooindicate que vous utilisez des hôtes VMM toomanage hello Hyper-V.
5. Sélectionnez **Oui** si vous avez un serveur VMM secondaire. Si vous déployez la réplication entre des clouds sur un seul serveur VMM, cliquez sur **Non**. Cliquez ensuite sur **OK**.

    ![Sélectionner des objectifs](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Installer hello fournisseur Azure Site Recovery sur les serveurs VMM et découvrir et inscrire les serveurs dans le coffre hello.

1. Cliquez sur **Étape 1 : Préparer l’infrastructure** > **Source**.

    ![Configurer la source](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. Dans **Prepare source**, cliquez sur **+ VMM** tooadd un serveur VMM.

    ![Configurer la source](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. Dans **ajouter un serveur**, vérifiez que **serveur System Center VMM** s’affiche dans **type de serveur** et le serveur VMM hello satisfont à hello [conditions préalables](#prerequisites).
4. Téléchargez le fichier d’installation hello fournisseur Azure Site Recovery.
5. Téléchargez la clé d’inscription de hello. Vous en aurez besoin lorsque vous exécuterez le programme d’installation. clé de Hello est valide pendant cinq jours après que l’avoir généré.

    ![Configurer la source](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Installez hello fournisseur Azure Site Recovery sur le serveur VMM de hello. Vous n’avez pas besoin tooexplicitly installer quoi que ce soit sur des serveurs hôtes Hyper-V.


### <a name="install-hello-azure-site-recovery-provider"></a>Installer hello fournisseur Azure Site Recovery

1. Exécutez le fichier de configuration de fournisseur hello sur chaque serveur VMM. Si VMM est déployé dans un cluster, procédez comme suit de hello hello première fois que vous installez :
    -  Installer le fournisseur de hello sur un nœud actif et de fin hello installation tooregister hello serveur VMM dans le coffre hello.
    - Ensuite, installez hello fournisseur sur hello autres nœuds. Nœuds de cluster doivent tous exécuter hello même version de hello fournisseur.
2. Le programme d’installation exécute quelques vérifications et demandes de service d’autorisation toostop hello VMM. Hello service VMM va redémarrer automatiquement lorsque le programme d’installation se termine. Si vous installez sur un cluster VMM, vous êtes le rôle de Cluster hello toostop demandées.
3. Dans **Microsoft Update**, vous pouvez la choisir toospecify que les mises à jour du fournisseur sont installées conformément à votre stratégie Microsoft Update.
4. Dans **Installation**, acceptez ou modifiez l’emplacement d’installation par défaut hello et cliquez sur **installer**.

    ![Emplacement d’installation](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. Une fois l’installation terminée, cliquez sur **inscrire** serveur hello de tooregister dans le coffre hello.

    ![Emplacement d’installation](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. Dans **nom du coffre**, vérifier nom hello de coffre hello dans le hello serveur sera inscrit. Cliquez sur *Suivant*.

    ![Enregistrement du serveur](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. Dans **connexion Internet**, spécifiez comment hello fournisseur en cours d’exécution sur le serveur VMM de hello connecte tooAzure.

    ![Paramètres Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - Vous pouvez spécifier que le fournisseur hello doit se connecter directement toohello internet, ou via un proxy.
   - Spécifiez les paramètres de proxy, si nécessaire.
   - Si vous utilisez un proxy, un compte RunAs VMM (DRAProxyAccount) est créé automatiquement à l’aide de hello spécifié les informations d’identification de proxy. Configurer le serveur de proxy hello afin que ce compte peut s’authentifier avec succès. Hello les paramètres de compte d’identification peuvent être modifiés dans la console VMM hello > **paramètres** > **sécurité** > **exécuter en tant que comptes**. Redémarrez les modifications de tooupdate service hello VMM.
8. Dans **clé d’inscription**, sélectionnez clé hello téléchargés à partir d’Azure Site Recovery et copiée serveur VMM de toohello.
9. paramètre de chiffrement Hello est uniquement utilisé lorsque vous répliquez des ordinateurs virtuels Hyper-V dans VMM clouds tooAzure. Si vous effectuez une réplication site secondaire de tooa n’est pas utilisé.
10. Dans **nom du serveur**, spécifiez un serveur VMM à hello tooidentify nom convivial dans le coffre hello. Dans une configuration de cluster spécifier le nom de rôle de cluster VMM hello.
11. Dans **synchroniser les métadonnées du cloud**, sélectionnez si vous souhaitez toosynchronize métadonnées pour tous les clouds sur le serveur VMM de hello avec le coffre de hello. Cette action ne doit toohappen qu’une seule fois sur chaque serveur. Si vous ne souhaitez pas toosynchronize tous les clouds, vous pouvez laisser ce paramètre désactivé et synchroniser chaque cloud individuellement dans les propriétés du cloud hello dans la console VMM hello.
12. Cliquez sur **suivant** processus de hello toocomplete. Après l’inscription, les métadonnées d’un serveur hello VMM sont récupérées par Azure Site Recovery. serveur de Hello est affiché sur hello **serveurs VMM** onglet hello **serveurs** page dans le coffre hello.

    ![Serveur](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Une fois le serveur de hello est disponible dans la console de récupération de Site hello dans **Source** > **Prepare source** sélectionnez hello VMM server et nuage hello sélectionnez quels Bonjour Hyper-V se trouve. Cliquez ensuite sur **OK**.

Vous pouvez également installer le fournisseur de hello à partir de la ligne de commande hello :

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello

Sélectionner le cloud et le serveur VMM de hello cible.

1. Cliquez sur **Prepare infrastructure** > **cible**et sélectionnez hello cible VMM serveur toouse.
2. Les clouds sur le serveur hello qui sont synchronisés avec la récupération de Site seront affiche. Sélectionnez le cloud cible de hello.

   ![Cible](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>Configurer les paramètres de réplication

- Lorsque vous créez une stratégie de réplication, tous les hôtes à l’aide de la stratégie de hello doit hello même système d’exploitation. Hello cloud VMM peut contenir des hôtes Hyper-V qui exécutent différentes versions de Windows Server, mais dans ce cas, vous avez besoin de plusieurs stratégies de réplication.
- Vous pouvez effectuer la réplication initiale hello hors connexion. [En savoir plus](#prepare-for-initial-offline-replication)

1. Cliquez sur le toocreate une stratégie de réplication **Prepare infrastructure** > **les paramètres de réplication** > **+ créer et associer**.

    ![Réseau](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie. Hello type source et cible doit-elle être **Hyper-V**.
3. Dans **version de l’hôte Hyper-V**, sélectionnez le système d’exploitation est en cours d’exécution sur l’ordinateur hôte de hello.
4. Dans **type d’authentification** et **le port d’authentification**, spécifiez comment le trafic est authentifié entre hello principal et les serveurs hôtes Hyper-V de récupération. Sélectionnez **Certificat** , sauf si vous avez un environnement Kerberos opérationnel. Azure Site Recovery configurera automatiquement des certificats pour l'authentification HTTPS. Vous n’avez pas besoin toodo quoi que ce soit manuellement. Par défaut, les ports 8083 et 8084 (pour les certificats) seront ouverts dans hello le pare-feu Windows sur les serveurs hôtes de Hyper-V hello. Si vous sélectionnez **Kerberos**, un ticket Kerberos sera utilisé pour l’authentification mutuelle des serveurs hôtes de hello. Notez que ce paramètre n'est utile que pour les serveurs hôtes Hyper-V s'exécutant sur Windows Server 2012 R2.
5. Dans **fréquence de copie**, spécifiez la fréquence à laquelle vous souhaitez tooreplicate d’éventuelles données delta après la réplication initiale de hello (toutes les 30 secondes, 5 ou 15 minutes).
6. Dans **rétention du point de récupération**, spécifiez, en heures, la durée de conservation hello sera être pour chaque point de récupération. Les ordinateurs protégés peuvent être récupérées point tooany dans une fenêtre.
7. Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures). Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello. Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello. Si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications exécutées sur des machines virtuelles sources. Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.
8. Dans **Compression du transfert de données**, indiquez si les données répliquées transférées doivent être compressées.
9. Sélectionnez **supprimer le réplica VM**, toospecify qui hello d’ordinateur virtuel de réplication doit être supprimé si vous désactivez la protection de machine virtuelle de la source hello. Si vous activez ce paramètre, quand vous désactivez la protection pour la source de hello VM, il est supprimé de la console de récupération de Site hello, paramètres de Site Recovery pour hello VMM sont supprimés à partir de la console VMM hello et hello réplica est supprimé.
10. Dans **Initial de la méthode de réplication**, si vous effectuez une réplication sur le réseau de hello, spécifiez si toostart hello la réplication initiale ou la planifier. la bande passante du réseau toosave, vous souhaiterez peut-être tooschedule il en dehors des heures occupés. Cliquez ensuite sur **OK**.

     ![Stratégie de réplication](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. Lorsque vous créez une nouvelle stratégie, il est automatiquement associé hello cloud VMM. Dans **Stratégie de réplication**, cliquez sur **OK**. Vous pouvez associer Clouds VMM supplémentaires (et hello machines virtuelles dans les) cette stratégie de réplication dans **réplication** > nom de la stratégie > **associer le Cloud VMM**.

     ![Stratégie de réplication](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>configurer le mappage réseau

- En savoir plus sur le [mappage réseau](#prepare-for-network-mapping) avant de démarrer.
- Vérifiez que les ordinateurs virtuels sur les serveurs VMM sont connectés tooa réseau d’ordinateurs virtuels.


1. Dans **Infrastructure Site Recovery** > **Mappage réseau** > **Mappages réseau**, cliquez sur **+Mappage réseau**.

    ![Mappage réseau](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. Dans **ajouter le mappage réseau** , sélectionnez la source de hello et serveurs VMM cible. réseaux d’ordinateurs virtuels Hello associés aux serveurs VMM de hello sont récupérés.
3. Dans **réseau Source**, sélectionnez réseau hello toouse à partir de la liste de hello des réseaux d’ordinateurs virtuels associé avec le serveur VMM principal de hello.
4. Dans **réseau cible**, sélectionnez réseau hello toouse sur le serveur VMM secondaire de hello. Cliquez ensuite sur **OK**.

    ![Mappage réseau](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

Voici le processus exécuté lorsque le mappage réseau démarre :

* Les ordinateurs virtuels réplica existants qui correspondent le réseau d’ordinateurs virtuels toohello source sera réseau d’ordinateurs virtuels connectés toohello cible.
* Nouveaux ordinateurs virtuels qui sont le réseau d’ordinateurs virtuels connectés toohello source sera connecté toohello réseau cible après la réplication.
* Si vous modifiez un mappage existant avec un nouveau réseau, les machines virtuelles de réplication sera connectées à l’aide de nouveaux paramètres de hello.
* Si le réseau cible de hello possède plusieurs sous-réseaux et d’un de ces sous-réseaux a hello trouve du même nom que le sous-réseau sur lequel hello source virtual machine, puis hello ordinateur virtuel sera connecté toothat cible sous-réseau après le basculement. S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.

### <a name="configure-storage-mapping"></a>Configurez le mappage de stockage.

[Mappage de stockage](#prepare-for-storage-mapping) n’est pas pris en charge dans le nouveau portail de Azure hello. Toutefois, il peut être activé à l’aide de Powershell. [En savoir plus](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping).

## <a name="step-5-capacity-planning"></a>Étape 5 : planifier la capacité

Votre infrastructure de base est désormais configurée. Vous pouvez donc réfléchir à la planification de la capacité et déterminer si des ressources supplémentaires sont nécessaires.

- Téléchargez et exécutez hello [Azure Site Recovery Capacity planner](site-recovery-capacity-planner.md), toogather les informations relatives à votre environnement de réplication, y compris les ordinateurs virtuels, des disques par machine virtuelle et de stockage par disque.
- Une fois que vous avez collecté les informations de réplication en temps réel, vous pouvez modifier la bande passante de réplication hello NetQos stratégie toocontrol pour les machines virtuelles. Pour en savoir plus sur la [limitation du trafic des réplicas Hyper-V](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/), consultez le blog de Thomas Maurer. Obtenir plus d’informations sur hello [applet de commande New-NetQosPolicy](https://technet.microsoft.com/library/hh967468.aspx.).

## <a name="enable-replication"></a>Activer la réplication

1. Cliquez sur **Étape 2 : Répliquer l’application** > **Source**. Une fois que vous avez activé la réplication pour hello première fois, vous cliquez sur **+ répliquer** dans la réplication de tooenable hello coffre pour des ordinateurs supplémentaires.

    ![Activer la réplication](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. Dans **Source**, sélectionnez le serveur VMM de hello et hello cloud dans quel hello hôtes Hyper-V que vous souhaitez tooreplicate sont situés. Cliquez ensuite sur **OK**.

    ![Activer la réplication](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. Dans **cible**, vérifiez que le serveur VMM secondaire de hello et cloud.
4. Dans **virtuels**, sélectionnez hello machines virtuelles tooprotect à partir de la liste de hello.

    ![Activer la protection pour les machines virtuelles](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

Vous pouvez suivre la progression de hello **activer la Protection** action dans **travaux** > **les tâches de récupération de Site**. Après avoir hello **finaliser la Protection** tâche se termine, la machine virtuelle de hello est prêt pour le basculement.

Notez les points suivants :

- Vous pouvez également activer la protection des machines virtuelles dans la console VMM hello. Cliquez sur **activer la Protection** de barre d’outils hello dans les propriétés d’une machine virtuelle hello > **Azure Site Recovery** onglet.
- Une fois que vous avez activé la réplication, vous pouvez afficher les propriétés d’hello VM dans **répliquées des éléments**. Sur hello **Essentials** tableau de bord, vous pouvez voir des informations sur la stratégie de réplication hello pour hello machine virtuelle et son état. Cliquez sur **Propriétés** pour obtenir plus de détails.

### <a name="onboard-existing-virtual-machines"></a>Intégrer des machines virtuelles existantes
Si vous avez des machines virtuelles existantes dans VMM qui sont répliquées à l’aide du réplica Hyper-V, vous pouvez les intégrer à la réplication Azure Site Recovery comme suit :

1. Assurez-vous que ce serveur hello Hyper-V héberge hello que machine virtuelle existante se trouve dans un cloud principal hello, et ce serveur d’Hyper-V hello hébergement hello ordinateur virtuel se trouve dans le cloud secondaire de hello.
2. Assurez-vous que la stratégie de réplication est configurée pour un cloud VMM principal hello.
3. Activer la réplication pour l’ordinateur virtuel principal hello. Azure Site Recovery et VMM s’assurer que hello même hôte de réplica et de la machine virtuelle est détectée et Azure Site Recovery réutilise et spécifié les paramètres de réplication de rétablir la connexion à l’aide de hello.

## <a name="test-your-deployment"></a>Tester votre déploiement

tootest votre déploiement, vous pouvez exécuter un [test de basculement](site-recovery-test-failover-vmm-to-vmm.md) pour une seule machine virtuelle, ou [créer un plan de récupération](site-recovery-create-recovery-plans.md) qui contient un ou plusieurs ordinateurs virtuels.



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



## <a name="prepare-for-network-mapping"></a>Préparer le mappage réseau
Mappages de mappage réseau entre réseaux VM de VMM sur les serveurs VMM des principaux et secondaires hello pour :

* Optimiser le positionnement des machines virtuelles de réplication sur les hôtes Hyper-V secondaires après le basculement.
* Connecter des réseaux d’ordinateurs virtuels tooappropriate réplica machines virtuelles après le basculement.

Notez les points suivants :
- Le mappage réseau peut être configuré entre les réseaux VM sur deux serveurs VMM ou sur un seul serveur VMM si deux sites sont gérés par hello même serveur.
- Lorsque le mappage est correctement configuré la réplication est activée, une machine virtuelle à l’emplacement principal de hello sera connecté tooa réseau et son réplica dans l’emplacement cible de hello sera connecté tooits mappé réseau.
- Si les réseaux ont été configurées correctement dans VMM, lorsque vous sélectionnez un réseau de machines virtuelles cible lors du mappage réseau, les clouds sources hello VMM qui utilisent le réseau d’ordinateurs virtuels hello source seront affichera, ainsi que les réseaux d’ordinateurs virtuels hello cibles disponibles sur les clouds cibles hello qui sont utilisés pour protection.
- Si le réseau cible de hello a plusieurs sous-réseaux et de ces sous-réseaux a hello même nom comme hello sous-réseau sur quel hello ordinateur virtuel source se trouve, puis hello machine virtuelle de réplication sera connectée toothat cible sous-réseau après le basculement. S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.


Voici un exemple tooillustrate ce mécanisme. Prenons l’exemple d’une entreprise ayant ouvert deux bureaux, l’un à New York et l’autre à Chicago.

| **Emplacement** | **Serveur VMM** | **Réseaux de machines virtuelles** | **Mappés à** |
| --- | --- | --- | --- |
| New York |VMM-NewYork |VMNetwork1-NewYork |Mappé tooVMNetwork1-Chicago |
| VMNetwork2-NewYork |Non mappé | | |
| Chicago |VMM-Chicago |VMNetwork1-Chicago |TooVMNetwork1-NewYork mappé |
| VMNetwork2-Chicago |Non mappé | | |

Dans cet exemple :

* Lorsqu’un ordinateur virtuel est créé pour un ordinateur virtuel qui est connecté tooVMNetwork1-NewYork, il sera connecté tooVMNetwork1-Chicago.
* Lorsqu’un ordinateur virtuel est créé pour VMNetwork2-NewYork ou VMNetwork2-Chicago, il ne sera pas connectée tooany réseau.

Voici la façon dont les clouds VMM sont configurés dans notre exemple d’organisation et les réseaux logiques hello associées aux clouds de hello.

### <a name="cloud-protection-settings"></a>Paramètres de protection des clouds
| **Cloud protégé** | **Cloud de protection** | **Réseau logique (New York)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>N/D</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |
| SilverCloud2 |<p>N/D</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>Paramètres des réseaux de machines virtuelles et des réseaux logiques
| **Emplacement** | **Réseau logique** | **Réseau de machines virtuelles associé** |
| --- | --- | --- |
| New York |LogicalNetwork1-NewYork |VMNetwork1-NewYork |
| Chicago |LogicalNetwork1-Chicago |VMNetwork1-Chicago |
| LogicalNetwork2Chicago |VMNetwork2-Chicago | |

### <a name="target-networks"></a>Réseaux cibles
Selon ces paramètres, lorsque vous sélectionnez le réseau d’ordinateurs virtuels hello cible, hello tableau suivant affiche les options de hello qui seront disponibles.

| **Sélection** | **Cloud protégé** | **Cloud de protection** | **Réseau cible disponible** |
| --- | --- | --- | --- |
| VMNetwork1-Chicago |SilverCloud1 |SilverCloud2 |Disponible |
| GoldCloud1 |GoldCloud2 |Disponible | |
| VMNetwork2-Chicago |SilverCloud1 |SilverCloud2 |Non disponible |
| GoldCloud1 |GoldCloud2 |Disponible | |


### <a name="failback"></a>Restauration automatique
toosee que se passe-t-il en cas de hello de la restauration automatique (réplication inverse), supposons que VMNetwork1-NewYork est mappé tooVMNetwork1-Chicago, avec hello suivant les paramètres.

| **Machine virtuelle** | **Réseau de tooVM connecté** |
| --- | --- |
| MV1 |VMNetwork1-Network |
| VM2 (réplica de VM1) |VMNetwork1-Chicago |

Examinons ce qui se passe dans différents scénarios possibles avec ces paramètres.

| **Scénario** | **Résultat** |
| --- | --- |
| Aucune modification dans les propriétés du réseau hello de VM-2 après le basculement. |VM-1 reste connecté toohello source réseau. |
| Les propriétés du réseau de la machine VM2 sont modifiées après le basculement ; la machine est déconnectée. |La machine VM1 est déconnectée. |
| Propriétés réseau de VM-2 sont modifiées après basculement et sont connecté tooVMNetwork2-Chicago. |Si le réseau VMNetwork2-Chicago n’est pas mappé, la machine VM1 est déconnectée. |
| Le mappage réseau de VMNetwork1-Chicago est modifié. |VM-1 sera connecté toohello réseau mappé tooVMNetwork1-Chicago. |


## <a name="prepare-for-single-server-deployment"></a>Préparation du déploiement d’un serveur unique


Si vous avez uniquement un seul serveur VMM, vous pouvez répliquer machines virtuelles dans les hôtes Hyper-V dans hello cloud VMM trop[Azure](site-recovery-vmm-to-azure.md) ou tooa secondaire VMM cloud. Option de première hello est recommandée, car la réplication entre des clouds n’est pas transparente. Si vous ne souhaitez pas tooreplicate entre des clouds, vous pouvez répliquer le serveur VMM autonome unique ou avec un seul serveur VMM déployé dans un cluster Windows étendu

### <a name="standalone-vmm-server"></a>Serveur VMM autonome

Dans ce scénario, vous déployez un seul serveur VMM de hello comme une machine virtuelle dans le site principal de hello et répliquez ce site secondaire de tooa de machine virtuelle à l’aide de la récupération de Site et le réplica Hyper-V.

1. **Configurez VMM sur une machine virtuelle Hyper-V**. Nous vous suggérons de que vous colocalisation d’instance de SQL Server hello utilisé par VMM sur hello même machine virtuelle. Ce gain de temps qu’une seule machine virtuelle a toobe créé. Si vous voulez toouse instance distante de SQL Server et si une panne se produit, vous devez toorecover cette instance avant de pouvoir récupérer VMM.
2. **Vérifiez le serveur VMM de hello a au moins deux clouds configurés**. Un cloud contiendra hello machines virtuelles vous le souhaitez tooreplicate et hello autres cloud servira d’emplacement secondaire de hello. Hello cloud qui contient hello machines virtuelles doivent satisfaire tooprotect [conditions préalables](#prerequisites).
3. Configurez Site Recovery comme le décrit cet article. Créer et inscrire le serveur VMM de hello dans un coffre, définir une stratégie de réplication et activer la réplication. noms VMM source et cible Hello sera hello à la même. Spécifiez que la réplication initiale a lieu sur le réseau de hello.
4. Lorsque vous configurez le mappage réseau vous mappez le réseau d’ordinateurs virtuels hello hello cloud principal toohello réseau de machines virtuelles pour le cloud secondaire de hello.
5. Dans la console Gestionnaire Hyper-V hello, activer la réplication Hyper-V sur l’ordinateur hôte Hyper-V hello contenant hello VMM VM et activer la réplication sur hello machine virtuelle. Assurez-vous que vous n’ajoutez pas tooclouds d’ordinateur virtuel VMM hello qui sont protégées par la récupération de Site, tooensure que les paramètres de réplication Hyper-V ne sont pas remplacés par la récupération de Site.
6. Si vous créez des plans de récupération pour le basculement, que vous utilisez hello même serveur VMM pour la source et cible.
7. Lors d’une panne complète, vous effectuez le basculement et la récupération comme suit :

   1. Dans la console du Gestionnaire Hyper-V hello dans un site secondaire hello, toofail sur le site secondaire hello principal VMM VM toohello, exécutez un basculement non planifié.
   2. Vérifiez que hello que VMM VM est activé et en cours d’exécution et dans le coffre de hello, exécuter un toofail basculement non planifié sur des machines virtuelles de hello de clouds spécifiques toosecondary principal. Valider le basculement de hello, puis sélectionnez un autre point de récupération si nécessaire.
   3. Une fois hello basculement non planifié est terminé, toutes les ressources accessibles à partir du site principal de hello à nouveau.
   4. Lorsque le site principal de hello est disponible, dans la console du Gestionnaire Hyper-V hello dans le site secondaire de hello, activez la réplication inverse pour hello VMM VM. Démarre la réplication pour hello machine virtuelle à partir de tooprimary secondaire.
   5. Dans la console du Gestionnaire Hyper-V hello dans un site secondaire hello, toofail sur le site principal de VMM VM toohello de hello, exécutez un basculement planifié. Valider le basculement de hello. Activez la réplication inverse, pour hello VMM VM est à nouveau réplication à partir de toosecondary principal.
   6. Dans le coffre Recovery Services hello, activez la réplication inverse pour les machines virtuelles, toostart répliquant tooprimary secondaire à partir de la charge de travail hello.
   7. Dans le coffre Recovery Services hello, exécuter un basculement planifié toofail hello précédent la charge de travail ordinateurs virtuels toohello site principal. Valider hello basculement toocomplete il. Ensuite, activez la réplication inverse toostart réplication hello charges de travail ordinateurs virtuels de toosecondary principal.

### <a name="stretched-vmm-cluster"></a>Cluster VMM étiré

Au lieu de déployer un serveur VMM autonome en tant qu’une machine virtuelle qui réplique le site secondaire de tooa, vous pouvez rendre VMM hautement disponible en la déployant comme une machine virtuelle dans un cluster de basculement Windows. pour fournir une résilience de la charge de travail et une protection contre les défaillances matérielles. toodeploy avec hello de récupération de Site VMM VM doit être déployé dans un cluster de stretch sur des sites géographiquement distincts. toodo cela :

1. Installez VMM sur un ordinateur virtuel dans un cluster de basculement Windows et sélectionnez hello option toorun hello serveur comme étant hautement disponible pendant l’installation.
2. instance de SQL Server Hello qui est utilisé par VMM doit être répliquée avec SQL Server AlwaysOn, afin qu’il existe un réplica de base de données hello dans le site secondaire de hello.
3. Suivez les instructions de hello dans cette toocreate article un coffre, inscrire hello serveur et configurer la protection. Vous devez tooregister chaque serveur VMM Bonjour cluster Bonjour de coffre Recovery Services. toodo, vous installez hello fournisseur sur un nœud actif et inscrire le serveur VMM de hello. Puis, vous installez hello fournisseur sur d’autres nœuds.
4. En cas de panne, hello VMM serveur et sa base de données SQL Server correspondante sont basculés et accessibles à partir du site secondaire de hello.



## <a name="prepare-for-storage-mapping"></a>Préparer le mappage de stockage


Vous configurez le stockage en mappant les classifications de stockage sur une source et la cible suivantes de VMM serveurs toodo hello :

  * **Identifier le stockage cible pour les machines virtuelles de réplication**: un disque dur de machine virtuelle source seront répliqués toohello stockage que vous avez spécifiée (partage SMB ou cluster shared volumes (CSV)) dans l’emplacement cible de hello.
  * **Placement des machines virtuelles de réplica**: le mappage de stockage est utilisé toooptimally machines virtuelles de réplication sur place sur les serveurs hôtes Hyper-V. Machines virtuelles de réplication seront placées sur des hôtes qui peuvent accéder à classification de stockage hello mappé.
  * **Aucun mappage de stockage**: Si vous ne configurez pas le mappage de stockage, les machines virtuelles seront répliquées toohello emplacement de stockage par défaut spécifié sur le serveur hôte de hello Hyper-V associé avec l’ordinateur virtuel de réplication hello.

Notez les points suivants :
- Vous pouvez configurer le mappage entre 2 clouds VMM sur un serveur unique.
- Classifications de stockage doivent être disponible toohello les groupes hôtes situés dans des clouds source et cible.
- Les classifications n’avez pas besoin toohave hello même type de stockage. Par exemple, vous pouvez mapper une classification source contenant la classification SMB partages tooa cible qui contient des volumes partagés de cluster.

### <a name="example"></a>Exemple
Si les classifications sont correctement configurées dans VMM lorsque vous sélectionnez la source de hello et cible le serveur VMM lors du mappage de stockage, les classifications source et cible hello seront affichera. Voici un exemple de partages de fichiers de stockage et de classifications pour une entreprise ayant deux sites à New York et Chicago.

| **Emplacement** | **Serveur VMM** | **Partage de fichiers (source)** | **Classification (source)** | **Mappé à** | **Partage de fichiers (cible)** |
| --- | --- | --- | --- | --- | --- |
| New York |VMM_Source |SourceShare1 |GOLD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |SILVER |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONZE |BRONZE_TARGET |TargetShare3 | | |
| Chicago |VMM_Target | |GOLD_TARGET |Non mappé | |
|  |SILVER_TARGET |Non mappé | | | |
|  |BRONZE_TARGET |Non mappé | | | |

Dans cet exemple :

* Lorsqu’un ordinateur virtuel est créé pour un ordinateur virtuel sur le stockage GOLD (SourceShare1), il sera répliqué tooa GOLD_TARGET stockage (TargetShare1).
* Lorsqu’un ordinateur virtuel est créé pour un ordinateur virtuel sur le stockage SILVER (SourceShare2), il soit au stockage répliqué tooa SILVER_TARGET (TargetShare2) et ainsi de suite.

### <a name="multiple-storage-locations"></a>Emplacements de stockage multiples
Si classification cible de hello est attribuée à des partages SMB toomultiple ou des volumes partagés de cluster, emplacement de stockage optimal hello est sélectionnée automatiquement lorsque l’ordinateur virtuel de hello est protégé. Si aucun stockage cible appropriée n’est disponible avec hello spécifié la classification, par défaut de hello emplacement de stockage spécifié sur l’ordinateur hôte de hello Hyper-V est utilisé tooplace hello réplica des disques durs virtuels.

Hello tableau suivant affiche la classification de stockage et les volumes partagés de cluster sont configurés dans notre exemple.

| **Emplacement** | **Classification** | **Stockage associé** |
| --- | --- | --- |
| New York |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| Chicago |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

Ce tableau récapitule le comportement de hello lorsque vous activez la protection des machines virtuelles (VM1 - VM5) dans cet exemple d’environnement.

| **Machine virtuelle** | **Stockage source** | **Classification source** | **Stockage cible mappé** |
| --- | --- | --- | --- |
| MV1 |C:\ClusterStorage\SourceVolume1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>GOLD_TARGET pour les deux</p> |
| MV2 |\\FileServer\SourceShare1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>GOLD_TARGET pour les deux</p> |
| MV3 |C:\ClusterStorage\SourceVolume2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| MV4 |\FileServer\SourceShare2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>SILVER_TARGET pour les deux</p> |
| MV5 |C:\ClusterStorage\SourceVolume3 |N/A |Aucun mappage, afin de l’emplacement de stockage par défaut hello d’hôte de hello Hyper-V est utilisé. |



### <a name="data-privacy-overview"></a>Présentation de la confidentialité des données

Le tableau suivant résume la façon dont les données sont stockées dans ce scénario :

- - -
| Action | **Détails** | **Données collectées** | **Utilisation** | **Obligatoire** |
| --- | --- | --- | --- | --- |
| **Inscription** | Vous inscrivez un serveur VMM dans un coffre Recovery Services. Si vous souhaitez ultérieurement toounregister un serveur, vous pouvez le faire en supprimant les informations sur le serveur hello de hello portail Azure. | Après avoir inscrit un serveur VMM récupération de Site collecte, traite et transfère les métadonnées sur le serveur VMM de hello et les noms de hello des clouds VMM de hello détectées par la récupération de Site. | les données de salutation sont tooidentify utilisé et communiquent avec le serveur VMM approprié de hello et configurer les paramètres pour les clouds VMM appropriés. | Cette fonctionnalité est requise. Si vous ne souhaitez pas cette tooSite informations récupération toosend vous ne devez pas utiliser le service de récupération de Site hello. |
| **Activer la réplication** | Hello fournisseur Azure Site Recovery est installé sur le serveur VMM de hello et est conduit hello pour la communication avec hello service Site Recovery. Hello fournisseur est une bibliothèque de liens dynamiques (DLL) hébergée dans le processus de VMM hello. Après hello que fournisseur est installé, la fonctionnalité de « Récupération de centre de données » hello obtient activée dans la console Administrateur VMM hello. Ordinateurs virtuels nouveaux et existants peuvent activer cette protection tooenable de fonctionnalité pour une machine virtuelle. |Avec cette propriété est définie, hello fournisseur envoie le nom de hello et l’ID de hello VM tooSite récupération.  La réplication est activée par le réplica Hyper-V de Windows Server 2012 ou Windows Server 2012 R2. données de machine virtuelle Hello répliquées à partir d’un tooanother d’ordinateur hôte Hyper-V (généralement situé dans un centre de données différent de « récupération »). |Récupération de site utilise les informations de machine virtuelle de hello métadonnées toopopulate hello Bonjour portail Azure. | Cette fonctionnalité est une partie essentielle du service de hello et ne peut pas être désactivée. Si vous ne souhaitez pas toosend ces informations, n’activez la protection de récupération de Site pour les machines virtuelles. Notez que toutes les données envoyées par le fournisseur de hello tooSite récupération est envoyé via HTTPS. |
| **Plan de récupération** | Plans de récupération vous aider à générer un plan d’orchestration pour le centre de données de récupération hello. Vous pouvez définir l’ordre de hello dans lequel les machines virtuelles ou un groupe d’ordinateurs virtuels doit être démarré sur site de récupération hello. Vous pouvez également spécifier n’importe quel toobe des scripts automatisés exécuter ou n’importe quel toobe action manuelle effectuée au moment de hello de récupération pour chaque machine virtuelle. Basculement est généralement déclenché au niveau de plan de récupération hello pour la récupération coordonnée. | Récupération de site collecte, traite et transmet les métadonnées de plan de récupération hello, y compris les métadonnées de l’ordinateur virtuel et les métadonnées des scripts d’automatisation et notes de l’action manuelle. |Hello métadonnées sont un plan de récupération utilisé toobuild hello Bonjour portail Azure. |Cette fonctionnalité est une partie essentielle du service de hello et ne peut pas être désactivée. Si vous ne souhaitez pas cette tooSite informations récupération toosend, ne créez pas de plans de récupération. |
| **Mappage réseau** | Cartes réseau des informations à partir du centre de données de récupération de toohello hello données primaires center. Lors de la récupération des machines virtuelles sur le site de récupération hello, le mappage réseau permet d’établir une connectivité réseau. |Récupération de site collecte, traite et transmet les métadonnées hello de réseaux logiques de hello pour chaque site (principal et centre de données). |les métadonnées Hello sont toopopulate utilisé les paramètres de réseau afin que vous pouvez mapper les informations du réseau hello. | Cette fonctionnalité est une partie essentielle du service de hello et ne peut pas être désactivée. Si vous ne souhaitez pas cette tooSite informations récupération toosend, n’utilisez pas le mappage réseau. |
| **Basculement (planifié/non planifié/test)** | Basculement échoue sur les ordinateurs virtuels à partir de tooanother de centre de données géré par VMM. action de basculement Hello est déclenchée manuellement Bonjour portail Azure. |Hello fournisseur sur le serveur VMM de hello est informé de l’événement de basculement hello par Site Recovery et exécute une action de basculement sur l’ordinateur hôte Hyper-V de hello via les interfaces VMM. Basculement réel d’un ordinateur virtuel est à partir d’un tooanother d’ordinateur hôte Hyper-V et gérés par Windows Server 2012 ou Windows Server 2012 R2 Hyper-V Replica. Récupération de Site arrière utilise les informations de hello envoyées d’état de hello toopopulate d’informations sur l’action de basculement hello Bonjour portail Azure. | Cette fonctionnalité est une partie essentielle du service de hello et ne peut pas être désactivée. Si vous ne souhaitez pas cette tooSite informations récupération toosend, n’utilisez pas de basculement. |

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez testé le déploiement de hello, en savoir plus sur les autres types de [basculement](site-recovery-failover.md)
