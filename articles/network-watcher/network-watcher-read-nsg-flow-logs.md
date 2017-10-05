---
title: "Lire les journaux de flux de groupe de sécurité réseau | Documents Microsoft"
description: "Cet article explique comment analyser les journaux de flux de groupe de sécurité réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: 9bb48157b2b8e483e063058f761c3a8f531927f9
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="3ce8e-103">Lire des journaux de flux NSG</span><span class="sxs-lookup"><span data-stu-id="3ce8e-103">Read NSG flow logs</span></span>

<span data-ttu-id="3ce8e-104">Découvrez comment lire les entrées de journaux de flux de groupe de sécurité réseau avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-104">Learn how to read NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="3ce8e-105">Les journaux de flux de groupe de sécurité réseau sont stockés dans un compte de stockage dans de [objets blob de bloc](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span><span class="sxs-lookup"><span data-stu-id="3ce8e-105">NSG flow logs are stored in a storage account in [block blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span></span> <span data-ttu-id="3ce8e-106">Les objets blob de blocs sont composés de blocs plus petits.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="3ce8e-107">Chaque journal est un objet blob de blocs séparé généré toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="3ce8e-108">Les nouveaux journaux sont créés toutes les heures, les journaux sont mis à jour avec les nouvelles entrées toutes les quelques minutes avec les dernières données.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-108">New logs are generated every hour, the logs are updated with new entries every few minutes with the latest data.</span></span> <span data-ttu-id="3ce8e-109">Dans cet article vous allez apprendre à lire une partie des journaux de flux.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-109">In this article you learn how to read portions of the flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="3ce8e-110">Scénario</span><span class="sxs-lookup"><span data-stu-id="3ce8e-110">Scenario</span></span>

<span data-ttu-id="3ce8e-111">Dans le scénario suivant, vous disposez d’un exemple de journal de flux stocké dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-111">In the following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="3ce8e-112">nous parcourons comment vous pouvez lire sélectivement les derniers événements dans les journaux de flux de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-112">we step through how you can selectively read the latest events in NSG flow logs.</span></span> <span data-ttu-id="3ce8e-113">Dans cet article, nous allons utiliser PowerShell, toutefois, les concepts abordés dans l’article ne sont pas limités au langage de programmation et sont applicables à tous les langages pris en charge par les API de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="3ce8e-113">In this article we will use PowerShell, however, the concepts discussed in the article are not limited to the programming language and are applicable to all languages supported by the Azure Storage APIs</span></span>

## <a name="setup"></a><span data-ttu-id="3ce8e-114">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="3ce8e-114">Setup</span></span>

<span data-ttu-id="3ce8e-115">Avant de commencer, la journalisation des flux de groupe de sécurité réseau doit être activée sur un ou plusieurs groupes de sécurité réseau de votre compte.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="3ce8e-116">Pour obtenir des instructions sur l’activation des journaux de flux de sécurité réseau, consultez l’article suivant [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md) (Introduction à la journalisation des flux pour les groupes de sécurité réseau).</span><span class="sxs-lookup"><span data-stu-id="3ce8e-116">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-the-block-list"></a><span data-ttu-id="3ce8e-117">Récupérer la liste de blocs</span><span class="sxs-lookup"><span data-stu-id="3ce8e-117">Retrieve the block list</span></span>

<span data-ttu-id="3ce8e-118">La commande PowerShell suivante définit les variables nécessaires pour interroger l’objet blob des journaux de flux de groupe de sécurité réseau et répertorier les blocs dans l’objet blob de blocs [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3).</span><span class="sxs-lookup"><span data-stu-id="3ce8e-118">The following PowerShell sets up the variables needed to query the NSG flow log blob and list the blocks within the [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="3ce8e-119">Mettez à jour le script pour contenir des valeurs valides pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-119">Update the script to contain valid values for your environment.</span></span>

```powershell
# The SubscriptionID to use
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains the Network Security Group
$resourceGroupName = "<resourceGroupName>"

# The name of the Network Security Group
$nsgName = "NSGName"

# The storage account name that contains the NSG logs
$storageAccountName = "<storageAccountName>" 

# The date and time for the log to be queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve the primary storage account key to access the NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context to be used to query the logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of the blob that contains the NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets the storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets the block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from the storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores the block list in a variable from the block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

<span data-ttu-id="3ce8e-120">La variable `$blockList` renvoie une liste des blocs dans l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-120">The `$blockList` variable returns a list of the blocks in the blob.</span></span> <span data-ttu-id="3ce8e-121">Chaque objet blob de blocs contient au moins deux blocs.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="3ce8e-122">Le premier bloc a une longueur de `21` octets, ce bloc contient les crochets d’ouverture du journal json.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-122">The first block has a length of `21` bytes, this block contains the opening brackets of the json log.</span></span> <span data-ttu-id="3ce8e-123">L’autre bloc contient les crochets fermant avec une longueur de `9` octets.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-123">The other block is the closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="3ce8e-124">Comme vous pouvez le constater, le journal d’exemple suivant comporte sept entrées, chacune étant une entrée individuelle.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-124">As you can see the following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="3ce8e-125">Toutes les nouvelles entrées dans le journal sont ajoutées à la fin, juste avant le dernier bloc.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-125">All new entries in the log are added to the end right before the final block.</span></span>

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     21      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      9      True
```

## <a name="read-the-block-blob"></a><span data-ttu-id="3ce8e-126">Lire l’objet blob de blocs</span><span class="sxs-lookup"><span data-stu-id="3ce8e-126">Read the block blob</span></span>

<span data-ttu-id="3ce8e-127">Ensuite, nous avons besoin de lire la variable `$blocklist` pour récupérer les données.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-127">Next we need to read the `$blocklist` variable to retrieve the data.</span></span> <span data-ttu-id="3ce8e-128">Dans cet exemple que nous itérons dans la liste de blocs, lisez les octets de chaque bloc et estimez-les dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-128">In this example we iterate through the blocklist, read the bytes from each block and story them in an array.</span></span> <span data-ttu-id="3ce8e-129">Nous utilisons la méthode [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) pour récupérer les données.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-129">We use the [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method to retrieve the data.</span></span>

```powershell
# Set the size of the byte array to the largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array to store values in
$valuearray = @()

# Define the starting index to track the current block being read
$index = 0

# Loop through each block in the block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object to story the bytes from the block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download the data into the ByteArray, starting with the current index, for the number of bytes in the current block. Index is increased by 3 when reading to remove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment the index by adding the current block length to the previous index
$index = $index + $blockList[$i].Length

# Retrieve the string from the byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add the log entry to the value array
$valuearray += $value
}
```

<span data-ttu-id="3ce8e-130">Maintenant le tableau `$valuearray` contient la valeur de chaîne de chaque bloc.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-130">Now the `$valuearray` array contains the string value of each block.</span></span> <span data-ttu-id="3ce8e-131">Pour vérifier l’entrée, enregistrez le deuxième à la dernière valeur du tableau en exécutant `$valuearray[$valuearray.Length-2]`.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-131">To verify the entry, get the second to the last value from the array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="3ce8e-132">Nous ne souhaitons pas que la dernière valeur soit simplement le crochet fermant.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-132">We do not want the last value is just the closing bracket.</span></span>

<span data-ttu-id="3ce8e-133">Les résultats de cette valeur sont affichés dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="3ce8e-133">The results of this value are shown in the following example:</span></span>

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

<span data-ttu-id="3ce8e-134">Ce scénario est un exemple montrant comment lire les entrées dans les journaux de flux de groupe de sécurité réseau sans avoir à analyser l’ensemble du journal.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-134">This scenario is an example of how to read entries in NSG flow logs without having to parse the entire log.</span></span> <span data-ttu-id="3ce8e-135">Vous pouvez lire les nouvelles entrées dans le journal comme elles sont écrites à l’aide de l’ID de bloc ou en effectuant le suivi de la longueur des blocs stockés dans l’objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-135">You can read new entries in the log as they are written by using the block ID or by tracking the length of blocks stored in the block blob.</span></span> <span data-ttu-id="3ce8e-136">Cela vous permet de lire uniquement les nouvelles entrées.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-136">This allows you to read only the new entries.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3ce8e-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ce8e-137">Next steps</span></span>

<span data-ttu-id="3ce8e-138">Visiter [visualiser les journaux de flux de NSG de l’Observateur réseau Azure à l’aide d’outils open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) pour en savoir plus sur d’autres moyens pour afficher les journaux de flux NSG.</span><span class="sxs-lookup"><span data-stu-id="3ce8e-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) to learn more about other ways to view NSG flow logs.</span></span>

<span data-ttu-id="3ce8e-139">Pour en savoir plus sur les objets blob de stockage, visitez : [liaisons de stockage d’objets blob de fonction Azure](../azure-functions/functions-bindings-storage-blob.md)</span><span class="sxs-lookup"><span data-stu-id="3ce8e-139">To learn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>