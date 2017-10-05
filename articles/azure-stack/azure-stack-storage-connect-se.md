---
title: "Connecter l’Explorateur Stockage à un abonnement Azure Stack"
description: "Découvrir comment connecter l’Explorateur Stockage à un abonnement Azure Stack"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/24/2017
ms.author: xiaofmao
ms.openlocfilehash: 3c1ee7665da41c0fae9ddd492127495fe7e5581b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-storage-explorer-to-an-azure-stack-subscription"></a><span data-ttu-id="a34bc-103">Connecter l’Explorateur Stockage à un abonnement Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a34bc-103">Connect Storage Explorer to an Azure Stack subscription</span></span>

<span data-ttu-id="a34bc-104">L’Explorateur Stockage Azure (préversion) est une application autonome qui vous permet d’utiliser facilement les données de stockage Azure Stack sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="a34bc-104">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Stack Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="a34bc-105">Il existe plusieurs outils qui permettent de déplacer des données vers et à partir du stockage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a34bc-105">There are several tools avaialble to move data to and from Azure Stack Storage.</span></span> <span data-ttu-id="a34bc-106">Pour plus d’informations, consultez [Outils de transfert de données pour le stockage Azure Stack](azure-stack-storage-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="a34bc-106">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="a34bc-107">Dans cet article, vous découvrez comment vous connecter à vos comptes de stockage Azure Stack à l’aide de l’Explorateur Stockage.</span><span class="sxs-lookup"><span data-stu-id="a34bc-107">In this article, you learn how to connect to your Azure Stack storage accounts using Storage Explorer.</span></span> 

<span data-ttu-id="a34bc-108">Si vous n’avez pas installé l’Explorateur Stockage, [téléchargez](http://www.storageexplorer.com/)-le et installez-le.</span><span class="sxs-lookup"><span data-stu-id="a34bc-108">If you haven't installed Storage Explorer yet, [download](http://www.storageexplorer.com/) and and install it.</span></span>

<span data-ttu-id="a34bc-109">Une fois que vous êtes connecté à votre abonnement Azure Stack, vous pouvez utiliser les [articles sur l’Explorateur Stockage Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) pour utiliser vos données Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a34bc-109">After you connect to your Azure Stack subscription, you can use the [Azure Storage Explorer articles](../vs-azure-tools-storage-manage-with-storage-explorer.md) to work with your Azure Stack data.</span></span> 

## <a name="prepare-an-azure-stack-subscription"></a><span data-ttu-id="a34bc-110">Préparer un abonnement Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a34bc-110">Prepare an Azure Stack subscription</span></span>

<span data-ttu-id="a34bc-111">Vous avez besoin d’un accès au bureau de la machine hôte d’Azure Stack ou d’une connexion VPN pour que l’Explorateur Stockage puisse accéder à l’abonnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a34bc-111">You need access to the Azure Stack host machine's desktop or a VPN connection for Storage Explorer to access the Azure Stack subscription.</span></span> <span data-ttu-id="a34bc-112">Pour savoir comment configurer une connexion VPN à Azure Stack, consultez [Connect to Azure Stack](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) (Se connecter à Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="a34bc-112">To learn how to set up a VPN connection to Azure Stack, see [Connect to Azure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="a34bc-113">Pour le Kit de développement Azure Stack, vous devez exporter le certificat racine d’autorité Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a34bc-113">For the Azure Stack Development Kit, you need to export the Azure Stack authority root certificate.</span></span>

### <a name="to-export-and-then-import-the-azure-stack-certificate"></a><span data-ttu-id="a34bc-114">Pour exporter et importer le certificat Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a34bc-114">To export and then import the Azure Stack certificate</span></span>

1. <span data-ttu-id="a34bc-115">Ouvrez `mmc.exe` sur une machine hôte Azure Stack ou sur une machine locale avec une connexion VPN à Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a34bc-115">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection to Azure Stack.</span></span> 

2. <span data-ttu-id="a34bc-116">Dans **Fichier**, sélectionnez **Ajouter/Supprimer un composant logiciel enfichable**, ajoutez **Certificats** pour gérer le **compte d’ordinateur** d’un **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-116">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** to manage **Computer account** of **Local Computer**.</span></span>



3. <span data-ttu-id="a34bc-117">Sous **Racine de la console\Certificats (ordinateur local)\Autorités de certification racines de confiance\Certificats**, recherchez **AzureStackSelfSignedRootCert**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-117">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![Charger le certificat racine Azure Stack via mmc.exe][25]

4. <span data-ttu-id="a34bc-119">Cliquez avec le bouton droit sur le certificat, sélectionnez **Toutes les tâches** > **Exporter**, puis suivez les instructions pour exporter le certificat avec **X.509 encodé en base 64 (.cer)**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-119">Right-click the certificate, select **All Tasks** > **Export**, and then follow the instructions to export the certificate with **Base-64 encoded X.509 (.CER)**.</span></span>  

    <span data-ttu-id="a34bc-120">Le certificat exporté sera utilisé à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="a34bc-120">The exported certificate will be used in the next step.</span></span>
5. <span data-ttu-id="a34bc-121">Démarrez l’Explorateur Stockage (préversion) et, si vous voyez la boîte de dialogue **Connexion au stockage Azure**, cliquez sur Annuler.</span><span class="sxs-lookup"><span data-stu-id="a34bc-121">Start Storage Explorer (Preview), and if you see the **Connect to Azure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="a34bc-122">Dans le menu **Modifier**, pointez sur **Certificats SSL**, puis cliquez sur **Importer les certificats**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-122">On the **Edit** menu, point to **SSL Certificates**, and then click **Import Certificates**.</span></span> <span data-ttu-id="a34bc-123">Utilisez la boîte de dialogue du sélecteur de fichier pour rechercher et ouvrir le certificat que vous avez exporté à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="a34bc-123">Use the file picker dialog box to find and open the certificate that you exported in the previous step.</span></span>

    <span data-ttu-id="a34bc-124">Vous êtes invité à redémarrer l’Explorateur de stockage suite à l’importation.</span><span class="sxs-lookup"><span data-stu-id="a34bc-124">After importing, you are prompted to restart Storage Explorer.</span></span>

    ![Importer le certificat dans l’explorateur de stockage (version préliminaire)][27]

<span data-ttu-id="a34bc-126">Vous êtes maintenant prêts à connecter l’Explorateur Stockage à un abonnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a34bc-126">Now you are ready to connect Storage Explorer to an Azure Stack subscription.</span></span>

### <a name="to-connect-an-azure-stack-subscription"></a><span data-ttu-id="a34bc-127">Connexion à un abonnement Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a34bc-127">To connect an Azure Stack subscription</span></span>


1. <span data-ttu-id="a34bc-128">Après le redémarrage de l’Explorateur de stockage (version préliminaire), sélectionnez le menu **Modifier** et vérifiez que l’option **Target Azure Stack** (Cibler Azure Stack) est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="a34bc-128">After Storage Explorer (Preview) restarts, select the **Edit** menu, and then ensure that **Target Azure Stack** is selected.</span></span> <span data-ttu-id="a34bc-129">Si l’option n’est pas sélectionnée, sélectionnez-la et redémarrez l’Explorateur de stockage pour appliquer la modification.</span><span class="sxs-lookup"><span data-stu-id="a34bc-129">If it is not selected, select it, and then restart Storage Explorer for the change to take effect.</span></span> <span data-ttu-id="a34bc-130">Cette configuration est requise pour la compatibilité avec votre environnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a34bc-130">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![S’assurer que l’option Target Azure Stack (Cibler Azure Stack) est sélectionnée][28]

7. <span data-ttu-id="a34bc-132">Dans le volet gauche, sélectionnez **Gérer les comptes**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-132">In the left pane, select **Manage Accounts**.</span></span>  
    <span data-ttu-id="a34bc-133">Tous les comptes Microsoft auxquels vous êtes connecté sont affichés.</span><span class="sxs-lookup"><span data-stu-id="a34bc-133">All the Microsoft accounts that you are signed in to are displayed.</span></span>

8. <span data-ttu-id="a34bc-134">Pour vous connecter au compte Azure Stack, sélectionnez **Ajouter un compte**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-134">To connect to the Azure Stack account, select **Add an account**.</span></span>

    ![Ajouter un compte Azure Stack][29]

9. <span data-ttu-id="a34bc-136">Dans la boîte de dialogue **Connexion au stockage Azure**, sous **Environnement Azure**, sélectionnez **Utiliser l’environnement Azure Stack**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-136">In the **Connect to Azure Storage** dialog box, under **Azure environment**, select **Use Azure Stack Environment**, and then click **Next**.</span></span>

10. <span data-ttu-id="a34bc-137">Pour vous connecter au compte Azure Stack associé à au moins un abonnement Azure Stack actif, remplissez la boîte de dialogue **Se connecter à un environnement Azure Stack**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-137">To sign in with the Azure Stack account that's associated with at least one active Azure Stack subscription, fill in the **Sign in to Azure Stack Environment** dialog box.</span></span>  

    <span data-ttu-id="a34bc-138">Les détails de chaque champ figurent ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a34bc-138">The details for each field are as follows:</span></span>

    * <span data-ttu-id="a34bc-139">**Nom de l’environnement** : le champ peut être personnalisé par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a34bc-139">**Environment name**: The field can be customized by user.</span></span>
    * <span data-ttu-id="a34bc-140">**ARM resource endpoint** (Point de terminaison de ressource ARM) : les exemples de points de terminaison de ressource ARM :</span><span class="sxs-lookup"><span data-stu-id="a34bc-140">**ARM resource endpoint**: The samples of Azure Resource Manager resource endpoints:</span></span>

        * <span data-ttu-id="a34bc-141">Pour un opérateur cloud :</span><span class="sxs-lookup"><span data-stu-id="a34bc-141">For cloud operator:</span></span><br> <span data-ttu-id="a34bc-142">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="a34bc-142">https://adminmanagement.local.azurestack.external</span></span>   
        * <span data-ttu-id="a34bc-143">Pour un locataire :</span><span class="sxs-lookup"><span data-stu-id="a34bc-143">For tenant:</span></span><br> <span data-ttu-id="a34bc-144">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="a34bc-144">https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="a34bc-145">**ID de locataire** : Facultatif.</span><span class="sxs-lookup"><span data-stu-id="a34bc-145">**Tenant Id**: Optional.</span></span> <span data-ttu-id="a34bc-146">La valeur est fournie uniquement lorsque le répertoire doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="a34bc-146">The value is given only when the directory must be specified.</span></span>

12. <span data-ttu-id="a34bc-147">Une fois que vous êtes connecté avec un compte Azure Stack, le volet gauche est renseigné avec les abonnements Azure Stack associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="a34bc-147">After you successfully sign in with an Azure Stack account, the left pane is populated with the Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="a34bc-148">Sélectionnez les abonnements Azure Stack que vous souhaitez utiliser, puis sélectionnez **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-148">Select the Azure Stack subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="a34bc-149">(La case à cocher **Tous les abonnements** permet de sélectionner ou de désélectionner l’ensemble des abonnements Azure Stack répertoriés.)</span><span class="sxs-lookup"><span data-stu-id="a34bc-149">(Selecting or clearing the **All subscriptions** check box toggles selecting all or none of the listed Azure Stack subscriptions.)</span></span>

    ![Sélectionner les abonnements Azure Stack après avoir renseigné la boîte de dialogue Custom Cloud Environment (Environnement cloud personnalisé)][30]  
    <span data-ttu-id="a34bc-151">Le volet de gauche affiche les comptes de stockage associés aux abonnements Azure Stack sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="a34bc-151">The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.</span></span>

    ![Liste des comptes de stockage, y compris les comptes d’abonnement Azure Stack][31]

## <a name="next-steps"></a><span data-ttu-id="a34bc-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a34bc-153">Next steps</span></span>
* [<span data-ttu-id="a34bc-154">Bien démarrer avec l’Explorateur Stockage (préversion)</span><span class="sxs-lookup"><span data-stu-id="a34bc-154">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="a34bc-155">Stockage Azure Stack : Différences et considérations</span><span class="sxs-lookup"><span data-stu-id="a34bc-155">Azure Stack Storage: differences and considerations</span></span>](azure-stack-acs-differences.md)


* <span data-ttu-id="a34bc-156">Pour en savoir plus sur le stockage Azure, consultez [Présentation du stockage Microsoft Azure](../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="a34bc-156">To learn more about Azure Storage, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md)</span></span>

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
