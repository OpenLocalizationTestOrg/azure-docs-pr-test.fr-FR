---
title: aaaUse PowerShell tooCreate une machine virtuelle avec un serveur en Mode natif rapport | Documents Microsoft
description: "Cette rubrique décrit et vous guide à travers le déploiement de hello et la configuration d’un serveur de rapports SQL Server Reporting Services en mode natif dans une Machine virtuelle Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>Utilisez PowerShell tooCreate un Azure VM avec un serveur en Mode natif rapport
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Cette rubrique décrit et vous guide à travers le déploiement de hello et la configuration d’un serveur de rapports SQL Server Reporting Services en mode natif dans une Machine virtuelle Azure. Hello étapes tooconfigure Reporting Services dans ce document utilisent une combinaison de machine virtuelle d’étapes manuelles toocreate hello et un script Windows PowerShell sur hello machine virtuelle. script de configuration Hello inclut l’ouverture d’un port de pare-feu pour HTTP ou HTTPs.

> [!NOTE]
> Si vous n’avez pas besoin **HTTPS** sur le serveur de rapports hello, **ignorez l’étape 2**.
> 
> Après avoir créé le hello machine virtuelle à l’étape 1, accédez à HTTP et le serveur de rapports toohello section Utilisation script tooconfigure hello. Après avoir exécuté le script de hello, le serveur de rapports hello est toouse prêt.

## <a name="prerequisites-and-assumptions"></a>Configuration requise et hypothèses
* **Abonnement Azure**: vérifier le nombre de hello de cœurs disponibles dans votre abonnement Azure. Si vous créez hello recommandée de machine virtuelle **A3**, vous devez **4** cœurs disponibles. Si vous utilisez une machine virtuelle de taille **A2**, vous devez disposer de **2** mémoires à tores magnétiques.
  
  * limite de cœurs hello tooverify de votre abonnement, hello portail Azure classic, cliquez sur paramètres dans le volet gauche de hello, puis cliquez sur l’utilisation dans le menu du haut hello.
  * tooincrease hello quota de cœurs, contactez [prise en charge Azure](https://azure.microsoft.com/support/options/). Pour plus d’informations sur les tailles de machines virtuelles, consultez la page [Tailles de machines virtuelles pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* **Exécution de scripts Windows PowerShell**: hello nous supposons que vous avez une connaissance de base de Windows PowerShell. Pour plus d’informations sur l’utilisation de Windows PowerShell, voir hello :
  
  * [Démarrage de Windows PowerShell sur Windows Server](https://technet.microsoft.com/library/hh847814.aspx)
  * [Prise en main de Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>Étape 1 : Approvisionner une machine virtuelle Azure
1. Parcourir toohello portail Azure classic.
2. Cliquez sur **virtuels** dans le volet gauche de hello.
   
    ![microsoft azure virtual machines](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. Cliquez sur **Nouveau**.
   
    ![bouton nouveau](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. Cliquez sur **À partir de la galerie**.
   
    ![nouvelle machine virtuelle à partir de la galerie](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. Cliquez sur **SQL Server 2014 RTM Standard – Windows Server 2012 R2** puis cliquez sur hello flèche toocontinue.
   
    ![Suivant](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Si vous avez besoin de fonctionnalité d’abonnements pilotés par les données de Reporting Services salutation, choisissez **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**. Pour plus d’informations sur les éditions de SQL Server et de prise en charge de la fonctionnalité, consultez [fonctionnalités prises en charge par les éditions de SQL Server 2012 de hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).
6. Sur hello **configuration d’ordinateur virtuel** page, modifier hello champs qui suivent :
   
   * S’il existe plusieurs **DATE de publication de la VERSION**, sélectionnez hello version la plus récente.
   * **Nom de Machine virtuelle**: nom de l’ordinateur hello est également utilisé sur la page de configuration suivante hello en tant que nom de Cloud Service DNS par défaut hello. nom DNS de Hello doit être unique sur hello service Azure. Envisagez de configurer hello machine virtuelle avec un nom qui décrit quelles hello pour que machine virtuelle est utilisée. Par exemple, ssrsnativecloud.
   * **Niveau**: Standard
   * **Taille : A3** hello est recommandé de taille de machine virtuelle pour les charges de travail SQL Server. Si un ordinateur virtuel est utilisé uniquement comme un serveur de rapports, une taille de machine virtuelle A2 est suffisante, sauf si le serveur de rapports hello rencontre une grande charge de travail. Pour connaître les informations de tarification des machines virtuelles, consultez la page [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/).
   * **Nouveau nom d’utilisateur**: nom hello que vous fournissez est créé en tant qu’administrateur sur la machine virtuelle de hello.
   * **Nouveau mot de passe** et **confirmation**. Ce mot de passe est utilisé pour le nouveau compte d’administrateur hello et il est recommandé de qu'utiliser un mot de passe fort.
   * Cliquez sur **Suivant**. ![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. Sur la page suivante de hello, modifiez hello champs qui suivent :
   
   * **Service cloud** : sélectionnez **Créer un service cloud**.
   * **Nom DNS du Service de cloud computing**: le nom DNS public de hello Hello Service Cloud qui est associé à hello machine virtuelle. nom par défaut de Hello est hello que vous avez tapé pour le nom d’ordinateur virtuel hello. Si dans les étapes ultérieures de la rubrique de hello, vous créez un certificat SSL approuvé et le nom DNS de hello est utilisée pour valeur hello Hello »**délivré à**» du certificat de hello.
   * **Affinité de la région/groupe/réseau virtuel**: choisissez hello région le plus proche tooyour les utilisateurs finaux.
   * **Compte de stockage**: utilisez un compte de stockage généré automatiquement.
   * **Groupe à haute disponibilité**: Aucun.
   * **Points de terminaison** conserver hello **Bureau à distance** et **PowerShell** points de terminaison, puis ajoutez le point de terminaison HTTP ou HTTPS, selon votre environnement.
     
     * **HTTP**: hello par défaut des ports publics et privés sont **80**. Notez que si vous utilisez un port privé autre que 80, modifiez **$HTTPport = 80** dans le script de http hello.
     * **HTTPS**: hello par défaut des ports publics et privés sont **443**. Meilleure pratique de sécurité est un port privé toochange hello et configurer votre pare-feu et hello report server toouse hello port privé. Pour plus d’informations sur les points de terminaison, consultez [comment configurer la Communication avec un ordinateur virtuel de tooSet](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Notez que si vous utilisez un port autre que 443, modifiez le paramètre hello **$HTTPsport = 443** Bonjour script HTTPS.
   * Cliquez sur suivant. ![Suivant](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. Dans hello dernière page de l’Assistant de hello, conservez par défaut de hello **installer l’agent de machine virtuelle hello** sélectionné. Hello étapes décrites dans cette rubrique n’utilisent pas l’agent de machine virtuelle hello, mais si vous envisagez de tookeep cet ordinateur virtuel, agent de machine virtuelle hello et extensions vous permettra de tooenhance he CM.  Pour plus d’informations sur l’agent de machine virtuelle hello, consultez [Agent de machine virtuelle et Extensions – partie 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/). L’un de l’annonce d’extensions installées par défaut hello en cours d’exécution est extension hello « BGINFO » qui s’affiche sur le bureau de machine virtuelle hello, espace de lecteur informations système telles que de l’adresse IP interne et libre.
9. Cliquez Terminé . ![OK](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. Hello **état** de machine virtuelle affiche sous la forme de hello **départ (Provisioning)** au cours de processus de fourniture de hello, puis en tant que **en cours d’exécution** lorsque hello machine virtuelle est configurée et prête toouse.

## <a name="step-2-create-a-server-certificate"></a>Étape 2 : Créer un certificat de serveur
> [!NOTE]
> Si vous n’avez pas besoin de HTTPS sur le serveur de rapports hello, vous pouvez **ignorez l’étape 2** et consultez la section de toohello **utiliser HTTP et le serveur de rapports de script tooconfigure hello**. Utilisez hello HTTP script tooquickly configurer le serveur de rapports hello et rapport hello serveur sera prêt toouse.

Dans l’ordre toouse HTTPS sur hello machine virtuelle, vous devez un certificat SSL approuvé. Selon votre scénario, vous pouvez utiliser une des deux méthodes suivantes de hello :

* Un certificat SSL valide émis par une autorité de certification et approuvé par Microsoft. certificats de Hello autorité de certification racine sont requis toobe distribué via hello programme de certificat racine Microsoft. Pour plus d’informations sur ce programme, consultez [Windows et Windows Phone 8 SSL Root Certificate Program (autorités de certification membres)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) et [Introduction toohello programme de certificat racine Microsoft](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).
* Un certificat auto-signé. Les certificats auto-signés sont déconseillés pour les environnements de production.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse un certificat créé par une autorité de certificat approuvé (CA)
1. **Demander un certificat de serveur pour le site Web de hello à partir d’une autorité de certification**. 
   
    Vous pouvez utiliser hello Assistant certificat de serveur Web soit toogenerate un fichier de demande de certificat (Certreq.txt) que vous envoyez autorité de certification tooa ou toogenerate une demande pour une autorité de certification en ligne. Par exemple, les services de certificats Microsoft dans Windows Server 2012. Selon le niveau d’assurance d’identification proposé par votre certificat de serveur hello est plusieurs mois de tooseveral jours pour tooapprove d’autorité de certification hello votre demande et envoi d’un fichier de certificat. 
   
    Pour plus d’informations sur la demande d’un certificat de serveur, voir hello : 
   
   * Utiliser [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).
   * TooAdminister d’outils de sécurité Windows Server 2012.
     
     [Outils de sécurité tooAdminister Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > Hello **délivré à** champ Hello approuvé le certificat SSL doit être hello même comme hello **nom DNS du Service Cloud** vous avez utilisé pour hello nouvelle machine virtuelle.

2. **Installer le certificat de serveur hello sur le serveur Web de hello**. Dans ce cas, serveur Web de Hello est hello VM que hôtes hello serveur de rapports et le site Web de hello est créé dans les étapes ultérieures lorsque vous configurez Reporting Services. Pour plus d’informations sur l’installation du certificat de serveur hello sur le serveur Web de hello en utilisant le composant logiciel enfichable MMC certificat hello, consultez [installer un certificat de serveur](https://technet.microsoft.com/library/cc740068).
   
    Si vous voulez toouse hello script est inclus dans cette rubrique, le serveur de rapports tooconfigure hello, hello valeur des certificats de hello **l’empreinte numérique** est requis en tant que paramètre du script de hello. Voir section suivante de hello pour plus d’informations sur la façon dont tooobtain hello empreinte numérique du certificat de hello.
3. Affecter hello certificat toohello de rapports server. Hello s’effectue dans la section suivante de hello lorsque vous configurez le serveur de rapports hello.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>toouse hello un certificat auto-signé Machines virtuelles
Un certificat auto-signé a été créé sur la machine virtuelle de hello hello machine virtuelle a été configuré. certificat de Hello a hello comme hello nom VM DNS du même nom. Des erreurs de certificat ordre tooavoid, il est nécessaire que le certificat hello est approuvé sur hello machine virtuelle proprement dite, ainsi que par tous les utilisateurs du site de hello.

1. autorité de certification de racine de hello tootrust du certificat hello sur hello Local de machine virtuelle, ajoutez hello certificat toohello **autorités de Certification racines de confiance**. Hello Voici un résumé des étapes hello requises. Pour obtenir des instructions détaillées sur la façon dont tootrust hello autorité de certification, consultez [installer un certificat de serveur](https://technet.microsoft.com/library/cc740068).
   
   1. À partir de hello portail Azure classic, sélectionnez hello machine virtuelle et cliquez sur se connecter. Selon la configuration de votre navigateur, vous pouvez être demandées par invite toosave un fichier .rdp pour la connexion toohello machine virtuelle.
      
       ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Utilisez le nom de machine virtuelle hello, nom d’utilisateur et mot de passe configurés lors de la création de hello machine virtuelle. 
      
       Par exemple, Bonjour suivant image, nom d’ordinateur virtuel hello est **ssrsnativecloud** et le nom d’utilisateur hello est **testuser**.
      
       ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. Exécutez mmc.exe. Pour plus d’informations, consultez [Comment : afficher les certificats avec hello le composant logiciel enfichable MMC](https://msdn.microsoft.com/library/ms788967.aspx).
   3. Dans l’application de console hello **fichier** menu, ajouter hello **certificats** -composant logiciel enfichable, sélectionnez **compte d’ordinateur** lorsque vous y êtes invité, puis cliquez sur **suivant**.
   4. Sélectionnez **ordinateur Local** toomanage puis cliquez sur **Terminer**.
   5. Cliquez sur **Ok** , puis développez hello **certificats - personnel** nœuds, puis cliquez sur **certificats**. Hello certificat est nommé d’après le nom DNS hello hello machine virtuelle et se termine par **cloudapp.net**. Cliquez sur le nom de certificat hello et cliquez sur **copie**.
   6. Développez hello **autorités de Certification racines de confiance** nœud et avec le bouton droit puis **certificats** puis cliquez sur **coller**.
   7. toovalidate, double cliquez sur le nom de certificat hello sous **autorités de Certification racines de confiance** et vérifiez qu’aucun message d’erreur et que vous voyez le certificat. Si vous voulez toouse hello HTTPS script est inclus dans cette rubrique, le serveur de rapports tooconfigure hello, hello valeur des certificats de hello **l’empreinte numérique** est requis en tant que paramètre du script de hello. **valeur d’empreinte numérique hello tooget**, suivez hello suivantes. Il existe également une empreinte numérique de PowerShell exemple tooretrieve hello dans la section [utiliser le serveur de rapports de script tooconfigure hello et HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).
      
      1. Double-cliquez sur nom hello certificat hello, par exemple ssrsnativecloud.cloudapp.net.
      2. Cliquez sur hello **détails** onglet.
      3. Cliquez sur **Empreinte numérique**. valeur de Hello de l’empreinte numérique hello est affichée dans le champ de détails hello, par exemple a6 08 3c df f9 0 b f7 e3 7C 25 ed a4 ed 7e CA 91 9c 2C fb 2f.
      4. Copiez l’empreinte numérique hello et enregistrer la valeur de hello pour une date ultérieure ou modifier le script de hello maintenant.
      5. (*) Avant d’exécuter les script hello, supprimez les espaces de hello entre les paires de hello de valeurs. Par exemple l’empreinte numérique hello indiquée précédemment est maintenant a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.
      6. Affecter hello certificat toohello de rapports server. Hello s’effectue dans la section suivante de hello lorsque vous configurez le serveur de rapports hello.

Si vous utilisez un certificat SSL auto-signé, nom hello sur le certificat de hello correspond déjà hostname hello Hello machine virtuelle. Par conséquent, hello DNS de l’ordinateur de hello est déjà enregistré globalement et sont accessibles à partir de n’importe quel client.

## <a name="step-3-configure-hello-report-server"></a>Étape 3 : Configurer le serveur de rapports de hello
Cette section vous guide tout au long de la configuration de hello machine virtuelle comme un serveur de rapports Reporting Services en mode natif. Vous pouvez utiliser une des hello suivant du serveur de rapports de méthodes tooconfigure hello :

* Utiliser le serveur de rapports hello script tooconfigure hello
* Utilisez le Gestionnaire de Configuration tooConfigure hello serveur de rapports.

Pour plus d’étapes, consultez la section de hello [Connect toohello Machine virtuelle et démarrer hello Gestionnaire de Configuration de Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).

**Remarque sur l’authentification :** l’authentification Windows est hello, méthode d’authentification recommandée et authentification de Reporting Services par défaut hello. Seuls les utilisateurs qui sont configurés sur la machine virtuelle de hello peuvent accéder aux Services de création de rapports et attribué des rôles Services tooReporting.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>Utiliser le serveur de rapports de script tooconfigure hello et HTTP
toouse hello Windows PowerShell script tooconfigure hello serveur de rapports, hello complète comme suit. configuration de Hello inclut le protocole HTTP, HTTPS pas :

1. À partir de hello portail Azure classic, sélectionnez hello machine virtuelle et cliquez sur se connecter. Selon la configuration de votre navigateur, vous pouvez être demandées par invite toosave un fichier .rdp pour la connexion toohello machine virtuelle.
   
    ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Utilisez le nom de machine virtuelle hello, nom d’utilisateur et mot de passe configurés lors de la création de hello machine virtuelle. 
   
    Par exemple, Bonjour suivant image, nom d’ordinateur virtuel hello est **ssrsnativecloud** et le nom d’utilisateur hello est **testuser**.
   
    ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Sur la machine virtuelle de hello, ouvrez **Windows PowerShell ISE** avec des privilèges d’administrateur. Hello PowerShell ISE est installé par défaut sur Windows server 2012. Il est recommandé de qu'utiliser hello ISE plutôt qu’une fenêtre Windows PowerShell standard afin que vous pouvez coller le script de hello hello ISE, modifiez le script de hello et puis exécutez le script de hello.
3. Dans Windows PowerShell ISE, cliquez sur hello **vue** menu, puis sur **afficher le volet Script**.
4. Hello script suivant de copier et coller le script de hello dans le volet de script Windows PowerShell ISE hello.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. Si vous avez créé hello machine virtuelle avec un port HTTP autre que 80, modifiez le paramètre hello $HTTPport = 80.
6. Hello script est actuellement configuré pour Reporting Services. Si vous souhaitez le script de hello toorun pour Reporting Services, modifier trop partie de version hello d’espace de noms toohello hello chemin d’accès « v11 » sur l’instruction de hello Get-WmiObject.
7. Exécutez le script de hello.

**Validation**: tooverify fonctionnalités du serveur de rapports de base hello fonctionnent, consultez hello [configuration de hello Vérifiez](#verify-the-configuration) section plus loin dans cette rubrique.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>Utiliser le serveur de rapports de script tooconfigure hello et HTTPS
toouse Windows PowerShell tooconfigure hello serveur de rapports, hello complète comme suit. configuration de Hello inclut le protocole HTTPS, non HTTP.

1. À partir de hello portail Azure classic, sélectionnez hello machine virtuelle et cliquez sur se connecter. Selon la configuration de votre navigateur, vous pouvez être demandées par invite toosave un fichier .rdp pour la connexion toohello machine virtuelle.
   
    ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Utilisez le nom de machine virtuelle hello, nom d’utilisateur et mot de passe configurés lors de la création de hello machine virtuelle. 
   
    Par exemple, Bonjour suivant image, nom d’ordinateur virtuel hello est **ssrsnativecloud** et le nom d’utilisateur hello est **testuser**.
   
    ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Sur la machine virtuelle de hello, ouvrez **Windows PowerShell ISE** avec des privilèges d’administrateur. Hello PowerShell ISE est installé par défaut sur Windows server 2012. Il est recommandé de qu'utiliser hello ISE plutôt qu’une fenêtre Windows PowerShell standard afin que vous pouvez coller le script de hello hello ISE, modifiez le script de hello et puis exécutez le script de hello.
3. tooenable en cours d’exécution des scripts, exécutez hello commande de Windows PowerShell suivante :
   
        Set-ExecutionPolicy RemoteSigned
   
    Vous pouvez ensuite exécuter hello suivant la stratégie de hello tooverify :
   
        Get-ExecutionPolicy
4. Dans **Windows PowerShell ISE**, cliquez sur hello **vue** menu, puis sur **afficher le volet Script**.
5. Copiez hello suivants de script et collez-le dans le volet de script Windows PowerShell ISE hello.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Modifier hello **$certificatehash** paramètre hello script :
   
   * Il s’agit d’un paramètre **obligatoire** . Si vous n’avez pas enregistré la valeur du certificat hello des étapes précédentes de hello, utilisez une de hello suivant la valeur de hachage du certificat hello toocopy méthodes à partir de l’empreinte numérique des certificats hello. :
     
       Sur hello machine virtuelle, ouvrez Windows PowerShell ISE et exécutez hello de commande suivante :
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       sortie de Hello recherche similaire toohello suivant. Si le script de hello renvoie une ligne vide, hello machine virtuelle n’a pas d’un certificat configuré par exemple, consultez la section de hello [toouse hello un certificat auto-signé Machines virtuelles](#to-use-the-virtual-machines-self-signed-certificate).
     
     OU
   * Hello de machine virtuelle, exécutez le mmc.exe et puis ajoutez hello **certificats** enfichable.
   * Sous hello **autorités de certification racine de confiance** nœud double-cliquez sur le nom du certificat. Si vous utilisez un certificat auto-signé de hello Hello machine virtuelle, les certificats hello est nommé d’après le nom DNS hello hello machine virtuelle et se termine par **cloudapp.net**.
   * Cliquez sur hello **détails** onglet.
   * Cliquez sur **Empreinte numérique**. valeur de Hello de l’empreinte numérique hello est affichée dans le champ de détails hello, par exemple af 11 60 b6 4 b 28 8 d 89 0 a 82 12 ff 6 b a9 c3 66 4f 31 90 48
   * **Avant d’exécuter les script hello**, supprimer les espaces entre les paires de hello de valeurs hello. Par exemple af1160b64b288d890a8212ff6ba9c3664f319048
7. Modifier hello **$httpsport** paramètre : 
   
   * Si vous avez utilisé le port 443 pour le point de terminaison HTTPS hello, puis il est inutile tooupdate ce paramètre dans le script de hello. Sinon, utilisez vous avez sélectionné lorsque vous avez configuré le point de terminaison privé hello HTTPS sur hello machine virtuelle de la valeur du port hello.
8. Modifier hello **$DNSName** paramètre : 
   
   * script de Hello est configuré pour un certificat de caractère générique $DNSName = « + ». Si vous ne procédez à aucune tooconfigure que vous souhaitez pour une liaison de certificat avec caractères génériques, commentez $DNSName = « + « et activez hello suivant la ligne, référence $DNSNAme complète de hello, ## $DNSName="$server.cloudapp.net ».
     
       Modifiez la valeur de hello $DNSName si vous ne souhaitez pas le nom DNS de l’ordinateur virtuel toouse hello pour Reporting Services. Si vous utilisez le paramètre hello, hello certificat doit également utiliser ce nom et vous inscrivez nom hello globalement sur un serveur DNS.
9. Hello script est actuellement configuré pour Reporting Services. Si vous souhaitez le script de hello toorun pour Reporting Services, modifier trop partie de version hello d’espace de noms toohello hello chemin d’accès « v11 » sur l’instruction de hello Get-WmiObject.
10. Exécutez le script de hello.

**Validation**: tooverify fonctionnalités du serveur de rapports de base hello fonctionnent, consultez hello [configuration de hello Vérifiez](#verify-the-connection) section plus loin dans cette rubrique. liaison de certificat tooverify hello ouvrir une invite de commandes avec des privilèges d’administrateur et puis exécutez hello commande suivante :

    netsh http show sslcert

résultat de Hello inclura hello qui suit :

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>Utilisez le Gestionnaire de Configuration tooConfigure hello serveur de rapports
Si vous ne souhaitez pas de serveur de rapports toorun hello PowerShell script tooconfigure hello, suivez les étapes de hello dans cette section toouse hello Reporting Services en mode natif configuration manager tooconfigure hello serveur de rapports.

1. À partir de hello portail Azure classic, sélectionnez hello machine virtuelle et cliquez sur se connecter. Utilisez le nom d’utilisateur hello et mot de passe configurés lors de la création de hello machine virtuelle.
   
    ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Exécutez Windows update et installez les mises à jour toohello machine virtuelle. Si un redémarrage de hello machine virtuelle est nécessaire, redémarrez hello machine virtuelle et se reconnecter toohello machine virtuelle à partir de hello portail Azure classic.
3. À partir du menu Démarrer hello hello machine virtuelle, tapez **Reporting Services** et ouvrez **Gestionnaire de Configuration de Reporting Services**.
4. Laissez les valeurs par défaut de hello **nom du serveur** et **Instance de serveur de rapports**. Cliquez sur **Connecter**.
5. Dans le volet gauche de hello, cliquez sur **URL du Service Web**.
6. Par défaut, Reporting Services est configuré pour le port HTTP 80 avec l’adresse IP « entièrement affectée ». tooadd HTTPS :
   
   1. Dans **certificat SSL**: hello select certificat toouse, par exemple [nom de la machine virtuelle]. cloudapp.net. Si aucun certificat n’est répertorié, consultez la section de hello **étape 2 : créer un certificat de serveur** pour plus d’informations sur comment tooinstall et approbation hello certificat sur hello machine virtuelle.
   2. Sous **Port SSL**: sélectionnez 443. Si vous avez configuré le point de terminaison privé hello HTTPS Bonjour machine virtuelle avec un autre port privé, utilisez cette valeur ici.
   3. Cliquez sur **appliquer** et attendez hello opération toocomplete.
7. Dans le volet gauche de hello, cliquez sur **base de données**.
   
   1. Cliquez sur **Changer la base de données**.
   2. Cliquez sur **Créer une nouvelle base de données de serveur de rapports**, puis sur **Suivant**.
   3. Laissez la valeur par défaut hello **nom du serveur**: hello machine virtuelle sous la forme nom et laissez la valeur par défaut hello **Type d’authentification** en tant que **utilisateur actuel** – **lasécuritéintégrée**. Cliquez sur **Suivant**.
   4. Laissez la valeur par défaut hello **nom de la base de données** en tant que **ReportServer** et cliquez sur **suivant**.
   5. Laissez la valeur par défaut hello **Type d’authentification** en tant que **informations d’identification du Service** et cliquez sur **suivant**.
   6. Cliquez sur **suivant** sur hello **Résumé** page.
   7. Lors de la configuration de hello est terminée, cliquez sur **Terminer**.
8. Dans le volet gauche de hello, cliquez sur **URL du Gestionnaire de rapports**. Laissez la valeur par défaut hello **répertoire virtuel** en tant que **rapports** et cliquez sur **appliquer**.
9. Cliquez sur **Exit** tooclose hello Gestionnaire de Configuration de Reporting Services.

## <a name="step-4-open-windows-firewall-port"></a>Étape 4 : Ouvrir le port du pare-feu Windows
> [!NOTE]
> Si vous avez utilisé un hello scripts tooconfigure hello serveur de rapports, vous pouvez ignorer cette section. script de Hello inclus un port de pare-feu étape tooopen hello. par défaut de Hello est le port 80 pour HTTP et le port 443 pour HTTPS.
> 
> 

tooconnect à distance tooReport Manager ou hello rapports Server sur l’ordinateur virtuel de hello, d’un point de terminaison TCP est requis sur hello machine virtuelle. Il est hello tooopen requis même port dans le pare-feu de machine virtuelle hello. point de terminaison Hello a été créé lors de la configuration hello machine virtuelle.

Cette section fournit des informations de base sur la façon dont tooopen hello port de pare-feu. Pour plus d’informations, consultez la page [Configurer un pare-feu pour accéder au serveur de rapports](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> Si vous avez utilisé le serveur de rapports hello hello script tooconfigure, vous pouvez ignorer cette section. script de Hello inclus un port de pare-feu étape tooopen hello.
> 
> 

Si vous avez configuré un port privé pour HTTPS autre que 443, modifiez hello script suivant en conséquence. port de tooopen **443** sur hello pare-feu Windows, suivez suivantes de hello :

1. Ouvrez une fenêtre Windows PowerShell avec des privilèges administratifs.
2. Si vous avez utilisé un port autre que 443 lorsque vous avez configuré le point de terminaison HTTPS hello sur hello VM, mettre à jour le port hello Bonjour de commande suivante, puis exécutez commande hello :
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Lors de la commande hello se termine, **Ok** s’affiche dans l’invite de commandes hello.

tooverify que le port de hello est ouvert, ouvrez une fenêtre Windows PowerShell et l’exécution hello commande suivante :

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Vérifier la configuration de hello
tooverify fonctionnalités du serveur de rapports de base hello fonctionne à présent, ouvrez votre navigateur avec des privilèges d’administrateur et puis de signaler les Gestionnaire de rapports ad server URL Parcourir toohello suivantes :

* Sur la machine virtuelle de hello, accédez à toohello URL du serveur de rapports :
  
        http://localhost/reportserver
* Sur la machine virtuelle de hello, accédez à toohello URL du Gestionnaire de rapports :
  
        http://localhost/Reports
* À partir de votre ordinateur local, accédez toohello **distant** au Gestionnaire de rapports sur la machine virtuelle de hello. Mettre à jour le nom de DNS hello Bonjour selon l’exemple suivant. Lors de l’invité à entrer un mot de passe, utiliser les informations d’identification de l’administrateur hello que vous avez créé lors de la configuration de machine virtuelle de hello. nom d’utilisateur Hello est Bonjour [domaine]\[nom d’utilisateur] format, où domaine de hello est le nom de l’ordinateur hello machine virtuelle, par exemple ssrsnativecloud\testuser. Si vous n’utilisez pas HTTP**S**, supprimez hello **s** dans l’URL de hello. Consultez la section suivante de hello pour plus d’informations sur la création d’utilisateurs supplémentaires sur la machine virtuelle.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* À partir de votre ordinateur local, accédez toohello URL du serveur de rapports distant. Mettre à jour le nom de DNS hello Bonjour selon l’exemple suivant. Si vous n’utilisez pas HTTPS, supprimez hello s dans les URL hello.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>Créer des utilisateurs et attribuer des rôles
Une fois que le serveur de rapports de configuration et la vérification hello, une tâche administrative courante est toocreate un ou plusieurs utilisateurs et affecter des utilisateurs tooReporting rôles des Services. Pour plus d’informations, voir hello :

* [Créer un compte d’utilisateur local](https://technet.microsoft.com/library/cc770642.aspx)
* [Accorder l’accès utilisateur tooa le serveur de rapports (Gestionnaire de rapports)](https://msdn.microsoft.com/library/ms156034.aspx))
* [Créer et gérer des attributions de rôles](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate et publier les rapports toohello Machine virtuelle Azure
Hello tableau suivant récapitule certaines des rapports existants de hello options toopublish disponibles à partir d’un serveur de rapports local ordinateur toohello hébergé sur hello Machine virtuelle Microsoft Azure :

* **Script RS.exe**: utilisez RS.exe script toocopy les éléments de rapports et tooyour de serveur de rapports existante Machine virtuelle Microsoft Azure. Pour plus d’informations, consultez le section hello « en mode natif tooNative Mode – Machine virtuelle Microsoft Azure » dans [Sample Reporting Services rs.exe Script tooMigrate contenu entre des serveurs de rapports](https://msdn.microsoft.com/library/dn531017.aspx).
* **Générateur de rapports**: machine virtuelle de hello inclut hello cliquez-une fois la version du Générateur de rapports Microsoft SQL Server. hello de générateur de rapports toostart première fois sur l’ordinateur virtuel de hello :
  
  1. Démarrez votre navigateur avec des privilèges administratifs.
  2. Recherchez gestionnaire tooreport sur l’ordinateur virtuel de hello et cliquez sur **le Générateur de rapports** dans le ruban de hello.
     
     Pour plus d’informations, consultez [Installation, désinstallation et prise en charge du Générateur de rapports](https://technet.microsoft.com/library/dd207038.aspx).
* **SQL Server Data Tools : Machine virtuelle**: Si vous avez créé hello machine virtuelle avec SQL Server 2012, SQL Server Data Tools est installé sur l’ordinateur virtuel de hello et peut être utilisé toocreate **projets Report Server** et des rapports sur hello virtuel ordinateur. SQL Server Data Tools peut publier le serveur de rapports hello rapports toohello sur l’ordinateur virtuel de hello.
  
    Si vous avez créé hello machine virtuelle avec SQL server 2014, vous pouvez installer SQL Server données Tools - Business Intelligence pour visual Studio. Pour plus d’informations, voir hello :
  
  * [Microsoft SQL Server Data Tools - Business Intelligence pour Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools - Business Intelligence pour Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server Data Tools et SQL Server Business Intelligence (SSDT-BI)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server Data Tools : distant** : sur votre ordinateur local, créez un projet Reporting Services contenant des rapports Reporting Services dans SQL Server Data Tools. Configurer l’URL du service web tooconnect toohello hello projet.
  
    ![propriétés de projet ssdt pour un projet SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **Utilisez le script**: utiliser le contenu du serveur de rapports toocopy script. Pour plus d’informations, consultez [Sample Reporting Services rs.exe Script tooMigrate contenu entre des serveurs de rapports](https://msdn.microsoft.com/library/dn531017.aspx).

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>Réduire les coûts si vous n’utilisez pas hello machine virtuelle
> [!NOTE]
> pour vos Machines virtuelles de Azure inutilisés, des frais toominimize arrêter hello machine virtuelle à partir de hello portail Azure classic. Si vous utilisez les options d’alimentation Windows hello à l’intérieur d’un tooshut de machine virtuelle vers le bas hello machine virtuelle, vous êtes toujours facturé hello montant pour hello machine virtuelle. les frais tooreduce, vous devez tooshut vers le bas hello VM Bonjour portail Azure classic. Si vous n’avez plus besoin hello machine virtuelle, n’oubliez pas de toodelete hello VM et hello des frais de stockage de tooavoid de fichiers .vhd associés. Pour plus d’informations, consultez la section hello FAQ à [détails de tarification des Machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="more-information"></a>Informations complémentaires
### <a name="resources"></a>Ressources
* Pour obtenir un contenu similaire liés au déploiement de serveur unique tooa de SQL Server Business Intelligence et SharePoint 2013, consultez [tooCreate d’utiliser Windows PowerShell une machine virtuelle Azure avec SQL Server BI et SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).
* Pour tooa connexe de contenu similaire déploiement multiserveur de SQL Server Business Intelligence et SharePoint 2013, consultez [déployer SQL Server Business Intelligence dans des Machines virtuelles Azure](https://msdn.microsoft.com/library/dn321998.aspx).
* Pour obtenir des informations générales toodeployments associées de SQL Server Business Intelligence dans des Machines virtuelles Azure, consultez [SQL Server Business Intelligence dans des Machines virtuelles Azure](virtual-machines-windows-classic-ps-sql-bi.md).
* Pour plus d’informations sur le coût de hello frais de calcul Azure, consultez onglet de Machines virtuelles hello de [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).

### <a name="community-content"></a>Contenu de la communauté
* Pour obtenir des instructions étape par étape sur la façon dont toocreate un mode natif de Reporting Services serveur de rapports sans utiliser de script, consultez [SQL Reporting Service d’hébergement sur Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Ressources de tooother de liens pour SQL Server dans des machines virtuelles Azure
[Vue d’ensemble de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

