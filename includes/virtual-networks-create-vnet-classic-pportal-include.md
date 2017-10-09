## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a>Comment toocreate un réseau classique virtuel Bonjour portail Azure
toocreate un réseau classique basé sur un scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.

1. À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.
2. Cliquez sur **nouveau** > **réseau** > **réseau virtuel**, notez que hello **sélectionner un modèle de déploiement** liste déjà indique **classique**, puis cliquez sur **créer**, comme indiqué dans la figure ci-dessous hello.
   
    ![Créer un réseau virtuel dans le portail Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. Sur hello **réseau virtuel** panneau, hello de type **nom** de hello réseau virtuel, puis cliquez sur **l’espace d’adressage**. Configurez les paramètres de votre espace de hello réseau virtuel et son premier sous-réseau, puis cliquez sur **OK**. figure Hello ci-dessous montre les paramètres de bloc CIDR hello dans notre scénario.
   
    ![Panneau Espace d’adressage](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. Cliquez sur **groupe de ressources** et sélectionnez hello virtuel à un tooadd de groupe de ressources, ou cliquez sur **créer un groupe de ressources** tooadd hello réseau virtuel tooa nouveau groupe de ressources. Hello figure ci-dessous montre les ressources hello paramètres de groupe pour un groupe de ressources appelé **TestRG**. Pour plus d’informations sur les groupes de ressources, consultez [Présentation d’Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
   
    ![Panneau Créer un groupe de ressources](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. Si nécessaire, modifiez hello **abonnement** et **emplacement** paramètres pour votre réseau virtuel. 
6. Si vous ne souhaitez pas toosee hello réseau virtuel sous forme de vignette Bonjour **tableau d’accueil**, désactiver **tooStartboard du code confidentiel**. 
7. Cliquez sur **créer** et la vignette de hello avis nommé **création Virtual network** comme indiqué dans la figure ci-dessous hello.
   
    ![Créer un réseau virtuel dans le portail](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. Attendez hello toobe de réseau virtuel créé, et lorsque vous consultez hello vignette ci-dessous, cliquez dessus tooadd d’autres sous-réseaux.
   
    ![Créer un réseau virtuel dans le portail](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. Vous devez voir hello **Configuration** pour votre réseau virtuel comme indiqué ci-dessous. 
   
    ![Créer un réseau virtuel dans le portail](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. Cliquez sur **Sous-réseaux** > **Ajouter**, renseignez les zones **Nom** et **Plage d’adresses (bloc CIDR)** pour votre sous-réseau, puis cliquez sur **OK**. Hello figure ci-dessous paramètres hello pour notre scénario en cours.
    
    ![Créer un réseau virtuel dans le portail Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

