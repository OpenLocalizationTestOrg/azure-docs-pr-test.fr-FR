---
title: "aaaCreate HDInsight clusters avec Data Lake Store en tant que de stockage par défaut à l’aide de PowerShell | Des documents Microsoft"
description: Utiliser Azure PowerShell toocreate et utiliser des clusters HDInsight avec Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Créer des clusters HDInsight avec Data Lake Store comme stockage par défaut à l’aide de PowerShell
> [!div class="op_single_selector"]
> * [Utilisez hello portail Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Utiliser PowerShell (pour le stockage par défaut)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Utiliser PowerShell (pour le stockage supplémentaire)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Utiliser Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Découvrez comment toouse Azure PowerShell tooconfigure Azure HDInsight clusters avec Azure Data Lake Store en tant que stockage de la valeur par défaut. Pour obtenir des instructions sur la création d’un cluster HDInsight avec Data Lake Store comme stockage supplémentaire, consultez [Créer un cluster HDInsight avec Data Lake Store en tant que stockage supplémentaire](data-lake-store-hdinsight-hadoop-use-powershell.md).

Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :

* clusters de HDInsight Hello option toocreate avec un accès tooData Lake Store en tant que stockage de la valeur par défaut est disponible pour HDInsight version 3.5 et 3.6.

* toocreate d’option Hello des clusters HDInsight avec accès tooData Lake Store car le stockage de la valeur par défaut est *non disponible* pour les clusters HDInsight Premium.

tooconfigure toowork de HDInsight avec Data Lake Store à l’aide de PowerShell, suivez les instructions de hello dans les cinq sections hello.

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, assurez-vous que vous remplissez hello suivant les exigences :

* **Un abonnement Azure**: accédez trop[version d’évaluation gratuite de Azure d’obtenir](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 ou supérieur**: consultez [comment tooinstall et configurez PowerShell](/powershell/azure/overview).
* **Kit de développement logiciel (SDK) Windows**: tooinstall Kit de développement logiciel Windows, accédez trop[téléchargements et outils pour Windows 10](https://dev.windows.com/en-us/downloads). Hello SDK est toocreate utilisé un certificat de sécurité.
* **Principal du service Azure Active Directory**: ce didacticiel explique comment toocreate un principal de service dans Azure Active Directory (Azure AD). Toutefois, de le toocreate un principal de service, vous devez être un administrateur Azure AD. Si vous êtes un administrateur, vous pouvez ignorer cette condition préalable et poursuivre le didacticiel de hello.

    >[!NOTE]
    >Vous pouvez créer un principal de service uniquement si vous être administrateur Azure AD. Votre administrateur Azure AD doit créer un principal de service. Vous pouvez ensuite créer un cluster HDInsight avec Data Lake Store. Hello principal de service doit être créé avec un certificat, comme décrit dans [créer un principal de service avec certificat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Créer un compte Data Lake Store
toocreate un compte Data Lake Store, procédez comme hello suivant :

1. À partir de votre bureau, ouvrez une fenêtre PowerShell, puis entrez des extraits de code hello ci-dessous. Lorsque vous avez demandée toosign dans, connectez-vous en tant qu’un des administrateurs d’abonnements hello ou propriétaires. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Si vous inscrivez le fournisseur de ressources Data Lake Store hello et que vous recevez un message d’erreur similaire trop`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, votre abonnement est peut-être pas dans la liste approuvée pour Data Lake Store. tooenable votre abonnement Azure pour hello Data Lake Store public preview, suivez les instructions de hello dans [prise en main Azure Data Lake Store à l’aide de hello Azure portal](data-lake-store-get-started-portal.md).
    >

2. Un compte Data Lake Store est associé à un groupe de ressources Azure. Commencez par créer un groupe de ressources.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Vous devriez obtenir un résultat similaire à ceci :

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Créez un compte Data Lake Store. compte Hello nom que vous spécifiez doit contenir uniquement des lettres minuscules et chiffres.

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

4. À l’aide de Data Lake Store en tant que stockage par défaut nécessite toospecify qu'un fichiers spécifiques à un cluster hello de toowhich de chemin d’accès racine sont copiés au cours de la création du cluster. toocreate un chemin d’accès racine, qui est **hdiadlcluster/clusters** dans l’extrait de code hello, utilisez hello suivant d’applets de commande :

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Configurer l’authentification dans en fonction du rôle d’accès tooData Lake Store
Chaque abonnement Azure est associé à une entité Azure AD. Les utilisateurs et les services que les accès aux ressources de l’abonnement à l’aide de hello portail Azure ou hello API Azure Resource Manager doivent tout d’abord s’authentifier auprès d’Azure AD. L’accès est accordé tooAzure abonnements et services en leur attribuant le rôle approprié de hello sur une ressource Azure. Pour les services, un principal du service identifie le service de hello dans Azure AD.

Cette section illustre comment toogrant une application de service, telles que HDInsight, tooan d’accès aux ressources Azure (hello compte Data Lake Store que vous avez créé précédemment). Pour faire en créant un service principal pour l’application hello et en assignant des tooit rôles via PowerShell.

tooset l’authentification Active Directory pour Azure Data Lake, effectuer hello hello les deux sections suivantes.

### <a name="create-a-self-signed-certificate"></a>Créer un certificat auto-signé
Assurez-vous que vous avez [Kit de développement logiciel Windows](https://dev.windows.com/en-us/downloads) installé avant de poursuivre la hello étapes de cette section. Vous devez également créer un répertoire, tel que *C:\mycertdir*, où vous créez le certificat de hello.

1. À partir de la fenêtre de PowerShell hello, accédez à emplacement toohello où vous avez installé le Kit de développement logiciel Windows (en général, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) et utiliser hello [MakeCert] [ makecert] utilitaire toocreate un certificat auto-signé et une clé privée. Utilisez hello suivant de commandes :

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Vous serez invité à tooenter hello privée clé mot de passe. Une fois la commande hello est exécuté avec succès, vous devez voir **CertFile.cer** et **mykey.pvk** dans le répertoire de certificats hello que vous avez spécifié.
2. Hello d’utilisation [Pvk2Pfx] [ pvk2pfx] utilitaire tooconvert hello .pvk et .cer fichiers fichier .pfx créé tooa MakeCert. Exécutez hello de commande suivante :

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Lorsque vous êtes invité, entrez hello privée clé mot de passe que vous avez spécifié précédemment. Hello valeur que vous spécifiez pour hello **- bon de commande** paramètre est un mot de passe hello a associé à un fichier .pfx de hello. Une fois la commande hello est terminée avec succès, vous devez également voir un **CertFile.pfx** dans le répertoire de certificats hello que vous avez spécifié.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Créer une application Azure AD et un principal de service
Dans cette section, vous créez un principal de service pour une application Azure AD, attribuer un principal de service de rôle toohello et authentifiez-vous en tant que principal du service hello en fournissant un certificat. toocreate une application dans Azure AD, exécutez hello suivant de commandes :

1. Collez hello suivant d’applets de commande dans la fenêtre de console PowerShell hello. Assurez-vous que cette valeur hello que vous spécifiez pour hello **- DisplayName** propriété est unique. Hello pour les valeurs **- page d’accueil** et **- IdentiferUris** sont des valeurs d’espace réservé et ne sont pas vérifiées.

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
2. Créez un principal de service à l’aide de l’ID application hello.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Accordez le racine Data Lake Store toohello hello service accès principal et tous les dossiers hello dans le chemin d’accès racine hello que vous avez spécifié précédemment. Utilisez hello suivant d’applets de commande :

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Créer un cluster HDInsight Linux avec Data Lake Store en tant que stockage par défaut de hello

Dans cette section, vous créez un cluster HDInsight Hadoop Linux avec Data Lake Store comme stockage par défaut de hello. Pour cette version, hello cluster HDInsight et Data Lake Store doit être Bonjour même emplacement.

1. Extraire l’ID de client d’abonnement hello et stockez-le toouse plus tard.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Créer le cluster HDInsight de hello à l’aide de hello suivant d’applets de commande :

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Une fois que l’applet de commande hello est terminée, vous devez voir une sortie qui répertorie les détails du cluster hello.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Exécuter les tâches de test sur hello HDInsight cluster toouse Data Lake Store
Après avoir configuré un cluster HDInsight, vous pouvez exécuter les travaux test dessus tooensure qu’il peut accéder à Data Lake Store. toodo donc exécuter un toocreate de travail Hive exemple une table qui utilise les données d’exemple hello qui sont déjà disponibles dans Data Lake Store à  *<cluster root>/example/data/sample.log*.

Dans cette section, vous établissez une connexion Secure Shell (SSH) dans hello cluster HDInsight Linux que vous avez créé, puis vous exécutez un exemple de requête Hive.

* Si vous utilisez un toomake de client Windows à une connexion SSH en cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Si vous utilisez un toomake de client à une connexion SSH en cluster de hello Linux, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. Une fois que vous avez effectué la connexion de hello, démarrer une interface de ligne hello Hive (CLI) à l’aide de hello de commande suivante :

        hive
2. Utilisez Bonjour CLI tooenter Bonjour suivant les instructions toocreate une nouvelle table nommée **véhicules** à l’aide des données d’exemple hello dans Data Lake Store :

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Vous devez voir le résultat de la requête hello sur la console SSH hello.

    >[!NOTE]
    >Bonjour chemin d’accès toohello échantillon de données hello précédant la commande CREATE TABLE est `adl:///example/data/`, où `adl:///` est hello cluster racine. Exemple hello de la racine du cluster hello qui est spécifiée dans ce didacticiel, commande hello est `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. Vous pouvez utiliser d’alternative plus courte hello ou fournir la racine du cluster toohello hello chemin d’accès complet.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Accéder à Data Lake Store avec les commandes HDFS
Une fois que vous avez configuré le cluster HDInsight de hello toouse Data Lake Store, vous pouvez utiliser le système de fichiers distribués Hadoop (HDFS) shell commandes tooaccess hello magasin.

Dans cette section, vous effectuez une connexion SSH en hello cluster HDInsight Linux que vous avez créé, puis vous exécutez les commandes HDFS hello.

* Si vous utilisez un toomake de client Windows à une connexion SSH en cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Si vous utilisez un toomake de client à une connexion SSH en cluster de hello Linux, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

Une fois que vous avez effectué la connexion de hello, répertorient les fichiers de hello dans Data Lake Store à l’aide de hello suivant de commande de système de fichiers HDFS.

    hdfs dfs -ls adl:///

Vous pouvez également utiliser hello `hdfs dfs -put` commande tooupload certains fichiers tooData Lake Store, puis utilisez `hdfs dfs -ls` tooverify indique si les fichiers de hello ont été téléchargés avec succès.

## <a name="see-also"></a>Voir aussi
* [Portail Azure : créer un toouse du cluster HDInsight Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
