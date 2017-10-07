---
title: "les comptes de stockage Azure supplémentaires d’aaaAdd tooHDInsight | Documents Microsoft"
description: "Découvrez comment le stockage Azure supplémentaires tooadd comptes tooan les cluster HDInsight existant."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a>Ajouter tooHDInsight des comptes de stockage supplémentaire

Découvrez comment toouse script actions tooadd supplémentaires le stockage Azure comptes tooHDInsight. Hello étapes de ce document ajoutent un cluster HDInsight de basés sur Linux stockage compte tooan existant.

> [!IMPORTANT]
> informations Hello dans ce document sont sur l’ajout de cluster de stockage supplémentaire tooa après que qu’elle a été créée. Pour plus d’informations sur l’ajout de comptes de stockage lors de la création du cluster, voir [Configurer des clusters dans HDInsight avec Hadoop, Spark, Kafka, etc](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="how-it-works"></a>Fonctionnement

Ce script accepte hello paramètres suivants :

* __Nom de compte de stockage Azure__: nom hello du cluster HDInsight de hello stockage compte tooadd toohello. Après avoir exécuté le script de hello, HDInsight peut lire et écrire les données stockées dans ce compte de stockage.

* __Clé de compte de stockage Azure__: une clé qui accorde l’accès toohello de stockage Azure.

* __p -__ (facultatif) : si spécifié, la clé de hello n’est pas chiffré et est stocké dans le fichier core-site.XML de hello en tant que texte brut.

Au cours du traitement, hello de script effectue hello suivant des actions :

* Si hello compte de stockage existe déjà dans la configuration de base-site.XML hello pour le cluster de hello, hello script s’arrête et aucune action supplémentaire n’est effectuée.

* Vérifie que le compte de stockage hello existe et est accessible à l’aide de la clé de hello.

* Chiffre clé hello à l’aide des informations d’identification du cluster hello.

* Ajoute le fichier core-site.XML toohello hello stockage compte.

* Arrête et redémarre les services Oozie, fils, MapReduce2 et HDFS hello. Arrêter et démarrer ces services leur permet de toouse hello nouveau compte de stockage.

> [!WARNING]
> À l’aide d’un compte de stockage dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.

## <a name="hello-script"></a>script de Hello

__Emplacement du script__ : [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__Conditions requises__ :

* script de Hello doit être appliquée sur hello __Head nœuds__.

## <a name="toouse-hello-script"></a>script de hello toouse

Ce script peut être utilisé à partir de hello portail Azure, Azure PowerShell, ou hello Azure CLI 1.0. Pour plus d’informations, consultez hello [HDInsight de basés sur Linux de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.

> [!IMPORTANT]
> Lorsque vous utilisez les étapes de hello fournies dans le document de personnalisation hello, utilisez hello suivant informations tooapply ce script :
>
> * Remplacez les URI d’action de script exemple hello URI pour ce script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).
> * Remplacez les exemples de paramètres avec le nom de compte de stockage Windows Azure hello et la clé de cluster de hello stockage compte toobe toohello ajouté. Si à l’aide de hello le portail Azure, ces paramètres doivent être séparés par un espace.
> * Vous n’avez pas besoin toomark ce script en tant que __Persisted__, tel qu’il met à jour hello Ambari de configuration pour hello cluster directement.

## <a name="known-issues"></a>Problèmes connus

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Comptes de stockage non affichés dans le portail ou les outils Azure

Lors de l’affichage hello HDInsight cluster Bonjour portail Azure, en sélectionnant hello __comptes de stockage__ entrée sous __propriétés__ n’affiche pas les comptes de stockage ajoutés à cette action de script. Azure PowerShell et CLI d’Azure n’affichent pas compte de stockage supplémentaire hello soit.

informations de stockage Hello n’est pas affichées, car le script de hello modifie uniquement hello core-site.XML de configuration pour hello cluster. Ces informations ne sont pas utilisées lors de la récupération des informations de cluster hello à l’aide des API de gestion Azure.

les informations de compte de stockage tooview ajouté cluster toohello à l’aide de ce script, utilisez hello Ambari REST API. Utilisez hello suivant de commandes tooretrieve ces informations pour votre cluster :

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> Définissez `$clusterName` nom toohello du cluster HDInsight de hello. Définissez `$storageAccountName` nom toohello hello du compte de stockage. Lorsque vous y êtes invité, entrez la connexion de cluster hello (admin) et le mot de passe.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> Définissez `$PASSWORD` mot de passe de compte à la connexion (admin) toohello cluster. Définissez `$CLUSTERNAME` nom toohello du cluster HDInsight de hello. Définissez `$STORAGEACCOUNTNAME` nom toohello hello du compte de stockage.
>
> Cet exemple utilise [curl (http://curl.haxx.se/)](http://curl.haxx.se/) et [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve et l’analyse des données JSON.

Lorsque vous utilisez cette commande, remplacez __CLUSTERNAME__ avec nom hello du cluster HDInsight de hello. Remplacez __mot de passe__ avec un mot de passe de connexion pour le cluster de hello hello HTTP. Remplacez __STORAGEACCOUNT__ avec nom hello hello du compte de stockage ajouté à l’aide d’action de script. Informations retournées par cette commande apparaissent toohello similaire après le texte :

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

Ce texte est un exemple d’une clé chiffrée, ce qui est utilisé tooaccess hello compte de stockage.

### <a name="unable-tooaccess-storage-after-changing-key"></a>Stockage tooaccess impossible après avoir modifié la clé

Si vous modifiez la clé de hello pour un compte de stockage, HDInsight peut ne plus accéder aux comptes de stockage hello. HDInsight utilise une copie mise en cache de clé dans hello core-site.XML pour le cluster de hello. Cette copie mise en cache doit être la nouvelle clé de hello toomatch mis à jour.

Action de script hello à nouveau en cours d’exécution est __pas__ mettre à jour de la clé de hello, que le contrôle de script de hello toosee si une entrée pour le compte de stockage hello existe déjà. Si une entrée existe déjà, aucune modification n’est apportée.

toowork résoudre ce problème, vous devez supprimer l’entrée existante de hello hello compte de stockage. Utilisez hello étapes tooremove hello existant entrée suivante :

1. Dans un navigateur web, ouvrez hello l’interface utilisateur de Ambari Web pour votre cluster HDInsight. Hello URI est https://CLUSTERNAME.azurehdinsight.net. Remplacez __CLUSTERNAME__ avec nom hello de votre cluster.

    Lorsque vous y êtes invité, entrez hello HTTP nom d’utilisateur et mot de passe pour votre cluster.

2. À partir de la liste de hello des services sur la gauche hello de page de hello, sélectionnez __HDFS__. Puis sélectionnez hello __configurations__ onglet dans le centre de hello de page de hello.

3. Bonjour __filtre...__  , entrez une valeur de __fs.azure.account__. Cela retourne les entrées pour tous les comptes de stockage supplémentaires ont été ajoutées toohello cluster. Il existe deux types d’entrées : __keyprovider__ et __key__. Tous les deux contenir le nom hello hello du compte de stockage en tant que partie du nom de la clé hello.

    Hello Voici des exemples d’entrées pour un compte de stockage nommé __mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. Après avoir identifié les clés hello pour le compte de stockage hello vous devez tooremove, utilisez hello rouge '-' toohello icône à droite de hello entrée toodelete il. Utilisez ensuite hello __enregistrer__ bouton toosave vos modifications.

5. Une fois que les modifications ont été enregistrées, utilisez le compte de stockage hello script action tooadd hello et le nouveau cluster toohello de valeur de clé.

### <a name="poor-performance"></a>Problèmes de performances

Si le compte de stockage hello est dans une autre région que le cluster HDInsight de hello, vous pouvez rencontrer des performances médiocres. L’accès aux données dans un autre région envoie réseau du trafic à l’extérieur du centre de données Azure régional hello et à travers hello internet public, qui peut introduire une latence.

> [!WARNING]
> À l’aide d’un compte de stockage dans une autre région que le cluster HDInsight de hello n’est pas pris en charge.

### <a name="additional-charges"></a>Frais supplémentaires

Si le compte de stockage hello est dans une autre région de hello cluster HDInsight, vous remarquerez peut-être des frais de sortie supplémentaires sur votre facturation Azure. Des frais de sortie sont appliqués lorsque des données quittent un centre de données régional. Ces frais sont appliqués même si le trafic de hello est destiné à un autre centre de données Azure dans une autre région.

> [!WARNING]
> À l’aide d’un compte de stockage dans une autre région que le cluster HDInsight de hello n’est pas pris en charge.

## <a name="next-steps"></a>Étapes suivantes

Vous avez appris comment les comptes de stockage de plus de tooadd tooan les cluster HDInsight existant. Pour plus d’informations sur les actions de script, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md).
