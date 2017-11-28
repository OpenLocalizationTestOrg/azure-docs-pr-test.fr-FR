## <a name="overview"></a><span data-ttu-id="ee2e2-101">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ee2e2-101">Overview</span></span>
<span data-ttu-id="ee2e2-102">Lorsque vous créez une machine virtuelle (VM) dans un groupe de ressources en déployant une image à partir d’ [Azure Marketplace](https://azure.microsoft.com/marketplace/), le lecteur du système d’exploitation par défaut est de 127 Go.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), the default OS drive is 127 GB.</span></span> <span data-ttu-id="ee2e2-103">Même s’il est possible d’ajouter des disques de données à la machine virtuelle (le nombre dépend de la référence (SKU) choisie) et de plus, il est recommandé d’installer les applications et les charges de travail intensives du processeur sur ces disques supplémentaires, il peut arriver que les clients doivent développer le lecteur du système d’exploitation pour prendre en charge certains scénarios, tels que les suivants :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-103">Even though it’s possible to add data disks to the VM (how many depending upon the SKU you’ve chosen) and moreover it’s recommended to install applications and CPU intensive workloads on these addendum disks, oftentimes customers need to expand the OS drive to support certain scenarios such as following:</span></span>

1. <span data-ttu-id="ee2e2-104">Prendre en charge les applications héritées qui installent des composants sur le lecteur du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="ee2e2-105">Migrer un ordinateur physique ou une machine virtuelle depuis un emplacement local avec un lecteur de système d’exploitation plus volumineux.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee2e2-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="ee2e2-107">Cet article traite de l’utilisation du modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-107">This article covers using the Resource Manager model.</span></span> <span data-ttu-id="ee2e2-108">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

## <a name="resize-the-os-drive"></a><span data-ttu-id="ee2e2-109">Redimensionner le lecteur du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="ee2e2-109">Resize the OS drive</span></span>
<span data-ttu-id="ee2e2-110">Dans cet article, nous allons exécuter la tâche consistant à redimensionner le lecteur du système d’exploitation à l’aide de modules Resource Manager d’ [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="ee2e2-110">In this article we’ll accomplish the task of resizing the OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="ee2e2-111">Ouvrez votre Powershell ISE ou une fenêtre Powershell en mode administrateur et suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-111">Open your Powershell ISE or Powershell window in administrative mode and follow the steps below:</span></span>

1. <span data-ttu-id="ee2e2-112">Connectez-vous à votre compte Microsoft Azure en mode de gestion des ressources et sélectionnez votre abonnement comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-112">Sign-in to your Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="ee2e2-113">Définissez le nom du groupe de ressources et le nom de la machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="ee2e2-114">Obtenez une référence à votre machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-114">Obtain a reference to your VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="ee2e2-115">Arrêtez la machine virtuelle avant de redimensionner le disque comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-115">Stop the VM before resizing the disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="ee2e2-116">Et voici le moment que nous attendions !</span><span class="sxs-lookup"><span data-stu-id="ee2e2-116">And here comes the moment we’ve been waiting for!</span></span> <span data-ttu-id="ee2e2-117">Définissez la taille du disque du système d’exploitation sur la valeur souhaitée et mettez à jour la machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-117">Set the size of the OS disk to the desired value and update the VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="ee2e2-118">La nouvelle taille doit être supérieure à la taille du disque actuelle.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-118">The new size should be greater than the existing disk size.</span></span> <span data-ttu-id="ee2e2-119">La valeur maximale autorisée est de 1 023 Go.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-119">The maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="ee2e2-120">La mise à jour de la machine virtuelle peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-120">Updating the VM may take a few seconds.</span></span> <span data-ttu-id="ee2e2-121">Une fois que l’exécution de la commande est terminée, redémarrez la machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-121">Once the command finishes executing, restart the VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="ee2e2-122">Vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-122">And that’s it!</span></span> <span data-ttu-id="ee2e2-123">Connectez-vous via RDP à la machine virtuelle, ouvrez Gestion de l’ordinateur (ou Gestion des disques) et développez le lecteur à l’aide de l’espace qui vient d’être alloué.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-123">Now RDP into the VM, open Computer Management (or Disk Management) and expand the drive using the newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="ee2e2-124">Résumé</span><span class="sxs-lookup"><span data-stu-id="ee2e2-124">Summary</span></span>
<span data-ttu-id="ee2e2-125">Dans cet article, nous avons utilisé les modules Azure Resource Manager de PowerShell pour développer le lecteur du système d’exploitation d’une machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-125">In this article, we used Azure Resource Manager modules of Powershell to expand the OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="ee2e2-126">Le script complet est indiqué ci-dessous, à titre de référence :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-126">Reproduced below is the complete script for your reference:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ee2e2-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ee2e2-127">Next Steps</span></span>
<span data-ttu-id="ee2e2-128">Bien que dans cet article, nous avons choisi de nous concentrer principalement sur l’expansion du disque du système d’exploitation de la machine virtuelle, le script développé peut également servir à développer les disques de données associés à la machine virtuelle en modifiant une seule ligne de code.</span><span class="sxs-lookup"><span data-stu-id="ee2e2-128">Though in this article, we focused primarily on expanding the OS disk of the VM, the developed script may also be used for expanding the data disks attached to the VM by changing a single line of code.</span></span> <span data-ttu-id="ee2e2-129">Par exemple, pour développer le premier disque de données associé à la machine virtuelle, remplacez l’objet ```OSDisk``` de ```StorageProfile``` par le tableau ```DataDisks``` et utilisez un index numérique pour obtenir une référence au premier disque de données associé, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-129">For example, to expand the first data disk attached to the VM, replace the ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index to obtain a reference to first attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="ee2e2-130">De même, vous pouvez référencer d’autres disques de données associés à la machine virtuelle, à l’aide d’un index comme indiqué ci-dessus ou à l’aide de la propriété ```Name``` du disque comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ee2e2-130">Similarly you may reference other data disks attached to the VM, either by using an index as shown above or the ```Name``` property of the disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="ee2e2-131">Si vous souhaitez savoir comment associer des disques à une machine virtuelle Azure Resource Manager, consultez cet [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ee2e2-131">If you want to find out how to attach disks to an Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

