---
title: "base de données Analysis Services aaaAzure de sauvegarde et de restauration | Documents Microsoft"
description: "Décrit comment toobackup et restauration un Azure Analysis Services base de données."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>Sauvegarde et restauration

Sauvegarde des bases de données de modèle tabulaire dans Azure Analysis Services est une grande partie hello même que pour les Services d’analyse local. Hello principale différence est l’endroit où vous stockez vos fichiers de sauvegarde. Fichiers de sauvegarde doivent être enregistrés conteneur tooa dans un [compte de stockage Azure](../storage/common/storage-create-storage-account.md). Vous pouvez utiliser un compte de stockage et un conteneur que vous avez déjà, ou bien en créer de nouveaux lors de la configuration des paramètres de stockage de votre serveur.

> [!NOTE]
> La création d’un compte de stockage peut entraîner un nouveau service facturable. toolearn, voir [tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

Les sauvegardes sont enregistrées avec l’extension .abf. Pour les modèles tabulaires en mémoire, les données et les métadonnées de modèle sont enregistrées. Pour les modèles tabulaires DirectQuery, seules les métadonnées de modèle sont stockées. Les sauvegardes peuvent être compressées et chiffrées, en fonction des options que vous choisissez hello. 



## <a name="configure-storage-settings"></a>Configurer les paramètres de stockage
Avant de sauvegarder, vous devez tooconfigure les paramètres de stockage pour votre serveur.


### <a name="tooconfigure-storage-settings"></a>paramètres de stockage tooconfigure
1.  Dans le portail Azure > **Paramètres**, cliquez sur **Sauvegarde**.

    ![Sauvegardes dans Paramètres](./media/analysis-services-backup/aas-backup-backups.png)

2.  Cliquez sur **Activé**, puis cliquez sur **Paramètres de stockage**.

    ![Activer](./media/analysis-services-backup/aas-backup-enable.png)

3. Sélectionnez un compte de stockage ou créez-en un nouveau.

4. Sélectionnez un conteneur ou créez-en un nouveau.

    ![Sélectionner un conteneur](./media/analysis-services-backup/aas-backup-container.png)

5. Enregistrez vos paramètres de sauvegarde.

    ![Enregistrer les paramètres de sauvegarde](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Sauvegarde

### <a name="toobackup-by-using-ssms"></a>toobackup à l’aide de SSMS

1. Dans SSMS, effectuez un clic droit sur une base de données > **Sauvegarder**.

2. Dans **Sauvegarder une base de données** > **Fichier de sauvegarde**, cliquez sur **Parcourir**.

3. Bonjour **enregistrer le fichier sous** boîte de dialogue, vérifiez le chemin d’accès du dossier hello et tapez un nom pour le fichier de sauvegarde hello. 

4. Bonjour **Backup Database** boîte de dialogue, sélectionnez les options.

    **Autoriser les fichiers remplacer** -Sélectionnez cette option toooverwrite sauvegarde de fichiers hello même nom. Si cette option n’est pas sélectionnée, hello fichier que vous utilisez ne peut pas avoir hello même nom en tant que fichier figurant déjà dans hello même emplacement.

    **Appliquer la compression** -Sélectionnez ce fichier de sauvegarde option toocompress hello. Les fichiers de sauvegarde compressés permettent d’économiser de l’espace disque, mais nécessite une utilisation un peu plus intensive du processeur. 

    **Chiffrer le fichier de sauvegarde** -Sélectionnez ce fichier de sauvegarde option tooencrypt hello. Cette option nécessite un fichier de sauvegarde de mot de passe fourni par l’utilisateur toosecure hello. mot de passe Hello empêche la lecture des données de sauvegarde hello autrement qu’une opération de restauration. Si vous choisissez les sauvegardes tooencrypt, stocker hello le mot de passe dans un endroit sûr.

5. Cliquez sur **OK** toocreate et enregistrez le fichier de sauvegarde hello.


### <a name="powershell"></a>PowerShell
Utilisez l’applet de commande [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).

## <a name="restore"></a>Restauration
Lors de la restauration, votre fichier de sauvegarde doit être hello compte de stockage que vous avez configurée pour votre serveur. Si vous devez toomove un fichier de sauvegarde à partir d’un compte de stockage tooyour emplacement local, utilisez [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) ou hello [AzCopy](../storage/common/storage-use-azcopy.md) utilitaire de ligne de commande. 



> [!NOTE]
> Si vous restaurez à partir d’un serveur local, vous devez supprimer tous les utilisateurs de domaine hello les rôles du modèle hello et ajoutez-les sauvegarder rôles toohello en tant qu’utilisateurs d’Azure Active Directory.
> 
> 

### <a name="toorestore-by-using-ssms"></a>toorestore à l’aide de SSMS

1. Dans SSMS, effectuez un clic droit sur une base de données > **Restaurer**.

2. Bonjour **Backup Database** boîte de dialogue, dans **le fichier de sauvegarde**, cliquez sur **Parcourir**.

3. Bonjour **rechercher les fichiers de base de données** boîte de dialogue, fichier hello sélectionnez toorestore.

4. Dans **restauration de base de données**, sélectionnez base de données hello.

5. Spécifiez les options. Options de sécurité doivent correspondre à des options de sauvegarde hello utilisées lors de la sauvegarde.


### <a name="powershell"></a>PowerShell

Utilisez l’applet de commande [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).


## <a name="related-information"></a>Informations connexes

[Des comptes de stockage Azure](../storage/common/storage-create-storage-account.md)  
[Haute disponibilité](analysis-services-bcdr.md)     
[Gérer Azure Analysis Services](analysis-services-manage.md)
