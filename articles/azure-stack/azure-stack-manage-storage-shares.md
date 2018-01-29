---
title: "Gérer la capacité de stockage dans Azure Stack | Microsoft Docs"
description: "Surveillez et gérez l’espace de stockage disponible pour Azure Stack."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: b0e694e4-3575-424c-afda-7d48c2025a62
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/14/2017
ms.author: brenduns
ms.reviewer: jiahan
ms.openlocfilehash: dce4252846732ca5161018103438df1f9ff6146d
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2018
---
# <a name="manage-storage-capacity-for-azure-stack"></a>Gérer la capacité de stockage pour Azure Stack

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

Les informations contenues dans cet article aident l’opérateur de cloud d’Azure Stack à surveiller et à gérer la capacité de stockage de son déploiement Azure Stack. L’infrastructure de stockage d’Azure Stack alloue un sous-ensemble de la capacité de stockage totale du déploiement Azure Stack aux **services de stockage**. Les services de stockage stockent les données d’un locataire dans les partages des volumes qui correspondent aux nœuds du déploiement.

En tant qu’opérateur de cloud, vous disposez d’une quantité limitée de stockage à utiliser. La quantité de stockage est définie par la solution que vous implémentez. Votre solution est fournie par votre fournisseur OEM si vous utilisez une solution à plusieurs nœuds ou par le matériel sur lequel vous installez le kit de développement Azure Stack.

Comme Azure Stack ne prend pas en charge l’extension de la capacité de stockage, il est important de [surveiller](#monitor-shares) le stockage disponible pour assurer le maintien du bon fonctionnement.  

Lorsque la capacité libre restante d’un partage se restreint, pensez à [gérer l’espace](#manage-available-space) pour empêcher les partages de manquer de capacité.

Options de gestion de la capacité :
- Récupérer de la capacité
- Migrer un conteneur

Quand un partage est utilisé à 100 %, le service de stockage ne fonctionne plus pour celui-ci. Pour obtenir de l’aide sur les opérations de restauration du partage, contactez le support Microsoft.

## <a name="understand-volumes-and-shares-containers-and-disks"></a>Présentation des volumes, des partages, des conteneurs et des disques
### <a name="volumes-and-shares"></a>Volumes et partages
Le *service de stockage* partitionne le stockage disponible en volumes distincts et égaux qui sont alloués pour stocker des données de locataire. Le nombre de volumes est égal au nombre de nœuds du déploiement Azure Stack :

- Un déploiement de quatre nœuds comporte quatre volumes. Chaque volume possède un seul partage. Dans un déploiement de plusieurs nœuds, le nombre de partages n’est pas réduit si un nœud est supprimé ou ne fonctionne pas correctement.
- Le kit de développement Azure Stack ne comporte qu’un seul volume avec un partage unique.

Comme les partages de service de stockage sont destinés à l’utilisation exclusive des services de stockage, vous ne devez pas y modifier, ajouter ni supprimer directement des fichiers. Seuls les services de stockage doivent fonctionner sur les fichiers stockés dans ces volumes.

Partages des volumes contenant des données de locataire. Les données de locataire incluent des objets blob de pages, des objets blob de blocs, des objets blob d’ajouts, des tables, des files d’attente, des bases de données et des magasins de métadonnées associés. Comme les objets de stockage (objets blob, etc.) sont individuellement contenus dans un seul et même partage, la taille maximale de chaque objet ne peut pas dépasser la taille d’un partage. La taille maximale des nouveaux objets dépend de la capacité restant dans un partage sous forme d’espace inutilisé lorsque ce nouvel objet est créé.

Lorsqu’un partage manque d’espace libre et que les actions pour [récupérer](#reclaim-capacity) de l’espace n’aboutissent pas ou ne sont pas disponibles, l’opérateur de cloud d’Azure Stack peut [migrer](#migrate-a-container-between) les conteneurs d’objets blob d’un partage vers un autre.

- Pour plus d’informations sur les conteneurs et les objets blob, consultez la section [Stockage d’objets blob](azure-stack-key-features.md#blob-storage) dans l’article Fonctionnalités et concepts clés d’Azure Stack.
- Pour plus d’informations sur l’utilisation du stockage d’objets blob dans Azure Stack par les utilisateurs locataires, consultez la section [Services de stockage Azure Stack](/azure/azure-stack/user/azure-stack-storage-overview#azure-stack-storage-services).


### <a name="containers"></a>Conteneurs
Les utilisateurs locataires créent des conteneurs qui sont ensuite utilisés pour stocker des données d’objet blob. Alors que l’utilisateur décide du conteneur dans lequel placer les objets blob, le service de stockage utilise un algorithme pour identifier le volume dans lequel placer le conteneur. En règle générale, l’algorithme choisit le volume contenant la plus grande quantité d’espace disponible.  

Une fois qu’un objet blob a été placé dans un conteneur, il peut se développer pour utiliser plus d’espace. À mesure que vous ajoutez de nouveaux objets blob et que les objets blob existants se développent, l’espace disponible dans le volume de ce conteneur se réduit.  

Les conteneurs ne sont pas limités à un seul partage. Lorsque les données d’objets blob combinées dans un conteneur augmentent et utilisent 80 % ou plus de l’espace disponible, le conteneur passe en mode *dépassement de capacité*. En mode dépassement de capacité, les nouveaux objets blob créés dans ce conteneur sont alloués à un autre volume disposant d’un espace suffisant. Au fil du temps, un conteneur en mode dépassement de capacité peut présenter des objets blob répartis sur plusieurs volumes.

Lorsque 80 %, puis 90 % de l’espace disponible d’un volume sont utilisés, le système déclenche des alertes dans le portail d’administration d’Azure Stack. Les opérateurs de cloud doivent vérifier la capacité de stockage disponible et envisagez de rééquilibrer le contenu. Le service de stockage cesse de fonctionner si un disque est utilisé à 100 %, et aucune alerte supplémentaire n’est déclenchée.

### <a name="disks"></a>Disques
Les disques de machine virtuelle sont ajoutés aux conteneurs par les locataires, et incluent un disque de système d’exploitation. Les machines virtuelles peuvent également posséder un ou plusieurs disques de données. Les deux types de disque sont stockés en tant qu’objets blob de pages. Il est conseillé aux locataires de placer chaque disque dans un conteneur distinct pour améliorer les performances de la machine virtuelle.
- Chaque conteneur qui contient un disque (objet blob de pages) d’une machine virtuelle est considéré comme un conteneur attaché à la machine virtuelle qui possède le disque.
- Un conteneur dépourvu de disque d’une machine virtuelle est considéré comme un conteneur libre.

Les options permettant de libérer de l’espace dans un conteneur attaché [sont limitées](#move-vm-disks).
> [!TIP]  
> Les opérateurs de cloud ne gèrent pas directement les disques qui sont attachés aux machines virtuelles (VM) que les locataires peuvent ajouter à un conteneur. Toutefois, lors de la planification de la gestion de l’espace des partages de stockage, il peut être utile de comprendre comment les disques sont liés aux conteneurs et aux partages.

## <a name="monitor-shares"></a>Surveiller les partages
Utilisez PowerShell ou le portail d’administration pour surveiller les partages afin de pouvoir savoir à quel moment l’espace libre sera limité. Lorsque vous utilisez le portail, vous recevez des alertes sur les partages qui manquent d’espace.    

### <a name="use-powershell"></a>Utiliser PowerShell
En tant qu’opérateur de cloud, vous pouvez surveiller la capacité de stockage d’un partage à l’aide de la cmdlet **Get-AzsStorageShare** PowerShell. La cmdlet Get-AzsStorageShare retourne l’espace libre, alloué et total (en octets) de chacun des partages.   
![Exemple : retourner l’espace libre des partages](media/azure-stack-manage-storage-shares/free-space.png)

- La **capacité totale** est l’espace total (en octets) disponible dans le partage. Cet espace est utilisé pour les données et métadonnées gérées par les services de stockage.
- La **capacité utilisée** est la quantité de données (en octets) utilisée par toutes les extensions des fichiers qui stockent les données de locataire et les métadonnées associées.

### <a name="use-the-administrator-portal"></a>Utiliser le portail d’administration
En tant qu’opérateur de cloud, vous pouvez utiliser le portail d’administration pour afficher la capacité de stockage de tous les partages. **Accédez à Stockage** > **Partages de fichiers** pour ouvrir la liste de partages de fichiers où vous pouvez consulter les informations d’utilisation.
![Exemple : partages de fichiers de stockage](media/azure-stack-manage-storage-shares/storage-file-shares.png)
- **TOTAL** représente l’espace total (en octets) disponible dans le partage. Cet espace est utilisé pour les données et métadonnées gérées par les services de stockage.
- **UTILISÉ** représente la quantité de données (en octets) utilisée par toutes les extensions des fichiers qui stockent les données de locataire et les métadonnées associées.

### <a name="storage-space-alerts"></a>Alertes de l’espace de stockage
Lorsque vous utilisez le portail d’administration, vous recevez des alertes sur les partages qui manquent d’espace.

> [!IMPORTANT]
> En tant qu’opérateur de cloud, empêchez les partages d’être utilisés complètement. Quand un partage est utilisé à 100 %, le service de stockage ne fonctionne plus pour celui-ci. Pour récupérer de l’espace libre et les opérations de restauration dans un partage utilisé à 100 %, vous devez contacter le support Microsoft.

**Avertissement** : quand un partage de fichiers est utilisé à plus de 80 %, vous recevez une alerte de type *Avertissement* dans le portail d’administration : ![Exemple : alerte d’avertissement](media/azure-stack-manage-storage-shares/alert-warning.png)


**Critique** : quand un partage de fichiers est utilisé à plus de 90 %, vous recevez une alerte de type *Critique* dans le portail d’administration : ![Exemple : alerte critique](media/azure-stack-manage-storage-shares/alert-critical.png)

**Afficher les détails** : dans le portail d’administration, vous pouvez ouvrir les détails d’une alerte pour afficher les options d’atténuation : ![Exemple : afficher les détails de l’alerte](media/azure-stack-manage-storage-shares/alert-details.png)


## <a name="manage-available-space"></a>Gérer l’espace disponible
Lorsqu’il est nécessaire de libérer de l’espace dans un partage, utilisez d’abord les méthodes les moins invasives. Par exemple, essayez de récupérer de l’espace avant de migrer un conteneur.  

### <a name="reclaim-capacity"></a>Récupérer de la capacité
*Cette option s’applique aux déploiements de plusieurs nœuds et au kit de développement Azure Stack.*

Vous pouvez récupérer la capacité utilisée par les comptes locataires qui ont été supprimés. Cette capacité est automatiquement récupérée lorsque la [période de rétention](azure-stack-manage-storage-accounts.md#set-the-retention-period) des données est atteinte. Vous pouvez également choisir de la récupérer immédiatement.

Pour en avoir plus, voir [Récupérer de la capacité](azure-stack-manage-storage-accounts.md#reclaim) dans l’article Gérer les comptes de stockage dans Azure Stack.

### <a name="migrate-a-container-between-volumes"></a>Migrer un conteneur entre des volumes
*Cette option s’applique uniquement aux déploiements de plusieurs nœuds.*

En raison des modèles d’utilisation de locataire, certains partages de locataire utilisent davantage d’espace que d’autres. En conséquence, un partage exécuté peut manquer d’espace avant d’autres partages relativement peu utilisés.

Vous pouvez tenter de libérer de l’espace dans un partage surutilisé en migrant manuellement des conteneurs d’objets blob vers un autre partage. Vous pouvez migrer plusieurs conteneurs plus petits vers un partage unique dont la capacité est suffisante pour les contenir intégralement. Vous pouvez utiliser la migration pour déplacer des conteneurs *libres*. Les conteneurs libres sont des conteneurs dépourvus de disque pour une machine virtuelle.   

La migration consolide tous les objets blob d’un conteneur du nouveau partage.

- Si un conteneur passe en mode dépassement de capacité et a placé des objets blob dans des volumes supplémentaires, le nouveau partage doit disposer d’une capacité suffisante pour contenir tous les objets blob du conteneur que vous migrez. Cela inclut les objets blob qui se trouvent dans les partages supplémentaires.

- La cmdlet PowerShell *Get-AzsStorageContainer* identifie uniquement l’espace utilisé dans le volume initial d’un conteneur. La cmdlet n’identifie pas l’espace utilisé par les objets blob placés dans des volumes supplémentaires. Par conséquent, la taille totale d’un conteneur peut ne peut pas être évidente. Il est possible que la consolidation d’un conteneur dans un nouveau partage envoie ce nouveau partage dans une condition de dépassement de capacité où il place les données dans des partages supplémentaires. Vous devrez donc peut-être rééquilibrer les partages une nouvelle fois.

- Si vous ne disposez pas d’autorisations sur un groupe de ressources et ne pouvez pas utiliser PowerShell pour interroger les volumes supplémentaires à propos des données de dépassement de capacité, contactez le propriétaire de ces conteneurs et groupes de ressources pour connaître la taille totale des données à migrer avant de procéder à cette migration.  

> [!IMPORTANT]
> La migration des objets blob d’un conteneur est une opération hors connexion qui requiert l’utilisation de PowerShell. Tant que la migration n’est pas terminée, tous les objets blob du conteneur que vous migrez restent hors connexion et ne peuvent pas être utilisés.

#### <a name="to-migrate-containers-using-powershell"></a>Pour migrer des conteneurs en utilisant PowerShell
1. Vérifiez qu’[Azure PowerShell est installé et configuré](http://azure.microsoft.com/documentation/articles/powershell-install-configure/). Pour plus d'informations, consultez [Utilisation d'Azure PowerShell avec le Gestionnaire de ressources Azure](http://go.microsoft.com/fwlink/?LinkId=394767).
2.  Examinez le conteneur pour connaître les données du partage que vous envisagez de migrer. Pour identifier les meilleurs conteneurs candidats pour la migration d’un volume, utilisez la cmdlet **Get-AzsStorageContainer** :

    ```
    $shares = Get-AzsStorageShare
    $containers = Get-AzsStorageContainer -ShareName $shares[0].ShareName -Intent Migration
    ```
    Examinez ensuite $containers :
    ```
    $containers
    ```
    ![Exemple : $Containers](media/azure-stack-manage-storage-shares/containers.png)

3.  Identifiez les meilleurs partages de destination pour contenir le conteneur que vous migrez :
    ```
    $destinationshares = Get-AzsStorageShare -SourceShareName
    $shares[0].ShareName -Intent ContainerMigration
    ```
    Examinez ensuite $destinationshares :
    ```
    $destinationshares
    ```    
    ![Exemple : partages $destination](media/azure-stack-manage-storage-shares/examine-destinationshares.png)

4. Démarrez la migration d’un conteneur. Il s’agit d’un processus asynchrone. Si vous démarrez la migration des conteneurs supplémentaires avant la fin de la première migration, utilisez l’ID de travail pour suivre l’état de chaque migration.
  ```
  $jobId = Start-AzsStorageContainerMigration -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares[0].UncPath
  ```
  Examinez ensuite $jobId. Dans l’exemple suivant, remplacez *d62f8f7a-8b46-4f59-a8aa-5db96db4ebb0* par l’ID de travail que vous souhaitez examiner :
  ```
  $jobId
  d62f8f7a-8b46-4f59-a8aa-5db96db4ebb0
  ```
5. Utilisez l’ID de travail pour vérifier l’état du travail de migration. À la fin de la migration d’un conteneur, l’état **MigrationStatus** est défini sur **Terminé**.
  ```
  Get-AzsStorageContainerMigrationStatus -JobId $jobId
  ```
  ![Exemple : état de la migration](media/azure-stack-manage-storage-shares/migration-status1.png)

6.  Vous pouvez annuler une tâche de migration en cours d’exécution. Les travaux de migration annulés sont traités de façon asynchrone. Vous pouvez suivre l’annulation à l’aide de $jobid :

  ```
  Stop-AzsStorageContainerMigration -JobId $jobId
  ```
  ![Exemple : état de la restauration](media/azure-stack-manage-storage-shares/rollback.png)

7. Vous pouvez réexécuter la commande de l’étape 6 jusqu’à ce que l’état confirme que le travail de migration est **Annulé** :  
    ![Exemple : état Annulé](media/azure-stack-manage-storage-shares/cancelled.png)

### <a name="move-vm-disks"></a>Déplacer des disques de machine virtuelle
*Cette option s’applique uniquement aux déploiements de plusieurs nœuds.*

La méthode la plus extrême de gestion de l’espace implique le déplacement des disques de machine virtuelle. Comme le déplacement d’un conteneur attaché (contenant un disque de machine virtuelle) est complexe, contactez le support Microsoft pour effectuer cette action.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’[offre des machines virtuelles aux utilisateurs](azure-stack-tutorial-tenant-vm.md).
