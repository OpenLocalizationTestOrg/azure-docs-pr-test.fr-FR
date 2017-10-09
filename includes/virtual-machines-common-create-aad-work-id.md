
<br>

> [!NOTE]
> <span data-ttu-id="5ef6d-101">Si un administrateur vous a donné un nom d’utilisateur et un mot de passe, il est probable que vous disposiez déjà d’un ID professionnel ou scolaire (parfois appelé *ID d’organisation*).</span><span class="sxs-lookup"><span data-stu-id="5ef6d-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="5ef6d-102">Dans ce cas, vous pouvez commencer immédiatement toouse votre tooaccess compte Azure des ressources Azure qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="5ef6d-103">Si vous trouvez que vous ne pouvez pas utiliser ces ressources, vous devrez peut-être tooreturn toothis article d’aide.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="5ef6d-104">Pour plus d’informations, consultez [les comptes que vous pouvez utiliser pour se connecter](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) et [abonnement de la manière dont un Azure est connexe tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="5ef6d-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="5ef6d-105">étapes de Hello sont simples.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-105">hello steps are simple.</span></span> <span data-ttu-id="5ef6d-106">Vous devez toolocate votre signé identité Bonjour portail Azure classic, découvrir votre domaine d’Azure Active Directory par défaut et ajouter un nouveau tooit d’utilisateur en tant qu’un coadministrateur Azure.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="5ef6d-107">Recherchez le répertoire par défaut Bonjour portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="5ef6d-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="5ef6d-108">Commencez par la journalisation dans toohello [portail Azure classic](https://manage.windowsazure.com) avec votre identité de compte Microsoft personnelle.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="5ef6d-109">Après vous être connecté, faites défiler panneau hello bleu sur hello côté gauche vers le bas et cliquez sur **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="5ef6d-111">Commençons par rechercher des informations sur votre identité dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="5ef6d-112">Vous devez voir quelque chose comme hello suivant dans le volet principal de hello, indiquant que vous disposez d’un répertoire par défaut.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="5ef6d-113">Recherchons quelques informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-113">Let's find out some more information about it.</span></span> <span data-ttu-id="5ef6d-114">Cliquez sur ligne hello par défaut active, ce qui vous permet de propriétés du répertoire par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="5ef6d-115">nom de domaine par défaut tooview hello, cliquez sur **domaines**.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="5ef6d-116">Ici, vous devez être en mesure de toosee lors de la création de hello compte Azure, Azure Active Directory créé un domaine personnel par défaut qui est une valeur de hachage (un nombre généré à partir d’une chaîne de texte) de votre ID personnel utilisé comme un sous-domaine de onmicrosoft.com. Qui est toowhich de domaine hello vous allez maintenant ajouter un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="5ef6d-117">Création d’un utilisateur dans le domaine par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="5ef6d-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="5ef6d-118">Cliquez sur **UTILISATEURS** et recherchez votre compte personnel unique.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="5ef6d-119">Vous devez voir Bonjour **provenance** colonne qu’il est un **compte Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="5ef6d-120">Nous souhaitons toocreate un utilisateur dans la valeur par défaut. domaine Azure Active Directory de onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="5ef6d-121">Nous allons toofollow [ces instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) dans hello lors des étapes suivantes, mais utiliser un exemple spécifique.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="5ef6d-122">Au bas de hello de page de hello, cliquez sur **+ ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="5ef6d-123">Dans la page hello qui s’affiche, tapez le nouveau nom d’utilisateur hello et rendre hello **Type d’utilisateur** un **nouvel utilisateur dans votre organisation**.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="5ef6d-124">Dans cet exemple, le nouveau nom d’utilisateur hello est `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="5ef6d-125">Sélectionnez le domaine par défaut hello que vous avez découvert précédemment en tant que domaine hello pour l’adresse de messagerie du ahmet.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="5ef6d-126">Cliquez sur hello la flèche suivante une fois.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="5ef6d-127">Ajoutez plus de détails pour Ahmet, mais assurez-vous que tooselect hello approprié **rôle** valeur.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="5ef6d-128">Il est facile toouse **administrateur Global** toomake que cela fonctionne, mais si vous pouvez utiliser un rôle plus petit, qui est une bonne idée.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="5ef6d-129">Cet exemple utilise hello **utilisateur** rôle.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-129">This example uses hello **User** role.</span></span> <span data-ttu-id="5ef6d-130">(Pour plus d’informations, consultez la section relative aux [autorisations des administrateurs par rôle](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) N’activez pas l’authentification multifacteur, sauf si vous souhaitez que l’authentification multifacteur toouse pour chaque journal dans l’opération.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="5ef6d-131">Lorsque vous avez terminé, cliquez sur flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="5ef6d-132">Cliquez sur hello **créer** bouton toogenerate et afficher un mot de passe temporaire pour Ahmet.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="5ef6d-133">Copier l’adresse de messagerie hello user name, ou utiliser **envoyer un message électronique de mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="5ef6d-134">Vous devez hello informations toolog sur peu de temps.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="5ef6d-135">Maintenant vous devriez voir hello nouvel utilisateur **Ahmet hello développeur**, Corée d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="5ef6d-136">Vous avez créé le nouveau travail de hello ou l’identité de l’établissement scolaire avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="5ef6d-137">Toutefois, cette identité n’a pas encore autorisations toouse Azure ressources.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="5ef6d-138">Si vous utilisez **envoyer un message électronique de mot de passe**, hello suivant le type de courrier électronique est envoyé.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="5ef6d-139">Ajout de droits de co-administrateur Azure pour les abonnements</span><span class="sxs-lookup"><span data-stu-id="5ef6d-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="5ef6d-140">Vous devez maintenant utilisateur tooadd hello en tant que coadministrateur de votre abonnement pour la connexion utilisateur hello dans toohello portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="5ef6d-141">toodo, dans le panneau inférieur gauche de hello cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="5ef6d-142">Dans la zone de paramètres principaux hello, cliquez sur **administrateurs** à hello haut et que vous devez voir seulement votre identité du compte Microsoft personnelle.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="5ef6d-143">Au bas de hello de page de hello, cliquez sur **+ ajouter** toospecify un coadministrateur.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="5ef6d-144">Saisir une adresse de messagerie hello du hello nouvel utilisateur que vous avez créé, y compris votre domaine par défaut.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="5ef6d-145">Comme indiqué dans la capture d’écran suivante de hello, une coche verte apparaît utilisateur toohello suivant hello répertoire par défaut.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="5ef6d-146">N’oubliez pas de tooselect tous les abonnements hello que vous souhaitez que cette tooadminister en mesure de toobe utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="5ef6d-147">Lorsque vous avez terminé, vous devriez voir deux utilisateurs, y compris la nouvelle identité de votre co-administrateur.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="5ef6d-148">Déconnectez-vous de portail de hello.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="5ef6d-149">Connexion et la modification de mot de passe hello du nouvel utilisateur</span><span class="sxs-lookup"><span data-stu-id="5ef6d-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="5ef6d-150">Ouvrez une session en tant qu’utilisateur de nouvelle hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="5ef6d-151">Vous verrez alors immédiatement toocreate invité à un nouveau mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="5ef6d-152">Vous devez être récompensé avec succès qui ressemble à hello suivant.</span><span class="sxs-lookup"><span data-stu-id="5ef6d-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="5ef6d-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ef6d-153">Next steps</span></span>
<span data-ttu-id="5ef6d-154">Vous pouvez maintenant utiliser votre nouveau toouse d’identité Azure Active Directory [modèles de groupe de ressources Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5ef6d-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
