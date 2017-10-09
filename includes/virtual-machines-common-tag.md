


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="41772-101">Balisage d’une machine virtuelle via des modèles</span><span class="sxs-lookup"><span data-stu-id="41772-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="41772-102">Voyons d’abord le balisage via des modèles.</span><span class="sxs-lookup"><span data-stu-id="41772-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="41772-103">[Ce modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) place des balises sur hello suivant des ressources : calcul (Machine virtuelle), de stockage (compte de stockage) et de réseau (adresse IP publique, un réseau virtuel et une Interface réseau).</span><span class="sxs-lookup"><span data-stu-id="41772-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="41772-104">Ce modèle est destiné à une machine virtuelle Windows, mais il peut être Aaapté pour les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="41772-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="41772-105">Cliquez sur hello **déployer tooAzure** bouton hello [lien modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="41772-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="41772-106">Cela permet d’accéder toohello [portail Azure](https://portal.azure.com/) dans laquelle vous pouvez déployer ce modèle.</span><span class="sxs-lookup"><span data-stu-id="41772-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Déploiement simple avec des balises](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="41772-108">Ce modèle inclut hello les étiquettes suivantes : *service*, *Application*, et *créé par*.</span><span class="sxs-lookup"><span data-stu-id="41772-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="41772-109">Vous pouvez ajouter/modifier ces balises directement dans le modèle de hello si vous souhaitez que les noms de balise différents.</span><span class="sxs-lookup"><span data-stu-id="41772-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Balises Azure dans un modèle](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="41772-111">Comme vous pouvez le voir, les balises de hello sont définies en tant que paires clé/valeur, séparées par un signe deux-points ( :).</span><span class="sxs-lookup"><span data-stu-id="41772-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="41772-112">les balises de Hello doivent être définies dans ce format :</span><span class="sxs-lookup"><span data-stu-id="41772-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="41772-113">Enregistrez le fichier de modèle hello après avoir terminé la modification avec balises hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="41772-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="41772-114">Ensuite, dans hello **modifier les paramètres** section, vous pouvez remplir les valeurs hello pour vos balises.</span><span class="sxs-lookup"><span data-stu-id="41772-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Modifier des balises dans le portail Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="41772-116">Cliquez sur **créer** toodeploy ce modèle avec les valeurs de balise.</span><span class="sxs-lookup"><span data-stu-id="41772-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="41772-117">Le balisage via hello portail</span><span class="sxs-lookup"><span data-stu-id="41772-117">Tagging through hello Portal</span></span>
<span data-ttu-id="41772-118">Après avoir créé vos ressources avec des balises, vous pouvez afficher, ajouter et supprimer des balises dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="41772-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="41772-119">Sélectionnez hello balises icône tooview vos balises :</span><span class="sxs-lookup"><span data-stu-id="41772-119">Select hello tags icon tooview your tags:</span></span>

![Icône Balises dans le portail Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="41772-121">Ajouter une nouvelle balise via le portail de hello en définissant votre propre paire clé/valeur, puis enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="41772-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Ajouter une nouvelle balise dans le portail Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="41772-123">Votre nouvelle balise doit maintenant apparaître dans la liste hello des balises pour votre ressource.</span><span class="sxs-lookup"><span data-stu-id="41772-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Nouvelle balise enregistrée dans le portail Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

