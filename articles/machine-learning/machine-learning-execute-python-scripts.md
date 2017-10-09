---
title: scripts apprentissage Python automatique aaaExecute | Documents Microsoft
description: "Décrit les principes de conception sous-jacents de la prise en charge des scripts Python dans Azure Machine Learning, les scénarios d’utilisation, les fonctionnalités et les restrictions de base."
keywords: "apprentissage automatique Python, pandas, pandas de python, scripts python, exécuter des scripts python"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Exécution des scripts d’apprentissage automatique Python dans Azure Machine Learning Studio

Cette rubrique décrit les principes de conception hello sous-jacent hello prise en charge actuelle scripts Python dans Azure Machine Learning. principales fonctionnalités Hello sont également présentées, y compris :

- Exécution de scénarios d’usage de base
- Notation d’une expérience dans un service web
- Prise en charge de l’importation de code existant
- Exportation de visualisations
- Sélection de fonctionnalités supervisée
- Prise en compte de certaines limitations

[Python](https://www.python.org/) est un outil indispensable dans les coffres d’outil hello de nombreux chercheurs de données. Il comprend :

* une syntaxe concise et élégante, 
* une prise en charge interplateforme, 
* un vaste ensemble de bibliothèques puissantes, et 
* des outils de développement avancés. 

Python est employé dans toutes les phases d’un flux de travail généralement utilisé dans la modélisation de l’apprentissage automatique :

- Ingestion et traitement des données 
- Construction des fonctionnalités
- Formation aux modèles 
- Validation des modèles
- déploiement des modèles de hello

Azure Machine Learning Studio prend en charge l’intégration des scripts Python dans plusieurs parties d’une expérience d’apprentissage automatique ainsi que leur publication transparente en tant que services web sur Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>Principes de conception des scripts Python dans Machine Learning

tooPython d’interface principale Hello dans Azure Machine Learning Studio est via hello [Execute Python Script] [ execute-python-script] module illustré dans la Figure 1.

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

Figure 1. Hello **Execute Python Script** module.

Hello [Execute Python Script] [ execute-python-script] module dans Azure ML Studio accepte des entrées de toothree et produit des sorties tootwo (décrits hello après section), comme son analogique R, hello [ Exécutez le Script R] [ execute-r-script] module. toobe de code Python exécutée Hello est entré dans la zone du paramètre hello comme spéciale nommée fonction appelée point d’entrée `azureml_main`. Voici la conception de clés hello principes utilisé tooimplement ce module :

1. *Doit être idiomatique pour les utilisateurs de Python.* La plupart des utilisateurs de Python factorisent leur code en tant que fonctions au sein des modules. De ce fait, l’insertion de nombreuses instructions exécutables dans un module de niveau supérieur est relativement rare. Par conséquent, zone de script hello prend également une fonction de Python spéciale nommée comme toojust opposé une séquence d’instructions. Hello objets exposés dans la fonction hello sont des types de bibliothèque Python standard comme [Pandas](http://pandas.pydata.org/) des trames de données et [NumPy](http://www.numpy.org/) tableaux.
2. *Doit disposer d'une haute fidélité entre les exécutions locales et les exécutions du cloud.* principal utilisé tooexecute hello code Python Hello est basée sur [Anaconda](https://store.continuum.io/cshop/anaconda/), largement utilisé distribution de Python scientifique inter-plateformes. Il est fourni avec too200 fermer des packages Python courants de hello. Par conséquent, les scientifiques de données peuvent déboguer et qualifier leur code dans leur environnement Anaconda local compatible avec Azure Machine Learning. Puis utiliser un environnement de développement existant, tel que [IPython](http://ipython.org/) bloc-notes ou [outils Python pour Visual Studio](http://aka.ms/ptvs), toorun dans le cadre d’une expérience Azure ML. Hello `azureml_main` point d’entrée est une fonction de Python vanille et donc *** peuvent être créés sans code spécifique à Azure ML ou hello SDK installé.
3. *Doit être composé, de manière transparente, d’autres modules Azure Machine Learning.* Hello [Execute Python Script] [ execute-python-script] module accepte comme entrées et sorties, des jeux de données Azure Machine Learning standard. infrastructure sous-jacente de Hello efficacement et de façon transparente établit un pont entre les runtimes Azure ML et Python hello. Python peut donc être utilisé en combinaison avec des flux de travail Azure ML existants, y compris ceux qui font appel à R et SQLite. Un scientifique des données peut ainsi composer des flux de travail qui :
   * utilisent Python et Pandas pour le prétraitement et le nettoyage de données
   * flux hello données tooa SQL transformation, jointure de plusieurs fonctionnalités tooform de jeux de données
   * l’apprentissage des modèles à l’aide d’algorithmes de hello dans Azure Machine Learning 
   * Évaluez et post-traiter les résultats hello à l’aide de R.


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>Scénarios d’usage de base des scripts Python dans ML

Dans cette section, nous enquête quelques-unes des utilisations de base hello Hello [Execute Python Script] [ execute-python-script] module. Module de Python toohello entrées sont exposées comme des trames de données Pandas. Hello fonction doit retourner une seule image de données Pandas empaquetée à l’intérieur d’une Python [séquence](https://docs.python.org/2/c-api/sequence.html) comme un tuple, une liste ou un tableau de NumPy. Hello premier élément de cette séquence est ensuite renvoyé dans hello premier port de sortie du module de hello. Ce schéma est illustré dans la Figure 2.

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

Figure 2 : Mappage de port de toooutput valeur tooparameters et retournent des ports d’entrée.

Plus d’une sémantique de façon dont les ports d’entrée hello get tooparameters mappé de hello `azureml_main` fonction sont affichés dans le tableau 1 :

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

Tableau 1. Mappage de paramètres toofunction de ports d’entrée.

mappage de Hello entre les ports d’entrée et les paramètres de fonction est positionnel :

- port d’entrée connecté première Hello est mappé toohello premier paramètre de fonction hello. 
- Hello deuxième entrée (si vous êtes connecté) est mappé toohello deuxième paramètre de fonction hello.

Consultez *Python pour l’analyse de données* (o ' Reilly, 2012) par McKinney ouest pour plus d’informations sur Python Pandas et comment il peut être utilisé toomanipulate données efficacement. 


## <a name="translation-of-input-and-output-types"></a>Conversion des types d'entrée et de sortie 
Jeux de données d’entrée dans Azure ML est les frames toodata converti dans Pandas. Les trames de données de sortie sont converties en arrière tooAzure ML de jeux de données. Hello suivant conversions est effectuée :

1. Les colonnes numériques et de chaîne sont converties en tant que-est et les valeurs manquantes dans un jeu de données sont converties too'NA' valeurs Pandas. Hello même conversion s’effectue sur hello remonte (NA valeurs dans Pandas soient toomissing converti dans Azure ML).
2. Les vecteurs d’index dans Pandas ne sont pas pris en charge dans Azure ML. Toutes les trames de données d’entrée dans la fonction de Python hello toujours ont un index numérique de 64 bits à partir de 0 toohello nombre de lignes moins 1. 
3. Les jeux de données Azure ML ne peuvent pas comporter de noms de colonnes dupliqués et de noms de colonnes autres que des chaînes. Si une trame de données de sortie contient les colonnes non numériques, hello le framework appelle `str` sur les noms de colonne hello. De même, tous les noms de colonne en double sont automatiquement tronqué tooinsure hello noms sont uniques. suffixe de Hello (2) est ajouté le premier toohello doublon, (3) toohello deuxième doublon et ainsi de suite.


## <a name="operationalizing-python-scripts"></a>Mise en place des scripts Python

Les modules [Exécuter le script Python][execute-python-script] utilisés dans une expérience de notation sont appelés lorsqu’ils sont publiés en tant que service web. Par exemple, la Figure 3 illustre une expérience de score contenant tooevaluate de code hello une seule expression Python. 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

Figure 3. Service web pour l'évaluation d'une expression Python.

Un service web créé à partir de cette expérience :

- utilise comme entrée une expression Python (sous forme de chaîne)
- Il envoie l’interpréteur Python sous % toohello 
- Retourne une table qui contient l’expression de hello et résultats de hello évaluée.


## <a name="importing-existing-python-script-modules"></a>Importation des modules de script Python existants

Un cas d’usage courant pour nombreux chercheurs de données est tooincorporate des scripts Python existants dans des expériences d’Azure ML. Au lieu de demander que tout le code concaténé et collé dans une zone de script unique, hello [Execute Python Script] [ execute-python-script] module accepte un fichier zip qui contient des modules Python au port d’entrée de hello tiers. fichier de Hello est décompressé par l’infrastructure d’exécution hello lors de l’exécution et contenu de hello est ajoutées toohello chemin d’accès de bibliothèque de l’interpréteur Python sous hello. Hello `azureml_main` point d’entrée (fonction) pouvez ensuite importer ces modules directement.

Par exemple, considérez le fichier hello Hello.py contenant une fonction « Hello, World » simple.

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

Figure 4. Fonction définie par l’utilisateur dans le fichier Hello.py.

Ensuite, nous créons un fichier Hello.zip contenant Hello.py :

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

Figure 5. Fichier zip contenant le code Python défini par l'utilisateur.

Téléchargez le fichier zip de hello comme un jeu de données dans Azure Machine Learning Studio. Puis créez et exécutez une expérience qui utilise du code Python hello dans le fichier de Hello.zip hello en le joignant toohello troisième port d’entrée de hello **Execute Python Script** module, comme indiqué dans cette illustration.

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

Figure 6. Exemple d'expérience dotée d'un code Python défini par l'utilisateur et chargé en tant que fichier zip.

sortie de module Hello montre le fichier zip hello a été décompressée et cette fonction hello `print_hello` a été exécutée.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

Figure 7. Fonction définie par l’utilisateur en cours d’utilisation à l’intérieur de hello [Execute Python Script] [ execute-python-script] module.


## <a name="working-with-visualizations"></a>Utilisation des visualisations

Les graphiques créés à l’aide de MatplotLib qui peut être visualisé dans le navigateur de hello peuvent être retournées par hello [Execute Python Script][execute-python-script]. Mais hello graphiques ne sont pas automatiquement redirigés tooimages que lors de l’utilisation de R. Afin de hello utilisateur doit explicitement enregistrer les tracés tooPNG fichiers s’ils sont toobe retourné précédent tooAzure Machine Learning. 

toogenerate des images à partir de MatplotLib, vous devez effectuer hello procédure :

* commutateur hello principal trop « Agrégation » à partir de hello par défaut en fonction de Qt le convertisseur 
* créer un nouvel objet figure 
* obtenir l’axe de hello et générer tous les tracés dans celui-ci 
* Enregistrez le fichier PNG de hello figure tooa 

Ce processus est illustré dans hello suivant Figure 8 qui crée une matrice de traçage à nuages de points à l’aide de la fonction de scatter_matrix hello dans Pandas.

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

Figure 8. Toosave que matplotlib tooimages les chiffres du code.

La figure 9 illustre une expérience qui utilise un script hello illustré précédemment tooreturn trace via le port de sortie deuxième hello.

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

Figure 9. Visualisation des graphiques générés à partir d'un code Python.

Est possible tooreturn plusieurs illustrations en les enregistrant dans des images, hello Azure Machine Learning runtime récupère toutes les images et les concatène pour la visualisation.


## <a name="advanced-examples"></a>Exemples avancés

environnement de Anaconda Hello installé dans Azure Machine Learning contient les packages courants tels que NumPy, SciPy et Scikits-Learn. Ces packages peuvent être utilisés efficacement pour diverses tâches de traitement des données dans un pipeline d’apprentissage automatique. Par exemple, hello script et expérience suivant illustrent hello utilisation d’apprenants ensemble dans Scikits-Learn des scores d’importance de fonctionnalité toocompute pour un jeu de données. les scores Hello peuvent être la sélection des fonctionnalités utilisées tooperform supervisé avant d’être introduit dans un autre modèle ML.

Voici les scores d’importance hello Python fonction utilisée toocompute hello et les fonctionnalités de hello ordre selon les scores hello :

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

Figure 10. Fonctionnalités de toorank fonction par scores.
 Hello expérience suivante puis calcule et retourne les scores d’importance hello des fonctionnalités hello « Pima indien du diabète » jeu de données dans Azure Machine Learning :

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

Figure 11. Fonctionnalités de toorank expérience hello Pima indien DIABÈTE jeu de données.

## <a name="limitations"></a>Limites
Hello [Execute Python Script] [ execute-python-script] a actuellement hello limites suivantes :

1. *Exécution dans un bac à sable (sandbox).* Hello Python runtime est actuellement de bac à sable et, par conséquent, n’autorise pas toohello accès réseau ou toohello système de fichiers local de manière persistante. Tous les fichiers enregistrés localement sont isolés et supprimés une fois le module de hello se termine. Hello code Python ne peut pas accéder à la plupart des répertoires sur l’ordinateur hello qu'il s’exécute, en cours d’exception hello hello répertoire en cours et ses sous-répertoires.
2. *Manque de support de développement et de débogage sophistiqué.* actuellement, module de Python Hello ne prend pas en charge les fonctionnalités IDE comme intellisense et le débogage. En outre, si le module de hello échoue lors de l’exécution, hello trace de pile Python complète est disponible. Mais elle doit être affichée dans le journal de sortie hello pour le module de hello. Actuellement, nous vous recommandons développer et déboguer des scripts Python dans un environnement tel que IPython et réimporter les code hello dans le module de hello.
3. *Sortie de trame de données unique.* point d’entrée Python Hello est uniquement autorisée tooreturn une trame de données unique en tant que sortie. Il n’est pas possible actuellement tooreturn que Python arbitraire des objets tels que les modèles formés sauvegarder directement toohello Azure Machine Learning runtime. Comme [Execute R Script][execute-r-script], qui a hello même restriction, il est possible dans de nombreux cas, les objets de toopickle dans un octet de tableau et qui retournent ensuite à l’intérieur d’une trame de données.
4. *Incapacité toocustomize installation de Python*. Actuellement, hello uniquement moyen tooadd Python modules personnalisés est via le mécanisme de fichier zip hello décrit précédemment. Bien que ceci soit faisable pour les petits modules, la procédure est assez lourde pour les gros modules (notamment ceux constitués de DLL natives) ou un grand nombre de modules. 

## <a name="conclusions"></a>Conclusions
Hello [Execute Python Script] [ execute-python-script] module permet de code Python existant de tooincorporate un spécialiste des données dans le flux de travail hébergés dans le cloud de machine learning dans Azure Machine Learning et tooseamlessly tiens en tant que partie d’un service web. module de script Python Hello interagit naturellement avec d’autres modules dans Azure Machine Learning. module de Hello peut être utilisé pour une plage de tâches à partir d’exploration de données toopre-traitement et d’extraction de fonctionnalité et tooevaluation et traitement des résultats de hello. Hello principal runtime est utilisé pour l’exécution est basée sur Anaconda, une distribution de Python bien testée et largement utilisée. Cette principal facilite pour vous, les ressources de code existant de la carte tooon dans le cloud de hello.

Nous pensons que tooprovide des fonctionnalités supplémentaires toohello [Execute Python Script] [ execute-python-script] module comme hello capacité tootrain et opérationnaliser les modèles de Python et tooadd meilleure prise en charge pour hello développement et débogage de code dans Azure Machine Learning Studio.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement Python](https://azure.microsoft.com/develop/python/).

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
