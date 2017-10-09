
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="4e25d-101">toosave des coûts, vous pouvez suspendre et reprendre des ressources à la demande de calcul.</span><span class="sxs-lookup"><span data-stu-id="4e25d-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="4e25d-102">Par exemple, si vous n’utiliserez pas de base de données hello pendant la nuit de hello et le week-end, suspendre pendant les heures et reprendre la journée hello.</span><span class="sxs-lookup"><span data-stu-id="4e25d-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="4e25d-103">Vous ne sera pas facturé pour Dwu lorsque la base de données hello est suspendue.</span><span class="sxs-lookup"><span data-stu-id="4e25d-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="4e25d-104">Lorsque vous suspendez une base de données :</span><span class="sxs-lookup"><span data-stu-id="4e25d-104">When you pause a database:</span></span>

* <span data-ttu-id="4e25d-105">Ressources de calcul et de mémoire sont retournés pool toohello des ressources disponibles dans le centre de données hello</span><span class="sxs-lookup"><span data-stu-id="4e25d-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="4e25d-106">Les coûts de DWU sont zéro pour la durée de pause de hello hello.</span><span class="sxs-lookup"><span data-stu-id="4e25d-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="4e25d-107">Le stockage de données n’est pas affecté et vos données restent intactes.</span><span class="sxs-lookup"><span data-stu-id="4e25d-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="4e25d-108">SQL Data Warehouse annule toutes les opérations en cours d’exécution ou en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="4e25d-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

