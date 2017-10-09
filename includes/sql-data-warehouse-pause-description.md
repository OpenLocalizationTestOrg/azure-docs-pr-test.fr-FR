
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
toosave des coûts, vous pouvez suspendre et reprendre des ressources à la demande de calcul. Par exemple, si vous n’utiliserez pas de base de données hello pendant la nuit de hello et le week-end, suspendre pendant les heures et reprendre la journée hello. Vous ne sera pas facturé pour Dwu lorsque la base de données hello est suspendue.

Lorsque vous suspendez une base de données :

* Ressources de calcul et de mémoire sont retournés pool toohello des ressources disponibles dans le centre de données hello
* Les coûts de DWU sont zéro pour la durée de pause de hello hello.
* Le stockage de données n’est pas affecté et vos données restent intactes. 
* SQL Data Warehouse annule toutes les opérations en cours d’exécution ou en file d’attente.

