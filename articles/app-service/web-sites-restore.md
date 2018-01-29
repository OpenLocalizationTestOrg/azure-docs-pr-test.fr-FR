---
title: Restauration d'une application dans Azure App Service
description: "Découvrez comment restaurer votre application à partir d'une sauvegarde."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 60b55acaf687dae76e054b428b8d6584d8eb09f8
ms.sourcegitcommit: 933af6219266cc685d0c9009f533ca1be03aa5e9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2017
---
# <a name="restore-an-app-in-azure"></a>Restauration d'une application dans Azure App Service
Cet article vous explique comment restaurer une application dans [Azure App Service](../app-service/app-service-web-overview.md) que vous avez précédemment sauvegardée (voir [Sauvegarde de votre application dans Azure](web-sites-backup.md)). Vous pouvez restaurer votre application avec ses bases de données liées à la demande à un état antérieur ou créer une application à partir de l’une des sauvegardes de votre application d’origine. Azure App Service prend en charge les bases de données suivantes pour la sauvegarde et restauration :
- [Base de données SQL](https://azure.microsoft.com/en-us/services/sql-database/)
- [Azure Database pour MySQL (Version préliminaire)](https://azure.microsoft.com/en-us/services/mysql)
- [Azure Database pour PostgreSQL (Version préliminaire)](https://azure.microsoft.com/en-us/services/postgres)
- [MySQL dans l’application](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

La restauration à partir de sauvegardes est disponible pour des applications exécutées dans les niveaux **Standard** et **Premium**. Pour en savoir plus sur la mise à l’échelle de votre application, consultez [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md). Notez que le niveau **Premium** autorise un plus grand nombre de sauvegardes quotidiennes que le niveau **Standard**.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Restauration d’une application à partir d’une sauvegarde existante
1. Dans la page **Paramètres** de votre application dans le portail Azure, cliquez sur **Sauvegardes** pour afficher la page **Sauvegardes**. Cliquez ensuite sur **Restaurer**.
   
    ![Sélectionner Restaurer maintenant][ChooseRestoreNow]
2. Dans la page **Restaurer**, sélectionnez tout d’abord la source de la sauvegarde.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    L’option de **sauvegarde d’une application** vous montre toutes les sauvegardes existantes de l’application actuelle, et vous pouvez facilement sélectionner une.
    L’option de **stockage** vous permet de sélectionner un fichier ZIP de sauvegarde quelconque à partir de n’importe quel compte de stockage Azure et conteneur existants dans votre abonnement.
    Si vous essayez de restaurer une sauvegarde d’une autre application, utilisez l’option **Stockage** .
3. Ensuite, spécifiez la destination de la restauration de l'application dans **Destination de restauration**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Si vous choisissez **Remplacer**, toutes les données existantes dans votre application actuelle seront effacées et remplacées. Avant de cliquer sur **OK**, vérifiez que c'est bien ce que vous voulez faire.
   > 
   > 
   
    Vous pouvez sélectionner **Application existante** pour restaurer la sauvegarde d'une application vers une autre application dans le même groupe de ressources. Avant d'utiliser cette option, vous devez avoir créé une autre application dans votre groupe de ressources avec mise en miroir de la configuration de la base de données sur celle définie dans la sauvegarde de l'application. Vous pouvez également créer une **nouvelle** application dans laquelle restaurer votre contenu.

4. Cliquez sur **OK**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Télécharger ou supprimer une sauvegarde à partir d’un compte de stockage
1. Dans la page **Parcourir** principale du portail Azure, sélectionnez **Comptes de stockage**. La liste de vos comptes de stockage existants s’affiche.
2. Sélectionnez le compte de stockage contenant la sauvegarde que vous souhaitez télécharger ou supprimer. La page du compte de stockage s’affiche.
3. Dans la page du compte de stockage, sélectionnez le conteneur souhaité.
   
    ![Afficher les conteneurs][ViewContainers]
4. Sélectionnez le fichier de sauvegarde à télécharger ou à supprimer.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Cliquez sur **Télécharger** ou **Supprimer** selon ce que vous souhaitez faire.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Surveillance d’une opération de restauration
Pour afficher les détails concernant la réussite ou l’échec de l’opération de restauration de l’application, accédez à la page **Journal d’activité** dans le portail Azure.  
 

Faites défiler la liste pour trouver l’opération de restauration souhaitée et cliquez dessus.

La page de détails affiche les informations disponibles concernant l’opération de restauration.

## <a name="automate-with-scripts"></a>Automatiser des tâches à l’aide de scripts

Vous pouvez automatiser la gestion des sauvegardes à l’aide de scripts, en utilisant [Azure CLI](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).

Pour obtenir des exemples, consultez :

- [Exemples d’interface de ligne de commande Azure](app-service-cli-samples.md)
- [Exemples Azure PowerShell](app-service-powershell-samples.md)

<!-- ## Next Steps
You can backup and restore App Service apps using REST API. -->


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
