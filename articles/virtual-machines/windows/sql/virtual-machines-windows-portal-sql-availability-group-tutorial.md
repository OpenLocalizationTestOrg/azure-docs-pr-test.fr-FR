---
title: "aaaSQL groupes de disponibilité de serveur - des Machines virtuelles Azure - didacticiel | Documents Microsoft"
description: "Ce didacticiel montre comment toocreate un SQL Server groupe de disponibilité AlwaysOn sur des Machines virtuelles Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Configurer manuellement des groupes de disponibilité AlwaysOn dans une machine virtuelle Azure

Ce didacticiel montre comment toocreate un SQL Server groupe de disponibilité AlwaysOn sur des Machines virtuelles Azure. didacticiel complet de Hello crée un groupe de disponibilité avec un réplica de base de données sur deux serveurs SQL Server.

**Durée estimée**: prend environ 30 minutes toocomplete une fois que les conditions préalables de hello sont remplies.

diagramme de Hello illustre ce que vous créez dans le didacticiel de hello.

![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Composants requis

Hello est supposé qu'avoir une connaissance élémentaire de SQL Server groupes de disponibilité AlwaysOn. Pour plus d’informations, consultez [Vue d’ensemble des groupes de disponibilité AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Hello tableau suivant répertorie les conditions préalables de hello que vous avez besoin de toocomplete avant de commencer ce didacticiel :

|  |Prérequis |Description |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | Deux serveurs SQL Server | - Dans un groupe à haute disponibilité Azure <br/> - Dans un domaine <br/> - Avec la fonctionnalité de Clustering de basculement installée |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Partage de fichiers pour le témoin de cluster |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Compte du service SQL Server | Compte du domaine |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Compte du service SQL Server Agent | Compte du domaine |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Ports du pare-feu ouverts | - SQL Server : **1433** pour l’instance par défaut <br/> - Point de terminaison de mise en miroir de bases de données : **5022** ou un port disponible <br/> - Sonde d’équilibrage de charge Azure : **59999** ou un port disponible |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Ajout de la fonctionnalité de Clustering de basculement | Fonctionnalité requise sur les deux serveurs SQL Server |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Compte du domaine d’installation | - Administrateur local sur chaque serveur SQL Server <br/> - Membres du rôle de serveur fixe sysadmin pour chaque instance de SQL Server  |


Avant de commencer le didacticiel de hello, vous devez trop[remplir les conditions préalables pour la création de groupes de disponibilité AlwaysOn dans Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md). Si ces conditions préalables ne sont déjà terminées, vous pouvez passer trop[création d’un Cluster](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Créer le cluster de hello

Après avoir hello conditions préalables sont remplies, hello première étape consiste toocreate un Cluster de basculement Windows Server qui inclut deux serveurs de SQL et un serveur témoin.  

1. RDP toohello première SQL Server à l’aide d’un compte de domaine qui est administrateur sur les serveurs SQL et le serveur témoin hello.

   >[!TIP]
   >Si vous avez suivi hello [document configuration requise](virtual-machines-windows-portal-sql-availability-group-prereq.md), vous avez créé un compte appelé **CORP\Install**. Utilisez ce compte.

2. Bonjour **le Gestionnaire de serveur** tableau de bord, sélectionnez **outils**, puis cliquez sur **Gestionnaire du Cluster de basculement**.
3. Dans le volet gauche de hello, cliquez sur **Gestionnaire du Cluster de basculement**, puis cliquez sur **créer un Cluster**.
   ![Création d’un cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. Dans Assistant Création d’un Cluster de hello, créer un cluster à un nœud en parcourant les pages hello avec les paramètres de hello en hello tableau suivant :

   | Page | Paramètres |
   | --- | --- |
   | Avant de commencer |Utilisation des valeurs par défaut |
   | Sélection des serveurs |Hello de type premier SQL Server nom de **nom du serveur** et cliquez sur **ajouter**. |
   | Avertissement de validation |Sélectionnez **non. je ne nécessitent pas de prise en charge de Microsoft pour ce cluster et par conséquent ne voulez pas que la validation toorun hello teste. Lorsque vous cliquez sur Suivant, poursuivre la création de cluster de hello**. |
   | Point d’accès pour administration hello Cluster |Tapez un nom de cluster, par exemple **SQLAGCluster1** dans **Nom du cluster**.|
   | Confirmation |Utilisez les valeurs par défaut, sauf si vous utilisez des espaces de stockage. Voir la Remarque hello sous ce tableau. |

### <a name="set-hello-cluster-ip-address"></a>Définir l’adresse IP du cluster hello

1. Dans **Gestionnaire du Cluster de basculement**, faites défiler la liste trop**ressources principales du Cluster** et développez les détails du cluster hello. Vous devez voir deux hello **nom** et hello **adresse IP** ressources Bonjour **n’a pas pu** état. Hello ressource d’adresse IP ne peut pas être mises en ligne, car le cluster de hello est assigné hello même adresse IP en tant qu’ordinateur hello lui-même, par conséquent, il est une adresse en double.

2. Hello avec le bouton échoué **adresse IP** ressource, puis cliquez sur **propriétés**.

   ![Propriétés du cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Sélectionnez **adresse IP statique** et spécifiez une adresse disponible à partir du sous-réseau dans lequel hello SQL Server est dans la zone de texte adresse hello. Cliquez ensuite sur **OK**.
4. Bonjour **ressources principales du Cluster** , cliquez sur le nom de cluster et cliquez sur **mettre en ligne**. Attendez que les deux ressources soient en ligne. Lors de la ressource de nom de cluster hello est mis en ligne, il met à jour serveur du contrôleur de domaine hello avec un nouveau compte d’ordinateur Active Directory. Utilisez cette hello de toorun AD compte service de cluster du groupe de disponibilité plus tard.

### <a name="addNode"></a>Ajouter hello autres toocluster SQL Server

Ajouter hello autre cluster toohello de SQL Server.

1. Dans l’arborescence du navigateur hello, cliquez sur le cluster de hello, sur **ajouter un nœud**.

    ![Ajouter le nœud toohello Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. Bonjour **Assistant Ajout de nœud**, cliquez sur **suivant**. Bonjour **sélectionner des serveurs** , ajoutez hello du deuxième serveur SQL Server. Nom de serveur de type hello dans **nom du serveur** puis cliquez sur **ajouter**. Une fois ces opérations effectuées, cliquez sur **Suivant**.

1. Bonjour **avertissement de Validation** , cliquez sur **non** (dans un scénario de production vous devez effectuer les tests de validation hello). Cliquez ensuite sur **Suivant**.

8. Bonjour **Confirmation** page si vous utilisez des espaces de stockage, hello désactivez case à cocher **ajouter tous les clusters de toohello totalité du stockage.**

   ![Confirmation de l’ajout du nœud](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Si vous utilisez des espaces de stockage et que vous ne désactivez pas **ajouter tous les totalité du stockage du cluster toohello**, Windows détache les disques virtuels hello pendant hello processus de clustering. Par conséquent, ils n’apparaissent pas dans le Gestionnaire de disque ou de l’Explorateur, jusqu'à ce que les espaces de stockage hello sont supprimés du cluster de hello et rattachés à l’aide de PowerShell. Les espaces de stockage regroupe plusieurs disques dans des pools toostorage. Pour plus d’informations, consultez la page [Espaces de stockage](https://technet.microsoft.com/library/hh831739).

1. Cliquez sur **Suivant**.

1. Cliquez sur **Terminer**.

   Gestionnaire du Cluster de basculement indique que votre cluster a un nouveau nœud et il répertorie Bonjour **nœuds** conteneur.

10. Déconnecter la session de bureau à distance hello.

### <a name="add-a-cluster-quorum-file-share"></a>Ajouter un partage de fichiers de quorum de cluster

Dans cet exemple cluster de Windows hello utilise un toocreate de partage de fichier un quorum de cluster. Ce didacticiel utilise un quorum Nœud et partage de fichiers majoritaires. Pour plus d’informations, consultez [Présentation des configurations de quorum dans un cluster de basculement](http://technet.microsoft.com/library/cc731739.aspx).

1. Connecter le serveur membre de témoin de partage de fichier toohello avec une session Bureau à distance.

1. Dans **Gestionnaire de serveur**, cliquez sur **Outils**. Ouvrez **Gestion de l’ordinateur**.

1. Cliquez sur **Dossiers partagés**.

1. Cliquez avec le bouton droit sur **Partages**, puis cliquez sur **Nouveau partage...**.

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Utilisez **créer un Assistant dossier partagé** toocreate un partage.

1. Sur **chemin d’accès du dossier**, cliquez sur **Parcourir** et localiser ou créer un chemin d’accès pour le dossier partagé de hello. Cliquez sur **Suivant**.

1. Dans **nom, Description et paramètres** Vérifiez le nom de partage hello et chemin d’accès. Cliquez sur **Suivant**.

1. Dans **Autorisations du dossier partagé**, sélectionnez **Personnaliser les autorisations**. Cliquez sur **Personnalisé...**.

1. Dans **Personnaliser les autorisations**, cliquez sur **Ajouter...**.

1. Assurez-vous que ce cluster de hello toocreate hello compte utilisé dispose du contrôle total.

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. Cliquez sur **OK**.

1. Dans **Autorisations du dossier partagé**, cliquez sur **Terminer**. Cliquez à nouveau sur **Terminer**.  

1. Fermez la session sur le serveur de hello

### <a name="configure-cluster-quorum"></a>Configurer le quorum du cluster

Ensuite, définissez le quorum du cluster hello.

1. Se connecter toohello premier nœud du cluster avec le Bureau à distance.

1. Dans **Gestionnaire du Cluster de basculement**, cliquez sur le cluster de hello, pointez trop**autres Actions**, puis cliquez sur **configurer les paramètres du Quorum du Cluster...** .

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. Dans l’**Assistant Configuration de quorum du cluster**, cliquez sur **Suivant**.

1. Dans **sélectionner l’Option de Configuration de Quorum**, choisissez **sélectionner le témoin de quorum hello**, puis cliquez sur **suivant**.

1. Dans **Sélectionner le témoin de quorum**, cliquez sur **Configurer un témoin de partage de fichiers**.

   >[!TIP]
   >Windows Server 2016 prend en charge un témoin cloud. Si vous choisissez ce type de témoin, un témoin de partage de fichiers est inutile. Pour plus d’informations, consultez [Déployer un témoin cloud pour un cluster de basculement](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). Ce didacticiel utilise un témoin de partage de fichiers, que les systèmes d’exploitation antérieurs prennent en charge.

1. Sur **témoin de partage de fichier de configuration**, chemin d’accès de type hello pour partage hello vous avez créé. Cliquez sur **Suivant**.

1. Vérifiez les paramètres de hello sur **Confirmation**. Cliquez sur **Suivant**.

1. Cliquez sur **Terminer**.

ressources principales du cluster Hello sont configurés avec un témoin de partage de fichiers.

## <a name="enable-availability-groups"></a>Activer les groupes de disponibilité

Ensuite, activez hello **groupes de disponibilité AlwaysOn** fonctionnalité. Effectuez ces étapes pour les deux serveurs SQL Server.

1. À partir de hello **Démarrer** écran, lancez **Gestionnaire de Configuration SQL Server**.
2. Dans l’arborescence du navigateur hello, cliquez sur **SQL Server Services**, puis cliquez sur hello **SQL Server (MSSQLSERVER)** , puis cliquez sur **propriétés**.
3. Cliquez sur hello **haute disponibilité AlwaysOn** , puis sélectionnez **activer les groupes de disponibilité AlwaysOn**, comme suit :

    ![Activation des groupes à haute disponibilité AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. Cliquez sur **Apply**. Cliquez sur **OK** dans la boîte de dialogue contextuelle hello.

5. Redémarrez le service SQL Server de hello.

Répétez ces étapes sur hello autre serveur SQL Server.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Créer une base de données sur hello premier serveur SQL Server

1. Lancement hello RDP fichier toohello première SQL Server avec un domaine de compte qui est membre de sysadmin de rôle de serveur fixe.
1. Ouvrez SQL Server Management Studio et connectez-vous toohello premier serveur SQL Server.
7. Dans l’**Explorateur d’objets**, cliquez avec le bouton droit sur **Bases de données**, puis cliquez sur **Nouvelle base de données**.
8. Dans **Nom de base de données**, saisissez **MyDB1**, puis cliquez sur **OK**.

### <a name="backupshare"></a> Créer un partage de sauvegarde

1. Sur hello première SQL Server dans **le Gestionnaire de serveur**, cliquez sur **outils**. Ouvrez **Gestion de l’ordinateur**.

1. Cliquez sur **Dossiers partagés**.

1. Cliquez avec le bouton droit sur **Partages**, puis cliquez sur **Nouveau partage...**.

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Utilisez **créer un Assistant dossier partagé** toocreate un partage.

1. Sur **chemin d’accès du dossier**, cliquez sur **Parcourir** et localiser ou créer un chemin d’accès pour le dossier partagé sauvegarde de base de données hello. Cliquez sur **Suivant**.

1. Dans **nom, Description et paramètres** Vérifiez le nom de partage hello et chemin d’accès. Cliquez sur **Suivant**.

1. Dans **Autorisations du dossier partagé**, sélectionnez **Personnaliser les autorisations**. Cliquez sur **Personnalisé...**.

1. Dans **Personnaliser les autorisations**, cliquez sur **Ajouter...**.

1. Assurez-vous que contrôle total sur les comptes de service hello SQL Server et SQL Server Agent pour les deux serveurs.

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. Cliquez sur **OK**.

1. Dans **Autorisations du dossier partagé**, cliquez sur **Terminer**. Cliquez à nouveau sur **Terminer**.  

### <a name="take-a-full-backup-of-hello-database"></a>Effectuer une sauvegarde de base de données hello complète

Vous devez tooback hello nouvelle base de données tooinitialize hello journal dans la chaîne. Si vous ne prenez pas une sauvegarde de base de données hello, il ne peut pas être inclus dans un groupe de disponibilité.

1. Dans **l’Explorateur d’objets**, avec le bouton droit de la base de données hello, pointez trop**tâches...** , cliquez sur **Back Up**.

1. Cliquez sur **OK** tootake un emplacement de sauvegarde par défaut toohello sauvegarde complète.

## <a name="create-hello-availability-group"></a>Créer le groupe de disponibilité de hello
Vous êtes maintenant prêt tooconfigure étapes d’un groupe de disponibilité à l’aide de hello suivant :

* Créer une base de données sur hello premier serveur SQL Server.
* Effectuez une sauvegarde complète et une sauvegarde du journal des transactions de base de données hello
* Hello de restauration complète et toohello de sauvegardes de journal deuxième SQL Server avec hello **NORECOVERY** option
* Créer le groupe de disponibilité de hello (**AG1**) avec validation synchrone, le basculement automatique et réplicas secondaires lisibles

### <a name="create-hello-availability-group"></a>Créer le groupe de disponibilité de hello :

1. Sur la session Bureau à distance toohello premier serveur SQL Server. Dans l’**Explorateur d’objets** dans SSMS, cliquez avec le bouton droit sur **Haute disponibilité AlwaysOn**, puis cliquez sur **Assistant Nouveau groupe de disponibilité**.

    ![Lancer l'Assistant Nouveau groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. Bonjour **Introduction** , cliquez sur **suivant**. Bonjour **spécifier un nom de groupe de disponibilité** , tapez un nom pour hello groupe de disponibilité, par exemple **AG1**, dans **nom du groupe de disponibilité**. Cliquez sur **Suivant**.

    ![Assistant Nouveau groupe de disponibilité, spécifier le nom du groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. Bonjour **sélectionner les bases de données** page, sélectionnez votre base de données, cliquez sur **suivant**.

   >[!NOTE]
   >base de données Hello remplit les conditions préalables de hello pour un groupe de disponibilité car vous avez effectué au moins une sauvegarde complète sur le réplica principal de hello prévue.

   ![Assistant Nouveau groupe de disponibilité, sélectionner les bases de données](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. Bonjour **spécifier les réplicas** , cliquez sur **ajouter un réplica**.

   ![Assistant Nouveau groupe de disponibilité, spécifier les réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Hello **connecter tooServer** boîte de dialogue. Nom du type hello du serveur de deuxième hello dans **nom du serveur**. Cliquez sur **Connecter**.

   Dans hello **spécifier les réplicas** page, vous devez maintenant voir hello second serveur répertorié dans **réplicas de disponibilité**. Configurez les réplicas hello comme suit.

   ![Assistant Nouveau groupe de disponibilité, spécifier les réplicas (Terminé)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Cliquez sur **points de terminaison** toosee hello mise en miroir point de terminaison pour ce groupe de disponibilité. Hello d’utiliser le même port que vous avez utilisé lorsque vous définissez hello [règle de pare-feu pour les points de terminaison de mise en miroir de base de données](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Assistant Nouveau groupe de disponibilité, sélectionner la synchronisation initiale des données](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. Bonjour **sélectionner la synchronisation initiale des données** , sélectionnez **complète** et spécifiez un emplacement réseau partagé. Pour l’emplacement de hello, utiliser hello [partage de sauvegarde que vous avez créé](#backupshare). Dans l’exemple hello qu’il a été, **\\\\\<premier SQL Server\>\Backup\**. Cliquez sur **Suivant**.

   >[!NOTE]
   >Synchronisation complète effectue une sauvegarde complète de base de données hello hello première instance de SQL Server et il restaure toohello une deuxième instance. Pour les bases de données volumineuses, une synchronisation complète n’est pas recommandée, car elle peut prendre longtemps. Vous pouvez réduire ce délai en manuellement une sauvegarde de base de données hello et sa restauration avec `NO RECOVERY`. Si la base de données hello est déjà restaurée avec `NO RECOVERY` sur hello deuxième SQL Server avant de configurer le groupe de disponibilité de hello, choisissez **joindre uniquement**. Si vous souhaitez la sauvegarde de hello tootake après avoir configuré le groupe de disponibilité de hello, choisissez **ignorer la synchronisation initiale des données**.

    ![Assistant Nouveau groupe de disponibilité, sélectionner la synchronisation initiale des données](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. Bonjour **Validation** , cliquez sur **suivant**. Cette page doit être similaire toohello suivant l’image :

    ![Assistant Nouveau groupe de disponibilité, validation](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Il est un avertissement pour la configuration de l’écouteur hello, car vous n’avez pas configuré un écouteur de groupe de disponibilité. Vous pouvez ignorer cet avertissement, car sur les machines virtuelles que vous créez les écouteur hello après la création d’équilibrage de charge Azure hello.

10. Bonjour **Résumé** , cliquez sur **Terminer**, puis patientez pendant que l’Assistant hello configure hello nouveau groupe de disponibilité. Bonjour **progression** page, vous pouvez cliquer sur **plus de détails** tooview hello détaillées de progression. Une fois l’Assistant de hello est terminé, vérifiez que hello **résultats** tooverify page qui hello du groupe de disponibilité est créé avec succès.

     ![Assistant Nouveau groupe de disponibilité, résultats](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Cliquez sur **fermer** Assistant de hello tooexit.

### <a name="check-hello-availability-group"></a>Hello de vérification de groupe de disponibilité

1. Dans l’**Explorateur d’objets**, développez **Haute disponibilité AlwaysOn**, puis **Groupes de disponibilité**. Vous devez maintenant voir hello du nouveau groupe de disponibilité de ce conteneur. Avec le bouton droit hello groupe de disponibilité, puis cliquez sur **afficher le tableau de bord**.

   ![Afficher le tableau de bord de groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   Votre **tableau de bord AlwaysOn** doit ressembler toothis similaire.

   ![Tableau de bord de groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Vous pouvez voir les réplicas hello, le mode de basculement hello de chaque état de synchronisation de réplica et hello.

2. Dans le **Gestionnaire du cluster de basculement**, cliquez sur votre cluster. Sélectionnez **Rôles**. nom de groupe de disponibilité de Hello utilisé est un rôle sur le cluster de hello. Ce groupe de disponibilité n’a pas une adresse IP pour les connexions clientes, car vous n’avez pas configuré d’écouteur. Vous allez configurer le port d’écoute hello après avoir créé un équilibrage de charge Azure.

   ![Groupe de disponibilité dans le Gestionnaire du cluster de basculement](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > N’essayez pas de toofail sur hello groupe de disponibilité à partir de hello Gestionnaire du Cluster de basculement. Vous devez effectuer toutes les opérations de basculement à partir du **tableau de bord AlwaysOn** dans SSMS. Pour plus d’informations, consultez [Restrictions d’utilisation hello Gestionnaire du Cluster de basculement avec des groupes de disponibilité](https://msdn.microsoft.com/library/ff929171.aspx).
    >

À ce stade, vous avez un groupe de disponibilité avec des réplicas sur les deux instances de SQL Server. Vous pouvez déplacer hello groupe de disponibilité entre des instances. Connexion impossible toohello groupe de disponibilité encore car vous ne disposez pas d’un écouteur. Dans Azure virtual machines, port d’écoute hello requiert un équilibrage de charge. étape suivante de Hello est un équilibreur de charge toocreate hello dans Azure.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Crée un équilibrage de charge Azure

Sur les machines virtuelles Azure, un groupe de disponibilité SQL Serveur requiert un équilibrage de charge. équilibrage de charge Hello conserve adresse hello pour l’écouteur de groupe de disponibilité hello. Cette section résume comment toocreate hello l’équilibrage de charge Bonjour portail Azure.

1. Bonjour portail Azure, accédez à toohello groupe de ressources où vos serveurs SQL sont et cliquez sur **+ ajouter**.
2. Recherchez **Équilibrage de charge**. Choisissez l’équilibrage de charge hello publié par Microsoft.

   ![Groupe de disponibilité dans le Gestionnaire du cluster de basculement](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  Cliquez sur **Créer**.
3. Configurer hello suivant les paramètres d’équilibrage de charge hello.

   | Paramètre | Champ |
   | --- | --- |
   | **Name** |Utiliser un nom pour l’équilibrage de charge hello, par exemple **sqlLB**. |
   | **Type** |Interne |
   | **Réseau virtuel** |Utiliser le nom hello Hello réseau virtuel Azure. |
   | **Sous-réseau** |Utiliser le nom hello de sous-réseau hello hello d’ordinateur virtuel est dans.  |
   | **Affectation d’adresses IP** |Statique |
   | **Adresse IP** |Utilisez une adresse disponible du sous-réseau. |
   | **Abonnement** |Utilisez hello même abonnement que l’ordinateur virtuel de hello. |
   | **Emplacement** |Utilisez hello même emplacement que l’ordinateur virtuel de hello. |

   Hello panneau portail Azure doit ressembler à ceci :

   ![Créer un équilibreur de charge](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Cliquez sur **créer**, équilibrage de charge toocreate hello.

équilibrage de charge tooconfigure hello, vous devez toocreate un pool principal, une sonde, ensemble hello équilibrage de charge et les règles. Procédez comme suit dans hello portail Azure.

### <a name="add-backend-pool"></a>Ajouter le pool principal

1. Bonjour portail Azure, accédez à tooyour le groupe de disponibilité. Vous devrez peut-être l’équilibrage de charge toorefresh hello vue toosee hello nouvellement créé.

   ![Rechercher l’équilibrage de charge dans le groupe de ressources](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Sur l’équilibrage de charge hello, cliquez sur **pools principaux**, puis cliquez sur **+ ajouter**. Définissez le pool principal d’hello comme suit :

   | Paramètre | Description | Exemple
   | --- | --- |---
   | **Nom** | Tapez un nom. | SQLLBBE
   | **Associé à** | Choisir dans la liste | Groupe à haute disponibilité
   | **Groupe à haute disponibilité** | Utilisez un nom de groupe à haute disponibilité hello situés dans vos machines virtuelles SQL Server | sqlAvailabilitySet |
   | **Machines virtuelles** |Hello deux noms de machine virtuelle Azure SQL Server | sqlserver-0, sqlserver-1

1. Nom de type hello pour le pool de back-end hello.

1. Cliquez sur **+ Ajouter une machine virtuelle**.

1. Pour l’ensemble de disponibilité hello, choisissez hello haute disponibilité que hello sont des serveurs SQL Server dans.

1. Pour les ordinateurs virtuels, vous pouvez inclure les deux hello serveurs SQL Server. N’incluez pas de serveur témoin de partage de fichier hello.

1. Cliquez sur **OK** pool principal de toocreate hello.

### <a name="set-hello-probe"></a>Sonde de hello ensemble

1. Sur l’équilibrage de charge hello, cliquez sur **sondes d’intégrité**, puis cliquez sur **+ ajouter**.

1. Définir la détection de l’intégrité de hello comme suit :

   | Paramètre | Description | Exemple
   | --- | --- |---
   | **Nom** | Texte | SQLAlwaysOnEndPointProbe |
   | **Protocole** | Choisissez TCP. | TCP |
   | **Port** | Tout port inutilisé. | 59999 |
   | **Intervalle**  | Durée Hello entre sonde tentatives en secondes |5 |
   | **Seuil de défaillance sur le plan de l’intégrité** | nombre d’échecs de sonde consécutifs devant se produire pour une toobe de machine virtuelle considéré comme non intègre de Hello  | 2 |

1. Cliquez sur **OK** sonde d’intégrité tooset hello.

### <a name="set-hello-load-balancing-rules"></a>Définir des règles d’équilibrage de charge de hello

1. Sur l’équilibrage de charge hello, cliquez sur **règles d’équilibrage de charge**, puis cliquez sur **+ ajouter**.

1. Définissez comme suit les règles d’équilibrage de charge hello.
   | Paramètre | Description | Exemple
   | --- | --- |---
   | **Nom** | Texte | SQLAlwaysOnEndPointListener |
   | **Frontend IP address (Adresse IP frontale)** | Choisissez une adresse. |Utiliser une adresse hello que vous avez créé lorsque vous avez créé l’équilibrage de charge hello. |
   | **Protocole** | Choisissez TCP. |TCP |
   | **Port** | Utiliser le port de hello pour l’instance de SQL Server hello | 1433 |
   | **Port principal** | Ce champ est inutilisé lorsque l’option IP flottante est définie pour Retour au serveur direct. | 1433 |
   | **Sonde** |nom Hello spécifié pour la sonde de hello | SQLAlwaysOnEndPointProbe |
   | **Persistance de session** | Liste déroulante | **Aucun** |
   | **Délai d’inactivité** | Tookeep minutes d’ouvrir une connexion TCP | 4 |
   | **Adresse IP flottante (retour serveur direct)** | |Activé |

   > [!WARNING]
   > Le retour au serveur direct est configuré lors de la création. Cette valeur n’est pas modifiable.

1. Cliquez sur **OK** tooset hello équilibrage de la charge des règles.

## <a name="configure-listener"></a>Configurer le port d’écoute hello

Hello suivant chose toodo est tooconfigure un écouteur de groupe de disponibilité sur un cluster de basculement hello.

> [!NOTE]
> Ce didacticiel montre comment la corriger toocreate un seul écouteur - avec une adresse IP ILB. un ou plusieurs écouteurs à l’aide d’une ou plusieurs adresses IP, reportez-vous à toocreate [écouteur de créer un groupe de disponibilité et équilibrage de charge | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Configurer le port d’écoute

Dans SQL Server Management Studio, définissez le port d’écoute hello.

1. Lancez SQL Server Management Studio et connectez-vous toohello le réplica principal.

1. Accédez trop**haute disponibilité AlwaysOn** | **groupes de disponibilité** | **écouteurs de groupe de disponibilité**.

1. Vous devez maintenant voir le nom de l’écouteur hello que vous avez créé dans le Gestionnaire de Cluster de basculement. Cliquez sur le nom d’écouteur hello et cliquez sur **propriétés**.

1. Bonjour **Port** , spécifiez le numéro de port hello pour l’écouteur de groupe de disponibilité hello à l’aide de hello $EndpointPort utilisé précédemment (1433 était la valeur par défaut hello), puis cliquez sur **OK**.

Vous avez maintenant un groupe de disponibilité SQL Server dans des machines virtuelles Azure exécutées en mode Resource Manager.

## <a name="test-connection-toolistener"></a>Toolistener de connexion de test

connexion de hello tootest :

1. RDP tooa SQL Server qui se trouve dans hello virtuel même réseau, mais ne pas les réplicas hello propre. Vous pouvez utiliser hello autre serveur SQL Server dans un cluster de hello.

1. Utilisez **sqlcmd** connexion de hello tootest utilitaire. Par exemple, hello script suivant établit une **sqlcmd** réplica principal de connexion toohello via écouteur hello avec l’authentification Windows :

    ```
    sqlcmd -S <listenerName> -E
    ```

    Si l’écouteur de hello utilise un port autre que hello par défaut du port (1433), spécifiez le port de hello dans la chaîne de connexion hello. Par exemple, hello commande sqlcmd suivante établit une connexion écouteur tooa sur le port 1435 :

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Hello connexion de SQLCMD connecte automatiquement à instance toowhichever de SQL Server héberge hello le réplica principal.

> [!TIP]
> Assurez-vous que port hello que vous spécifiez est ouvert sur le pare-feu hello des deux serveurs SQL. Les deux serveurs requièrent une règle de trafic entrant pour hello le port TCP que vous utilisez. Pour plus d’informations, consultez [Ajouter ou modifier une règle de pare-feu](http://technet.microsoft.com/library/cc753558.aspx).
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Étapes suivantes

- [Ajouter un équilibrage de charge de tooa d’adresse IP pour un deuxième groupe de disponibilité](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
