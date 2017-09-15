## <a name="how-to-create-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="2f2d4-101">Création d’un réseau virtuel à l’aide d’un fichier de configuration réseau à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f2d4-101">How to create a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="2f2d4-102">Azure utilise un fichier XML pour définir tous les réseaux virtuels disponibles pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="2f2d4-102">Azure uses an xml file to define all virtual networks available to a subscription.</span></span> <span data-ttu-id="2f2d4-103">Vous pouvez télécharger ce fichier, y apporter des changements pour modifier ou supprimer des réseaux virtuels existants, et en créer de nouveaux.</span><span class="sxs-lookup"><span data-stu-id="2f2d4-103">You can download this file, edit it to modify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="2f2d4-104">Dans ce didacticiel, vous découvrez comment télécharger ce fichier, appelé fichier de configuration réseau (ou netcfg), et le modifier pour créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="2f2d4-104">In this tutorial, you learn how to download this file, referred to as network configuration (or netcfg) file, and edit it to create a new virtual network.</span></span> <span data-ttu-id="2f2d4-105">Pour plus d’informations sur le fichier de configuration réseau, consultez la rubrique [Schéma de configuration du réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f2d4-105">To learn more about the network configuration file, see the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="2f2d4-106">Pour créer un réseau virtuel avec un fichier netcfg à l’aide de PowerShell, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f2d4-106">To create a virtual network with a netcfg file using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="2f2d4-107">Si vous n’avez jamais utilisé Azure PowerShell, procédez de la manière décrite dans l’article [Installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) puis connectez-vous à Azure et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="2f2d4-107">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in to Azure and select your subscription.</span></span>
2. <span data-ttu-id="2f2d4-108">Dans la console Azure PowerShell, utilisez la cmdlet **Get-AzureVnetConfig** pour télécharger le fichier de configuration réseau dans un répertoire de votre ordinateur en exécutant la commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2f2d4-108">From the Azure PowerShell console, use the **Get-AzureVnetConfig** cmdlet to download the network configuration file to a directory on your computer by running the following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="2f2d4-109">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="2f2d4-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="2f2d4-110">Ouvrez le fichier enregistré à l’étape 2 à l’aide d’un éditeur XML ou de texte quelconque, et recherchez l’élément **<VirtualNetworkSites>**.</span><span class="sxs-lookup"><span data-stu-id="2f2d4-110">Open the file you saved in step 2 using any XML or text editor application, and look for the **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="2f2d4-111">Si vous avez déjà créé des réseaux, chacun est affiché comme son propre élément **<VirtualNetworkSite>**.</span><span class="sxs-lookup"><span data-stu-id="2f2d4-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="2f2d4-112">Pour créer le réseau virtuel décrit dans ce scénario, ajoutez le code XML suivant juste sous l’élément **<VirtualNetworkSites>** :</span><span class="sxs-lookup"><span data-stu-id="2f2d4-112">To create the virtual network described in this scenario, add the following XML just under the **<VirtualNetworkSites>** element:</span></span>

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. <span data-ttu-id="2f2d4-113">Enregistrez le fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="2f2d4-113">Save the network configuration file.</span></span>
6. <span data-ttu-id="2f2d4-114">Dans la console Azure PowerShell, utilisez la cmdlet **Set-AzureVnetConfig** pour charger le fichier de configuration réseau en exécutant la commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2f2d4-114">From the Azure PowerShell console, use the **Set-AzureVnetConfig** cmdlet to upload the network configuration file by running the following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="2f2d4-115">Sortie retournée :</span><span class="sxs-lookup"><span data-stu-id="2f2d4-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="2f2d4-116">Si **OperationStatus** n’a pas la valeur *Succeeded* dans les résultats retournés, vérifiez les éventuelles erreurs dans le fichier XML et effectuez à nouveau l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="2f2d4-116">If **OperationStatus** is not *Succeeded* in the returned output, check the xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="2f2d4-117">Dans la console Azure PowerShell, utilisez la cmdlet **Get-AzureVnetSite** pour vérifier que le nouveau réseau a été ajouté en exécutant la commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2f2d4-117">From the Azure PowerShell console, use the **Get-AzureVnetSite** cmdlet to verify that the new network was added by running the following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="2f2d4-118">La sortie (abrégée) retournée contient le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="2f2d4-118">The returned (abbreviated) output includes the following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
