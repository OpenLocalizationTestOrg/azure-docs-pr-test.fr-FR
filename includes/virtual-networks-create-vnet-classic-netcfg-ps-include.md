## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="2c21e-101">Comment toocreate un réseau virtuel à l’aide d’une configuration de réseau de fichiers à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c21e-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="2c21e-102">Azure utilise une toodefine de fichier xml abonnement de tooa disponibles tous les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="2c21e-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="2c21e-103">Vous pouvez télécharger ce fichier, toomodify le modifier ou supprimer des réseaux virtuels existants et créer de nouveaux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="2c21e-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="2c21e-104">Dans ce didacticiel, vous apprendrez comment toodownload ce fichier, appelée tooas fichier de configuration (ou netcfg) du réseau et le modifier toocreate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="2c21e-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="2c21e-105">toolearn en savoir plus sur le fichier de configuration de réseau hello, consultez hello [schéma de configuration de réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c21e-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="2c21e-106">toocreate un réseau virtuel avec un fichier netcfg à l’aide de PowerShell, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="2c21e-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="2c21e-107">Si vous n’avez jamais utilisé Azure PowerShell, hello terminé les étapes Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) de l’article, puis connectez-vous à tooAzure et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="2c21e-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="2c21e-108">À partir de la console Azure PowerShell hello, utilisez hello **Get-AzureVnetConfig** applet de commande toodownload hello configuration tooa répertoire de fichiers réseau sur votre ordinateur en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2c21e-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="2c21e-109">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="2c21e-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="2c21e-110">Ouvrir le fichier hello enregistré à l’étape 2 à l’aide de n’importe quelle application de l’éditeur XML ou texte et recherchez hello  **<VirtualNetworkSites>**  élément.</span><span class="sxs-lookup"><span data-stu-id="2c21e-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="2c21e-111">Si vous avez déjà créé des réseaux, chacun est affiché comme son propre élément **<VirtualNetworkSite>**.</span><span class="sxs-lookup"><span data-stu-id="2c21e-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="2c21e-112">réseau virtuel de toocreate hello décrite dans ce scénario, ajoutez hello XML suivant juste sous hello  **<VirtualNetworkSites>**  élément :</span><span class="sxs-lookup"><span data-stu-id="2c21e-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

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
   
5. <span data-ttu-id="2c21e-113">Enregistrez le fichier de configuration de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="2c21e-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="2c21e-114">À partir de la console Azure PowerShell hello, utilisez hello **Set-AzureVnetConfig** fichier de configuration de réseau applet de commande tooupload hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2c21e-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="2c21e-115">Sortie retournée :</span><span class="sxs-lookup"><span data-stu-id="2c21e-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="2c21e-116">Si **OperationStatus** n’est pas *Succeeded* Bonjour retourné de sortie, vérifiez à nouveau fichier xml de hello pour les erreurs et l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="2c21e-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="2c21e-117">À partir de la console Azure PowerShell hello, utilisez hello **Get-AzureVnetSite** tooverify d’applet de commande qui hello nouveau réseau a été ajouté en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2c21e-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="2c21e-118">Hello retourné sortie (abrégé) inclut hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="2c21e-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
