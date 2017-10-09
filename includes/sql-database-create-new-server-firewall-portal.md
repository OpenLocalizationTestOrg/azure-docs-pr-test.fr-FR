
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="0934a-101">Créer une règle de pare-feu de niveau serveur dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0934a-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="0934a-102">Dans le panneau de serveur SQL hello, sous Paramètres, cliquez sur **pare-feu** Panneau de pare-feu tooopen hello pour SQL server de hello.</span><span class="sxs-lookup"><span data-stu-id="0934a-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="0934a-103">Vérifiez l’adresse IP du client hello affiché et valider qu’il s’agit de votre adresse IP sur Internet à l’aide d’un navigateur de votre choix de hello (demandez « quel est mon adresse IP).</span><span class="sxs-lookup"><span data-stu-id="0934a-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="0934a-104">Parfois, elles ne correspondent pas pour diverses raisons.</span><span class="sxs-lookup"><span data-stu-id="0934a-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="0934a-105">En supposant que les adresses IP de hello correspondent, cliquez sur **ajouter l’adresse IP du client** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="0934a-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![add client IP](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="0934a-107">Vous pouvez ouvrir le pare-feu de base de données SQL hello hello tooa unique adresse IP de serveur ou d’une plage entière d’adresses.</span><span class="sxs-lookup"><span data-stu-id="0934a-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="0934a-108">Ouverture hello pare-feu permet aux administrateurs SQL et les utilisateurs toologin tooany base de données sur hello toowhich serveur comportant des informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="0934a-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="0934a-109">Cliquez sur **enregistrer** dans hello toosave de barre d’outils de cette règle de pare-feu de niveau serveur, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0934a-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![add client IP](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="0934a-111">Pour trouver un didacticiel, consultez [Didacticiel sur la base de données SQL : création d’un serveur, d’une règle de pare-feu de niveau serveur, d’un exemple de base de données, d’une règle de pare-feu de niveau base de données et connexion à SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0934a-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
