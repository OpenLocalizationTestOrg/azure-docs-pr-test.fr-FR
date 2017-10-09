


## <a name="tagging-a-virtual-machine-through-templates"></a>Balisage d’une machine virtuelle via des modèles
Voyons d’abord le balisage via des modèles. [Ce modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) place des balises sur hello suivant des ressources : calcul (Machine virtuelle), de stockage (compte de stockage) et de réseau (adresse IP publique, un réseau virtuel et une Interface réseau). Ce modèle est destiné à une machine virtuelle Windows, mais il peut être Aaapté pour les machines virtuelles Linux.

Cliquez sur hello **déployer tooAzure** bouton hello [lien modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Cela permet d’accéder toohello [portail Azure](https://portal.azure.com/) dans laquelle vous pouvez déployer ce modèle.

![Déploiement simple avec des balises](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Ce modèle inclut hello les étiquettes suivantes : *service*, *Application*, et *créé par*. Vous pouvez ajouter/modifier ces balises directement dans le modèle de hello si vous souhaitez que les noms de balise différents.

![Balises Azure dans un modèle](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Comme vous pouvez le voir, les balises de hello sont définies en tant que paires clé/valeur, séparées par un signe deux-points ( :). les balises de Hello doivent être définies dans ce format :

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Enregistrez le fichier de modèle hello après avoir terminé la modification avec balises hello de votre choix.

Ensuite, dans hello **modifier les paramètres** section, vous pouvez remplir les valeurs hello pour vos balises.

![Modifier des balises dans le portail Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Cliquez sur **créer** toodeploy ce modèle avec les valeurs de balise.

## <a name="tagging-through-hello-portal"></a>Le balisage via hello portail
Après avoir créé vos ressources avec des balises, vous pouvez afficher, ajouter et supprimer des balises dans le portail de hello.

Sélectionnez hello balises icône tooview vos balises :

![Icône Balises dans le portail Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Ajouter une nouvelle balise via le portail de hello en définissant votre propre paire clé/valeur, puis enregistrez-le.

![Ajouter une nouvelle balise dans le portail Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

Votre nouvelle balise doit maintenant apparaître dans la liste hello des balises pour votre ressource.

![Nouvelle balise enregistrée dans le portail Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

