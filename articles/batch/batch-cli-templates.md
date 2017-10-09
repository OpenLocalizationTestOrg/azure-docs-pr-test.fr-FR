---
title: "aaaRun Azure Batch travaux de bout en bout sans écrire de code (version préliminaire) | Documents Microsoft"
description: "Créer des fichiers de modèles pour les pools de lot toocreate hello CLI d’Azure, des tâches et des tâches."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Utiliser des modèles d’interface CLI Azure Batch et le transfert de fichiers (préversion)

À l’aide de hello CLI d’Azure il s’agit des traitements toorun possible sans écrire de code.

Fichiers de modèle peuvent être créés et utilisés avec hello CLI d’Azure qui permettent de lot pools, de tâches toobe tâches créé. Fichiers d’entrée de travail peuvent être facilement transférées au compte de stockage hello associé hello lot compte et le travail de fichiers de sortie téléchargés.

## <a name="overview"></a>Vue d'ensemble

Une extension de toohello CLI d’Azure permet de lot toobe utilisée de bout en bout par les utilisateurs qui ne sont pas des développeurs. Un pool peut être créé et téléchargement de données d’entrée, tâches et les tâches associées créés, hello sortie données résultantes téléchargées – aucun code requis, hello CLI utilisée directement ou intégrées dans les scripts.

Générer des modèles de traitement par lots sur hello [prise en charge de traitement par lots existante Bonjour Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) qui permet de fichiers JSON toospecify les valeurs de propriété pour la création de hello de pools, travaux, tâches et autres éléments. Avec les modèles de lot, hello fonctionnalités suivantes sont ajoutées sur ce qui est possible avec les fichiers au format JSON hello :

-   Des paramètres peuvent être définis. Lorsque le modèle de hello est utilisé, seules les valeurs de paramètre hello sont des éléments de hello de toocreate spécifié, avec d’autres valeurs de propriété d’élément spécifiée dans le corps du modèle hello. Un utilisateur qui comprend le traitement par lots et l’applications toobe exécutent par lot peut créer des modèles, en spécifiant le pool de travail et les valeurs de propriété de tâche. Un utilisateur moins familiarisés avec le lot et/ou les applications doit uniquement les valeurs hello toospecify pour les paramètres de hello défini.

-   Fabriques de tâches de travail en créer un ou plusieurs tâches associées à un travail, ce qui évite de hello ont besoin pour de nombreux toobe de définitions de tâche créé et ce qui simplifie considérablement la soumission de travaux.


Les fichiers de données d’entrée doivent toobe fourni pour les travaux et entraînait souvent des fichiers de données de sortie. Un compte de stockage est associé, par défaut, chaque lot compte et les fichiers peuvent être facilement transféré tooand à partir de ce compte de stockage à l’aide de l’interface CLI, sans codage, et aucune information d’identification de stockage ne requis.

Par exemple, [ffmpeg](http://ffmpeg.org/) est une application courante qui traite les fichiers audio et vidéo. Hello CLI de traitement par lots Azure peut être utilisé tooinvoke ffmpeg tootranscode source des fichiers vidéo toodifferent résolutions.

-   Un modèle de pool est créé. utilisateur Hello création hello modèle sait comment toocall hello ffmpeg application et ses besoins ; ils spécifient hello système d’exploitation approprié, la machine virtuelle de taille, comment ffmpeg est installée (à partir d’un package d’application ou à l’aide d’un gestionnaire de package, par exemple) et d’autres valeurs de propriété du pool. Paramètres sont créés lorsque le modèle de hello est utilisé, seuls les id du pool hello et nombre d’ordinateurs virtuels devez toobe spécifié.

-   Un modèle de travail est créé. le modèle de hello création Hello utilisateur sait comment ffmpeg besoins toobe appelé autre résolution tootranscode source vidéo tooa et spécifie la ligne de commande de tâche hello ; ils savent également qu’il existe un dossier contenant des fichiers vidéo source de hello, avec une tâche requise par le fichier d’entrée.

-   Un utilisateur final avec un ensemble de fichiers vidéo tootranscode crée d’abord un pool à l’aide du modèle de pool hello, en spécifiant uniquement id de pool hello et le nombre d’ordinateurs virtuels requis. Ils peuvent ensuite télécharger tootranscode de fichiers source hello. Un travail peut ensuite être envoyé à l’aide du modèle de projet hello, en spécifiant uniquement l’id de pool hello et emplacement des fichiers de source de hello téléchargés. traitement par lots Hello est créé, avec une tâche par le fichier d’entrée qui est généré. Enfin, les fichiers de sortie hello transcodé peuvent être téléchargement.

## <a name="installation"></a>Installation

fonctionnalités de transfert de modèle et de fichier Hello nécessitent un toobe extension installée.

Pour obtenir des instructions sur tooinstall hello CLI d’Azure voir [installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

Une fois hello que CLI d’Azure a été installé, hello lot extension peut être installée à l’aide de la commande CLI suivante :

```azurecli
az component update --add batch-extensions --allow-third-party
```

Pour plus d’informations sur l’extension de traitement par lots de hello, consultez [Microsoft Azure Batch CLI Extensions pour Windows, Mac et Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).

## <a name="templates"></a>Modèles

Hello CLI d’Azure Batch autorise des éléments tels que les pools, toobe de tâches créée en spécifiant un fichier JSON qui contient les noms de propriété et les valeurs de tâches. Par exemple :

```azurecli
az batch pool create –-json-file AppPool.json
```

Modèles de traitement par lots Azure sont des modèles de gestionnaire de ressources tooAzure similaires, dans la syntaxe et des fonctionnalités. Ils sont des fichiers JSON qui contiennent des valeurs et les noms de propriété d’élément, mais ajouter hello suivant des principaux concepts :

-   **Paramètres**

    -   Autoriser toobe de valeurs de propriété spécifié dans une section de corps, avec uniquement les valeurs de paramètre nécessitant toobe fourni lorsque le modèle de hello est utilisé. Par exemple, définition complète de hello pour un pool peut être placée dans le corps de hello et qu’un seul paramètre défini pour l’id du pool ; uniquement une chaîne d’id pool doit par conséquent toobe fourni toocreate un pool.
        
    -   corps de modèle Hello peuvent être créés par une personne disposant de connaissances du lot et hello applications toobe exécutée par le traitement par lots ; Seules les valeurs des paramètres définis par l’auteur de hello doivent être fournis lorsque le modèle de hello est utilisé. Un utilisateur sans hello lot détaillée et/ou des connaissances de l’application peut par conséquent utiliser les modèles.

-   **Variables**

    -   Autoriser toobe de valeurs de paramètre simple ou complexe spécifié dans un seul emplacement et utilisé dans un ou plusieurs emplacements dans le corps du modèle hello. Les variables peuvent simplifier et réduire la taille de hello du modèle de hello, ainsi rendre plus facile à gérer en ayant en un emplacement toochange propriétés dont la valeur peut changer.

-   **Constructions de niveau supérieur**

    -   Certaines constructions de niveau supérieur sont disponibles dans le modèle hello qui ne sont pas encore disponibles dans hello API de lot. Par exemple, une fabrique de tâches peut être définie dans un modèle de tâche qui crée plusieurs tâches pour la tâche hello à l’aide d’une définition de tâche commune. Ces constructions éviter toocode besoin de hello pour dynamiquement créer plusieurs fichiers JSON, telle qu’un fichier par la tâche, ainsi que de créer de script fichiers tooinstall applications via un gestionnaire de package, par exemple.

    -   À un point, si applicable, que ces constructions peuvent être ajoutées toothe lot service et disponible dans hello API de lot, les interfaces utilisateur, etc..

### <a name="pool-templates"></a>Modèles de pool

En outre, toohello des fonctions de modèle standard des paramètres et des variables, hello suivant des structures de niveau supérieur sont pris en charge par le modèle de pool hello :

-   **Références de package**

    -   Si vous le souhaitez permet aux logiciels toobe copié toopool nœuds à l’aide du package gestionnaires. Gestionnaire de package Hello et id de package sont spécifiés. Qui est en mesure de toodeclare un ou plusieurs packages évite hello besoin toocreate un script qui obtient les packages de hello requis, hello script d’installation et exécuter le script de hello sur chaque nœud du pool.

Hello Voici un exemple d’un modèle qui crée un pool de machines virtuelles Linux avec ffmpeg installé et que seul nécessite un pool id chaîne hello nombre et de machines virtuelles toobe fourni toouse :

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

Si le fichier de modèle hello était nommé _ffmpeg.json-pool_, puis le modèle de hello serait appelé comme suit :

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>Modèles de travail

En outre, toohello des fonctions de modèle standard des paramètres et des variables, hello suivant des structures de niveau supérieur sont pris en charge par le modèle de tâche hello :

-   **Fabrique de tâches**

    -   Crée plusieurs tâches pour un travail à partir d’une définition de tâche. Trois types de fabrique de tâches sont pris en charge : balayage paramétrique, tâche par fichier et collection de tâches.

Hello Voici un exemple d’un modèle qui crée une tâche qui utilise ffmpeg pour transcoder tooone de fichiers vidéo MP4 de deux résolutions inférieures, avec une tâche créée par le fichier vidéo source :

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

Si le fichier de modèle hello était nommé _ffmpeg.json de travail_, puis le modèle de hello serait appelé comme suit :

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>Groupes de fichiers et transfert de fichiers

La plupart des travaux et des tâches requièrent les fichiers d’entrée et produisent des fichiers de sortie. Les deux fichiers d’entrée et les fichiers de sortie est généralement nécessaire toobe transféré, à partir du nœud de toohello hello client ou à partir du client de toohello nœud hello. Hello extension d’Azure Batch CLI s’approprie le transfert de fichiers absent et utilise le compte de stockage hello est créé par défaut pour chaque compte de traitement par lots.

Un groupe de fichiers équivaut tooa conteneur qui est créé dans hello compte de stockage Azure. groupe de fichiers Hello peut comporter des sous-dossiers.

Hello, extension de traitement par lots CLI fournit des commandes pour le téléchargement de fichiers à partir du groupe de fichiers spécifié tooa client et télécharger des fichiers à partir du client de tooa groupe hello fichier spécifié.

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

Modèles de pool et de travail permettent de fichiers stockés dans toobe de groupes de fichiers spécifié pour la copie sur les nœuds de pool ou hors pool nœuds sauvegarder le groupe de fichiers tooa. Par exemple, dans le modèle de projet spécifié précédemment, hello fichier groupe « ffmpeg-entrée » n’est spécifiée pour la fabrique de tâches hello en tant qu’emplacement hello des fichiers vidéo de hello source copiés vers le bas sur le nœud hello pour le transcodage ; groupe « ffmpeg-sortie de Hello fichier » est utilisé comme emplacement des fichiers de sortie hello transcodé hello copiés nœud de hello toofrom chaque tâche en cours d’exécution.

## <a name="summary"></a>Résumé

Prise en charge du transfert modèle et de fichier actuellement ajoutés uniquement toohello CLI d’Azure. Hello vise audience hello tooexpand qui permet de toousers de lot qui n’ont pas besoin de code toodevelop à l’aide de hello API de lot, tels que les chercheurs, les utilisateurs et ainsi de suite. Sans effectuer de codage, les utilisateurs possédant des connaissances de Azure, lot et toobe d’applications hello exécutée par traitement peuvent créer des modèles pour la création de pool et de travail. Paramètres de modèle, les utilisateurs sans une connaissance détaillée de lot et hello applications peuvent utiliser les modèles de hello.

Tester hello extension de traitement par lots pour hello CLI d’Azure et nous fournir des commentaires ou des suggestions, soit hello dans les commentaires pour cet article ou via hello [forum d’Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).

## <a name="next-steps"></a>Étapes suivantes

- Voir hello lot modèles blog : [des travaux en cours d’exécution de traitement par lots Azure à l’aide de hello CLI d’Azure – aucun code requis](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).
- Code source, des exemples et documentation d’installation et d’utilisation détaillée sont disponibles dans hello [référentiel GitHub de Azure](https://github.com/Azure/azure-batch-cli-extensions).
