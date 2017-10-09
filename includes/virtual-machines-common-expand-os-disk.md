## <a name="overview"></a><span data-ttu-id="bcdb0-101">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bcdb0-101">Overview</span></span>
<span data-ttu-id="bcdb0-102">Lorsque vous créez un nouvel ordinateur virtuel (VM) dans un groupe de ressources en déployant une image à partir de [Azure Marketplace](https://azure.microsoft.com/marketplace/), lecteur de système d’exploitation hello par défaut est de 127 Go.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="bcdb0-103">Même si elle est toohello de disques de données tooadd possible VM (selon le nombre hello référence (SKU) que vous avez choisie) et plus il est recommandé tooinstall applications et charges de travail intensives du processeur sur ces disques addenda, les clients doivent souvent tooexpand hello du système d’exploitation lecteur toosupport certains scénarios tels que les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="bcdb0-104">Prendre en charge les applications héritées qui installent des composants sur le lecteur du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="bcdb0-105">Migrer un ordinateur physique ou une machine virtuelle depuis un emplacement local avec un lecteur de système d’exploitation plus volumineux.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcdb0-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="bcdb0-107">Cet article décrit à l’aide du modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="bcdb0-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="bcdb0-109">Redimensionner le lecteur de hello du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="bcdb0-109">Resize hello OS drive</span></span>
<span data-ttu-id="bcdb0-110">Dans cet article nous allons faire hello de redimensionnement lecteur hello du système d’exploitation à l’aide des modules de gestionnaire de ressources de [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="bcdb0-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="bcdb0-111">Ouvrez votre fenêtre Powershell ou Powershell ISE en mode administrateur et suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="bcdb0-112">Connectez-vous tooyour Microsoft Azure dans le mode de gestion des ressources de compte et sélectionnez votre abonnement comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="bcdb0-113">Définissez le nom du groupe de ressources et le nom de la machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="bcdb0-114">Obtenir une référence de tooyour machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="bcdb0-115">Arrêter hello machine virtuelle avant de redimensionner le disque de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="bcdb0-116">Et ici proviennent moment hello que nous avons attend !</span><span class="sxs-lookup"><span data-stu-id="bcdb0-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="bcdb0-117">Définir la taille de valeur de hello du système d’exploitation disque toohello souhaité hello et mettre à jour de hello machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="bcdb0-118">Hello nouvelle taille doit être supérieure à la taille du disque existant hello.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="bcdb0-119">Hello maximale autorisée est de 1 023 go.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="bcdb0-120">Mise à jour hello machine virtuelle peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="bcdb0-121">Une fois la commande hello fin d’exécution, redémarrez hello machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="bcdb0-122">Vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-122">And that’s it!</span></span> <span data-ttu-id="bcdb0-123">Maintenant RDP dans hello machine virtuelle, ouvrez Gestion de l’ordinateur (ou de gestion des disques) et développez le lecteur hello hello qui vient d’être l’espace alloué à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="bcdb0-124">Résumé</span><span class="sxs-lookup"><span data-stu-id="bcdb0-124">Summary</span></span>
<span data-ttu-id="bcdb0-125">Dans cet article, nous avons utilisé les modules Powershell tooexpand Hello lecteur du système d’exploitation d’une machine virtuelle IaaS Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="bcdb0-126">Reproduite ci-dessous est complète du script hello de référence :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-126">Reproduced below is hello complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="bcdb0-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcdb0-127">Next Steps</span></span>
<span data-ttu-id="bcdb0-128">Bien que dans cet article, nous principalement sur l’expansion de disque hello du système d’exploitation de machine virtuelle de hello, hello développé script peut également être utilisé pour le développement hello données disques attachés toohello machine virtuelle en modifiant une seule ligne de code.</span><span class="sxs-lookup"><span data-stu-id="bcdb0-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="bcdb0-129">Par exemple, tooexpand hello commencez par les données de disque attaché toohello machine virtuelle, remplacez hello ```OSDisk``` objet de ```StorageProfile``` avec ```DataDisks``` de tableau et utilisez un tooobtain index numérique un disque de données attaché toofirst de référence, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="bcdb0-130">De même vous pouvez référencer d’autres disques de données attaché toohello machine virtuelle, à l’aide d’un index comme indiqué ci-dessus ou hello ```Name``` propriété du disque hello comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bcdb0-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="bcdb0-131">Si vous souhaitez toofind out comment tooattach disques tooan Azure Resource Manager VM, activez cette option [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bcdb0-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

