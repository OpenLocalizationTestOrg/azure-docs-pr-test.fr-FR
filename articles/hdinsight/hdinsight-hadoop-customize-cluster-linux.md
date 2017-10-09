---
title: "aaaCustomize des clusters HDInsight à l’aide des actions de script - Azure | Documents Microsoft"
description: "Ajouter des composants personnalisés en fonction de tooLinux de HDInsight des clusters à l’aide des Actions de Script. Actions de script sont des scripts Bash qui peuvent être la configuration de cluster utilisé toocustomize hello ou ajouter des services supplémentaires et des utilitaires de teinte, de Solr ou R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Personnalisation de clusters HDInsight basés sur Linux à l'aide d'une action de script

HDInsight fournit une option de configuration appelée **Action de Script** qui appelle des scripts personnalisés qui personnalisent le cluster de hello. Ces scripts sont utilisé tooinstall des composants supplémentaires et modifier les paramètres de configuration. Les actions de script peuvent être utilisées pendant ou après la création du cluster.

> [!IMPORTANT]
> actions de script toouse Hello capacité sur un cluster déjà en cours d’exécution est uniquement disponible pour les clusters HDInsight de basés sur Linux.
>
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Actions de script peuvent également être publiée toohello Azure Marketplace en tant qu’une application HDInsight. Certains des exemples hello dans ce document montrent comment vous pouvez installer une application de HDInsight à l’aide des commandes d’action de script à partir de PowerShell et hello du SDK .NET. Pour plus d’informations sur les applications de HDInsight, consultez [HDInsight de publier des applications dans Azure Marketplace de hello](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Autorisations

Si vous utilisez un cluster HDInsight à un domaine, il existe deux autorisations Ambari qui sont requises lors de l’utilisation des actions de script avec le cluster de hello :

* **AMBARI. Exécutez\_personnalisé\_commande**: rôle d’administrateur de Ambari hello possède cette autorisation par défaut.
* **METTRE EN CLUSTER. Exécutez\_personnalisé\_commande**: les deux hello administrateur de Cluster HDInsight et Ambari administrateur ont cette autorisation par défaut.

Pour plus d’informations sur l’utilisation des autorisations avec un cluster HDInsight joint à un domaine, consultez [Gestion des clusters HDInsight joints à un domaine](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>Contrôle d’accès

Si vous n’êtes pas administrateur de hello/propriétaire de votre abonnement Azure, votre compte doit posséder au moins **collaborateur** groupe de ressources toohello accès qui contient le cluster HDInsight de hello.

En outre, si vous créez un cluster HDInsight, une personne disposant au moins **collaborateur** accès toohello abonnement Azure doit avoir inscrite précédemment fournisseur hello pour HDInsight. Inscription du fournisseur qui se produit quand un utilisateur avec un abonnement de collaborateur accès toohello crée une ressource pour hello première fois sur l’abonnement de hello. Vous pouvez également faire cela sans créer une ressource en [enregistrant un fournisseur à l’aide de REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Pour plus d’informations sur l’utilisation de la gestion de l’accès, consultez hello suivant des documents :

* [Prise en main Bonjour Azure portail de gestion de l’accès](../active-directory/role-based-access-control-what-is.md)
* [Utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Comprendre les actions de script

Une action de script est tout simplement un script Bash auquel vous apportez une URI et des paramètres. script de Hello s’exécute sur les nœuds de cluster de HDInsight hello. Hello Voici les caractéristiques et fonctionnalités des actions de script.

* Doit être stocké sur un URI qui est accessible à partir du cluster HDInsight de hello. Hello Voici les emplacements de stockage possibles :

    * Un **Azure Data Lake Store** compte qui est accessible par le cluster HDInsight de hello. Pour plus d’informations sur l’utilisation d'Azure Data Lake Store avec HDInsight, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Lorsque vous utilisez un script stocké dans Data Lake Store, le format d’URI hello est `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Hello service principal HDInsight utilise tooaccess Data Lake Store doit avoir accès en lecture toohello script.

    * Un objet blob dans un **compte de stockage Azure** qui est un compte de stockage primaire ou une autre de hello pour le cluster HDInsight de hello. HDInsight est accordé tooboth d’accès de ces types de comptes de stockage pendant la création du cluster.

    * Un service de partage de fichiers public, comme Azure Blob, GitHub, OneDrive, Dropbox, etc.

        Par exemple les URI, consultez hello [scripts d’action de script exemple](#example-script-action-scripts) section.

        > [!WARNING]
        > HDInsight prend uniquement en charge les comptes de stockage Azure à __usage général__. Il ne prend pas en charge hello __stockage d’objets Blob__ type de compte.

* Peut être restreinte trop**s’exécutent sur les seuls certains types de nœud**, pour les nœuds principaux d’un exemple ou les nœuds de travail.

  > [!NOTE]
  > Lorsqu’il est utilisé avec HDInsight Premium, vous pouvez spécifier que le script de hello doit être utilisé sur le nœud de périmètre hello.

* Son état peut être **persistant** ou **ad hoc**.

    **Persistante** scripts sont cluster de toohello ajouté nœuds tooworker appliqué après exécution du script hello. Par exemple, lors de la mise à l’échelle d’un cluster de hello.

    Un script persistant peut également appliquer les modifications tooanother nœud type, tel qu’un nœud principal.

  > [!IMPORTANT]
  > Les actions de script persistantes doivent avoir un nom unique.

    Les scripts**Ad hoc** ne sont pas conservés. Ils ne sont pas cluster de toohello ajouté nœuds tooworker appliquées après l’exécution de script de hello. Par la suite, vous pouvez promouvoir un tooa script ad hoc persistant de script, ou rétrograder un script ad hoc tooan de script persistantes.

  > [!IMPORTANT]
  > Les actions de script utilisées lors de la création du cluster sont automatiquement rendues persistantes.
  >
  > Les scripts qui échouent ne sont pas rendus persistants, même si vous précisez qu’ils doivent l’être.

* Peut accepter **paramètres** qui sont utilisés par le script de hello lors de l’exécution.
* Exécuter avec **racine des privilèges de niveau** sur les nœuds de cluster hello.
* Peut être utilisé par le biais hello **portail Azure**, **Azure PowerShell**, **CLI d’Azure**, ou **HDInsight .NET SDK**

cluster de Hello conserve un historique de tous les scripts ont été exécutés. historique de Hello est utile lorsque vous avez besoin d’ID de hello toofind d’un script pour les opérations de promotion ou la rétrogradation.

> [!IMPORTANT]
> Il n’existe aucun tooundo de façon automatique hello les modifications apportées par une action de script. Hello annuler manuellement ou fournir un script qui les inverse.


### <a name="script-action-in-hello-cluster-creation-process"></a>Action de script dans le processus de création de cluster hello

Les actions de script utilisées lors de la création du cluster sont légèrement différentes des actions de script exécutées sur un cluster existant :

* script de Hello est **automatiquement persistantes**.
* A **échec** Bonjour script peut entraîner des toofail de processus de création de cluster hello.

Hello diagramme ci-dessous illustre lors de l’Action de Script est exécutée pendant le processus de création de hello :

![Personnalisation du cluster HDInsight et procédure de création d’un cluster][img-hdi-cluster-states]

script de Hello s’exécute pendant la configuration de HDInsight est en cours. À ce stade, hello s’exécute le script en parallèle sur tous les hello nœuds spécifiés dans le cluster de hello et s’exécute avec des privilèges racine sur les nœuds hello.

> [!NOTE]
> Étant donné que le script de hello s’exécute avec des privilèges de niveau racine sur les nœuds de cluster hello, vous pouvez effectuer des opérations telles que l’arrêt et démarrage des services, y compris les services liés à Hadoop. Si vous arrêtez les services, vous devez vous assurer que service de Ambari hello et autres services Hadoop sont en cours d’exécution avant la fin de script de hello en cours d’exécution. Ces services sont requis toosuccessfully déterminer l’intégrité de hello et l’état du cluster de hello lors de sa création.


Lors de la création du cluster, vous pouvez utiliser plusieurs actions de script à la fois. Ces scripts sont appelés dans l’ordre de hello dans lequel elles ont été spécifiées.

> [!IMPORTANT]
> Les actions de script doivent se terminer dans les 60 minutes, faute de quoi elles expirent. Lors de la configuration de cluster, script de hello s’exécute en même temps que d’autres processus d’installation et la configuration. Concurrence pour les ressources, telles que la bande passante du réseau ou de temps processeur peut entraîner hello script tootake plu toofinish qu’il ne le fait dans votre environnement de développement.
>
> toominimize hello fois qu’il prend toorun hello script, évitez de tâches, telles que le téléchargement et la compilation d’applications à partir de la source. Précompiler des applications et stocker les binaires hello dans le stockage Azure.


### <a name="script-action-on-a-running-cluster"></a>Action de script sur un cluster en cours d’exécution

Contrairement aux actions utilisées lors de la création du cluster, une défaillance dans un script exécutées sur un cluster déjà en cours d’exécution de script ne provoque pas automatiquement l’état hello cluster toochange tooa a échoué. Une fois qu’un script s’achève, cluster de hello doit retourner tooa « running » l’état.

> [!IMPORTANT]
> Même si le cluster de hello a un état « en cours d’exécution », hello script ayant échoué peut-être rompu choses. Par exemple, un script peut supprimer les fichiers requis par le cluster de hello.
>
> Les actions de scripts s’exécutent avec des privilèges racine, donc vous devez vous assurer que vous comprenez ce que fait par un script avant de l’appliquer tooyour cluster.

Lorsque vous appliquez un cluster tooa de script, état du cluster hello change toofrom **en cours d’exécution** trop**accepté**, puis **configuration HDInsight**et enfin trop**En cours d’exécution** pour les scripts réussies. statut du script Hello est enregistré dans l’historique des actions de script hello, et vous pouvez utiliser cette toodetermine informations si le script de hello a réussi ou échoué. Par exemple, hello `Get-AzureRmHDInsightScriptActionHistory` applet de commande PowerShell peut être l’état de hello tooview utilisé d’un script. Il retourne toohello similaire à informations suivant le texte :

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Si vous avez modifié le mot de passe utilisateur (admin) hello cluster après la création de cluster de hello, actions exécutées sur ce cluster peut échouer. Si vous disposez de toutes les actions de script persistantes que de nœuds de travail cible, ces scripts peuvent échouer lorsque vous mettez à l’échelle de cluster de hello.

## <a name="example-script-action-scripts"></a>Exemple de script d’action de script

Scripts d’Action de script peuvent être utilisés par le biais hello suivant utilitaires :

* Portail Azure
* Azure PowerShell
* Interface de ligne de commande Azure
* Kit de développement logiciel (SDK) .NET de HDInsight

HDInsight fournit hello tooinstall de scripts suivant des composants de clusters HDInsight :

| Nom | Script |
| --- | --- |
| **Ajouter un compte Azure Storage** |https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Consultez [ajouter un stockage supplémentaire tooan HDInsight cluster](hdinsight-hadoop-add-storage.md). |
| **Installez Hue.** |https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Consultez [Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md). |
| **Installer Presto** |https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Consultez la rubrique [Installer et utiliser Presto sur des clusters HDInsight](hdinsight-hadoop-install-presto.md). |
| **Installation de Solr** |https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Consultez [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install-linux.md). |
| **Installation de Giraph** |https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Consultez [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). |
| **Précharger les bibliothèques Hive** |https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Consultez [Ajouter des bibliothèques Hive sur des clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md). |
| **Installer ou mettre à jour Mono** | https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash. Consultez [Installer ou mettre à jour Mono sur HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Utiliser une action de script lors de la création du cluster

Cette section fournit des exemples sur hello différentes utilisations des actions de script lors de la création d’un cluster HDInsight.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Utiliser une Action de Script lors de la création du cluster à partir de hello portail Azure

1. Démarrez la création d'un cluster comme décrit dans [Création de clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Arrêtez quand vous atteignez hello __résumé du Cluster__ section.

2. À partir de hello __résumé du Cluster__ section, sélectionnez hello __modifier__ de liens pour __paramètres avancés__.

    ![Lien des Paramètres avancés](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. À partir de hello __paramètres avancés__ section, sélectionnez __actions de Script__. À partir de hello __actions de Script__ section, sélectionnez __+ soumettre à nouveau__

    ![Soumettre une nouvelle action de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Hello d’utilisation __sélectionner un script__ entrée tooselect un script existant. toouse un script personnalisé, sélectionnez __personnalisé__ , puis indiquez hello __nom__ et __Bash URI de script__ pour votre script.

    ![Ajouter un script hello sélectionnez sous forme de script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Hello tableau suivant décrit les éléments de hello sur le formulaire de hello :

    | Propriété | Valeur |
    | --- | --- |
    | Sélectionner un script | toouse votre propre script, sélectionnez __personnalisé__. Sinon, sélectionnez un des scripts de hello fourni. |
    | Nom |Spécifiez un nom pour l’action de script hello. |
    | URI de script bash |Spécifiez hello URI toohello script qui est appelée toocustomize hello cluster. |
    | Principal/Employé/Zookeeper |Spécifier les nœuds hello (**Head**, **travail**, ou **soigneur**) sur la personnalisation hello script est exécuté. |
    | Paramètres |Spécifiez des paramètres de hello, si requis par le script de hello. |

    Hello d’utilisation __conserver cette action de script__ tooensure d’entrée qui hello script est appliqué pendant les opérations de mise à l’échelle.

5. Sélectionnez __créer__ script de hello toosave. Vous pouvez ensuite utiliser __+ soumettre de nouvelles__ tooadd un autre script.

    ![Plusieurs actions de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Lorsque vous avez terminé l’ajout de scripts, utilisez hello __sélectionnez__ bouton et puis hello __suivant__ bouton tooreturn toohello __résumé du Cluster__ section.

3. cluster de hello toocreate, sélectionnez __créer__ de hello __résumé du Cluster__ sélection.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Utilisez une action de Script à partir de modèles Azure Resource Manager

exemples de Hello dans cette section montrent comment toouse script actions avec les modèles Azure Resource Manager.

#### <a name="before-you-begin"></a>Avant de commencer

* Pour plus d’informations sur la configuration d’une station de travail de toorun applets de commande HDInsight Powershell, consultez [installer et configurer Azure PowerShell](/powershell/azure/overview).
* Pour obtenir des instructions sur la façon de toocreate modèles, consultez [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Si vous n’avez pas déjà utilisé Azure PowerShell avec Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Création de clusters à l’aide d’une action de script

1. Copiez hello suivant l’emplacement du modèle tooa sur votre ordinateur. Ce modèle installe Giraph sur les nœuds de hello headnodes et de travail dans un cluster de hello. Vous pouvez également vérifier si le modèle de hello JSON est valide. Collez le contenu de votre modèle dans [JSONLint](http://jsonlint.com/), un outil de validation JSON en ligne.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Démarrer PowerShell d’Azure et connectez-vous tooyour compte Azure. Après avoir entré vos informations d’identification, commande hello retourne des informations relatives à votre compte.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Si vous avez plusieurs abonnements, indiquez l’ID d’abonnement hello vous souhaitez toouse pour le déploiement.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > Vous pouvez utiliser `Get-AzureRmSubscription` tooget une liste de tous les abonnements associés à votre compte, ce qui inclut l’ID d’abonnement hello pour chacun d’eux.

4. Si vous n’avez pas de groupe de ressources, créez-en un. Fournir le nom hello du groupe de ressources hello et l’emplacement que vous avez besoin pour votre solution. Un résumé du nouveau groupe de ressources hello est retourné.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. toocreate de déploiement de votre groupe de ressources, exécutez hello **New-AzureRmResourceGroupDeployment** de commandes et de fournir les paramètres nécessaires hello. les paramètres de Hello incluent hello données suivantes :

    * un nom pour votre déploiement ;
    * nom de Hello de votre groupe de ressources
    * chemin d’accès Hello ou modèle d’URL toohello que vous avez créé.

  Si votre modèle requiert n’importe quel paramètre, vous devez également transférer les paramètres. Dans ce cas, hello script action tooinstall R sur le cluster de hello ne nécessite pas de paramètres de.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    Vous n’êtes tooprovide invité à des valeurs pour les paramètres de hello définis dans le modèle de hello.

1. Lorsque le groupe de ressources hello a été déployé, un résumé du déploiement de hello s’affiche.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Si votre déploiement échoue, vous pouvez utiliser hello suivant d’applets de commande tooget plus d’informations sur les échecs de hello.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Utiliser une action de script lors de la création du cluster à partir d’Azure PowerShell

Dans cette section, nous utilisons hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) scripts de tooinvoke d’applet de commande en utilisant l’Action de Script toocustomize un cluster. Avant de poursuivre, assurez-vous que vous avez installé et configuré Azure PowerShell. Pour plus d’informations sur la configuration d’une station de travail de toorun applets de commande HDInsight PowerShell, consultez [installer et configurer Azure PowerShell](/powershell/azure/overview).

Hello de script suivant montre comment tooapply une action de script lors de la création d’un cluster à l’aide de PowerShell :

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Il peut prendre plusieurs minutes avant que le cluster de hello est créé.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Utiliser une Action de Script lors de la création du cluster à partir de hello HDInsight .NET SDK

Hello HDInsight .NET SDK fournit des bibliothèques clientes qui rend plus facile toowork avec HDInsight à partir d’une application .NET. Pour un exemple de code, consultez [basés sur Linux de créer des clusters HDInsight à l’aide hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Appliquer un tooa d’Action de Script en cours d’exécution cluster

Dans cette section, découvrez comment tooapply script tooa actions cluster en cours d’exécution.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Appliquer un tooa d’Action de Script en cours d’exécution cluster à partir de hello portail Azure

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight.

2. Dans la vue d’ensemble du cluster HDInsight hello, sélectionnez hello **Actions de Script** vignette.

    ![Vignette Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Vous pouvez également sélectionner **tous les paramètres** , puis sélectionnez **Actions de Script** de hello section de paramètres.

3. À partir du haut hello Hello section Actions de Script, sélectionnez **envoyer nouveau**.

    ![Ajouter un tooa script cluster en cours d’exécution](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Hello d’utilisation __sélectionner un script__ entrée tooselect un script existant. toouse un script personnalisé, sélectionnez __personnalisé__ , puis indiquez hello __nom__ et __Bash URI de script__ pour votre script.

    ![Ajouter un script hello sélectionnez sous forme de script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Hello tableau suivant décrit les éléments de hello sur le formulaire de hello :

    | Propriété | Valeur |
    | --- | --- |
    | Sélectionner un script | toouse votre propre script, sélectionnez __personnalisé__. Sinon, sélectionnez un script fourni. |
    | Nom |Spécifiez un nom pour l’action de script hello. |
    | URI de script bash |Spécifiez hello URI toohello script qui est appelée toocustomize hello cluster. |
    | Principal/Employé/Zookeeper |Spécifier les nœuds hello (**Head**, **travail**, ou **soigneur**) sur la personnalisation hello script est exécuté. |
    | Paramètres |Spécifiez des paramètres de hello, si requis par le script de hello. |

    Hello d’utilisation __conserver cette action de script__ script d’entrée toomake vraiment hello est appliqué pendant les opérations de mise à l’échelle.

5. Enfin, utilisez hello **créer** le cluster toohello script bouton tooapply hello.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Appliquer un tooa d’Action de Script en cours d’exécution cluster à partir d’Azure PowerShell

Avant de poursuivre, assurez-vous que vous avez installé et configuré Azure PowerShell. Pour plus d’informations sur la configuration d’une station de travail de toorun applets de commande HDInsight PowerShell, consultez [installer et configurer Azure PowerShell](/powershell/azure/overview).

Hello exemple suivant montre comment tooapply un cluster en cours d’exécution de script action tooa :

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Une fois que hello terminée, vous recevez toohello similaire à informations suivant le texte :

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Appliquer un tooa d’Action de Script en cours d’exécution cluster à partir de hello CLI d’Azure

Avant de continuer, assurez-vous que vous avez installé et configuré hello CLI d’Azure. Pour plus d’informations, consultez [installation Bonjour Azure CLI](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure mode du Gestionnaire de ressources, utilisez hello commande à la ligne de commande hello suivante :

        azure config mode arm

2. Utilisez hello suivant tooauthenticate tooyour abonnement Azure.

        azure login

3. Utilisez hello suivant commande tooapply un tooa d’action de script en cours d’exécution cluster

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Si vous omettez les paramètres de cette commande, vous êtes invité à les saisir. Si hello script que vous spécifiez avec `-u` accepte des paramètres, vous pouvez spécifier les à l’aide de hello `-p` paramètre.

    Les types de nœud valides sont `headnode`, `workernode` et `zookeeper`. Si le script de hello doit être appliqué toomultiple les types de nœuds, spécifiez les types de hello séparés par un ';'. Par exemple, `-n headnode;workernode`.

    toopersist hello script, ajoutez hello `--persistOnSuccess`. Vous pouvez également rendre persistantes les script hello ultérieurement à l’aide de `azure hdinsight script-action persisted set`.

    Une fois que hello est terminée, vous recevez toohello similaire de sortie suivant du texte :

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>Appliquer un tooa d’Action de Script en cours d’exécution à l’aide des API REST de cluster

Consultez [Exécuter des actions de script sur un cluster en cours d’exécution](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Appliquer un tooa d’Action de Script en cours d’exécution cluster à partir de hello HDInsight .NET SDK

Pour obtenir un exemple d’utilisation de cluster de tooa hello .NET SDK tooapply des scripts, consultez [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Afficher l’historique, promouvoir et abaisser des actions de script

### <a name="using-hello-azure-portal"></a>À l’aide de hello portail Azure

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight.

2. Dans la vue d’ensemble du cluster HDInsight hello, sélectionnez hello **Actions de Script** vignette.

    ![Vignette Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Vous pouvez également sélectionner **tous les paramètres** , puis sélectionnez **Actions de Script** de hello section de paramètres.

4. Un historique des scripts pour ce cluster s’affiche sur hello section Actions de Script. Ces informations comprennent une liste de scripts persistants. Dans la capture d’écran de hello ci-dessous, vous pouvez voir que hello Solr script a été exécuté sur ce cluster. capture d’écran de Hello n’affiche pas tous les scripts persistantes.

    ![Section Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. Sélection d’un script à partir de l’historique de hello affiche la section des propriétés hello pour ce script. À partir du haut hello d’écran hello, vous pouvez réexécuter le script de hello ou promouvoir en tant que.

    ![Propriétés des actions de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. Vous pouvez également utiliser hello **...**  toohello à droite des entrées sur les actions de tooperform section hello Actions de Script.

    ![Utilisation de … des actions de script](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Utilisation de Microsoft Azure PowerShell

| Utilisez les éléments suivants de hello... | trop... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Récupérer des informations sur les actions de script persistantes |
| Get-AzureRmHDInsightScriptActionHistory |Récupérer un historique de script actions appliquées toohello cluster ou les détails d’un script spécifique |
| Set-AzureRmHDInsightPersistedScriptAction |Promeut un ad hoc tooa d’action de script persistantes action de script |
| Remove-AzureRmHDInsightPersistedScriptAction |Rétrograde une action ad hoc de script persistantes action tooan |

> [!IMPORTANT]
> À l’aide de `Remove-AzureRmHDInsightPersistedScriptAction` n’annule pas les actions hello effectuées par un script. Cette applet de commande supprime uniquement l’indicateur de rendu persistant hello.

Hello, exemple de script suivant illustre l’utilisation de toopromote d’applets de commande hello, puis rétrograder un script.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>À l’aide de hello CLI d’Azure

| Utilisez les éléments suivants de hello... | trop... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Récupérer une liste des actions de script persistantes |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Récupérer des informations sur les actions de script persistantes |
| `azure hdinsight script-action history list <clustername>` |Récupérer un historique de script actions appliquées toohello cluster |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Récupérer des informations sur une action de script spécifique |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Promeut un ad hoc tooa d’action de script persistantes action de script |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Rétrograde une action ad hoc de script persistantes action tooan |

> [!IMPORTANT]
> À l’aide de `azure hdinsight script-action persisted delete` n’annule pas les actions hello effectuées par un script. Cette applet de commande supprime uniquement l’indicateur de rendu persistant hello.

### <a name="using-hello-hdinsight-net-sdk"></a>À l’aide de hello HDInsight .NET SDK

Pour obtenir un exemple d’utilisation de l’historique de script tooretrieve hello .NET SDK à partir d’un cluster, vous devez promouvoir ou rétrograder des scripts, consultez [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Cet exemple montre également comment une application de HDInsight à l’aide de tooinstall hello du SDK .NET.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Prise en charge des logiciels open source utilisés sur les clusters HDInsight

Hello service Microsoft Azure HDInsight utilise un écosystème de technologies open source sur Hadoop. Microsoft Azure fournit un niveau général de prise en charge pour les technologies open source. Pour plus d’informations, consultez hello **prise en charge étendue** section Hello [Azure prise en charge du site Web](https://azure.microsoft.com/support/faq/). Hello service HDInsight fournit un niveau supplémentaire de prise en charge pour les composants intégrés.

Il existe deux types de composants open source qui sont disponibles dans hello service HDInsight :

* **Les composants intégrés** -ces composants sont déjà installés sur les clusters HDInsight et fournir des fonctionnalités principales du cluster de hello. Par exemple, fils ResourceManager, langage de requête Hive hello (HiveQL) et la bibliothèque de Mahout hello appartiennent toothis catégorie. Une liste complète des composants de cluster est disponible dans [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight](hdinsight-component-versioning.md).
* **Les composants personnalisés** -vous, en tant qu’utilisateur de cluster de hello, pourrez installer ou utiliser dans votre charge de travail n’importe quel composant disponible dans la Communauté de hello ou créée par vous.

> [!WARNING]
> Composants fournis avec le cluster HDInsight de hello sont entièrement pris en charge. Support technique de Microsoft vous aide à tooisolate et résoudre les problèmes connexes toothese composants.
>
> Les composants personnalisés de réception efforcera toohelp vous toofurther hello de dépannage. Prise en charge Microsoft soit en mesure de tooresolve hello ou elles peuvent demander tooengage les canaux disponibles pour les technologies open source hello où se trouve une grande expérience pour laquelle la technologie. Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).

Hello service HDInsight propose plusieurs manières toouse des composants personnalisés. Bonjour s’applique même au niveau de prise en charge, quelle que soit la façon dont un composant est utilisé ou installé sur le cluster de hello. Hello liste suivante décrit les méthodes les plus courantes hello que les composants personnalisés peuvent être utilisés sur les clusters HDInsight :

1. Envoi de travaux - Hadoop ou autres types de tâches qui s’exécutent, ou utilisent des composants personnalisés peut être soumis toohello cluster.

2. Personnalisation de cluster - lors de la création du cluster, vous pouvez spécifier des paramètres supplémentaires et des composants personnalisés qui sont installés sur les nœuds de cluster hello.

3. Exemples - pour les composants personnalisés populaires, Microsoft et d’autres peuvent fournir des exemples de la façon dont ces composants peuvent être utilisés sur des clusters HDInsight de hello. Ces exemples sont fournis sans support.

## <a name="troubleshooting"></a>Résolution des problèmes

Vous pouvez utiliser Ambari web UI tooview les informations enregistrées par les actions de script. Si le script de hello échoue pendant la création du cluster, hello journaux sont également disponibles dans le compte de stockage par défaut hello associé hello cluster. Cette section fournit des informations sur la façon dont tooretrieve hello connecte à l’aide de ces deux options.

### <a name="using-hello-ambari-web-ui"></a>À l’aide de hello Ambari Web UI

1. Dans votre navigateur, accédez à toohttps://CLUSTERNAME.azurehdinsight.net. Remplacez CLUSTERNAME par nom hello de votre cluster HDInsight.

    Lorsque vous y êtes invité, entrez le nom du compte administrateur hello (admin) et le mot de passe pour le cluster de hello. Vous pouvez avoir des informations d’identification d’administrateur de hello tooreenter dans un formulaire web.

2. Dans la barre de hello en hello haut hello, sélectionnez hello **ops** entrée. Une liste des opérations actuelles et précédentes effectuées sur le cluster de hello via Ambari s’affiche.

    ![Barre de l’interface utilisateur web Ambari avec ops sélectionné](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Rechercher des entrées hello ayant **exécuter\_customscriptaction** Bonjour **Operations** colonne. Ces entrées sont créées lorsque vous exécutez des Actions de Script hello.

    ![Capture d’écran des opérations](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    tooview hello STDOUT et la sortie STDERR, sélectionnez hello run\customscriptaction entrée et Explorer les liens de hello. Cette sortie est générée lorsque hello script s’exécute et peut contenir des informations utiles.

### <a name="access-logs-from-hello-default-storage-account"></a>Journaux d’accès de compte de stockage par défaut hello

Si la création du cluster hello échoue en raison de l’erreur de script d’action de tooa, hello journaux accessibles à partir du compte de stockage de cluster hello.

* Hello journaux de stockage sont disponibles dans `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Capture d’écran des opérations](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    Sous ce répertoire, les journaux de hello sont organisés séparément pour le nœud principal et les nœuds soigneur workernode. Voici quelques exemples :

    * **Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Nœud Worker** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Nœud Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Tous les stdout et stderr d’hôte correspondant de hello est téléchargés du compte de stockage toohello. Il existe un fichier **output-\*.txt** et un fichier **errors-\*.txt** pour chaque action de script. fichier de sortie-*.txt Hello contient des informations sur hello URI de script de hello qui a été exécuté sur l’ordinateur hôte de hello. Par exemple :

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Il est possible que vous créez un cluster d’action de script à plusieurs reprises avec hello même nom. Dans ce cas, vous pouvez distinguer les journaux appropriés hello basés sur le nom du dossier DATE hello. Par exemple, structure de dossiers de hello pour un cluster (mycluster) créé à des dates différentes apparaît similaire toohello suivant des entrées de journal :

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04``\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Si vous créez un cluster d’action de script avec hello même nom sur hello même jour, vous pouvez utiliser des fichiers journaux pertinents de hello préfixe unique tooidentify hello.

* Si vous créez un cluster près de 12:00 (minuit), il est possible que les fichiers journaux hello s’étendre sur deux jours. Dans ce cas, vous voyez deux dossiers de date différents pour hello même cluster.

* Conteneur par défaut de téléchargement journal fichiers toohello peut prendre jusqu'à minutes too5, en particulier pour les clusters de grande taille. Par conséquent, si vous souhaitez que les journaux tooaccess hello, vous ne devez pas immédiatement supprimer hello cluster si une action de script échoue.

### <a name="ambari-watchdog"></a>Agent de surveillance Ambari

> [!WARNING]
> Ne modifiez pas le mot de passe hello hello Ambari surveillance (hdinsightwatchdog) sur votre cluster HDInsight de basés sur Linux. Un mot de passe de modification hello pour ce compte interrompt les actions de script nouveau hello capacité toorun sur cluster HDInsight de hello.

### <a name="cant-import-name-blobservice"></a>Impossible d’importer le nom BlobService

__Symptômes__: hello action de script échoue. Texte similaire toohello est l’erreur suivante s’affiche lorsque vous affichez les opération hello dans Ambari :

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Cause__: cette erreur se produit si vous mettez à niveau le client de stockage Azure de Python hello qui est inclus dans le cluster HDInsight de hello. HDInsight attend le client de stockage Azure 0.20.0.

__Résolution__: tooresolve cette erreur, vous connecter manuellement à l’aide de nœud de cluster tooeach `ssh` et utilisez hello suivant la version du client de stockage correct commande tooreinstall hello :

```
sudo pip install azure-storage==0.20.0
```

Pour plus d’informations sur la connexion de cluster toohello avec SSH, consultez [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>L’historique n’affiche pas les scripts utilisés lors de la création du cluster

Si votre cluster a été créé avant le 15 mars 2016, une entrée pourrait ne pas s’afficher dans l’historique des actions de script. Si vous redimensionnez un cluster de hello après le 15 mars 2016, les scripts hello à l’aide lors de la création de cluster s’affiche dans l’historique lorsqu’ils sont appliqués toonew des nœuds dans le cluster hello dans le cadre de hello redimensionnement l’opération.

Deux exceptions :

* Si votre cluster a été créé avant le 1er septembre 2015. Il s’agit de la date à laquelle les actions de script ont été introduites. Tout cluster créé avant cette date n’aurait pas pu utiliser les actions de script pour la création du cluster.

* Si vous avez utilisé plusieurs Actions de Script lors de la création du cluster et utilisé hello même nom pour plusieurs scripts ou hello même nom, même URI, mais des paramètres différents pour plusieurs scripts. Dans ce cas, vous recevez hello l’erreur suivante :

    Aucun nouveau script, les actions peuvent être n’exécutés sur ce cluster en raison de noms de script tooconflicting dans les scripts existants. Les noms de script fournis au moment de la création du cluster doivent être uniques. Les scripts existants sont exécutés lors du redimensionnement.

## <a name="next-steps"></a>Étapes suivantes

* [Développer des scripts d’action de script pour HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Ajouter un cluster de stockage supplémentaire tooan HDInsight](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Procédure de création d’un cluster"
