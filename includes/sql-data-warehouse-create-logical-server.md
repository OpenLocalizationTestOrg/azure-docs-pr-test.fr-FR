### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="88bab-101">Créer un nouveau serveur SQL logique Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="88bab-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="88bab-102">Cliquez sur **Nouveau**, recherchez **Serveur logique**, puis appuyez sur **ENTRÉE**.</span><span class="sxs-lookup"><span data-stu-id="88bab-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![rechercher un serveur logique](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="88bab-104">Sélectionnez **Serveur SQL (serveur logique)**</span><span class="sxs-lookup"><span data-stu-id="88bab-104">Select **SQL server (logical server)**</span></span> 

    ![sélectionner un serveur logique](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="88bab-106">Cliquez sur **créer** tooopen hello nouveau SQL Server (serveur logique) panneau.</span><span class="sxs-lookup"><span data-stu-id="88bab-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="88bab-107"><kbd>![ouvrir le panneau de serveur logique](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![panneau serveur logique](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="88bab-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="88bab-108">Dans la zone de texte du nom du serveur de la lame hello SQL Server (serveur logique), fournissez un nom valide pour le nouveau serveur de logique hello.</span><span class="sxs-lookup"><span data-stu-id="88bab-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="88bab-109">Une coche verte indique que vous avez fourni un nom valide.</span><span class="sxs-lookup"><span data-stu-id="88bab-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![new server name](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="88bab-111">Hello nom qualifié complet pour le nouveau serveur sera < votre_nom_serveur >. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="88bab-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="88bab-112">Dans zone de texte connexion hello serveur admin, fournissez un nom d’utilisateur pour la connexion d’authentification SQL hello pour ce serveur.</span><span class="sxs-lookup"><span data-stu-id="88bab-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="88bab-113">Cette connexion est appelée connexion du serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="88bab-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="88bab-114">Une coche verte indique que vous avez fourni un nom valide.</span><span class="sxs-lookup"><span data-stu-id="88bab-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![SQL admin login](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="88bab-116">Bonjour **mot de passe** et **confirmer le mot de passe** zones de texte, fournir un mot de passe pour le compte de connexion du principal de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="88bab-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="88bab-117">Une coche verte indique que vous avez fourni un mot de passe valide.</span><span class="sxs-lookup"><span data-stu-id="88bab-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![SQL admin password](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="88bab-119">Sélectionnez un abonnement dans lequel vous avez des objets d’autorisation toocreate.</span><span class="sxs-lookup"><span data-stu-id="88bab-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![abonnement](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="88bab-121">Dans la zone de texte de groupe de ressources de hello, sélectionnez **nouvel** et puis, dans la zone de texte de groupe de ressources de hello, fournissez un nom valide pour le nouveau groupe de ressources hello (vous pouvez également utiliser un groupe de ressources existant si vous avez déjà créé un pour vous-même).</span><span class="sxs-lookup"><span data-stu-id="88bab-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="88bab-122">Une coche verte indique que vous avez fourni un nom valide.</span><span class="sxs-lookup"><span data-stu-id="88bab-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![new resource group](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="88bab-124">Bonjour **emplacement** zone de texte, sélectionnez une données poste approprié tooyour - telles que « Est de l’Australie ».</span><span class="sxs-lookup"><span data-stu-id="88bab-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![server location](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="88bab-126">Hello case à cocher pour **server d’Autoriser les services azure tooaccess** ne peut pas être modifié sur ce panneau.</span><span class="sxs-lookup"><span data-stu-id="88bab-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="88bab-127">Vous pouvez modifier ce paramètre sur le panneau de pare-feu serveur hello.</span><span class="sxs-lookup"><span data-stu-id="88bab-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="88bab-128">Pour plus d'informations, consultez [Prise en main de la sécurité](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="88bab-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="88bab-129">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="88bab-129">Click **Create**.</span></span>

    ![créer un bouton](./media/sql-data-warehouse-create-logical-server/create.png)

