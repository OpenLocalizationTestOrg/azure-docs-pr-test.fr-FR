<span data-ttu-id="bec16-101">Lorsque vous n’avez plus besoin d’un disque de données qui est attaché à une machine virtuelle, vous pouvez le détacher facilement.</span><span class="sxs-lookup"><span data-stu-id="bec16-101">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="bec16-102">Détacher un disque supprime le disque de la machine virtuelle, mais ne supprime pas le disque du compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="bec16-102">Detaching a disk removes the disk from the virtual machine, but doesn't delete the disk from the Azure storage account.</span></span>

<span data-ttu-id="bec16-103">Si vous souhaitez réutiliser les données du disque, vous pouvez l’attacher à la même machine virtuelle ou à une autre.</span><span class="sxs-lookup"><span data-stu-id="bec16-103">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="bec16-104">Pour détacher un disque de système d’exploitation, vous devez tout d’abord supprimer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bec16-104">To detach an operating system disk, you first need to delete the virtual machine.</span></span>
>

## <a name="find-the-disk"></a><span data-ttu-id="bec16-105">Recherche du disque</span><span class="sxs-lookup"><span data-stu-id="bec16-105">Find the disk</span></span>
<span data-ttu-id="bec16-106">Si vous ne connaissez pas le nom du disque ou souhaitez le vérifier avant de le détacher, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="bec16-106">If you don't know the name of the disk or want to verify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="bec16-107">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bec16-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bec16-108">Cliquez sur **Machines virtuelles**, puis sélectionnez la machine virtuelle appropriée.</span><span class="sxs-lookup"><span data-stu-id="bec16-108">Click **Virtual Machines**, and then select the appropriate VM.</span></span>

3. <span data-ttu-id="bec16-109">Cliquez sur **Disques** sur le bord gauche du tableau de bord de la machine virtuelle, sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bec16-109">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="bec16-110">Ce tableau de bord de machine virtuelle répertorie le nom et le type de tous les disques attachés.</span><span class="sxs-lookup"><span data-stu-id="bec16-110">The virtual machine dashboard lists the name and type of all attached disks.</span></span> <span data-ttu-id="bec16-111">Par exemple, cet écran affiche une machine virtuelle avec un disque de système d’exploitation et un disque de données :</span><span class="sxs-lookup"><span data-stu-id="bec16-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Rechercher un disque de données](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-the-disk"></a><span data-ttu-id="bec16-113">Détachement du disque</span><span class="sxs-lookup"><span data-stu-id="bec16-113">Detach the disk</span></span>
1. <span data-ttu-id="bec16-114">À partir du portail Azure, cliquez sur **Machines virtuelles**, sur le nom de la machine virtuelle qui comporte le disque de données que vous souhaitez détacher.</span><span class="sxs-lookup"><span data-stu-id="bec16-114">From the Azure portal, click **Virtual Machines**, and then click the name of the virtual machine that has the data disk you want to detach.</span></span>

2. <span data-ttu-id="bec16-115">Cliquez sur **Disques** sur le bord gauche du tableau de bord de la machine virtuelle, sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bec16-115">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="bec16-116">Cliquez sur le disque que vous souhaitez détacher.</span><span class="sxs-lookup"><span data-stu-id="bec16-116">Click the disk you want to detach.</span></span>

  ![Identification du disque à détacher](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="bec16-118">Dans la barre de commandes, cliquez sur **Détacher**.</span><span class="sxs-lookup"><span data-stu-id="bec16-118">From the command bar, click **Detach**.</span></span>

  ![Localiser la commande de détachement](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="bec16-120">Dans la fenêtre de confirmation, cliquez sur **Oui** pour détacher le disque.</span><span class="sxs-lookup"><span data-stu-id="bec16-120">In the confirmation window, click **Yes** to detach the disk.</span></span>

  ![Confirmation du détachement du disque](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="bec16-122">Le disque reste dans le stockage, mais il n’est plus attaché à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bec16-122">The disk remains in storage but is no longer attached to a virtual machine.</span></span>
