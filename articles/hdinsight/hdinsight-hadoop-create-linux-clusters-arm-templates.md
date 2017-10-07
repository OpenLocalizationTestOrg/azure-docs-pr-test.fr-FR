---
title: "aaaCreate Hadoop clusters à l’aide de modèles - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate clusters pour HDInsight à l’aide de modèles de gestionnaire de ressources"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Créer des clusters Hadoop dans HDInsight avec des modèles Resource Manager
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Dans cet article, vous découvrez plusieurs façons toocreate Azure HDInsight clusters avec des modèles Azure Resource Manager. Pour plus d’informations, consultez la page [Déploiement d’une application avec un modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). toolearn sur d’autres outils de création de cluster et les fonctionnalités, cliquez sur le sélecteur de tabulations hello haut hello de cette page ou de voir [méthodes de création de Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

obtenir des instructions toofollow hello dans cet article, vous devez :

* Un [abonnement Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* L’interface de ligne de commande Azure ou Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Modèles Resource Manager
Un modèle de gestionnaire de ressources facilite hello toocreate facile pour votre application dans une opération unique de coordonnées :
* Clusters HDInsight et leurs ressources dépendantes (par exemple, le compte de stockage par défaut hello)
* Autres ressources (telles que la base de données SQL Azure toouse Apache Sqoop)

Dans le modèle de hello, vous définissez des ressources hello qui sont nécessaires pour l’application hello. Vous également spécifiez des valeurs de tooinput de paramètres de déploiement pour les différents environnements. modèle de Hello se compose de JSON et les expressions que vous utilisez des valeurs de tooconstruct pour votre déploiement.

Pour accéder à des exemples de modèles HDInsight, consultez la page [Modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight). Utilisez inter-plateformes [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) avec hello [extension du Gestionnaire de ressources](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou un modèle de hello texte éditeur toosave dans un fichier sur votre station de travail. Vous allez apprendre comment toocall hello modèle à l’aide de différentes méthodes.

Pour plus d’informations sur les modèles de gestionnaire de ressources, consultez hello suivant des articles :

* [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [Déployer une application avec des modèles Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Génération de modèles

À l’aide de hello portail Azure, vous pouvez configurer toutes les propriétés de hello d’un cluster et puis enregistrez le modèle de hello avant de le déployer. Vous pouvez réutiliser les modèles hello.

**toogenerate un modèle à l’aide de hello portail Azure**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **nouveau** sur menu gauche hello **Intelligence + analytique**, puis cliquez sur **HDInsight**.
3. Suivre les propriétés de tooenter instructions hello. Vous pouvez utiliser soit hello **création rapide** ou hello **personnalisé** option.
4. Sur hello **Résumé** , cliquez sur **télécharger le modèle et les paramètres**:

    ![Téléchargement de modèle Resource Manager pour la création de clusters Hadoop dans HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    Vous consultez une liste des fichiers de modèle hello, fichier de paramètres et le modèle de code échantillons utilisés toodeploy hello :

    ![Option de téléchargement de modèle Resource Manager pour la création de clusters Hadoop dans HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    À ce stade, vous pouvez télécharger le modèle de hello, enregistrer la bibliothèque de modèles tooyour ou déployer le modèle de hello.

    tooaccess un modèle dans votre bibliothèque, cliquez sur **davantage de services** dans le menu de gauche hello, puis cliquez sur **modèles** (sous hello **autres** catégorie).

    > [!Note]
    > fichier de modèle et les paramètres Hello doit être utilisé ensemble. Sinon, vous obtiendrez peut-être des résultats inattendus. Par exemple, hello par défaut **clusterKind** valeur de propriété est toujours **hadoop**, malgré ce que vous spécifiez avant de télécharger le modèle de hello.



## <a name="deploy-with-powershell"></a>Déployer avec PowerShell

Cette procédure crée un cluster Hadoop dans HDInsight.

1. Enregistrez le fichier JSON de hello Bonjour [annexe](#appx-a-arm-template) tooyour de station de travail. Bonjour script PowerShell, nom du fichier hello est `C:\HDITutorials-ARM\hdinsight-arm-template.json`.
2. Définir des variables et paramètres de hello si nécessaire.
3. Modèle de hello exécution à l’aide de hello PowerShell script suivant :

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    Hello script PowerShell configure uniquement le nom de cluster hello. nom de compte de stockage Hello est codé en dur dans le modèle de hello. Vous êtes invité à tooenter hello cluster mot de passe. (nom d’utilisateur par défaut de hello est **admin**.) Vous êtes également invité à tooenter hello SSH mot de passe. (le nom d’utilisateur SSH hello par défaut est **sshuser**.)  

Pour plus d’informations, consultez la rubrique [Déploiement avec PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).

## <a name="deploy-with-cli"></a>Déploiement avec la CLI
Hello suivant l’exemple utilise Azure interface de ligne de commande (CLI). Il appelle un modèle Resource Manager pour créer un cluster, son compte de stockage dépendant et son conteneur :

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

Vous êtes invité à tooenter :
* nom du cluster Hello.
* mot de passe utilisateur de cluster Hello. (nom d’utilisateur par défaut de hello est **admin**.)
* mot de passe utilisateur SSH Hello. (le nom d’utilisateur SSH hello par défaut est **sshuser**.)

Hello suivant le code fournit des paramètres inclus :

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>Déployer avec hello API REST
Consultez [déployer avec l’API REST de hello](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Déployer avec Visual Studio
 Utilisez Visual Studio toocreate un projet de groupe de ressources et de déploiement tooAzure via l’interface utilisateur hello. Vous sélectionnez le type hello de tooinclude de ressources dans votre projet. Ces ressources sont automatiquement ajoutés toohello Gestionnaire de ressources du modèle. projet de Hello fournit également un modèle de hello de toodeploy de script PowerShell.

Pour une introduction toousing Visual Studio avec des groupes de ressources, consultez [création et déploiement des groupes de ressources Azure via Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris plusieurs façons toocreate un cluster HDInsight. toolearn, voir hello suivant des articles :

* Pour obtenir un exemple de déploiement de ressources via la bibliothèque cliente .NET hello, consultez [déployer des ressources à l’aide de bibliothèques .NET et un modèle](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Pour obtenir un exemple détaillé de déploiement d’une application, consultez [Approvisionner et déployer des microservices de manière prévisible dans Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).
* Pour obtenir des conseils sur le déploiement de vos environnements toodifferent de solution, consultez [environnements de développement et de test dans Microsoft Azure](../solution-dev-test-environments.md).
* toolearn sur les sections hello du modèle du Gestionnaire de ressources Azure hello, consultez [création de modèles](../azure-resource-manager/resource-group-authoring-templates.md).
* Pour obtenir la liste des fonctions hello vous pouvez utiliser dans un modèle Azure Resource Manager, consultez [fonctions de modèle](../azure-resource-manager/resource-group-template-functions.md).

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>Annexe : Gestionnaire de ressources du modèle toocreate un cluster Hadoop
Hello modèle Azure Resource Manager suivant crée un cluster Hadoop basé sur Linux avec un compte de stockage Azure dépendants hello.

> [!NOTE]
> Cet exemple inclut des informations de configuration pour le metastore Hive et le metastore Oozie. Supprimer la section de hello ou configurer la section de hello avant d’utiliser le modèle de hello.
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>Annexe : Gestionnaire de ressources du modèle toocreate un cluster Spark

Cette section fournit un modèle de gestionnaire de ressources que vous pouvez utiliser toocreate un cluster HDInsight Spark. Ce modèle inclut les configurations pour `spark-defaults` et `spark-thrift-sparkconf` (pour les clusters Spark 1.6) et `spark2-defaults` et `spark2-thrift-sparkconf` (pour les clusters Spark 2). En outre toothis, HDInsight calcule et définit des configurations telles que `spark.executor.instances`, `spark.executor.memory`, et `spark.executor.cores` selon la taille de cluster hello. 

Si vous définissez un paramètre dans une section en tant que partie du modèle hello lui-même, HDInsight ne calculer et définir des autres paramètres de hello hello même section. Par exemple, le paramètre `spark.executor.instances` est Bonjour `spark-defaults` configuration. Si vous définissez un autre paramètre (par exemple, `spark.yarn.exector.memoryOverhead`) Bonjour `spark-defaults` configuration, HDInsight ne pas calculer et définir hello `spark.executor.instances` également le paramètre.

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
