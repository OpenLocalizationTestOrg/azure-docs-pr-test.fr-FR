---
title: aaaHPC Pack de cluster pour Excel et SOA | Documents Microsoft
description: "Prise en main de l’exécution de charges de travail Excel et SOA à grande échelle sur un cluster HPC Pack dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Prise en main de l’exécution de charges de travail Excel et SOA sur un cluster HPC Pack dans Azure
Cet article explique comment toodeploy un Microsoft HPC Pack 2012 R2 de cluster sur des machines virtuelles à l’aide d’un modèle de démarrage rapide Azure, ou éventuellement un script de déploiement d’Azure PowerShell. cluster de Hello utilise conçus des images de machine virtuelle de Azure Marketplace toorun Microsoft Excel ou de charges de travail architecture orientée services (SOA) avec HPC Pack. Vous pouvez utiliser hello toorun de cluster HPC d’Excel et des services SOA à partir d’un ordinateur de client local. Hello Excel HPC services incluent le déchargement de classeur Excel et les fonctions définies par l’utilisateur Excel ou UDF.

> [!IMPORTANT] 
> Cet article est basé sur les fonctionnalités, les modèles et les scripts pour HPC Pack 2012 R2. Ce scénario n’est pas pris en charge dans HPC Pack 2016 pour l’instant.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

À un niveau élevé, hello diagramme suivant montre hello HPC Pack cluster que vous créez.

![Cluster HPC avec des nœuds exécutant des charges de travail Excel][scenario]

## <a name="prerequisites"></a>Composants requis
* **Ordinateur client** -vous besoin d’un cluster de toohello travaux clients basés sur Windows ordinateur toosubmit exemple Excel et SOA. Vous devez également un Bonjour de toorun de l’ordinateur Windows Azure PowerShell script de déploiement du cluster (si vous choisissez cette méthode de déploiement).
* **Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) en quelques minutes.
* **Quota de cœurs** -vous devrez peut-être le quota de hello tooincrease de cœurs, surtout si vous déployez plusieurs nœuds de cluster avec des tailles de machine virtuelle multicœurs. Si vous utilisez un modèle de démarrage rapide Azure, le quota de cœurs hello dans le Gestionnaire de ressources est par région Azure. Dans ce cas, vous devrez peut-être quota de hello tooincrease dans une région spécifique. Consultez [Abonnement Azure et limites, quotas et contraintes du service](../../azure-subscription-service-limits.md). tooincrease un quota, [ouvrir une demande de support client en ligne](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sans frais.
* **Licence Microsoft Office** : si vous déployez des nœuds de calcul à l’aide d’une image de machine virtuelle HPC Pack 2012 R2 de la Place de marché avec Microsoft Excel, une version d’évaluation de Microsoft Excel Professionnel Plus 2013 est installée et valable pendant 30 jours. Après la période d’évaluation hello, vous devez tooprovide une valide Microsoft Office licence tooactivate Excel toocontinue toorun les charges de travail. Consultez [Activation d’Excel](#excel-activation) plus loin dans cet article. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>Étape 1. Configuration d’un cluster HPC Pack dans Azure
Nous allons montrer deux tooset options cluster HPC Pack 2012 R2 de hello : première, à l’aide d’un modèle de démarrage rapide Azure et un hello portail Azure ; et, ensuite, à l’aide d’un script de déploiement d’Azure PowerShell.

### <a name="option-1-use-a-quickstart-template"></a>Option 1. Utilisation d’un modèle de démarrage rapide
Utilisez un tooquickly de modèle de démarrage rapide Azure déployer un cluster HPC Pack dans hello portail Azure. Lorsque vous ouvrez un modèle de hello dans le portail de hello, vous obtenez une interface utilisateur simple, où vous entrez des paramètres de hello pour votre cluster. Voici les étapes hello. 

> [!TIP]
> Si vous le souhaitez, utilisez un [modèle Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) qui crée un cluster similaire spécialement pour les charges de travail Excel. étapes de Hello est légèrement différentes des options suivantes hello.
> 
> 

1. Visitez hello [page modèle de création d’un Cluster HPC sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). Si vous le souhaitez, passez en revue les informations sur le modèle de hello et le code source de hello.
2. Cliquez sur **déployer tooAzure** toostart un déploiement avec le modèle hello Bonjour portail Azure.
   
   ![Déployer le modèle tooAzure][github]
3. Dans le portail de hello, suivez ces étapes tooenter hello les paramètres pour le modèle de cluster HPC hello.
   
   a. Sur hello **paramètres** page, entrez ou modifiez les valeurs des paramètres du modèle hello. (Cliquez sur le paramètre suivant tooeach hello icône pour les informations d’aide.) Exemples de valeurs sont affichés dans hello suivant l’écran. Cet exemple crée un cluster nommé *hpc01* Bonjour *hpc.local* domaine constitué d’un nœud principal et 2 nœuds de calcul. les nœuds de calcul Hello sont créés à partir d’une image de machine virtuelle HPC Pack qui inclut Microsoft Excel.
   
   ![Saisie des paramètres][parameters-new-portal]
   
   > [!NOTE]
   > machine virtuelle est créée automatiquement à partir de hello du nœud principal Hello [dernière image Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) de HPC Pack 2012 R2 sur Windows Server 2012 R2. Actuellement, les images hello sont basée sur HPC Pack 2012 R2 Update 3.
   > 
   > Machines virtuelles de nœud de calcul sont créés à partir de la dernière image de hello de famille de nœud de calcul hello sélectionné. Sélectionnez hello **ComputeNodeWithExcel** option pour hello dernière HPC Pack calcul nœud image qui inclut une version d’évaluation de Microsoft Excel Professionnel Plus 2013. toodeploy un cluster pour les sessions SOA générales ou pour le déchargement de l’UDF d’Excel, choisissez hello **ComputeNode** option (sans Excel installé).
   > 
   > 
   
   b. Choisissez un abonnement de hello.
   
   c. Créer un groupe de ressources de cluster de hello, tel que *hpc01RG*.
   
   d. Choisissez un emplacement pour le groupe de ressources hello, tels que du centre des États-Unis.
   
   e. Sur hello **juridiques** , lisez les termes du contrat de hello. Si vous les acceptez, cliquez sur **Acheter**. Ensuite, lorsque vous avez terminé la définition des valeurs hello pour le modèle de hello, cliquez sur **créer**.
4. Lorsque le déploiement de hello se termine (il prend généralement environ 30 minutes), exporter le fichier de certificat de cluster hello hello nœud principal du cluster. Dans une étape ultérieure, vous importez ce certificat public sur hello ordinateur tooprovide hello côté serveur, l’authentification du client pour la liaison HTTP sécurisée.
   
   a. Bonjour portail Azure, accédez à toohello du tableau de bord, nœud de tête hello sélectionnez, puis cliquez sur **Connect** haut hello hello tooconnect de page à l’aide du Bureau à distance.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Utilisez les procédures standard dans le Gestionnaire de certificats tooexport hello du nœud principal certificat (situé sous Cert : \LocalMachine\My) sans la clé privée de hello. Dans cet exemple, exportez *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Exporter le certificat de hello][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Option 2. Utilisez le script de déploiement de IaaS de HPC Pack hello
Hello script de déploiement IaaS de HPC Pack fournit une autre façon polyvalente toodeploy un cluster HPC Pack. Il crée un cluster dans le modèle de déploiement classique de hello, tandis que le modèle de hello utilise le modèle de déploiement du Gestionnaire de ressources Azure hello. En outre, le script de hello est compatible avec un abonnement dans hello Global Azure ou le service en Chine d’Azure.

**Autres composants requis**

* **Azure PowerShell** - [installez et configurez Azure PowerShell](/powershell/azure/overview) (version 0.8.10 ou ultérieure) sur votre ordinateur client.
* **Script de déploiement IaaS de HPC Pack** - Téléchargez et décompressez hello dernière version de script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Vérifier la version de hello du script de hello en exécutant `New-HPCIaaSCluster.ps1 –Version`. Cet article est basé sur la version 4.5.0 ou ultérieure de script de hello.

**Créer le fichier de configuration hello**

 Hello script de déploiement IaaS de HPC Pack utilise un fichier de configuration XML comme entrée qui décrit l’infrastructure de cluster HPC de hello hello. toodeploy un cluster constitué d’un nœud principal et 18 nœuds créés à partir de l’image de nœud de calcul hello qui inclut Microsoft Excel, remplacez les valeurs pour votre environnement en hello suivant l’exemple de fichier de configuration. Pour plus d’informations sur le fichier de configuration hello, consultez fichier Manual.rtf de hello dans le dossier de scripts hello et [créer un cluster HPC avec hello script de déploiement IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Remarques sur le fichier de configuration hello**

* Hello **VMName** de nœud principal de hello **doit** être même hello comme hello **ServiceName**, ou les travaux SOA échouent toorun.
* Veillez à spécifier **EnableWebPortal** afin que hello certificat du nœud principal est généré et exporté.
* fichier de Hello spécifie un script PowerShell de post-configuration PostConfig.ps1 qui s’exécute sur le nœud principal de hello. Hello script de l’exemple suivant configure la chaîne de connexion de stockage Windows Azure hello, supprime le rôle de nœud de calcul hello à partir du nœud principal hello et affiche tous les nœuds en ligne lorsqu’ils sont déployés. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Exécutez le script de hello**

1. Ouvrez la console PowerShell de hello sur l’ordinateur client de hello en tant qu’administrateur.
2. Modifier le dossier de scripts Active toohello (E:\IaaSClusterScript dans cet exemple).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. cluster de HPC Pack hello toodeploy, exécutez hello commande suivante. Cet exemple suppose que ce fichier de configuration hello se trouve dans E:\HPCDemoConfig.xml.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

Hello script de déploiement de HPC Pack s’exécute pendant un certain temps. Une chose du script hello est tooexport et télécharger le certificat de cluster hello et l’enregistrer dans le dossier Documents de l’utilisateur actuel hello sur l’ordinateur client de hello. script de Hello génère un similaire toohello suivante du message. Dans une étape suivante, vous importez les certificats hello dans le magasin de certificats approprié hello.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>Étape 2. Déchargement de classeurs Excel et exécution d’UDF à partir d'un client local
### <a name="excel-activation"></a>Activation d’Excel
Lorsque vous utilisez hello image ComputeNodeWithExcel VM pour les charges de production, vous devez tooprovide une valide Microsoft Office licence clé tooactivate Excel sur les nœuds de calcul hello. Sinon, version d’évaluation de hello d’Excel expire après 30 jours, et exécute des classeurs Excel échouent avec hello COMException (0x800AC472). 

Vous pouvez réarmer Excel 30 jours de la période d’évaluation : ouvrez une session sur le nœud principal de toohello et clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` sur Excel tous les nœuds via HPC Cluster Manager. Vous pouvez rallonger la période d’évaluation 2 fois au maximum. Ensuite, vous devez fournir une clé de licence Office valide.

Hello Office Professionnel Plus 2013 est installé sur l’image de machine virtuelle hello est une édition en volume avec une clé de licence Volume générique (GVLK). Vous pouvez l’activer par le biais du service de gestion de clés (KMS), de l’activation basée sur Active Directory (AD-BA) ou d’une clé d’activation multiple (MAK). 

    * toouse KMS/AD-BA, utiliser un serveur KMS existant ou en configurer une autre à l’aide de hello Volume License Pack pour Microsoft Office 2013. (Si vous le souhaitez, configurer hello serveur sur le nœud principal de hello.) Activez ensuite la clé d’hôte KMS hello via hello Internet ou par téléphone. Puis clusrun `ospp.vbs` tooset hello port et le serveur KMS et activer Office sur tous les nœuds de calcul Excel hello. 

    * toouse MAK, première clusrun `ospp.vbs` tooinput hello clé et puis activer tous les nœuds de calcul Excel hello via hello Internet ou par téléphone. 

> [!NOTE]
> Les clés de produit commercialisées pour Office Professionnel Plus 2013 ne peuvent pas être utilisées avec cette image de machine virtuelle. Si vous disposez de clés valides et d’un support d’installation pour des éditions Office ou Excel autres que cette édition en volume Office Professionnel Plus 2013 (édition de volume), vous pouvez également les utiliser. Tout d’abord désinstaller cette édition en volume et installer l’édition hello dont vous disposez. Hello réinstallé Excel de nœud de calcul peut être capturé en tant qu’un personnalisé toouse d’image de machine virtuelle dans un déploiement à grande échelle.
> 
> 

### <a name="offload-excel-workbooks"></a>Déchargement de classeurs Excel
Suivez ces toooffload étapes un classeur Excel afin qu’il s’exécute sur un cluster HPC Pack hello dans Azure. toodo, vous devez avoir Excel 2010 ou 2013 est déjà installé sur l’ordinateur client de hello.

1. Utilisez une des options de hello dans l’étape 1 toodeploy un cluster HPC Pack avec hello Excel image de nœud de calcul. Obtenir le fichier de certificat de cluster hello (.cer) et nom d’utilisateur du cluster et un mot de passe.
2. Sur l’ordinateur client de hello, importez le certificat de cluster de hello sous Cert : \CurrentUser\Root.
3. Assurez-vous qu'Excel est installé. Créer un fichier Excel.exe.config avec hello suivant contenu dans hello même dossier que Excel.exe sur l’ordinateur client de hello. Cette étape garantit que hello complément HPC Pack 2012 R2 Excel COM est chargé avec succès.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Configurer le cluster HPC Pack de hello client toosubmit travaux toohello. Une option consiste à hello toodownload complète [installation de HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) et installer hello HPC Pack client. Vous pouvez également télécharger et installer hello [les utilitaires clients HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) et hello approprié Visual C++ 2010 redistributable pour votre ordinateur ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. Dans cet exemple, nous utilisons un exemple de classeur Excel nommé ConvertiblePricing_Complete.xlsb. Vous pouvez le télécharger [ici](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Copiez le dossier de travail hello Excel classeur tooa tels que D:\Excel\Run.
7. Ouvrez le classeur Excel de hello. Sur hello **développer** du ruban, cliquez sur **compléments COM** et confirmez que hello HPC Pack Excel complément est chargé avec succès.
   
   ![Complément Excel pour HPC Pack][addin]
8. Lignes de commentaires modifier hello VBA macro HPCControlMacros dans Excel en modifiant hello comme indiqué dans le script suivant de hello. Remplacez les valeurs par celles appropriées pour votre environnement.
   
   ![Macro Excel pour HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Copiez hello Excel classeur tooan téléchargement répertoire tel que D:\Excel\Upload. Ce répertoire est spécifié dans la constante de HPC_DependsFiles hello dans la macro VBA de hello.
10. classeur de hello toorun sur cluster hello dans Azure, cliquez sur hello **Cluster** bouton sur la feuille de calcul hello.

### <a name="run-excel-udfs"></a>Exécution d’UDF Excel
toorun Excel UDF, suivez hello étapes précédentes tooset de 1 à 3 d’ordinateur du client hello. Pour Excel UDF, vous n’avez pas besoin toohave hello Excel application installée sur les nœuds de calcul. Par conséquent, lors de la création de votre cluster de nœuds de calcul, vous pouvez choisir une image de nœud de calcul normal au lieu de hello calcul image de nœud avec Excel.

> [!NOTE]
> Il existe une limite de 34 caractères Bonjour Excel 2010 et de la boîte de dialogue de connecteur de cluster 2013. Vous utilisez ce cluster hello toospecify boîte dialogue qui s’exécute hello UDF. Si le nom de cluster complet hello est plus long (par exemple, hpcexcelhn01.southeastasia.cloudapp.azure.com), il ne tient pas dans la boîte de dialogue hello. Bonjour solution de contournement est tooset une variable de l’échelle de l’ordinateur comme *CCP_IAASHN* avec la valeur hello du nom de cluster long hello. Ensuite, entrez *CCP_IAASHN %* dans la boîte de dialogue hello en tant que nom de nœud principal de cluster hello. 
> 
> 

Une fois le cluster de hello est déployé, poursuivre hello suivant les étapes toorun intégré exemple Excel UDF. Pour des UDF Excel personnalisées, consultez ces [ressources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLL et les déployer sur un cluster IaaS de hello.

1. Ouvrez un nouveau classeur Excel. Sur hello **développer** du ruban, cliquez sur **compléments**. Puis, dans la boîte de dialogue hello, cliquez sur **Parcourir**, accédez toohello %CCP_HOME%Bin\XLL32 dossier et sélectionnez l’exemple hello ClusterUDF32.xll. Si hello ClusterUDF32 n’existe pas sur l’ordinateur client de hello, copiez-le à partir du dossier %CCP_HOME%Bin\XLL32 hello sur le nœud principal de hello.
   
   ![Sélectionnez hello UDF][udf]
2. Cliquez sur **Fichier** > **Options** > **Avancé**. Sous **formules**, vérifiez **autoriser toorun de fonctions XLL définies par l’utilisateur à un cluster de calcul**. Puis cliquez sur **Options** et entrez le nom du cluster complète hello dans **nom de nœud principal de Cluster**. (Comme indiqué précédemment cette zone d’entrée étant limité too34 caractères, un nom de cluster long peut ne pas correspond. Vous pouvez utiliser des variables au niveau de la machine ici pour les noms de cluster longs.)
   
   ![Configurer hello UDF][options]
3. toorun hello calcul UDF sur le cluster de hello, cliquez sur la cellule hello avec la valeur =XllGetComputerNameC() et appuyez sur ENTRÉE. fonction Hello extrait simplement le nom hello du nœud de calcul hello sur quel hello UDF s’exécute. Pourquoi exécuter tout d’abord, une boîte de dialogue informations d’identification demande hello nom d’utilisateur et mot de passe tooconnect toohello cluster IaaS.
   
   ![Exécution de l’UDF][run]
   
   Lorsqu’il existe de nombreuses cellules toocalculate, appuyez sur Ctrl-Maj-Alt + de calcul de hello toorun F9 sur toutes les cellules.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>Étape 3. Exécution d’une charge de travail SOA depuis un client local
les applications SOA générales toorun sur un cluster IaaS HPC Pack de hello, utilisez d’abord une des méthodes de hello dans un cluster de hello toodeploy étape 1. Spécifiez une image de nœud de calcul générique dans ce cas, étant donné que vous n’avez pas besoin d’Excel sur les nœuds de calcul hello. Puis, procédez comme suit.

1. Après avoir récupéré le certificat de cluster hello, vous devez l’importer sur l’ordinateur client de hello sous Cert : \CurrentUser\Root.
2. Installer hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) et [les utilitaires clients HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923). Ces outils vous toodevelop et exécutent des applications clientes SOA.
3. Télécharger hello HelloWorldR2 [exemple de code](https://www.microsoft.com/download/details.aspx?id=41633). Ouvrez hello HelloWorldR2.sln dans Visual Studio 2010 ou 2012. (Cet exemple n’est pas compatible actuellement avec les versions plus récentes de Visual Studio).
4. Générez le projet EchoService de hello tout d’abord. Ensuite, déployez le cluster IaaS de hello service toohello Bonjour même façon que vous déployez tooan local cluster. Pour des instructions détaillées, consultez hello Lisezmoi.doc dans HelloWordR2. Modifier et générer hello HellWorldR2 et autres projets, comme décrit dans hello suivant la section toogenerate hello SOA les applications clientes qui s’exécutent sur un cluster IaaS Azure.

### <a name="use-http-binding-with-azure-storage-queue"></a>Utilisation de la liaison HTTP avec la file d'attente de stockage Azure
liaison Http de toouse avec une file d’attente de stockage Azure, apporter quelques modifications toohello exemple de code.

* Nom de cluster hello mise à jour.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* Si vous le souhaitez, utilisez la valeur par défaut de hello TransportScheme dans SessionStartInfo ou définir explicitement tooHttp.

```
    info.TransportScheme = TransportScheme.Http;
```

* Utilisez la liaison par défaut pour hello BrokerClient.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    Ou définies explicitement à l’aide de hello basicHttpBinding.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* Vous pouvez également définir hello UseAzureQueue indicateur tootrue dans SessionStartInfo. Si ce n’est pas le cas, ensemble, elle est définie tootrue par défaut lors de nom de cluster hello possède des suffixes de domaine Azure et hello TransportScheme est Http.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Utilisation de la liaison HTTP sans la file d'attente de stockage Azure
liaison Http de toouse sans une file d’attente de stockage Azure, explicitement ensemble hello UseAzureQueue indicateur toofalse Bonjour SessionStartInfo.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>Utilisation de la liaison NetTcp
toouse NetTcp liaison, configuration de hello est cluster local de tooan similaire tooconnecting. Vous devez tooopen quelques points de terminaison sur la machine virtuelle du nœud principal hello. Si vous avez utilisé le cluster de hello IaaS HPC Pack déploiement script toocreate hello, par exemple, jeu de points de terminaison hello dans hello portail Azure comme suit.

1. Arrêter hello machine virtuelle.
2. Ajouter des ports TCP hello 9090, 9087, 9091, 9094 pour hello Session, service Broker, service Broker de traitement et de services de données, respectivement
   
    ![Configuration des points de terminaison][endpoint-new-portal]
3. Démarrez hello machine virtuelle.

Hello application cliente SOA ne nécessite aucune modification à l’exception de la modification hello principal toohello IaaS cluster nom complet.

## <a name="next-steps"></a>Étapes suivantes
* Consultez [ces ressources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) pour plus d'informations sur l'exécution de charges de travail Excel avec HPC Pack.
* Consultez [Gestion des Services SOA dans Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) pour plus d'informations sur le déploiement et la gestion des services SOA avec HPC Pack.

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
