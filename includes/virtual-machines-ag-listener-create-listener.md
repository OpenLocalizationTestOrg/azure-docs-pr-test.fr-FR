Dans cette étape, vous créez manuellement l’écouteur du groupe de disponibilité hello dans le Gestionnaire du Cluster de basculement et de SQL Server Management Studio.

1. Ouvrez le Gestionnaire du Cluster de basculement à partir du nœud hello qui héberge le réplica principal de hello.

2. Sélectionnez hello **réseaux** nœud, puis le nom de réseau du cluster Remarque hello. Ce nom est utilisé dans la variable hello $ClusterNetworkName Bonjour script PowerShell.

3. Développez le nom du cluster hello, puis cliquez sur **rôles**.

4. Bonjour **rôles** volet, le groupe de disponibilité avec le bouton hello nom et sélectionnez **ajouter une ressource** > **Point d’accès Client**.
   
    ![Ajouter un point d’accès client pour le groupe de disponibilité](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. Bonjour **nom** , créez un nom pour ce nouveau port d’écoute, cliquez sur **suivant** à deux reprises, puis cliquez sur **Terminer**.  
    Ne mettez pas hello port d’écoute ou ressource en ligne à ce stade.

6. Cliquez sur hello **ressources** onglet, puis cliquez sur point d’accès client hello vous venez de créer. 
    ressource d’adresse IP Hello pour chaque réseau de cluster dans votre cluster s’affiche. S’il s’agit d’une solution basée uniquement sur Azure, une seule ressource d’adresse IP est affichée.

7. Effectuez une des manières suivantes les hello :
   
   * tooconfigure une solution hybride :
     
        a. Cliquez sur la ressource d’adresse IP hello qui correspond le sous-réseau local de tooyour, puis sélectionnez **propriétés**. Notez le nom de l’adresse IP hello et nom de réseau.
   
        b. Sélectionnez **Adresse IP statique**, affectez une adresse IP inutilisée, puis cliquez sur **OK**.
 
   * tooconfigure une solution Azure uniquement :

        a. Cliquez sur la ressource d’adresse IP hello correspondant tooyour sous-réseau Azure, puis sélectionnez **propriétés**.
       
       > [!NOTE]
       > Si l’écouteur de hello échoue ultérieurement toocome en ligne en raison d’une adresse IP conflictuelle par DHCP, vous pouvez configurer une adresse IP statique valide dans cette fenêtre de propriétés.
       > 
       > 

       b. Dans hello même **adresse IP** fenêtre Propriétés, modification hello **nom de l’adresse IP**.  
        Ce nom est utilisé dans la variable hello $IPResourceName Hello script PowerShell. Si votre solution couvre plusieurs réseaux virtuels Azure, répétez cette étape pour chaque ressource IP.

