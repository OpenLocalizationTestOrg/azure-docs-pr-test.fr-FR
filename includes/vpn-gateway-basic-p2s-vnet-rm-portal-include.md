Pour créer un réseau virtuel dans le modèle de déploiement Resource Manager à l’aide du portail Azure, suivez les étapes ci-dessous. Les captures d’écran sont fournies à titre d’exemple. Assurez-vous de remplacer ces valeurs par les vôtres. Pour plus d’informations sur l’utilisation des réseaux virtuels, voir [Présentation du réseau virtuel](../articles/virtual-network/virtual-networks-overview.md).

1. Dans un navigateur, accédez au [portail Azure](http://portal.azure.com) et, si nécessaire, connectez-vous avec votre compte Azure.
2. Cliquez sur **+** Dans le champ **Rechercher dans le marketplace**, tapez « réseau virtuel ». Localisez **Réseau virtuel** dans la liste renvoyée et cliquez pour ouvrir la page **Réseau virtuel**.

  ![Page Localiser les ressources du réseau virtuel](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/newvnetportal700.png "Page Localiser les ressources du réseau virtuel")
3. En bas de la page Réseau virtuel, à partir de la liste **Sélectionner un modèle de déploiement**, choisissez **Gestionnaire des ressources** puis cliquez sur **Créer**.

  ![Sélectionnez le Gestionnaire de ressources](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/resourcemanager250.png "Sélectionner le Gestionnaire de ressources")
4. Sur la page **Créer un réseau virtuel**, configurez les paramètres du réseau virtuel. Lorsque vous renseignez les champs, le point d’exclamation rouge se transforme en coche verte si les caractères saisis dans le champ sont valides. Il se peut que certaines valeurs soient renseignées automatiquement. Dans ce cas, remplacez ces valeurs par les vôtres. La page **Créer un réseau virtuel** ressemble à l’exemple suivant :

  ![Validation du champ](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/createp2sgvnet.png "Validation du champ")
5. **Nom** : entrez le nom du réseau virtuel.
6. **Espace d’adressage** : entrez l’espace d’adressage. Si vous avez plusieurs espaces d’adressage à ajouter, ajoutez le premier espace d’adressage. Vous pourrez ajouter des espaces d’adressage supplémentaires plus tard, après avoir créé le réseau virtuel.
7. **Nom du sous-réseau** : ajoutez le nom du sous-réseau et de la plage d’adresses de sous-réseau. Vous pourrez ajouter des sous-réseaux supplémentaires plus tard, après avoir créé le réseau virtuel.
8. **Abonnement** : vérifiez que l’abonnement répertorié est approprié. Vous pouvez modifier des abonnements à l’aide de la liste déroulante.
9. **Groupe de ressources** : sélectionnez un groupe de ressources existant ou créez-en un nouveau en tapant un nom pour ce dernier. Si vous créez un groupe, nommez-le en fonction de vos valeurs de configuration planifiée. Pour plus d’informations sur les groupes de ressources, consultez [Présentation d’Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
10. **Emplacement** : sélectionnez l’emplacement du réseau virtuel. L’emplacement détermine où se trouveront les ressources que vous déployez sur ce réseau virtuel.
11. Sélectionnez **Épingler au tableau de bord** si vous souhaitez être en mesure de trouver votre réseau virtuel facilement sur le tableau de bord, puis cliquez sur **Créer**.

 ![Épingler au tableau de bord](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/pintodashboard150.png "Épingler au tableau de bord")
12. Après avoir cliqué sur **Créer**, vous verrez une vignette apparaître sur votre tableau de bord. Celle-ci indique la progression de votre réseau virtuel. La vignette change lorsque le réseau virtuel est créé.

  ![Mosaïque de création du réseau virtuel](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/deploying150.png "Mosaïque de création du réseau virtuel")