---
title: "Se connecter à la base de données SQL avec SQL Server Management Studio dans Azure RemoteApp | Microsoft Docs"
description: "Utilisez ce didacticiel pour apprendre à utiliser SQL Server Management Studio dans Azure RemoteApp pour la sécurité et les performances lors de la connexion à la base de données SQL"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a><span data-ttu-id="efae8-103">Connexion à une base de données SQL à l’aide de SQL Server Management Studio dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="efae8-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efae8-104">Azure RemoteApp n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="efae8-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="efae8-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="efae8-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="efae8-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="efae8-106">Introduction</span></span>
<span data-ttu-id="efae8-107">Ce didacticiel vous montre comment utiliser SQL Server Management Studio (SSMS) dans Azure RemoteApp pour vous connecter à une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="efae8-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span></span> <span data-ttu-id="efae8-108">Il vous guide tout au long de la configuration de SQL Server Management Studio dans Azure RemoteApp, vous en décrit les avantages, et indique les fonctionnalités de sécurité que vous pouvez utiliser dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="efae8-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="efae8-109">**Durée estimée :** 45 minutes</span><span class="sxs-lookup"><span data-stu-id="efae8-109">**Estimated time to complete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="efae8-110">SSMS dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="efae8-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="efae8-111">Azure RemoteApp est un service RDS d’Azure, qui fournit des applications.</span><span class="sxs-lookup"><span data-stu-id="efae8-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="efae8-112">Vous pouvez obtenir plus d’informations sur ce service ici : [Qu’est-ce que RemoteApp ?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="efae8-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="efae8-113">L’exécution de SSMS dans Azure RemoteApp et l’exécution locale de SSMS vous donnent la même expérience.</span><span class="sxs-lookup"><span data-stu-id="efae8-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span></span>

![Capture d’écran illustrant SSMS en cours d’exécution dans Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="efae8-115">Avantages</span><span class="sxs-lookup"><span data-stu-id="efae8-115">Benefits</span></span>
<span data-ttu-id="efae8-116">Les avantages liés à l’utilisation de SSMS dans Azure RemoteApp sont nombreux :</span><span class="sxs-lookup"><span data-stu-id="efae8-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="efae8-117">Le port 1433 sur Azure SQL Server ne doit pas être exposé en externe (en dehors d’Azure).</span><span class="sxs-lookup"><span data-stu-id="efae8-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="efae8-118">Il est inutile de continuer à ajouter et à supprimer des adresses IP dans le pare-feu d’Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="efae8-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span></span>
* <span data-ttu-id="efae8-119">Toutes les connexions Azure RemoteApp ont lieu via HTTPS sur le port 443 à l’aide du protocole RDP (Remote Desktop Protocol) chiffré.</span><span class="sxs-lookup"><span data-stu-id="efae8-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="efae8-120">SSMS est multi-utilisateur et évolutif.</span><span class="sxs-lookup"><span data-stu-id="efae8-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="efae8-121">Posséder SSMS dans la même région que la base de données SQL permet d’obtenir des gains de performances.</span><span class="sxs-lookup"><span data-stu-id="efae8-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span></span>
* <span data-ttu-id="efae8-122">Vous pouvez auditer l’utilisation d’Azure RemoteApp avec l’édition Premium d’Azure Active Directory qui propose des rapports d’activité utilisateur.</span><span class="sxs-lookup"><span data-stu-id="efae8-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="efae8-123">Vous pouvez activer l’authentification multifacteur (MFA).</span><span class="sxs-lookup"><span data-stu-id="efae8-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="efae8-124">Vous pouvez accéder à SSMS où que vous soyez à l’aide de l’un des clients Azure RemoteApp pris en charge, notamment iOS, Android, Mac, Windows Phone et PC Windows.</span><span class="sxs-lookup"><span data-stu-id="efae8-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-the-azure-remoteapp-collection"></a><span data-ttu-id="efae8-125">Créer la collection Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="efae8-125">Create the Azure RemoteApp collection</span></span>
<span data-ttu-id="efae8-126">Voici la procédure à suivre pour créer votre collection Azure RemoteApp avec SSMS :</span><span class="sxs-lookup"><span data-stu-id="efae8-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="efae8-127">1. Créer une machine virtuelle Windows à partir d’une image</span><span class="sxs-lookup"><span data-stu-id="efae8-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="efae8-128">Utilisez l’image « Windows Server 2012 R2 Hôte de session Bureau à distance Windows Server » de la galerie pour créer votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="efae8-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="efae8-129">2. Installer SSMS à partir de SQL Express</span><span class="sxs-lookup"><span data-stu-id="efae8-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="efae8-130">Accédez à la nouvelle machine virtuelle et à cette page de téléchargement : [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="efae8-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="efae8-131">Une option permet de télécharger uniquement SSMS.</span><span class="sxs-lookup"><span data-stu-id="efae8-131">There is an option to only download SSMS.</span></span> <span data-ttu-id="efae8-132">À l’issue du téléchargement, accédez au répertoire d’installation et exécutez le programme d’installation de SSMS.</span><span class="sxs-lookup"><span data-stu-id="efae8-132">After download, go into the install directory and run Setup to install SSMS.</span></span>

<span data-ttu-id="efae8-133">Vous devez également installer SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="efae8-133">You also need to install SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="efae8-134">Vous pouvez le télécharger ici : [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="efae8-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="efae8-135">SQL Server 2014 Service Pack 1 inclut des fonctionnalités essentielles pour l’utilisation de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="efae8-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="efae8-136">3. Exécuter le script de validation et Sysprep</span><span class="sxs-lookup"><span data-stu-id="efae8-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="efae8-137">Un script PowerShell de validation figure sur le Bureau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="efae8-137">On the desktop of the VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="efae8-138">Exécutez-le en double-cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="efae8-138">Run this by double-clicking.</span></span> <span data-ttu-id="efae8-139">Il vérifie que la machine virtuelle est prête à être utilisée pour l’hébergement distant des applications.</span><span class="sxs-lookup"><span data-stu-id="efae8-139">It will verify that the VM is ready to be used for remote hosting of applications.</span></span> <span data-ttu-id="efae8-140">À l’issue de la vérification, il demande d’exécuter Sysprep. Choisissez de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="efae8-140">When verification is complete, it will ask to run sysprep - choose to run it.</span></span>

<span data-ttu-id="efae8-141">Lorsque l’exécution de Sysprep est terminée, il arrête la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="efae8-141">When sysprep completes, it will shut down the VM.</span></span>

<span data-ttu-id="efae8-142">Pour en savoir plus sur la création d'une image Azure RemoteApp, consultez la page [Création d'une image de modèle RemoteApp dans Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="efae8-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="efae8-143">4. Capturer l’image</span><span class="sxs-lookup"><span data-stu-id="efae8-143">4. Capture image</span></span>
<span data-ttu-id="efae8-144">Lorsque l’exécution de la machine virtuelle est arrêtée, recherchez-la dans le portail actuel et capturez-la.</span><span class="sxs-lookup"><span data-stu-id="efae8-144">When the VM has stopped running, find it in the current portal and capture it.</span></span>

<span data-ttu-id="efae8-145">Pour en savoir plus sur la capture d’une image, consultez [Capturer l’image d’une machine virtuelle Windows Azure créée avec le modèle de déploiement classique](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="efae8-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-to-azure-remoteapp-template-images"></a><span data-ttu-id="efae8-146">5. Ajouter des images de modèle à Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="efae8-146">5. Add to Azure RemoteApp Template images</span></span>
<span data-ttu-id="efae8-147">Dans la section Azure RemoteApp du portail actuel, cliquez sur l’onglet Images de modèle, puis sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="efae8-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span></span> <span data-ttu-id="efae8-148">Dans la zone contextuelle, sélectionnez Importez une image depuis votre bibliothèque de machines virtuelles, puis choisissez l’image que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="efae8-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="efae8-149">6. Créer une collection cloud</span><span class="sxs-lookup"><span data-stu-id="efae8-149">6. Create cloud collection</span></span>
<span data-ttu-id="efae8-150">Dans le portail actuel, créez une collection cloud Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="efae8-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="efae8-151">Choisissez l’image de modèle que vous venez d’importer avec SSMS installé dessus.</span><span class="sxs-lookup"><span data-stu-id="efae8-151">Choose the Template Image that you just imported with SSMS installed on it.</span></span>

![Créer une collection cloud][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="efae8-153">7. Publier SSMS</span><span class="sxs-lookup"><span data-stu-id="efae8-153">7. Publish SSMS</span></span>
<span data-ttu-id="efae8-154">Dans l’onglet Publication de votre nouvelle collection cloud, sélectionnez Publier une application dans le menu Démarrer, puis choisissez SSMS dans la liste.</span><span class="sxs-lookup"><span data-stu-id="efae8-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span></span>

![Publier une application][5]

### <a name="8-add-users"></a><span data-ttu-id="efae8-156">8. Ajouter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="efae8-156">8. Add users</span></span>
<span data-ttu-id="efae8-157">Dans l’onglet Accès utilisateur, vous pouvez sélectionner les utilisateurs qui auront accès à cette collection Azure RemoteApp qui inclut uniquement SSMS.</span><span class="sxs-lookup"><span data-stu-id="efae8-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span></span>

![Ajouter un utilisateur][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a><span data-ttu-id="efae8-159">9. Installer l’application cliente Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="efae8-159">9. Install the Azure RemoteApp client application</span></span>
<span data-ttu-id="efae8-160">Vous pouvez télécharger et installer un client Azure RemoteApp ici : [Télécharger | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="efae8-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="efae8-161">Configuration d’Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="efae8-161">Configure Azure SQL server</span></span>
<span data-ttu-id="efae8-162">La seule configuration nécessaire est de s’assurer qu’Azure Services est activé pour le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="efae8-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span></span> <span data-ttu-id="efae8-163">Si vous utilisez cette solution, vous n’avez pas besoin d’ajouter des adresses IP pour ouvrir le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="efae8-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span></span> <span data-ttu-id="efae8-164">Le trafic réseau autorisé vers le serveur SQL Server provient d’autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="efae8-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span></span>

![Autoriser dans Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="efae8-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="efae8-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="efae8-167">La MFA peut être activée spécifiquement pour cette application.</span><span class="sxs-lookup"><span data-stu-id="efae8-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="efae8-168">Accédez à l’onglet Applications d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="efae8-168">Go to the Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="efae8-169">Vous trouverez une entrée correspondant à Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="efae8-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="efae8-170">Si vous cliquez sur cette application et que vous la configurez, la page suivante s’affiche et vous permet d’activer la MFA pour cette application.</span><span class="sxs-lookup"><span data-stu-id="efae8-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span></span>

![Activer la MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="efae8-172">Auditer l’activité utilisateur avec Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="efae8-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="efae8-173">Si vous ne possédez pas Azure AD Premium, vous devez alors l’activer dans la section Licences de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="efae8-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span></span> <span data-ttu-id="efae8-174">L’édition Premium étant activée, vous pouvez affecter des utilisateurs au niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="efae8-174">With Premium enabled, you can assign users to the Premium level.</span></span>

<span data-ttu-id="efae8-175">Lorsque vous accédez à un utilisateur dans Azure Active Directory, vous pouvez cliquer sur l’onglet Activité pour afficher les informations de connexion pour Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="efae8-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efae8-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="efae8-176">Next steps</span></span>
<span data-ttu-id="efae8-177">Après avoir effectué toutes les étapes ci-dessus, vous serez en mesure d’exécuter le client Azure RemoteApp et de vous connecter avec un utilisateur affecté.</span><span class="sxs-lookup"><span data-stu-id="efae8-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="efae8-178">SSMS est présenté comme étant l’une de vos applications, et vous pouvez l’exécuter comme s’il était installé sur votre ordinateur avec un accès à Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="efae8-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span></span>

<span data-ttu-id="efae8-179">Pour plus d'informations sur l'établissement d'une connexion avec la base de données SQL, consultez la page [Se connecter à la base de données SQL avec SQL Server Management Studio et exécuter un exemple de requête T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="efae8-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="efae8-180">C’est tout pour le moment.</span><span class="sxs-lookup"><span data-stu-id="efae8-180">That's everything for now.</span></span> <span data-ttu-id="efae8-181">Vous n’avez plus qu’à l’utiliser !</span><span class="sxs-lookup"><span data-stu-id="efae8-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png