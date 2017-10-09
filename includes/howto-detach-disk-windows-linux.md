<span data-ttu-id="ac6e6-101">Lorsque vous n’avez plus besoin un disque de données est attachée tooa virtual machine, vous pouvez facilement la détacher.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="ac6e6-102">Détachement d’un disque supprime le disque de hello à partir de l’ordinateur virtuel de hello, mais ne supprime pas les disques hello de hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="ac6e6-103">Si vous souhaitez toouse hello données existantes hello disque à nouveau, vous pouvez rattacher il toohello même ordinateur virtuel ou un autre.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="ac6e6-104">toodetach un disque de système d’exploitation, vous devez tout d’abord toodelete hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="ac6e6-105">Trouver de disque de hello</span><span class="sxs-lookup"><span data-stu-id="ac6e6-105">Find hello disk</span></span>
<span data-ttu-id="ac6e6-106">Si vous ne connaissez nom hello de hello disque ou souhaitez tooverify avant de vous détacher, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="ac6e6-107">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac6e6-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ac6e6-108">Cliquez sur **virtuels**, et puis sélectionnez hello machine virtuelle appropriée.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="ac6e6-109">Cliquez sur **disques** le long de hello bord gauche du tableau de bord de machine virtuelle hello, sous **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="ac6e6-110">tableau de bord de machine virtuelle Hello répertorie le nom de hello et type de tous les disques attachés.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="ac6e6-111">Par exemple, cet écran affiche une machine virtuelle avec un disque de système d’exploitation et un disque de données :</span><span class="sxs-lookup"><span data-stu-id="ac6e6-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Rechercher un disque de données](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="ac6e6-113">Détacher un disque de hello</span><span class="sxs-lookup"><span data-stu-id="ac6e6-113">Detach hello disk</span></span>
1. <span data-ttu-id="ac6e6-114">À partir de hello portail Azure, cliquez sur **virtuels**, puis cliquez sur nom hello de machine virtuelle hello qui possède le disque de données hello souhaité toodetach.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="ac6e6-115">Cliquez sur **disques** le long de hello bord gauche du tableau de bord de machine virtuelle hello, sous **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="ac6e6-116">Cliquez sur le disque hello toodetach.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-116">Click hello disk you want toodetach.</span></span>

  ![Identifier hello disque toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="ac6e6-118">Dans la barre de commandes hello, cliquez sur **détachement**.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-118">From hello command bar, click **Detach**.</span></span>

  ![Recherchez hello detach, commande](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="ac6e6-120">Dans la fenêtre de confirmation hello, cliquez sur **Oui** disque de hello toodetach.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Confirmer le détachement du disque hello](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="ac6e6-122">disque de Hello reste dans le stockage, mais n’est plus attaché tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ac6e6-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
