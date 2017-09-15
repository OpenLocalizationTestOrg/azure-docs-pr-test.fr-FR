
<br>

> [!NOTE]
> <span data-ttu-id="9ba19-101">Si un administrateur vous a donné un nom d’utilisateur et un mot de passe, il est probable que vous disposiez déjà d’un ID professionnel ou scolaire (parfois appelé *ID d’organisation*).</span><span class="sxs-lookup"><span data-stu-id="9ba19-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="9ba19-102">Dans ce cas, vous pouvez commencer à utiliser votre compte Azure immédiatement pour accéder aux ressources Azure qui requièrent l'utilisation d'un compte.</span><span class="sxs-lookup"><span data-stu-id="9ba19-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span></span> <span data-ttu-id="9ba19-103">Si vous constatez que vous ne pouvez pas utiliser ces ressources, vous devrez peut-être revenir à cet article pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="9ba19-103">If you find that you cannot use those resources, you may need to return to this article for help.</span></span> <span data-ttu-id="9ba19-104">Pour plus d’informations, consultez la section [Comptes que vous pouvez utiliser pour vous connecter](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) et [Association d’un abonnement Azure à Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="9ba19-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="9ba19-105">Les étapes sont simples.</span><span class="sxs-lookup"><span data-stu-id="9ba19-105">The steps are simple.</span></span> <span data-ttu-id="9ba19-106">Vous devez localiser votre identité de connexion sur le portail Azure Classic, découvrir votre domaine Azure Active Directory par défaut et y ajouter un nouvel utilisateur en tant que coadministrateur Azure.</span><span class="sxs-lookup"><span data-stu-id="9ba19-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a><span data-ttu-id="9ba19-107">Localisez votre répertoire par défaut sur le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="9ba19-107">Locate your default directory in the Azure classic portal</span></span>
<span data-ttu-id="9ba19-108">Commencez par vous connecter au [portail Azure Classic](https://manage.windowsazure.com) avec votre identité de compte Microsoft personnel.</span><span class="sxs-lookup"><span data-stu-id="9ba19-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="9ba19-109">Une fois que vous êtes connecté, faites défiler vers le bas le panneau bleu à gauche, puis cliquez sur **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="9ba19-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="9ba19-111">Commençons par rechercher des informations sur votre identité dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9ba19-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="9ba19-112">Des éléments semblables à ce qui suit doivent s'afficher dans le volet principal pour indiquer que vous avez un répertoire par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ba19-112">You should see something like the following in the main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="9ba19-113">Recherchons quelques informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9ba19-113">Let's find out some more information about it.</span></span> <span data-ttu-id="9ba19-114">Cliquez sur la ligne de répertoire par défaut pour afficher les propriétés de répertoire par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ba19-114">Click the default directory row, which brings you into the default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="9ba19-115">Pour afficher le nom de domaine par défaut, cliquez sur **DOMAINES**.</span><span class="sxs-lookup"><span data-stu-id="9ba19-115">To view the default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="9ba19-116">Ici, vous devez être en mesure de voir que, lors de la création du compte Azure, Azure Active Directory a créé un domaine personnel par défaut qui est une valeur de hachage (nombre généré à partir d’une chaîne de texte) de votre ID personnel utilisé en tant que sous-domaine de onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9ba19-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span></span> <span data-ttu-id="9ba19-117">C'est à ce domaine que vous allez maintenant ajouter un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ba19-117">That's the domain to which you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-the-default-domain"></a><span data-ttu-id="9ba19-118">Création d'un nouvel utilisateur dans le domaine par défaut</span><span class="sxs-lookup"><span data-stu-id="9ba19-118">Creating a new user in the default domain</span></span>
<span data-ttu-id="9ba19-119">Cliquez sur **UTILISATEURS** et recherchez votre compte personnel unique.</span><span class="sxs-lookup"><span data-stu-id="9ba19-119">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="9ba19-120">Vous devez voir dans la colonne **PROVENANCE** qu’il s’agit d’un **compte Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="9ba19-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="9ba19-121">Nous voulons créer un utilisateur dans votre domaine Azure Active Directory .onmicrosoft.com par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ba19-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="9ba19-122">Nous allons suivre [ces instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) dans les étapes suivantes, mais utiliser un exemple spécifique.</span><span class="sxs-lookup"><span data-stu-id="9ba19-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span></span>

<span data-ttu-id="9ba19-123">Au bas de la page, cliquez sur **+AJOUTER UN UTILISATEUR**.</span><span class="sxs-lookup"><span data-stu-id="9ba19-123">At the bottom of the page, click **+ADD USER**.</span></span> <span data-ttu-id="9ba19-124">Sur la page qui s’affiche, tapez le nouveau nom d’utilisateur et définissez **Type d’utilisateur** sur **Nouvel utilisateur dans votre organisation**.</span><span class="sxs-lookup"><span data-stu-id="9ba19-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="9ba19-125">Dans cet exemple, le nouveau nom d'utilisateur est `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="9ba19-125">In this example, the new user name is `ahmet`.</span></span> <span data-ttu-id="9ba19-126">Sélectionnez le domaine par défaut que vous avez découvert précédemment comme domaine pour l’adresse de messagerie d’ahmet.</span><span class="sxs-lookup"><span data-stu-id="9ba19-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span></span> <span data-ttu-id="9ba19-127">Lorsque vous avez terminé, cliquez sur la flèche Suivant.</span><span class="sxs-lookup"><span data-stu-id="9ba19-127">Click the next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="9ba19-128">Ajoutez d’autres détails pour Ahmet, mais veillez à sélectionner la valeur **RÔLE** appropriée.</span><span class="sxs-lookup"><span data-stu-id="9ba19-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span></span> <span data-ttu-id="9ba19-129">Il est facile d’utiliser la valeur **Administrateur général** pour vous assurer que tout fonctionne, mais nous vous conseillons d’utiliser un rôle inférieur.</span><span class="sxs-lookup"><span data-stu-id="9ba19-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="9ba19-130">Cet exemple utilise le rôle **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="9ba19-130">This example uses the **User** role.</span></span> <span data-ttu-id="9ba19-131">(Pour plus d’informations, consultez la section relative aux [autorisations des administrateurs par rôle](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) N’activez pas l’authentification multifacteur, sauf si vous souhaitez l’utiliser pour chaque journal de l’opération.</span><span class="sxs-lookup"><span data-stu-id="9ba19-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span></span> <span data-ttu-id="9ba19-132">Lorsque vous avez terminé, cliquez sur la flèche Suivant.</span><span class="sxs-lookup"><span data-stu-id="9ba19-132">Click the next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="9ba19-133">Cliquez sur le bouton **Créer** pour générer et afficher un mot de passe temporaire pour Ahmet.</span><span class="sxs-lookup"><span data-stu-id="9ba19-133">Click the **create** button to generate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="9ba19-134">Copiez l’adresse de messagerie du nom d’utilisateur, ou utilisez **ENVOYER UN MOT DE PASSE PAR MESSAGERIE ÉLECTRONIQUE**.</span><span class="sxs-lookup"><span data-stu-id="9ba19-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="9ba19-135">Vous aurez rapidement besoin des informations pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="9ba19-135">You'll need the information to log on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="9ba19-136">À présent, vous devez voir le nouvel utilisateur, **Ahmet le développeur**, provenant d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ba19-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="9ba19-137">Vous avez créé la nouvelle identité professionnelle ou scolaire avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ba19-137">You've created the new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="9ba19-138">Toutefois, cette identité ne dispose pas encore des autorisations pour utiliser les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9ba19-138">However, this identity does not yet have permissions to use Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="9ba19-139">Si vous utilisez **ENVOYER UN MOT DE PASSE PAR MESSAGERIE ÉLECTRONIQUE**, le type de message électronique suivant est envoyé.</span><span class="sxs-lookup"><span data-stu-id="9ba19-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="9ba19-140">Ajout de droits de co-administrateur Azure pour les abonnements</span><span class="sxs-lookup"><span data-stu-id="9ba19-140">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="9ba19-141">Vous devez maintenant ajouter le nouvel utilisateur en tant que co-administrateur de votre abonnement, afin que le nouvel utilisateur puisse se connecter au portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="9ba19-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span></span> <span data-ttu-id="9ba19-142">Pour ce faire, dans le panneau inférieur gauche, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="9ba19-142">To do this, in the lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="9ba19-143">Dans la zone principale des paramètres, cliquez sur **ADMINISTRATEURS** en haut et seule votre identité de compte Microsoft personnelle doit s'afficher.</span><span class="sxs-lookup"><span data-stu-id="9ba19-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="9ba19-144">Au bas de la page, cliquez sur **+AJOUTER** pour spécifier un co-administrateur.</span><span class="sxs-lookup"><span data-stu-id="9ba19-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span></span> <span data-ttu-id="9ba19-145">Ici, entrez l'adresse de messagerie du nouvel utilisateur que vous avez créé, y compris votre domaine par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ba19-145">Here, enter the email address of the new user you had created, including your default domain.</span></span> <span data-ttu-id="9ba19-146">Comme le montre la capture d’écran suivante, une coche verte est affichée en regard de l’utilisateur pour le répertoire par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ba19-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span></span> <span data-ttu-id="9ba19-147">N’oubliez pas de sélectionner tous les abonnements que vous souhaitez que cet utilisateur puisse gérer.</span><span class="sxs-lookup"><span data-stu-id="9ba19-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="9ba19-148">Lorsque vous avez terminé, vous devriez voir deux utilisateurs, y compris la nouvelle identité de votre co-administrateur.</span><span class="sxs-lookup"><span data-stu-id="9ba19-148">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="9ba19-149">Déconnectez-vous du portail.</span><span class="sxs-lookup"><span data-stu-id="9ba19-149">Log out of the portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a><span data-ttu-id="9ba19-150">Connexion et modification du mot de passe du nouvel utilisateur</span><span class="sxs-lookup"><span data-stu-id="9ba19-150">Logging in and changing the new user's password</span></span>
<span data-ttu-id="9ba19-151">Connectez-vous en tant que le nouvel utilisateur que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="9ba19-151">Log in as the new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="9ba19-152">Il vous sera immédiatement demandé de créer un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9ba19-152">You will immediately be prompted to create a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="9ba19-153">Votre réussite doit ressembler à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="9ba19-153">You should be rewarded with success that looks like the following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="9ba19-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ba19-154">Next steps</span></span>
<span data-ttu-id="9ba19-155">Vous pouvez maintenant vous servir de votre nouvelle identité Azure Active Directory pour utiliser des [modèles de groupe de ressources Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9ba19-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
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
