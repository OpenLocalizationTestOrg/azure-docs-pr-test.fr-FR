---
title: aaaUsing Azure PowerShell avec le stockage Azure | Documents Microsoft
description: "Découvrez comment toouse hello applets de commande Azure PowerShell pour Azure Storage toocreate et gérer les comptes de stockage ; travailler avec des objets BLOB, les tables, les files d’attente et les fichiers ; configurer et de requête analytique de stockage et créent des signatures d’accès partagé."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Utilisation d'Azure PowerShell avec Azure Storage
## <a name="overview"></a>Vue d'ensemble
Azure PowerShell est un module qui fournit des applets de commande toomanage Azure via Windows PowerShell. Il s'agit d'un interpréteur de ligne de commande et d'un langage de script basé sur des tâches, conçu spécialement pour l'administration système. Avec PowerShell, vous pouvez facilement contrôler et automatiser l’administration hello de vos services et applications Azure. Par exemple, vous pouvez utiliser Bonjour applets de commande tooperform Bonjour même tâches que vous pouvez effectuer via hello [portail Azure](https://portal.azure.com).

Dans ce guide, nous allons examiner comment toouse hello [applets de commande de stockage Azure](/powershell/module/azurerm.storage/#storage) tooperform diverses tâches de développement et d’administration avec le stockage Azure.

Ce guide part du principe que vous avez une certaine expérience en tant qu’utilisateur d’[Azure Storage](https://azure.microsoft.com/documentation/services/storage/) et de [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). guide de Hello fournit un nombre de scripts hello de toodemonstrate l’utilisation de PowerShell avec le stockage Azure. Vous devez mettre à jour les variables de script hello en fonction de votre configuration avant d’exécuter chaque script.

Hello première section de ce guide fournit un aperçu rapide au stockage Azure et PowerShell. Pour plus d’informations et des instructions, démarrer à partir de hello [conditions préalables à l’aide d’Azure PowerShell avec le stockage Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Prise en main d'Azure Storage et de PowerShell en 5 minutes
Cette section vous montre comment tooaccess le stockage Azure via PowerShell dans 5 minutes.

**Nouvelle tooAzure :** obtenir un abonnement Microsoft Azure et un compte Microsoft associé à cet abonnement. Pour en savoir plus sur les options d’achat de Microsoft Azure, voir [Essai gratuit](https://azure.microsoft.com/pricing/free-trial/), [Options d’achat](https://azure.microsoft.com/pricing/purchase-options/) et [Offres spéciales membres](https://azure.microsoft.com/pricing/member-offers/) (pour les membres de MSDN, Microsoft Partner Network et BizSpark, ainsi que d’autres programmes Microsoft).

Pour plus d’informations sur les abonnements Azure, consultez la section [Attribution de rôles d’administrateur dans Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .

**Une fois le compte et l’abonnement à Microsoft Azure créés :**

1. Télécharger et installer les dernières hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Démarrer Windows PowerShell Scripting environnement intégré (ISE) : Sur votre ordinateur local, accédez à toohello **Démarrer** menu. Type **outils d’administration** sur toorun il. Bonjour **outils d’administration** fenêtre, avec le bouton droit **Windows PowerShell ISE**, cliquez sur **exécuter en tant qu’administrateur**.
3. Dans **Windows PowerShell ISE**, cliquez sur **fichier** > **nouveau** toocreate un fichier de script.
4. Maintenant, nous donnons un script simple qui montre la base tooaccess de commandes PowerShell Azure Storage. script de Hello sera tout d’abord demander à votre tooadd d’informations d’identification de compte Azure votre environnement PowerShell local de compte Azure toohello. Ensuite, hello script définir la valeur par défaut de hello abonnement Azure et créez un compte de stockage dans Azure. Ensuite, hello script créer un conteneur dans ce nouveau compte de stockage et télécharger un conteneur de toothat (blob) de fichier image existant. Une fois le script de hello répertorie tous les objets BLOB dans le conteneur, elle crée un nouveau répertoire de destination dans votre ordinateur local et télécharger le fichier d’image hello.
5. Bonjour suivant la section de code, sélectionnez le script de hello entre la section Notes hello **#begin** et **#end**. Appuyez sur CTRL + C toocopy il toohello Presse-papiers.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. Dans **Windows PowerShell ISE**, appuyez sur le script de hello toocopy CTRL + V. Cliquez sur **Fichier** > **Enregistrer**. Bonjour **Enregistrer sous** boîte de dialogue, entrez un nom hello du fichier de script hello, tels que « mystoragescript ». Cliquez sur **Enregistrer**.
7. Maintenant, vous devez les variables de script tooupdate hello en fonction de vos paramètres de configuration. Vous devez mettre à jour hello **$SubscriptionName** variable avec votre propre abonnement. Vous pouvez conserver les autres variables comme spécifié dans le script de hello hello ou les mettre à jour que vous le souhaitez.
   
   * **$SubscriptionName :** vous devez mettre à jour cette variable avec le nom de votre propre abonnement. Suivez l’une des hello suivant trois nom hello toolocate de façons de votre abonnement :
     
    a. Dans **Windows PowerShell ISE**, cliquez sur **fichier** > **nouveau** toocreate un fichier de script. Suivant de hello copie toohello nouveau fichier de script de script et cliquez sur **déboguer** > **exécuter**. Hello script suivant sera tout d’abord demander votre tooadd d’informations d’identification de compte Azure à votre environnement PowerShell local de compte Azure toohello et présentent ensuite tous les abonnements hello session PowerShell locale de toohello connecté. Notez une hello nom d’abonnement de hello que vous souhaitez toouse en suivant ce didacticiel :
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. toolocate et copiez votre abonnement nom Bonjour [portail Azure](https://portal.azure.com)hello menu Hub sur hello gauche, cliquez sur dans **abonnements**. Copiez hello nom de l’abonnement que vous souhaitez toouse lors de l’exécution des scripts de hello dans ce guide.
     
     ![Portail Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. toolocate et copiez votre abonnement nom Bonjour [portail classique Azure](https://manage.windowsazure.com/), faites défiler la liste et cliquez sur **paramètres** sur hello gauche du portail de hello. Cliquez sur **abonnements** toosee une liste de vos abonnements. Nom de hello copie d’abonnement que vous souhaitez toouse lors de l’exécution des scripts hello donnés dans ce guide.
     
     ![portail Azure Classic](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName :** utiliser hello attribué dans le script de hello ou entrez un nouveau nom pour votre compte de stockage. **Important :** nom hello hello du compte de stockage doit être unique dans Azure. Il doit également inclure des minuscules uniquement.
   * **$Location :** hello donné « Ouest des États-Unis » dans le script de hello ou sélectionnez d’autres emplacements de Azure, tels que les États-Unis, Europe du Nord et ainsi de suite.
   * **$ContainerName :** utiliser hello attribué dans le script de hello ou entrez un nouveau nom pour votre conteneur.
   * **$ImageToUpload :** saisir une image de tooa de chemin d’accès sur votre ordinateur local, tel que : « C:\Images\HelloWorld.png ».
   * **$DestinationFolder :** Entrez un chemin d’accès tooa répertoire local toostore les fichiers téléchargés depuis le stockage Azure, telles que : « C:\DownloadImages ».
8. Après la mise à jour les variables de script hello dans le fichier de « mystoragescript.ps1 » hello, cliquez sur **fichier** > **enregistrer**. Ensuite, cliquez sur **déboguer** > **exécuter** ou appuyez sur **F5** script de hello toorun.  

Après l’exécution du script de hello, vous devez disposer d’un dossier local de destination qui inclut le fichier d’image hello téléchargé. Hello suivant capture d’écran montre un exemple de sortie :

![Téléchargement d'objets blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Hello section « Mise en route avec le stockage Azure et de PowerShell dans 5 minutes » fourni une brève introduction sur la façon de toouse Azure PowerShell avec le stockage Azure. Pour plus d’informations et des instructions, nous vous encourageons hello tooread les sections suivantes.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Conditions préalables à l’utilisation d’Azure PowerShell avec Azure Storage
Vous avez besoin d’un abonnement et compte toorun hello PowerShell applets de commande Azure donné dans ce guide, comme décrit ci-dessus.

Azure PowerShell est un module qui fournit des applets de commande toomanage Azure via Windows PowerShell. Pour plus d’informations sur l’installation et configuration d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). Nous vous recommandons de télécharger et installer ou mettre à niveau du module Azure PowerShell toohello plus récent avant d’utiliser ce guide.

Vous pouvez exécuter les applets de commande hello dans la console Windows PowerShell standard de hello ou hello Windows PowerShell Integrated Scripting Environment (ISE). Par exemple, tooopen **Windows PowerShell ISE**atteindre le menu Démarrer de toohello, tapez outils d’administration, cliquez sur toorun il. Dans la fenêtre Outils d’administration de hello, avec le bouton droit de Windows PowerShell ISE, cliquez sur Exécuter en tant qu’administrateur.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Le mode de stockage de toomanage comptes dans Azure

Commençons par étudier la gestion des comptes de stockage dans Azure avec PowerShell

### <a name="how-tooset-a-default-azure-subscription"></a>Comment tooset un abonnement Azure par défaut
toomanage le stockage Azure à l’aide d’Azure PowerShell, vous devez tooauthenticate votre environnement de client avec Azure via l’authentification Azure Active Directory ou l’authentification par certificat. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) didacticiel. Ce guide utilise l’authentification Azure Active Directory hello.

1. Dans Windows PowerShell ISE, tapez Bonjour suivant commande tooadd votre environnement PowerShell local de compte Azure toohello :

    ```powershell
    Add-AzureAccount
    ```

2. Dans la fenêtre de hello « Connexion tooMicrosoft Azure », adresse de messagerie de type hello et mot de passe associé à votre compte. Azure authentifie et enregistre les informations d’identification de hello, puis ferme la fenêtre hello.

3. Ensuite, exécutez hello suivant commande tooview hello Azure des comptes dans votre environnement PowerShell local et vérifiez que votre compte est répertorié :
   
    ```powershell
    Get-AzureAccount
    ```
4. Ensuite, exécutez hello suivant tooview de l’applet de commande tous les abonnements hello session PowerShell locale de toohello connecté et vérifiez que votre abonnement est répertorié :

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset un abonnement Azure, par défaut, exécutez l’applet de commande hello Select-AzureSubscription :

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Vérifiez le nom hello d’abonnement par défaut de hello en exécutant l’applet de commande Get-AzureSubscription hello :

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee que tous hello applets de commande PowerShell disponibles pour le stockage Azure, exécutez :
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>Comment toocreate un compte de stockage Azure
Vous devrez toouse le stockage Azure, un compte de stockage. Vous pouvez créer un nouveau compte de stockage Azure une fois que vous avez configuré votre abonnement de tooyour tooconnect ordinateur.

1. Exécutez toofind d’applet de commande Get-AzureLocation hello tous les emplacements de centres de données disponibles hello :

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Ensuite, exécutez toocreate d’applet de commande New-AzureStorageAccount hello pour un compte de stockage. Hello exemple suivant crée un nouveau compte de stockage dans le centre de données hello « Ouest des États-Unis ».
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> nom de Hello de votre compte de stockage doit être unique dans Azure et doit être en minuscule. Pour connaître les conventions d’affectation de noms et les restrictions, consultez les pages [À propos des comptes de stockage Azure](../storage-create-storage-account.md) et [Affectation de noms et références aux conteneurs, objets blob et métadonnées](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>Comment tooset un compte de stockage Azure par défaut
Vous pouvez disposer de plusieurs comptes de stockage dans votre abonnement. Vous pouvez choisir un d’eux et définissez-le comme compte de stockage par défaut hello pour tous les hello stockage commandes Bonjour même session PowerShell. Cela vous permet commandes de stockage Azure PowerShell toorun hello sans spécifier le contexte de stockage hello explicitement.

1. tooset un compte de stockage par défaut pour votre abonnement, vous pouvez exécuter l’applet de commande Set-AzureSubscription hello.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Ensuite, exécutez tooverify d’applet de commande Get-AzureSubscription de hello que le compte de stockage hello est associé à votre compte d’abonnement par défaut. Cette commande retourne les propriétés de l’abonnement hello sur abonnement hello, y compris son compte de stockage actuel.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Le mode toolist tout le stockage Azure de comptes dans un abonnement
Chaque abonnement Azure peut avoir des comptes de stockage too100. Pour hello dernières informations sur les limites, consultez [abonnement Azure et limites de Service, Quotas et contraintes](../../azure-subscription-service-limits.md).

Exécutez hello suivant toofind d’applet de commande out nom de hello et l’état hello de comptes de stockage dans l’abonnement actif de hello :

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>Comment toocreate un contexte de stockage Azure
Contexte de stockage Azure est un objet d’informations d’identification du stockage hello tooencapsulate PowerShell. À l’aide d’un contexte de stockage lors de l’exécution d’une applet de commande suivante permet de vous tooauthenticate votre demande sans spécification explicite de compte de stockage hello et sa clé d’accès. Vous pouvez créer un contexte de stockage de plusieurs façons, par exemple à l'aide du nom du compte et de la clé d'accès, du jeton de signature d'accès partagé (SAS), de la chaîne de connexion ou de façon anonyme. Pour plus d’informations, consultez la page [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Utilisez une des hello suivant de trois façons toocreate d’un contexte de stockage :

* Exécutez hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind d’applet de commande à la clé d’accès de stockage principal hello pour votre compte de stockage Azure. Ensuite, appelez hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) toocreate de l’applet de commande un contexte de stockage :

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Générer un jeton de signature d’accès partagé pour un conteneur de stockage Azure et l’utiliser toocreate un contexte de stockage :

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Pour plus d’informations, consultez [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) et [Utilisation des signatures d’accès partagé (SAP)](../storage-dotnet-shared-access-signature-part-1.md).

* Dans certains cas, vous pouvez vouloir points de terminaison de service toospecify hello lorsque vous créez un nouveau contexte de stockage. Cela peut être nécessaire lorsque vous avez enregistré un nom de domaine personnalisé pour votre compte de stockage avec service d’objets Blob hello ou toouse une signature d’accès partagé pour l’accès aux ressources de stockage. Définir des points de terminaison de service hello dans une chaîne de connexion et utilisez toocreate un nouveau contexte de stockage comme indiqué ci-dessous :

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Pour plus d’informations sur la façon de tooconfigure une chaîne de connexion de stockage, consultez [configuration des chaînes de connexion](../storage-configure-connection-string.md).

Maintenant que vous avez configuré votre ordinateur et appris comment toomanage abonnements et les comptes de stockage à l’aide d’Azure PowerShell, accédez toohello toolearn de section suivant comment toomanage Azure BLOB et instantanés d’objets blob.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>Comment tooretrieve et régénérer les clés de stockage Azure
Un compte Azure Storage est fourni avec deux clés de compte. Vous pouvez utiliser hello suivant l’applet de commande tooretrieve vos clés.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Utilisez hello suivant l’applet de commande tooretrieve une clé spécifique. Les valeurs valides sont : Primaire et Secondaire.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Si vous souhaitez que tooregenerate vos clés, utilisez hello suivant l’applet de commande. Les valeurs valides pour -KeyType sont « Primaire » et « Secondaire »

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Comment toomanage Azure BLOB
Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS. Cette section part du principe que vous êtes déjà familiarisé avec les concepts de Service de stockage d’objets Blob Azure hello. Pour obtenir des informations détaillées, consultez [Prise en main du stockage d’objets blob à l’aide de .NET](../blobs/storage-dotnet-how-to-use-blobs.md) et [Concepts du service BLOB](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-toocreate-a-container"></a>Comment toocreate un conteneur
Chaque objet blob du stockage Azure doit se trouver dans un conteneur. Vous pouvez créer un conteneur privé à l’aide d’applet de commande New-AzureStorageContainer de hello :

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Il existe trois niveaux d’accès en lecture anonyme : **Désactivé**, **Blob** et **Conteneur**. tooprevent anonyme accéder à tooblobs, le paramètre d’autorisation ensemble hello**hors**. Par défaut, hello nouveau conteneur est privé et sont accessibles uniquement par le propriétaire du compte hello. public anonyme de tooallow lire tooblob d’accéder aux ressources, mais pas toocontainer métadonnées ou toohello liste d’objets BLOB dans le conteneur de hello, définissez le paramètre d’autorisation hello trop**Blob**. public complet de tooallow lire tooblob d’accéder aux ressources, les métadonnées de conteneur et hello liste d’objets BLOB dans le conteneur de hello, définissez le paramètre d’autorisation hello trop**conteneur**. Pour plus d’informations, consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../blobs/storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>Comment tooupload un objet blob dans un conteneur
Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page. Pour plus d’informations, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooupload objets BLOB dans tooa conteneur, vous pouvez utiliser hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) applet de commande. Par défaut, cette commande télécharge le blob de blocs tooa hello fichiers locaux. type de hello toospecify pour l’objet blob de hello, vous pouvez utiliser le paramètre - BlobType de hello.

exemple Hello exécute hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget d’applet de commande hello tous les fichiers dans le dossier spécifié de hello et les transmet toohello applet de commande suivante en utilisant l’opérateur de pipeline hello. Hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) applet de commande télécharge le conteneur de tooyour hello fichiers locaux :

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Comment toodownload les objets BLOB à partir d’un conteneur
Bonjour à l’exemple suivant montre comment toodownload les objets BLOB à partir d’un conteneur. exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès primaire. Ensuite, hello exemple récupère une référence d’objet blob à l’aide de hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) applet de commande. Ensuite, hello utilise hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobs de toodownload d’applet de commande dans le dossier de destination local hello.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Comment toocopy les objets BLOB à partir d’un tooanother de conteneur de stockage
Vous pouvez également copier des objets blob entre les comptes de stockage et les régions de façon asynchrone. Hello exemple suivant montre comment les objets BLOB toocopy de tooanother de conteneur de stockage dans les deux comptes de stockage différents. exemple de Hello définit les variables pour les comptes de stockage source et de destination et crée ensuite un contexte de stockage pour chaque compte. Ensuite, hello exemple copie les objets BLOB à partir du conteneur hello source conteneur toohello destination à l’aide de hello [AzureStorageBlobCopy de début](/powershell/module/azure.storage/start-azurestorageblobcopy) applet de commande. Hello suppose que les conteneurs et les comptes de stockage source et de destination hello existent déjà.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Notez que cet exemple effectue une copie asynchrone. Vous pouvez surveiller l’état de hello de chaque copie en exécutant hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) applet de commande.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>Comment toocopy les objets BLOB à partir d’un emplacement secondaire
Vous pouvez copier des objets BLOB à partir de l’emplacement secondaire de hello d’un compte activé RA-GRS.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>Comment toodelete un objet blob
toodelete un objet blob, commencez par obtenir une référence d’objet blob, puis appelez applet de commande Remove-AzureStorageBlob hello sur celui-ci. Bonjour à l’exemple suivant supprime tous les objets BLOB de hello dans un conteneur donné. exemple de Hello définit les variables pour un compte de stockage et crée ensuite un contexte de stockage. Ensuite, hello exemple récupère une référence d’objet blob à l’aide de hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello applet de commande et exécute [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) blobs de tooremove d’applet de commande à partir d’un conteneur dans le stockage Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Comment toomanage Azure instantanés d’objets blob
Azure vous permet de créer l'instantané d'un objet blob. Un instantané est une version en lecture seule d'un objet blob capturé à un instant donné. Un instantané peut être lu, copié ou supprimé, mais pas modifié. Instantanés fournissent un tooback moyen d’un objet blob, tel qu’il apparaît à un moment donné. Pour plus d’informations, consultez [Création d’un instantané d’objet blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>Comment toocreate un instantané d’objet blob
tout d’abord obtenir une référence d’objet blob de toocreate un instantané d’un objet blob et ensuite appeler hello `ICloudBlob.CreateSnapshot` méthode dessus. Bonjour exemple suivant définit les variables pour un compte de stockage et crée ensuite un contexte de stockage. Ensuite, hello exemple récupère une référence d’objet blob à l’aide de hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello applet de commande et exécute [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) méthode toocreate un instantané.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>Comment les instantanés de toolist un objet blob
Vous pouvez créer autant d'instantanés que vous le souhaitez pour un objet blob. Vous pouvez répertorier les instantanés hello associés à votre tootrack blob vos instantanés actuels. Hello exemple suivant utilise un prédéfinis Bonjour blob et les appels [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) applet de commande toolist hello des instantanés de cet objet blob.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>Comment toocopy un instantané d’un objet blob
Vous pouvez copier un instantané d’un instantané de hello toorestore blob. Pour plus d’informations et d’autres informations sur les restrictions, consultez [Création d’un instantané d’objet blob](http://msdn.microsoft.com/library/azure/hh488361.aspx). Bonjour exemple suivant définit les variables pour un compte de stockage et crée ensuite un contexte de stockage. Ensuite, hello exemple définit des variables de nom de conteneur et d’objet blob hello. Hello exemple récupère une référence d’objet blob à l’aide de hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello applet de commande et exécute [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) méthode toocreate un instantané. Exemple de hello exécute ensuite hello [AzureStorageBlobCopy de début](/powershell/module/azure.storage/start-azurestorageblobcopy) instantané de hello toocopy applet de commande d’un objet blob à l’aide d’objet de ICloudBlob hello pour l’objet blob source de hello. Que les variables hello tooupdate reposer sur votre configuration avant d’exemple hello en cours. Notez que hello l’exemple suivant suppose que la source de hello et conteneurs de destination et hello source blob existent déjà.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Maintenant que vous avez appris comment toomanage Azure BLOB et instantanés avec Azure PowerShell d’objets blob, accédez à toohello suivant section toolearn comment toomanage tables, files d’attente et les fichiers.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Comment toomanage Azure tables et entités de table
Service de stockage de Table Azure est une banque de données NoSQL, que vous pouvez utiliser des jeux d’énorme toostore et requête de données structurées et non relationnelles. Hello principaux composants du service de hello sont des tables, des entités et propriétés. une table est une collection d’entités. Une entité est un ensemble de propriétés. Chaque entité peut avoir les propriétés too252, qui sont toutes les paires nom-valeur. Cette section part du principe que vous êtes déjà familiarisé avec les concepts de Service de stockage de Table Azure hello. Pour plus d’informations, consultez [hello de présentation des modèle de données de Service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx) et [prise en main le stockage de Table Azure à l’aide de .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).

Bonjour suivant sous-sections, vous allez apprendre comment toomanage stockage de Table Azure de service à l’aide d’Azure PowerShell. Hello scénarios abordés incluent **création**, **suppression**, et **récupération** **tables**, ainsi que **ajout**, **interrogation**, et **la suppression des entités de table**.

### <a name="how-toocreate-a-table"></a>Comment toocreate une table
Toutes les tables doivent se trouver dans un compte de stockage Azure. Hello exemple suivant montre comment toocreate une table dans le stockage Azure. exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès. Ensuite, il utilise hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) toocreate de l’applet de commande une table dans le stockage Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>Comment tooretrieve une table
Vous pouvez interroger et récupérer une des tables ou toutes les tables dans un compte de stockage. Hello exemple suivant montre comment une table donnée à l’aide de tooretrieve hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) applet de commande.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Si vous appelez hello applet de commande Get-AzureStorageTable sans aucun paramètre, il obtient toutes les tables de stockage pour un compte de stockage.

### <a name="how-toodelete-a-table"></a>Comment toodelete une table
Vous pouvez supprimer une table à partir d’un compte de stockage à l’aide de hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) applet de commande.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Comment toomanage table des entités
Actuellement, Azure PowerShell ne fournit pas directement des entités de table toomanage applets de commande. tooperform des opérations sur les entités de table, vous pouvez utiliser les classes de hello figurant hello [bibliothèque cliente de stockage Azure pour .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Comment tooadd table des entités
tooadd une table tooa d’entité, d’abord créer un objet qui définit les propriétés de l’entité. Une entité peut avoir les propriétés too255, y compris 3 Propriétés système : **PartitionKey**, **RowKey**, et **Timestamp**. Vous êtes chargé d’insertion et de mise à jour des valeurs hello de **PartitionKey** et **RowKey**. valeur hello gère Hello server **Timestamp**, qui ne peut pas être modifié. Ensemble hello **PartitionKey** et **RowKey** identifier de façon unique chaque entité d’une table.

* **PartitionKey**: détermine la partition hello stockées dans les entités hello.
* **RowKey**: identifie de façon unique entité hello au sein de la partition de hello.

Vous pouvez définir les propriétés personnalisées de too252 pour une entité. Pour plus d’informations, consultez [hello de présentation des modèle de données de Service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hello exemple suivant montre la table de tooa tooadd entités. Hello montre comment tooretrieve hello table employee et comment ajouter plusieurs entités dans celui-ci. Tout d’abord, il établit une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès. Ensuite, il récupère hello fonction table à l’aide de hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) applet de commande. Si la table de hello n’existe pas, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) applet de commande est utilisée toocreate une table dans le stockage Azure. Ensuite, hello exemple définit une fonction personnalisée table de toohello-ajouter une entité tooadd entités en spécifiant la partition de chaque entité et la clé de ligne. Hello ajouter une entité fonction appels hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) applet de commande hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) classe toocreate un objet entité. Une version ultérieure, hello exemple appelle hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) méthode sur cette tooadd d’objet entité il tooa table.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Comment tooquery table des entités
tooquery une table, utilisez hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) classe. Hello exemple suivant suppose que vous avez déjà exécuté le script hello figurant hello la section d’entités tooadd de ce guide. exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès. Ensuite, il tente de table de hello créé précédemment « employés » tooretrieve à l’aide de hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) applet de commande. Appel hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) hello Microsoft.WindowsAzure.Storage.Table.TableQuery classe applet de commande crée un nouvel objet de requête. exemple de Hello recherche entités hello qui possèdent une colonne « ID » dont la valeur est 1, comme spécifié dans un filtre de chaîne. Pour plus d’informations, consultez [Interrogation de tables et d’entités](http://msdn.microsoft.com/library/azure/dd894031.aspx). Lorsque vous exécutez cette requête, il retourne toutes les entités qui correspondent aux critères de filtre hello.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Comment toodelete table des entités
Vous pouvez supprimer une entité en utilisant ses clés de partition et de ligne. Hello exemple suivant suppose que vous avez déjà exécuté le script hello figurant hello la section d’entités tooadd de ce guide. exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès. Ensuite, il tente de table de hello créé précédemment « employés » tooretrieve à l’aide de hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) applet de commande. Si la table de hello existe, hello exemple appelle hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve méthode une entité en fonction de ses valeurs de clé de partition et de ligne. Ensuite, passez hello entité toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete de méthode.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Comment toomanage Azure files d’attente et file d’attente de messages
Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS. Cette section part du principe que vous êtes déjà familiarisé avec les concepts de Service de stockage de file d’attente Azure hello. Pour obtenir des informations détaillées, consultez [Prise en main d’Azure Queue Storage à l’aide de .NET](../storage-dotnet-how-to-use-queues.md).

Cette section vous indiquera comment toomanage stockage de file d’attente Azure service à l’aide d’Azure PowerShell. Hello scénarios abordés incluent **insertion** et **suppression** file d’attente de messages, ainsi que **création**, **suppression**et **la récupération des files d’attente**.

### <a name="how-toocreate-a-queue"></a>Comment toocreate une file d’attente
Hello exemple suivant établit d’abord une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès. Ensuite, il appelle [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) toocreate de l’applet de commande une file d’attente nommée 'queuename'.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Pour plus d’informations sur les conventions d’affectation de noms pour le service de File d’attente Azure, consultez la page [Affectation de noms pour les files d’attente et les métadonnées](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>Comment tooretrieve une file d’attente
Vous pouvez interroger et extraire une file d’attente spécifique ou une liste de toutes les files d’attente de hello dans un compte de stockage. Hello exemple suivant montre comment une file d’attente spécifiée à l’aide de tooretrieve hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) applet de commande.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Si vous appelez hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) applet de commande sans aucun paramètre, il obtient une liste de toutes les files d’attente de hello.

### <a name="how-toodelete-a-queue"></a>Comment toodelete une file d’attente
toodelete une file d’attente et tous les messages hello qu’il contient, applet de commande Remove-AzureStorageQueue de hello appel. Bonjour à l’exemple suivant montre comment une file d’attente spécifiée à l’aide de toodelete hello applet de commande Remove-AzureStorageQueue.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>Comment tooinsert un message dans une file d’attente
tooinsert un message dans une file d’attente existante, commencez par créer une nouvelle instance de hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe. Ensuite, appelez hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) (méthode). Un CloudQueueMessage peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.

Hello, l’exemple suivant montre comment la file d’attente de tooa de message tooadd. exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès. Ensuite, il récupère la file d’attente spécifiée hello à l’aide de hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) applet de commande. Si la file d’attente hello existe, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) toocreate utilisé une instance de hello est [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe. Une version ultérieure, hello exemple appelle hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) méthode sur cette tooadd d’objet de message il file d’attente tooa. Voici le code qui Récupère une file d’attente et insère le message de type hello 'MessageInfo' :

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Comment toode la file d’attente à hello message suivant
Votre code enlève un message d'une file d'attente en deux étapes. Lorsque vous appelez hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) (méthode), vous obtenez message de type hello suivante dans une file d’attente. Un message retourné à partir de **GetMessage** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente. toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) (méthode). Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez. Votre code appelle **DeleteMessage** juste après le message de salutation a été traité.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>Comment toomanage fichier Azure et les fichiers
Stockage de fichiers Azure offre un stockage partagé pour les applications à l’aide du protocole SMB standard de hello. Machines virtuelles Microsoft Azure et les services de cloud computing peuvent partager des données de fichier entre les composants d’application via des partages montés, et des applications locales peuvent accéder à des données de fichier dans un partage via l’API de stockage de fichier hello ou Azure PowerShell.

Pour plus d’informations sur le stockage de fichiers Azure, consultez [Prise en main du stockage de fichiers Azure sous Windows](../storage-dotnet-how-to-use-files.md) et [API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-tooset-and-query-storage-analytics"></a>Comment tooset et la requête analytique de stockage
Vous pouvez utiliser [Analytique de stockage Azure](../storage-analytics.md) métriques toocollect pour vos comptes de stockage Azure et les données du journal sur les demandes envoyées de compte de stockage tooyour. Vous pouvez utiliser des mesures toomonitor hello l’intégrité du stockage d’un compte de stockage et le stockage journalisation toodiagnose et résoudre les problèmes avec votre compte de stockage. Vous pouvez configurer la surveillance à l’aide de hello portail Azure ou Windows PowerShell, ou par programme à l’aide de la bibliothèque cliente de stockage hello. Stockage de la journalisation produit côté serveur et vous permet de toorecord les détails pour les demandes réussies et échouées dans votre compte de stockage. Ces journaux vous permettent de toosee les détails de la lecture, écriture et les opérations de suppression sur vos tables, files d’attente et objets BLOB ainsi que raisons hello pour les demandes ayant échouées.

toolearn tooenable et afficher les données des métriques de stockage à l’aide de PowerShell, voir [comment tooenable Storage Metrics à l’aide de PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

toolearn tooenable et récupérer l’enregistrement de stockage des données à l’aide de PowerShell, voir [comment tooenable Storage Logging à l’aide de PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) et [recherche de vos données de journal Storage Logging](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Pour plus d’informations sur l’utilisation des indicateurs de stockage et les problèmes de stockage tootroubleshoot de journalisation du stockage, consultez [surveillance, diagnostic et résolution des problèmes Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Mode de partage toomanage Signature d’accès (SAP) et la stratégie d’accès stockée
Signatures d’accès partagé sont une partie importante de modèle de sécurité hello pour les applications qui utilisent le stockage Azure. Ils sont utiles pour fournir des autorisations limitées tooyour tooclients stockage compte que vous ne devez pas de clé de compte hello. Par défaut, seul propriétaire du hello hello du compte de stockage peut accéder aux objets BLOB, tables et files d’attente dans ce compte. Si votre service ou application doit toomake ces clients disponibles tooother de ressources sans partager votre clé d’accès, vous disposez de trois options :

* Définissez le conteneur toohello l’accès en lecture anonyme d’un conteneur autorisations toopermit et ses objets BLOB. Cela n’est pas autorisé pour les tables ou les files d'attente.
* Utiliser une signature d’accès partagé qui accorde toocontainers de droits d’accès restreint, les objets BLOB, les files d’attente et les tables pour un intervalle de temps spécifique.
* Utilisez un tooobtain de stratégie d’accès stockée un niveau supplémentaire de contrôle de signatures d’accès partagé pour un conteneur ou ses objets BLOB, pour une file d’attente ou pour une table. Hello stratégie d’accès stockée vous permet de l’heure de début toochange hello, délai d’expiration ou des autorisations pour une signature, ou toorevoke après qu’il a été émise.

Une signature d’accès partagé peut prendre deux formes :

* **SAS ad hoc**: lorsque vous créez un SAS ad hoc, l’heure de début hello, la durée d’expiration et les autorisations pour hello SAS sont toutes spécifiées sur hello URI SAS. Ce type de signature d'accès partagé peut être créé sur un conteneur, un objet blob, une table ou une file d'attente, et il ne peut pas être révoqué.
* **Associations de sécurité avec la stratégie d’accès stockée**: une stratégie d’accès stockée est définie sur un conteneur de ressources un conteneur d’objets blob, une table ou une file d’attente - et vous pouvez l’utiliser toomanage contraintes pour une ou plusieurs signatures d’accès partagé. Lorsque vous associez un SAS avec une stratégie d’accès stockée, hello SAS hérite des contraintes de hello - hello heure de début, date d’expiration et autorisations - définies pour la stratégie d’accès stockée hello. Ce type de signature d'accès partagé peut être révoqué.

Pour plus d’informations, consultez [à l’aide de Signatures SAP (accès partagé)](../storage-dotnet-shared-access-signature-part-1.md) et [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../blobs/storage-manage-access-to-resources.md).

Dans les sections suivantes de hello, vous allez apprendre comment toocreate une stratégie d’accès stockée et de jeton de signature accès partagé pour les tables Azure. PowerShell Azure fournit aussi des applets de commande semblables pour les conteneurs, les objets blob et les files d'attente. scripts de hello toorun dans cette section, télécharger hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) ou version ultérieure.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>Comment jeton de Signature d’accès partagé toocreate basée sur des stratégies
Utilisez toocreate d’applet de commande New-AzureStorageTableStoredAccessPolicy hello une stratégie d’accès stockée. Ensuite, appelez hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate de l’applet de commande un nouveau jeton de signature basée sur des stratégies d’accès partagé pour une table de stockage Azure.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Comment toocreate un jeton de Signature d’accès partagé ad hoc (non révocables)
Hello d’utilisation [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate de l’applet de commande un nouveau jeton de Signature d’accès partagé de (non révocables) ad hoc pour une table de stockage Azure :

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>Comment toocreate une stratégie d’accès stockée
Utilisez toocreate d’applet de commande hello AzureStorageTableStoredAccessPolicy de nouveau une stratégie d’accès stockée pour une table de stockage Azure :

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>Comment tooupdate une stratégie d’accès stockée
Utilisez tooupdate d’applet de commande Set-AzureStorageTableStoredAccessPolicy hello une stratégie d’accès stockée existante pour une table de stockage Azure :

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>Comment toodelete une stratégie d’accès stockée
Utilisez toodelete d’applet de commande hello AzureStorageTableStoredAccessPolicy de supprimer une stratégie d’accès stockée sur une table de stockage Azure :

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Comment toouse le stockage Azure pour le gouvernement des États-Unis et Azure Chine
Un environnement Azure est un déploiement indépendant de Microsoft Azure, par exemple [Azure Government pour le gouvernement des États-Unis](https://azure.microsoft.com/features/gov/), [AzureCloud pour Azure global](https://portal.azure.com) et [AzureChinaCloud pour Azure exploité par 21Vianet en Chine](http://www.windowsazure.cn/). Vous pouvez déployer de nouveaux environnements Azure pour le gouvernement des États-Unis et Azure en Chine.

toouse le stockage Azure avec AzureChinaCloud, vous devez toocreate un contexte de stockage qui est associé à AzureChinaCloud. Suivez ces tooget étapes que vous avez démarré :

1. Exécutez hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee de l’applet de commande hello environnements Azure disponibles :
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Ajouter un tooWindows de compte Azure Chine PowerShell :
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Créez un contexte de stockage pour un compte AzureChinaCloud :
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse Azure Storage avec [des États-Unis pour le gouvernement des États-Unis](https://azure.microsoft.com/features/gov/), vous devez définir un nouvel environnement, puis créer un contexte de stockage avec cet environnement :

1. Exécutez hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee de l’applet de commande hello environnements Azure disponibles :

    ```powershell
    Get-AzureEnvironment
    ```

2. Ajouter un tooWindows de compte Azure du gouvernement PowerShell :
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Créez un contexte de stockage pour un compte Azure pour le gouvernement américain :
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Pour plus d'informations, consultez les pages suivantes :

* [Guide du développeur Microsoft Azure Government](../../azure-government/documentation-government-developer-guide.md).
* [Vue d'ensemble des différences lors de la création d'une application sur le service Chine](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Étapes suivantes
Dans ce guide, vous avez appris comment toomanage le stockage Azure avec Azure PowerShell. Pour en savoir plus, consultez les articles et ressources suivants :

* [Documentation d'Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Applets de commande Azure Storage PowerShell](/powershell/module/azurerm.storage/#storage)
* [Référence Windows PowerShell](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
