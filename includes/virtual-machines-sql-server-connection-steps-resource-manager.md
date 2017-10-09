### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="1bfd9-101">Configurer un nom DNS pour l’adresse IP publique de hello</span><span class="sxs-lookup"><span data-stu-id="1bfd9-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="1bfd9-102">tooconnect toohello du moteur de base de données SQL Server à partir de hello Internet, créez un nom DNS pour votre adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="1bfd9-103">Vous pouvez vous connecter à l’adresse IP, mais hello nom DNS crée un enregistrement A qui est plus facile tooidentify et des résumés hello sous-jacent adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="1bfd9-104">Étiquettes de DNS ne sont pas requises si plan tooonly connecter toohello SQL Server de l’instance dans hello même réseau virtuel ou que localement.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="1bfd9-105">toocreate un nom DNS, sélectionnez d’abord **virtuels** dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="1bfd9-106">Sélectionnez votre toobring de machine virtuelle SQL Server ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="1bfd9-107">Dans la vue d’ensemble de la machine virtuelle hello, sélectionnez votre **adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![adresse IP publique](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="1bfd9-109">Dans Propriétés hello pour votre adresse IP publique, développez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="1bfd9-110">Entrez un nom DNS.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-110">Enter a DNS Label name.</span></span> <span data-ttu-id="1bfd9-111">Ce nom est un enregistrement A qui peut être utilisé tooconnect tooyour machine virtuelle SQL Server par un nom à la place de l’adresse IP directement.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="1bfd9-112">Cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-112">Click hello **Save** button.</span></span>

    ![nom dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="1bfd9-114">Se connecter toohello du moteur de base de données à partir d’un autre ordinateur</span><span class="sxs-lookup"><span data-stu-id="1bfd9-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="1bfd9-115">Sur un ordinateur connecté toohello internet, ouvrez SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="1bfd9-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="1bfd9-116">Si vous n’avez pas SQL Server Management Studio, vous pouvez le télécharger [ici](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="1bfd9-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="1bfd9-117">Bonjour **connecter tooServer** ou **connecter tooDatabase moteur** boîte de dialogue, modifier hello **nom du serveur** valeur.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="1bfd9-118">Entrez l’adresse IP de hello ou un nom DNS complet de l’ordinateur virtuel de hello (déterminée dans la tâche précédente hello).</span><span class="sxs-lookup"><span data-stu-id="1bfd9-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="1bfd9-119">Vous pouvez également ajouter une virgule et indiquer le port TCP du serveur SQL.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="1bfd9-120">Par exemple, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="1bfd9-121">Bonjour **authentification** boîte, sélectionnez **l’authentification SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="1bfd9-122">Bonjour **connexion** zone, entrez un nom hello d’une connexion SQL valide.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="1bfd9-123">Bonjour **mot de passe** boîte, un mot de passe hello type de connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="1bfd9-124">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="1bfd9-124">Click **Connect**.</span></span>

    ![connecter ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)