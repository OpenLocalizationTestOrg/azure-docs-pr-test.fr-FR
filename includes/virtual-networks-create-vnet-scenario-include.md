## <a name="scenario"></a><span data-ttu-id="e6bac-101">Scénario</span><span class="sxs-lookup"><span data-stu-id="e6bac-101">Scenario</span></span>
<span data-ttu-id="e6bac-102">toobetter illustrent comment toocreate un réseau virtuel et sous-réseaux, ce document Utilisez scénario hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e6bac-102">toobetter illustrate how toocreate a VNet and subnets, this document will use hello scenario below.</span></span>

![Scénario de réseau virtuel](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="e6bac-104">Dans ce scénario, vous allez créer un réseau virtuel nommé **TestVNet** avec un bloc CIDR réservé de **192.168.0.0./16**.</span><span class="sxs-lookup"><span data-stu-id="e6bac-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="e6bac-105">Votre réseau virtuel contiendra hello suivant sous-réseaux :</span><span class="sxs-lookup"><span data-stu-id="e6bac-105">Your VNet will contain hello following subnets:</span></span> 

* <span data-ttu-id="e6bac-106">**FrontEnd**, qui utilise **192.168.1.0/24** comme bloc CIDR.</span><span class="sxs-lookup"><span data-stu-id="e6bac-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="e6bac-107">**BackEnd**, qui utilise **192.168.2.0/24** comme bloc CIDR.</span><span class="sxs-lookup"><span data-stu-id="e6bac-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

