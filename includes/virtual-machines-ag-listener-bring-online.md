1. Dans le Gestionnaire du cluster de basculement, développez les **Rôles**, puis mettez votre groupe de disponibilité en surbrillance.  

2. Sur hello **ressources** onglet, cliquez sur le nom d’écouteur hello, puis cliquez sur **propriétés**.

3. Cliquez sur hello **dépendances** onglet. Si plusieurs ressources sont répertoriés, vérifiez que les adresses IP hello ont ou non et dépendances.  

4. Cliquez sur **OK**.

5. Cliquez sur le nom d’écouteur hello, puis cliquez sur **mettre en ligne**.

6. Après avoir hello écouteur en ligne, sur hello **ressources** onglet, cliquez sur le groupe de disponibilité hello, puis cliquez sur **propriétés**.
   
    ![Configurer la ressource du groupe de disponibilité hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Créer une dépendance sur la ressource de nom d’écouteur hello (pas hello IP adresse ressources nom), puis cliquez sur **OK**.
   
    ![Ajouter une dépendance sur le nom de l’écouteur hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. Démarrez SQL Server Management Studio, puis connectez-vous toohello le réplica principal.

9. Accédez trop**haute disponibilité AlwaysOn** > **groupes de disponibilité** > **\<Nomgroupedisponibilité\>**   >  **Écouteurs de groupe de disponibilité**.  
    nom de l’écouteur Hello que vous avez créé dans le Gestionnaire de Cluster de basculement doit être affiché.

10. Cliquez sur le nom d’écouteur hello, puis cliquez sur **propriétés**.

11. Bonjour **Port** , spécifiez un numéro de port hello écouteur hello à l’aide de hello $EndpointPort que vous avez utilisé précédemment (dans ce didacticiel, 1433 était par défaut de hello), puis cliquez sur **OK**.

