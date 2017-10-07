---
title: "aaaGet démarrer avec les outils de base de données élastique | Documents Microsoft"
description: "Explication de la base de la fonctionnalité d’outils de base de données élastique hello de base de données SQL Azure, y compris une application d’exemple de simple à s’exécuter."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>Prise en main des outils de base de données élastiques
Ce document vous présente l’expérience de développement toohello en vous aidant à toorun hello exemple d’application. exemple Hello crée une simple application partitionnée et explore des fonctionnalités clés des outils de base de données élastique. exemple Hello illustre les fonctions Hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md).

bibliothèque de hello tooinstall, accédez trop[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). bibliothèque de Hello est installée avec hello exemple d’application qui est décrite dans hello suivant la section.

## <a name="prerequisites"></a>Composants requis
* Visual Studio 2012 ou ultérieur avec C#. Téléchargez une version gratuite à la page [Téléchargements Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* NuGet 2.7 ou ultérieur. version la plus récente tooget hello, consultez [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).

## <a name="download-and-run-hello-sample-app"></a>Téléchargez et exécutez l’exemple d’application hello
Hello **élastique outils de base de données pour SQL Azure - mise en route** exemple d’application illustre les aspects les plus importants d’expérience en développement hello pour les applications partitionnées qui utilisent des outils de base de données élastique hello. Il s’intéresse aux principaux cas d’utilisation pour la [gestion des cartes de partition](sql-database-elastic-scale-shard-map-management.md), le [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) et [l’interrogation de plusieurs partitions](sql-database-elastic-scale-multishard-querying.md). toodownload et exemple d’exécution hello, procédez comme suit : 

1. Télécharger hello [élastique outils de base de données SQL Azure - exemple de mise en route de](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) à partir de MSDN. Décompressez hello exemple tooa d’emplacement que vous choisissez.

2. toocreate un projet, ouvrez hello **ElasticScaleStarterKit.sln** solution hello **c#** active.

3. Dans la solution hello pour exemple de projet hello, ouvrez hello **app.config** fichier. Suivez ensuite les instructions de hello dans hello fichier tooadd le nom de votre serveur de base de données SQL Azure et vos informations de connexion (nom d’utilisateur et mot de passe).

4. Générez et exécutez l’application hello. Lorsque vous y êtes invité, activez Visual Studio toorestore hello NuGet packages de solution de hello. Cela télécharge la version la plus récente de la bibliothèque cliente de base de données élastique hello hello de NuGet.

5. Faites des essais avec toolearn de différentes options hello en savoir plus sur les fonctionnalités de bibliothèque hello du client. Notez les étapes hello hello prend d’application dans la sortie de console hello et estimez le code de hello tooexplore libre coulisses hello.
   
    ![Progression][4]

Félicitations. Vous avez correctement conçu et exécuté votre première application partitionnée à l’aide des outils de base de données élastique sur Azure SQL Database. Utilisez Visual Studio ou SQL Server Management Studio tooconnect tooyour SQL de base de données et un coup de œil les partitions hello qui hello exemple créé. Vous remarquerez les nouvelles bases de données exemple partition et une base de données du Gestionnaire de mappage partition cet exemple hello a créé.

> [!IMPORTANT]
> Nous vous recommandons de toujours utiliser hello dernière version de Management Studio afin que vous êtes toujours synchronisé avec tooAzure de mises à jour et de la base de données SQL. [Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>Éléments clés de l’exemple de code hello
* **La gestion des partitions et partition mappe**: hello code illustre comment toowork avec des partitions, des plages et des mappages dans le fichier de hello **ShardManagementUtils.cs**. Pour plus d’informations, consultez [montée en charge des bases de données avec le Gestionnaire de carte de partitions hello](http://go.microsoft.com/?linkid=9862595).  

* **Routage dépendant des données**: routage de partition de transactions toohello droite est illustré **DataDependentRoutingSample.cs**. Pour plus d’informations, consultez la page [Routage dépendant des données](http://go.microsoft.com/?linkid=9862596). 

* **Interrogation sur plusieurs partitions**: interrogation de partitions est illustré dans le fichier de hello **MultiShardQuerySample.cs**. Pour plus d’informations, consultez la page [Interrogation de plusieurs partitions](http://go.microsoft.com/?linkid=9862597).

* **Ajout de partitions vides**: hello itératif Ajout de nouvelles partitions vides est effectuée par le code hello dans le fichier de hello **CreateShardSample.cs**. Pour plus d’informations, consultez [montée en charge des bases de données avec le Gestionnaire de carte de partitions hello](http://go.microsoft.com/?linkid=9862595).

### <a name="other-elastic-scale-operations"></a>Autres opérations de mise à l’échelle élastique
* **Fractionnement d’une partition existante**: partitions de toosplit hello fonctionnalité est fournie par hello **outil de fusion et fractionnement**. Pour plus d’informations, consultez la page [Déplacement de données entre des bases de données cloud montées en charge](sql-database-elastic-scale-overview-split-and-merge.md).

* **La fusion de partitions existantes**: fusion de partitions est également effectuées à l’aide de hello **outil de fusion et fractionnement**. Pour plus d’informations, consultez la page [Déplacement de données entre des bases de données cloud montées en charge](sql-database-elastic-scale-overview-split-and-merge.md).   

## <a name="cost"></a>Coût
outils de base de données élastique Hello sont gratuits. Lorsque vous utilisez les outils de base de données élastique, vous ne recevez pas des frais supplémentaires sur le coût de hello de votre utilisation d’Azure. 

Par exemple, exemple d’application hello crée de nouvelles bases de données. coût Hello pour ce dépend de l’édition de base de données SQL hello que vous choisissez et de hello Azure de l’utilisation de votre application.

Pour plus d’informations sur la tarification, consultez la page [Tarification de SQL Database](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les outils de base de données élastique, consultez hello suivant des pages :

* Exemples de code : 
  * [Outils de base de données élastique pour SQL Azure - Bien démarrer](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [Outils de base de données élastique pour SQL Azure - Intégration Entity Framework](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE).
  * [Partitionner l’élasticité sur le centre de scripts](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* Blog : [Annonce de la mise à l’échelle élastique](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)
* Microsoft Virtual Academy : [implémentant le montée en puissance parallèle à l’aide de partitionnement avec hello élastique de base de données Client bibliothèque vidéo](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* Channel 9 : [Vidéo de présentation de la mise à l’échelle élastique](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* Forum de discussion : [Forum sur Azure SQL Database](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* performances de toomeasure : [compteurs de performances pour le Gestionnaire de carte de partitions](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

