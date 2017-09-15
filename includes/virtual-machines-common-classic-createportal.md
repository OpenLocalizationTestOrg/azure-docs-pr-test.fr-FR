

<span data-ttu-id="d562c-101">Une machine virtuelle *personnalisée* correspond simplement à une machine virtuelle créée à l’aide d’une **Application recommandée** à partir de la **Place de marché**, car elle fait l’essentiel du travail à votre place.</span><span class="sxs-lookup"><span data-stu-id="d562c-101">A *custom* virtual machine simply means a virtual machine that you create using a **Featured app** from the **Marketplace** because it does much of the work for you.</span></span> <span data-ttu-id="d562c-102">Cependant, vous pouvez toujours effectuer des choix de configuration parmi les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d562c-102">Yet, you can still make configuration choices that include the following items:</span></span>

* <span data-ttu-id="d562c-103">Connecter la machine virtuelle à un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d562c-103">Connecting the virtual machine to a virtual network.</span></span>
* <span data-ttu-id="d562c-104">Installer l’agent de machine virtuelle et les extensions de machine virtuelle Azure, telles que l’extension anti-programme malveillant</span><span class="sxs-lookup"><span data-stu-id="d562c-104">Installing the Azure Virtual Machine Agent and Azure Virtual Machine Extensions, such as for antimalware.</span></span>
* <span data-ttu-id="d562c-105">Ajouter la machine virtuelle aux services cloud existants</span><span class="sxs-lookup"><span data-stu-id="d562c-105">Adding the virtual machine to existing cloud services.</span></span>
* <span data-ttu-id="d562c-106">Ajouter la machine virtuelle à un compte de stockage existant</span><span class="sxs-lookup"><span data-stu-id="d562c-106">Adding the virtual machine to an existing Storage account.</span></span>
* <span data-ttu-id="d562c-107">Ajouter la machine virtuelle à un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="d562c-107">Adding the virtual machine to an availability set.</span></span>

<!--
> [!IMPORTANT]
> If you want your virtual machine to use a virtual network so you can connect to it directly by host name or set up cross-premises connections, make sure that you specify the virtual network when you create the virtual machine. A virtual machine can be configured to join a virtual network only when you create the virtual machine. For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).
>
>
 -->

> [!IMPORTANT]
> <span data-ttu-id="d562c-108">si vous voulez que votre machine virtuelle utilise un réseau virtuel, assurez-vous de bien indiquer le réseau virtuel lorsque vous la créez.</span><span class="sxs-lookup"><span data-stu-id="d562c-108">If you want your virtual machine to use a virtual network, make sure that you specify the virtual network when you create the virtual machine.</span></span>

> * <span data-ttu-id="d562c-109">Il y a deux avantages à l’utilisation d’un réseau virtuel : se connecter directement à la machine virtuelle et configurer des connexions entre différents locaux.</span><span class="sxs-lookup"><span data-stu-id="d562c-109">Two benefits of using a virtual network are connecting directly to the virtual machine and to set up cross-premises connections.</span></span>

> * <span data-ttu-id="d562c-110">Vous pouvez configurer une machine virtuelle pour qu'elle rejoigne uniquement un réseau virtuel lorsque vous la créez.</span><span class="sxs-lookup"><span data-stu-id="d562c-110">A virtual machine can be configured to join a virtual network only when you create the virtual machine.</span></span> <span data-ttu-id="d562c-111">Pour plus d’informations sur les réseaux virtuels, consultez la page [Présentation du réseau virtuel Azure](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d562c-111">For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).</span></span>
>
>

## <a name="to-create-the-virtual-machine"></a><span data-ttu-id="d562c-112">Création de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d562c-112">To create the virtual machine</span></span>
