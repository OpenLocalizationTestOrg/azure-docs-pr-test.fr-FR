---
title: "aaaWhat est un ordinateur virtuel de science des données ? | Microsoft Docs"
description: "Comment tooget démarrer effectuant des scénarios clés analytique avec des données pour la science des ordinateurs virtuels."
keywords: "outils de science des données, machine virtuelle science des données, outils pour la science des données, science des données linux"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>Introduction toohello basée sur le cloud de Machine virtuelle pour la science des données pour Linux et Windows
Hello Machine virtuelle de science des données (DSVM) est une image personnalisée de la machine virtuelle sur Microsoft Azure cloud créé spécifiquement pour effectuer la recherche de données. Il a des nombreuses pour la science des données courants et les autres outils préinstallée et préconfigurée toojump-commencez la création d’applications intelligentes d’analytique avancée. Elle est disponible sur Windows Server et sur Linux. Nous vous proposons l’édition Windows de la DSVM sous Server 2016 et Server 2012. Nous offrons la version Linux de hello DSVM sur Ubuntu 16.04 LTS et sur les distributions de Linux basée sur les OpenLogic 7.2 CentOS. 

Cette rubrique explique ce que vous pouvez faire avec hello VM de science des données répertorie une partie des principaux scénarios de hello d’à l’aide de la machine virtuelle de hello, détaille les principales fonctionnalités hello disponibles sur hello Windows et les versions de Linux et fournit des instructions sur comment tooget démarrer leur utilisation.

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>Que puis-je faire avec hello Machine virtuelle de science des données ?
Hello hello Machine virtuelle de science des données vise tooprovide professionnels des données à tous les niveaux de compétence et les rôles avec un environnement de science des données sans friction. Cette machine virtuelle vous fait gagner le temps considérable nécessaire qu’il vous faudrait pour déployer vous-même un environnement comparable. Commencez immédiatement votre projet de science des données dans une nouvelle instance de machine virtuelle. 

Hello VM de science des données est conçu et configuré pour travailler avec des scénarios d’utilisation générale. Vous pouvez faire évoluer ou réduire votre environnement en fonction des besoins de votre projet. Vous est en mesure de toouse vos tâches de science des données de langue par défaut tooprogram. Vous pouvez installer d’autres outils et personnaliser le système de hello pour vos besoins.

## <a name="key-scenarios"></a>Principaux scénarios
Cette section propose certains scénarios clés pour le hello VM de science des données peut être déployé.

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>Préconfiguré bureau analytique dans le cloud de hello
Hello VM de science des données fournit une configuration de référence pour les équipes de science des données recherche tooreplace leur bureau local avec un ordinateur de bureau cloud géré. Cette ligne de base garantit que tous les chercheurs de données hello d’une équipe ont une configuration cohérente avec les expériences tooverify et promouvoir la collaboration. Il permet également de réduire les coûts en réduisant la charge de sysadmin hello et l’enregistrement dans les temps de hello nécessaires tooevaluate, installer et entretenir hello différents packages logiciels nécessaires toodo avancé analytique.  

### <a name="data-science-training-and-education"></a>Formation et éducation de la science des données
Formateurs de l’entreprise et aux enseignants qui indiquent généralement des classes de science des données fournissent un tooensure d’image de machine virtuelle que leurs étudiants ont une configuration cohérente et que les exemples hello fonctionnent comme prévu. Hello VM de science des données crée un environnement à la demande avec une configuration cohérente qui facilite les défis de prise en charge et incompatibilité hello. Les cas où ces environnements doivent toobe générés fréquemment, en particulier pour les classes de formation plus courts, bénéficier considérablement.

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>Flexibilité à la demande pour les projets d’envergure
Les concours de science des données ou la modélisation et l’exploration de données à grande échelle nécessitent une augmentation de la capacité matérielle, généralement sur une courte durée. Hello VM de science des données peut aider à répliquer hello données science environnement rapidement à la demande, sur les serveurs de montée en puissance parallèle qui permettent des expériences nécessitant une puissante toobe ressources informatiques exécutez.

### <a name="short-term-experimentation-and-evaluation"></a>Expérimentation et évaluation à court terme
Hello VM de science des données peut être utilisé tooevaluate ou en savoir plus les outils tels que Microsoft R Server, SQL Server, Visual Studio tools, Notebook, la profondeur de formation / ML kits d’outils et de nouveaux outils courants dans hello Communauté d’effort le programme d’installation minimale. Étant donné que hello VM de science des données permet de configurer rapidement, elle peut être appliquée dans d’autres scénarios d’utilisation à court terme telles que la réplication des expériences publiés, l’exécution des démonstrations, des procédures suivantes dans les sessions en ligne ou les didacticiels de conférence.

### <a name="deep-learning"></a>Apprentissage approfondi
pour la science des données Hello machine virtuelle peuvent servir de modèle d’apprentissage à l’aide d’algorithmes d’apprentissage automatique approfondie sur du matériel en fonction de GPU (unités de traitement graphique). Utilisant les capacités de cloud Azure de mise à l’échelle de machine virtuelle, DSVM vous permet d’utiliser matériel GPU basé sur le cloud hello conformément aux besoins. Un peut basculer tooa GPU en fonction des ordinateurs virtuels lors de l’apprentissage des modèles volumineux ou avez besoin de calculs à haut débit tout en conservant hello même disque de système d’exploitation.  Édition de Windows Server 2016 de Hello de DSVM est préinstallée avec les pilotes GPU, infrastructures et version GPU de hello approfondie d’algorithmes d’apprentissage. Sur hello Linux, ciblé sur le GPU de formation est activé uniquement sur hello [virtuels de science des données pour l’édition de Linux (Ubuntu)](http://aka.ms/dsvm/ubuntu). Vous pouvez déployer hello Ubuntu/Windows-2016 edition de machine virtuelle Azure de machine virtuelle de science des données toonon en fonction de GPU auquel cas toutes les infrastructures d’apprentissage approfondie hello seront en mode de secours toohello du processeur. Précédemment, nous avons publié un [kit d’apprentissage approfondi](http://aka.ms/dsvm/deeplearning) pour Windows Server 2012, mais nous recommandons l’utilisation de Windows Server 2016 pour des charges de travail d’apprentissage approfondi basées sur Windows. Hello basée sur CentOS Linux edition de hello DSVM contient uniquement hello processeur crée de certaines hello complète d’outils (CNTK, Tensorflow, MXNet) d’apprentissage, mais ne provient pas préinstallées avec les infrastructures et les pilotes GPU hello. 

## <a name="whats-included-in-hello-data-science-vm"></a>Ce qui est inclus dans hello VM de science des données ?
Hello Machine virtuelle de science des données comporte de nombreuses de science des données populaires et de profondeur outils déjà installé et configuré d’apprentissage. Il inclut également des outils qui permettent de facilement toowork avec différents produits analytique et de données Azure. Vous pouvez Explorer et créer des modèles prédictifs sur des jeux de données à grande échelle à l’aide de hello Microsoft R Server ou SQL Server 2016. Un ordinateur hôte d’autres outils à partir de la Communauté open source de hello et de Microsoft sont également inclus, ainsi que les exemples de code et les ordinateurs portables. Hello tableau suivant détaille et compare les composants principaux hello inclus dans hello Windows et Linux de hello Machine virtuelle de science des données.


| **Outil**                                                           | **Édition Windows** | **Édition Linux** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| [Microsoft R Open](https://mran.microsoft.com/open/) avec packages courants préinstallés   |O                      | O             |
| [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) Developer Edition inclut : <br />  L’infrastructure R haute performance distribuée et parallèle &nbsp;&nbsp;&nbsp;&nbsp;* [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started)<br />  &nbsp;&nbsp;&nbsp;&nbsp;*   [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) – nouveaux algorithmes ML de pointe de Microsoft <br />  &nbsp;&nbsp;&nbsp;&nbsp;*   [Opérationnalisation de R](https://msdn.microsoft.com/microsoft-r/operationalize/about)                                            |O                      | O <br/> (MicrosoftML n’est pas encore disponible)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) Pro-Plus avec activation partagée : Excel, Word et PowerPoint   |O                      |N              |
| [Anaconda Python](https://www.continuum.io/) 2.7, 3.5 avec packages populaires préinstallés    |O                      |O              |
| [JuliaPro](https://juliacomputing.com/products/juliapro.html) avec packages populaires préinstallés                         |O                      |O              |
| Bases de données relationnelles                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Developer Edition| [PostgreSQL](https://www.postgresql.org/) |
| Outils de base de données                                                       | * SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [bcp, sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> * Pilotes ODBC/JDBC| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/) (outil de requête), <br /> * bcp, sqlcmd <br /> * Pilotes ODBC/JDBC|
| Analytiques en base de données évolutives avec services SQL Server R | O     |N              |
| **[Serveur Bloc-notes Jupyter](http://jupyter.org/) avec noyaux suivants,**                                  | O     | O |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | O | O |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 et 3.5 | O | O |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Julia | O | O |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | N | O |
|     &nbsp;&nbsp;&nbsp;&nbsp;*   [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | N | O (Ubuntu uniquement) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | N | O |
| JupyterHub (serveur de bloc-notes multi-utilisateur)| N | O |
| **Outils de développement, éditeurs de code et EDI**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/community/) &gt; avec plug-in Git, Azure HDInsight (Hadoop), Data Lake, SQL Server Data Tools, [Node.js](https://github.com/Microsoft/nodejstools), [Python](http://aka.ms/ptvs), et [R Tools for Visual Studio (RTVS)](http://microsoft.github.io/RTVS-docs/) | O | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Visual Studio Code](https://code.visualstudio.com/) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [RStudio Server](https://www.rstudio.com/products/rstudio/#Server) | N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [PyCharm](https://www.jetbrains.com/pycharm/) | N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Atom](https://atom.io/) | N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Juno (Julia IDE)](http://junolab.org/)| O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;* Vim et Emacs | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git et GitBash | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;* .Net Framework | O | N |
| PowerBI Desktop | O | N |
| Tooaccess de kits de développement logiciel Azure et Cortana Intelligence Suite de services | O | O |
| **Outils de gestion et de déplacement de données** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Explorateur de stockage Microsoft Azure | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/overview) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Powershell | O | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | O | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Adlcopy (Azure Data Lake Storage)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | O | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Outil de migration de données DocDB](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | O | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Passerelle de gestion de données Microsoft](https://msdn.microsoft.com/library/dn879362.aspx) : déplace les données entre OnPrem et le cloud | O | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* Utilitaires de ligne de commande Unix/Linux | O | O |
| [Apache Drill](http://drill.apache.org) pour l’exploration des données | O | O |
| **Outils Machine Learning** |||
| &nbsp;&nbsp;&nbsp;&nbsp;* Intégration avec [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (R, Python) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Xgboost](https://github.com/dmlc/xgboost) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Rattle](http://rattle.togaware.com/) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [LightGBM](https://github.com/Microsoft/LightGBM) | N | O (Ubuntu uniquement) |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [H2O](https://www.h2o.ai/h2o/) | N | O (Ubuntu uniquement) |
| **Outils d’apprentissage approfondi basés sur processeur graphique (GPU)** |Édition Windows Server 2016  |Édition Ubuntu |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Microsoft Cognitive Toolkit (CNTK)](http://cntk.ai) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Tensorflow](https://www.tensorflow.org/) | O | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [MXNet](http://mxnet.io/) | O | O|
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Caffe et Caffe2](https://github.com/caffe2/caffe2) | N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Torch](http://torch.ch/) | N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Theano](https://github.com/Theano/Theano) | N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Keras](https://keras.io/)| N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [NVidia Digits](https://github.com/NVIDIA/DIGITS) | N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [CUDA, CUDNN, Nvidia Driver](https://developer.nvidia.com/cuda-toolkit) | O | O |
| **Plateforme Big Data (Devtest uniquement)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* [Spark](http://spark.apache.org/) autonome localité | N | O |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Hadoop](http://hadoop.apache.org/) local (HDFS, YARN) | N | O |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>Comment tooget démarrer avec hello VM de science des données Windows
* Créez une instance de l’édition de Windows DSVM hello souhaitée en accédant à
  * [Machine virtuelle basée sur Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  or 
  * [Machine virtuelle basée sur Windows Server 2012](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) 
* Cliquez sur hello **GET IT maintenant** bouton.
* Connectez-vous toohello machine virtuelle à partir de votre Bureau à distance à l’aide d’informations d’identification hello vous avez spécifié lors de la création de hello machine virtuelle.
* toodiscover et lancez outils hello disponibles, cliquez sur hello **Démarrer** menu.

## <a name="get-started-with-hello-linux-data-science-vm"></a>Prise en main hello VM de science des données Linux
* Créez une instance de hello souhaité édition Linux DSVM en naviguant trop
  * [Machine virtuelle Science des données basée sur Ubuntu](http://aka.ms/dsvm/ubuntu)

  or

  * [Machine virtuelle Science des données basée sur OpenLogic CentOS](http://aka.ms/dsvm/centos)

  
* Cliquez sur hello **maintenant** bouton.
* Connectez-vous à toohello machine virtuelle à partir d’un client SSH, tel que Putty ou commande SSH, à l’aide des informations d’identification hello spécifié lors de la création de hello machine virtuelle.
* Dans l’invite de hello, entrez dsvm-plus-info.
* Pour un graphique desktop, téléchargez le client de hello X2Go pour votre plateforme cliente [ici](http://wiki.x2go.org/doku.php/doc:installation:x2goclient) et suivez les instructions de hello dans le document de VM de science des données Linux hello [hello de configurer une Machine virtuelle Linux données Science](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>Étapes suivantes
### <a name="for-hello-windows-data-science-vm"></a>Pourquoi Windows VM de science des données
* Pour plus d’informations sur comment des outils disponible sur la version de Windows hello toorun spécifique, consultez [hello d’approvisionner la Machine virtuelle pour la science des données Microsoft](machine-learning-data-science-provision-vm.md) et
* Pour plus d’informations sur comment tooperform différentes tâches nécessaires pour votre projet de science des données sur hello machine virtuelle Windows, consultez [dix choses à faire sur hello pour la science des données Machine virtuelle](machine-learning-data-science-vm-do-ten-things.md).

### <a name="for-hello-linux-data-science-vm"></a>Pourquoi VM de science des données Linux
* Pour plus d’informations sur comment des outils disponible sur la version de Linux hello toorun spécifique, consultez [hello de configurer une Machine virtuelle pour la science des données Linux](machine-learning-data-science-linux-dsvm-intro.md).
* Pour une procédure pas à pas qui vous montre comment tooperform scientifiques de données commun plusieurs tâches avec hello Linux VM, consultez [science des données sur hello une Machine virtuelle pour la science des données Linux](machine-learning-data-science-linux-dsvm-walkthrough.md).

