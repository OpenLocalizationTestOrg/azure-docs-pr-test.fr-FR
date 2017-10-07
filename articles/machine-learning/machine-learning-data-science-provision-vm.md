---
title: "aaaProvision hello Machine virtuelle de science des données Microsoft | Documents Microsoft"
description: "Configurez et créez une machine virtuelle pour la science des données sur Microsoft Azure pour vos besoins d’analyse et d’apprentissage automatique."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Hello d’approvisionner la Machine virtuelle pour la science des données Microsoft
Hello Machine virtuelle de science des données Microsoft est une image de machine virtuelle (VM) de Windows Azure préalablement installé et configuré avec plusieurs outils courants qui sont couramment utilisées pour l’analytique des données et l’apprentissage. outils Hello inclus sont :

* Microsoft R Server Developer Edition
* Distribution Anaconda Python
* Jupyter Notebook (avec noyaux R, Python)
* Visual Studio Community Edition
* Power BI Desktop
* SQL Server 2016 Developer Edition
* Outils Machine Learning et Analyse des données
  * [Computational Network Toolkit (CNTK)](https://github.com/Microsoft/CNTK): kit de ressources logicielles d’apprentissage approfondi de Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): système de Machine Learning rapide prenant en charge des techniques (apprentissage en ligne, hachage, allreduce, réductions, learning2search, actif et interactif).
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): outil offrant une implémentation rapide et précise des arborescences optimisées.
  * [Vibrer](http://rattle.togaware.com/) (hello facilement l’outil d’analyse R tooLearn) : un outil qui facilite la prise en main de l’analytique des données et de la machine learning dans R facile, avec l’exploration de données basées sur une interface graphique utilisateur et de modélisation avec la génération de code automatique R.
  * [mxnet](https://github.com/dmlc/mxnet): infrastructure de formation approfondie conçue pour offrir efficacité et flexibilité.
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/) : logiciel Machine Learning et d’exploration des données visuelle dans Java.
  * [Apache Drill](https://drill.apache.org/) : moteur de requêtes SQL sans schéma pour Hadoop, NoSQL et le stockage cloud.  Prend en charge d’ODBC et JDBC tooenable interfaces interrogation NoSQL et fichiers à partir des Outils BI standard tels que Power BI, Excel, Tableau.
* Bibliothèques dans les langages R et Python à utiliser dans Azure Machine Learning et d’autres services Azure
* GIT, notamment l’interpréteur de commandes Git toowork avec les référentiels de code source, notamment GitHub, Visual Studio Team Services
* Ports Windows de plusieurs utilitaires de ligne de commande Linux populaires (notamment awk, sed, perl, grep, find, wget, curl, etc.) accessibles via l’invite de commandes. 

La science des données consiste à itérer sur une séquence de tâches :

1. Recherche, chargement et traitement des données
2. Création et test des modèles
3. Déploiement de modèles hello pour l’utilisation dans des applications intelligentes

Les chercheurs de données utilisent divers outils toocomplete ces tâches. Il peut s’agir de toofind beaucoup de temps hello des versions appropriées des logiciels de hello, puis téléchargez et les installer. Hello Machine virtuelle de science des données Microsoft peut faciliter ce fardeau en fournissant une image prêt à l’emploi qui peut être configurée sur Azure avec tous les outils courants plusieurs préalablement installé et configuré. 

Hello Machine virtuelle de science des données Microsoft élan à votre projet analytique. Il vous permet de toowork sur des tâches dans plusieurs langues, y compris R, Python, SQL et c#. Visual Studio fournit un toodevelop IDE et tester votre code est toouse facile. Bonjour Azure SDK inclus dans hello machine virtuelle vous permet de toobuild vos applications à l’aide de divers services de plateforme cloud de Microsoft. 

Cette image de machine virtuelle de science des données ne génère pas de frais. Vous ne payez que pour les frais d’utilisation d’Azure hello qui dépendent de la taille hello de machine virtuelle de hello que vous configurez. Plus de détails sur hello calcul frais sont accessibles dans la section de détails de tarification sur hello de hello [Machine virtuelle de science des données](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) page. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Autres Versions de hello Machine virtuelle de science des données
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) image est également disponible, avec la plupart des hello des mêmes outils que hello image système Windows. Une image [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) est également disponible, avec de nombreux outils similaires et des cadres de formation approfondis.

## <a name="prerequisites"></a>Composants requis
Avant de pouvoir créer une Machine virtuelle de science des données Microsoft, vous devez disposer de hello :

* **Un abonnement Azure**: voir d’un seul, tooobtain [version d’évaluation gratuite de Azure d’obtenir](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un compte de stockage Azure**: voir d’un seul, toocreate [créer un compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). Vous pouvez également compte de stockage hello peut être créé dans le cadre du processus de hello de création hello machine virtuelle si vous ne souhaitez pas toouse un compte existant.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Création d’une machine virtuelle pour la science des données
Voici une instance de Machine virtuelle de science des données Microsoft de hello hello étapes toocreate :

1. Accédez de machine virtuelle de toohello liste sur [portail Azure](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Sélectionnez hello **créer** bouton en hello bas toobe est effectuée dans un Assistant.![ configurer les données-science-machine virtuelle](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Hello Assistant utilisé toocreate hello requiert de la Machine virtuelle de science des données Microsoft **entrées** pour chacun des hello **cinq étapes** énuméré sur hello à droite de cette illustration. Voici hello entrées nécessitées tooconfigure chaque de ces étapes :
   
   1. **Concepts de base**
      
      1. **Name**(Nom) : nom du serveur Data Science que vous créez.
      2. **Nom d’utilisateur**: identifiant de connexion du compte administrateur.
      3. **Mot de passe**: mot de passe du compte administrateur.
      4. **Abonnement**: Si vous avez plusieurs abonnements, sélectionnez hello sur quel hello machine est toobe créées et facturées.
      5. **Resource Group**(Groupe de ressources) : vous pouvez créer un nouveau groupe ou utiliser un groupe existant.
      6. **Emplacement**: centre de données Sélectionnez hello qui convient le mieux. Il est généralement de centre de données hello qui comporte une grande partie de vos données ou qui est le plus proche emplacement physique tooyour pour l’accès réseau plus rapide.
   2. **Taille**: sélectionnez un des types de serveur hello qui répond à vos exigences fonctionnelles et les contraintes liées au coût. Sélectionnez « Afficher tout » pour obtenir d’autres choix de tailles de machines virtuelles
   3. **Paramètres**:
      
      1. **Type de disque** : choisissez Premium si vous préférez un disque SSD. Sinon, choisissez « Standard ».
      2. **Compte de stockage**: vous pouvez créer un nouveau compte de stockage Azure dans votre abonnement ou utilisez-en un existant Bonjour même *emplacement* qui a été choisie sur hello **notions de base** étape de l’Assistant de hello.
      3. **Autres paramètres**: vous utilisez généralement simplement des valeurs par défaut de hello. Vous pouvez pointer sur le lien informatif a hello pour une aide sur les champs spécifiques hello au cas où vous souhaiteriez utiliser hello tooconsider les valeurs par défaut.
   4. **Résumé**: vérifiez que toutes les informations que vous avez saisies sont correctes.
   5. **Acheter**: cliquez sur **acheter** toostart l’approvisionnement hello. Un lien est fourni toohello les termes du contrat de transaction de hello. Hello machine virtuelle n’a pas de tous les frais supplémentaires au-delà de calcul hello pour la taille du serveur hello choisis Bonjour **taille** étape. 

> [!NOTE]
> l’approvisionnement Hello doit prendre environ 10 à 20 minutes. état de Hello hello provisionnement est affiché sur hello portail Azure.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>Comment tooaccess hello Machine virtuelle de science des données Microsoft
Une fois hello machine virtuelle est créée, vous pouvez Bureau à distance à l’aide de hello Admin informations d’identification que vous avez configuré dans hello précédent **notions de base** section. 

Une fois que votre machine virtuelle est créée et configurée, vous êtes prêt toostart à l’aide des outils hello qui sont installés et configurés sur celui-ci. Il existe des icônes pour un grand nombre des outils de hello et mosaïques du menu Démarrer. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>Comment toocreate un mot de passe fort pour le bloc-notes et démarrer hello server de l’ordinateur portable
Par défaut, serveur de jupyter Notebook hello est préconfiguré mais désactivé sur hello machine virtuelle jusqu'à ce que vous définissez un mot de passe disponible. exécution hello suivant de commande à partir d’une invite de commandes sur hello données Science Machine virtuelle ou double-cliquez sur raccourci du bureau hello que nous vous avons fourni de toocreate un mot de passe fort pour serveur de jupyter Notebook hello installé sur l’ordinateur de hello, appelé  **Notebook définir le mot de passe & début** à partir d’un compte d’administrateur local de machine virtuelle.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Suivez les messages de type hello et choisissez un mot de passe lorsque vous y êtes invité.

Hello script précédent crée un hachage de mot de passe et le magasin dans le fichier de configuration hello Notebook situé à : **C:\ProgramData\jupyter\jupyter_notebook_config.py** sous le nom du paramètre hello ***c. NotebookApp.password***.

script de Hello permet également et s’exécutent de serveur de Notebook hello en arrière-plan de hello. Notebook serveur est créée comme une tâche windows Bonjour Planificateur de tâches WIndows appelé **Start_IPython_Notebook**.  Vous avez peut-être toowait pendant quelques secondes après avoir défini un mot de passe hello avant d’ouvrir le bloc-notes hello sur votre navigateur. Consultez la section hello ci-dessous intitulée **bloc-notes Jupyter** sur la façon dont tooaccess hello serveur jupyter Notebook. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Outils installés sur hello Machine virtuelle de science des données Microsoft

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
Si vous le souhaitez toouse R pour vos analytique, hello machine virtuelle a édition développeur Microsoft R Server installée. Microsoft R Server est une plateforme d’analyse d’entreprise basée sur R, prise en charge, extensible et sécurisée, que vous pouvez largement déployer. Prise en charge des statistiques des données volumineuses, modélisation prédictive et capacités d’apprentissage, R Server prend en charge hello complète d’analytique – exploration, analyse, visualisation et modélisation. En utilisant et en étendant R open source, Microsoft R Server est entièrement compatible avec les scripts R, des fonctions et des packages CRAN, tooanalyze des données à l’échelle de l’entreprise. Il traite également les limitations de mémoire de hello Open Source r en ajoutant des parallèles et segmenté de traitement des données. Cela vous permet d’analytique toorun sur des données plus volumineuses que tout ce qui tient dans la mémoire principale.  Visual Studio Community Edition est inclus sur hello que machine virtuelle contient hello R Tools pour extension Visual Studio qui fournit un IDE complète pour l’utilisation de R. Vous pouvez également télécharger et utiliser ainsi comme les autres environnements IDE [RStudio](http://www.rstudio.com). 

### <a name="python"></a>Python
Pour un développement basé sur Python, les versions 2.7 et 3.5 de la distribution Anaconda Python ont été installées. Cette distribution contient hello Python avec environ 300 de hello packages plus populaires mathématiques, engineering et données analytique de base. Vous pouvez utiliser les outils Python pour les commandes Visual les Studio (PTVS) qui est installée dans l’édition de Visual Studio Community 2015 hello ou l’un des hello Qu'ide fourni avec Anaconda comme inactif ou Spyder. Vous pouvez lancer une recherche sur la barre de recherche hello (**Win** + **S** clé).

> [!NOTE]
> toopoint hello outils Python pour Visual Studio au Anaconda Python 2.7 et 3.5, vous devez toocreate des environnements personnalisés pour chaque version. tooset ces chemins d’accès de l’environnement Bonjour Visual Studio 2015 Community Edition, accédez trop**outils** -> **outils Python** -> **desenvironnementsPython** puis cliquez sur **+ personnalisé**. 
> 
> 

Anaconda Python 2.7 est installé sous C:\Anaconda et Anaconda Python 3.5 est installé sous c:\Anaconda\envs\py35. Pour obtenir des instructions détaillées, consultez la [documentation de PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) . 

### <a name="jupyter-notebook"></a>Jupyter Notebook
Distribution anaconda est également fourni avec un bloc-notes jupyter, un environnement de code tooshare et l’analyse. Un serveur Jupyter Notebook a été préconfiguré avec Python 2.7, Python 3.4, Python 3.5 et les noyaux R. Une icône de bureau nommé « bloc-notes Jupyter toolaunch hello navigateur tooaccess hello server de l’ordinateur portable. Si vous êtes sur hello machine virtuelle via le Bureau à distance, vous pouvez également consulter [https://localhost:9999 /](https://localhost:9999/) tooaccess hello serveur de jupyter Notebook lorsque connecté toohello machine virtuelle.

> [!NOTE]
> Si vous recevez des avertissements relatifs au certificat, vous pouvez les ignorer. 
> 
> 

Nous avons inclus dans le package plusieurs exemples d’agendas dans Python et dans R. hello comment afficher des ordinateurs portables Notebook toowork Microsoft R Server, SQL Server 2016 R Services (analytique dans base de données), Python, Microsoft cognitifs ToolKit (CNTK) pour en savoir plus approfondie et autres Azure une fois que vous vous connectez tooJupyter les technologies. Vous pouvez voir des exemples de toohello hello lien sur la page d’accueil hello bloc-notes après que vous être authentifié à l’aide du mot de passe hello créé dans une étape antérieure de toohello bloc-notes jupyter. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community Edition
Visual Studio Community edition doit être installée sur la machine virtuelle de hello. Il s’agit d’une version gratuite de hello populaires IDE de Microsoft, vous pouvez utiliser à des fins d’évaluation et des petites équipes. Vous pouvez extraire des termes du contrat de licence de hello [ici](https://www.visualstudio.com/support/legal/mt171547).  Ouvrez Visual Studio en double-cliquant sur l’icône du bureau hello ou hello **Démarrer** menu. Vous pouvez également lancer une recherche de programmes avec **Win** + **S** et en entrant « Visual Studio ». Là, vous pouvez créer des projets dans des langages tels que C#, Python, R, node.js. Plug-ins sont également installés qui la rendent toowork pratique avec les services Azure, Azure Data Catalog, Azure HDInsight (Hadoop, Spark) et Azure Data Lake. 

> [!NOTE]
> Il est possible que vous receviez un message indiquant que votre période d’évaluation a expiré. Entrez vos informations d’identification de compte Microsoft ou créer un nouveau compte gratuit tooget accès toohello Visual Studio Community Edition. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Developer Edition
Une version développeur de SQL Server 2016 avec analytique de R Services toorun dans base de données est fournie sur hello machine virtuelle. R Services fournit une plateforme pour développer et déployer des applications intelligentes. Vous pouvez utiliser hello riche et puissant langage R et hello de nombreux packages à partir de modèles de toocreate Communauté hello et générer des prédictions pour vos données de SQL Server. Vous pouvez conserver des données de fermer toohello analytique car R Services (de-de base de données) intégrer le langage de hello R avec SQL Server. Cela élimine les coûts de hello et les risques de sécurité liés au déplacement des données.

> [!NOTE]
> Hello SQL Server 2016 developer edition peut uniquement être utilisé pour le développement et à des fins de test. Vous avez besoin d’une licence toorun dans la production. 
> 
> 

Vous pouvez accéder à SQL server de hello en lançant **SQL Server Management Studio**. Le nom de votre machine virtuelle est rempli comme hello nom du serveur. Utilisez l’authentification Windows lorsque connecté tant qu’hello admin sur Windows. Dans SQL Server Management Studio, vous pouvez créer d’autres utilisateurs, créer des bases de données, importer des données et exécuter des requêtes SQL. 

analytique tooenable dans base de données à l’aide de Microsoft R, exécutez hello suivant de commande en tant qu’une fois l’action dans SQL Server management studio une fois connecté en tant qu’administrateur de serveur hello. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Microsoft Azure
Plusieurs outils Azure sont installés sur hello machine virtuelle :

* Il existe un raccourci sur le bureau de tooaccess documentation du Kit de développement logiciel Azure hello. 
* **AzCopy**: utilisé toomove des données vers et depuis votre compte de stockage Microsoft Azure. utilisation de toosee, type **Azcopy** à une utilisation de l’invite de commandes toosee hello. 
* **Microsoft Azure Storage Explorer**: utilisé toobrowse par le biais des objets hello que vous avez stocké dans votre tooand des données de compte de stockage Azure et de transfert à partir du stockage Azure. Vous pouvez taper **Explorateur de stockage** dans la recherche ou de recherche sur hello tooaccess de menu Windows Démarrer cet outil. 
* **Adlcopy**: utilisé toomove données tooAzure Data Lake. utilisation de toosee, type **adlcopy** dans une invite de commandes. 
* **dtui**: utilisé tooand de données toomove à partir d’Azure Cosmos DB, une base de données NoSQL sur le cloud de hello. Il suffit de taper **dtui** dans une invite de commandes. 
* **Passerelle de gestion des données de Microsoft** : permet le déplacement des données entre des sources de données locales et le cloud. Elle est utilisée dans les outils tels que Azure Data Factory. 
* **Microsoft Azure Powershell**: utiliser un outil tooadminister vos ressources Azure Bonjour Powershell langage de script est également installé sur votre machine virtuelle. 

### <a name="power-bi"></a>Power BI
toohelp vous générez des tableaux de bord et visualisations excellentes, hello **Power BI Desktop** a été installé. Utilisez ces données de toopull outil à partir de différentes sources, tooauthor vos tableaux de bord, rapports et toopublish les toohello cloud. Pour plus d’informations, consultez hello [Power BI](http://powerbi.microsoft.com) site. Vous pouvez trouver Power BI desktop sur le menu Démarrer de hello. 

> [!NOTE]
> Vous avez besoin d’un tooaccess de compte Office 365 Power BI. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Autres outils de développement Microsoft
Hello [ **Microsoft Web Platform Installer** ](https://www.microsoft.com/web/downloads/platform.aspx) peuvent être utilisé toodiscover et télécharger d’autres outils de développement Microsoft. Il existe également un outil de toohello raccourci fourni sur le bureau de Machine virtuelle de science des données Microsoft hello.  

## <a name="important-directories-on-hello-vm"></a>Répertoires importants sur hello machine virtuelle
| Item | Répertoire |
| --- | --- |
| Configurations de serveur de Jupyter Notebook |C:\ProgramData\jupyter |
| Répertoire des exemples de Jupyter Notebook |c:\dsvm\notebooks |
| Autres exemples |c:\dsvm\samples |
| Anaconda (valeur par défaut : Python 2.7) |c:\Anaconda |
| Environnement Anaconda Python 3.5 |c:\Anaconda\envs\py35 |
| Répertoire de l’instance R Server autonome (instance par défaut de R basée sur R3.2.2) |C:\Program Files\Microsoft SQL Server\130\R_SERVER |
| Répertoire de l’instance de base de données R Server (R3.2.2) |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES |
| Répertoire de l’instance Microsoft R Open (R3.3.1) |C:\Program Files\Microsoft\MRO-3.3.1 |
| Outils divers |c:\dsvm\tools |

> [!NOTE]
> Les instances de hello que machine virtuelle de science des données Microsoft créé avant 1.5.0 (avant le 3 septembre 2016) utilisées une structure de répertoire légèrement différent que le nombre spécifié dans le tableau précédent de hello. 
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Voici certains toocontinue étapes suivant votre apprentissage et l’exploration. 

* Explorer hello divers outils de science des données sur la recherche de données hello machine virtuelle en cliquant sur hello menu démarrent et la récupération des outils de hello répertoriés dans le menu de hello.
* Accédez trop**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** pour obtenir des exemples à l’aide de la bibliothèque de RevoScaleR hello dans R qui prend en charge d’analytique des données à l’échelle de l’entreprise.  
* Lire l’article de hello : [10 opérations pouvant être exécutées sur hello pour la science des données Machine virtuelle](http://aka.ms/dsvmtenthings)
* Découvrez comment les solutions analytiques toobuild fin tooend systématiquement à l’aide de hello [processus de science des données équipe](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Visitez hello [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com) pour ce hello utilisez Cortana Intelligence Suite d’exemples analytique d’apprentissage et de données machine. Nous fournissons également une icône sur hello **Démarrer** menu et sur le bureau hello de galerie de toothis hello machine virtuelle.

