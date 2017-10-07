---
title: aaaSet de HPC Pack hybride de cluster dans Azure | Documents Microsoft
description: "Découvrez comment toouse Microsoft HPC Pack et Azure tooset jusqu'à un petit, hybride haute performance computing (HPC) cluster"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Configuration d’un cluster de calcul haute performance (HPC) hybride avec Microsoft HPC Pack et les nœuds de calcul Azure à la demande
Utilisez Microsoft HPC Pack 2012 R2 et Azure tooset d’un petite, hybride informatiques hautes performances cluster (HPC). cluster Hello illustré dans cet article se compose d’un nœud principal de HPC Pack sur site et certains nœuds que vous déployez à la demande dans Azure cloud service de calcul. Vous pouvez ensuite exécuter des travaux de calcul sur un cluster hybride de hello.

![Cluster HPC hybride][Overview] 

Ce didacticiel illustre une approche, parfois appelé cluster « rafale toohello cloud », applications de calcul intensif toorun toouse évolutive, à la demande des ressources Azure.

Ce didacticiel ne requiert pas d'expérience préalable avec les clusters de calcul ou HPC Pack. Il est prévu toohelp uniquement, vous déployez un cluster de calcul hybride rapidement à des fins de démonstration. Pour considérations et toodeploy étapes de cluster HPC Pack hybride à plus grande échelle dans un environnement de production, ou toouse HPC Pack 2016, consultez hello [conseils détaillés](http://go.microsoft.com/fwlink/p/?LinkID=200493). Pour d’autres scénarios avec HPC Pack, notamment le déploiement automatisé de clusters dans des machines virtuelles Azure, consultez [Options pour créer et gérer un cluster de calcul haute performance dans Azure avec Microsoft HPC Pack](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="prerequisites"></a>Composants requis
* **Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.
* **Un ordinateur local exécutant Windows Server 2012 R2 ou Windows Server 2012** -utiliser cet ordinateur en tant que nœud principal de hello de cluster HPC de hello. Si vous n'utilisez pas déjà Windows Server, vous pouvez télécharger et installer une [version d'évaluation](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).
  
  * ordinateur de Hello doit être domaine d’Active Directory tooan jointes. À des fins de test, vous pouvez configurer l’ordinateur du nœud principal hello comme contrôleur de domaine. tooadd hello du rôle de serveur Services de domaine Active Directory et promouvoir l’ordinateur du nœud principal hello comme contrôleur de domaine, consultez la documentation de hello pour Windows Server.
  * toosupport HPC Pack, le système d’exploitation de hello doit être installé dans un de ces langues : anglais, japonais et chinois (simplifié).
  * Vérifiez que les mises à jour importantes et critiques sont installées.
* **HPC Pack 2012 R2** - [télécharger](http://go.microsoft.com/fwlink/p/?linkid=328024) package d’installation hello pour la version la plus récente hello sans frais et copie hello fichiers toohello ordinateur du nœud principal. Choisissez les fichiers d’installation Bonjour même langue que celle de votre installation de Windows Server.

    >[!NOTE]
    > Si vous souhaitez toouse HPC Pack 2016, au lieu de HPC Pack 2012 R2, une configuration supplémentaire est nécessaire. Consultez hello [conseils détaillés](http://go.microsoft.com/fwlink/p/?LinkID=200493).
    > 
* **Compte de domaine** -ce compte doit être configuré avec des autorisations d’administrateur locales sur hello tooinstall de nœud principal HPC Pack.
* **Connectivité TCP sur le port 443** de tooAzure de nœud principal hello.

## <a name="install-hpc-pack-on-hello-head-node"></a>Installez le Pack HPC sur le nœud principal de hello
Vous devez tout d'abord installer Microsoft HPC Pack sur votre ordinateur local qui exécute Windows Server Cet ordinateur devient hello nœud de tête hello cluster.

1. Ouvrez une session sur le nœud principal de toohello à l’aide d’un compte de domaine qui dispose des autorisations d’administrateur locales.

2. Démarrez hello Assistant d’Installation de HPC Pack en exécutant Setup.exe à partir de fichiers d’installation de HPC Pack hello.

3. Sur hello **le programme d’installation de HPC Pack 2012 R2** , cliquez sur **nouvelle installation ou ajoutez l’installation existante de nouvelles fonctionnalités tooan**.

    ![Configuration de HPC Pack 2012][install_hpc1]

4. Sur hello **page contrat utilisateur de logiciels Microsoft**, cliquez sur **suivant**.

5. Sur hello **sélectionner le Type d’Installation** , cliquez sur **créer un cluster HPC en créant un nœud principal**, puis cliquez sur **suivant**.

6. Assistant de Hello exécute plusieurs tests avant l’installation. Cliquez sur **suivant** sur hello **règles d’Installation** page si tous les tests réussissent. Sinon, passez en revue les informations hello fournies et apportez les modifications nécessaires dans votre environnement. Puis exécutez à nouveau les tests hello ou si nécessaire démarrer hello Assistant Installation à nouveau.
7. Sur hello **Configuration de base de données HPC** , vérifiez que **le nœud principal** est activée pour toutes les bases de données HPC, puis cliquez sur **suivant**. 

    ![Configuration de base de données][install_hpc4]

8. Acceptez les sélections par défaut sur les pages restantes de hello d’Assistant de hello. Sur hello **installer les composants nécessaires** , cliquez sur **installer**.
   
    ![Installer][install_hpc6]

9. Après l’installation de hello, décochez la case **démarrer HPC Cluster Manager** puis cliquez sur **Terminer**. (Vous pourrez démarrer HPC Cluster Manager à une étape ultérieure.)
   
    ![Terminer][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Préparer hello abonnement Azure
Effectuer hello comme suit dans hello [portail Azure](https://portal.azure.com) avec votre abonnement Azure. Après avoir effectué ces étapes, vous pouvez déployer des nœuds Azure à partir du nœud principal local hello. 
  
  > [!NOTE]
  > Notez votre ID d’abonnement Azure. Il vous sera utile par la suite. Trouver l’ID de hello dans **abonnements** dans le portail de hello.
  > 

### <a name="upload-hello-default-management-certificate"></a>Télécharger le certificat de gestion par défaut hello
HPC Pack installe un certificat auto-signé sur le nœud principal hello, appelé certificat de gestion par défaut Microsoft HPC Azure hello, que vous pouvez télécharger en tant qu’un certificat de gestion Azure. Ce certificat est fourni pour le test et les déploiements de preuve de concept toosecure hello relier hello du nœud principal et Azure.

1. À partir de l’ordinateur du nœud principal hello, connectez-vous toohello [portail Azure](https://portal.azure.com).

2. Cliquez sur **Abonnements** > *nom_de_votre_abonnement*.

3. Cliquez sur **Certificats de gestion** > **Télécharger**.4. Rechercher sur le nœud principal de hello pour hello fichier C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer. Cliquez ensuite sur **Télécharger**.

   
Hello **gestion de Azure HPC par défaut** certificat apparaît dans la liste hello des certificats de gestion.

### <a name="create-an-azure-cloud-service"></a>Création d'un service cloud Azure
> [!NOTE]
> Pour de meilleures performances, créer un compte de stockage de hello (dans une étape ultérieure) et de service de cloud computing hello Bonjour même région géographique.
> 
> 

1. Dans le portail de hello, cliquez sur **(classiques) de services de cloud computing** > **+ ajouter**.

2.  Tapez un nom DNS pour le service de hello, choisissez un groupe de ressources et un emplacement, puis cliquez sur **créer**.


### <a name="create-an-azure-storage-account"></a>Création d'un compte de stockage Azure
1. Dans le portail de hello, cliquez sur **comptes de stockage (classiques)** > **+ ajouter**.

2. Tapez un nom pour le compte de hello et sélectionnez hello **classique** modèle de déploiement.

3. Sélectionnez un groupe de ressources et un emplacement, et conservez les valeurs par défaut des autres paramètres. Cliquez ensuite sur **Créer**.

## <a name="configure-hello-head-node"></a>Configurer le nœud principal de hello
toouse toodeploy de HPC Cluster Manager nœuds Azure et les travaux de toosubmit, d’abord effectuer certaines étapes de configuration de cluster nécessaires.

1. Sur le nœud principal de hello, démarrez HPC Cluster Manager. Si hello **sélectionner le nœud principal** boîte de dialogue s’affiche, cliquez sur **ordinateur Local**. Hello **liste des tâches de déploiement** s’affiche.

2. Sous **Tâches de déploiement requises**, cliquez sur **Configurer votre réseau**.
   
    ![Configurer le réseau][config_hpc2]

3. Dans l’Assistant Configuration du réseau de hello, sélectionnez **tous les nœuds sur un réseau d’entreprise** (topologie 5). Cette configuration de réseau est hello plus simple à des fins de démonstration.
   
    ![Topologie 5][config_hpc3]
   
4. Cliquez sur **suivant** tooaccept les valeurs par défaut sur hello restant des pages d’Assistant de hello. Ensuite, sous hello **révision** , cliquez sur **configurer** configuration du réseau toocomplete hello.

5. Bonjour **liste des tâches de déploiement**, cliquez sur **fournissent des informations d’identification de l’installation**.

6. Bonjour **informations d’identification de l’Installation** boîte de dialogue, les informations d’identification de type hello du compte de domaine hello que vous avez utilisé tooinstall HPC Pack. Cliquez ensuite sur **OK**. 
   
    ![Installation Credentials][config_hpc6]
   
7. Bonjour **liste des tâches de déploiement**, cliquez sur **configurer hello d’affectation de noms des nouveaux nœuds**.

8. Bonjour **spécifier une série de noms de nœud** boîte de dialogue zone, accepter d’affectation de noms série et cliquez sur la valeur par défaut hello **OK**. Effectuez cette étape, même si hello nœuds Azure, que vous ajoutez dans ce didacticiel sont nommées automatiquement.
   
    ![Noms de nœuds][config_hpc8]
   
9. Bonjour **liste des tâches de déploiement**, cliquez sur **créer un modèle de nœud**. Plus loin dans le didacticiel de hello, vous utilisez cluster toohello de hello nœud modèle tooadd nœuds Azure.

10. Dans hello Assistant modèle de nœud, procédez comme hello suivant :
    
    a. Sur hello **choisir le Type de modèle de nœud** , cliquez sur **modèle de nœud Windows Azure**, puis cliquez sur **suivant**.
    
    ![Modèle de nœud][config_hpc10]
    
    b. Cliquez sur **suivant** nom de modèle par défaut tooaccept hello.
    
    c. Sur hello **fournissent des informations d’abonnement** , entrez votre ID d’abonnement Azure (disponible dans les informations de votre compte Azure). Puis, sous **Certificat de gestion**, recherchez **Gestion Azure Microsoft HPC par défaut**. Cliquez ensuite sur **Suivant**.
    
    ![Modèle de nœud][config_hpc12]
    
    d. Sur hello **fournissent des informations de Service** page, le service cloud sélectionnez hello et compte de stockage hello que vous avez créé à l’étape précédente. Cliquez ensuite sur **Suivant**.
    
    ![Modèle de nœud][config_hpc13]
    
    e. Cliquez sur **suivant** tooaccept les valeurs par défaut sur hello restant des pages d’Assistant de hello. Ensuite, sous hello **révision** , cliquez sur **créer** modèle de nœud toocreate hello.
    
    > [!NOTE]
    > Par défaut, modèle de nœud Azure hello inclut des paramètres pour toostart (disposition) et les nœuds de hello arrêter manuellement, à l’aide de HPC Cluster Manager. Vous pouvez éventuellement configurer un toostart de planification et d’arrêter hello automatiquement des nœuds Azure.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Ajouter des nœuds Azure toohello cluster
Maintenant utiliser le cluster de toohello hello nœud modèle tooadd nœuds Azure. Ajout de cluster de toohello nœuds hello stocke ses informations de configuration afin que vous puissiez démarrer (approvisionner) les à tout moment dans le service cloud hello. Votre abonnement obtient uniquement facturé pour les nœuds Azure une fois que les instances de hello sont en cours d’exécution dans le service cloud hello.

Suivez ces étapes tooadd deux petits nœuds.

1. Dans HPC Cluster Manager, cliquez sur **Gestion des nœuds** (ou **Gestion des ressources** dans les versions actuelles de HPC Pack) > **Ajouter un nœud**.
   
    ![Add Node][add_node1]

2. Dans hello Assistant Ajout de nœud, sur hello **sélectionner la méthode de déploiement** , cliquez sur **nœuds ajouter Windows Azure**, puis cliquez sur **suivant**.
   
    ![Ajouter un nœud Azure][add_node1_1]

3. Sur hello **spécifier de nouveaux nœuds** page, le modèle de nœud Azure hello sélectionnez vous avez créé précédemment (appelée par défaut **par défaut AzureNode modèle**). Spécifiez ensuite **2** nœuds de taille **Petite**, puis cliquez sur **Suivant**.
   
    ![Spécifier les nœuds][add_node2]
   
4. Sur hello **fin hello Assistant Ajout de nœud** , cliquez sur **Terminer**.
    
     Deux nœuds Azure, nommés **AzureCN-0001** et **AzureCN-0002**, sont désormais affichés dans HPC Cluster Manager. Les deux sont Bonjour **Not-Deployed** état.
   
    ![Nœuds ajoutés][add_node3]

## <a name="start-hello-azure-nodes"></a>Démarrer hello des nœuds Azure
Lorsque vous souhaitez que les ressources du cluster de hello toouse dans Azure, utilisez HPC Cluster Manager toostart (disposition) hello des nœuds Azure et les mettent en ligne.

1. Dans HPC Cluster Manager, cliquez sur **la gestion des nœuds** (appelé **gestion des ressources** dans les versions actuelles de HPC Pack), et sélectionnez hello nœuds Azure.

2. Cliquez sur **Démarrer**, puis sur **OK**.
   
   ![Démarrer les nœuds][add_node4]
   
    les nœuds Hello transition toohello **Provisioning** état. Hello vue hello tootrack de journal progression de provisionnement de configuration.
   
    ![Nœuds d'approvisionnement][add_node6]

3. Après quelques minutes, hello nœuds Azure terminer l’approvisionnement et sont Bonjour **hors connexion** état. Dans cet état, les instances de rôle hello sont en cours d’exécution mais ne peut pas accepter encore les travaux de cluster.

4. tooconfirm qui hello des instances de rôle sont en cours d’exécution, Bonjour portail Azure, cliquez sur **Services Cloud (classiques)** > *your_cloud_service_name*.
   
   Vous devez voir deux **HpcWorkerRole** instances (nœuds) en cours d’exécution dans le service hello. HPC Pack déploie automatiquement deux **HpcProxy** instances de communication de toohandle (taille moyenne) entre le nœud principal de hello et Azure.

   ![Instances en cours d'exécution][view_instances1]

5. toorun en ligne des nœuds Azure hello toobring de travaux, les nœuds sélectionnez hello, avec le bouton droit, puis cliquez sur cluster **mettre en ligne**.
   
    ![Nœuds hors ligne][add_node7]
   
    HPC Cluster Manager indique que les nœuds de hello sont Bonjour **Online** état.

## <a name="run-a-command-across-hello-cluster"></a>Exécuter une commande sur le cluster de hello
installation de hello toocheck, utilisez hello HPC Pack **clusrun** commande toorun une commande ou une application sur un ou plusieurs nœuds de cluster. À titre d’exemple, utilisez **clusrun** configuration d’IP tooget hello de hello nœuds Azure.

1. Sur le nœud principal de hello, ouvrez une invite de commandes en tant qu’administrateur.

2. Tapez hello de commande suivante :
   
    `clusrun /nodes:azurecn* ipconfig`

3. Si vous y êtes invité, entrez votre mot de passe administrateur de cluster. Vous devez voir similaire toohello suivant de sortie de commande.
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a>Exécution d'une tâche de test
Maintenant soumettre un travail de test qui s’exécute sur un cluster hybride de hello. Cet exemple est une simple tâche de « balayage paramétrique » (un type de calcul intrinsèquement parallèle). Cet exemple exécute des tâches subordonnées qui ajoutent une tooitself entier à l’aide de hello **set /a** commande. Tous les nœuds hello cluster de hello contribuent toofinishing les tâches subordonnées hello pour les entiers de 1 too100.

1. Dans HPC Cluster Manager, cliquez sur **Gestion des tâches** > **Nouvelle tâche de balayage paramétrique**.
   
    ![Nouvelle tâche][test_job1]

2. Bonjour **nouveau travail de balayage paramétrique** boîte de dialogue **ligne de commande**, type `set /a *+*` (ligne de commande hello par défaut qui s’affiche par écrasement). Conservez les valeurs par défaut pour hello restant de paramètres, puis cliquez sur **Submit** tâche hello de toosubmit.
   
    ![Balayage paramétrique][param_sweep1]

3. Lorsque le travail hello est terminé, double-cliquez sur hello **Mes tâches balayage** travail.

4. Cliquez sur **afficher les tâches**, puis cliquez sur une sortie de hello calculé sous-tâche tooview cette tâche subordonnée.
   
    ![Résultats de la tâche][view_job361]

5. toosee quel nœud effectué le calcul de hello pour cette tâche subordonnée, cliquez sur **alloué des nœuds**. (votre cluster peut indiquer un nom de nœud différent).
   
    ![Résultats de la tâche][view_job362]

## <a name="stop-hello-azure-nodes"></a>Arrêter hello des nœuds Azure
Une fois que vous essayez de cluster de hello, arrêtez compte tooyour de hello nœuds Azure tooavoid les coûts inutiles. Cette étape arrête le service de cloud computing hello et supprime des instances de rôle Azure hello.

1. Dans HPC Cluster Manager, sous **Gestion des nœuds** (ou **Gestion des ressources** dans les versions antérieures de HPC Pack), sélectionnez les deux nœuds Azure. Cliquez ensuite sur **Arrêter**.
   
    ![Arrêter les nœuds][stop_node1]

2. Bonjour **nœuds arrêter Windows Azure** boîte de dialogue, cliquez sur **arrêter**. 
   
3. les nœuds Hello transition toohello **arrêt** état. Après quelques minutes, HPC Cluster Manager indique que les nœuds hello **Not-Deployed**.
   
    ![Nœuds non déployés][stop_node4]

4. tooconfirm les instances de rôle hello sont n’est plus en cours d’exécution dans Azure, dans hello portail, Azure, sur **(classiques) de services de cloud computing** > *your_cloud_service_name*. Aucune instance n’est déployés dans un environnement de production hello. 
   
    Didacticiel de hello est terminée.

## <a name="next-steps"></a>Étapes suivantes
* Explorer la documentation hello pour [HPC Pack](https://technet.microsoft.com/library/cc514029).
* tooset d’un déploiement de cluster HPC Pack à une échelle supérieure, hybride voir [croître tooAzure des Instances de rôle de travail avec Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).
* Pour les autres façons toocreate un cluster HPC Pack dans Azure, y compris à l’aide de modèles Azure Resource Manager, consultez [options de cluster HPC avec Microsoft HPC Pack dans Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
