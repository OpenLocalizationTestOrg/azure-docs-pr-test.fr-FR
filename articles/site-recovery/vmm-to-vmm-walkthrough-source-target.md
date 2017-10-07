---
title: "aaaSet hello source et un cible pour le site secondaire tooa réplication Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment tooset jusqu'à la source de hello et cibler lorsque des ordinateurs virtuels Hyper-V de réplication de site toosecondary VMM avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>Étape 6 : Configurer la cible et source de réplication hello


Après avoir créé un Services de récupération de coffre pour Hyper-V réplication tooa site VMM secondaire avec [Azure Site Recovery](site-recovery-overview.md), utiliser cette tooset article source de hello et cibler des emplacements de réplication. 

Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Installer hello fournisseur Azure Site Recovery sur les serveurs VMM et découvrir et inscrire les serveurs dans le coffre hello.

1. Cliquez sur **Étape 1 : Préparer l’infrastructure** > **Source**.

    ![Configurer la source](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. Dans **Prepare source**, cliquez sur **+ VMM** tooadd un serveur VMM.

    ![Configurer la source](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. Dans **ajouter un serveur**, vérifiez que **serveur System Center VMM** s’affiche dans **type de serveur** et le serveur VMM hello satisfont à hello [conditions préalables](#prerequisites).
4. Téléchargez le fichier d’installation hello fournisseur Azure Site Recovery.
5. Téléchargez la clé d’inscription de hello. Vous en aurez besoin lorsque vous exécuterez le programme d’installation. clé de Hello est valide pendant cinq jours après que l’avoir généré.

    ![Configurer la source](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Installez hello fournisseur Azure Site Recovery sur le serveur VMM de hello. Vous n’avez pas besoin tooexplicitly installer quoi que ce soit sur des serveurs hôtes Hyper-V.


## <a name="install-hello-azure-site-recovery-provider"></a>Installer hello fournisseur Azure Site Recovery

1. Exécutez le fichier de configuration de fournisseur hello sur chaque serveur VMM. Si VMM est déployé dans un cluster, procédez comme suit de hello hello première fois que vous installez :
    -  Installer le fournisseur de hello sur un nœud actif et de fin hello installation tooregister hello serveur VMM dans le coffre hello.
    - Ensuite, installez hello fournisseur sur hello autres nœuds. Nœuds de cluster doivent tous exécuter hello même version de hello fournisseur.
2. Le programme d’installation exécute quelques vérifications et demandes de service d’autorisation toostop hello VMM. Hello service VMM va redémarrer automatiquement lorsque le programme d’installation se termine. Si vous installez sur un cluster VMM, vous êtes le rôle de Cluster hello toostop demandées.
3. Dans **Microsoft Update**, vous pouvez la choisir toospecify que les mises à jour du fournisseur sont installées conformément à votre stratégie Microsoft Update.
4. Dans **Installation**, acceptez ou modifiez l’emplacement d’installation par défaut hello et cliquez sur **installer**.

    ![Emplacement d’installation](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. Une fois l’installation terminée, cliquez sur **inscrire** serveur hello de tooregister dans le coffre hello.

    ![Emplacement d’installation](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. Dans **nom du coffre**, vérifier nom hello de coffre hello dans le hello serveur sera inscrit. Cliquez sur *Suivant*.

    ![Enregistrement du serveur](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. Dans **connexion Internet**, spécifiez comment hello fournisseur en cours d’exécution sur le serveur VMM de hello connecte tooAzure.

    ![Paramètres Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - Vous pouvez spécifier que le fournisseur hello doit se connecter directement toohello internet, ou via un proxy.
   - Spécifiez les paramètres de proxy, si nécessaire.
   - Si vous utilisez un proxy, un compte RunAs VMM (DRAProxyAccount) est créé automatiquement à l’aide de hello spécifié les informations d’identification de proxy. Configurer le serveur de proxy hello afin que ce compte peut s’authentifier avec succès. Hello les paramètres de compte d’identification peuvent être modifiés dans la console VMM hello > **paramètres** > **sécurité** > **exécuter en tant que comptes**. Redémarrez les modifications de tooupdate service hello VMM.
8. Dans **clé d’inscription**, sélectionnez clé hello téléchargés à partir d’Azure Site Recovery et copiée serveur VMM de toohello.
9. paramètre de chiffrement Hello est uniquement utilisé lorsque vous répliquez des ordinateurs virtuels Hyper-V dans VMM clouds tooAzure. Si vous effectuez une réplication site secondaire de tooa n’est pas utilisé.
10. Dans **nom du serveur**, spécifiez un serveur VMM à hello tooidentify nom convivial dans le coffre hello. Dans une configuration de cluster spécifier le nom de rôle de cluster VMM hello.
11. Dans **synchroniser les métadonnées du cloud**, sélectionnez si vous souhaitez toosynchronize métadonnées pour tous les clouds sur le serveur VMM de hello avec le coffre de hello. Cette action ne doit toohappen qu’une seule fois sur chaque serveur. Si vous ne souhaitez pas toosynchronize tous les clouds, vous pouvez laisser ce paramètre désactivé et synchroniser chaque cloud individuellement dans les propriétés du cloud hello dans la console VMM hello.
12. Cliquez sur **suivant** processus de hello toocomplete. Après l’inscription, les métadonnées d’un serveur hello VMM sont récupérées par Azure Site Recovery. serveur de Hello est affiché sur hello **serveurs VMM** onglet hello **serveurs** page dans le coffre hello.

    ![Serveur](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Une fois le serveur de hello est disponible dans la console de récupération de Site hello dans **Source** > **Prepare source** sélectionnez hello VMM server et nuage hello sélectionnez quels Bonjour Hyper-V se trouve. Cliquez ensuite sur **OK**.

Vous pouvez également installer le fournisseur de hello à partir de la ligne de commande hello :

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello

Sélectionner le cloud et le serveur VMM de hello cible :

1. Cliquez sur **Prepare infrastructure** > **cible**et sélectionnez hello cible VMM serveur toouse.
2. Les clouds sur le serveur hello qui sont synchronisés avec la récupération de Site seront affiche. Sélectionnez le cloud cible de hello.

   ![Cible](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 7 : configurer le mappage réseau](vmm-to-vmm-walkthrough-network-mapping.md).
