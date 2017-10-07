---
title: "aaaCreate des artefacts personnalisés pour votre machine de virtuelle DevTest Labs | Documents Microsoft"
description: "Découvrez comment tooauthor vos propres artefacts pour utilisent avec DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Créer des artefacts personnalisés pour vos machines virtuelles DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Vue d'ensemble
**Artefacts** sont toodeploy utilisé et de configurer votre application après la configuration d’une machine virtuelle. Un artefact se compose d'un fichier de définition d'artefact et autres fichiers de script qui sont stockés dans un dossier de dépôt git. Fichiers de définition d’artefact se composent de JSON et les expressions que vous pouvez utiliser toospecify ce que vous voulez tooinstall sur une machine virtuelle. Par exemple, vous pouvez définir nom hello d’un artefact, toorun de commande et les paramètres qui sont rendues disponibles lors de l’exécution de commande hello. Vous pouvez faire référence à des fichiers de script tooother dans le fichier de définition d’artefact hello par nom.

## <a name="artifact-definition-file-format"></a>Format de fichier de définition d'artefact
Hello suivant montre les sections hello qui composent la structure de base de hello d’un fichier de définition :

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| Nom de l'élément | Requis ? | Description |
| --- | --- | --- |
| $schema |Non |Emplacement du fichier de schéma JSON hello qui vous aide à tester la validité hello hello du fichier de définition. |
| title |Oui |Nom de l’artefact de hello affiché dans le laboratoire de hello. |
| description |Oui |Description de l’artefact de hello affiché dans le laboratoire de hello. |
| iconUri |Non |URI de l’icône de hello affichée dans le laboratoire de hello. |
| targetOsType |Oui |Système d’exploitation de hello où artefact est installée. Les options prises en charge sont : Windows et Linux. |
| parameters |Non |Les valeurs fournies lorsque la commande d'installation d'artefact est exécutée sur une machine. Cela permet de personnaliser votre artefact. |
| runCommand |Oui |Commande d'installation d'artefact qui est exécutée sur une machine virtuelle. |

### <a name="artifact-parameters"></a>Paramètres d'artefact
Dans la section Paramètres de hello hello du fichier de définition, vous spécifiez les valeurs d’un utilisateur peut entrer lors de l’installation d’un artefact. Vous pouvez consulter les valeurs de toothese dans la commande d’installation artefact hello.

Vous définissez des paramètres par hello suivant structure :

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Nom de l'élément | Requis ? | Description |
| --- | --- | --- |
| type |Oui |Type de la valeur du paramètre. Consultez hello suivant liste pour hello types autorisé : |
| displayName |Oui |Nom du paramètre hello utilisateur tooa affichées dans le laboratoire de hello. | |
| description |Oui |Description du paramètre hello qui s’affiche dans le laboratoire de hello. |

Hello types autorisés sont :

* string : n'importe quelle chaîne JSON valide
* int : n'importe quel entier JSON valide
* bool : n'importe quel booléen JSON valide 
* array : n'importe quel tableau JSON valide

## <a name="artifact-expressions-and-functions"></a>Expressions et fonctions d'artefact
Vous pouvez utiliser expression et d’artefact de fonctions tooconstruct hello la commande d’installation.
Les expressions sont placées entre crochets ([et]) et sont évaluées lors de l’artefact de hello est installé. Les expressions peuvent apparaître n'importe où dans une valeur de chaîne JSON et retournent toujours une autre valeur JSON. Si vous avez besoin d’une chaîne littérale qui commence par un crochet de toouse [, vous devez utiliser deux crochets [[.
En règle générale, vous utilisez des expressions avec les fonctions tooconstruct une valeur. Exactement comme dans JavaScript, les appels de fonctions sont mis en forme selon functionName(arg1,arg2,arg3).

Hello liste suivante présente les fonctions courantes :

* Parameters(parameterName) - renvoie une valeur de paramètre qui est fournie lors de l’exécution de commande d’artefact hello.
* concat(arg1,arg2,arg3,...) : combine plusieurs valeurs de chaîne. Cette fonction peut prendre n'importe quel nombre d'arguments.

Hello suivant montre l’exemple de comment toouse expression et fonctions tooconstruct une valeur :

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Création d'un artefact personnalisé
Créez votre artefact personnalisé en suivant les étapes ci-dessous :

1. Installer un éditeur JSON, vous avez besoin d’un toowork de l’éditeur JSON avec les fichiers de définition d’artefact. Nous vous recommandons d'utiliser [Visual Studio Code](https://code.visualstudio.com/), qui est disponible pour Windows, Linux et OS X.
2. Get un artifactfile.json exemple : extraction des artefacts de hello créé par l’équipe Azure DevTest Labs notre [référentiel GitHub](https://github.com/Azure/azure-devtestlab), où nous avons créé une bibliothèque riche d’artefacts qui vous aident à créent vos propres artefacts. Télécharger un fichier de définition d’artefact et apporter des modifications tooit toocreate vos propres artefacts.
3. Assurez-vous d’utiliser IntelliSense - éléments valides IntelliSense de tirer parti de la toosee qui peuvent être tooconstruct utilisé un fichier de définition d’artefact. Vous pouvez également voir hello différentes options pour les valeurs d’un élément. Par exemple, les afficher IntelliSense vous hello deux choix de Windows ou Linux lors de la modification hello **targetOsType** élément.
4. Artefact de hello magasin dans un [référentiel git](devtest-lab-add-artifact-repo.md).
   
   1. Créer un répertoire différent pour chaque artefact où nom de répertoire hello est même hello en tant que nom d’artefact hello.
   2. Stocker le fichier de définition d’artefact hello (artifactfile.json) dans le répertoire hello que vous avez créé.
   3. Commande d’installation scripts hello magasin qui sont référencés à partir de l’artefact de hello.
      
      Voici un exemple de dossier d'artefact :
      
      ![Exemple de dépôt git d'artefacts](./media/devtest-lab-artifact-author/git-repo.png)
5. Ajouter un laboratoire de hello artefacts référentiel toohello - consultez l’article toohello, [ajouter un référentiel Git des artefacts et des modèles](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Articles connexes
* [Comment les échecs d’artefact toodiagnose dans DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Joindre un domaine Active Directory à l’aide d’un modèle de gestionnaire de ressources dans Azure DevTest Labs de tooexisting machine virtuelle](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[ajouter un laboratoire de tooa référentiel Git artefact](devtest-lab-add-artifact-repo.md).

