### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Créer un nouveau serveur SQL logique Bonjour portail Azure

1. Cliquez sur **Nouveau**, recherchez **Serveur logique**, puis appuyez sur **ENTRÉE**.

    ![rechercher un serveur logique](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. Sélectionnez **Serveur SQL (serveur logique)** 

    ![sélectionner un serveur logique](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Cliquez sur **créer** tooopen hello nouveau SQL Server (serveur logique) panneau.

   <kbd>![ouvrir le panneau de serveur logique](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![panneau serveur logique](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. Dans la zone de texte du nom du serveur de la lame hello SQL Server (serveur logique), fournissez un nom valide pour le nouveau serveur de logique hello. Une coche verte indique que vous avez fourni un nom valide.
    
    ![new server name](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Hello nom qualifié complet pour le nouveau serveur sera < votre_nom_serveur >. database.windows.net.
    >
    
4. Dans zone de texte connexion hello serveur admin, fournissez un nom d’utilisateur pour la connexion d’authentification SQL hello pour ce serveur. Cette connexion est appelée connexion du serveur principal hello. Une coche verte indique que vous avez fourni un nom valide.
    
    ![SQL admin login](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. Bonjour **mot de passe** et **confirmer le mot de passe** zones de texte, fournir un mot de passe pour le compte de connexion du principal de serveur hello. Une coche verte indique que vous avez fourni un mot de passe valide.
    
    ![SQL admin password](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. Sélectionnez un abonnement dans lequel vous avez des objets d’autorisation toocreate.

    ![abonnement](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. Dans la zone de texte de groupe de ressources de hello, sélectionnez **nouvel** et puis, dans la zone de texte de groupe de ressources de hello, fournissez un nom valide pour le nouveau groupe de ressources hello (vous pouvez également utiliser un groupe de ressources existant si vous avez déjà créé un pour vous-même). Une coche verte indique que vous avez fourni un nom valide.

    ![new resource group](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. Bonjour **emplacement** zone de texte, sélectionnez une données poste approprié tooyour - telles que « Est de l’Australie ».
    
    ![server location](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > Hello case à cocher pour **server d’Autoriser les services azure tooaccess** ne peut pas être modifié sur ce panneau. Vous pouvez modifier ce paramètre sur le panneau de pare-feu serveur hello. Pour plus d'informations, consultez [Prise en main de la sécurité](../articles/sql-database/sql-database-manage-servers-portal.md).
    >
    
9. Cliquez sur **Create**.

    ![créer un bouton](./media/sql-data-warehouse-create-logical-server/create.png)

