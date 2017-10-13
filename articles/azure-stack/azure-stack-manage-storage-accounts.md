---
title: "Gérer les comptes de stockage Azure Stack | Microsoft Docs"
description: "Découvrez comment rechercher, gérer, restaurer et récupérer des comptes de stockage Azure Stack"
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
ms.openlocfilehash: 6e14bd6312135b45984a82099e68a934ec2a4a70
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="7db11-103">Gérer les comptes de stockage dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7db11-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="7db11-104">Découvrez comment gérer les comptes de stockage dans Azure Stack pour rechercher, restaurer et récupérer de la capacité de stockage en fonction des besoins de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="7db11-104">Learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs.</span></span>

## <span data-ttu-id="7db11-105"><a name="find"></a>Rechercher un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="7db11-105"><a name="find"></a>Find a storage account</span></span>
<span data-ttu-id="7db11-106">La liste des comptes de stockage de la région peut être affichée dans Azure Stack comme suit :</span><span class="sxs-lookup"><span data-stu-id="7db11-106">The list of storage accounts in the region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="7db11-107">Dans un navigateur Internet, accédez à https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="7db11-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="7db11-108">Connectez-vous au portail d’administration d’Azure Stack comme opérateur cloud (en utilisant les informations d’identification que vous avez fournies lors du déploiement)</span><span class="sxs-lookup"><span data-stu-id="7db11-108">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="7db11-109">Dans le tableau de bord par défaut, recherchez la liste **Gestion des régions** et cliquez sur la région que vous voulez explorer.</span><span class="sxs-lookup"><span data-stu-id="7db11-109">On the default dashboard – find the **Region management** list and click the region you want to explore.</span></span> <span data-ttu-id="7db11-110">Par exemple **(local**).</span><span class="sxs-lookup"><span data-stu-id="7db11-110">For example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="7db11-111">Sélectionnez **Stockage** dans la liste **Fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="7db11-111">Select **Storage** from the **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="7db11-112">Ensuite, dans le panneau de l’administrateur du fournisseur de ressources de stockage, faites défiler jusqu’à l’onglet **Comptes de stockage** et cliquez sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="7db11-112">Now, on the storage Resource Provider administrator blade – scroll down to the **Storage accounts** tab and click it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="7db11-113">La page résultante est la liste des comptes de stockage dans cette région.</span><span class="sxs-lookup"><span data-stu-id="7db11-113">The resulting page is the list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="7db11-114">Par défaut, les 10 premiers comptes sont affichés.</span><span class="sxs-lookup"><span data-stu-id="7db11-114">By default, the first 10 accounts are displayed.</span></span> <span data-ttu-id="7db11-115">Vous pouvez choisir d’en afficher plus en cliquant sur le lien **Charger plus** en bas de la liste.</span><span class="sxs-lookup"><span data-stu-id="7db11-115">You can choose to fetch more by clicking the  **Load more** link at the bottom of the list.</span></span>

<span data-ttu-id="7db11-116">OU</span><span class="sxs-lookup"><span data-stu-id="7db11-116">OR</span></span>

<span data-ttu-id="7db11-117">Si vous êtes intéressé par un compte de stockage particulier, vous pouvez **filtrer et extraire les comptes appropriés** uniquement.</span><span class="sxs-lookup"><span data-stu-id="7db11-117">If you are interested in a particular storage account – you can **filter and fetch the relevant accounts** only.</span></span>


<span data-ttu-id="7db11-118">**Pour filtrer les comptes :**</span><span class="sxs-lookup"><span data-stu-id="7db11-118">**To filter for accounts:**</span></span>

1. <span data-ttu-id="7db11-119">Cliquez sur **Filtrer** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="7db11-119">Click **Filter** at the top of the blade.</span></span>
2. <span data-ttu-id="7db11-120">Dans le panneau Filtrer, vous pouvez spécifier un **nom de compte**, un **ID d’abonnement** ou un **état** pour affiner la liste des comptes de stockage à afficher.</span><span class="sxs-lookup"><span data-stu-id="7db11-120">On the Filter blade, it allows you to specify **account name**, **subscription ID** or **status** to fine-tune the list of storage accounts to be displayed.</span></span> <span data-ttu-id="7db11-121">Utilisez-les pour filtrer selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="7db11-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="7db11-122">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="7db11-122">Click **Update**.</span></span> <span data-ttu-id="7db11-123">La liste est normalement actualisée en conséquence.</span><span class="sxs-lookup"><span data-stu-id="7db11-123">The list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="7db11-124">Pour réinitialiser le filtre : cliquez sur **Filtrer**, effacez les sélections et mettez à jour la liste.</span><span class="sxs-lookup"><span data-stu-id="7db11-124">To reset the filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="7db11-125">La zone de texte de recherche (en haut du panneau de la liste de comptes de stockage) vous permet de mettre en surbrillance le texte sélectionné dans la liste des comptes.</span><span class="sxs-lookup"><span data-stu-id="7db11-125">The search text box (on the top of the storage accounts list blade) lets you highlight the selected text in the list of accounts.</span></span> <span data-ttu-id="7db11-126">Ceci est très pratique dans le cas où le nom complet ou l’ID n’est pas facilement disponible.</span><span class="sxs-lookup"><span data-stu-id="7db11-126">This is really handy in the case when the full name or id is not easily available.</span></span>

<span data-ttu-id="7db11-127">Vous pouvez utiliser ici du texte libre pour rechercher le compte qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="7db11-127">You can use free text here to help find the account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="7db11-128">Accéder aux détails du compte</span><span class="sxs-lookup"><span data-stu-id="7db11-128">Look at account details</span></span>
<span data-ttu-id="7db11-129">Une fois que vous avez trouvé les comptes qui vous intéressent, vous pouvez cliquer sur un compte particulier pour afficher certains détails.</span><span class="sxs-lookup"><span data-stu-id="7db11-129">Once you have located the accounts you are interested in viewing, you can click the particular account to view certain details.</span></span> <span data-ttu-id="7db11-130">Un nouveau panneau s’ouvre avec les informations détaillées du compte, comme le type du compte, l’heure de création, l’emplacement, etc.</span><span class="sxs-lookup"><span data-stu-id="7db11-130">A new blade opens with the account details such as: the type of the account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="7db11-131">Récupérer un compte supprimé</span><span class="sxs-lookup"><span data-stu-id="7db11-131">Recover a deleted account</span></span>
<span data-ttu-id="7db11-132">Il peut être parfois nécessaire de récupérer un compte supprimé.</span><span class="sxs-lookup"><span data-stu-id="7db11-132">You may be in a situation where you need to recover a deleted account.</span></span>

<span data-ttu-id="7db11-133">Dans Azure Stack, il existe un moyen très simple de le faire :</span><span class="sxs-lookup"><span data-stu-id="7db11-133">In Azure Stack there is a very simple way to do that:</span></span>

1. <span data-ttu-id="7db11-134">Accédez à la liste de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="7db11-134">Browse to the storage accounts list.</span></span> <span data-ttu-id="7db11-135">Pour plus d’informations, consultez [Rechercher un compte de stockage](#find) dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="7db11-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="7db11-136">Localisez ce compte particulier dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7db11-136">Locate that particular account in the list.</span></span> <span data-ttu-id="7db11-137">Il peut être nécessaire de filtrer.</span><span class="sxs-lookup"><span data-stu-id="7db11-137">You may need to filter.</span></span>
3. <span data-ttu-id="7db11-138">Vérifiez l’*état* du compte.</span><span class="sxs-lookup"><span data-stu-id="7db11-138">Check the *state* of the account.</span></span> <span data-ttu-id="7db11-139">Il doit être **Supprimé**.</span><span class="sxs-lookup"><span data-stu-id="7db11-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="7db11-140">Cliquez sur le compte pour ouvrir le panneau des détails du compte.</span><span class="sxs-lookup"><span data-stu-id="7db11-140">Click the account which opens the account details blade.</span></span>
5. <span data-ttu-id="7db11-141">En haut de ce panneau, recherchez le bouton **Récupérer** et cliquez sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="7db11-141">On top of this blade, locate the **Recover** button and click it.</span></span>
6. <span data-ttu-id="7db11-142">Cliquez sur **Yes** (Oui) pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="7db11-142">Click **Yes** to confirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="7db11-143">La récupération est maintenant *en cours... Attendez* un message indiquant que la récupération est effective.</span><span class="sxs-lookup"><span data-stu-id="7db11-143">The recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="7db11-144">Vous pouvez aussi cliquer sur l’icône « cloche » en haut du portail pour voir des indications sur la progression.</span><span class="sxs-lookup"><span data-stu-id="7db11-144">You can also click the “bell” icon at the top of the portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="7db11-145">Une fois que le compte récupéré est synchronisé, il peut à nouveau être utilisé.</span><span class="sxs-lookup"><span data-stu-id="7db11-145">Once the recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="7db11-146">Quelques astuces</span><span class="sxs-lookup"><span data-stu-id="7db11-146">Some Gotchas</span></span>
* <span data-ttu-id="7db11-147">Votre compte supprimé affiche un état **hors conservation**.</span><span class="sxs-lookup"><span data-stu-id="7db11-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="7db11-148">Cela signifie que le compte supprimé a dépassé la période de conservation et qu’il n’est peut-être pas récupérable.</span><span class="sxs-lookup"><span data-stu-id="7db11-148">This means that the deleted account has exceeded the retention period and may not be recoverable.</span></span>
* <span data-ttu-id="7db11-149">Votre compte supprimé n’apparaît pas dans la liste des comptes.</span><span class="sxs-lookup"><span data-stu-id="7db11-149">Your deleted account does not show in the accounts list.</span></span>
  
  <span data-ttu-id="7db11-150">Cela peut signifier que le compte supprimé a été déjà fait l’objet d’un nettoyage de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="7db11-150">This could mean that the deleted account has already been garbage collected.</span></span> <span data-ttu-id="7db11-151">Dans ce cas, il ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="7db11-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="7db11-152">Consultez [Récupérer de la capacité](#reclaim) dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="7db11-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-the-retention-period"></a><span data-ttu-id="7db11-153">Définir la période de conservation</span><span class="sxs-lookup"><span data-stu-id="7db11-153">Set the retention period</span></span>
<span data-ttu-id="7db11-154">Le paramètre de période de conservation permet à un opérateur cloud de spécifier une période de temps en jours (entre 0 et 9 999 jours) pendant laquelle un compte supprimé peut être récupéré.</span><span class="sxs-lookup"><span data-stu-id="7db11-154">The retention period setting allows a cloud operator to specify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="7db11-155">La période de conservation par défaut est définie sur 15 jours.</span><span class="sxs-lookup"><span data-stu-id="7db11-155">The default retention period is set to 15 days.</span></span> <span data-ttu-id="7db11-156">La valeur « 0 » pour ce paramètre signifie qu’un compte supprimé est immédiatement hors conservation et est marqué pour faire l’objet d’un nettoyage périodique de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="7db11-156">Setting the value to “0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="7db11-157">**Pour changer la période de conservation :**</span><span class="sxs-lookup"><span data-stu-id="7db11-157">**To change the retention period:**</span></span>

1. <span data-ttu-id="7db11-158">Dans un navigateur Internet, accédez à https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="7db11-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="7db11-159">Connectez-vous au portail d’administration d’Azure Stack comme opérateur cloud (en utilisant les informations d’identification que vous avez fournies lors du déploiement)</span><span class="sxs-lookup"><span data-stu-id="7db11-159">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="7db11-160">Dans le tableau de bord par défaut, recherchez la liste **Gestion des régions** et cliquez sur la région que vous voulez explorer, par exemple **(local**).</span><span class="sxs-lookup"><span data-stu-id="7db11-160">On the default dashboard – find the **Region management** list and click the region you want to explore – for example **(local**).</span></span>
4. <span data-ttu-id="7db11-161">Sélectionnez **Stockage** dans la liste **Fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="7db11-161">Select **Storage** from the **Resource Providers** list.</span></span>
5. <span data-ttu-id="7db11-162">Cliquez sur **Paramètres** en haut pour ouvrir le panneau des paramètres.</span><span class="sxs-lookup"><span data-stu-id="7db11-162">Click **Settings** at the top to open the setting blade.</span></span>
6. <span data-ttu-id="7db11-163">Cliquez sur **Configuration**, puis changez la valeur de la période de conservation.</span><span class="sxs-lookup"><span data-stu-id="7db11-163">Click **Configuration** then edit the retention period value.</span></span>

   <span data-ttu-id="7db11-164">Définissez le nombre de jours et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="7db11-164">Set the number of days and then save it.</span></span>
   
   <span data-ttu-id="7db11-165">Cette valeur est prise en compte immédiatement et est appliquée à toute votre région.</span><span class="sxs-lookup"><span data-stu-id="7db11-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <span data-ttu-id="7db11-166"><a name="reclaim"></a>Récupérer de la capacité</span><span class="sxs-lookup"><span data-stu-id="7db11-166"><a name="reclaim"></a>Reclaim capacity</span></span>
<span data-ttu-id="7db11-167">Un des effets secondaires de la période de conservation est qu’un compte supprimé continue à consommer de la capacité jusqu’à ce qu’il sorte de cette période de conservation.</span><span class="sxs-lookup"><span data-stu-id="7db11-167">One of the side effects of having a retention period is that a deleted account continues to consume capacity until it comes out of the retention period.</span></span> <span data-ttu-id="7db11-168">En tant qu’opérateur cloud, vous pouvez avoir besoin d’un moyen de récupérer l’espace du compte supprimé, même si la période de conservation n’a pas encore expiré.</span><span class="sxs-lookup"><span data-stu-id="7db11-168">As a cloud operator you may need a way to reclaim the deleted account space even though the retention period has not yet expired.</span></span>

<span data-ttu-id="7db11-169">Vous pouvez récupérer de la capacité en utilisant le portail ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7db11-169">You can reclaim capacity using either the portal or PowerShell.</span></span>

<span data-ttu-id="7db11-170">**Pour récupérer de la capacité en utilisant le portail :**</span><span class="sxs-lookup"><span data-stu-id="7db11-170">**To reclaim capacity using the portal:**</span></span>
1. <span data-ttu-id="7db11-171">Accédez au panneau des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="7db11-171">Navigate to the storage accounts blade.</span></span> <span data-ttu-id="7db11-172">Consultez [Rechercher un compte de stockage](#find).</span><span class="sxs-lookup"><span data-stu-id="7db11-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="7db11-173">Cliquez sur **Récupérer de l’espace** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="7db11-173">Click **Reclaim space** at the top of the blade.</span></span>
3. <span data-ttu-id="7db11-174">Lisez le message, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7db11-174">Read the message and then click **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="7db11-175">Attendez la notification de la réussite de l’opération. Utilisez l’icône de cloche sur le portail.</span><span class="sxs-lookup"><span data-stu-id="7db11-175">Wait for success notification See the bell icon on the portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="7db11-176">Actualisez la page Comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="7db11-176">Refresh the Storage accounts page.</span></span> <span data-ttu-id="7db11-177">Les comptes supprimés ne figurent plus dans la liste, car ils ont été supprimés définitivement.</span><span class="sxs-lookup"><span data-stu-id="7db11-177">The deleted accounts are no longer shown in the list because they have been purged.</span></span>

<span data-ttu-id="7db11-178">Vous pouvez aussi utiliser PowerShell pour remplacer explicitement la période de rétention et récupérer immédiatement de la capacité.</span><span class="sxs-lookup"><span data-stu-id="7db11-178">You can also use PowerShell to explicitly override the retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="7db11-179">**Pour récupérer de la capacité en utilisant PowerShell :**</span><span class="sxs-lookup"><span data-stu-id="7db11-179">**To reclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="7db11-180">Vérifiez qu’Azure PowerShell est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="7db11-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="7db11-181">Dans le cas contraire, suivez ces instructions :</span><span class="sxs-lookup"><span data-stu-id="7db11-181">If not, use the following instructions:</span></span> 
   * <span data-ttu-id="7db11-182">Pour installer la dernière version d’Azure PowerShell et l’associer à votre abonnement Azure, consultez [Installer et configurer Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="7db11-182">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="7db11-183">Pour plus d’informations sur les applets de commande Azure Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="7db11-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="7db11-184">Exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7db11-184">Run the following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="7db11-185">Si vous exécutez cette applet de commande, vous supprimez définitivement le compte et son contenu.</span><span class="sxs-lookup"><span data-stu-id="7db11-185">If you run this cmdlet you permanently delete the account and its contents.</span></span> <span data-ttu-id="7db11-186">Il n’est pas récupérable.</span><span class="sxs-lookup"><span data-stu-id="7db11-186">It is not recoverable.</span></span> <span data-ttu-id="7db11-187">Utilisez cette option avec précaution.</span><span class="sxs-lookup"><span data-stu-id="7db11-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="7db11-188">Pour plus d’informations, consultez la [documentation d’Azure Stack PowerShell.](https://msdn.microsoft.com/library/mt637964.aspx)</span><span class="sxs-lookup"><span data-stu-id="7db11-188">For more details, refer to [Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="7db11-189">Migrer un conteneur</span><span class="sxs-lookup"><span data-stu-id="7db11-189">Migrate a container</span></span>
<span data-ttu-id="7db11-190">En raison d’une utilisation inégale du stockage par les locataires, un opérateur cloud peut constater qu’un ou plusieurs partages de locataire sous-jacent utilisent plus d’espace que d’autres.</span><span class="sxs-lookup"><span data-stu-id="7db11-190">Due to uneven storage use by tenants, an cloud operator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="7db11-191">Si cela se produit, l’opérateur cloud peut essayer de libérer de l’espace sur le partage trop sollicité en migrant manuellement des conteneurs d’objets blob vers un autre partage.</span><span class="sxs-lookup"><span data-stu-id="7db11-191">If this occurs, the cloud operator can attempt to free up some space on the stressed share by manually migrating some blob containers to another share.</span></span> 

<span data-ttu-id="7db11-192">Vous devez utiliser PowerShell pour migrer des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="7db11-192">You must use PowerShell to migrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="7db11-193">La migration de conteneurs d’objets blob ne prend pas en charge la migration dynamique et est actuellement une opération hors connexion.</span><span class="sxs-lookup"><span data-stu-id="7db11-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="7db11-194">Pendant la migration et jusqu’à ce qu’elle soit terminée, les objets blob sous-jacents de ce conteneur ne peuvent pas être utilisés et sont « hors connexion ».</span><span class="sxs-lookup"><span data-stu-id="7db11-194">During migration and until it is complete the underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="7db11-195">**Pour migrer des conteneurs en utilisant PowerShell :**</span><span class="sxs-lookup"><span data-stu-id="7db11-195">**To migrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="7db11-196">Vérifiez qu’Azure PowerShell est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="7db11-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="7db11-197">Dans le cas contraire, suivez ces instructions :</span><span class="sxs-lookup"><span data-stu-id="7db11-197">If not, use the following instructions:</span></span>
    * <span data-ttu-id="7db11-198">Pour installer la dernière version d’Azure PowerShell et l’associer à votre abonnement Azure, consultez [Installer et configurer Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="7db11-198">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="7db11-199">Pour plus d’informations sur les applets de commande Azure Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="7db11-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="7db11-200">Obtenez le nom de la batterie de serveurs :</span><span class="sxs-lookup"><span data-stu-id="7db11-200">Get the farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="7db11-201">Obtenez les partages :</span><span class="sxs-lookup"><span data-stu-id="7db11-201">Get the shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="7db11-202">Obtenez les conteneurs d’un partage donné.</span><span class="sxs-lookup"><span data-stu-id="7db11-202">Get the containers for a given share.</span></span> <span data-ttu-id="7db11-203">Notez que les paramètres Count et Intent sont facultatifs :</span><span class="sxs-lookup"><span data-stu-id="7db11-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="7db11-204">Examinez ensuite $containers :</span><span class="sxs-lookup"><span data-stu-id="7db11-204">Then examine $containers:</span></span>

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="7db11-205">Obtenez les meilleurs partages de destination pour la migration du conteneur :</span><span class="sxs-lookup"><span data-stu-id="7db11-205">Get the best destination shares for the container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="7db11-206">Examinez ensuite $destinationshares :</span><span class="sxs-lookup"><span data-stu-id="7db11-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="7db11-207">Lancez la migration d’un conteneur. Notez qu’il s’agit d’une implémentation asynchrone : vous pouvez donc boucler dans tous les conteneurs d’un partage et en suivre l’état en utilisant l’ID de tâche retourné.</span><span class="sxs-lookup"><span data-stu-id="7db11-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track the status using the returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="7db11-208">Examiner ensuite $jobId :</span><span class="sxs-lookup"><span data-stu-id="7db11-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="7db11-209">Vérifiez l’état de la tâche de migration par son ID de tâche. Une fois la migration du conteneur terminée, MigrationStatus est défini sur « Terminé ».</span><span class="sxs-lookup"><span data-stu-id="7db11-209">Check status of the migration job by its job id. When the container migration finishes, MigrationStatus is set to “Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="7db11-210">Vous pouvez annuler une tâche de migration en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7db11-210">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="7db11-211">Il s’agit à nouveau d’une opération asynchrone, qui peut être suivie en utilisant $jobid :</span><span class="sxs-lookup"><span data-stu-id="7db11-211">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="7db11-212">Vous pouvez aussi vérifier l’état de l’annulation de la migration :</span><span class="sxs-lookup"><span data-stu-id="7db11-212">You can check the status of the migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  