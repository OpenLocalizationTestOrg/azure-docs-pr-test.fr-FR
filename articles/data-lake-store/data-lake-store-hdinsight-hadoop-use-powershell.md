---
titre : aaa « PowerShell : cluster Azure HDInsight avec Data Lake Store en tant que stockage complémentaire | Les services Microsoft Docs » : data lake store, hdinsight documentationcenter : '' auteur : Gestionnaire de nitinme : jhubbard éditeur : cgronlun

MS.AssetId : 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service : magasin de données lake ms.devlang : na ms.topic : article ms.tgt_pltfrm : na ms.workload : ms.date de données volumineuses : 06/08/2017 ms.author : nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>Utiliser Azure PowerShell toocreate un cluster HDInsight avec Data Lake Store (en tant que stockage supplémentaire)
> [!div class="op_single_selector"]
> * [Utilisation du portail](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Utilisation de PowerShell (pour le stockage par défaut)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Utilisation de PowerShell (pour le stockage supplémentaire)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Utilisation du gestionnaire des ressources](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Découvrez comment toouse Azure PowerShell tooconfigure un HDInsight de cluster avec Azure Data Lake Store **en tant que stockage supplémentaire**. Pour savoir comment toocreate un HDInsight de cluster avec Azure Data Lake Store en tant que stockage par défaut, consultez [créer un cluster HDInsight avec Data Lake Store en tant que stockage de la valeur par défaut](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).

> [!NOTE]
> Si vous vous apprêtez toouse Azure Data Lake Store en tant que stockage supplémentaire pour le cluster HDInsight, nous vous recommandons vivement de procéder ainsi lorsque vous créez le cluster de hello comme décrit dans cet article. Ajout d’Azure Data Lake Store en tant que stockage supplémentaire tooan cluster HDInsight existant est un processus complexe et susceptible d’engendrer des tooerrors.
>

Pour les types de clusters pris en charge, Data Lake Store est utilisé comme compte de stockage par défaut ou supplémentaire. Lorsque Data Lake Store est utilisé comme espace de stockage supplémentaire, compte de stockage par défaut hello pour les clusters de hello sera toujours les objets BLOB de stockage Azure (WASB) et fichiers hello cluster (par exemple, les journaux, etc.) sont toujours enregistrées toohello du stockage par défaut, lors des données hello que vous avez choix tooprocess peuvent être stockées dans un compte Data Lake Store. À l’aide de Data Lake Store en tant qu’un compte de stockage supplémentaires n’affecte pas les performances ou le stockage de toohello hello capacité tooread/écriture à partir du cluster de hello.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Utilisation de Data Lake Store pour le stockage de cluster HDInsight

Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :

* Clusters de HDInsight option toocreate avec un accès tooData Lake Store en tant que stockage supplémentaire est disponible pour les versions 3.2, 3.4, 3.5 et 3.6 de HDInsight.

La configuration HDInsight toowork avec Data Lake Store à l’aide de PowerShell implique de hello comme suit :

* Créer un Azure Data Lake Store
* Configurer l’authentification dans en fonction du rôle d’accès tooData Lake Store
* Créer un cluster HDInsight avec authentification tooData Lake Store
* Exécuter une tâche de test sur le cluster de hello

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 ou version ultérieure**. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
* **Kit de développement logiciel (SDK) Windows**. Vous pouvez l’installer à partir d’ [ici](https://dev.windows.com/en-us/downloads). Vous utilisez ce toocreate un certificat de sécurité.
* **Principal du service Azure Active Directory**. Étapes de ce didacticiel fournissent des instructions sur la façon de toocreate un principal de service dans Azure AD. Toutefois, vous devez être un toocreate en mesure de Azure AD administrateur toobe un principal de service. Si vous êtes un administrateur Azure AD, vous pouvez ignorer cette condition préalable et poursuivre le didacticiel de hello.

    **Si vous n’êtes pas un administrateur Azure AD**, vous ne serez pas en mesure de tooperform hello étapes requises toocreate un principal de service. Dans ce cas, votre administrateur Azure AD doit d’abord créer un principal du service. Vous pourrez ensuite créer un cluster HDInsight avec Data Lake Store. En outre, hello principal du service doit être créé à l’aide d’un certificat, comme décrit dans [créer un principal de service avec certificat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-azure-data-lake-store"></a>Créer un Azure Data Lake Store
Suivez ces étapes de toocreate un Data Lake Store.

1. À partir de votre bureau, ouvrez une nouvelle fenêtre Azure PowerShell et entrez hello suivant extrait de code. Toolog demandée, assurez-vous que vous vous connectez comme administrateur/propriétaire de l’abonnement hello :

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > Si vous recevez un message d’erreur similaire trop`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` lorsque vous inscrivez le fournisseur de ressources Data Lake Store hello, il est possible que votre abonnement n’est pas dans la liste approuvée pour Azure Data Lake Store. Veillez à activer votre abonnement Azure pour la version préliminaire publique de Data Lake Store en suivant ces [instructions](data-lake-store-get-started-portal.md).
   >
   >
2. Un compte Azure Data Lake Store est associé à un groupe de ressources Azure. Commencez par créer un groupe de ressources Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Vous devriez obtenir un résultat similaire à ceci :

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Créer un compte Azure Data Lake Store. compte Hello nom que vous spécifiez doit contenir uniquement des lettres minuscules et chiffres.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Vous devez voir une sortie semblable à hello suivante :

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. Télécharger certaines tooAzure de données exemple lac de données. Nous l’utiliserons plus loin dans cette tooverify article que les données de salutation sont accessibles à partir d’un cluster HDInsight. Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Configurer l’authentification dans en fonction du rôle d’accès tooData Lake Store
Chaque abonnement Azure est associé à un Azure Active Directory. Les utilisateurs et services qui accèdent aux ressources d’abonnement hello à l’aide de hello portail classique Azure ou des API Azure Resource Manager doivent s’authentifier avec Azure Active Directory. L’accès est accordé tooAzure abonnements et services en leur attribuant le rôle approprié de hello sur une ressource Azure.  Pour les services, un principal du service identifie le service hello Bonjour Azure Active Directory (AAD). Cette section illustre comment toogrant une application de service, telles que HDInsight, tooan d’accès aux ressources Azure (hello compte Azure Data Lake Store créé précédemment) en créant un principal de service pour l’application hello et en assignant des toothat rôles via Azure PowerShell.

tooset l’authentification Active Directory pour Azure Data Lake, vous devez effectuer hello tâches suivantes.

* Créer un certificat auto-signé
* Créer une application dans Azure Active Directory et un principal du service

### <a name="create-a-self-signed-certificate"></a>Créer un certificat auto-signé
Assurez-vous que vous avez [Kit de développement logiciel Windows](https://dev.windows.com/en-us/downloads) installé avant de poursuivre la hello étapes de cette section. Vous devez également créer un répertoire, tel que **C:\mycertdir**, où hello certificat sera créé.

1. À partir de la fenêtre Windows PowerShell de hello, accédez à emplacement toohello où vous avez installé le Kit de développement logiciel Windows (en général, `C:\Program Files (x86)\Windows Kits\10\bin\x86` et utiliser hello [MakeCert] [ makecert] utilitaire toocreate un certificat auto-signé et un clé privée. Utilisez hello suivant les commandes.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Vous serez invité à tooenter hello privée clé mot de passe. Une fois la commande hello est correctement exécutée, vous devez voir un **CertFile.cer** et **mykey.pvk** dans le répertoire de certificat hello spécifié.
2. Hello d’utilisation [Pvk2Pfx] [ pvk2pfx] utilitaire tooconvert hello .pvk et .cer fichiers fichier .pfx créé tooa MakeCert. Exécutez hello commande suivante.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Lorsque vous y êtes invité Entrez le mot de passe clé privée hello vous avez spécifié précédemment. Hello valeur que vous spécifiez pour hello **- bon de commande** paramètre est un mot de passe hello qui est associé au fichier .pfx de hello. Une fois la commande hello terminée avec succès, vous devez également voir un CertFile.pfx dans le répertoire de certificat hello spécifié.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Créer une application Azure Active Directory et un principal du service
Dans cette section, vous effectuez hello étapes toocreate un principal de service pour une application Azure Active Directory, attribuer un principal de service de rôle toohello et s’authentifier en tant que principal du service hello en fournissant un certificat. Exécutez hello suivant de commandes toocreate une application dans Azure Active Directory.

1. Collez hello suivant d’applets de commande dans la fenêtre de console PowerShell hello. Vous spécifiez pour hello assurer qu’une valeur hello **- DisplayName** propriété est unique. Hello en outre, les valeurs pour **- page d’accueil** et **- IdentiferUris** sont des valeurs d’espace réservé et ne sont pas vérifiées.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Créer un principal de service à l’aide des ID d’application hello.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Accordez le dossier Data Lake Store toohello hello service principal l’accès et fichier hello sera accessible à partir de cluster HDInsight de hello. extrait de code Hello ci-dessous fournit racine toohello accès hello Data Lake Store (où vous avez copié le fichier de données d’exemple hello) de compte et hello fichier lui-même.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Créer un cluster Linux HDInsight avec Data Lake Store comme stockage par supplémentaire

Dans cette section, nous créons un cluster HDInsight Hadoop Linux avec Data Lake Store comme stockage supplémentaire. Pour cette version, le cluster HDInsight de hello et hello Data Lake Store doivent être Bonjour même emplacement.

1. Commencer la récupération hello ID client d’abonnement. Vous en aurez besoin ultérieurement.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. Pour cette version, pour un cluster Hadoop, Data Lake Store peut uniquement servir en tant qu’un stockage supplémentaire pour le cluster de hello. stockage par défaut de Hello sera toujours les objets BLOB de stockage Azure hello (WASB). Par conséquent, nous allons tout d’abord créer hello conteneurs du compte et le stockage de stockage requis pour le cluster de hello.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Créer un cluster HDInsight de hello. Utilisez hello suivant d’applets de commande.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Une fois que l’applet de commande hello terminée avec succès, vous devez voir une sortie d’affichage des détails du cluster hello.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Exécuter les tâches de test sur Bonjour HDInsight cluster toouse Bonjour Data Lake Store
Après avoir configuré un cluster HDInsight, vous pouvez exécuter les travaux test sur hello cluster tootest que hello HDInsight peut accéder à Data Lake Store. toodo par conséquent, nous allons exécuter un travail Hive exemple qui crée une table à l’aide des données d’exemple hello que vous avez téléchargé antérieures tooyour Data Lake Store.

Dans cette section, vous allez SSH dans hello HDInsight Linux cluster que vous avez créé et exécuté hello un exemple de requête Hive.

* Si vous utilisez un tooSSH de client Windows dans un cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Si vous utilisez un tooSSH de client Linux dans un cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. Une fois connecté, démarrer hello CLI de la ruche à l’aide de hello de commande suivante :

        hive
2. À l’aide de hello CLI, entrez hello suivant les instructions toocreate une nouvelle table nommée **véhicules** à l’aide des données d’exemple hello Bonjour Data Lake Store :

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    Vous devez voir s’afficher une sortie similaire toohello :

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a>Accéder à Data Lake Store avec les commandes HDFS
Une fois que vous avez configuré le cluster HDInsight de hello toouse Data Lake Store, vous pouvez utiliser hello HDFS shell commandes tooaccess hello magasin.

Dans cette section, vous allez SSH dans hello HDInsight Linux cluster que vous avez créé et exécuter des commandes HDFS hello.

* Si vous utilisez un tooSSH de client Windows dans un cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Si vous utilisez un tooSSH de client Linux dans un cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

Une fois connecté, utilisez hello suivant fichiers HDFS filesystem commande toolist hello Bonjour Data Lake Store.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

Elle doit répertorier fichier hello que vous avez téléchargé antérieures toohello Data Lake Store.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

Vous pouvez également utiliser hello `hdfs dfs -put` commande tooupload certains toohello fichiers Data Lake Store, puis utilisez `hdfs dfs -ls` tooverify indique si les fichiers de hello ont été téléchargés avec succès.

## <a name="see-also"></a>Voir aussi
* [Portail : Créer un toouse du cluster HDInsight Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
