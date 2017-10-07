---
title: "outil aaaRun hello Hyper-V capacity planner pour la récupération de Site | Documents Microsoft"
description: "Cet article décrit comment toorun hello outil Hyper-V capacity planner pour Azure Site Recovery"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>Exécuter l’outil de planification de capacité hello Hyper-V pour la récupération de Site

Dans le cadre de votre déploiement d’Azure Site Recovery, vous devez toofigure votre réplication et les besoins en bande passante. outil Hello Hyper-V capacity planner pour la récupération de Site vous aide à vous toodo, pour la réplication d’ordinateur virtuel Hyper-V.

Cet article décrit comment toorun hello outil de planification de capacité Hyper-V. Cet outil doit être utilisé avec les informations de hello dans [planification des capacités pour la récupération de Site](site-recovery-capacity-planner.md).

## <a name="before-you-start"></a>Avant de commencer
Vous exécutez l’outil de hello sur un nœud de serveur ou un cluster Hyper-V dans votre site principal. serveurs Hyper-V toorun hello outil hello doit :

* Système d’exploitation : Windows Server 2012 ou 2012 R2
* Mémoire : 20 Mo (minimum)
* Processeur : surcharge de 5 pour cent (minimum)
* Espace disque : 5 Mo (minimum)

Avant d’exécuter les outil hello, vous devez le site principal de tooprepare hello. Si vous effectuez une réplication entre deux sites locaux vous souhaitez la bande passante toocheck, vous devez tooprepare également un serveur de réplication.

## <a name="step-1-prepare-hello-primary-site"></a>Étape 1 : Préparer le site principal de hello

1. Sur le site principal de hello, dressez la liste des toutes hello machines virtuelles de Hyper-V vous souhaitez tooreplicate et Hyper-V hello hôtes/clusters sur lequel ils se trouvent. outil de Hello peut exécuter pour plusieurs hôtes autonomes, ou pour un seul cluster, mais pas les deux ensemble. Il doit également toorun séparément pour chaque système d’exploitation, donc vous devez rassembler des informations sur les serveurs Hyper-V comme suit :

   * Serveurs autonomes Windows Server 2012
   * Clusters Windows Server 2012
   * Serveurs autonomes Windows Server 2012 R2
   * Clusters Windows Server 2012 R2
2. Activer tooWMI l’accès à distance sur tous les ordinateurs hôtes Hyper-V de hello et les clusters. Exécuter cette commande sur chaque serveur/cluster, les règles de pare-feu que toomake et les autorisations utilisateur sont définies :

        netsh firewall set service RemoteAdmin enable
3. Activez l’analyse des performances sur les serveurs et les clusters comme suit :

   * Hello ouvrir le pare-feu Windows avec hello **fonctions avancées de sécurité** composant logiciel enfichable, et puis suivant de hello activer les règles de trafic entrant : **accès réseau COM + (DCOM-IN)** et toutes les règles de hello **journal des événements à distance Groupe d’administration**.

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>Étape 2 : Préparer un serveur de réplication (réplication de site tooon local)
Vous n’avez pas besoin toodo cela si vous effectuez une réplication tooAzure.

Nous vous recommandons de configurer un seul hôte Hyper-V en tant qu’un serveur de récupération, afin qu’une machine virtuelle factice peut être répliquées tooit toocheck passante.  Vous pouvez ignorer cette étape, mais vous ne serez pas la bande passante en mesure de toomeasure sauf si vous le faites.

1. Si vous voulez toouse un nœud de cluster en tant que réplica du hello configurer service broker de réplication de Hyper-V :

   * Dans le **Gestionnaire de serveur**, ouvrez **Gestionnaire du cluster de basculement**.
   * Se connecter toohello cluster, mettez en surbrillance le nom du cluster hello et cliquez sur **Actions** > **configurer un rôle** Assistant de haute disponibilité tooopen hello.
   * Dans **Sélectionner un rôle** cliquez sur **Service Broker de réplication Hyper-V**. Dans l’Assistant de hello fournissent un **nom NetBIOS** et hello **adresse IP** toobe utilisé en tant que cluster de toohello de point de connexion hello (appelé point d’accès client). Hello **Service Broker de réplication Hyper-V** configuré, ce qui entraîne un nom de point d’accès client que vous devez noter.
   * Vérifiez le rôle Hyper-V Replica Broker hello est mis en ligne et peut basculer entre tous les nœuds du cluster de hello. toodo, cliquez avec le bouton droit sur le rôle hello, pointez trop**déplacer**, puis cliquez sur **sélectionner un nœud**. Sélectionner un nœud > **OK**.
   * Si vous utilisez l’authentification basée sur certificat, assurez-vous que chaque nœud de cluster et point d’accès client hello tous les hello certificat installé.
2. Activez un serveur réplica :

   * Pour un cluster, ouvrez Gestionnaire du Cluster de défaillance, connectez toohello cluster et cliquez sur **rôles** > Sélectionner un rôle > **les paramètres de réplication** > **activer ce cluster comme un réplica serveur**. Si vous utilisez un cluster en tant que réplica de hello, vous avez besoin de rôle de service Broker de réplication Hyper-V toohave hello présent dans le cluster de hello en hello principal site.
   * Pour un serveur autonome, ouvrez le Gestionnaire Hyper-V. Bonjour **Actions** volet, cliquez sur **paramètres Hyper-V** pour hello serveur vous souhaitez tooenable et dans **Configuration de la réplication** cliquez sur **activer cette option l’ordinateur comme serveur de réplication**.
3. Configurez l’authentification :

   * Dans **authentification et ports**, sélectionnez la façon dont tooauthenticate hello serveur principal, ainsi que les ports d’authentification hello. Si vous utilisez un certificat, cliquez sur **sélectionner un certificat** tooselect une. Utiliser Kerberos si hôtes de Hyper-V principal et de récupération hello hello même domaine, ou dans des domaines approuvés. Utilisez des certificats pour des domaines différents ou pour un déploiement de groupe de travail.
   * Dans **autorisation et stockage**, autoriser **tout** authentifié le serveur de réplication toothis de données de serveur (principal) toosend la réplication.

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * Exécutez **netsh http show servicestate**, toocheck cet écouteur hello est en cours d’exécution pour hello protocole/port spécifié :  
4. Configurez des pare-feu. Pendant l’installation d’Hyper-V, les règles de pare-feu sont créées tooallow trafic sur les ports par défaut hello (HTTPS sur le port 443, Kerberos sur 80). Activez ces règles comme suit :
  - Authentification de certificat sur le cluster (443) : ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - Authentification Kerberos sur le cluster (80) : ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - Authentification de certificat sur le serveur autonome : ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - Authentification Kerberos sur le serveur autonome : ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>Étape 3 : Exécuter l’outil de planification de capacité hello
Une fois que vous avez préparé votre site principal, et configurer un serveur de récupération, vous pouvez exécuter l’outil de hello.

1. [Télécharger](https://www.microsoft.com/download/details.aspx?id=39057) outil hello hello Microsoft Download Center.
2. Exécutez l’outil hello à partir d’un des serveurs principaux de hello (ou un des nœuds hello cluster principal de hello). Cliquez sur le fichier .exe de hello, puis choisissez **exécuter en tant qu’administrateur**.
3. Dans **avant de commencer**, spécifiez la durée pendant laquelle vous voulez toocollect données. Nous vous recommandons de qu'exécuter les outil hello pendant tooensure d’heures de production que les données sont représentatives. Si vous essayez uniquement la connectivité de réseau toovalidate, vous pouvez collecter pour seulement une minute.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. Dans **les détails du site principal**, spécifiez le nom du serveur hello ou nom de domaine complet pour un ordinateur hôte autonome, ou pour un cluster spécifiez hello nom de domaine complet du client de hello accepter n’importe quel nœud dans le cluster de hello, nom du cluster ou point puis cliquez sur **suivant**. outil de Hello détecte automatiquement le nom hello du serveur hello sur qu'elle s’exécute. machines virtuelles qui peuvent être analysés Hello outil récupère hello serveurs spécifiés.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. Dans **détails du réplica de Site**si vous effectuez une réplication tooAzure, ou si vous effectuez une réplication tooa de centre de données secondaire et que vous n’avez pas défini un serveur réplica, sélectionnez **ignorer les tests impliquant le site de réplication**. Si vous répliquez tooa de centre de données secondaire et que vous avez configuré un type de réplica, entrez nom de domaine complet d’un serveur autonome hello ou point d’accès client hello pour le cluster de hello, dans **serveur nom (ou) Hyper-V réplica Broker CAP**.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. Dans **détails du réplica étendu**, activer **site de réplica étendu qui impliquent des tests hello de Skip**. Ces tests ne sont pas pris en charge par Site Recovery.
7. Dans **choisir les machines virtuelles tooReplicate**, les outils de hello se connecte toohello serveur ou un cluster et affiche les machines virtuelles et disques en cours d’exécution sur le serveur principal de hello, conformément aux paramètres de hello vous avez spécifié sur hello **les détails du Site principal**  page. Les machines virtuelles déjà activées pour la réplication ou qui ne sont pas en cours d’exécution ne s’affichent pas. Sélectionnez les machines virtuelles de hello pour lequel vous souhaitez toocollect métriques. Sélection automatique des disques durs virtuels hello collecte des données pour les machines virtuelles de hello trop.
8. Si vous avez configuré un serveur de réplication ou un cluster, dans **informations réseau**, spécifier hello approximative la bande passante WAN vous pensez à utiliser entre les sites principal et de réplica hello et les certificats de hello Sélectionnez si vous avez configuré authentification par certificat.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. Dans **Résumé**, vérifiez les paramètres de hello et cliquez sur **suivant** toobegin collecte des métriques. Progression de l’outil et l’état est affiché sur hello **calculer la capacité** page. Lorsque l’outil de hello a terminé son exécution, cliquez sur **afficher le rapport** sortie de hello tooview. Par défaut, les rapports et les journaux sont stockés dans **%systemdrive%\Utilisateurs\Public\Documents\Capacity Planner**.

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>Étape 4 : Interpréter les résultats de hello

Voici les métriques importantes hello. Vous pouvez ignorer celles qui n’y sont pas mentionnées. Elles n’ont aucune utilité pour Site Recovery.

### <a name="on-premises-tooon-premises-replication"></a>La réplication intersite tooon local

* Impact de la réplication sur le calcul de l’hôte principal hello, mémoire
* Impact de la réplication sur hello principal, espace disque de stockage d’ordinateurs hôtes de récupération, e/s
* Bande passante totale requise pour la réplication delta (Mbits/s)
* Bande passante réseau observé entre l’hôte principal hello et l’hôte de récupération hello (Mbps)
* Suggestion pour nombre idéal de hello de transferts parallèles actifs entre deux hôtes/clusters de hello

### <a name="on-premises-tooazure-replication"></a>Réplication locale tooAzure

* Impact de la réplication sur le calcul de l’hôte principal hello, mémoire
* Impact de la réplication sur l’espace disque de stockage de l’hôte principal hello, e/s
* Bande passante totale requise pour la réplication delta (Mbits/s)

## <a name="more-resources"></a>Autres ressources
* Pour obtenir des informations détaillées sur l’outil de hello, lisez le document hello qui accompagne le téléchargement de l’outil hello.
* Regarder une procédure pas à pas d’outil hello sur de Keith Mayer [blog TechNet](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx).
* [Obtenir des résultats hello](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) nos tests de performances pour la réplication Hyper-V sur site local tooon

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez terminé la planification de la capacité, vous pouvez commencer à déployer Site Recovery :

* [Répliquer des ordinateurs virtuels Hyper-V dans VMM clouds tooAzure](site-recovery-vmm-to-azure.md)
* [Répliquer des ordinateurs virtuels Hyper-V (sans VMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Répliquer des machines virtuelles Hyper-V entre des sites VMM](site-recovery-vmm-to-vmm.md)
