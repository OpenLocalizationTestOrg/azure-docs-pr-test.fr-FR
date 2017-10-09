---
title: "aaaProvision hello données Science Machine virtuelle pour Linux (Ubuntu) sur Azure | Documents Microsoft"
description: "Configurer et créer une données Science Machine virtuelle pour Linux (Ubuntu) sur Azure toodo analytique et l’apprentissage."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 037c126c0a35d8065fc89c591089df73d2b91425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-data-science-virtual-machine-for-linux-ubuntu"></a>Configurer hello Machine virtuelle de science des données pour Linux (Ubuntu)
Hello virtuels de science des données pour Linux est basé sur un Ubuntu image de machine virtuelle qui le rend facile tooget démarrer l’apprentissage approfondie sur Azure. Outils d’apprentissage approfondi :

  * [Caffe](http://caffe.berkeleyvision.org/) : infrastructure d’apprentissage approfondi conçue pour la vitesse, l’expressivité et la modularité
  * [Caffe2](https://github.com/caffe2/caffe2) : version multiplateforme de Caffe
  * [Computational Network Toolkit (CNTK)](https://github.com/Microsoft/CNTK) : kit de ressources logicielles d’apprentissage approfondi de Microsoft Research
  * [H2O](https://www.h2o.ai/) : plateforme Big Data open source et interface utilisateur graphique
  * [Keras](https://keras.io/) : API de réseau neuronal principal dans Python pour Theano et TensorFlow
  * [MXNet](http://mxnet.io/) : bibliothèque d’apprentissage approfondi flexible et efficace avec de nombreuses liaisons de langage
  * [NVIDIA DIGITS](https://developer.nvidia.com/digits) : système graphique qui simplifie les tâches d’apprentissage approfondi courantes
  * [TensorFlow](https://www.tensorflow.org/) : bibliothèque open source de Google pour l’intelligence artificielle
  * [Theano](http://deeplearning.net/software/theano/) : bibliothèque Python pour définir, optimiser et évaluer efficacement les expressions mathématiques impliquant des tableaux multidimensionnels
  * [Torch](http://torch.ch/) : infrastructure informatique scientifique avec prise en charge étendue des algorithmes d’apprentissage automatique
  * Pilote NVIDIA hello CUDA et cuDNN
  * Nombreux exemples de bloc-notes Jupyter

Toutes les bibliothèques sont des versions GPU hello, si elles seront exécuteront également sur hello du processeur.

Hello Machine virtuelle Linux données Science contient également des outils courants pour les activités développement et de la science des données, y compris :

* Microsoft R Server Developer Edition avec Microsoft R Open
* Distribution Anaconda Python (versions 2.7 et 3.5), comprenant les bibliothèques courantes d’analyse des données
* JuliaPro - une distribution organisée du langage Julia avec des bibliothèques scientifiques et d’analyse de données courantes
* Instance Spark autonome et nœud Hadoop unique (HDFS, Yarn)
* JupyterHub : un serveur de bloc-notes Jupyter multi-utilisateur prenant en charge les noyaux R, Python, PySpark et Julia
* Explorateur de stockage Azure
* Interface de ligne de commande (CLI) Azure pour la gestion des ressources Azure
* Outils de Machine Learning
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) : système d’apprentissage automatique rapide prenant en charge des techniques (apprentissage en ligne, hachage, allreduce, réductions, learning2search, actif et interactif)
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/) : outil offrant une implémentation rapide et précise des arborescences optimisées
  * [Rattle](http://rattle.togaware.com/) : outil graphique qui facilite la prise en main de l’analyse des données et de l’apprentissage automatique dans R
  * [LightGBM](https://github.com/Microsoft/LightGBM) : infrastructure d’amélioration progressive rapide, distribuée et hautes performances
* Kit SDK Azure dans Java, Python, node.js, Ruby, PHP
* Bibliothèques dans les langages R et Python à utiliser dans Azure Machine Learning et d’autres services Azure
* Outils de développement et éditeurs (RStudio, PyCharm, IntelliJ, Emacs, vim)


La science des données consiste à itérer sur une séquence de tâches :

1. Recherche, chargement et traitement des données
2. Création et test des modèles
3. Déploiement de modèles hello pour l’utilisation dans des applications intelligentes

Les chercheurs de données utilisent divers outils toocomplete ces tâches. Il peut y avoir beaucoup de temps toofind hello des versions appropriées des logiciels de hello et ensuite toodownload, compilez et installez ces versions.

Hello Machine virtuelle Linux données Science peut faciliter cette charge considérablement. Utiliser toojump-démarrer votre projet analytique. Il vous permet de toowork sur des tâches dans différents langages, notamment R, Python, SQL, Java et C++. Bonjour Azure SDK inclus dans hello machine virtuelle vous permet de toobuild vos applications à l’aide de divers services sur Linux pour la plateforme de cloud de Microsoft hello. En outre, vous avez accès tooother langues comme Ruby, Perl, PHP et node.js également préinstallés.

Cette image de machine virtuelle de science des données ne génère pas de frais. Vous payez uniquement hello matériel Azure l’utilisation des frais qui sont évalués en fonction de taille hello de machine virtuelle hello que vous préparez. Plus de détails sur hello calcul frais se trouvent sur hello [page d’annonce de machine virtuelle sur Azure Marketplace de hello](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/).

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Autres Versions de hello Machine virtuelle de science des données
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) image est également disponible, avec la plupart des hello des mêmes outils que hello Ubuntu image. Une image [Windows](machine-learning-data-science-provision-vm.md) est également disponible.

## <a name="prerequisites"></a>Prérequis
Avant de pouvoir créer une machine virtuelle pour la science des données pour Linux, vous devez disposer d’un abonnement Azure. tooobtain, consultez [version d’évaluation gratuite de Azure d’obtenir](https://azure.microsoft.com/free/).

## <a name="create-your-data-science-virtual-machine-for-linux"></a>Créer une machine virtuelle pour la science des données pour Linux
Voici hello étapes toocreate une instance de Machine virtuelle Linux données scientifiques de hello :

1. Accédez de machine virtuelle de toohello liste sur hello [portail Azure](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vm-ubuntulinuxdsvmubuntu).
2. Cliquez sur **créer** (au bas de hello) toobring Assistant de hello.![ configurer les données-science-machine virtuelle](./media/machine-learning-data-science-dsvm-ubuntu-intro/configure-data-science-virtual-machine.png)
3. Hello les sections suivantes fournit des entrées hello pour chacune des étapes hello dans l’Assistant hello (énuméré sur hello à droite de hello précédant figure) utilisé toocreate hello Machine virtuelle de science des données Microsoft. Voici hello entrées nécessitées tooconfigure chaque de ces étapes :
   
   a. **Paramètres de base**:
   
   * **Name**(Nom) : nom du serveur Data Science que vous créez.
   * **User Name**(Nom d’utilisateur) : premier ID de connexion du compte.
   * **Password**(Mot de passe) : premier mot de passe du compte (vous pouvez utiliser une clé publique SSH au lieu d’un mot de passe).
   * **Abonnement**: Si vous avez plusieurs abonnements, sélectionnez hello sur quel hello machine est toobe créées et facturées. Vous devez disposer des privilèges de création de ressources pour cet abonnement.
   * **Resource Group**(Groupe de ressources) : vous pouvez créer un nouveau groupe ou utiliser un groupe existant.
   * **Emplacement**: centre de données Sélectionnez hello qui convient le mieux. Il est généralement de centre de données hello qui comporte une grande partie de vos données ou qui est le plus proche emplacement physique tooyour pour l’accès réseau plus rapide.
   
   b. **Taille**:
   
   * Sélectionnez un des types de serveur hello qui répond à vos exigences fonctionnelles et les contraintes liées au coût. Sélectionnez **afficher tout** toosee plus de choix de tailles de machine virtuelle. Sélectionnez une machine virtuelle de classe NC pour la formation à la GPU.
   
   c. **Paramètres**:
   
   * **Type de disque** : choisissez **Premium** si vous préférez un disque SSD. Sinon, choisissez **Standard**. Les machines virtuelles GPU nécessitent un disque Standard.
   * **Compte de stockage**: vous pouvez créer un nouveau compte de stockage Azure dans votre abonnement, ou utiliser un déjà existant dans hello même emplacement a été choisie sur hello **notions de base** étape de l’Assistant de hello.
   * **Autres paramètres**: dans la plupart des cas, vous utilisez simplement les valeurs par défaut de hello. les valeurs par défaut tooconsider, placez votre curseur sur le lien d’information de hello pour aider à sur des champs spécifiques hello.
   
   d. **Résumé**:
   
   * Vérifiez que toutes les informations que vous avez saisies sont correctes.
   
   e. **Acheter**:
   
   * toostart hello approvisionnement, cliquez sur **acheter**. Un lien est fourni toohello les termes du contrat de transaction de hello. Hello machine virtuelle n’a pas de tous les frais supplémentaires au-delà de calcul hello pour la taille du serveur hello choisis Bonjour **taille** étape.

l’approvisionnement Hello doit prendre environ 5 à 10 minutes. état de Hello hello provisionnement est affiché sur hello portail Azure.

## <a name="how-tooaccess-hello-data-science-virtual-machine-for-linux"></a>Comment tooaccess hello Machine virtuelle de science des données pour Linux
Après hello que machine virtuelle est créée, vous pouvez vous connecter tooit à l’aide de SSH. Utiliser des informations d’identification de compte hello que vous avez créé dans hello **notions de base** section de l’étape 3 pour l’interface de shell texte hello. Sous Windows, vous pouvez télécharger un outil client SSH tel que [Putty](http://www.putty.org). Si vous préférez un graphique Bureau (X, Windows et système), vous pouvez utiliser X11 Putty de transfert ou installer hello X2Go client.

> [!NOTE]
> Hello X2Go client effectuée considérablement plus performants que X11 de transfert dans le test. Nous recommandons d’utiliser le client de X2Go hello pour une interface graphique de bureau.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>Installation et configuration du client X2Go
Hello Linux VM est déjà configuré avec X2Go server et les connexions client tooaccept prêt. tooconnect toohello bureau graphique de Linux VM, hello suivant sur votre client :

1. Téléchargez et installez le client hello X2Go pour votre plateforme de client à partir de [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Exécutez hello X2Go client, puis sélectionnez **nouvelle Session**. Une fenêtre de configuration avec plusieurs onglets s’ouvre. Entrez hello les paramètres de configuration suivants :
   * **Onglet Session**:
     * **Hôte**: nom d’hôte hello ou adresse IP de votre machine virtuelle scientifiques de données Linux.
     * **Connexion**: nom d’utilisateur sur hello Linux VM.
     * **Port SSH**: laissez 22, valeur par défaut de hello.
     * **Type de session**: modification hello valeur tooXFCE. Actuellement hello Linux VM prend uniquement en charge le bureau XFCE.
   * **Onglet support**: vous pouvez désactiver son support et de client d’impression si vous n’avez pas besoin de toouse les.
   * **Dossiers partagés**: Si vous souhaitez que les répertoires à partir de vos ordinateurs client montés sur hello Linux VM, ajouter des répertoires de l’ordinateur client hello que vous souhaitez tooshare avec hello machine virtuelle sous cet onglet.

Après que vous être connecté toohello machine virtuelle à l’aide de hello SSH client ou du bureau de graphique XFCE via le client de X2Go hello, vous êtes prêt toostart à l’aide des outils hello qui sont installés et configurés sur la machine virtuelle de hello. Sur XFCE, vous pouvez voir des icônes et raccourcis d’applications pour la plupart des outils de hello.

## <a name="tools-installed-on-hello-data-science-virtual-machine-for-linux"></a>Outils sont installés sur la Machine virtuelle de science des données de hello pour Linux
### <a name="deep-learning-libraries"></a>Bibliothèques d’apprentissage approfondi

#### <a name="cntk"></a>CNTK (Computational Network Toolkit de Microsoft Research)
Hello Toolki cognitifs de Microsoft - également appelé CNTK - est une open source complète le Kit de ressources d’apprentissage. Liaisons de Python sont disponibles dans les environnements de Conda racine et py35 hello. Il possède également un outil de ligne de commande (cntk) qui est déjà dans le chemin d’accès de hello.

Des exemples de bloc-notes Python sont disponibles dans JupyterHub. toorun un exemple de base à la ligne de commande hello, exécutez hello suivant les commandes dans le shell hello :

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

Pour plus d’informations, consultez hello section CNTK [GitHub](https://github.com/Microsoft/CNTK)et hello [CNTK wiki](https://github.com/Microsoft/CNTK/wiki).

#### <a name="caffe"></a>Caffe
Caffe est approfondie d’apprentissage framework à partir de hello Berkeley Vision et le centre d’apprentissage. Elle est disponible dans /opt/caffe. Vous en trouverez des exemples dans /opt/caffe/examples.

#### <a name="caffe2"></a>Caffe2
Caffe2 est un framework de formation approfondie de Facebook qui repose sur Caffe. Il est disponible dans les Python 2.7 dans l’environnement de hello Conda racine. tooactivate il, exécutez les hello qui suit à partir de l’interpréteur de commandes hello :

    source /anaconda/bin/activate root

Quelques exemples de bloc-notes sont disponibles dans JupyterHub.

#### <a name="h2o"></a>H2O
H2O est une plateforme d’analyse prédictive et d’apprentissage automatique rapide, en mémoire et distribuée. Un package Python est installé dans les deux environnements de Anaconda racine et py35 hello. Un package R est également installé. toostart H2O à partir de la ligne de commande hello exécuter `java -jar /dsvm/tools/h2o/current/h2o.jar`; il existe différentes [les options de ligne de commande](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/starting-h2o.html#from-the-command-line) que vous pouvez rendre tooconfigure. Hello de flux de l’interface utilisateur Web accessibles par navigation tooget toohttp://localhost:54321 a démarré. Des exemples de bloc-notes sont également disponibles dans JupyterHub.

#### <a name="keras"></a>Keras
Keras est une API de réseau neuronal principal dans Python qui est capable de s’exécuter sur Tensorflow ou Theano. Il est disponible dans les environnements de Python racine et py35 hello. 

#### <a name="mxnet"></a>MXNet
MXNet est une infrastructure d’apprentissage approfondi conçue pour offrir efficacité et flexibilité. Il possède des liaisons de R et Python inclus sur hello DSVM. Des exemples de bloc-notes sont inclus dans JupyterHub et un exemple de code est disponible dans /dsvm/samples/mxnet.

#### <a name="nvidia-digits"></a>NVIDIA DIGITS
Hello NVIDIA approfondie d’apprentissage GPU système de formation, appelé des chiffres, est un système toosimplify commun learning approfondie des tâches telles que la gestion des données, de conception et de réseaux neuronaux de formation sur les systèmes GPU et surveillance des performances en temps réel avec visualisation avancée. 

DIGITS est disponible en tant que service. Démarrer le service de hello et parcourir tooget toohttp://localhost:5000 a démarré.

CHIFFRES est également installé en tant que Python module dans un environnement de hello Conda racine.

#### <a name="tensorflow"></a>TensorFlow
TensorFlow est la bibliothèque d’apprentissage approfondi de Google. C’est une bibliothèque de logiciels open source destinée aux calculs numériques à l’aide de graphiques de flux de données. TensorFlow est disponible dans l’environnement de Python py35 hello, et certains ordinateurs portables d’exemple sont incluses dans JupyterHub.

#### <a name="theano"></a>Theano
Theano est une bibliothèque Python destinée à des calculs numériques efficaces. Il est disponible dans les environnements de Python racine et py35 hello. 

#### <a name="torch"></a>Torch
Torch est une infrastructure informatique scientifique avec prise en charge étendue des algorithmes d’apprentissage automatique. Il est disponible dans /dsvm/tools/torch, et la session interactive hello th et Gestionnaire de package luarocks sont disponibles à la ligne de commande hello. Des exemples sont disponibles dans /dsvm/samples/torch.

PyTorch est également disponible dans l’environnement de Anaconda hello racine. Des exemples sont disponibles dans /dsvm/samples/pytorch.

### <a name="microsoft-r-server"></a>Microsoft R Server
R est un des langages les plus populaires de hello pour l’analyse des données et l’apprentissage. Si vous souhaitez toouse R pour vos analytique, hello machine virtuelle a Microsoft R Server (MRS) avec hello Microsoft R Open Diffusée et Math Kernel Library (MKL). Hello MKL optimise les opérations mathématiques courantes dans les algorithmes analytiques. MRO est 100 % compatible avec CRAN-R, et une des bibliothèques hello R publiés dans CRAN peut être installée sur hello MRO. MRS assure la mise à l’échelle et l’opérationnalisation des modèles R dans les services web. Vous pouvez modifier vos programmes R dans un des éditeurs par défaut de hello, tels que RStudio, vi ou Emacs. Si vous utilisez l’éditeur de Emacs hello, notez ce package de Emacs hello ESS (Emacs parle statistiques), ce qui simplifie l’utilisation des fichiers de R dans l’éditeur de Emacs hello, a été préinstallé.

la console toolaunch R, vous tapez simplement **R** dans le shell hello. Cela vous prend un environnement interactif de tooan. toodevelop votre programme R, vous en règle générale, utilisez un éditeur comme Emacs ou vi, puis exécutez les scripts hello dans R. Avec RStudio, vous avez un graphique toodevelop d’environnement IDE votre programme de R.

Il existe également un script R pour hello de tooinstall vous [packages haut 20 R](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) si vous le souhaitez. Ce script peut être exécuté une fois que vous êtes dans l’interface interactive hello R, qui peut être entrée (comme indiqué) en tapant **R** dans le shell hello.  

### <a name="python"></a>Python
Pour un développement basé sur Python, les versions 2.7 et 3.5 de la distribution Anaconda Python ont été installées. Cette distribution contient hello Python avec environ 300 de hello packages plus populaires mathématiques, engineering et données analytique de base. Vous pouvez utiliser les éditeurs de texte hello par défaut. En outre, vous pouvez utiliser Spyder, un IDE Python fourni avec les distributions Anaconda Python. Spyder requiert un bureau graphique ou le transfert X11. Un raccourci tooSpyder est fourni dans le bureau de graphique hello.

Étant donné que nous avons Python 2.7 et 3.5, vous devez toospecifically activer hello souhaité Python version (environnement conda) que vous souhaitez toowork sur Bonjour session active. processus d’activation Hello définit la version souhaitée de la variable toohello de chemin d’accès d’hello de Python.

environnement de conda hello Python 2.7 tooactivate, exécutez les hello qui suit à partir de l’interpréteur de commandes hello :

    source /anaconda/bin/activate root

Python 2.7 est installé dans */anaconda/bin*.

environnement de conda hello Python 3.5 tooactivate, exécutez les hello qui suit à partir de l’interpréteur de commandes hello :

    source /anaconda/bin/activate py35


Python 3.5 est installé dans */anaconda/envs/py35/bin*.

tooinvoke une session interactive de Python, tapez simplement **python** dans le shell hello. Si vous y sur une interface graphique ou que vous avez X11 ensemble de transfert des, vous pouvez taper **pycharm** toolaunch hello PyCharm d’environnement IDE Python.

tooinstall des bibliothèques Python supplémentaires, vous devez toorun ```conda``` ou ````pip```` commande sous sudo et fournissent de chemin d’accès complet du Gestionnaire de package Python hello (conda ou pip) tooinstall toohello Python environnement approprié. Par exemple :

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Jupyter Notebook
Hello distribution Anaconda est également fourni avec un bloc-notes jupyter, un environnement de code tooshare et l’analyse. Bloc-notes jupyter de Hello est accessible via JupyterHub. Vous vous connectez en utilisant votre nom d’utilisateur Linux local et votre mot de passe.

serveur de jupyter Notebook Hello a été préconfigurée avec Python 2, 3 de Python et des noyaux de R. Il existe une icône de bureau nommée « Bloc-notes Jupyter » toolaunch hello navigateur tooaccess hello bloc-notes server. Si vous êtes sur hello machine virtuelle via le client SSH ou X2Go, vous pouvez également consulter [https://localhost:8000 /](https://localhost:8000/) tooaccess hello serveur jupyter Notebook.

> [!NOTE]
> Si vous recevez des avertissements relatifs au certificat, vous pouvez les ignorer.
> 
> 

Serveur de jupyter Notebook hello est accessible à partir de n’importe quel hôte. Tapez simplement *https://\<nom DNS ou adresse IP de la machine virtuelle\>:8000/*

> [!NOTE]
> Port 8000 est ouvert dans le pare-feu hello par défaut lors de la configuration de machine virtuelle de hello.
> 
> 

Nous avons empaqueté blocs-notes exemple--Python dans un et l’autre dans R. Vous pouvez voir des exemples de toohello hello lien sur la page d’accueil hello bloc-notes après que vous être authentifié toohello bloc-notes jupyter en utilisant votre nom d’utilisateur Linux local et le mot de passe. Vous pouvez créer un nouvel ordinateur portable en sélectionnant **nouveau**et ensuite le noyau hello langue appropriée. Si vous ne voyez pas hello **nouveau** et sur hello **Notebook** icône sur toogo gauche supérieur hello toohello une page d’accueil du serveur de bloc-notes hello.

### <a name="apache-spark-standalone"></a>Apache Spark autonome 
Une instance autonome d’Apache Spark est préinstallée sur hello toohelp Linux DSVM vous développerez des applications de Spark localement tout d’abord avant de tester et déployer des clusters de grande taille. Vous pouvez exécuter des programmes de PySpark par le biais du noyau de Notebook hello. Lorsque vous ouvrez le bloc-notes et que vous cliquez sur le bouton « Nouveau » de hello, vous verrez une liste de noyaux disponibles. Hello « Python de – Spark » est le noyau PySpark hello permettant de créer des applications à l’aide du langage Python Spark. Vous pouvez également utiliser un IDE Python comme PyCharm ou Spyder toobuild vous au service de programme. Depuis, il s’agit d’une instance autonome, pile de Spark hello s’exécute au sein de hello appelant le programme client. Il est ainsi plus rapide et plus facile tootroubleshoot problèmes comparée toodeveloping sur un cluster Spark. 

Un bloc-notes de PySpark exemple est fourni sur Notebook vous trouverez dans le répertoire de « SparkML » hello sous le répertoire de base hello de Notebook ($HOME/portables/SparkML/pySpark). 

Si vous programmez en R pour Spark, vous pouvez utiliser Microsoft R Server, SparkR ou sparklyr. 

Avant d’exécuter dans le contexte de Spark dans Microsoft R Server, vous devez toodo une seule instance de fils et une fois le programme d’installation étape tooenable un seul nœud Hadoop HDFS local. Par défaut, les services Hadoop sont installés mais désactivés sur hello DSVM. Commande tooenable, vous devez hello toorun suivant les commandes en tant que hello de racine première fois :

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

Vous pouvez arrêter hello Hadoop lorsque vous n’en avez besoin en exécutant des services liés ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` un exemple illustrant comment MRS toodevelop et de test dans le contexte Spark distant (qui est l’instance de Spark hello autonome sur hello DSVM) est fourni et disponibles dans hello `/dsvm/samples/MRS` active. 

### <a name="ides-and-editors"></a>IDE et éditeurs
Vous avez le choix entre plusieurs éditeurs de code, notamment vi/VIM, Emacs, PyCharm, RStudio et IntelliJ. IntelliJ, RStudio PyCharm sont les éditeurs graphiques et vous devez toobe connecté toouse de bureau graphique tooa les. Ces éditeurs proposent des applications et bureau toolaunch de raccourcis de menu les.

**VIM** et **Emacs** sont des éditeurs de texte. Sur Emacs, nous avons installé un package de module complémentaire appelé Emacs parle statistiques (ESS) qui facilite l’utilisation de R dans l’éditeur de Emacs hello. Des informations supplémentaires sont disponibles ici : [ESS](http://ess.r-project.org/).

**LaTex** est installé via un package de texlive hello ainsi que d’un module complémentaire Emacs [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) package, ce qui simplifie la création de vos documents LaTex Emacs.  

### <a name="databases"></a>Bases de données

#### <a name="graphical-sql-client"></a>Client SQL graphique
**HIPPOCAMPIQUES SQL**, un client SQL graphique, a été fourni tooconnect toodifferent bases de données (par exemple, Microsoft SQL Server et MySQL) et les requêtes SQL toorun. Vous pouvez l’exécuter à partir d’une session de bureau graphique (à l’aide de client de X2Go hello, par exemple). tooinvoke non SQL, vous pouvez lancer à partir de l’icône hello sur le bureau de hello ou exécutez hello commande suivante sur l’interpréteur de commandes hello.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Avant de hello la première utilisation, configurer les pilotes et les alias de la base de données. les pilotes JDBC Hello sont trouvent dans :

*/usr/share/Java/jdbcdrivers*

Pour plus d’informations, consultez [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots).

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Outils en ligne de commande pour l’accès à Microsoft SQL Server
package de pilotes ODBC Hello pour SQL Server est également fourni avec deux outils de ligne de commande :

**bcp**: hello bcp utilitaire copie en bloc des données entre une instance de Microsoft SQL Server et un fichier de données dans un format spécifié par l’utilisateur. utilitaire bcp de Hello peut être tooimport utilisé un grand nombre de nouvelles lignes dans les tables SQL Server, ou des données tooexport de tables dans des fichiers de données. tooimport des données dans une table, vous devez utiliser un fichier de format créé pour cette table, ou comprendre la structure de hello de table de hello et de types hello de données qui sont valides pour ses colonnes.

Pour plus d’informations, consultez [Connexion avec bcp](https://msdn.microsoft.com/library/hh568446.aspx).

**SQLCMD**: vous pouvez entrer des instructions Transact-SQL avec l’utilitaire sqlcmd de hello, ainsi que des procédures système et les fichiers à l’invite de commandes hello de script. Cet utilitaire utilise ODBC tooexecute Transact-SQL lots.

Pour plus d’informations, consultez [Connexion avec sqlcmd](https://msdn.microsoft.com/library/hh568447.aspx).

> [!NOTE]
> L’utilitaire diffère légèrement entre les plateformes Linux et Windows. Consultez la documentation de hello pour plus d’informations.
> 
> 

#### <a name="database-access-libraries"></a>Bibliothèques pour l’accès aux bases de données
Bibliothèques sont disponibles dans les bases de données tooaccess R et Python.

* Dans R, hello **RODBC** package ou **dplyr** package vous permet de tooquery ou exécuter des instructions SQL sur le serveur de base de données hello.
* Dans Python, hello **pyodbc** bibliothèque fournit l’accès de base de données avec ODBC comme hello couche sous-jacente.  

### <a name="azure-tools"></a>Outils Azure
Hello suivant de Windows Azure tools est installé sur hello machine virtuelle :

* **Interface de ligne de commande Azure**: hello CLI d’Azure vous permet de toocreate et gérer des ressources Azure grâce aux commandes de l’interpréteur de commandes. tooinvoke hello Windows Azure tools, tapez simplement **aide azure**. Pour plus d’informations, consultez hello [page de documentation Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* **Microsoft Azure Storage Explorer**: Microsoft Azure Storage Explorer est un outil graphique qui est toobrowse utilisé par le biais des objets hello que vous avez stocké dans votre compte de stockage Azure et le téléchargement et tooupload tooand de données d’objets BLOB Azure. Vous pouvez accéder à l’Explorateur de stockage à partir de l’icône de raccourci du bureau hello. Vous pouvez l’appeler à partir d’une invite de commandes en tapant **StorageExplorer**. Toobe connecté à partir d’un client X2Go, ou que vous avez X11 ensemble de transfert des.
* **Les bibliothèques Azure**: hello Voici quelques-uns des bibliothèques de préinstallées hello.
  
  * **Python**: les bibliothèques liées à Azure hello dans Python installés sont **azure**, **azureml**, **pydocumentdb**, et **pyodbc** . Avec Bonjour tout d’abord trois bibliothèques, vous pouvez accéder aux services de stockage Azure, Azure Machine Learning et base de données Azure Cosmos (une base de données NoSQL sur Azure). bibliothèque quatrième Hello, pyodbc (ainsi que hello pilote Microsoft ODBC pour SQL Server), permet tooSQL accès serveur, base de données SQL Azure et Azure SQL Data Warehouse à partir de Python à l’aide de l’interface ODBC. Entrez **liste de pip** toosee tous hello répertoriés bibliothèques. Être toorun que cette commande dans les deux hello Python 2.7 et 3.5 environnements.
  * **R**: hello liées à Azure bibliothèques dans R installés sont **AzureML** et **RODBC**.
  * **Java**: vous trouverez la liste de hello des bibliothèques de Azure Java dans le répertoire de hello **/dsvm/sdk/AzureSDKJava** sur hello machine virtuelle. bibliothèques de clé Hello sont Azure stockage et gestion des API Azure Cosmos DB, pilotes et JDBC pour SQL Server.  

Vous pouvez accéder à hello [portail Azure](https://portal.azure.com) à partir du navigateur Firefox préinstallée de hello. Sur hello portail Azure, vous pouvez créer, gérer et surveiller les ressources Azure.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning est un service cloud entièrement géré qui vous permet de toobuild, déployer et partager des solutions d’analytique prédictive. Créez vos expériences et modèles dans Azure Machine Learning Studio. Il est accessible à partir d’un navigateur web sur l’ordinateur virtuel de hello données science en vous rendant sur [Microsoft Azure Machine Learning](https://studio.azureml.net).

Après que vous être connecté tooAzure Machine Learning Studio, vous avez accès tooan expérimentation canevas où vous pouvez générer un flux logique pour les algorithmes d’apprentissage hello. Également, vous avez accès tooa bloc-notes jupyter hébergé sur Azure Machine Learning et fonctionne de façon transparente avec les expériences hello dans Machine Learning Studio. Opérationnaliser les modèles que vous avez créés en les encapsulant dans une interface de service web d’apprentissage hello. Ainsi, les clients écrits dans des prédictions de tooinvoke de langue à partir de modèles d’apprentissage hello. Pour plus d’informations, consultez hello [documentation d’apprentissage](https://azure.microsoft.com/documentation/services/machine-learning/).

Vous pouvez également créer vos modèles dans R ou Python sur hello machine virtuelle et déployer en production sur Azure Machine Learning. Nous avons installé bibliothèques dans R (**AzureML**) et Python (**azureml**) tooenable cette fonctionnalité.

Pour plus d’informations sur la façon dont toodeploy modèles R et Python dans Azure Machine Learning, consultez [dix choses à faire sur hello pour la science des données Machine virtuelle](machine-learning-data-science-vm-do-ten-things.md) (en particulier, hello section « générer des modèles à l’aide de R ou Python et effectuent les à l’aide de Azure Machine Learning »).

> [!NOTE]
> Ces instructions ont été écrites pour la version de Windows hello Hello VM de science des données. Mais les informations hello fournies sur le déploiement de modèles tooAzure Machine Learning sont applicable toohello Linux VM.
> 
> 

### <a name="machine-learning-tools"></a>Outils de Machine Learning
Hello machine virtuelle s’accompagne d’apprentissage quelques outils et les algorithmes qui ont été précompilés et préinstallés localement. Vous avez notamment vu les points suivants :

* **Vowpal Wabbit**: algorithme d’apprentissage en ligne rapide.
* **xgboost**: outil qui fournit des algorithmes d’arborescence optimisés.
* **Rattle** : outil graphique R destiné à faciliter l’exploration et la modélisation des données.
* **Python**: Anaconda Python est fourni avec des algorithmes de Machine Learning et des bibliothèques comme Scikit-learn. Vous pouvez installer les autres bibliothèques à l’aide de hello `pip install` commande.
* **LightGBM** : infrastructure d’amélioration progressive rapide, distribuée et hautes performances basée sur les algorithmes d’arbre de décision.
* **R**: une riche bibliothèque de fonctions d’apprentissage machine est disponible pour R. Certaines des bibliothèques hello préinstallés sont lm, glm, randomForest, rpart. D’autres bibliothèques peuvent être installées en exécutant la commande suivante :
  
        install.packages(<lib name>)

Voici quelques informations supplémentaires sur hello tout d’abord trois outils d’apprentissage machine dans la liste de hello.

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit est un système de Machine Learning utilisant des techniques (apprentissage en ligne, hachage, allreduce, réductions, learning2search, actif et interactif).

outil de hello toorun sur un exemple très simple, hello suivant :

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

Ce répertoire inclut d’autres démonstrations plus conséquentes. Pour plus d’informations sur les unités VW, consultez [cette section de GitHub](https://github.com/JohnLangford/vowpal_wabbit)et hello [wiki de Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki).

#### <a name="xgboost"></a>XGBoost
Cette bibliothèque a été conçue et optimisée pour les algorithmes d’arborescence optimisés. objectif de Hello de cette bibliothèque est nécessaire de limites de calcul hello toopush d’extrêmes toohello de machines tooprovide boosting d’arbre à grande échelle qui est évolutif, portable et précises.

Elle est fournie sous forme de ligne de commande et de bibliothèque R.

toouse cette bibliothèque dans R, vous pouvez démarrer une session interactive de R (en tapant **R** dans le shell hello) et le chargement de la bibliothèque hello.

Voici un exemple simple que vous pouvez exécuter dans l’invite R :

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

ligne de commande xgboost toorun hello, voici hello commandes tooexecute dans le shell hello :

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


Un fichier .model est écrite répertoire toohello spécifié. Des informations sur cet exemple de démonstration sont disponibles [sur GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification).

Pour plus d’informations sur xgboost, consultez hello [page de documentation xgboost](https://xgboost.readthedocs.org/en/latest/)et son [référentiel GitHub](https://github.com/dmlc/xgboost).

#### <a name="rattle"></a>Rattle
Vibrer (hello **R** **A**nalytical **T**outil **T**o **L**gagner **E** asily) utilise la modélisation et l’exploration de données basées sur l’interface utilisateur graphique. Il présente des statistiques visual résumés de données, transformations de données qui peuvent être facilement modélisées, crée des modèles non supervisés et contrôlés à partir des données de hello, présente hello graphiquement les performances des modèles et définit de nouvelles données de scores. Il génère également du code R, réplication des opérations hello Bonjour l’interface utilisateur qui peuvent être exécutées directement dans R ou utilisées comme point de départ pour une analyse plus approfondie.

toorun Hochet, vous devez toobe dans une graphique bureau de session. Terminal de hello, tapez ```R``` environnement de hello R tooenter. À l’invite de hello R, entrez hello suivant de commandes :

    library(rattle)
    rattle()

À présent, une interface graphique s’ouvre avec un jeu d’onglets. Voici hello démarrage rapide des étapes dans Hochet nécessaire toouse un jeu de données exemple météo et générer un modèle. Dans certaines des étapes hello ci-dessous, vous tooautomatically invité à installer et chargez des packages R requis qui ne sont pas déjà sur le système de hello.

> [!NOTE]
> Si vous n’avez pas package de hello tooinstall accès dans le répertoire du système de hello (valeur par défaut de hello), vous pouvez voir une invite de commandes sur votre console fenêtre tooinstall packages tooyour personnel bibliothèque R. Répondez *o* si vous voyez ces invites.
> 
> 

1. Cliquez sur **Exécuter**.
2. Une boîte de dialogue s’affiche, vous demandant si vous le souhaitez toouse hello exemple jeu de données météo. Cliquez sur **Oui** exemple hello de tooload.
3. Cliquez sur hello **modèle** onglet.
4. Cliquez sur **Execute** toobuild un arbre de décision.
5. Cliquez sur **dessiner** arbre de décision toodisplay hello.
6. Cliquez sur hello **forêt** case d’option, puis cliquez sur **Execute** toobuild une forêt aléatoire.
7. Cliquez sur hello **évaluer** onglet.
8. Cliquez sur hello **risque** case d’option, puis cliquez sur **Execute** graphiques de performances toodisplay deux risques (cumulé).
9. Cliquez sur hello **journal** hello de tooshow onglet générer du code de R pour hello les opérations précédentes.
   (En raison du bogue tooa dans la version actuelle de hello de Hochet, vous devez tooinsert une  *#*  caractère devant *exporter ce journal...*  dans le texte hello du journal de hello.)
10. Cliquez sur hello **exporter** fichier de script hello R toosave bouton nommé *weather_script. R* toohello dossier de base.

Vous pouvez quitter Hochet et R. Vous pouvez maintenant modifier hello généré un script R, ou l’utiliser comme c’est le toorun il toorepeat à tout moment tout ce qui a été fait dans hello vibrer de l’interface utilisateur. En particulier pour les débutants dans R, il s’agit d’un moyen simple tooquickly effectuer des analyses et apprentissage dans une interface graphique simple, lors de la génération automatique de code dans R toomodify et/ou en savoir plus.

## <a name="next-steps"></a>Étapes suivantes
Voici comment poursuivre votre formation et votre exploration :

* Hello [science des données sur hello Machine virtuelle Linux données Science](machine-learning-data-science-linux-dsvm-walkthrough.md) procédure pas à pas vous montre comment tooperform scientifiques de données commun plusieurs tâches avec hello VM de science des données Linux configuré ici. 
* Explorer hello divers outils de science des données sur hello pour la science des données machine virtuelle en essayant de hello outils décrits dans cet article. Vous pouvez également exécuter *dsvm-plus-info* sur shell hello au sein de la machine virtuelle hello une introduction et des pointeurs toomore informations de base outils hello sur hello machine virtuelle.  
* Découvrez comment les solutions analytiques de bout en bout toobuild systématiquement à l’aide de hello [processus de science des données équipe](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).
* Visitez hello [Cortana Analytique galerie](http://gallery.cortanaanalytics.com) pour ce hello utilisez Cortana Analytique Suite d’exemples analytique d’apprentissage et de données machine.

