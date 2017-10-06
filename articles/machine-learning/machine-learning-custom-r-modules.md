---
title: "aaaAuthor des Modules R personnalisés dans Azure Machine Learning | Documents Microsoft"
description: "Démarrage rapide pour la création de modules R personnalisés dans Microsoft Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>Création de modules R personnalisés dans Azure Machine Learning
Cette rubrique décrit comment tooauthor et déployer un module R personnalisé dans Azure Machine Learning. Il explique ce que sont les modules R personnalisés et quels fichiers sont utilisé toodefine les. Il illustre comment tooconstruct hello les fichiers qui définissent un module et comment tooregister hello module pour le déploiement dans un espace de travail Machine Learning. Hello éléments et attributs utilisés dans la définition de hello de module personnalisé de hello sont ensuite décrits plus en détail. Comment les fonctionnalités auxiliaire toouse et les fichiers plusieurs sorties est également présenté. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>Qu’est-ce qu’un module R personnalisé ?
A **module personnalisé** est un module défini par l’utilisateur qui peut être téléchargés tooyour espace de travail et exécutée au sein d’une expérience Azure Machine Learning. Un **module R personnalisé** est un module exécutant une fonction R définie par l’utilisateur. **R** est un langage de programmation utilisé pour le traitement informatique des statistiques et les graphiques. Les chercheurs de données et les statisticiens s’en servent pour implémenter des algorithmes. Actuellement, R est hello seule langue prise en charge dans des modules personnalisés, mais prise en charge de langues supplémentaires est planifiée pour les versions futures.

Les modules personnalisés ont **état de première classe** dans Azure Machine Learning dans les sens hello qu’elles peuvent être utilisées comme tout autre module. Ils peuvent être exécutés avec d’autres modules, inclus dans des expériences publiées ou dans des visualisations. Vous contrôlez algorithme hello implémenté par le module de hello, hello toobe de ports d’entrée et de sortie utilisé, hello des paramètres de modélisation et d’autres comportements d’exécution différents. Une expérience qui contient des modules personnalisés peut également être publiée dans hello Cortana Intelligence galerie pour partager facilement.

## <a name="files-in-a-custom-r-module"></a>Fichiers dans un module R personnalisé
Un module R personnalisé est défini par un fichier .zip contenant au moins deux fichiers :

* A **fichier source** qui implémente la fonction hello R exposée par le module de hello
* Un **fichier de définition XML** qui décrit l’interface de module personnalisé hello

Autres fichiers auxiliaires peuvent également être inclus dans le fichier .zip hello qui fournit des fonctionnalités qui sont accessibles à partir de modules personnalisés de hello. Cette option est décrite dans hello **Arguments** dans le cadre de la section de référence hello **éléments dans le fichier de définition XML hello** hello quickstart exemple suivant.

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>Exemple de démarrage rapide : définir, mettre en package et enregistrer un module R personnalisé
Cet exemple illustre comment tooconstruct hello les fichiers requis par un module R personnalisé, empaqueter dans un fichier zip et module hello de Registre dans votre espace de travail Machine Learning. Hello exemple zip package et un exemple de fichiers peuvent être téléchargés à partir de [CustomAddRows.zip de télécharger le fichier](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).

## <a name="hello-source-file"></a>fichier de source de Hello
Considérez exemple hello d’un **personnalisé Add Rows** module qui modifie l’implémentation standard de hello Hello **Add Rows** module utilisé tooconcatenate lignes (observations) à partir de deux jeux de données (des trames de données). Hello standard **Add Rows** module ajoute des lignes de hello fin hello deuxième jeu de données d’entrée toohello du jeu de données d’entrée première hello à l’aide de hello `rbind` algorithme. Hello personnalisé `CustomAddRows` fonction accepte les deux jeux de données de la même façon, mais accepte également un paramètre booléen swap comme une entrée supplémentaire. Si la valeur du paramètre d’échange hello est trop**FALSE**, il retourne hello même jeu de données comme hello implémentation standard. Mais si le paramètre d’échange hello est **TRUE**, fonction hello ajoute des lignes de fin de toohello premier jeu de données d’entrée de hello le deuxième jeu de données à la place. fichier CustomAddRows.R Hello qui contient l’implémentation de hello Hello R `CustomAddRows` fonction exposée par hello **personnalisé Add Rows** module a hello suivant le code R.

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a>fichier de définition XML Hello
tooexpose cela `CustomAddRows` fonctionne comme un module d’Azure Machine Learning, un fichier de définition XML doit être créé toospecify comment hello **personnalisé Add Rows** module doit ressemblent et se comportent. 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


Il est critique toonote qui hello valeur Hello **id** attributs Hello **entrée** et **Arg** éléments dans le fichier XML de hello doivent correspondre aux noms de paramètre de fonction de hello Hello R le code dans le fichier de CustomAddRows.R hello exactement : (*dataset1*, *dataset2*, et *échange* dans l’exemple de hello). De même, hello valeur Hello **entryPoint** attribut Hello **langage** élément doit correspondre exactement au nom de hello de fonction hello dans le script de hello R : (*CustomAddRows* dans l’exemple hello). 

En revanche, hello **id** attribut pour hello **sortie** élément ne correspond pas tooany les variables de script de hello R. Quand plusieurs sorties est requis, se contentent de retourner une liste à partir de la fonction hello R résultats placés *Bonjour même ordre* en tant que **sorties** sont déclarés dans le fichier XML de hello.

### <a name="package-and-register-hello-module"></a>Package et inscrire le module de hello
Enregistrez ces deux fichiers comme *CustomAddRows.R* et *CustomAddRows.xml* et puis zip hello ensemble la deux fichiers dans un *CustomAddRows.zip* fichier.

tooregister dans votre espace de travail Machine Learning, espace de travail tooyour accédez hello Machine Learning Studio, cliquez sur hello **+ nouveau** bouton bas de hello **MODULE -> à partir de PACKAGE ZIP** tooupload Hello nouvelle **personnalisé Add Rows** module.

![Charger les zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

Hello **personnalisé Add Rows** module est désormais prêt toobe accédé par vos expériences d’apprentissage.

## <a name="elements-in-hello-xml-definition-file"></a>Éléments dans le fichier de définition XML hello
### <a name="module-elements"></a>Éléments de module
Hello **Module** élément est toodefine utilisé un module personnalisé dans le fichier XML de hello. Plusieurs modules peuvent être définis dans un fichier XML à l’aide de plusieurs éléments **module** . Chaque module de votre espace de travail doit avoir un nom unique. Enregistrer un module personnalisé avec le même nom qu’un module personnalisé existant de hello et il remplace un module existant de hello hello nouveau. Modules personnalisés peuvent, toutefois, être inscrit avec hello comme un module Azure Machine Learning existant du même nom. Si elles apparaissent donc, Bonjour **personnalisé** catégorie de la palette de module hello.

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


Au sein de hello **Module** élément, vous pouvez spécifier deux éléments facultatifs supplémentaires :

* un **propriétaire** élément imbriqué dans le module de hello  
* un **Description** élément qui contient le texte qui s’affiche dans l’aide rapide pour le module de hello et lorsque vous pointez sur le module hello Bonjour l’interface utilisateur de Machine Learning.

Règles pour les limites de caractères dans les éléments de Module hello :

* Hello valeur Hello **nom** attribut Bonjour **Module** élément ne doit pas dépasser 64 caractères. 
* Hello contenu Hello **Description** élément ne doit pas dépasser 128 caractères.
* Hello contenu Hello **propriétaire** élément ne doit pas dépasser 32 caractères.

Les résultats d’un module peuvent être déterministes ou nondeterministic.* * par défaut, tous les modules sont considérés comme toobe déterministe. Autrement dit, étant donné un jeu qui ne changent pas de paramètres d’entrée et de données, le module de hello doit retourner hello mêmes résultats eacRAND ou un functionh de son exécution. Étant donné ce comportement, Azure Machine Learning Studio réexécute uniquement les modules marqués comme étant déterministe si un paramètre ou les données d’entrée hello a changé. Retour des résultats de hello mis en cache fournit également une exécution beaucoup plus rapide d’expériences.

Il existe des fonctions qui sont non déterministes, telles que RAND ou une fonction qui retourne la date ou l’heure de hello. Si votre module utilise une fonction non déterministe, vous pouvez spécifier que le module hello est non déterministe par hello de paramètre facultatif **isDeterministic** trop d’attributs**FALSE**. Cela garantit que le module hello est exécuté à nouveau à chaque exécution de l’expérience de hello, même si hello module Paramètres d’entrée et n’ont pas changé. 

### <a name="language-definition"></a>Définition de l’élément Language
Hello **langage** élément dans votre fichier de définition XML est la langue de module personnalisé utilisé toospecify hello. Actuellement, R est hello uniquement prise en charge de langue. Hello valeur Hello **sourceFile** attribut doit être le nom hello du fichier hello R contenant hello fonction toocall lors de l’exécution de module de hello. Ce fichier doit faire partie du package zip de hello. Hello valeur Hello **entryPoint** attribut est le nom hello de fonction hello appelée et doit correspondre à une fonction valide définie dans le fichier de source de hello.

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>Ports
les ports d’entrée et de sortie pour un module personnalisé Hello sont spécifiés dans les éléments enfants de hello **Ports** section hello XML du fichier de définition. commande Hello de ces éléments détermine hello disposition expérimentée (UX) par les utilisateurs. premier enfant de Hello **d’entrée** ou **sortie** répertoriés dans hello **Ports** élément du fichier XML de hello devienne le port d’entrée de la plus à gauche hello Bonjour Machine Learning UX
Chaque d’entrée et de port de sortie peut-être avoir facultatif **Description** élément enfant qui spécifie le texte hello lorsque vous pointez la souris hello sur port hello Bonjour l’interface utilisateur de Machine Learning.

**Règles relatives aux ports**:

* Le nombre maximum de **ports d’entrée et de sortie** est de 8 pour chacun.

### <a name="input-elements"></a>Éléments d'entrée
Ports d’entrée vous permettent d’espace de travail et la fonction tooyour R toopass données. Hello **des types de données** qui sont pris en charge pour les ports d’entrée sont les suivantes : 

**DataTable :** ce type est passé de tooyour R fonction comme un data.frame. En fait, tous les types (par exemple, des fichiers CSV ou des fichiers ARFF) sont pris en charge par l’apprentissage automatique et qui sont compatibles avec **DataTable** sont convertis tooa data.frame automatiquement. 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

Hello **id** attribut associée à chaque **DataTable** port d’entrée doit avoir une valeur unique, et cette valeur doit correspondre à son paramètre dans votre fonction R nommé correspondant.
Facultatif **DataTable** ports qui ne sont pas transmis en tant qu’entrée dans une expérience ont la valeur de hello **NULL** toohello passé R fonction et les ports de zip facultatif sont ignorés si hello entrée n’est pas connectée. Hello **isOptional** attribut est facultatif pour les deux hello **DataTable** et **Zip** les types et est *false* par défaut.

**Zip :** modules personnalisés pouvant accepter un fichier .zip en entrée. Cette entrée est décompressée dans le répertoire de travail hello R de votre fonction.

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

Pour les modules R personnalisés, hello id pour un port Zip n’est pas toomatch tous les paramètres de fonction hello R. Il s’agit, car le fichier zip de hello est le répertoire de travail automatiquement extraits toohello R.

**Règles d'entrée :**

* Hello valeur Hello **id** attribut Hello **entrée** élément doit être un nom de variable R valide.
* Hello valeur Hello **id** attribut Hello **entrée** élément ne doit pas comporter plu de 64 caractères.
* Hello valeur Hello **nom** attribut Hello **entrée** élément ne doit pas comporter plu de 64 caractères.
* Hello contenu Hello **Description** élément ne doit pas comporter plu de 128 caractères
* Hello valeur Hello **type** attribut Hello **entrée** l’élément doit être *Zip* ou *DataTable*.
* Hello valeur Hello **isOptional** attribut Hello **entrée** élément n’est pas obligatoire (et est *false* par défaut lorsque ne pas spécifié) ; mais s’il est spécifié, il doit être *true* ou *false*.

### <a name="output-elements"></a>Éléments d’entrée
**Ports de sortie standard :** ports de sortie sont des valeurs de retour toohello mappé à partir de votre fonction R, qui peut ensuite être utilisé par les modules suivants. *DataTable* est de type de port de sortie standard uniquement hello actuellement pris en charge. (Les types *Learners* et *Transformers* seront prochainement pris en charge.) Une sortie *DataTable* est définie comme suit :

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

Pour les sorties dans des modules R personnalisés, hello valeur Hello **id** attribut n’a pas de toocorrespond avec quoi que ce soit dans le script de hello R, mais il doit être unique. Pour une sortie de module unique, la valeur de retour de hello à partir de la fonction hello R doit être un *data.frame*. Dans commande toooutput plusieurs objets d’un type de données pris en charge, ports de sortie appropriée de hello doivent toobe spécifié dans le fichier de définition XML hello et objets de hello doivent toobe retournée sous forme de liste. objets de sortie Hello assignés toooutput ports à partir de la gauche tooright, refléter l’ordre hello dans lequel les objets de hello sont placés dans hello retourné la liste.

Par exemple, si vous souhaitez toomodify hello **personnalisé Add Rows** module toooutput hello deux jeux de données d’origine, *dataset1* et *dataset2*, en outre toohello nouveau joint jeu de données, *dataset*, (dans un ordre, de gauche tooright, en tant que : *dataset*, *dataset1*, *dataset2*), puis définissez hello la sortie des ports dans le fichier de CustomAddRows.xml hello comme suit :

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


Et retourne la liste hello des objets dans une liste dans l’ordre correct de hello dans 'CustomAddRows.R' :

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**Sortie de visualisation :** vous pouvez également spécifier un port de sortie de type *visualisation*, qui affiche le contenu de hello à partir de la sortie de console et de périphérique graphique hello R. Ce port ne fait pas partie de la sortie de fonction hello R et n’interfère pas avec la commande hello Hello d’autres types de port de sortie. Ajout d’une visualisation port toohello des modules personnalisés, tooadd un **sortie** élément avec la valeur *visualisation* pour son **type** attribut :

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**Règles de sortie :**

* Hello valeur Hello **id** attribut Hello **sortie** élément doit être un nom de variable R valide.
* Hello valeur Hello **id** attribut Hello **sortie** élément ne doit pas comporter plu de 32 caractères.
* Hello valeur Hello **nom** attribut Hello **sortie** élément ne doit pas comporter plu de 64 caractères.
* Hello valeur Hello **type** attribut Hello **sortie** l’élément doit être *visualisation*.

### <a name="arguments"></a>Arguments
Données supplémentaires peuvent être passées toohello R fonction via les paramètres du module qui sont définies dans hello **Arguments** élément. Ces paramètres apparaissent dans le volet de propriétés plus à droite de hello Hello l’interface utilisateur de Machine Learning lorsque le module de hello est sélectionné. Les arguments peuvent être des types de hello pris en charge, ou vous pouvez créer une énumération personnalisée si nécessaire. Similaire toohello **Ports** éléments, **Arguments** les éléments peuvent avoir facultatif **Description** élément qui spécifie le texte hello qui s’affiche lorsque vous pointez la souris de hello sur le nom du paramètre hello.
Argument tooany comme tooa d’attributs peuvent être ajoutées à des propriétés facultatives pour un module, tels que defaultValue, minValue et maxValue **propriétés** élément. Les propriétés valides pour hello **propriétés** élément varie selon le type d’argument hello et sont décrites avec les types d’arguments hello pris en charge dans la section suivante de hello. Arguments par hello **isOptional** propriété trop**« true »** ne nécessitent pas de hello utilisateur tooenter une valeur. Si aucune valeur n’est pas fournie toohello argument, argument de hello n’est passé toohello fonction de point d’entrée. Arguments de fonction de point d’entrée hello toobe besoin facultatif géré explicitement par la fonction hello, affecté par exemple, une valeur par défaut NULL dans la définition de fonction de point d’entrée hello. Applique un argument facultatif hello autres contraintes d’argument, par exemple, min ou max, si une valeur est fournie par l’utilisateur de hello.
Comme avec les entrées et sorties, il est essentiel que chacun des paramètres de hello ont des valeurs d’id unique qui s’y rapportent. Dans notre Guide de démarrage rapide exemple hello associé le paramètre d’id a été *swap*.

### <a name="arg-element"></a>Élément Arg
Un module est défini à l’aide de hello **Arg** élément enfant de hello **Arguments** section hello XML du fichier de définition. Comme avec les éléments enfants de hello Bonjour **Ports** section, hello organisation des paramètres Bonjour **Arguments** section définit la disposition de hello rencontrée Bonjour UX. Hello paramètres apparaissent à partir du haut vers le bas dans l’interface utilisateur de hello Bonjour ordre dans lequel ils sont définis dans le fichier XML de hello. types de Hello pris en charge par l’apprentissage automatique pour les paramètres sont répertoriés ici. 

**int** : paramètre de type entier (32 bits).

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *Propriétés facultatives* : **min**, **max**, **default** et **isOptional**

**double** : paramètre de type double.

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *Propriétés facultatives* : **min**, **max**, **default** et **isOptional**

**bool** : paramètre booléen représenté par une case à cocher dans l’expérience utilisateur.

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *Propriétés facultatives* : **default**. False si non défini

**string**: chaîne standard

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *Propriétés facultatives* : **default** et **isOptional**

**ColumnPicker**: paramètre de sélection de colonne. Ce type de rendu Bonjour UX sous la forme d’un sélecteur de colonne. Hello **propriété** élément est utilisé toospecify ici les id de hello du port hello à partir de laquelle les colonnes sont sélectionnées, où le type de port hello cible doit être *DataTable*. résultat de Hello de sélection de la colonne hello est passé toohello R fonction sous forme de liste de chaînes contenant les noms de colonne hello sélectionné. 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *Propriétés requises*: **portId** -correspondances hello id d’un élément d’entrée avec le type *DataTable*.
* *Propriétés facultatives*:
  
  * **allowedTypes** -types de colonne de hello de filtres à partir de laquelle vous pouvez choisir. Les valeurs valides incluent : 
    
    * Chiffre
    * Boolean
    * Par catégorie
    * string
    * Étiquette
    * Fonctionnalité
    * Score
    * Tout
  * **par défaut** -les sélections par défaut valide pour le sélecteur de colonne hello incluent : 
    
    * Aucun
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * Tout

**DropDown**: liste (déroulante) énumérée spécifiée par l’utilisateur. les éléments de liste déroulante Hello sont spécifiés dans hello **propriétés** à l’aide de l’élément une **élément** élément. Hello **id** pour chaque **élément** doit être unique et une variable R valide. Hello valeur Hello **nom** d’un **élément** sert de texte hello que vous voyez et valeur hello toohello R fonction passée.

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *Propriétés facultatives*:
  * **par défaut** hello - valeur de propriété par défaut de hello doit correspondre à une valeur d’id de l’une des hello **élément** éléments.

### <a name="auxiliary-files"></a>Fichiers auxiliaires
N’importe quel fichier qui est placé dans votre fichier ZIP de module personnalisé est toobe cours disponible pour une utilisation pendant l’exécution. Toutes les structures de répertoire présentes sont conservées. Cela signifie que works d’approvisionnement fichier hello même localement et dans l’exécution d’Azure Machine Learning. 

> [!NOTE]
> Notez que tous les fichiers sont extraits too'src' directory pour tous les chemins doivent avoir ' src /' préfixe.
> 
> 

Par exemple, supposons que vous souhaitez tooremove les lignes avec NAs hello dataset, également supprimez toutes les lignes en double, avant de sortir dans CustomAddRows et que vous avez déjà écrit une fonction R qui fait que dans un fichier RemoveDupNARows.R :

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
Vous pouvez de source de fichier auxiliaire hello RemoveDupNARows.R Bonjour CustomAddRows fonction :

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

Ensuite, chargez un fichier .zip contenant les éléments « CustomAddRows.R », « CustomAddRows.xml » et « RemoveDupNARows.R » en tant que module R personnalisé.

## <a name="execution-environment"></a>Environnement d’exécution
environnement d’exécution Hello pour le script de hello R utilise hello même version de R que hello **Execute R Script** module et vous pouvez utiliser hello même par défaut des packages. Vous pouvez également ajouter supplémentaire module personnalisé R packages tooyour en les incluant dans le package zip de module personnalisé hello. Chargez-les simplement dans votre script R comme vous le feriez dans votre propre environnement R. 

**Limitations de l’environnement d’exécution hello** incluent :

* Système de fichiers non persistants : fichiers écrits lors de l’exécution de module personnalisé de hello ne sont pas conservés entre les différentes exécutions de hello même module.
* Pas d’accès réseau.

