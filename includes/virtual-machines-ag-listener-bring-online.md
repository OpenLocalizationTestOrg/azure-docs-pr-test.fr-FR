1. <span data-ttu-id="0cfb4-101">Dans le Gestionnaire du cluster de basculement, développez les **Rôles**, puis mettez votre groupe de disponibilité en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="0cfb4-102">Sur hello **ressources** onglet, cliquez sur le nom d’écouteur hello, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="0cfb4-103">Cliquez sur hello **dépendances** onglet. Si plusieurs ressources sont répertoriés, vérifiez que les adresses IP hello ont ou non et dépendances.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="0cfb4-104">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-104">Click **OK**.</span></span>

5. <span data-ttu-id="0cfb4-105">Cliquez sur le nom d’écouteur hello, puis cliquez sur **mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="0cfb4-106">Après avoir hello écouteur en ligne, sur hello **ressources** onglet, cliquez sur le groupe de disponibilité hello, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Configurer la ressource du groupe de disponibilité hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="0cfb4-108">Créer une dépendance sur la ressource de nom d’écouteur hello (pas hello IP adresse ressources nom), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Ajouter une dépendance sur le nom de l’écouteur hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="0cfb4-110">Démarrez SQL Server Management Studio, puis connectez-vous toohello le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="0cfb4-111">Accédez trop**haute disponibilité AlwaysOn** > **groupes de disponibilité** > **\<Nomgroupedisponibilité\>**   >  **Écouteurs de groupe de disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="0cfb4-112">nom de l’écouteur Hello que vous avez créé dans le Gestionnaire de Cluster de basculement doit être affiché.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="0cfb4-113">Cliquez sur le nom d’écouteur hello, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="0cfb4-114">Bonjour **Port** , spécifiez un numéro de port hello écouteur hello à l’aide de hello $EndpointPort que vous avez utilisé précédemment (dans ce didacticiel, 1433 était par défaut de hello), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cfb4-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

