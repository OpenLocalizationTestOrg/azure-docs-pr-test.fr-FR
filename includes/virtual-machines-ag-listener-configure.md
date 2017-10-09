écouteur du groupe de disponibilité Hello est un nom de réseau et d’adresse IP qui hello SQL Server écoute le groupe de disponibilité. écouteur du groupe de disponibilité toocreate hello, procédez comme hello suivant :

1. <a name="getnet"></a>Obtenir le nom de hello de ressource de réseau de clusters hello.

    a. Utilisez RDP tooconnect toohello machine virtuelle Azure qui héberge le réplica principal de hello. 

    b. Ouvrez le Gestionnaire du cluster de basculement.

    c. Sélectionnez hello **réseaux** nœud et le nom de réseau du cluster Remarque hello. Utilisez ce nom Bonjour `$ClusterNetworkName` variable Bonjour script PowerShell. Bonjour, suivant le nom de réseau du cluster image hello est **réseau du Cluster 1**:

   ![Nom réseau du cluster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Ajouter un point d’accès client hello.  
    point d’accès client Hello est le nom de réseau hello que les applications utilisent des bases de données tooconnect toohello dans un groupe de disponibilité. Créer le point d’accès client hello Gestionnaire du Cluster de basculement.

    a. Développez le nom du cluster hello, puis cliquez sur **rôles**.

    b. Bonjour **rôles** volet, le groupe de disponibilité avec le bouton hello nom et sélectionnez **ajouter une ressource** > **Point d’accès Client**.

   ![Point d’accès client](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. Bonjour **nom** zone, créez un nom pour ce nouvel écouteur. 
   Hello nom d’écouteur de nouveau hello est hello réseau que les applications utilisent tooconnect toodatabases dans le groupe de disponibilité de SQL Server hello.
   
    d. toofinish de la création du récepteur hello, cliquez sur **suivant** à deux reprises, puis cliquez sur **Terminer**. Ne mettez pas hello port d’écoute ou ressource en ligne à ce stade.

3. <a name="congroup"></a>Configurez la ressource IP de hello pour le groupe de disponibilité hello.

    a. Cliquez sur hello **ressources** onglet, puis cliquez sur point d’accès client hello vous avez créé.  
    point d’accès client Hello est hors connexion.

   ![Point d’accès client](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Avec le bouton droit de la ressource IP hello, puis cliquez sur Propriétés. Notez le nom hello d’adresse IP de hello et l’utiliser dans hello `$IPResourceName` variable Bonjour script PowerShell.

    c. Sous **Adresse IP**, cliquez sur **Adresse IP statique**. Définir l’adresse IP de hello comme hello même adresse que vous avez utilisé lorsque vous définissez l’adresse d’équilibrage de charge de hello sur hello portail Azure.

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Faites en sorte que ressource de groupe de disponibilité de SQL Server hello dépendante sur le point d’accès client hello.

    a. Dans le Gestionnaire du cluster de basculement, cliquez sur **Rôles**, puis sur votre groupe de disponibilité.

    b. Sur hello **ressources** sous l’onglet sous **autres ressources**, cliquez sur le groupe de ressources hello disponibilité, puis cliquez sur **propriétés**. 

    c. Sous l’onglet Dépendances de hello, ajoutez le nom de hello de ressource de hello client access point (écouteur hello).

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. Cliquez sur **OK**.

5. <a name="listname"></a>Hello d’accès client aux ressources dépendant de l’adresse IP de hello de point.

    a. Dans le Gestionnaire du cluster de basculement, cliquez sur **Rôles**, puis sur votre groupe de disponibilité. 

    b. Sur hello **ressources** onglet, cliquez sur la ressource de point d’accès hello client sous **nom du serveur**, puis cliquez sur **propriétés**. 

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Cliquez sur hello **dépendances** onglet. Vérifiez que les adresses IP de hello est une dépendance. Si elle n’est pas le cas, définir une dépendance sur l’adresse IP de hello. S’il existe plusieurs ressources sont répertoriés, vérifiez que les adresses IP hello ont ou non et dépendances. Cliquez sur **OK**. 

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Cliquez sur le nom d’écouteur hello, puis cliquez sur **mettre en ligne**. 

    >[!TIP]
    >Vous pouvez valider ce hello dépendances sont correctement configurées. Dans le Gestionnaire de Cluster de basculement, accédez à tooRoles, cliquez sur le groupe de disponibilité hello, cliquez sur **autres Actions**, puis cliquez sur **afficher le rapport de dépendance**. Lorsque hello dépendances sont correctement configurées, le groupe de disponibilité hello dépend du nom de réseau hello et nom de réseau hello dépend de l’adresse IP de hello. 


6. <a name="setparam"></a>Définir les paramètres de cluster hello dans PowerShell.
    
    a. Copiez hello suivant tooone de script PowerShell de vos instances de SQL Server. Mettre à jour les variables hello pour votre environnement.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Définir les paramètres de cluster de hello en hello script PowerShell en cours d’exécution sur l’un des nœuds de cluster hello.  

    > [!NOTE]
    > Si vos instances de SQL Server se trouvent dans des régions distinctes, vous avez besoin toorun hello PowerShell script à deux reprises. Hello la première fois, utilisez hello `$ILBIP` et `$ProbePort` à partir de la première région de hello. Hello la deuxième fois, utilisez hello `$ILBIP` et `$ProbePort` à partir de la deuxième zone de hello. nom réseau du cluster Hello et le nom de la ressource cluster IP hello sont hello même. 
