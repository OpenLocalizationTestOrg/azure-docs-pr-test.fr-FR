---
title: "tooHadoop d’Excel aaaConnect avec hello Hive ODBC Driver - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooset configuration et utilisation hello pilote ODBC de la ruche de Microsoft pour tooquery des données Excel dans des clusters HDInsight à partir de Microsoft Excel."
keywords: hadoop excel,hive excel,hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Rejoignez tooHadoop Excel dans Azure HDInsight hello Hive pilote ODBC de Microsoft

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

La solution Big Data de Microsoft intègre des composants de Microsoft Business Intelligence (BI) avec les clusters Apache Hadoop qui ont été déployés par hello Azure HDInsight. Un exemple de cette intégration est hello capacité tooconnect Excel toohello ruche de l’entrepôt de données d’un cluster Hadoop dans HDInsight à l’aide de hello les pilotes Microsoft Hive ODBC Open Database Connectivity ().

Il est également possible tooconnect les données de salutation associées à un cluster HDInsight et d’autres sources de données, y compris d’autres (non-HDInsight) Hadoop clusters, à partir d’Excel à l’aide de hello complément Microsoft Power Query pour Excel. Pour plus d’informations sur l’installation et à l’aide de Power Query, consultez [tooHDInsight connexion Excel avec Power Query][hdinsight-power-query].

> [!NOTE]
> Alors que les étapes hello cet article peut être utilisé avec une soit Linux ou cluster HDInsight de basés sur Windows, Windows est requis pour la station de travail cliente hello.
> 
> 

**Conditions préalables**:

Avant de commencer cet article, vous devez disposer de hello éléments suivants :

* **Un cluster HDInsight**. toocreate, consultez [prise en main Azure HDInsight][hdinsight-get-started].
* **Une station de travail** avec Office Professionnel Plus 2013, Office 365 ProPlus, l'édition autonome d'Excel 2013 ou Office Professionnel Plus 2010.

## <a name="install-microsoft-hive-odbc-driver"></a>Installation du pilote ODBC Microsoft Hive
Télécharger et installer Microsoft ODBC Driver de la ruche de hello [centre de téléchargement][hive-odbc-driver-download].

Ce pilote peut être installé sur les versions 32 bits ou 64 bits de Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 et Windows Server 2012. pilote de Hello permet la connexion tooAzure HDInsight (version 1.6 et versions ultérieure) et Azure HDInsight émulateur (v.1.0.0.0 et versions ultérieures). Vous doit installer hello version que hello d’application hello où vous utilisez le pilote ODBC de hello. Pour ce didacticiel, le pilote de hello est utilisé à partir d’Office Excel.

## <a name="create-hive-odbc-data-source"></a>Création d’une source de données ODBC Hive
Hello étapes suivantes vous montrent comment toocreate une Source de données ODBC de la ruche.

1. À partir de Windows 8 ou Windows 10, appuyez sur l’écran d’accueil hello Windows tooopen clé hello et tapez **des sources de données**.
2. Cliquez sur **Configurer les sources de données ODBC (32 bits)** ou **Configurer les sources de données ODBC (64 bits)** selon votre version d'Office. Si vous utilisez Windows 7, choisissez **Sources de données ODBC (32 bits)** ou **Sources de données ODBC (64 bits)** dans **Outils d'administration**. Vous allez voir hello **administrateur de sources de données ODBC** boîte de dialogue.
   
    ![Administrateur de sources de données ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configurer un DSN à l’aide de l’Administrateur de sources de données ODBC")

3. À partir du DNS de l’utilisateur, cliquez sur **ajouter** tooopen hello **créer une nouvelle Source de données** Assistant.
4. Sélectionnez **Microsoft Hive ODBC Driver**, puis cliquez sur **Terminer**. Vous allez voir hello **Microsoft Hive DNS configuration du pilote ODBC** boîte de dialogue.
5. Tapez ou sélectionnez hello valeurs suivantes :
   
   | Propriété | Description |
   | --- | --- |
   |  Data Source Name |Donner à une source de données tooyour nom |
   |  Host |Entrez &lt;HDInsightClusterName>.azurehdinsight.net. Par exemple, myHDICluster.azurehdinsight.net |
   |  Port |Utilisez <strong>443</strong>. (Ce port a été modifié à partir de too443 563.) |
   |  Base de données |Utilisez <strong>Default</strong>. |
   |  Mechanism |Sélectionnez <strong>Azure HDInsight Service</strong>. |
   |  User Name |Entrez le nom de l’utilisateur HTTP du cluster HDInsight. nom d’utilisateur par défaut de Hello est <strong>admin</strong>. |
   |  Mot de passe |Entrez le mot de passe du cluster HDInsight. |
   
    </table>
   
    Il existe certains paramètres importants de toobe connaître lorsque vous cliquez sur **Options avancées**:
   
   | Paramètre | Description |
   | --- | --- |
   |  Use Native Query |Lorsqu’elle est sélectionnée, le pilote ODBC de hello ne tente pas de tooconvert TSQL dans HiveQL. À utiliser uniquement si vous êtes sûr à 100 % que vous envoyez des instructions HiveQL pures. Lors de la connexion tooSQL serveur ou base de données SQL Azure, vous devez laisser désactivée. |
   |  Rows fetched per block |Lors de la récupération d’un grand nombre d’enregistrements, le réglage de ce paramètre peut être requis tooensure des performances optimales. |
   |  Default string column length, Binary column length, Decimal column scale |longueurs de type de données de Hello et précisions peuvent affecter la façon dont les données sont retournées. Ils entraînent toobe informations incorrectes retournée en raison tooloss de précision et/ou de troncation. |

    ![Options avancées](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Options avancées de configuration de DSN")

1. Cliquez sur **Test** source de données tootest hello. Lors de la source de données hello est correctement configuré, il montre *TESTS effectués avec succès !*.
2. Cliquez sur **OK** boîte de dialogue Test tooclose hello. nouvelle source de données Hello doit figurer sur hello **administrateur de sources de données ODBC**.
3. Cliquez sur **OK** Assistant de hello tooexit.

## <a name="import-data-into-excel-from-hdinsight"></a>Importation de données dans Microsoft Excel à partir de HDInsight
Hello étapes suivantes décrivent hello façon tooimport que les données à partir d’une table Hive dans un classeur Excel à l’aide de la source de données ODBC hello que vous avez créé dans la section précédente de hello.

1. Ouvrez un nouveau classeur ou un classeur existant dans Excel.
2. À partir de hello **données** , cliquez sur **obtenir des données**, cliquez sur **à partir d’autres Sources**, puis cliquez sur **ODBC à partir de** toolaunch hello  **Assistant connexion de données**.
   
    ![Assistant Ouvrir la connexion de données](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Assistant Ouvrir la connexion de données")
4. Les données de salutation sélectionnez le nom que vous avez créé dans la dernière section de hello de la source, puis cliquez sur **OK**.
5. Entrez le nom d’utilisateur Hadoop (hello par défaut est admin) et hello de mot de passe, puis cliquez sur **connexion**.
6. Dans le navigateur, développez **HIVE**, développez **par défaut**, cliquez sur **hivesampletable**, puis cliquez sur **Charger**. Il prend quelques secondes avant de données obtient tooExcel importé.

    ![Navigateur ODBC HDInsight Hive](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Assistant Ouvrir la connexion de données")


## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toouse hello des données de tooretrieve du pilote ODBC de Microsoft de la ruche de hello HDInsight Service dans Excel. De même, vous pouvez récupérer des données à partir de hello HDInsight Service dans la base de données SQL. Il est également données tooupload possibles dans un HDInsight Service. toolearn, voir :

* [Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-data]
* [Télécharger des données tooHDInsight][hdinsight-upload-data]
* [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


