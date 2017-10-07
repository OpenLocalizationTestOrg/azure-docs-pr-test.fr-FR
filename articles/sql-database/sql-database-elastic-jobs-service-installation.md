---
title: "tâches de base de données élastique aaaInstalling | Documents Microsoft"
description: "Suivez les étapes de fonction de travail élastique hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>Vue d’ensemble de l’installation de Tâches de bases de données élastiques
[**Les travaux de base de données élastiques** ](sql-database-elastic-jobs-overview.md) peut être installé via PowerShell ou via hello Portal.You classique de Azure peuvent avoir accès toocreate et gérer des travaux à l’aide des API PowerShell de hello uniquement si vous installez le package de PowerShell hello. En outre, hello PowerShell APIs fournir beaucoup plus de fonctionnalités que le portail de hello à ce stade.

Si vous avez déjà installé **des travaux de base de données élastique** via hello portail à partir d’un fichier **pool élastique**, préliminaire Powershell hello inclut des scripts tooupgrade votre installation existante. Il est fortement recommandé, tooupgrade toohello de votre installation dernières **des travaux de base de données élastique** parti de tootake d’ordre de nouvelles fonctionnalités exposées par le biais des composants hello APIs PowerShell.

## <a name="prerequisites"></a>Composants requis
* Un abonnement Azure. Pour un essai gratuit, consultez [Version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell. Installer la version la plus récente hello à l’aide de hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376). Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
* [L’utilitaire de ligne de commande NuGet](https://nuget.org/nuget.exe) est utilisé tooinstall hello élastique de base de données du package travaux. Pour plus d’informations, consultez http://docs.nuget.org/docs/start-here/installing-nuget.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>Téléchargez et importez le package de PowerShell travaux hello élastique de base de données
1. Lancer la fenêtre de commande PowerShell de Microsoft Azure et accédez répertoire toohello où vous avez téléchargé l’utilitaire de ligne de commande NuGet (nuget.exe).
2. Téléchargez et importez **des travaux de base de données élastique** package dans le répertoire en cours de hello avec hello de commande suivante :
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Hello **des travaux de base de données élastique** fichiers sont placés dans le répertoire local de hello dans un dossier nommé **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** où *x.x.xxxx.x* reflète le numéro de version hello. applets de commande PowerShell Hello (y compris les fichiers .dll du client requis) se trouvent dans hello **tools\ElasticDatabaseJobs** sous-répertoire et hello tooinstall de scripts PowerShell, la mise à niveau et désinstaller également résider dans hello  **outils** sous-répertoire.
3. Accédez toohello outils sous-répertoire sous hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x dossier en tapant cd outils, par exemple :
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Exécutez Active ElasticDatabaseJobs de hello.\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello dans $home\Documents\WindowsPowerShell\Modules. Cette opération va automatiquement importer le module hello pour l’utilisation, par exemple :
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>Installer les composants de travaux hello élastique de base de données à l’aide de PowerShell
1. Lancez une fenêtre de commande PowerShell de Microsoft Azure et accédez toohello \tools sous-répertoire sous le dossier de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello : tapez cd \tools
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Exécutez le script PowerShell de.\InstallElasticDatabaseJobs.ps1 hello et fournir des valeurs pour ses variables demandées. Ce script crée les composants hello décrits dans [composants et la tarification des travaux de base de données élastique](sql-database-elastic-jobs-overview.md#components-and-pricing) configuration hello Azure Cloud Service tooappropriately qui l’utilisent les composants dépendants hello.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

Lorsque vous exécutez cette commande, une fenêtre s’ouvre dans laquelle vous devez entrer un **nom d’utilisateur** et un **mot de passe**. Ce n’est pas vos informations d’identification Azure, entrez le nom d’utilisateur hello et le mot de passe administrateur hello toocreate souhaité pour le nouveau serveur de hello.

paramètres Hello fournis dans cet exemple d’appel peuvent être modifiées pour les paramètres de votre choix. suivant de Hello fournit plus d’informations sur le comportement de hello de chaque paramètre :

<table style="width:100%">
  <tr>
    <th>Paramètre</th>
    <th>Description</th>
  </tr>

<tr>
    <td>ResourceGroupName</td>
    <td>Fournit le nom de groupe de ressources Azure hello créé hello toocontain nouvellement créé les composants Azure. Ce paramètre par défaut est trop « __ElasticDatabaseJob ». Il n’est pas recommandé toochange cette valeur.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Fournit des toobe d’emplacement Azure hello utilisé pour hello nouvellement créé les composants Azure. Ce paramètre par défaut est toohello emplacement du centre des États-Unis.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Offre plusieurs hello tooinstall de threads de travail de service. Ce paramètre par défaut est too1. Un plus grand nombre de threads de travail peut être utilisé tooscale out hello service tooprovide haute disponibilité et. Il est recommandé de toouse « 2 » pour les déploiements qui nécessitent une haute disponibilité du service de hello.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Fournit la taille de machine virtuelle hello pour une utilisation dans hello Service Cloud. Ce paramètre par défaut est tooA0. Les valeurs de paramètres d’A0/A1/A2/A3 sont acceptées obligeant les processus de travail hello rôle toouse une taille ExtraSmall/petit/moyen/grand, respectivement. Pour plus d’informations sur les tailles de rôle de travail, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Fournit l’objectif de niveau de service hello pour une édition Standard. Ce paramètre par défaut est tooS0. Les valeurs de paramètre de S0/S1/S2/S3 sont acceptées obligeant hello de base de données SQL Azure toouse hello SLO respectif. Pour plus d’informations sur les objectifs de niveau de service SQL Database, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Fournit le nom d’utilisateur admin hello pour hello créé sur le serveur de base de données SQL Azure. Lorsque ne pas spécifié, une fenêtre d’informations d’identification PowerShell s’ouvre tooprompt pour des informations d’identification hello.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Fournit un mot de passe administrateur hello pour hello créé sur le serveur de base de données SQL Azure. Quand il est ne pas fourni, une fenêtre d’informations d’identification PowerShell s’ouvre tooprompt pour des informations d’identification hello.</td>
</tr>
</table>

Pour les systèmes qui ciblent de très nombreux de travaux en cours d’exécution en parallèle sur un grand nombre de bases de données, il est recommandé de toospecify paramètres tels que : - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>Mettez à jour une installation de composants de Tâches de bases de données élastiques existante à l'aide de PowerShell
**Tâches de bases de données élastiques** peut être mis à jour dans une installation existante pour assurer la mise à l'échelle et la haute disponibilité. Ce processus permet de futures mises à niveau du code de service sans avoir toodrop et recréer la base de données de contrôle hello. Ce processus peut également être utilisé au sein de hello même version toomodify hello service taille ou hello serveur worker nombre d’ordinateurs virtuels.

taille de machine virtuelle tooupdate hello d’une installation, hello exécution suivante du script avec les paramètres mis à jour toohello les valeurs de votre choix.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>Paramètre</th>
  <th>Description</th>
</tr>

  <tr>
    <td>ResourceGroupName</td>
    <td>Identifie le nom de groupe de ressources Azure hello utilisé lorsque les composants de tâche hello élastique de base de données ont été installés initialement. Ce paramètre par défaut est trop « __ElasticDatabaseJob ». Dans la mesure où il n’est pas recommandé toochange cette valeur, vous ne devez pas avoir toospecify ce paramètre.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Offre plusieurs hello tooinstall de threads de travail de service.  Ce paramètre par défaut est too1.  Un plus grand nombre de threads de travail peut être utilisé tooscale out hello service tooprovide haute disponibilité et.  Il est recommandé de toouse « 2 » pour les déploiements qui nécessitent une haute disponibilité du service de hello.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Fournit la taille de machine virtuelle hello pour une utilisation dans hello Service Cloud. Ce paramètre par défaut est tooA0. Les valeurs de paramètres d’A0/A1/A2/A3 sont acceptées obligeant les processus de travail hello rôle toouse une taille ExtraSmall/petit/moyen/grand, respectivement. Pour plus d’informations sur les tailles de rôle de travail, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Installer les composants de travaux hello élastique de base de données à l’aide de hello portail
Une fois que vous avez [créé un pool élastique](sql-database-elastic-pool-manage-portal.md), vous pouvez installer **des travaux de base de données élastique** l’exécution de tooenable composants des tâches d’administration sur chaque base de données dans le pool élastique de hello. Contrairement aux lorsque à l’aide de hello **des travaux de base de données élastique** PowerShell APIs, interface du portail hello est actuellement restreint tooonly l’exécution par rapport à un pool existant.

**Estimation du temps toocomplete :** 10 minutes.

1. À partir de l’affichage de tableau de bord hello du pool élastique de hello via hello [Azure Portal](https://portal.azure.com/#) , cliquez sur **travail de création de**.
2. Si vous créez un travail pour hello première fois, vous devez installer **des travaux de base de données élastique** en cliquant sur **les termes du contrat de l’aperçu**.
3. Accepter les termes du contrat de hello en cliquant sur hello case à cocher.
4. Dans la vue de hello « installer les services », cliquez sur **informations d’identification du travail**.
   
    ![L’installation des services de hello][1]
5. Tapez un nom d'utilisateur et un mot de passe d'administrateur de base de données. Dans le cadre de l’installation de hello, un nouveau serveur de base de données SQL Azure est créé. Dans ce nouveau serveur, une base de données, appelé base de données du contrôle hello, est créé et utilisé des métadonnées de toocontain hello pour les travaux de la base de données élastique. nom d’utilisateur Hello et mot de passe créés ici sont utilisés à des fins de hello de la journalisation dans la base de données de contrôle toohello. Informations d’identification distincte sont utilisée pour l’exécution du script par rapport aux bases de données hello dans le pool de hello.
   
    ![Créer le nom d'utilisateur et le mot de passe][2]
6. Cliquez sur le bouton OK de hello. composants de Hello sont créés pour vous dans quelques minutes dans un nouveau [groupe de ressources](../azure-resource-manager/resource-group-overview.md). nouveau groupe de ressources Hello est épinglé toohello démarrer le tableau, comme indiqué ci-dessous. Les travaux de base de données une fois créés, élastique (Service de cloud computing, de la base de données SQL, Service Bus et stockage) sont créés dans le groupe de hello.
   
    ![groupe de ressources dans le panneau de démarrage][3]
7. Si vous essayez de toocreate ou gérer un travail pendant que les tâches de base de données élastique s’installe lorsque vous fournissez **informations d’identification** hello message suivant s’affiche.
   
    ![Déploiement en cours][4]

Si la désinstallation est nécessaire, supprimer le groupe de ressources hello. Consultez [comment toouninstall hello élastique de base de données de la tâche composants](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Étapes suivantes
Vérifiez les informations d’identification avec les droits appropriés hello pour l’exécution du script est créée sur chaque base de données dans le groupe de hello, pour plus d’informations, consultez [sécurisation de votre base de données SQL](sql-database-manage-logins.md).
Consultez [création et gestion des travaux d’une base de données élastique](sql-database-elastic-jobs-create-and-manage.md) tooget a démarré.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
