---
title: "tooHadoop d’Excel aaaConnect avec Power Query - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment parti tootake de composants de business intelligence et utilisez Power Query pour les données Excel tooaccess stockées dans Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>Se connecter tooHadoop d’Excel à l’aide de Power Query
Une fonction clé de la solution de données volumineuses Microsoft hello est l’intégration de composants de Microsoft business intelligence (BI) avec des clusters Hadoop dans HDInsight de Azure hello. Un exemple principal est hello capacité tooconnect Excel toohello compte de stockage Azure qui contient les données hello associées à votre cluster Hadoop à l’aide de hello Microsoft Power Query pour Excel. Cet article vous guide tout au long de comment tooset des et utiliser les données de tooquery Power Query associées à un cluster Hadoop gérés avec HDInsight.

### <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello éléments suivants :

* **Un cluster HDInsight**. tooconfigure, consultez [prise en main Azure HDInsight][hdinsight-get-started].
* **Une station de travail** fonctionnant sous Windows 7, Windows Server 2008 R2 ou une version ultérieure.
* **Office 2016, Office 2013 Professionnel Plus, Office 365 ProPlus, Excel 2013 autonome ou Office 2010 Professionnel Plus**.

## <a name="install-power-query"></a>Installation de Power Query
Power Query permet d'importer des données produites ou générées par un travail Hadoop s'exécutant sur un cluster HDInsight.

Dans Excel 2016, Power Query a été intégré dans le ruban de données hello hello Get & Transform section. Pour les versions antérieures de Excel, téléchargez Microsoft Power Query pour Excel à partir de hello [Microsoft Download Center] [ powerquery-download] et l’installer.

## <a name="import-hdinsight-data-into-excel"></a>Importation de données HDInsight dans Excel
Hello complément Power Query pour Excel rend tooimport facilement les données à partir de votre cluster HDInsight dans Excel, où des outils de BI tels que PowerPivot et de mappage de l’alimentation peuvent être tooinspect utilisé, analyser et présenter des données hello.

**tooimport des données à partir d’un cluster HDInsight**

1. Ouvrez Excel.
2. Créez un classeur vide.
3. Effectuez hello selon la version d’Excel hello comme suit :

    - Excel 2016

        - Cliquez sur hello **données** menu, cliquez sur **obtenir des données** de hello **obtenir et transformer des données** du ruban, cliquez sur **à partir de Azure**, puis cliquez sur  **À partir d’Azure HDInsight(HDFS)**.

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Cliquez sur hello **Power Query** menu, cliquez sur **à partir de Azure**, puis cliquez sur **à partir de Microsoft Azure HDInsight**.
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Remarque :** si vous ne voyez pas hello **Power Query** menu, accédez trop**fichier** > **Options** > **descompléments**, puis sélectionnez **compléments COM** de déroulante hello **gérer** zone en bas de hello de page de hello. Sélectionnez hello **accédez...**  bouton et vérifier cette zone hello pour hello Power Query pour Excel a été vérifiée.
       
        **Remarque :** Power Query vous permet également de données tooimport de HDFS en cliquant sur **à partir d’autres Sources**.
4. Pour **nom de compte**, entrez le nom hello de compte de stockage d’objets Blob Azure hello associé à votre cluster, puis cliquez sur **OK**. Ce compte peut être hello [compte de stockage par défaut](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) ou un compte de stockage.  format de Hello est *https://&lt;StorageAccountName >.blob.core.windows.net/*.
5. Pour **clé de compte**, entrez la clé hello pour hello compte de stockage Blob, puis cliquez sur **enregistrer**. (Vous devez hello uniquement des informations compte hello tooenter lors du premier qu'accès cette banque d’informations.)
6. Bonjour **Navigator** volet hello à gauche de l’éditeur de requête de hello, double-cliquez sur le nom de conteneur de stockage Blob hello. Par défaut, nom du conteneur hello est hello même nom que le nom du cluster hello.
7. Recherchez **HiveSampleData.txt** Bonjour **nom** colonne (chemin d’accès du dossier hello **... / hive/de l’entrepôt/hivesampletable/**), puis cliquez sur **binaire** sur gauche hello de HiveSampleData.txt. HiveSampleData.txt est fourni avec tous les clusters de hello. Si vous le souhaitez, vous pouvez utiliser votre propre fichier.
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. Si vous le souhaitez, vous pouvez renommer les noms de colonne hello. Lorsque vous êtes prêt, cliquez sur **Fermer et charger**.  les données de salutation a été chargé tooyour classeur :
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toouse Power tooretrieve interroge les données de HDInsight dans Excel. De la même façon, vous pouvez extraire des données de HDInsight et les importer dans une base de données SQL Azure. Il est également données tooupload possible dans HDInsight. toolearn, voir hello suivant des articles :

* [Rejoignez Excel tooHDInsight hello Microsoft ODBC Driver de la ruche][hdinsight-ODBC]
* [Télécharger des données tooHDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
