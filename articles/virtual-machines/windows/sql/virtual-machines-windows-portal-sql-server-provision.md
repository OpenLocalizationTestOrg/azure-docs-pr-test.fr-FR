---
title: aaaProvision une Machine virtuelle de SQL Server | Documents Microsoft
description: "Créer et connecter l’ordinateur de virtuel tooa SQL Server dans Azure à l’aide du portail de hello. Ce didacticiel utilise le mode de gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Configurer un ordinateur virtuel de SQL Server dans hello portail Azure
> [!div class="op_single_selector"]
> * [Portail](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

Ce didacticiel de bout en bout vous montre comment toouse hello tooprovision portail Azure, une machine virtuelle exécutant SQL Server.

Galerie de machine virtuelle Azure (VM) Hello inclut plusieurs images qui contiennent Microsoft SQL Server. En quelques clics, vous pouvez sélectionner une des hello que SQL VM images à partir de la galerie de hello et configurer dans votre environnement Azure.

Ce didacticiel présente les procédures suivantes :

* [Sélectionnez une image de SQL VM à partir de la galerie de hello](#select-a-sql-vm-image-from-the-gallery)
* [Configurez et créez hello machine virtuelle](#configure-the-vm)
* [Ouvrez hello machine virtuelle avec le Bureau à distance](#open-the-vm-with-remote-desktop)
* [Se connecter tooSQL serveur à distance](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Sélectionnez une image de SQL VM à partir de la galerie de hello

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) à l’aide de votre compte.

   > [!NOTE]
   > Si vous n'avez pas de compte Azure, visitez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).

2. Dans hello portail Azure, cliquez sur **nouveau**. portail de Hello ouvre hello **nouveau** fenêtre.

3. Bonjour **nouveau** fenêtre, cliquez sur **de calcul** puis cliquez sur **afficher tous les**.

   ![Fenêtre Nouveau calcul](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. Dans le champ de recherche de hello, tapez **SQL Server**, puis appuyez sur ENTRÉE.

5. Puis cliquez sur hello **filtre** icône, sélectionnez **Microsoft** pour le serveur de publication hello. Cliquez sur **fait** sur les résultats de hello hello filtre fenêtre toofilter tooMicrosoft publié des images de SQL Server.

   ![Fenêtre Machines virtuelles Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Passez en revue les images SQL Server disponibles hello. Chaque image identifie une version de SQL Server et un système d’exploitation.

6. Image hello sélectionnez nommée **licence gratuite : développeur de SQL Server 2016 SP1 sur Windows Server 2016**.

   > [!TIP]
   > édition développeur de Hello est utilisée dans ce didacticiel, car il s’agit d’une version complète de SQL Server qui est disponible pour le développement à des fins de test. Vous payez uniquement pour les coûts hello de hello machine virtuelle en cours d’exécution. Toutefois, vous êtes libre toochoose des toouse d’images hello dans ce didacticiel.

   > [!TIP]
   > Images SQL VM comprennent les coûts de licence hello pour SQL Server dans hello par minute tarification Hello machine virtuelle que vous créez (à l’exception des éditions développeur et Express de hello). SQL Server Developer est gratuit pour le développement/les tests (hors production) et SQL Express est gratuit pour les charges légères (moins de 1 Go de mémoire, moins de 10 Go de stockage). Il existe une autre option toobring-your-propriétaire-licence (BYOL) et paie uniquement pour hello machine virtuelle. Ces noms d’images sont préfixés avec {BYOL}. 
   >
   > Pour en savoir plus sur ces options, consultez l’article [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Tarification des machines virtuelles SQL Server Azure).

7. Sous **Sélectionner un modèle de déploiement**, vérifiez que **Resource Manager** est sélectionné. Le Gestionnaire de ressources est hello recommandé de modèle de déploiement pour les nouveaux ordinateurs virtuels. 

8. Cliquez sur **Créer**.

    ![Créer une machine virtuelle avec Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Configurer hello machine virtuelle
Il existe cinq fenêtres de configuration d’une machine virtuelle SQL Server.

| Étape | Description |
| --- | --- |
| **Concepts de base** |[Configurer les paramètres de base](#1-configure-basic-settings) |
| **Taille** |[Choisir la taille de machine virtuelle](#2-choose-virtual-machine-size) |
| **Paramètres** |[Configurer des fonctionnalités facultatives](#3-configure-optional-features) |
| **Paramètres de SQL Server** |[Configurer les paramètres du serveur SQL](#4-configure-sql-server-settings) |
| **Résumé** |[Hello révision résumé](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Configurer les paramètres de base

Sur hello **notions de base** fenêtre, fournir hello informations suivantes :

* Entrez un **nom**de machine virtuelle unique.

* Pour optimiser les performances, sélectionnez **SSD** comme type de disque de machine virtuelle.

* Spécifiez un **nom d’utilisateur** pour le compte d’administrateur local hello sur hello machine virtuelle. Ce compte est également ajouté toohello SQL Server **sysadmin** rôle serveur fixe.

* Utilisez un **mot de passe**fort.

* Si vous avez plusieurs abonnements, vérifiez que l’abonnement de hello est correcte pour hello nouvelle machine virtuelle.

* Bonjour **groupe de ressources** , tapez un nom pour un groupe de ressources. Également cliquer toouse sur un groupe de ressources existant **existant**. Un groupe de ressources est une collection de ressources liées dans Azure (machines virtuelles, comptes de stockage, réseaux virtuels, etc.).

  > [!NOTE]
  > L’utilisation d’un nouveau groupe de ressources est utile si vous testez ou découvrez les déploiements SQL Server dans Azure. Une fois que vous avez terminé avec votre test, supprimez tooautomatically delete hello VM hello ressource groupe et toutes les ressources associées à ce groupe de ressources. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).

* Sélectionnez un **emplacement** pour hello région Azure qui hébergera ce déploiement.

* Cliquez sur **OK** toosave les paramètres hello.

    ![Fenêtre SQL Basics (Informations de base SQL)](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. Choisir la taille de machine virtuelle

Sur hello **taille** étape, choisissez une taille de machine virtuelle Bonjour **choisir une taille** fenêtre. fenêtre Hello affiche initialement les tailles recommandées en fonction de l’image hello sélectionnée.

> [!IMPORTANT]
> Hello estimation du coût mensuel affiché sur hello **choisir une taille** fenêtre n’inclut pas les coûts des licences de SQL Server. Il s’agit de coût hello Hello machine virtuelle autonome. Pour les éditions Express et Developer hello de SQL Server, il s’agit de coût estimé de hello total. Pour les autres éditions, consultez hello [page de tarification des Machines virtuelles Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) et sélectionnez votre édition de la cible de SQL Server. Voir aussi hello [tarification des conseils pour les machines virtuelles Azure de SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

![Options de taille de machine virtuelle SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Pour les charges de production, consultez hello recommandé de tailles d’ordinateur et la configuration dans [performances meilleures pratiques pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-performance.md). Si vous avez besoin d’une taille de l’ordinateur qui n’est pas répertoriée, cliquez sur hello **afficher toutes les** bouton.

> [!NOTE]
> Pour plus d’informations sur les tailles de machines virtuelles, voir [Tailles des machines virtuelles](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Choisissez la taille de votre machine, puis cliquez sur **Sélectionner**.

## <a name="3-configure-optional-features"></a>3. Configurer des fonctionnalités facultatives

Sur hello **paramètres** fenêtre, configurer le stockage Azure, de mise en réseau et la surveillance pour la machine virtuelle de hello.

* Dans la section **Stockage**, sélectionnez **Oui** sous **Utiliser Managed Disks**.

   > [!NOTE]
   > Microsoft recommande Managed Disks pour SQL Server. Géré gère le stockage des disques coulisses hello. En outre, lorsque les ordinateurs virtuels avec des disques gérés sont hello même ensemble de disponibilité, Azure distribue hello ressources tooprovide approprié une redondance de stockage. Pour plus d’informations, voir la page [Azure Managed Disks overview](../../../storage/storage-managed-disks-overview.md) (Vue d’ensemble d’Azure Managed Disks). Pour plus de détails sur les disques gérés dans un groupe à haute disponibilité, consultez l’article [Utilisation de disques gérés pour les machines virtuelles dans le groupe à haute disponibilité](../manage-availability.md).

* Sous **réseau**, vous pouvez accepter les valeurs hello rempli automatiquement. Vous pouvez également cliquer sur chaque fonctionnalité toomanually configurer hello **réseau virtuel**, **sous-réseau**, **adresse IP publique**, et **dugroupedesécuritéréseau**. À des fins hello de ce didacticiel, conserver les valeurs par défaut hello.

* Azure active **analyse** par défaut avec hello même compte de stockage désigné pour hello machine virtuelle. Vous pouvez modifier ces paramètres ici.

* Sous **à haute disponibilité**, vous pouvez laisser la valeur par défaut est hello **aucun** pour ce didacticiel. Si vous envisagez de tooset des groupes de disponibilité AlwaysOn SQL, configurer hello disponibilité tooavoid recréation hello virtual machine.  Pour plus d’informations, consultez [gérer hello disponibilité des Machines virtuelles](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Une fois que vous avez terminé la configuration des paramètres, cliquez sur **OK**.

## <a name="4-configure-sql-server-settings"></a>4. Configurer les paramètres du serveur SQL
Sur hello **paramètres SQL Server** fenêtre, configurer des paramètres spécifiques et des optimisations pour SQL Server. paramètres Hello que vous pouvez configurer pour SQL Server suivants hello.

| Paramètre |
| --- |
| [Connectivité](#connectivity) |
| [Authentification](#authentication) |
| [Configuration du stockage](#storage-configuration) |
| [Mise à jour corrective automatisée](#automated-patching) |
| [Sauvegarde automatisée](#automated-backup) |
| [Intégration du coffre de clés Azure](#azure-key-vault-integration) |
| [R Services](#r-services) |

### <a name="connectivity"></a>Connectivité

Sous **connectivité SQL**, spécifiez le type de hello d’accès souhaité toohello instance de SQL Server sur cet ordinateur virtuel. Pour des raisons de hello de ce didacticiel, sélectionnez **Public (internet)** tooallow connexions tooSQL Server à partir d’ordinateurs ou des services sur hello internet. Avec cette option est sélectionnée, Azure configure automatiquement le pare-feu hello et hello sécurité groupe tooallow le trafic sur le port 1433.

![Options de connectivité SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> Par défaut, SQL Server écoute un port bien connu, le port **1433**. Pour une sécurité accrue, modifiez le port hello dans hello toolisten de boîte de dialogue précédente sur un port non défini par défaut, tels que 1401. Si vous effectuez cette opération, vous devez vous connecter à l’aide de ce port à partir de tous les outils clients, tels que SSMS.

tooconnect tooSQL Server via hello internet, vous devez également autoriser l’authentification SQL Server, qui est décrit dans la section suivante de hello.

Si vous préférez toonot activer les connexions toohello du moteur de base de données via internet de hello, choisissez une des options suivantes de hello :

* **Local (à l’intérieur de la machine virtuelle uniquement)** tooallow connexions tooSQL serveur uniquement à partir de hello machine virtuelle.
* **Privé (dans le réseau virtuel)** tooallow connexions tooSQL Server à partir d’ordinateurs ou des services Bonjour même réseau virtuel.

En règle générale, améliorer la sécurité en choisissant la connectivité de la plus restrictive hello qui permet à votre scénario. Mais toutes les options de hello sont sécurisables via les règles du groupe de sécurité réseau et de l’authentification Windows/SQL. Vous pouvez modifier le groupe de sécurité réseau après hello que machine virtuelle est créée. Pour plus d’informations, consultez [Considérations relatives à la sécurité de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-security.md).

> [!NOTE]
> image de machine virtuelle Hello pour SQL Server Express edition n’active pas automatiquement le protocole de hello TCP/IP. Cela est vrai même pour hello connectivité publics et privés options. Pour l’édition Express, vous devez utiliser le Gestionnaire de Configuration SQL Server trop[activer manuellement le protocole de hello TCP/IP](#configure-sql-server-to-listen-on-the-tcp-protocol) après la création d’hello machine virtuelle.

### <a name="authentication"></a>Authentification

Si vous avez besoin de l’authentification SQL Server, cliquez sur **Activer** under **Authentification SQL**.

![l’authentification SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Si vous envisagez de tooaccess SQL Server sur hello internet (autrement dit, hello des options de connectivité Public), vous devez activer l’authentification SQL ici. Accès public toohello SQL Server nécessite l’utilisation de hello de l’authentification SQL.
> 
> 

Si vous activez l’authentification SQL Server, spécifiez un **nom de connexion** et un **mot de passe**. Ce nom d’utilisateur est configuré en tant que compte de connexion de l’authentification SQL Server et membre de hello **sysadmin** rôle serveur fixe. Pour plus d’informations sur les modes d’authentification, consultez [Choisir un mode d’authentification](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) .

Si vous n’activez pas l’authentification SQL Server, vous pouvez utiliser compte d’administrateur local hello sur l’instance de SQL Server hello VM tooconnect toohello.

### <a name="storage-configuration"></a>Configuration du stockage

Cliquez sur **configuration du stockage** besoins en stockage toospecify hello.

![Configuration du stockage SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Si vous avez configuré manuellement votre stockage standard toouse de machine virtuelle, cette option n’est pas disponible. L’optimisation du stockage automatique est disponible uniquement pour Premium Storage.

> [!TIP]
> nombre de Hello de s’arrête et des limites supérieures de hello de chaque curseur sont dépendantes de la taille hello de machine virtuelle que vous avez sélectionné. Une machine virtuelle le plus grande et plus puissante est en mesure de tooscale plus haut.

Vous pouvez spécifier des exigences comme les opérations d’entrée/sortie par seconde (E/S par seconde), le débit en Mbit/s et la taille totale de stockage. Configurez ces valeurs à l’aide des échelles décalé hello. Vous pouvez modifier ces paramètres de stockage en fonction de la charge de travail. portail de Hello calcule automatiquement hello du nombre de disques tooattach et le configurer en fonction de ces exigences.

Sous **stockage optimisé pour**, sélectionnez une des options suivantes de hello :

* **Général** est le paramètre par défaut de hello et prend en charge la plupart des charges de travail.
* **Transactionnelle** traitement optimise le stockage de hello pour les charges de travail OLTP classique de la base de données.
* **Entreposage des données** optimise le stockage hello pour les charges de travail d’analyse et de création de rapports.

### <a name="automated-patching"></a>Mise à jour corrective automatisée

**Automated patching** est activée par défaut. Mise à jour corrective automatique permet de système d’exploitation Azure tooautomatically correctif SQL Server et hello. Spécifiez un jour de semaine de hello, heure et la durée d’une fenêtre de maintenance. Azure effectue la mise à jour corrective dans cette fenêtre de maintenance. planification de fenêtre de maintenance Hello utilise les paramètres régionaux de machine virtuelle de hello pour le moment. Si vous ne souhaitez pas de système d’exploitation Azure tooautomatically correctif SQL Server et hello, cliquez sur **désactiver**.  

![Mise à jour corrective automatisée SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Pour plus d’informations, consultez [Mise à jour corrective automatisée pour SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Sauvegarde automatisée

Activez les sauvegardes automatiques de base de données pour toutes les bases de données sous **Sauvegarde automatisée**. La sauvegarde automatisée est désactivée par défaut.

Lorsque vous activez la sauvegarde automatisée SQL, vous pouvez configurer suivant de hello :

* Période de rétention (jours) pour les sauvegardes
* Toouse de compte de stockage pour les sauvegardes
* Option de chiffrement et mot de passe pour les sauvegardes
* Sauvegarde des bases de données système
* Configuration de la planification de sauvegarde

utilitaire sauvegarde, cliquez sur tooencrypt hello **activer**. Puis spécifiez hello **mot de passe**. Azure crée un certificat des sauvegardes tooencrypt hello et utilise hello spécifié tooprotect de mot de passe de ce certificat.

![Sauvegarde automatisée SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Pour plus d’informations, voir [Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-automated-backup.md).

### <a name="azure-key-vault-integration"></a>Intégration du coffre de clés Azure

les clés secrètes de sécurité toostore dans Azure pour le chiffrement, cliquez sur **intégration du coffre de clés Azure** et cliquez sur **activer**.

![Intégration du coffre de clés Azure SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Hello tableau suivant répertorie hello paramètres tooconfigure requis Azure Key Vault Integration.

| PARAMÈTRE | Description | EXEMPLE |
| --- | --- | --- |
| **URL du coffre de clés** |emplacement Hello de coffre de clés hello. |https://contosokeyvault.vault.azure.net/ |
| **Nom du principal** |Nom du principal du service Azure Active Directory Ce nom est également référencé tooas hello ID Client. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Secret du principal** |Secret du principal du service Azure Active Directory Ce secret est également référencé tooas hello question secrète du Client. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Nom des informations d’identification** |**Nom d’identification**: AKV Integration crée des informations d’identification dans SQL Server, ce qui permet de hello VM toohave accès toohello coffre de clés. Choisissez un nom pour cette identification. |mycred1 |

Pour plus d’informations, consultez [Configurer l’intégration d’Azure Key Vault pour SQL Server sur des machines virtuelles Azure](virtual-machines-windows-ps-sql-keyvault.md).

### <a name="r-services"></a>R Services

Vous avez hello option tooenable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx). Cela vous permet d’analytique toouse avancé avec SQL Server 2016. Cliquez sur **activer** sur hello **paramètres SQL Server** fenêtre.

> [!NOTE]
> Pour SQL Server 2016 Developer Edition, cette option est correctement désactivée par le portail de hello. Pour l’Édition Développeur, vous devez activer R Services manuellement après avoir créé votre machine virtuelle.

![Activer SQL Server R Services](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

Une fois la configuration des paramètres de SQL Server terminée, cliquez sur **OK**.

## <a name="5-review-hello-summary"></a>5. Hello révision résumé

Sur hello **Résumé** fenêtre, révision hello résumée et cliquez sur **achat** toocreate SQL Server, groupe de ressources et ressources spécifiés pour cet ordinateur virtuel.

Vous pouvez surveiller le déploiement hello de hello portail Azure. Hello **Notifications** bouton haut hello écran hello affiche l’état de base du déploiement de hello.

> [!NOTE]
> tooprovide vous avec une idée sur le déploiement de délai d’attente, j’ai déployé une région est des États-Unis de toohello SQL VM avec les paramètres par défaut. Ce déploiement de test a pris un total de 26 minutes toocomplete. Mais cette durée peut varier en fonction de votre région et des paramètres sélectionnés.

## <a name="open-hello-vm-with-remote-desktop"></a>Ouvrez hello machine virtuelle avec le Bureau à distance

Utilisez hello suivant les étapes tooconnect toohello SQL Server virtuels avec le Bureau à distance :

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Après la connexion de la machine virtuelle de SQL Server toohello, vous pouvez lancer SQL Server Management Studio et se connecter avec l’authentification Windows à l’aide de vos informations d’identification d’administrateur local. Si vous avez activé l’authentification SQL Server, vous pouvez également vous connecter avec l’authentification SQL à l’aide du compte de connexion SQL hello et le mot de passe configurés lors de la configuration.

Machine de toohello accès vous permet de toodirectly modification ordinateur et les paramètres de SQL Server en fonction de vos besoins. Par exemple, vous pourriez configurer les paramètres de pare-feu hello ou modifier les paramètres de configuration de SQL Server.

## <a name="enable-tcpip-for-developer-and-express-editions"></a>Activer TCP/IP pour les éditions Developer et Express

Lors de la configuration d’un nouvel ordinateur virtuel SQL Server, Azure n’active pas automatiquement le protocole TCP/IP hello pour les éditions Express et SQL Server Developer. les étapes de Hello ci-dessous expliquent comment toomanually activer TCP/IP afin de pouvoir vous connecter à distance par adresse IP.

Hello suivant l’utilisation d’étapes **Gestionnaire de Configuration SQL Server** protocole de hello TCP/IP tooenable pour les éditions Express et SQL Server Developer.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a>Se connecter tooSQL serveur à distance

Dans ce didacticiel, nous avons sélectionné **Public** accès pour la machine virtuelle de hello et **l’authentification SQL Server**. Ces connexions de SQL Server tooallow de paramètres configurés automatiquement hello machine virtuelle à partir de n’importe quel client sur hello internet (en supposant qu’ils ont la connexion SQL correcte de hello).

> [!NOTE]
> Si vous n’avez pas sélectionné Public lors de la configuration, vous pouvez modifier vos paramètres de connectivité SQL via le portail de hello après le déploiement. Pour plus d’informations, consultez la page [Modifier vos paramètres de connectivité SQL](virtual-machines-windows-sql-connect.md#change).

Hello les sections suivantes montrent comment instance de SQL Server tooconnect tooyour sur votre machine virtuelle à partir d’un autre ordinateur sur hello internet.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Étapes suivantes

D’autres informations sur l’utilisation de SQL Server dans Azure, consultez [SQL Server sur des Machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md) et hello [Forum aux Questions](virtual-machines-windows-sql-server-iaas-faq.md).
