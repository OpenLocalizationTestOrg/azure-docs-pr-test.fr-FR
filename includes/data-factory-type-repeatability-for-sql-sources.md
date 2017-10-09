## <a name="repeatability-during-copy"></a>Répétabilité pendant la copie
Copie des données tooAzure SQL/SQL Server à partir d’autres données lorsque stocke une répétabilité de tookeep besoins dans l’esprit tooavoid des résultats inattendus. 

Lors de la copie des données tooAzure base de données SQL/SQL Server, l’activité de copie sera par table récepteur des toohello de jeu de données par défaut APPEND hello par défaut. Par exemple, lors de la copie des données à partir d’une source de fichier CSV (valeurs de données séparées par des virgules) contenant deux enregistrements tooAzure base de données SQL/SQL Server, il s’agit quelle table hello ressemble à :

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Supposons que vous a détecté des erreurs dans le fichier source et de la quantité de mise à jour hello de Tube vers le bas à partir de 2 too4 dans le fichier de source de hello. Si vous réexécutez la tranche de données hello pour cette période, vous trouverez deux nouveaux enregistrements ajoutés tooAzure base de données SQL/SQL Server. Hello ci-dessous suppose que Hello des colonnes dans la table de hello ont de contrainte de clé primaire hello.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid, vous devez la sémantique UPSERT toospecify en tirant parti d’un des hello ci-dessous 2 mécanismes indiqué ci-dessous.

> [!NOTE]
> Une tranche peut être réexécutée automatiquement dans Azure Data Factory en fonction de la stratégie de nouvelle tentative hello spécifié.
> 
> 

### <a name="mechanism-1"></a>Mécanisme 1
Vous pouvez tirer parti de **sqlWriterCleanupScript** propriété toofirst effectuer l’action de nettoyage lors de l’exécution d’une tranche. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Hello script de nettoyage sera exécuté à la première pendant la copie pour une tranche de donnée qui supprime les données de salutation à partir de la tranche de toothat hello Table SQL correspondante. activité Hello est par la suite insérer des données de hello dans hello Table SQL. 

Si la tranche de hello est maintenant exécuter à nouveau, puis vous trouverez quantité de hello est mise à jour comme vous le souhaitez.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Supposons que hello enregistrement de laver plat est supprimé de volume partagé de cluster hello d’origine. Puis réexécutez tranche de hello produirait hello suivant des résultats : 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
Rien de nouveau avait toobe terminé. activité de copie Hello s’exécutaient hello nettoyage script toodelete hello données correspondantes pour ce secteur. Puis il lire l’entrée de hello de csv hello (qui puis contenu uniquement 1 enregistrement) et inséré dans la Table de hello. 

### <a name="mechanism-2"></a>Mécanisme 2
> [!IMPORTANT]
> Pour le moment, sliceIdentifierColumnName n’est pas pris en charge pour Azure SQL Data Warehouse. 

Répétabilité de tooachieve un autre mécanisme consiste à avoir une colonne dédiée (**sliceIdentifierColumnName**) Bonjour cibler la Table. Cette colonne peut être utilisée par Azure Data Factory tooensure hello source et destination reste synchronisé. Cette approche fonctionne quand il existe une grande souplesse dans la modification ou la définition de schéma de Table SQL de destination hello. 

Cette colonne devrait être utilisée par Azure Data Factory à des fins de répétabilité et de dans le processus de hello Azure Data Factory n’apporte aucun schéma change toohello Table. Méthode toouse cette approche :

1. Définir une colonne de type binary (32) dans la destination de hello Table SQL. Aucune contrainte ne doit exister sur cette colonne. Pour cet exemple, nommons cette colonne « ColumnForADFuseOnly ».
2. Utiliser dans l’activité de copie hello comme suit :
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

Azure Data Factory remplit cette colonne en fonction de son besoin tooensure hello source et destination restent synchronisés. les valeurs Hello de cette colonne ne doivent pas être utilisées en dehors de ce contexte par utilisateur de hello. 

Toomechanism similaires 1, est de l’activité de copie automatiquement première Nettoyez les données hello pour hello donné tranche à partir de destination hello Table SQL et puis exécutez l’activité de copie hello normalement données hello tooinsert toodestination source pour cette tranche. 

