---
title: "aaaIdentify avancée des scénarios d’analytique pour Azure Machine Learning | Documents Microsoft"
description: "Sélectionnez les scénarios appropriés de hello pour cette opération avancée analytique prédictive avec hello processus de science des données de Team."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Scénarios d’analyses avancées dans Azure Machine Learning
Cet article présente plusieurs exemples de sources de données et les scénarios de cibles qui peuvent être gérés par hello hello [processus de science des données équipe (TDSP)](data-science-process-overview.md). Hello TDSP fournit une approche systématique pour toocollaborate équipes sur la création d’applications intelligentes. les scénarios de Hello présentées ici illustrent les options disponibles dans le flux de travail de traitement des données hello qui dépendent des caractéristiques des données hello, les emplacements source et les référentiels de cible dans Azure.

Hello **arbre de décision** pour les scénarios d’exemple hello qui convient à vos données et l’objectif de sélection est présentée dans la dernière section de hello.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

Chacun des hello les sections suivantes présente un exemple de scénario. Pour chaque scénario, un flux possible de science des données ou d’analyse avancée et les ressources Azure connexes sont répertoriés.

> [!NOTE]
> **Pour tous les scénarios suivants de hello, vous devez :**
> <br/>
> 
> * [Créer un compte de stockage](../storage/common/storage-create-storage-account.md)
>   <br/>
> * [Création d’un espace de travail Microsoft Azure Machine Learning](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>Scénario \#1 : toomedium petit jeu de données tabulaires dans des fichiers locaux
![Fichiers locaux toomedium petit][1]

#### <a name="additional-azure-resources-none"></a>Autres ressources Azure : aucune
1. Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
2. Téléchargez un jeu de données.
3. Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux téléchargés.

## <a name="smalllocalprocess"></a>Scénario \#2 : toomedium petit jeu de données de fichiers locaux qui nécessitent un traitement
![Petite toomedium des fichiers locaux avec le traitement][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Autres ressources Azure : Machine virtuelle Azure (serveur IPython Notebook)
1. Créez une machine virtuelle Azure exécutant IPython Notebook.
2. Télécharger des données tooan conteneur de stockage Azure.
3. Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données à partir du conteneur de stockage Azure.
4. Transformer les données toocleaned, sous forme de tableau.
5. Enregistrez les données transformées dans des objets blob Azure.
6. Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
7. Lire les données de hello d’objets BLOB Windows Azure à l’aide de hello [importer des données] [ import-data] module.
8. Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.

## <a name="largelocal"></a>Scénario \#3 : jeu de données volumineux de fichiers locaux, ciblant des objets blob Azure
![Fichiers locaux volumineux][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Autres ressources Azure : Machine virtuelle Azure (serveur IPython Notebook)
1. Créez une machine virtuelle Azure exécutant IPython Notebook.
2. Télécharger des données tooan conteneur de stockage Azure.
3. Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.
4. Transformer les données toocleaned, sous forme de tableau si nécessaire.
5. Le cas échéant, explorez des données et créez des fonctionnalités.
6. Extrayez un échantillon de données petit à moyen.
7. Enregistrer les données de hello échantillonnée dans des objets BLOB Azure.
8. Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Lire les données de hello d’objets BLOB Windows Azure à l’aide de hello [importer des données] [ import-data] module.
10. Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.

## <a name="smalllocaltodb"></a>Scénario \#4 : petit toomedium de jeu de données de fichiers locaux, ciblant SQL Server dans une Machine virtuelle Azure
![Toomedium petits fichiers locaux tooSQL DB dans Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)
1. Créez une Machine virtuelle Azure exécutant SQL Server + IPython Notebook.
2. Télécharger des données tooan conteneur de stockage Azure.
3. Pré-traitez et nettoyez les données dans un conteneur de stockage Azure à l’aide d’IPython Notebook.
4. Transformer les données toocleaned, sous forme de tableau si nécessaire.
5. Enregistrer les fichiers de données local tooVM (notebooks portable est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence à des lecteurs tooVM).
6. Charger des données tooSQL serveur de base de données en cours d’exécution sur une machine virtuelle Azure.
   
   Option \#1 : utilisation de SQL Server Management Studio.
   
   * Connexion tooSQL machine virtuelle du serveur
   * Exécutez SQL Server Management Studio.
   * Créez la base de données et les tables cibles.
   * Utilisez une en bloc de hello importer des données de hello tooload de méthodes à partir des fichiers d’ordinateur virtuel local.
   
   Option \#2 : utilisation d’IPython Notebook – déconseillé pour les jeux de données de tailles moyenne et supérieure
   
   <!-- -->    
   * Utilisez tooaccess de chaîne de connexion ODBC SQL Server sur l’ordinateur virtuel.
   * Créez la base de données et les tables cibles.
   * Utilisez une en bloc de hello importer des données de hello tooload de méthodes à partir des fichiers d’ordinateur virtuel local.
7. Le cas échéant, explorez des données et créez des fonctionnalités. Notez que les fonctions hello n’avez pas besoin de toobe matérialisé dans les tables de base de données hello. Uniquement Notez hello requête nécessaire toocreate les.
8. Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.
9. Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
10. Les données de lecture hello directement à partir de SQL Server à l’aide de hello hello [importer des données] [ import-data] module. Coller hello nécessaire la requête qui extrait les champs, crée des fonctionnalités et exemples de données si nécessaire directement dans hello [importer des données] [ import-data] requête.
11. Créez un flux d’expérience Azure Machine Learning commençant par le ou les jeux de données ingérés.

## <a name="largelocaltodb"></a>Scénario \#5 : jeu de données volumineux dans des fichiers locaux, ciblant SQL Server dans une machine virtuelle Azure
![Les fichiers volumineux local tooSQL DB dans Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)
1. Créez une machine virtuelle Azure exécutant SQL Server et le serveur IPython Notebook.
2. Télécharger des données tooan conteneur de stockage Azure.
3. (Facultatif) Pré-traitez et nettoyez les données.
   
   a.  Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.
   
       blobs.
   
   b.  Transformer les données toocleaned, sous forme de tableau si nécessaire.
   
   c.  Enregistrer les fichiers de données local tooVM (notebooks portable est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence à des lecteurs tooVM).
4. Charger des données tooSQL serveur de base de données en cours d’exécution sur une machine virtuelle Azure.
   
   a.  Connexion tooSQL machine virtuelle du serveur.
   
   b.  Si les données ne sont pas déjà enregistrées, téléchargez les fichiers de données à partir d’Azure
   
       storage container toolocal-VM folder.
   
   c.  Exécutez SQL Server Management Studio.
   
   d.  Créez la base de données et les tables cibles.
   
   e.  Utilisez une en bloc de hello importer des données de hello tooload de méthodes.
   
   f.  Si les jointures de table sont nécessaires, créer des jointures de tooexpedite d’index.
   
   > [!NOTE]
   > Pour un chargement plus rapide des tailles de données volumineux, il est recommandé de créer des tables partitionnées et importer en bloc hello données en parallèle. Pour plus d’informations, consultez [importation parallèle des données tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Le cas échéant, explorez des données et créez des fonctionnalités. Notez que les fonctions hello n’avez pas besoin de toobe matérialisé dans les tables de base de données hello. Uniquement Notez hello requête nécessaire toocreate les.
6. Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.
7. Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Les données de lecture hello directement à partir de SQL Server à l’aide de hello hello [importer des données] [ import-data] module. Coller hello nécessaire la requête qui extrait les champs, crée des fonctionnalités et exemples de données si nécessaire directement dans hello [importer des données] [ import-data] requête.
9. Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé

## <a name="largedbtodb"></a>Scénario \#6 : jeu de données volumineux dans une base de données SQL Server locale, ciblant SQL Server dans une machine virtuelle Azure
![Grande base de données SQL locale tooSQL DB dans Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)
1. Créez une machine virtuelle Azure exécutant SQL Server et le serveur IPython Notebook.
2. Utilisez une des données de salutation exporter des données de hello tooexport de méthodes à partir de fichiers toodump de SQL Server.
   
   > [!NOTE]
   > Si vous décidez de toomove toutes les données de base de données de hello localement, une autre (plus rapide) méthode toomove hello complète de la base de données toothe instance SQL Server dans Azure. Ignorer les données de tooexport étapes hello, créer la base de données et la base de données de chargement et d’importation données toohello cible et procédez comme autre méthode de hello.
   > 
   > 
3. Téléchargez le conteneur de stockage de tooAzure de fichiers dump.
4. Charge hello données tooa de données SQL Server en cours d’exécution sur une Machine virtuelle de Azure.
   
   a.  Connexion toohello machine virtuelle SQL Server.
   
   b.  Télécharger les fichiers de données à partir d’un dossier de stockage Azure conteneur toohello local-VM.
   
   c.  Exécutez SQL Server Management Studio.
   
   d.  Créez la base de données et les tables cibles.
   
   e.  Utilisez une en bloc de hello importer des données de hello tooload de méthodes.
   
   f.  Si les jointures de table sont nécessaires, créer des jointures de tooexpedite d’index.
   
   > [!NOTE]
   > Pour un chargement plus rapide des tailles de données volumineux, créer des tables partitionnées et toobulk importer hello des données en parallèle. Pour plus d’informations, consultez [importation parallèle des données tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Le cas échéant, explorez des données et créez des fonctionnalités. Notez que les fonctions hello n’avez pas besoin de toobe matérialisé dans les tables de base de données hello. Uniquement Notez hello requête nécessaire toocreate les.
6. Choisissez une taille d’échantillon de données, si nécessaire et/ou souhaité.
7. Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Les données de lecture hello directement à partir de SQL Server à l’aide de hello hello [importer des données] [ import-data] module. Coller hello nécessaire la requête qui extrait les champs, crée des fonctionnalités et exemples de données si nécessaire directement dans hello [importer des données] [ import-data] requête.
9. Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé.

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>Autre méthode toocopy une base de données complète à partir d’un tooAzure de SQL Server sur site de la base de données SQL
![Détachez la base de données locale et d’attachement tooSQL DB dans Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Autres ressources Azure : Machine virtuelle Azure (SQL Server / serveur IPython Notebook)
tooreplicate hello ensemble de données SQL Server dans votre machine virtuelle SQL Server, vous devez copier une base de données à partir d’un serveur d’emplacement tooanother, en supposant que hello peut être placée temporairement hors connexion. Pour cela, dans hello Explorateur d’objets SQL Server Management Studio ou en utilisant les commandes Transact-SQL équivalentes hello.

1. Détachez la base de données de hello à l’emplacement source de hello. Pour plus d’informations, consultez la rubrique [Détacher une base de données](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).
2. Dans la fenêtre de l’Explorateur Windows ou l’invite de commandes Windows, hello de copie de détacher les fichiers de base de données ou fichiers et fichier journal ou emplacement cible toohello des fichiers sur hello machine virtuelle SQL Server dans Azure.
3. Joindre l’instance de SQL Server cible hello copié les fichiers toohello. Pour plus d’informations, consultez la rubrique [Attacher une base de données](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).

[Déplacer une base de données à l’aide de la méthode de détachement et d’attachement (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>Scénario \#7 : données volumineuses (« Big Data ») dans des fichiers locaux, ciblant une base de données Hive dans des clusters Hadoop Azure HDInsight
![Données volumineuses (« Big Data ») dans la base de données Hive cible locale][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>Autres ressources Azure : cluster Hadoop Azure HDInsight et machine virtuelle Azure (serveur IPython Notebook)
1. Créez une machine virtuelle Azure exécutant le serveur IPython Notebook.
2. Créez un cluster Hadoop Azure HDInsight.
3. (Facultatif) Pré-traitez et nettoyez les données.
   
   a.  Pré-traitez et nettoyez les données dans IPython Notebook, en accédant aux données des objets blob Azure.
   
       blobs.
   
   b.  Transformer les données toocleaned, sous forme de tableau si nécessaire.
   
   c.  Enregistrer les fichiers de données local tooVM (notebooks portable est en cours d’exécution sur l’ordinateur virtuel, les lecteurs locaux font référence à des lecteurs tooVM).
4. Téléchargez le conteneur de valeur par défaut toohello de données de cluster Hadoop de hello hello étape 2.
5. Charger la base de données tooHive de cluster Azure HDInsight Hadoop.
   
   a.  Connectez-vous à toohello le nœud principal du cluster Hadoop de hello
   
   b.  Ouvrez hello de ligne de commande Hadoop.
   
   c.  Entrez le répertoire racine de ruche hello par commande `cd %hive_home%\bin` depuis la ligne de commande de Hadoop.
   
   d.  Exécuter la base de données toocreate hello ruche de requêtes et les tables et charger des données à partir des tables de tooHive de stockage blob.
   
   > [!NOTE]
   > Si les données de salutation sont grande, les utilisateurs peuvent créer de table de Hive hello avec des partitions. Ensuite, les utilisateurs peuvent utiliser un `for` boucle Bonjour de ligne de commande Hadoop sur les données de tooload de nœud principal hello en hello ruche table est partitionnée par partition.
   > 
   > 
6. Le cas échéant, explorez des données et créez des fonctionnalités dans la ligne de commande Hadoop. Notez que les fonctions hello n’avez pas besoin de toobe matérialisé dans les tables de base de données hello. Uniquement Notez hello requête nécessaire toocreate les.
   
   a.  Connectez-vous à toohello le nœud principal du cluster Hadoop de hello
   
   b.  Ouvrez hello de ligne de commande Hadoop.
   
   c.  Entrez le répertoire racine de ruche hello par commande `cd %hive_home%\bin` depuis la ligne de commande de Hadoop.
   
   d.  Exécuter des requêtes Hive hello en ligne de commande Hadoop sur le nœud principal de hello hello Hadoop tooexplore hello de données de cluster et créer des fonctionnalités en fonction des besoins.
7. Si nécessaire, et/ou vous le souhaitez, les exemples de toofit de données hello dans Azure Machine Learning Studio.
8. Connectez-vous à toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Lire les données de salutation directement à partir de hello `Hive Queries` à l’aide de hello [importer des données] [ import-data] module. Coller hello nécessaire la requête qui extrait les champs, crée des fonctionnalités et exemples de données si nécessaire directement dans hello [importer des données] [ import-data] requête.
10. Flux d’expérience Azure Machine Learning simple commençant par le jeu de données téléchargé.

## <a name="decisiontree"></a>Arbre de décision pour le choix du scénario
- - -
Hello diagramme suivant résume les scénarios hello décrits ci-dessus et hello technologie et les processus d’Analytique avancée choix effectués prenant tooeach des scénarios de hello détaillé. Notez que le traitement des données, l’exploration, l’ingénierie de fonctionnalité et échantillonnage peuvent prendre placer dans un ou plusieurs (méthode) à l’environnement, à la source de hello, intermédiaire, et/ou les environnements cibles – et peuvent se poursuivre de manière itérative en fonction des besoins. diagramme de Hello sert à obtenir une illustration de certains flux possibles uniquement et ne fournit pas une énumération exhaustive.

![Exemples de scénarios de procédure pas à pas pour le processus DS][8]

### <a name="advanced-analytics-in-action-examples"></a>Analyse avancée en action, exemples
De bout en bout pour Azure Machine Learning procédures pas à pas qui emploient hello technologie et les processus d’Analytique avancée à l’aide de jeux de données publics, consultez :

* [Processus TDSP (Team Data Science Process) en action : utilisation de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).
* [Processus TDSP (Team Data Science Process) en action : utilisation de clusters Hadoop HDInsight](machine-learning-data-science-process-hive-walkthrough.md).

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
