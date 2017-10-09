---
title: "aaaConnect tooSQL de base de données à l’aide de SQL Server Management Studio dans Azure RemoteApp | Documents Microsoft"
description: "Utilisez ce didacticiel toolearn comment toouse SQL Server Management Studio dans Azure RemoteApp pour la sécurité et les performances lors de la connexion tooSQL de base de données"
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
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="c17e4-103">Utilisez SQL Server Management Studio dans Azure RemoteApp tooconnect tooSQL base de données</span><span class="sxs-lookup"><span data-stu-id="c17e4-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c17e4-104">Azure RemoteApp n’est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="c17e4-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="c17e4-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c17e4-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="c17e4-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="c17e4-106">Introduction</span></span>
<span data-ttu-id="c17e4-107">Ce didacticiel vous montre comment toouse SQL Server Management Studio (SSMS) dans Azure RemoteApp tooconnect tooSQL base de données.</span><span class="sxs-lookup"><span data-stu-id="c17e4-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="c17e4-108">Il vous guide tout au long des processus de hello de configuration SQL Server Management Studio dans Azure RemoteApp, explique les avantages de hello et montre les fonctionnalités de sécurité que vous pouvez utiliser dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c17e4-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="c17e4-109">**Estimation du temps toocomplete :** 45 minutes</span><span class="sxs-lookup"><span data-stu-id="c17e4-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="c17e4-110">SSMS dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c17e4-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="c17e4-111">Azure RemoteApp est un service RDS d’Azure, qui fournit des applications.</span><span class="sxs-lookup"><span data-stu-id="c17e4-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="c17e4-112">Vous pouvez obtenir plus d’informations sur ce service ici : [Qu’est-ce que RemoteApp ?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c17e4-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="c17e4-113">En cours d’exécution dans Azure RemoteApp donne SSMS vous hello même expérience en exécutant SSMS localement.</span><span class="sxs-lookup"><span data-stu-id="c17e4-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Capture d’écran illustrant SSMS en cours d’exécution dans Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="c17e4-115">Avantages</span><span class="sxs-lookup"><span data-stu-id="c17e4-115">Benefits</span></span>
<span data-ttu-id="c17e4-116">Il existe de nombreux avantages toousing SSMS dans Azure RemoteApp, y compris :</span><span class="sxs-lookup"><span data-stu-id="c17e4-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="c17e4-117">Le port 1433 sur le serveur SQL Azure n’a pas de toobe exposé en externe (en dehors d’Azure).</span><span class="sxs-lookup"><span data-stu-id="c17e4-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="c17e4-118">Aucun tookeep besoin, ajout et suppression d’adresses IP dans le pare-feu de serveur SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c17e4-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="c17e4-119">Toutes les connexions Azure RemoteApp ont lieu via HTTPS sur le port 443 à l’aide du protocole RDP (Remote Desktop Protocol) chiffré.</span><span class="sxs-lookup"><span data-stu-id="c17e4-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="c17e4-120">SSMS est multi-utilisateur et évolutif.</span><span class="sxs-lookup"><span data-stu-id="c17e4-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="c17e4-121">Il existe un gain de performances de l’utilisation de SSMS Bonjour même région que hello de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="c17e4-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="c17e4-122">Vous pouvez auditer l’utilisation d’Azure RemoteApp avec l’édition Premium d’Azure Active Directory qui a des rapports d’activité utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c17e4-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="c17e4-123">Vous pouvez activer l’authentification multifacteur (MFA).</span><span class="sxs-lookup"><span data-stu-id="c17e4-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="c17e4-124">Accès SSMS n’importe où lorsque vous utilisez une de hello clients pris en charge Azure RemoteApp qui inclut iOS, Android, Mac, Windows Phone et les PC Windows.</span><span class="sxs-lookup"><span data-stu-id="c17e4-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="c17e4-125">Créer la collection de hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c17e4-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="c17e4-126">Voici votre collection Azure RemoteApp avec SSMS hello étapes toocreate :</span><span class="sxs-lookup"><span data-stu-id="c17e4-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="c17e4-127">1. Créer une machine virtuelle Windows à partir d’une image</span><span class="sxs-lookup"><span data-stu-id="c17e4-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="c17e4-128">Utilisez hello Image « Windows Server à distance Bureau Session hôte Windows Server 2012 R2 » à partir de hello galerie toomake votre nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c17e4-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="c17e4-129">2. Installer SSMS à partir de SQL Express</span><span class="sxs-lookup"><span data-stu-id="c17e4-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="c17e4-130">Accédez à hello nouvelle machine virtuelle et de parcourir la page de téléchargement toothis : [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="c17e4-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="c17e4-131">Il existe un téléchargement de tooonly option SSMS.</span><span class="sxs-lookup"><span data-stu-id="c17e4-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="c17e4-132">Après le téléchargement, allez dans le répertoire d’installation hello et exécuter le programme d’installation tooinstall SSMS.</span><span class="sxs-lookup"><span data-stu-id="c17e4-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="c17e4-133">Vous devez également tooinstall SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="c17e4-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="c17e4-134">Vous pouvez le télécharger ici : [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="c17e4-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="c17e4-135">SQL Server 2014 Service Pack 1 inclut des fonctionnalités essentielles pour l’utilisation de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c17e4-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="c17e4-136">3. Exécuter le script de validation et Sysprep</span><span class="sxs-lookup"><span data-stu-id="c17e4-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="c17e4-137">Sur hello bureau Hello machine virtuelle est un script PowerShell appelé Validate.</span><span class="sxs-lookup"><span data-stu-id="c17e4-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="c17e4-138">Exécutez-le en double-cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="c17e4-138">Run this by double-clicking.</span></span> <span data-ttu-id="c17e4-139">Il vérifie que hello machine virtuelle est prête toobe utilisé pour l’hébergement à distance des applications.</span><span class="sxs-lookup"><span data-stu-id="c17e4-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="c17e4-140">Lors de la vérification est terminée, il demande toorun sysprep - choisissez toorun il.</span><span class="sxs-lookup"><span data-stu-id="c17e4-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="c17e4-141">Quand sysprep se termine, il s’arrêtera hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c17e4-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="c17e4-142">toolearn savoir plus sur la création d’une image Azure RemoteApp, consultez : [comment toocreate un modèle RemoteApp de l’image dans Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="c17e4-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="c17e4-143">4. Capturer l’image</span><span class="sxs-lookup"><span data-stu-id="c17e4-143">4. Capture image</span></span>
<span data-ttu-id="c17e4-144">Lorsque hello machine virtuelle est arrêtée, recherchez-le dans le portail actuel de hello et capturer.</span><span class="sxs-lookup"><span data-stu-id="c17e4-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="c17e4-145">toolearn savoir plus sur la capture d’une image, consultez [capturer une image d’une machine virtuelle de Microsoft Azure créée avec le modèle de déploiement classique de hello](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c17e4-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="c17e4-146">5. Ajouter des images de modèle RemoteApp tooAzure</span><span class="sxs-lookup"><span data-stu-id="c17e4-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="c17e4-147">Bonjour section Azure RemoteApp du portail en cours de hello, onglet des Images de modèle toohello, cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="c17e4-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="c17e4-148">Dans la boîte de hello, sélectionnez « Importer une image à partir de votre bibliothèque de Machines virtuelles », puis choisissez hello Image que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="c17e4-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="c17e4-149">6. Créer une collection cloud</span><span class="sxs-lookup"><span data-stu-id="c17e4-149">6. Create cloud collection</span></span>
<span data-ttu-id="c17e4-150">Dans le portail actuel hello, créez une nouvelle Collection de Cloud de RemoteApp Azure.</span><span class="sxs-lookup"><span data-stu-id="c17e4-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="c17e4-151">Choisissez hello Image de modèle que vous venez d’importer avec SSMS installé dessus.</span><span class="sxs-lookup"><span data-stu-id="c17e4-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Créer une collection cloud][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="c17e4-153">7. Publier SSMS</span><span class="sxs-lookup"><span data-stu-id="c17e4-153">7. Publish SSMS</span></span>
<span data-ttu-id="c17e4-154">Sur la publication d’onglet de votre nouvelle collection cloud, cliquez sur Publier une application à partir de hello hello Menu Démarrer, puis choisissez SSMS à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="c17e4-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![Publier une application][5]

### <a name="8-add-users"></a><span data-ttu-id="c17e4-156">8. Ajouter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c17e4-156">8. Add users</span></span>
<span data-ttu-id="c17e4-157">Sur l’onglet de l’accès utilisateur hello, vous pouvez sélectionner les utilisateurs de hello qui auront accès toothis Azure RemoteApp ensemble qui inclut uniquement les SSMS.</span><span class="sxs-lookup"><span data-stu-id="c17e4-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Ajouter un utilisateur][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="c17e4-159">9. Installer l’application de client hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c17e4-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="c17e4-160">Vous pouvez télécharger et installer un client Azure RemoteApp ici : [Télécharger | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="c17e4-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="c17e4-161">Configuration d’Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="c17e4-161">Configure Azure SQL server</span></span>
<span data-ttu-id="c17e4-162">Hello uniquement de la configuration requise est tooensure Services Azure est activée pour le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="c17e4-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="c17e4-163">Si vous utilisez cette solution, puis il est inutile tooadd toutes les adresses IP tooopen le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="c17e4-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="c17e4-164">le trafic réseau Hello autorisé toohello SQL Server est à partir d’autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="c17e4-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Autoriser dans Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="c17e4-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="c17e4-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="c17e4-167">La MFA peut être activée spécifiquement pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c17e4-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="c17e4-168">Accédez à onglet d’Applications toohello d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c17e4-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="c17e4-169">Vous trouverez une entrée correspondant à Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c17e4-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="c17e4-170">Si vous cliquez sur cette application, puis configurez, vous verrez la page hello ci-dessous vous permet d’activer l’authentification Multifacteur pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c17e4-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![Activer la MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="c17e4-172">Auditer l’activité utilisateur avec Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="c17e4-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="c17e4-173">Si vous n’avez pas d’Azure AD Premium, vous devez tooturn il sur dans hello section des licences de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c17e4-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="c17e4-174">Premium est activé, vous pouvez assigner des utilisateurs au niveau du toohello Premium.</span><span class="sxs-lookup"><span data-stu-id="c17e4-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="c17e4-175">Lorsque vous passez tooa utilisateur dans Azure Active Directory, vous pouvez ensuite accéder toohello activité onglet toosee connexion informations tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c17e4-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c17e4-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c17e4-176">Next steps</span></span>
<span data-ttu-id="c17e4-177">Après avoir effectué hello toutes les étapes ci-dessus, vous être en mesure de toorun hello Azure RemoteApp client et reconnectez-vous avec un utilisateur affecté.</span><span class="sxs-lookup"><span data-stu-id="c17e4-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="c17e4-178">Vous n’aurez SSMS comme l’un de vos applications, et vous pouvez l’exécuter comme vous le feriez s’il était installé sur votre ordinateur avec tooAzure accéder à SQL server.</span><span class="sxs-lookup"><span data-stu-id="c17e4-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="c17e4-179">Pour plus d’informations sur la façon dont toomake hello tooSQL de connexion de base de données, consultez [connecter tooSQL de base de données avec SQL Server Management Studio et exécuter un exemple de requête T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="c17e4-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="c17e4-180">C’est tout pour le moment.</span><span class="sxs-lookup"><span data-stu-id="c17e4-180">That's everything for now.</span></span> <span data-ttu-id="c17e4-181">Vous n’avez plus qu’à l’utiliser !</span><span class="sxs-lookup"><span data-stu-id="c17e4-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png