---
title: comptes de stockage Azure pile aaaManage | Documents Microsoft
description: "Découvrez comment toofind, gérer, restaurer et récupérer des comptes de stockage Azure pile"
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 350c92d6b5ce9b1582ede0256c4d3d23bdd94901
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="47456-103">Gérer les comptes de stockage dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="47456-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="47456-104">Découvrez comment toomanage les comptes de stockage dans Azure pile toofind, restaurer et récupérer de la capacité de stockage en fonction des besoins de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="47456-104">Learn how toomanage storage accounts in Azure Stack toofind, recover, and reclaim storage capacity based on business needs.</span></span>

## <span data-ttu-id="47456-105"><a name="find"></a>Rechercher un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="47456-105"><a name="find"></a>Find a storage account</span></span>
<span data-ttu-id="47456-106">liste Hello de comptes de stockage dans la région de hello peut être affichée dans la pile Azure par :</span><span class="sxs-lookup"><span data-stu-id="47456-106">hello list of storage accounts in hello region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="47456-107">Dans un navigateur Internet, accédez à https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="47456-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="47456-108">Se connecter toohello portail d’administration Azure pile comme un opérateur cloud (en utilisant les informations d’identification que vous avez fourni pendant le déploiement)</span><span class="sxs-lookup"><span data-stu-id="47456-108">Sign in toohello Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="47456-109">Sur le tableau de bord par défaut hello – recherche hello **gestion de la région** liste et cliquez sur la zone hello tooexplore.</span><span class="sxs-lookup"><span data-stu-id="47456-109">On hello default dashboard – find hello **Region management** list and click hello region you want tooexplore.</span></span> <span data-ttu-id="47456-110">Par exemple **(local**).</span><span class="sxs-lookup"><span data-stu-id="47456-110">For example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="47456-111">Sélectionnez **stockage** de hello **fournisseurs de ressources** liste.</span><span class="sxs-lookup"><span data-stu-id="47456-111">Select **Storage** from hello **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="47456-112">Désormais, dans Panneau d’administrateur de fournisseur de ressources de stockage de hello – défiler hello **comptes de stockage** onglet et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="47456-112">Now, on hello storage Resource Provider administrator blade – scroll down to hello **Storage accounts** tab and click it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="47456-113">page résultante de Hello est liste hello de comptes de stockage dans cette région.</span><span class="sxs-lookup"><span data-stu-id="47456-113">hello resulting page is hello list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="47456-114">Par défaut, hello 10 premiers comptes sont affichés.</span><span class="sxs-lookup"><span data-stu-id="47456-114">By default, hello first 10 accounts are displayed.</span></span> <span data-ttu-id="47456-115">Vous pouvez choisir toofetch plus en cliquant sur hello **davantage** lien en bas de hello de liste de hello.</span><span class="sxs-lookup"><span data-stu-id="47456-115">You can choose toofetch more by clicking hello  **Load more** link at hello bottom of hello list.</span></span>

<span data-ttu-id="47456-116">OU</span><span class="sxs-lookup"><span data-stu-id="47456-116">OR</span></span>

<span data-ttu-id="47456-117">Si vous êtes intéressé par un compte de stockage spécifique – vous pouvez **filtre et fetch hello comptes appropriés** uniquement.</span><span class="sxs-lookup"><span data-stu-id="47456-117">If you are interested in a particular storage account – you can **filter and fetch hello relevant accounts** only.</span></span>


<span data-ttu-id="47456-118">**toofilter pour les comptes :**</span><span class="sxs-lookup"><span data-stu-id="47456-118">**toofilter for accounts:**</span></span>

1. <span data-ttu-id="47456-119">Cliquez sur **filtre** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="47456-119">Click **Filter** at hello top of hello blade.</span></span>
2. <span data-ttu-id="47456-120">Dans Panneau de filtre hello, il vous permet de toospecify **nom de compte**, **ID d’abonnement** ou **état** liste de hello ajuster les toofine de stockage comptes toobe affiché.</span><span class="sxs-lookup"><span data-stu-id="47456-120">On hello Filter blade, it allows you toospecify **account name**, **subscription ID** or **status** toofine-tune hello list of storage accounts toobe displayed.</span></span> <span data-ttu-id="47456-121">Utilisez-les pour filtrer selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="47456-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="47456-122">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="47456-122">Click **Update**.</span></span> <span data-ttu-id="47456-123">liste de Hello doit actualiser en conséquence.</span><span class="sxs-lookup"><span data-stu-id="47456-123">hello list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="47456-124">filtre de hello tooreset : cliquez sur **filtre**, effacer les sélections et mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="47456-124">tooreset hello filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="47456-125">zone de texte Rechercher Hello (en haut de hello du Panneau de liste de comptes de stockage hello) vous permet de mettre en surbrillance le texte hello sélectionné dans la liste hello de comptes.</span><span class="sxs-lookup"><span data-stu-id="47456-125">hello search text box (on hello top of hello storage accounts list blade) lets you highlight hello selected text in hello list of accounts.</span></span> <span data-ttu-id="47456-126">Cela est très pratique dans les cas de hello lors de l’id ou nom complet de hello n’est pas facilement disponible.</span><span class="sxs-lookup"><span data-stu-id="47456-126">This is really handy in hello case when hello full name or id is not easily available.</span></span>

<span data-ttu-id="47456-127">Vous pouvez utiliser du texte libre ici, retrouvez toohelp compte hello vous intéressez.</span><span class="sxs-lookup"><span data-stu-id="47456-127">You can use free text here toohelp find hello account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="47456-128">Accéder aux détails du compte</span><span class="sxs-lookup"><span data-stu-id="47456-128">Look at account details</span></span>
<span data-ttu-id="47456-129">Une fois que vous avez localisé comptes hello que vous intéressez, vous pouvez cliquer hello compte particulier tooview certains détails.</span><span class="sxs-lookup"><span data-stu-id="47456-129">Once you have located hello accounts you are interested in viewing, you can click hello particular account tooview certain details.</span></span> <span data-ttu-id="47456-130">Un nouveau panneau s’ouvre avec les détails du compte hello telles que : hello du type de compte de hello, heure de création, l’emplacement, etc..</span><span class="sxs-lookup"><span data-stu-id="47456-130">A new blade opens with hello account details such as: hello type of hello account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="47456-131">Récupérer un compte supprimé</span><span class="sxs-lookup"><span data-stu-id="47456-131">Recover a deleted account</span></span>
<span data-ttu-id="47456-132">Vous pouvez être dans une situation où vous avez besoin de toorecover un compte supprimé.</span><span class="sxs-lookup"><span data-stu-id="47456-132">You may be in a situation where you need toorecover a deleted account.</span></span>

<span data-ttu-id="47456-133">Dans la pile d’Azure, il existe un moyen très simple de toodo qui :</span><span class="sxs-lookup"><span data-stu-id="47456-133">In Azure Stack there is a very simple way toodo that:</span></span>

1. <span data-ttu-id="47456-134">Parcourir la liste de comptes de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="47456-134">Browse toohello storage accounts list.</span></span> <span data-ttu-id="47456-135">Pour plus d’informations, consultez [Rechercher un compte de stockage](#find) dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="47456-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="47456-136">Recherchez ce compte dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="47456-136">Locate that particular account in hello list.</span></span> <span data-ttu-id="47456-137">Vous devrez peut-être toofilter.</span><span class="sxs-lookup"><span data-stu-id="47456-137">You may need toofilter.</span></span>
3. <span data-ttu-id="47456-138">Vérifiez hello *état* du compte de hello.</span><span class="sxs-lookup"><span data-stu-id="47456-138">Check hello *state* of hello account.</span></span> <span data-ttu-id="47456-139">Il doit être **Supprimé**.</span><span class="sxs-lookup"><span data-stu-id="47456-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="47456-140">Cliquez sur le compte hello qui ouvre le panneau des détails du compte hello.</span><span class="sxs-lookup"><span data-stu-id="47456-140">Click hello account which opens hello account details blade.</span></span>
5. <span data-ttu-id="47456-141">Au-dessus de ce panneau, recherchez hello **récupérer** bouton et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="47456-141">On top of this blade, locate hello **Recover** button and click it.</span></span>
6. <span data-ttu-id="47456-142">Cliquez sur **Oui** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="47456-142">Click **Yes** tooconfirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="47456-143">récupération de Hello est maintenant en *traiter... Patientez* pour obtenir une indication si elle a réussi.</span><span class="sxs-lookup"><span data-stu-id="47456-143">hello recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="47456-144">Vous pouvez également cliquez sur hello « cloche » en haut hello du portail hello pour afficher des indications de progression.</span><span class="sxs-lookup"><span data-stu-id="47456-144">You can also click hello “bell” icon at hello top of hello portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="47456-145">Une fois hello récupérée compte est correctement synchronisé, il peut être utilisé à nouveau.</span><span class="sxs-lookup"><span data-stu-id="47456-145">Once hello recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="47456-146">Quelques astuces</span><span class="sxs-lookup"><span data-stu-id="47456-146">Some Gotchas</span></span>
* <span data-ttu-id="47456-147">Votre compte supprimé affiche un état **hors conservation**.</span><span class="sxs-lookup"><span data-stu-id="47456-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="47456-148">Cela signifie que le compte de hello supprimé a dépassé la période de rétention hello et qu’il ne peut pas être récupérée.</span><span class="sxs-lookup"><span data-stu-id="47456-148">This means that hello deleted account has exceeded hello retention period and may not be recoverable.</span></span>
* <span data-ttu-id="47456-149">Votre compte supprimé n’affiche pas dans la liste des comptes hello.</span><span class="sxs-lookup"><span data-stu-id="47456-149">Your deleted account does not show in hello accounts list.</span></span>
  
  <span data-ttu-id="47456-150">Cela peut signifier que les comptes de hello supprimé a déjà été par le garbage collecté.</span><span class="sxs-lookup"><span data-stu-id="47456-150">This could mean that hello deleted account has already been garbage collected.</span></span> <span data-ttu-id="47456-151">Dans ce cas, il ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="47456-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="47456-152">Consultez [Récupérer de la capacité](#reclaim) dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="47456-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-hello-retention-period"></a><span data-ttu-id="47456-153">Définir la période de rétention hello</span><span class="sxs-lookup"><span data-stu-id="47456-153">Set hello retention period</span></span>
<span data-ttu-id="47456-154">définition de période de rétention Hello permet un toospecify d’opérateur de nuage une période en jours (entre 0 et 9 999 jours) pendant le n’importe quel compte supprimé peut potentiellement être récupéré.</span><span class="sxs-lookup"><span data-stu-id="47456-154">hello retention period setting allows a cloud operator toospecify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="47456-155">Hello période de rétention par défaut a la valeur too15 jours.</span><span class="sxs-lookup"><span data-stu-id="47456-155">hello default retention period is set too15 days.</span></span> <span data-ttu-id="47456-156">Hello valeur trop « 0 » signifie que n’importe quel compte supprimé est immédiatement en dehors de la rétention et marqué pour un garbage collection périodique.</span><span class="sxs-lookup"><span data-stu-id="47456-156">Setting hello value too“0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="47456-157">**période de rétention toochange hello :**</span><span class="sxs-lookup"><span data-stu-id="47456-157">**toochange hello retention period:**</span></span>

1. <span data-ttu-id="47456-158">Dans un navigateur Internet, accédez à https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="47456-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="47456-159">Se connecter toohello portail d’administration Azure pile comme un opérateur cloud (en utilisant les informations d’identification que vous avez fourni pendant le déploiement)</span><span class="sxs-lookup"><span data-stu-id="47456-159">Sign in toohello Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="47456-160">Sur le tableau de bord par défaut hello – recherche hello **gestion de la région** liste et cliquez sur la région de hello souhaité tooexplore – par exemple **(local**).</span><span class="sxs-lookup"><span data-stu-id="47456-160">On hello default dashboard – find hello **Region management** list and click hello region you want tooexplore – for example **(local**).</span></span>
4. <span data-ttu-id="47456-161">Sélectionnez **stockage** de hello **fournisseurs de ressources** liste.</span><span class="sxs-lookup"><span data-stu-id="47456-161">Select **Storage** from hello **Resource Providers** list.</span></span>
5. <span data-ttu-id="47456-162">Cliquez sur **paramètres** au panneau de configuration hello hello tooopen supérieur.</span><span class="sxs-lookup"><span data-stu-id="47456-162">Click **Settings** at hello top tooopen hello setting blade.</span></span>
6. <span data-ttu-id="47456-163">Cliquez sur **Configuration** puis modifiez la valeur de période de rétention hello.</span><span class="sxs-lookup"><span data-stu-id="47456-163">Click **Configuration** then edit hello retention period value.</span></span>

   <span data-ttu-id="47456-164">Définir hello nombre de jours et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="47456-164">Set hello number of days and then save it.</span></span>
   
   <span data-ttu-id="47456-165">Cette valeur est prise en compte immédiatement et est appliquée à toute votre région.</span><span class="sxs-lookup"><span data-stu-id="47456-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <span data-ttu-id="47456-166"><a name="reclaim"></a>Récupérer de la capacité</span><span class="sxs-lookup"><span data-stu-id="47456-166"><a name="reclaim"></a>Reclaim capacity</span></span>
<span data-ttu-id="47456-167">Un des effets secondaires hello d’avoir une période de rétention est qu’un compte supprimé continue tooconsume capacité jusqu'à ce qu’il s’agit de la période de rétention hello.</span><span class="sxs-lookup"><span data-stu-id="47456-167">One of hello side effects of having a retention period is that a deleted account continues tooconsume capacity until it comes out of hello retention period.</span></span> <span data-ttu-id="47456-168">Comme un cloud opérateur, vous devrez peut-être un Bonjour tooreclaim de façon supprimé espace du compte même si la période de rétention hello n’a pas encore expiré.</span><span class="sxs-lookup"><span data-stu-id="47456-168">As a cloud operator you may need a way tooreclaim hello deleted account space even though hello retention period has not yet expired.</span></span>

<span data-ttu-id="47456-169">Vous pouvez récupérer de la capacité à l’aide du portail de hello ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47456-169">You can reclaim capacity using either hello portal or PowerShell.</span></span>

<span data-ttu-id="47456-170">**capacité de tooreclaim à l’aide du portail de hello :**</span><span class="sxs-lookup"><span data-stu-id="47456-170">**tooreclaim capacity using hello portal:**</span></span>
1. <span data-ttu-id="47456-171">Accédez à panneau de comptes de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="47456-171">Navigate toohello storage accounts blade.</span></span> <span data-ttu-id="47456-172">Consultez [Rechercher un compte de stockage](#find).</span><span class="sxs-lookup"><span data-stu-id="47456-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="47456-173">Cliquez sur **récupérer de l’espace** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="47456-173">Click **Reclaim space** at hello top of hello blade.</span></span>
3. <span data-ttu-id="47456-174">Lire le message de type hello et puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="47456-174">Read hello message and then click **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="47456-175">Attendez l’icône représentant une cloche de réussite notification voir hello sur le portail hello.</span><span class="sxs-lookup"><span data-stu-id="47456-175">Wait for success notification See hello bell icon on hello portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="47456-176">Actualisez la page comptes de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="47456-176">Refresh hello Storage accounts page.</span></span> <span data-ttu-id="47456-177">les comptes Hello supprimé n’apparaissent plus dans la liste de hello, car ils ont été purgées.</span><span class="sxs-lookup"><span data-stu-id="47456-177">hello deleted accounts are no longer shown in hello list because they have been purged.</span></span>

<span data-ttu-id="47456-178">Vous pouvez également utiliser la période de rétention PowerShell tooexplicitly remplacement hello et récupérer immédiatement de la capacité.</span><span class="sxs-lookup"><span data-stu-id="47456-178">You can also use PowerShell tooexplicitly override hello retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="47456-179">**capacité de tooreclaim à l’aide de PowerShell :**</span><span class="sxs-lookup"><span data-stu-id="47456-179">**tooreclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="47456-180">Vérifiez qu’Azure PowerShell est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="47456-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="47456-181">Si ce n’est pas le cas, utilisez hello suivant les instructions :</span><span class="sxs-lookup"><span data-stu-id="47456-181">If not, use hello following instructions:</span></span> 
   * <span data-ttu-id="47456-182">tooinstall hello version la plus récente d’Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="47456-182">tooinstall hello latest Azure PowerShell version and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="47456-183">Pour plus d’informations sur les applets de commande Azure Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="47456-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="47456-184">Exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="47456-184">Run hello following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="47456-185">Si vous exécutez cette applet de commande vous supprimez définitivement le compte de hello et son contenu.</span><span class="sxs-lookup"><span data-stu-id="47456-185">If you run this cmdlet you permanently delete hello account and its contents.</span></span> <span data-ttu-id="47456-186">Il n’est pas récupérable.</span><span class="sxs-lookup"><span data-stu-id="47456-186">It is not recoverable.</span></span> <span data-ttu-id="47456-187">Utilisez cette option avec précaution.</span><span class="sxs-lookup"><span data-stu-id="47456-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="47456-188">Pour plus d’informations, consultez trop[documentation de pile d’Azure powershell.](https://msdn.microsoft.com/library/mt637964.aspx)</span><span class="sxs-lookup"><span data-stu-id="47456-188">For more details, refer too[Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="47456-189">Migrer un conteneur</span><span class="sxs-lookup"><span data-stu-id="47456-189">Migrate a container</span></span>
<span data-ttu-id="47456-190">En raison de l’utilisation du stockage toouneven par les locataires, un opérateur cloud peut trouver une ou plus sous-jacent locataire partages à l’aide de davantage d’espace que d’autres.</span><span class="sxs-lookup"><span data-stu-id="47456-190">Due toouneven storage use by tenants, an cloud operator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="47456-191">Si cela se produit, opérateur de cloud hello peut essayer de toofree l’espace sur le partage d’accentuée hello en effectuant une migration manuellement certains partage tooanother de conteneurs blob.</span><span class="sxs-lookup"><span data-stu-id="47456-191">If this occurs, hello cloud operator can attempt toofree up some space on hello stressed share by manually migrating some blob containers tooanother share.</span></span> 

<span data-ttu-id="47456-192">Vous devez utiliser PowerShell toomigrate conteneurs.</span><span class="sxs-lookup"><span data-stu-id="47456-192">You must use PowerShell toomigrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="47456-193">La migration de conteneurs d’objets blob ne prend pas en charge la migration dynamique et est actuellement une opération hors connexion.</span><span class="sxs-lookup"><span data-stu-id="47456-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="47456-194">Pendant la migration et qu’elle soit terminée hello sous-jacente des objets BLOB que le conteneur ne peut pas être utilisés et sont « hors connexion ».</span><span class="sxs-lookup"><span data-stu-id="47456-194">During migration and until it is complete hello underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="47456-195">**conteneurs de toomigrate à l’aide de PowerShell :**</span><span class="sxs-lookup"><span data-stu-id="47456-195">**toomigrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="47456-196">Vérifiez qu’Azure PowerShell est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="47456-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="47456-197">Si ce n’est pas le cas, utilisez hello suivant les instructions :</span><span class="sxs-lookup"><span data-stu-id="47456-197">If not, use hello following instructions:</span></span>
    * <span data-ttu-id="47456-198">tooinstall hello version la plus récente d’Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="47456-198">tooinstall hello latest Azure PowerShell version and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="47456-199">Pour plus d’informations sur les applets de commande Azure Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="47456-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="47456-200">Obtenir le nom de la batterie hello :</span><span class="sxs-lookup"><span data-stu-id="47456-200">Get hello farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="47456-201">Obtenir les partages hello :</span><span class="sxs-lookup"><span data-stu-id="47456-201">Get hello shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="47456-202">Obtenir les conteneurs hello pour un partage donné.</span><span class="sxs-lookup"><span data-stu-id="47456-202">Get hello containers for a given share.</span></span> <span data-ttu-id="47456-203">Notez que les paramètres Count et Intent sont facultatifs :</span><span class="sxs-lookup"><span data-stu-id="47456-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="47456-204">Examinez ensuite $containers :</span><span class="sxs-lookup"><span data-stu-id="47456-204">Then examine $containers:</span></span>

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="47456-205">Obtenir les partages de destination meilleures hello pour la migration de conteneur hello :</span><span class="sxs-lookup"><span data-stu-id="47456-205">Get hello best destination shares for hello container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="47456-206">Examinez ensuite $destinationshares :</span><span class="sxs-lookup"><span data-stu-id="47456-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="47456-207">Lancer la migration d’un conteneur, notez que ce étant une implémentation asynchrone, une boucle tous les conteneurs dans un état hello partage et du suivi à l’aide des id de tâche retournée de hello.</span><span class="sxs-lookup"><span data-stu-id="47456-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track hello status using hello returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="47456-208">Examiner ensuite $jobId :</span><span class="sxs-lookup"><span data-stu-id="47456-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="47456-209">Vérifiez le statut de tâche de migration hello par son id de tâche. Après la migration de conteneur hello, MigrationStatus est défini trop « terminé ».</span><span class="sxs-lookup"><span data-stu-id="47456-209">Check status of hello migration job by its job id. When hello container migration finishes, MigrationStatus is set too“Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="47456-210">Vous pouvez annuler une tâche de migration en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="47456-210">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="47456-211">Il s’agit à nouveau d’une opération asynchrone, qui peut être suivie en utilisant $jobid :</span><span class="sxs-lookup"><span data-stu-id="47456-211">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="47456-212">Vous pouvez réactiver état hello d’annulation de migration hello :</span><span class="sxs-lookup"><span data-stu-id="47456-212">You can check hello status of hello migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  