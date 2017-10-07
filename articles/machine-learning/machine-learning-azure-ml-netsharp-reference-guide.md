---
title: "aaaGuide toohello réseau neuronal réseaux langage de spécification | Documents Microsoft"
description: "Syntaxe de hello Net # neural networks langage de spécification, ainsi que des exemples de comment toocreate un réseau neuronal personnalisé modèle dans Microsoft Azure ML à l’aide de Net #"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Guide du langage de spécification de réseau neuronal tooNet # pour Azure Machine Learning
## <a name="overview"></a>Vue d'ensemble
NET # est un langage développé par Microsoft, qui est utilisé toodefine d’architectures réseau neuronal. Vous pouvez utiliser Net# dans des modules de réseau neuronal dans Microsoft Azure Machine Learning.

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

Dans cet article, vous allez apprendre les concepts de base nécessaires toodevelop un réseau neuronal personnalisé : 

* Configuration requise du réseau neuronal et comment toodefine hello composants principaux
* syntaxe de Hello et les mots clés de langage de spécification de Net # de hello
* Exemples de réseaux neuronaux personnalisés créés avec Net# 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>Principes fondamentaux des réseaux neuronaux
Consistant en une structure de réseau neuronal ***nœuds*** qui sont organisés en ***couches***et pondérées ***connexions*** (ou ***bords***) entre nœuds Hello. connexions de Hello sont directionnelles, et chaque connexion possède un ***source*** nœud et un ***destination*** nœud.  

Chaque ***couche apte à l’apprentissage*** (couche masquée ou de sortie) présente un ou plusieurs ***faisceaux de connexions***. Un regroupement de connexion se compose d’une couche source et une spécification de connexions hello de cette couche source. Toutes les connexions hello dans un partage de lot donné hello même ***couche source*** et même hello ***calque de destination***. Dans Net #, un regroupement de connexion est considéré comme couche de destination du regroupement appartenant toohello.  

NET # prend en charge différents types de paquets de connexion, ce qui vous permet de personnaliser la façon hello entrées sont mappés toohidden couches et fournit en sortie toohello mappé.   

par défaut de Hello ou de groupe standard est un **offre complète**, dans chaque nœud qui Bonjour couche source est le nœud connecté tooevery hello calque de destination.  

En outre, Net # prend en charge hello suivant quatre types de paquets de connexion avancées :  

* **Faisceaux filtrés**. utilisateur de la Hello peut définir un prédicat à l’aide des emplacements de nœud de couche source hello et nœud de couche hello destination hello. Nœuds sont connectés à chaque fois que le prédicat de hello a la valeur True.
* **Faisceaux convolutionnels**. utilisateur de Hello peut définir des petits cercles de nœuds dans la couche de source de hello. Chaque nœud de couche de destination hello est voisinage tooone connecté de nœuds de couche de source de hello.
* **Faisceaux de regroupement** et **faisceaux de normalisation de réponse**. Il s’agit des regroupements tooconvolutional similaire qui Bonjour utilisateur définit des petits cercles de nœuds de couche de source de hello. Hello différence est que les poids hello des bords hello dans ces offres ne sont pas capable d’apprentissage. Au lieu de cela, une fonction prédéfinie est appliquée toohello nœud de source de valeurs de la valeur de nœud de destination de hello toodetermine.  

À l’aide de Net # structure de hello toodefine d’un réseau neuronal rend possible toodefine des structures complexes telles que les réseaux neuronaux ou des structures de dimensions arbitraires, qui sont connues learning tooimprove sur des données telles que l’image, audio ou vidéo.  

## <a name="supported-customizations"></a>Personnalisations prises en charge
architecture de Hello des modèles de réseau neuronal que vous créez dans Azure Machine Learning peut être largement personnalisé à l’aide de Net #. Vous pouvez :  

* Créer des couches masquées et le nombre de nœuds hello de contrôle dans chaque couche.
* Spécifiez comment les couches sont toobe connecté tooeach autres.
* définir des structures de connectivité spéciales, telles que des convolutions et des faisceaux à poids partagé ;
* spécifier différentes fonctions d'activation.  

Pour plus d’informations de syntaxe du langage de spécification hello, consultez [spécification de la Structure](#Structure-specifications).  

Pour obtenir des exemples de définition de réseaux neuronaux pour certaines tâches, à partir de toocomplex simplex, d’apprentissage courantes, consultez [exemples](#Examples-of-Net#-usage).  

## <a name="general-requirements"></a>Conditions générales
* Il doit y avoir exactement une couche de sortie, au moins une couche d’entrée et aucune ou plusieurs couches masquées. 
* Chaque couche a un nombre fixe de nœuds, organisés de façon conceptuelle dans un tableau rectangulaire aux dimensions arbitraires. 
* Les couches d’entrée n’ont aucun paramètre formé associé et point hello où les données d’instance entre le réseau de hello. 
* Paramètres formés, appelés poids et des écarts ont associés à des couches capable d’apprentissage (hello couches masquées et de sortie). 
* les nœuds source et de destination Hello doivent être dans des couches distinctes. 
* Les connexions doivent être acycliques ; en d’autres termes, il ne peut pas être une chaîne de connexions de début du nœud source initial de toohello précédent.
* couche de sortie Hello ne peut pas être une source d’un groupe de connexion.  

## <a name="structure-specifications"></a>Spécifications de structures
Une spécification de structure de réseau neuronal est composée de trois sections : hello **déclaration de constante**, hello **déclaration de couche**, hello **déclaration de connexion**. Il existe également une section de **déclaration de partage**, qui est facultative. les sections Hello peuvent être spécifiées dans n’importe quel ordre.  

## <a name="constant-declaration"></a>Déclaration de constante
Ce type de déclaration est facultatif. Il fournit un moyen toodefine utilisées ailleurs dans la définition du réseau neuronal hello des valeurs. instruction de déclaration Hello se compose d’un identificateur suivi par un signe égal et une expression de valeur.   

Par exemple, après l’instruction de hello définit une constante **x**:  

    Const X = 28;  

toodefine deux ou plusieurs constantes simultanément, placez les valeurs et les noms d’identificateur hello entre accolades et séparés par des points-virgules. Par exemple :  

    Const { X = 28; Y = 4; }  

côté droit de Hello de chaque expression d’assignation peut être un entier, un nombre réel, une valeur booléenne (True ou False) ou une expression mathématique. Par exemple :  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>Déclaration de couche
déclaration de couche Hello est obligatoire. Il définit la taille de hello et de la source de la couche de hello, y compris ses attributs et groupes de connexion. Hello commence d’instruction de déclaration par nom hello de couche hello (entrée, masqués ou de sortie), suivis de dimensions hello de couche de hello (il s’agit d’un tuple d’entiers positifs). Par exemple :  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* Hello de dimensions de hello est nombre hello de nœuds de couche de hello. Dans cet exemple, il existe deux dimensions [5,20], ce qui signifie qu’il existe 100 nœuds dans la couche de hello.
* les couches Hello peuvent être déclarés dans n’importe quel ordre, à une exception près : Si plusieurs couches d’entrée est défini, hello dans lequel ils sont déclarés doivent suivre hello ordre de fonctionnalités dans les données d’entrée hello.  

toospecify hello le nombre de nœuds dans une couche être déterminé automatiquement, utilisez hello **automatique** (mot clé). Hello **automatique** (mot clé) a des effets différents, selon la couche de hello :  

* Dans une déclaration de la couche d’entrée, nombre de hello de nœuds est nombre hello de fonctionnalités dans les données d’entrée hello.
* Dans une déclaration de la couche masquée, nombre hello de nœuds est nombre hello spécifié par la valeur du paramètre hello pour **nombre de nœuds masqués**. 
* Dans une déclaration de couche de sortie, nombre hello de nœuds est 2 pour la classification de deux classes, 1 pour la régression et le numéro de toohello égale de nœuds de sortie pour la classification multiclasse.   

Par exemple, hello définition de réseau suivant autorise hello taille de toutes les couches toobe déterminé automatiquement :  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


Une déclaration de la couche d’une couche capable d’apprentissage (hello couches masquées ou de sortie) peut éventuellement inclure hello sortie (fonction) (également appelée une fonction d’activation), qui utilise par défaut trop**sigmoïde** pour les modèles de classification et **linéaire** pour les modèles de régression. (Même si vous utilisez la valeur par défaut de hello, vous pouvez déclarer explicitement fonction d’activation de hello, si vous le souhaitez pour plus de clarté.)

Hello des fonctions de sortie suivantes sont prises en charge :  

* sigmoid
* linear
* softmax
* rlinear
* square
* sqrt
* srlinear
* abs
* tanh 
* brlinear  

Par exemple, hello suit déclaration utilise hello **softmax** fonction :  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>Déclaration de connexion
Immédiatement après la définition de couche capable d’apprentissage de hello, vous devez déclarer les connexions entre les couches hello que vous avez défini. déclaration de regroupement de connexion Hello commence par le mot clé de hello **de**, suivi par nom hello de type de couche et hello de source de toocreate de regroupement de connexion du regroupement hello.   

À ce jour, cinq types de faisceau de connexions sont pris en charge :  

* **Complète** lots, indiqués par le mot clé de hello **toutes les**
* **Filtré** lots, indiqués par le mot clé de hello **où**, suivi d’une expression de prédicat
* **À convolution** lots, indiqués par le mot clé de hello **convolve**, suivi par les attributs de convolution hello
* **Le regroupement de** lots, indiquées par mots clés de hello **max pool** ou **signifie pool**
* **Normalisation de la réponse** lots, indiqués par le mot clé de hello **normales de réponse**      

## <a name="full-bundles"></a>Faisceaux complets
Un regroupement de connexion complète inclut une connexion à partir de chaque nœud dans le nœud de tooeach hello source couche hello calque de destination. Il s’agit de type de connexion réseau hello par défaut.  

## <a name="filtered-bundles"></a>Faisceaux filtrés
Une spécification de faisceau de connexion filtré inclut un prédicat, dont la syntaxe est assez similaire à celle d'une expression lambda C#. Hello exemple suivant définit deux groupes filtrées :  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* Dans le prédicat hello pour *ByRow*, **s** est un paramètre représentant un index dans un tableau rectangulaire de hello des nœuds de la couche d’entrée de hello, *Pixels*, et **d**  est un paramètre représentant un index dans le tableau hello des nœuds de couche masquée de hello, *ByRow*. Hello type des deux **s** et **d** est un tuple d’entiers de longueur deux. D’un point de vue conceptuel, **s** couvre toutes les paires d’entiers avec *0 <= s[0] < 10* et *0 <= s[1] < 20*, tandis que **d** couvre toutes les paires d’entiers avec *0 <= d[0] < 10* et *0 <= d[1] < 12*. 
* Sur le côté droit de hello d’expression de prédicat hello, il existe une condition. Dans cet exemple, pour chaque valeur de **s** et **d** telles que hello condition est True, il est un bord à partir du nœud de destination couche toohello hello source couche nœud. Par conséquent, cette expression de filtre indique cette offre groupée hello inclut une connexion à partir du nœud hello défini par **s** nœud toohello défini par **d** dans tous les cas où s [0] est égale alimentaire [0].  

Vous pouvez également spécifier un ensemble de poids pour un faisceau filtré. Hello valeur hello **poids** l’attribut doit être un tuple de valeurs à virgule flottante dont la longueur correspond au nombre de hello de connexions définis par l’offre groupée de hello. Par défaut, les poids sont générés de façon aléatoire.  

Valeurs de pondération sont regroupés par index hello du nœud de destination. Autrement dit, si le premier nœud de destination hello est connecté a duré nœuds sources, hello tout d’abord *K* éléments Hello **poids** tuple sont les poids hello pour hello premier nœud de destination, dans l’ordre d’index source. Hello que va de même pour hello restant des nœuds de destination.  

Il est possible de toospecify poids directement en tant que valeurs de constante. Par exemple, si vous avez appris les poids hello précédemment, vous pouvez les spécifier en tant que constantes à l’aide de cette syntaxe :

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>Faisceaux convolutionnels
Lorsque les données d’apprentissage hello possèdent une structure homogène, les connexions à convolution sont couramment utilisés toolearn les fonctionnalités de haut niveau de données de hello. Par exemple, pour les données images, audio ou vidéo, la dimensionnalité spatiale ou temporelle peut être assez uniforme.  

Les regroupements à convolution employant rectangulaire **noyaux** qui sont glissé des dimensions de hello. Essentiellement, chaque noyau définit un ensemble de poids appliquées dans les cercles locales, tooas référencé **applications du noyau**. Chaque application de noyau correspond nœud tooa dans la couche de source de hello, qui est référencé tooas hello **nœud central**. poids Hello d’un noyau sont partagés entre plusieurs connexions. Dans un regroupement à convolution, chaque noyau est rectangulaire et toutes les applications du noyau sont hello même taille.  

Les regroupements à convolution prennent en charge hello suivant d’attributs :

**InputShape** définit la dimensionnalité hello de couche de source de hello pour les besoins de hello de ce groupe à convolution. valeur de Hello doit être un tuple d’entiers positifs. produit Hello d’entiers de hello doit être égal à nombre hello de nœuds de couche de source de hello, mais dans le cas contraire, il n’a pas besoin dimensionnalité de hello toomatch déclarée pour la couche de source de hello. la longueur de ce tuple Hello devient hello **arité** valeur pour le regroupement à convolution de hello. (Généralement une arité fait référence toohello nombre d’arguments ou les opérandes qu’une fonction peut prendre).  

forme de hello toodefine et les emplacements des noyaux de hello, utiliser les attributs de hello **KernelShape**, **Stride**, **remplissage**, **LowerPad**, et **UpperPad**:   

* **KernelShape**: dimensionnalité de hello définit (obligatoire) de chaque noyau pour le regroupement à convolution de hello. valeur de Hello doit être un tuple d’entiers positifs avec une longueur égale à arité hello du groupement de hello. Chaque composant de ce tuple doit pas être supérieure à composant correspondant de hello de **InputShape**. 
* **STRIDE**: (facultatif) définit hello glissante tailles d’étape de la convolution de hello (taille d’une seule étape pour chaque dimension), qui est la distance entre les nœuds de centrale hello hello. valeur de Hello doit être un tuple d’entiers positifs avec une longueur arité hello du groupement de hello. Chaque composant de ce tuple doit pas être supérieure à composant correspondant de hello de **KernelShape**. valeur par défaut de Hello est un tuple avec tous les tooone égale de composants. 
* **Partage**: (facultatif) définit hello partage de la pondération pour chaque dimension de la convolution de hello. valeur de Hello peut être une valeur booléenne unique ou un tuple de valeurs booléennes avec une longueur arité hello du groupement de hello. Une valeur booléenne est étendue toobe un tuple de longueur correcte de hello avec tous les composants toohello égale de valeur spécifiée. valeur par défaut de Hello est un tuple qui se compose de toutes les valeurs True. 
* **MapCount**: (facultatif) définit hello nombre de fonctionnalité de mappages pour l’offre groupée à convolution de hello. valeur de Hello peut être un entier positif unique ou un tuple d’entiers positifs avec une longueur arité hello du groupement de hello. Une seule valeur entière est étendue toobe un tuple de longueur correcte de hello avec hello première composants égal toohello spécifié de valeur et tous les hello tooone égale des composants restants. Hello par défaut est 1. Nombre total de Hello des mappages de fonction est produit hello des composants hello de hello tuple. Hello factorisation de ce nombre total entre les composants de hello détermine comment les valeurs de mappage de fonction hello sont regroupés dans les nœuds de destination hello. 
* **Poids**: (facultatif) définit hello initiales poids pour le groupe de hello. valeur de Hello doit être un tuple de valeurs à virgule flottante avec une longueur de hello nombre de noyaux fois hello poids par noyau, tel que défini plus loin dans cet article. poids par défaut de Hello sont générés de façon aléatoire.  

Il existe deux ensembles de propriétés qui contrôlent la marge intérieure, propriétés hello en cours s’excluent mutuellement :

* **Marge intérieure**: (facultatif) détermine si hello d’entrée doit être remplie à l’aide un **modèle de remplissage par défaut**. valeur de Hello peut être une valeur booléenne unique, ou il peut être un tuple de valeurs booléennes avec une longueur arité hello du groupement de hello. Une valeur booléenne est étendue toobe un tuple de longueur correcte de hello avec tous les composants toohello égale de valeur spécifiée. Si la valeur hello pour une dimension a la valeur True, source de hello logiquement remplie dans la dimension avec des applications de cellules de valeur zéro toosupport noyau supplémentaires, telles que hello des nœuds central des noyaux de première et dernières hello dans la dimension sont des nœuds de premier et derniers de hello dans la dimension dans la couche de source de hello. Par conséquent, le nombre hello de nœuds de « factices » dans chaque dimension est déterminé automatiquement, toofit exactement *(InputShape [d] - 1) / Stride [d] + 1* noyaux dans la couche de source de hello complétée. Si la valeur hello pour une dimension a la valeur False, hello noyaux définies de sorte que le nombre de hello de nœuds de chaque côté sont omis est même hello (haut tooa la différence de 1). Hello par défaut de cet attribut est un tuple avec tous les tooFalse égale de composants.
* **UpperPad** et **LowerPad**: (facultatif) indiquez mieux contrôler durée hello toouse de remplissage. **Important :** ces attributs peuvent être définis si et seulement si hello **remplissage** propriété ci-dessus est ***pas*** défini. les valeurs de Hello doivent être des valeurs entières de tuples avec des longueurs qui sont arité hello du groupement de hello. Lorsque ces attributs sont spécifiés, « factices » nœuds sont ajoutés toohello inférieur et supérieures extrémités de chaque dimension du hello d’entrée couche. Hello nombre de nœuds ajoutés toohello inférieure et supérieure se termine dans chaque dimension est déterminée par **LowerPad**[i] et **UpperPad**[i] respectivement. tooensure que noyaux correspondent uniquement trop « réels » nœuds et pas trop « factice », hello conditions suivantes doit être remplie :
  * Chaque élément de **LowerPad** doit être strictement inférieur à KernelShape[d]/2. 
  * Chaque élément de **UpperPad** ne doit pas être supérieur à KernelShape[d]/2. 
  * Hello par défaut de ces attributs est un tuple avec tous les too0 égale de composants. 

paramètre de Hello **remplissage** = true permet de marge intérieure est besoins tookeep hello « center » du noyau de hello à l’intérieur de hello à « réal » d’entrée. Cela modifie mathématiques hello un bit pour le calcul de taille de la sortie hello. En règle générale, la taille de sortie hello *D* est calculée en tant que *D = (I - K) / S + 1*, où *I* est la taille de l’entrée hello, *K* est la taille du noyau de hello, *S* est stride de hello, et  */*  est la division d’entier (arrondi vers zéro). Si vous définissez UpperPad = [1, 1], hello entrée taille *I* est effectivement 29 et par conséquent *D = (29-5) / 2 + 1 = 13*. Toutefois, quand **Padding** = true, *I* est essentiellement augmenté de *K - 1* ; donc *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*. En spécifiant des valeurs pour **UpperPad** et **LowerPad** vous contrôlez beaucoup plus hello de remplissage qu’if vous venez de définir **remplissage** = true.

Pour plus d’informations sur les réseaux convolutionnels et leurs applications, consultez les articles suivants :  

* [http://deeplearning.net/tutorial/lenet.html ](http://deeplearning.net/tutorial/lenet.html)
* [http://research.microsoft.com/pubs/68920/icdar03.pdf](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>Faisceaux de regroupement
A **le regroupement de regroupement** s’applique à la connectivité tooconvolutional similaire geometry, mais il utilise la valeur de nœud destination valeurs tooderive hello fonctions prédéfinies toosource nœud. De ce fait, les faisceaux de regroupement n’ont pas d’état entraînable (poids ou biais). Le regroupement tous hello à convolution attributs à l’exception de la prise en charge regroupements **partage**, **MapCount**, et **poids**.  

En règle générale, les noyaux hello résumées par unités regroupement adjacentes ne se chevauchent pas. Si Stride [d] est égale tooKernelShape [d] dans chaque dimension, une couche hello obtenue est hello traditionnelle locale regroupement couche, qui est couramment employé dans les réseaux neuronaux à convolution. Chaque nœud de destination calcule hello maximale ou moyenne hello des activités de hello de son noyau dans la couche de source de hello.  

Hello, l’exemple suivant illustre un ensemble de regroupement : 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* arité Hello du groupement de hello est 3 (hello longueur de hello tuples **InputShape**, **KernelShape**, et **Stride**). 
* nombre de Hello de nœuds de couche de source de hello est *5 * 24 * 24 = 2880*. 
* Il s’agit d’une couche de regroupement locale traditionnelle, car les valeurs **KernelShape** et **Stride** sont égales. 
* nombre de Hello de nœuds de couche de destination hello est *5 * 12 * 12 = 1 440*.  

Pour plus d’informations sur les couches de regroupement, consultez les articles suivants :  

* [http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Section 3.4)
* [http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>Faisceaux de normalisation de réponse
**Normalisation de la réponse** est un modèle de normalisation local qui a été introduit par Geoffrey Hinton, et autres, dans le livre de hello [ImageNet Classiﬁcation avec des réseaux neuronaux à convolution approfondie](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf). Normalisation de la réponse est généralisation tooaid utilisés dans les réseaux neurones. Lorsqu’un neurone déclenche à un niveau très élevé d’activation, une couche de normalisation de réponse local supprime au niveau de l’activation de hello Hello entourant les neurones. Cette opération s’effectue à l’aide de trois paramètres (***α***, ***β*** et ***k***) et d’une structure convolutionnelle (ou forme de voisinage). Chaque neurone hello calque de destination ***y*** correspond tooa neurone ***x*** dans la couche de source de hello. Hello au niveau de l’activation de ***y*** est donnée par hello formule, suivante où ***f*** est au niveau de l’activation de hello d’un neurone, et ***Nx*** est noyau de hello (ou un ensemble de hello contenant hello neurones dans le voisinage hello de ***x***), comme défini par hello suivant à convolution structure :  

![][1]  

Groupes de normalisation de réponse prend en charge tous les attributs à convolution hello sauf **partage**, **MapCount**, et **poids**.  

* Si le noyau de hello contient neurones hello même mapper en tant que ***x***, schéma de normalisation hello est référencé tooas **même mapper normalisation**. toodefine même mapper normalisation, dans la première coordonnée hello **InputShape** doit avoir hello valeur 1.
* Si le noyau de hello contient neurones hello même position spatiale ***x***, mais les neurones hello se trouvent dans d’autres mappages, schéma de normalisation hello est appelée **mappe à travers de normalisation**. Ce type de normalisation de la réponse implémente un formulaire d’inhiber latéral inspiré par type de hello trouvé dans les neurones réels, création de concurrence pour les niveaux d’activation big dans la liste de sorties neurone calculées sur des cartes de différents. toodefine entre mappe la normalisation et la première coordonnée hello doit être un entier supérieur à un et ne supérieur au nombre de hello des mappages reste hello de coordonnées de hello doit avoir la valeur de hello 1.  

Étant donné que les offres groupées de normalisation de réponse s’appliquent à une fonction prédéfinie toosource nœud valeurs toodetermine hello nœud valeur de destination, ils n’ont aucun état capable d’apprentissage (poids ou écarts).   

**Alerte**: nœuds hello hello calque de destination correspondent tooneurons qui sont des nœuds de centrale hello des noyaux de hello. Par exemple, si KernelShape [d] est impair, puis *KernelShape [d] / 2* correspond le nœud de noyau central toohello. Si *KernelShape [d]* est pair, nœud central de hello est *KernelShape [d] / 2-1*. Par conséquent, si **remplissage**[d] est False, hello tout d’abord et hello dernière *KernelShape [d] / 2* nœuds n’ont pas de nœuds correspondants hello calque de destination. tooavoid cette situation, définissez **remplissage** en tant que [valeur est true, la valeur true,..., true].  

En outre toohello quatre attributs décrits précédemment, groupes de normalisation de réponse également hello prise en charge suivant d’attributs :  

* **Alpha**: (obligatoire) spécifie une valeur à virgule flottante qui correspond trop***α*** dans la formule précédente de hello. 
* **Version bêta**: (obligatoire) spécifie une valeur à virgule flottante qui correspond trop***β*** dans la formule précédente de hello. 
* **Décalage**: (facultatif) spécifie une valeur à virgule flottante qui correspond trop***k*** dans la formule précédente de hello. Too1 la valeur par défaut.  

Hello exemple suivant définit un groupe de normalisation de réponse à l’aide de ces attributs :  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* couche de source de Hello inclut cinq tables, chaque dimension unede 12 x 12, total de nœuds de 1440. 
* Hello valeur **KernelShape** indique qu’il s’agit d’une même normalisation couche, où les voisinage hello est un rectangle 3 x 3. 
* Hello la valeur par défaut de **remplissage** est False, par conséquent, la couche de destination hello est uniquement 10 nœuds dans chaque dimension. un nœud de tooinclude hello calque de destination qui correspond à nœud tooevery dans la couche de source de hello, ajouter une marge intérieure = [true, true, true] ; et également modifier taille hello de RN1 [5, 12, 12].  

## <a name="share-declaration"></a>Déclaration de partage
Net# peut prendre en charge la définition de plusieurs faisceaux avec des poids partagés. poids Hello de n’importe quel deux regroupements peuvent être partagées si leurs structures sont hello identiques. Hello syntaxe définit les regroupements avec des poids partagés :  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

Par exemple, hello partage-déclaration suivante spécifie les noms de couches hello, qui indique que le poids et biais doivent être partagés :  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* les fonctionnalités d’entrée Hello sont répartis dans deux couches d’entrée tailles égales. 
* les couches Hello masqué calculez des fonctionnalités au niveau supérieures sur deux couches de d’entrée hello. 
* Hello partage-déclaration spécifie que *H1* et *H2* doivent être calculées Bonjour même de façon à partir de leurs entrées respectives.  

Il est également possible de spécifier cet élément avec deux déclarations de partage indépendantes, comme suit :  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

Vous pouvez utiliser la forme abrégée de hello uniquement lorsque les couches hello contient un lot unique. En règle générale, de partage est possible uniquement lorsque la structure pertinentes de hello est identique, ce qui signifie que leur ont hello même taille, de même geometry à convolution et ainsi de suite.  

## <a name="examples-of-net-usage"></a>Exemples d’utilisation de Net#
Cette section fournit quelques exemples de la façon dont vous pouvez utiliser Net # tooadd masqué couches, qui définissent la façon de hello que couches masquées interagissent avec d’autres couches et créer des réseaux à convolution.   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>Définition d'un réseau neuronal personnalisé simple : exemple « Hello World »
Cet exemple simple montre comment toocreate un neuronal réseau modèle qui a une seule couche cachée.  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

Hello illustre certaines commandes de base comme suit :  

* première ligne Hello définit couche d’entrée de hello (nommé *données*). Lorsque vous utilisez hello **automatique** (mot clé), les réseaux neuronaux hello inclut automatiquement toutes les colonnes de fonctionnalités dans les exemples d’entrée hello. 
* Hello deuxième ligne crée la couche masquée de hello. nom de Hello *H* est attribué toohello couche masquée, qui possède des nœuds de 200. Cette couche est totalement connecté toohello d’entrée.
* troisième ligne de Hello définit la couche de sortie hello (nommé *O*), qui contient 10 nœuds de sortie. Si le réseau neuronal de hello est utilisé pour la classification, il est un nœud de sortie par la classe. mot clé de Hello **sigmoïde** indique que la fonction de sortie hello est couche de sortie toohello appliqué.   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>Définir plusieurs couches masquées : exemple de vision
Hello exemple suivant montre comment toodefine un réseau neuronal légèrement plus complexe, avec plusieurs couches masquées personnalisés.  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

Cet exemple illustre plusieurs fonctionnalités du langage de spécification de réseaux neuronaux hello :  

* structure de Hello possède deux couches d’entrée, *Pixels* et *métadonnées*.
* Hello *Pixels* couche est une couche de source pour les deux groupes de connexion, avec des couches de destination, *ByRow* et *ByCol*.
* Hello couches *collecter* et *résultat* sont des couches de destination dans plusieurs groupes de connexion.
* couche de sortie Hello *résultat*, est une couche de destination dans deux groupes de connexion, une par hello masqué (regroupement) de second niveau comme une couche de destination et hello autre avec la couche d’entrée de hello (métadonnées) comme une couche de destination.
* Hello couches masquées, *ByRow* et *ByCol*, spécifiez la connectivité filtrée à l’aide d’expressions de prédicat. Plus précisément, le nœud de hello dans *ByRow* à [x, y] est nœuds connectés toohello *Pixels* qui ont le premier x de coordonnées, hello premier index toohello égal coordonnées du nœud. De même, le nœud de hello dans *ByCol à [x, y] est nœuds connectés toohello _Pixels* qui ont des coordonnées d’index deuxième hello dans une des coordonnées de deuxième du nœud hello, y.  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>Définir un réseau convolutionnel pour la classification multiclasse : exemple de reconnaissance de chiffre
définition de Hello Hello suivant réseau est conçue toorecognize numéros et il illustre des techniques avancées pour la personnalisation d’un réseau neuronal.  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* structure de Hello dispose d’une couche d’entrée unique, *Image*.
* Hello mot clé **convolve** indique que les couches hello *Conv1* et *Conv2* sont des couches à convolution. Chacune de ces déclarations de couche est suivie d’une liste d’attributs de convolution hello.
* Hello net a une troisième masquée couche, *Hid3*, qui est entièrement connecté toohello deuxième couche masquée, *Conv2*.
* couche de sortie Hello *chiffre*, est la troisième couche masquée toohello uniquement connecté, *Hid3*. mot clé de Hello **tous les** indique cette couche de sortie hello est entièrement connectée trop*Hid3*.
* Hello arité de convolution de hello est trois (hello longueur de hello tuples **InputShape**, **KernelShape**, **Stride**, et **partage**). 
* nombre de Hello de poids par noyau est *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26. Ou 26 * 50 = 1 300*.
* Vous pouvez calculer les nœuds hello dans chaque couche masquée comme suit :
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[1] = (13 - 5) / 2 + 1 = 5. 
  * **NodeCount**\[2] = (13 - 5) / 2 + 1 = 5. 
* Hello nombre total de nœuds peut être calculée à l’aide de hello déclaré la dimensionnalité de hello de couche, [50, 5, 5], comme suit :  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*
* Étant donné que **partage**[d] a la valeur False uniquement pour *d == 0*, nombre de hello de noyaux est  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*. 

## <a name="acknowledgements"></a>Remerciements
Hello langage Net # pour personnaliser l’architecture hello des réseaux neuronaux a été développé à Microsoft par Shon Katzenberger (architecte, apprentissage) et Alexey Kamenev (Software Engineer, Microsoft Research). Il est utilisé en interne pour l’apprentissage de projets et des applications allant des analytique de tootext détection image. Pour plus d’informations, consultez [réseaux neuronaux dans Azure ML - Introduction tooNet #](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

