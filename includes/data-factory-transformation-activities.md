Azure Data Factory prend en charge hello suivant des activités de transformation qui peuvent être ajouté toopipelines soit individuellement ou chaîné avec une autre activité.

| Activités de transformation des données | Environnement de calcul |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Diffusion en continu Hadoop](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Activités Machine Learning : exécution de lot et mise à jour de ressource](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |Microsoft Azure |
| [Procédure stockée](../articles/data-factory/data-factory-stored-proc-activity.md) |SQL Azure, Azure SQL Data Warehouse ou SQL Server |
| [Langage U-SQL du service Analytique Data Lake](../articles/data-factory/data-factory-usql-activity.md) |Service Analytique Azure Data Lake |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |HDInsight [Hadoop] ou Azure Batch |

> [!NOTE]
> Vous pouvez utiliser les programmes MapReduce activité toorun Spark sur votre cluster HDInsight Spark. Consultez la page [Appeler des programmes Spark à partir d'Azure Data Factory](../articles/data-factory/data-factory-spark.md) pour plus d'informations.
> Vous pouvez créer une activité personnalisée toorun R scripts sur votre cluster HDInsight avec R installé. Consultez la page [Exécuter des scripts R avec Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).
> 
> 

