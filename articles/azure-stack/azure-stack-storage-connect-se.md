---
title: "Explorateur de stockage d’aaaConnect tooan abonnement de la pile de Azure"
description: "Découvrez comment tooconnect stockage Exporer tooan abonnement de la pile de Azure"
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
ms.openlocfilehash: 8508fcf41a114ff58f57582b4a6021d8050aabe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-storage-explorer-tooan-azure-stack-subscription"></a><span data-ttu-id="6fdbc-103">Connecter l’Explorateur de stockage tooan Azure pile abonnement</span><span class="sxs-lookup"><span data-stu-id="6fdbc-103">Connect Storage Explorer tooan Azure Stack subscription</span></span>

<span data-ttu-id="6fdbc-104">Explorateur de stockage Azure (aperçu) est une application autonome qui vous permet de travail tooeasily avec des données de pile le stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-104">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Stack Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="6fdbc-105">Il existe plusieurs outils tenant compte toomove données tooand à partir de la pile le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-105">There are several tools avaialble toomove data tooand from Azure Stack Storage.</span></span> <span data-ttu-id="6fdbc-106">Pour plus d’informations, consultez [Outils de transfert de données pour le stockage Azure Stack](azure-stack-storage-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="6fdbc-106">For more information, see [Data transfer tools for Azure Stack storage](azure-stack-storage-transfer.md).</span></span>

<span data-ttu-id="6fdbc-107">Dans cet article, vous apprendrez comment tooconnect tooyour stockage de Azure pile comptes à l’aide Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-107">In this article, you learn how tooconnect tooyour Azure Stack storage accounts using Storage Explorer.</span></span> 

<span data-ttu-id="6fdbc-108">Si vous n’avez pas installé l’Explorateur Stockage, [téléchargez](http://www.storageexplorer.com/)-le et installez-le.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-108">If you haven't installed Storage Explorer yet, [download](http://www.storageexplorer.com/) and and install it.</span></span>

<span data-ttu-id="6fdbc-109">Après la connexion d’abonnement de Azure pile tooyour, vous pouvez utiliser hello [articles de l’Explorateur de stockage Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork avec vos données de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-109">After you connect tooyour Azure Stack subscription, you can use hello [Azure Storage Explorer articles](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork with your Azure Stack data.</span></span> 

## <a name="prepare-an-azure-stack-subscription"></a><span data-ttu-id="6fdbc-110">Préparer un abonnement Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6fdbc-110">Prepare an Azure Stack subscription</span></span>

<span data-ttu-id="6fdbc-111">Vous devez accéder au bureau de l’ordinateur hôte toohello Azure pile ou une connexion VPN pour l’abonnement de pile d’Azure Storage Explorer tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-111">You need access toohello Azure Stack host machine's desktop or a VPN connection for Storage Explorer tooaccess hello Azure Stack subscription.</span></span> <span data-ttu-id="6fdbc-112">toolearn tooset d’un tooAzure de connexion VPN pile, voir [connecter tooAzure pile avec VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="6fdbc-112">toolearn how tooset up a VPN connection tooAzure Stack, see [Connect tooAzure Stack with VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

<span data-ttu-id="6fdbc-113">Pourquoi le Kit de développement de pile Azure, vous devez certificat d’autorité racine tooexport hello Azure pile.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-113">For hello Azure Stack Development Kit, you need tooexport hello Azure Stack authority root certificate.</span></span>

### <a name="tooexport-and-then-import-hello-azure-stack-certificate"></a><span data-ttu-id="6fdbc-114">tooexport, puis importer un certificat Azure pile hello</span><span class="sxs-lookup"><span data-stu-id="6fdbc-114">tooexport and then import hello Azure Stack certificate</span></span>

1. <span data-ttu-id="6fdbc-115">Ouvrez `mmc.exe` sur un ordinateur hôte de pile d’Azure, ou sur un ordinateur local avec un tooAzure de connexion VPN pile.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-115">Open `mmc.exe` on an Azure Stack host machine, or a local machine with a VPN connection tooAzure Stack.</span></span> 

2. <span data-ttu-id="6fdbc-116">Dans **fichier**, sélectionnez **ajouter/supprimer un composant logiciel enfichable**, puis ajoutez **certificats** toomanage **compte d’ordinateur** de **Local Ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-116">In **File**, select **Add/Remove Snap-in**, and then add **Certificates** toomanage **Computer account** of **Local Computer**.</span></span>



3. <span data-ttu-id="6fdbc-117">Sous **Racine de la console\Certificats (ordinateur local)\Autorités de certification racines de confiance\Certificats**, recherchez **AzureStackSelfSignedRootCert**.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-117">Under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** find **AzureStackSelfSignedRootCert**.</span></span>

    ![Charger un certificat de racine hello Azure pile via mmc.exe][25]

4. <span data-ttu-id="6fdbc-119">Certificat de hello avec le bouton droit, sélectionnez **toutes les tâches** > **exporter**, puis suivez hello instructions tooexport hello certificat **codé à Base 64 X.509 (. CER)**.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-119">Right-click hello certificate, select **All Tasks** > **Export**, and then follow hello instructions tooexport hello certificate with **Base-64 encoded X.509 (.CER)**.</span></span>  

    <span data-ttu-id="6fdbc-120">certificat exporté de Hello sera utilisé à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-120">hello exported certificate will be used in hello next step.</span></span>
5. <span data-ttu-id="6fdbc-121">Démarrage de l’Explorateur de stockage (version préliminaire), et si vous voyez hello **connecter tooAzure stockage** boîte de dialogue zone, annulez cette opération.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-121">Start Storage Explorer (Preview), and if you see hello **Connect tooAzure Storage** dialog box, cancel it.</span></span>

6. <span data-ttu-id="6fdbc-122">Sur hello **modifier** menu, pointez trop**certificats SSL**, puis cliquez sur **les certificats d’importation**.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-122">On hello **Edit** menu, point too**SSL Certificates**, and then click **Import Certificates**.</span></span> <span data-ttu-id="6fdbc-123">Utilisez le toofind boîte dialogue hello fichier sélecteur et certificat hello ouverts que vous avez exporté à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-123">Use hello file picker dialog box toofind and open hello certificate that you exported in hello previous step.</span></span>

    <span data-ttu-id="6fdbc-124">Après l’importation, vous êtes invité à toorestart Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-124">After importing, you are prompted toorestart Storage Explorer.</span></span>

    ![Importer un certificat hello dans l’Explorateur de stockage (version préliminaire)][27]

<span data-ttu-id="6fdbc-126">Vous êtes maintenant prêt tooconnect abonnement de pile d’Azure Storage Explorer tooan.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-126">Now you are ready tooconnect Storage Explorer tooan Azure Stack subscription.</span></span>

### <a name="tooconnect-an-azure-stack-subscription"></a><span data-ttu-id="6fdbc-127">tooconnect un abonnement Azure pile</span><span class="sxs-lookup"><span data-stu-id="6fdbc-127">tooconnect an Azure Stack subscription</span></span>


1. <span data-ttu-id="6fdbc-128">Après le redémarrage de l’Explorateur de stockage (version préliminaire), sélectionnez hello **modifier** menu, puis assurez-vous que **cible Azure pile** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-128">After Storage Explorer (Preview) restarts, select hello **Edit** menu, and then ensure that **Target Azure Stack** is selected.</span></span> <span data-ttu-id="6fdbc-129">Si elle n’est pas sélectionnée, sélectionnez-la et redémarrez l’Explorateur de stockage pour modifier un effet de tootake hello.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-129">If it is not selected, select it, and then restart Storage Explorer for hello change tootake effect.</span></span> <span data-ttu-id="6fdbc-130">Cette configuration est requise pour la compatibilité avec votre environnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-130">This configuration is required for compatibility with your Azure Stack environment.</span></span>

    ![S’assurer que l’option Target Azure Stack (Cibler Azure Stack) est sélectionnée][28]

7. <span data-ttu-id="6fdbc-132">Dans le volet gauche de hello, sélectionnez **gérer les comptes**.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-132">In hello left pane, select **Manage Accounts**.</span></span>  
    <span data-ttu-id="6fdbc-133">Tous les comptes de Microsoft hello que vous êtes connecté en tooare affiché.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-133">All hello Microsoft accounts that you are signed in tooare displayed.</span></span>

8. <span data-ttu-id="6fdbc-134">tooconnect toohello compte de la pile d’Azure, sélectionnez **ajouter un compte**.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-134">tooconnect toohello Azure Stack account, select **Add an account**.</span></span>

    ![Ajouter un compte Azure Stack][29]

9. <span data-ttu-id="6fdbc-136">Bonjour **connecter tooAzure stockage** boîte de dialogue **environnement Azure**, sélectionnez **utilisez Azure pile environnement**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-136">In hello **Connect tooAzure Storage** dialog box, under **Azure environment**, select **Use Azure Stack Environment**, and then click **Next**.</span></span>

10. <span data-ttu-id="6fdbc-137">toosign avec hello compte Azure pile qui est associé au moins un abonnement Azure pile actif, renseignez hello **connecter tooAzure environnement pile** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-137">toosign in with hello Azure Stack account that's associated with at least one active Azure Stack subscription, fill in hello **Sign in tooAzure Stack Environment** dialog box.</span></span>  

    <span data-ttu-id="6fdbc-138">Détails de Hello pour chaque champ sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6fdbc-138">hello details for each field are as follows:</span></span>

    * <span data-ttu-id="6fdbc-139">**Nom de l’environnement**: champ de hello peut être personnalisé par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-139">**Environment name**: hello field can be customized by user.</span></span>
    * <span data-ttu-id="6fdbc-140">**Point de terminaison de ressource ARM**: hello des exemples de points de terminaison de ressource Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="6fdbc-140">**ARM resource endpoint**: hello samples of Azure Resource Manager resource endpoints:</span></span>

        * <span data-ttu-id="6fdbc-141">Pour un opérateur cloud :</span><span class="sxs-lookup"><span data-stu-id="6fdbc-141">For cloud operator:</span></span><br> <span data-ttu-id="6fdbc-142">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="6fdbc-142">https://adminmanagement.local.azurestack.external</span></span>   
        * <span data-ttu-id="6fdbc-143">Pour un locataire :</span><span class="sxs-lookup"><span data-stu-id="6fdbc-143">For tenant:</span></span><br> <span data-ttu-id="6fdbc-144">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="6fdbc-144">https://management.local.azurestack.external</span></span>
 
    * <span data-ttu-id="6fdbc-145">**ID de locataire** : Facultatif.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-145">**Tenant Id**: Optional.</span></span> <span data-ttu-id="6fdbc-146">Hello est donné uniquement lorsque hello répertoire doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-146">hello value is given only when hello directory must be specified.</span></span>

12. <span data-ttu-id="6fdbc-147">Après que vous être connecté avec un compte Azure pile, volet de gauche hello est remplie avec les abonnements de pile de Azure hello associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-147">After you successfully sign in with an Azure Stack account, hello left pane is populated with hello Azure Stack subscriptions associated with that account.</span></span> <span data-ttu-id="6fdbc-148">Sélectionnez les abonnements Azure pile hello que vous souhaitez toowork avec, puis sélectionnez **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-148">Select hello Azure Stack subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="6fdbc-149">(Activant ou désactivant hello **tous les abonnements** case à cocher active ou désactive la sélection de tous ou aucun des hello répertorié abonnements de la pile de Azure.)</span><span class="sxs-lookup"><span data-stu-id="6fdbc-149">(Selecting or clearing hello **All subscriptions** check box toggles selecting all or none of hello listed Azure Stack subscriptions.)</span></span>

    ![Sélectionnez les abonnements Azure pile hello après avoir complété la boîte de dialogue d’environnement en nuage personnalisée hello][30]  
    <span data-ttu-id="6fdbc-151">volet de gauche de Hello affiche les comptes de stockage hello associées aux abonnements Azure pile de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6fdbc-151">hello left pane displays hello storage accounts associated with hello selected Azure Stack subscriptions.</span></span>

    ![Liste des comptes de stockage, y compris les comptes d’abonnement Azure Stack][31]

## <a name="next-steps"></a><span data-ttu-id="6fdbc-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fdbc-153">Next steps</span></span>
* [<span data-ttu-id="6fdbc-154">Bien démarrer avec l’Explorateur Stockage (préversion)</span><span class="sxs-lookup"><span data-stu-id="6fdbc-154">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="6fdbc-155">Stockage Azure Stack : Différences et considérations</span><span class="sxs-lookup"><span data-stu-id="6fdbc-155">Azure Stack Storage: differences and considerations</span></span>](azure-stack-acs-differences.md)


* <span data-ttu-id="6fdbc-156">toolearn en savoir plus sur le stockage Azure, consultez [Introduction tooMicrosoft stockage Azure](../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6fdbc-156">toolearn more about Azure Storage, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md)</span></span>

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
