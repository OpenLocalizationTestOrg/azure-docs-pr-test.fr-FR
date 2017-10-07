---
title: aaaSQL Server Business Intelligence | Documents Microsoft
description: "Cette rubrique utilise les ressources créées avec le modèle de déploiement classique hello et décrit les fonctionnalités de Business Intelligence (BI) hello disponibles pour SQL Server s’exécutant sur Azure des Machines virtuelles (VM)."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>Business Intelligence de SQL Server dans les machines virtuelles Azure
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Galerie de Machine virtuelle Microsoft Azure Hello inclut des images contenant les installations de SQL Server. Hello SQL Server sont des éditions prises en charge dans les images de la galerie hello hello mêmes fichiers d’installation vous pouvez installer des ordinateurs tooon locaux et les ordinateurs virtuels. Cette rubrique résume hello SQL Server Business Intelligence (BI) les fonctionnalités installées sur les images de hello et les étapes de configuration requises après la configuration d’un ordinateur virtuel. Elle décrit également les topologies de déploiement prises en charge pour les fonctionnalités et les bonnes pratiques en matière de Business Intelligence (BI).

## <a name="license-considerations"></a>Remarques sur la licence
Il existe deux façons toolicense SQL Server dans des Machines virtuelles Microsoft Azure :

1. Via les avantages License Mobility inclus dans la Software Assurance. Pour plus d’informations, consultez [License Mobility via Software Assurance sur Azure](https://azure.microsoft.com/pricing/license-mobility/).
2. Payez un tarif horaire pour Azure Virtual Machines avec SQL Server installé. Consultez hello la section « SQL Server » dans [tarification des Machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Pour plus d’informations sur les licences et les tarifs actuellement pratiqués, consultez [FAQ concernant les licences Virtual Machines](https://azure.microsoft.com/pricing/licensing-faq/%20/).

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>Images de SQL Server disponibles dans la galerie de machines virtuelles Azure
Galerie de Machine virtuelle Microsoft Azure Hello inclut plusieurs images qui contiennent Microsoft SQL Server. logiciels Hello installés sur les images de machine virtuelle hello varient en fonction de la version de hello du système d’exploitation de hello et hello de SQL Server. liste Hello des images disponibles dans la galerie de machine virtuelle Azure hello change fréquemment.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Image SQL dans la galerie de machines virtuelles Azure](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Hello script PowerShell suivant retourne la liste hello des images Azure qui contiennent « SQL Server » dans hello ImageName :

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

Pour plus d’informations sur les éditions et les fonctionnalités prises en charge par SQL Server, voir hello :

* [Éditions de SQL Server](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Fonctionnalités prises en charge par les éditions de SQL Server 2016 de hello](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>Fonctionnalités de BI installées sur hello Images de la galerie de Machine virtuelle SQL Server
Hello tableau suivant récapitule les fonctionnalités de Business Intelligence hello installées sur les images de la galerie de Machine virtuelle Microsoft Azure commun hello pour SQL Server :

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| Fonctionnalité BI de SQL Server | Installé sur l’image de la galerie hello | Remarques |
| --- | --- | --- |
| **Mode natif de Reporting Services** |Oui |Installé mais requiert une configuration, y compris les URL du Gestionnaire de rapports hello. Consultez la section de hello [configurer Reporting Services](#configure-reporting-services). |
| **Mode SharePoint de Reporting Services** |Non |Hello image de la galerie de Machine virtuelle Microsoft Azure n’inclut pas SharePoint ou SharePoint les fichiers d’installation. <sup>1</sup> |
| **Mode multidimensionnel et d’exploration de données Analysis Services (OLAP)** |Oui |Instance d’Analysis Services hello installé et configuré en tant que valeur par défaut |
| **Mode tabulaire Analysis Services** |Non |Pris en charge dans les images SQL Server 2012, 2014 et 2016, mais pas installé par défaut. Installez une autre instance d’Analysis Services. Consultez la section de hello installer d’autres Services SQL Server et les fonctionnalités de cette rubrique. |
| **Analysis Services Power Pivot pour SharePoint** |Non |Hello image de la galerie de Machine virtuelle Microsoft Azure n’inclut pas SharePoint ou SharePoint les fichiers d’installation. <sup>1</sup> |

<sup>1</sup> Pour plus d’informations sur SharePoint et les machines virtuelles Azure, consultez [Architectures Microsoft Azure pour SharePoint 2013](https://technet.microsoft.com/library/dn635309.aspx) et [Déploiement de SharePoint dans Microsoft Azure Virtual Machines](https://www.microsoft.com/download/details.aspx?id=34598).

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Exécutez hello suivant tooget de commande PowerShell une liste des services installés qui contiennent « SQL » dans le nom du service hello.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>Instructions générales et meilleures pratiques
* Hello minimale taille recommandée pour un ordinateur virtuel est **A3** lors de l’utilisation de SQL Server Enterprise Edition. Hello **A4** taille de machine virtuelle est recommandée pour les déploiements de SQL Server BI d’Analysis Services et Reporting Services.
  
    Pour plus d’informations sur les tailles de machine virtuelle en cours hello, consultez [tailles de Machine virtuelle pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Une meilleure pratique pour la gestion des disques est toostore données, journal et les fichiers de sauvegarde sur des lecteurs autres que **C**: et **D**:. Par exemple, créez des disques de données **E**: et **F**:.
  
  * lecteur Hello mise en cache de la stratégie pour le lecteur par défaut de hello **C**: n’est pas optimale pour travailler avec des données.
  * Hello **D**: lecteur est un lecteur temporaire qui est utilisé principalement pour le fichier d’échange hello. Hello **D**: n’est pas persistant et n’est pas enregistré dans le stockage blob. Tâches de gestion comme une taille de machine virtuelle toohello modification réinitialiser hello **D**: lecteur. Il est recommandé de trop**pas** utiliser hello **D**: lecteur pour les fichiers de base de données, y compris tempdb.
    
    Pour plus d’informations sur la création et attachement de disques, consultez [comment tooAttach un tooa de disque de données Virtual Machine](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Arrêtez ou désinstallez les services que vous n’envisagez pas de toouse. Par exemple si l’ordinateur virtuel de hello est utilisée uniquement pour Reporting Services, arrêtez ou désinstallez Analysis Services et SQL Server Integration Services. Hello image suivante est un exemple de services hello qui sont démarrés par défaut.
  
    ![Services SQL Server](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > moteur de base de données SQL Server Hello est requis dans les scénarios d’analyse Décisionnelle hello pris en charge. Dans une topologie de machine virtuelle de serveur unique, le moteur de base de données hello est requis toobe en cours d’exécution hello même machine virtuelle.
  
    Pour plus d’informations, voir hello : [désinstaller Reporting Services](https://msdn.microsoft.com/library/hh479745.aspx) et [désinstaller une Instance d’Analysis Services](https://msdn.microsoft.com/library/ms143687.aspx).
* Vérifiez les nouvelles mises à jour importantes sur **Windows Update** . images de Machine virtuelle Microsoft Azure Hello sont souvent actualisées ; Toutefois, les mises à jour importantes peuvent être disponibles à partir de **mise à jour Windows** après la dernière actualisation de l’image de machine virtuelle hello.

## <a name="example-deployment-topologies"></a>Exemples de topologies de déploiement
Hello Voici des exemples de déploiements qui utilisent des Machines virtuelles Microsoft Azure. topologies Hello dans ces diagrammes sont uniquement des topologies possibles de hello que vous pouvez utiliser avec les fonctionnalités BI de SQL Server et des Machines virtuelles Microsoft Azure.

### <a name="single-virtual-machine"></a>Une seule machine virtuelle
Analysis Services, Reporting Services, le moteur de base de données SQL Server et les sources de données sont sur une seule machine virtuelle.

![scénario BI iass avec 1 machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>Deux machines virtuelles
* Analysis Services, Reporting Services et hello du moteur de base de données SQL Server sur un seul ordinateur virtuel. Ce déploiement inclut les bases de données hello.
* Les sources de données sont sur une deuxième machine virtuelle. Hello deuxième machine virtuelle inclut le moteur de base de données SQL Server comme source de données.

![scénario BI iaas avec 2 machines virtuelles](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>Topologie mixte Azure - données sur Base de données SQL Azure
* Analysis Services, Reporting Services et hello du moteur de base de données SQL Server sur un seul ordinateur virtuel. Ce déploiement inclut les bases de données hello.
* La source de données est la Base de données SQL Azure.

![machine virtuelle de scénarios BI iaas et AzureSQL comme source de données](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>Topologie hybride – données locales
* Dans cet exemple de déploiement Analysis Services, Reporting Services et hello du moteur de base de données SQL Server s’exécutent sur un seul ordinateur virtuel. hôtes d’ordinateurs virtuels Hello hello des bases de données. machine virtuelle de Hello est tooan joint à un domaine local via le réseau virtuel Azure ou autre solution de tunneling VPN.
* La source de données est locale.

![machine virtuelle de scénarios BI iaas et sources de données locales](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Configuration du mode natif de Reporting Services
image de la galerie de machine virtuelle Hello pour SQL Server inclut le mode natif de Reporting Services installé, mais le serveur de rapports hello n’est pas configuré. étapes Hello dans cette section configurent le serveur de rapports Reporting Services hello. Pour plus d’informations sur la configuration du mode natif de Reporting Services, consultez la page [Installer le serveur de rapports Reporting Services en mode natif](https://msdn.microsoft.com/library/ms143711.aspx).

> [!NOTE]
> Pour un contenu semblable qui utilise le serveur de rapports de Windows PowerShell scripts tooconfigure hello, consultez [utiliser PowerShell tooCreate un Azure VM avec un serveur en Mode natif rapport](../classic/ps-sql-report.md).

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Se connecter toohello Machine virtuelle et démarrer hello Gestionnaire de Configuration de Reporting Services
Il existe deux flux de travail courants pour la connexion tooan Machine virtuelle Azure :

* tooconnect Bonjour, nom hello de machine virtuelle de hello, puis cliquez sur **connexion**. Une connexion Bureau à distance s’ouvre et nom de l’ordinateur hello est rempli automatiquement.
  
    ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Se connecter toohello virtuels avec une connexion Bureau à distance de Windows. Dans l’interface utilisateur hello du Bureau à distance de hello :
  
  1. Hello de type **nom du service cloud** comme nom d’ordinateur hello.
  2. Tapez le signe deux-points ( :) et hello numéro de port public qui est configuré pour hello TCP bureau point de terminaison distant.
     
      Myservice.cloudapp.net:63133
     
      Pour plus d’informations, consultez [Présentation d’un service cloud](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/).


**Démarrer le Gestionnaire de configuration de Reporting Services**

Dans **Windows Server 2012/2016** :

1. À partir de hello **Démarrer** , tapez **Reporting Services** toosee une liste d’applications.
2. Cliquez avec le bouton droit sur **Gestionnaire de configuration de Reporting Services**, puis cliquez sur **Exécuter en tant qu’administrateur**.

Dans **Windows Server 2008 R2**:

1. Cliquez sur **Démarrer**, puis sur **Tous les programmes**.
2. Cliquez sur **Microsoft SQL Server 2016**.
3. Cliquez sur **Outils de configuration**.
4. Cliquez avec le bouton droit sur **Gestionnaire de configuration de Reporting Services**, puis cliquez sur **Exécuter en tant qu’administrateur**.

Ou :

1. Cliquez sur **Start**.
2. Bonjour **rechercher les programmes et fichiers** type de la boîte de dialogue **reporting services**. Si hello machine virtuelle exécute Windows Server 2012, tapez **reporting services** sur l’écran d’accueil de Windows Server 2012 hello.
3. Cliquez avec le bouton droit sur **Gestionnaire de configuration de Reporting Services**, puis cliquez sur **Exécuter en tant qu’administrateur**.
   
    ![recherche du Gestionnaire de configuration de ssrs](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Configurer Reporting Services
**Compte de service et URL du service Web :**

1. Vérifiez que hello **nom du serveur** est le nom du serveur local hello et cliquez sur **connexion**.
2. Hello Remarque vide **nom de base de données de serveur de rapports**. base de données Hello est créé lors de la fin de la configuration de hello.
3. Vérifiez que hello **état de Report Server** est **démarré**. Si vous souhaitez que le service de hello tooverify dans le Gestionnaire de serveur Windows, le service de hello est hello **SQL Server Reporting Services** Service Windows.
4. Cliquez sur **compte de Service** et modifiez le compte de hello en fonction des besoins. Si l’ordinateur virtuel de hello est utilisé dans un environnement joint à un domaine, hello intégré **ReportServer** compte est suffisant. Pour plus d’informations sur le compte de service hello, consultez [compte de Service](https://msdn.microsoft.com/library/ms189964.aspx).
5. Cliquez sur **URL du Service Web** dans le volet gauche de hello.
6. Cliquez sur **appliquer** les valeurs par défaut tooconfigure hello.
7. Hello de note **URL de Service Web Report Server**. Notez que le port TCP hello par défaut est 80 et fait partie de l’URL de hello. Dans une étape ultérieure, vous créez une terminaison de Machine virtuelle Microsoft Azure pour le port de hello.
8. Bonjour **résultats** volet, vérifiez les actions hello s’est terminées correctement.

**Base de données :**

1. Cliquez sur **base de données** dans le volet gauche de hello.
2. Cliquez sur **Changer la base de données**.
3. Vérifiez que **Créer une nouvelle base de données de serveur de rapports** est sélectionné, puis cliquez sur Suivant.
4. Vérifiez le **Nom du serveur** et cliquez sur **Tester la connexion**.
5. Si le résultat de hello est **tester la connexion a réussi**, cliquez sur **OK** puis cliquez sur **suivant**.
6. Nom de base de données Remarque hello est **ReportServer** et hello **mode du serveur de rapports** est **natif** puis cliquez sur **suivant**.
7. Cliquez sur **suivant** sur hello **informations d’identification** page.
8. Cliquez sur **suivant** sur hello **Résumé** page.
9. Cliquez sur **suivant** sur hello **de progression et de fin** page.

**URL du portail web ou URL du Gestionnaire de rapports pour 2012 et 2014 :**

1. Cliquez sur **URL du portail Web**, ou **URL du Gestionnaire de rapports** pour 2014 et 2012, dans le volet gauche de hello.
2. Cliquez sur **Apply**.
3. Bonjour **résultats** volet, vérifiez les actions hello s’est terminées correctement.
4. Cliquez sur **Quitter**.

Pour plus d’informations sur les autorisations du serveur de rapports, consultez [Octroi d’autorisations sur un serveur de rapports en mode natif](https://msdn.microsoft.com/library/ms156014.aspx).

### <a name="browse-toohello-local-report-manager"></a>Parcourir toohello le Gestionnaire de rapports local
configuration de hello tooverify, parcourir le gestionnaire tooreport sur hello machine virtuelle.

1. Sur la machine virtuelle de hello, démarrez Internet Explorer avec des privilèges d’administrateur.
2. Parcourir toohttp://localhost/reports sur hello machine virtuelle.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>portail web de tooRemote tooConnect, ou le Gestionnaire de rapports pour 2014 et 2012
Si vous souhaitez le portail web de toohello tooconnect, ou le Gestionnaire de rapports pour 2014 et 2012, sur l’ordinateur virtuel de hello à partir d’un ordinateur distant, créez une machine virtuelle de point de terminaison TCP. Par défaut, serveur de rapports hello écoute les requêtes HTTP sur **le port 80**. Si vous configurez hello report server URL toouse un port différent, vous devez spécifier ce numéro de port Bonjour suivant les instructions.

1. Créer un point de terminaison hello Machine virtuelle le Port TCP 80. Pour plus d’informations, consultez hello [points de terminaison de Machine virtuelle et les Ports de pare-feu](#virtual-machine-endpoints-and-firewall-ports) section dans ce document.
2. Ouvrir le port 80 dans le pare-feu de l’ordinateur virtuel de hello.
3. Parcourir le portail web de toohello ou le Gestionnaire de rapports, à l’aide de la Machine virtuelle Azure **nom DNS** comme nom de serveur hello dans les URL hello. Par exemple :
   
    **Serveur de rapports** : http://uebi.cloudapp.net/reportserver  **Portail web** : http://uebi.cloudapp.net/reports
   
    [Configurer un pare-feu pour accéder au serveur de rapports](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate et publier les rapports toohello Machine virtuelle Azure
Hello tableau suivant récapitule certaines des rapports existants de hello options toopublish disponibles à partir d’un serveur de rapports local ordinateur toohello hébergé sur hello Machine virtuelle Microsoft Azure :

* **Générateur de rapports**: machine virtuelle de hello inclut hello cliquez-une fois la version du Générateur de rapports Microsoft SQL Server pour SQL 2014 et 2012. hello de générateur de rapports toostart première fois sur l’ordinateur virtuel de hello SQL 2016 :
  
  1. Démarrez votre navigateur avec des privilèges administratifs.
  2. Portail web toohello, sur l’ordinateur virtuel de hello, de parcourir et sélectionnez hello **télécharger** icône dans le coin supérieur droit de hello.
  3. Sélectionnez **Générateur de rapports**.
     
     Pour plus d’informations, consultez [Démarrer le Générateur de rapports](https://msdn.microsoft.com/library/ms159221.aspx).
* **SQL Server Data Tools**: machine virtuelle : SQL Server Data Tools est installé sur l’ordinateur virtuel de hello et peut être utilisé toocreate **projets Report Server** et des rapports sur l’ordinateur virtuel de hello. SQL Server Data Tools peut publier le serveur de rapports hello rapports toohello sur l’ordinateur virtuel de hello.
* **SQL Server Data Tools : distant** : sur votre ordinateur local, créez un projet Reporting Services contenant des rapports Reporting Services dans SQL Server Data Tools. Configurer l’URL du service web tooconnect toohello hello projet.
  
    ![propriétés de projet ssdt pour un projet SSRS](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* Créer un. Disque dur virtuel disque dur qui contient les rapports, puis télécharger et attacher un lecteur de hello.
  
  1. Créez un disque dur .VHD sur votre ordinateur local qui contient vos rapports.
  2. Créez et installez un certificat de gestion.
  3. Télécharger tooAzure de fichier de disque dur virtuel hello à l’aide d’applet de commande hello Add-AzureVHD [création et téléchargement d’un disque dur virtuel de Windows Server de tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
  4. Attacher la machine virtuelle de hello disque toohello.

## <a name="install-other-sql-server-services-and-features"></a>Installation d’autres services et fonctionnalités SQL Server
tooinstall SQL Server des services supplémentaires, tels que Analysis Services en mode tabulaire, exécutent l’Assistant hello SQL server. les fichiers de configuration de Hello sont sur le disque local de l’ordinateur virtuel de hello.

1. Cliquez sur **Démarrer**, puis sur **Tous les programmes**.
2. Cliquez sur **Microsoft SQL Server 2016**, **Microsoft SQL Server 2014** ou **Microsoft SQL Server 2012**, puis sur **Outils de configuration**.
3. Cliquez sur **Centre d’installation SQL Server**.

Vous pouvez également exécuter C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe ou C:\SQLServer_11.0_full\setup.exe

> [!NOTE]
> Hello la première fois que vous exécutez le programme d’installation de SQL Server, le programme d’installation plusieurs fichiers peuvent être téléchargés et nécessitent un redémarrage de l’ordinateur virtuel de hello et un redémarrage de l’installation de SQL Server.
> 
> Si vous avez besoin de toorepeatedly personnaliser l’image hello sélectionné à partir de la Machine virtuelle Microsoft Azure de hello, envisagez de créer votre propre image de SQL Server. La fonctionnalité d’Analysis Services SysPrep a été activée avec SQL Server 2012 SP1 CU2. Pour plus d’informations, consultez [Considérations relatives à l’installation de SQL Server à l’aide de SysPrep](https://msdn.microsoft.com/library/ee210754.aspx) et [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall Mode tabulaire d’Analysis Services
les étapes de cette section Hello **résumer** hello installation du mode tabulaire d’Analysis Services. Pour plus d’informations, voir hello :

* [Installer Analysis Services en mode tabulaire](https://msdn.microsoft.com/library/hh231722.aspx)
* [Modélisation tabulaire (didacticiel Adventure Works)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall Mode tabulaire d’Analysis Services :**

1. Dans l’Assistant installation de SQL Server hello, cliquez sur **Installation** dans hello du volet gauche, puis cliquez sur **installation autonome de nouveau SQL server ou ajoutez l’installation existante de fonctionnalités tooan**.
   
   * Si vous voyez hello **rechercher un dossier**, parcourir tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full ou c:\SQLServer_11.0_full, puis sur **Ok**.
2. Cliquez sur **suivant** page mises à jour de produit sur hello.
3. Sur hello **le Type d’Installation** page, sélectionnez **effectuer une nouvelle installation de SQL Server** et cliquez sur **suivant**.
4. Sur hello **rôle d’installation** , cliquez sur **Installation de fonctionnalités SQL Server**.
5. Sur hello **sélection des fonctionnalités** , cliquez sur **Analysis Services**.
6. Sur hello **Configuration de l’Instance** , tapez un nom descriptif, tel que **tabulaire** dans **Instance nommée** et **Id d’Instance** texte zones.
7. Sur hello **Configuration d’Analysis Services** page, sélectionnez **en Mode tabulaire**. Ajoutez hello toohello d’autorisations administratives liste des utilisateurs.
8. Terminer et fermer l’Assistant installation de SQL Server hello.

## <a name="analysis-services-configuration"></a>Configuration d’Analysis Services
### <a name="remote-access-tooanalysis-services-server"></a>TooAnalysis d’accès à distance serveur des Services
Le serveur Analysis Services prend en charge uniquement l’authentification Windows. tooaccess Analysis Services à distance à partir d’applications clientes telles que SQL Server Management Studio ou SQL Server Data Tools, ordinateur virtuel de hello doit toobe tooyour joint à un domaine local à l’aide du réseau virtuel Azure. Pour plus d’informations, consultez [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).

Une **instance par défaut** d’Analysis Services écoute sur le port TCP **2383**. Ouvrir le port de hello dans les pare-feu des machines virtuelles hello. Une instance en cluster nommée d’Analysis Services écoute également sur le port **2383**.

Pour un **instance nommée** d’Analysis Services, hello service SQL Server Browser est requis accès de port toomanage. configuration par défaut de SQL Server Browser Hello est le port **2382**.

Dans le pare-feu des machines virtuelles hello, ouvrez le port **2382** et créer un port d’instance nommée du statique Analysis Services.

1. tooverify les ports qui sont déjà dans utiliser sur hello machine virtuelle et quel processus utilise les ports hello, exécutez hello suivant de commande avec des privilèges d’administrateur :
   
        netstat /ao
2. Utilisez SQL Server Management Studio toocreate un statique Analysis Services port d’instance nommée en mettant à jour 'Port' tabulaire comme valeur des propriétés générales de l’instance. Pour plus d’informations, consultez hello « Utiliser un port fixe pour une valeur par défaut ou instance nommée » dans [configurer le pare-feu Windows de hello tooAllow accès à Analysis Services](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed).
3. Redémarrez l’instance tabulaire de hello Hello service Analysis Services.

Pour plus d’informations, consultez hello **points de terminaison de Machine virtuelle et les Ports de pare-feu** section dans ce document.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>Points de terminaison de la machine virtuelle et ports de pare-feu
Cette section résume les points de terminaison de Machine virtuelle Microsoft Azure des tooopen toocreate et les ports de pare-feu de machine virtuelle hello. Hello tableau suivant récapitule les hello **TCP** ports toocreate des points de terminaison pour et tooopen de ports hello dans le pare-feu des machines virtuelles hello.

* Si vous utilisez une seule machine virtuelle et hello deux éléments suivants sont remplies, vous n’avez pas besoin de points de terminaison de machine virtuelle toocreate et vous ne devez pas les ports de hello tooopen dans le pare-feu hello sur hello machine virtuelle.
  
  * Vous ne connectez pas toohello les fonctionnalités de SQL Server sur hello VM à distance. L’établissement d’une machine virtuelle de toohello connexion Bureau à distance et l’accès aux fonctionnalités de SQL Server hello localement sur hello machine virtuelle ne sont pas considéré comme une fonctionnalité de SQL Server toohello connexion à distance.
  * Vous ne joignez pas le domaine de hello VM tooan local via le réseau virtuel Azure ou une autre solution de tunneling VPN.
* Si l’ordinateur virtuel de hello n’est pas tooa joint à un domaine, mais que vous voulez tooremotely connexion toohello les fonctionnalités de SQL Server sur l’ordinateur virtuel :
  
  * Ouvrir des ports de hello dans le pare-feu hello sur hello machine virtuelle.
  * Créer des points de terminaison de machine virtuelle pour hello noter les ports (*).
* Si la machine virtuelle de hello est domaine tooa jointes à l’aide d’un tunnel VPN tel que le réseau virtuel Azure, les points de terminaison hello ne sont pas requis. Toutefois ouvrir les ports hello dans hello pare-feu sur hello machine virtuelle.
  
  | Port | Type | Description |
  | --- | --- | --- |
  | **80** |TCP |Accès distant au serveur de rapports (*). |
  | **1433** |TCP |SQL Server Management Studio (*). |
  | **1434** |UDP |SQL Server Browser. Cela est nécessaire lorsque hello VM tooa joint à un domaine. |
  | **2382** |TCP |SQL Server Browser. |
  | **2383** |TCP |Instance par défaut et instance en cluster nommée de SQL Server Analysis Services. |
  | **Définie par l’utilisateur** |TCP |Créer un port d’instance nommée pour un numéro de port que vous choisissez des Services analyse statique, puis débloquez le numéro de port hello dans le pare-feu hello. |

Pour plus d’informations sur la création de points de terminaison, voir hello :

* Créer des points de terminaison :[comment tooSet des points de terminaison tooa Machine virtuelle](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* SQL Server : Consultez la section « Terminer la Configuration étapes tooconnect toohello virtual machines en utilisant SQL Server Management Studio » hello [approvisionnement d’une Machine virtuelle de SQL Server sur Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Hello diagramme suivant illustre les composants sur hello machine virtuelle et les tooopen de ports hello Bonjour toofeatures de machine virtuelle pare-feu tooallow l’accès à distance.

![tooopen de ports pour les applications Business Intelligence dans des machines virtuelles Azure](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>Ressources
* Consultez la politique de prise en charge de hello pour les logiciels serveurs Microsoft utilisée dans un environnement de Machine virtuelle Azure hello. Hello rubrique suivante résume la prise en charge des fonctionnalités telles que BitLocker, le Clustering de basculement et équilibrage de charge réseau. [Prise en charge des logiciels serveur Microsoft pour Azure Virtual Machines](http://support.microsoft.com/kb/2721672).
* [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [Machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Configuration d'une machine virtuelle SQL Server sur Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [Comment tooAttach un tooa de disque de données Virtual Machine](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Migration d’une base de données de tooSQL Server sur une machine virtuelle Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Déterminer hello Mode serveur d’une Instance Analysis Services](https://msdn.microsoft.com/library/gg471594.aspx)
* [Modélisation multidimensionnelle (didacticiel Adventure Works)](https://technet.microsoft.com/library/ms170208.aspx)
* [Centre de documentation](https://azure.microsoft.com/documentation/)
* [Utilisation de Power BI dans un environnement hybride](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [Soumettre des commentaires et des informations de contact via Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>Contenu de la communauté
* [Gestion de base de données SQL Azure avec PowerShell](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

