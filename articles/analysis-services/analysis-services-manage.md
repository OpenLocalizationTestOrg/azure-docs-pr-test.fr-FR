---
title: "Gérer Azure Analysis Services | Microsoft Docs"
description: "Apprenez à gérer un serveur Analysis Services dans Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b897e81351ebee11c292e67ac76ba8202a6f0108
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="63eab-103">Gérer Analysis Services</span><span class="sxs-lookup"><span data-stu-id="63eab-103">Manage Analysis Services</span></span>
<span data-ttu-id="63eab-104">Une fois que vous avez créé un serveur Analysis Services dans Azure, vous devrez peut-être effectuer certaines tâches d’administration et de gestion immédiatement ou un peu plus tard.</span><span class="sxs-lookup"><span data-stu-id="63eab-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="63eab-105">Par exemple, exécuter le traitement d’actualisation des données, contrôler qui peut accéder aux modèles sur votre serveur ou surveiller l’intégrité de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="63eab-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="63eab-106">Certaines tâches de gestion ne peuvent être effectuées que dans le portail Azure, d’autres dans SQL Server Management Studio (SSMS), et certaines tâches encore peuvent être effectuées dans les deux.</span><span class="sxs-lookup"><span data-stu-id="63eab-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="63eab-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="63eab-107">Azure portal</span></span>
<span data-ttu-id="63eab-108">Le [portail Azure](http://portal.azure.com/) est l’endroit où vous pouvez créer et supprimer des serveurs, surveiller les ressources du serveur, modifier la taille et gérer qui a accès à vos serveurs.</span><span class="sxs-lookup"><span data-stu-id="63eab-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="63eab-109">Si vous rencontrez des problèmes, vous pouvez également envoyer une demande de support.</span><span class="sxs-lookup"><span data-stu-id="63eab-109">If you're having some problems, you can also submit a support request.</span></span>

![Obtenir le nom du serveur dans Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="63eab-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="63eab-111">SQL Server Management Studio</span></span>
<span data-ttu-id="63eab-112">La connexion à votre serveur dans Azure revient à vous connecter à une instance de serveur dans votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="63eab-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="63eab-113">À partir de SSMS, vous pouvez effectuer la plupart des tâches identiques comme traiter des données ou créer un script de traitement, gérer des rôles et utiliser PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63eab-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="63eab-115">Téléchargement et installation de SSMS</span><span class="sxs-lookup"><span data-stu-id="63eab-115">Download and install SSMS</span></span>
<span data-ttu-id="63eab-116">Pour obtenir toutes les dernières fonctionnalités et bénéficier d’une expérience parfaitement fluide lors de la connexion à votre serveur Azure Analysis Services, veillez à utiliser la version la plus récente de SSMS.</span><span class="sxs-lookup"><span data-stu-id="63eab-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="63eab-117">[Téléchargez SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="63eab-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="63eab-118">Pour se connecter avec SSMS</span><span class="sxs-lookup"><span data-stu-id="63eab-118">To connect with SSMS</span></span>
 <span data-ttu-id="63eab-119">Quand vous utilisez SSMS, avant de vous connecter à votre serveur pour la première fois, vérifiez que votre nom d’utilisateur figure dans le groupe Administrateurs Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="63eab-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="63eab-120">Pour plus d’informations, consultez [Administrateurs de serveur](#server-administrators) plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="63eab-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="63eab-121">Avant de vous connecter, vous devez obtenir le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="63eab-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="63eab-122">Dans **Portail Azure** > Serveur > **Présentation** > **Nom du serveur**, copiez le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="63eab-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="63eab-124">Dans SSMS > **Explorateur d’objets**, cliquez sur **Se connecter** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="63eab-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="63eab-125">Dans la boîte de dialogue **Se connecter au serveur**, copiez le nom du serveur puis, dans **Authentification**, choisissez l’un des types d’authentification suivants :</span><span class="sxs-lookup"><span data-stu-id="63eab-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>
   
    <span data-ttu-id="63eab-126">**Authentification Windows** pour utiliser vos informations de domaine, nom d’utilisateur et mot de passe Windows.</span><span class="sxs-lookup"><span data-stu-id="63eab-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="63eab-127">**Authentification par mot de passe Active Directory** pour utiliser un compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="63eab-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="63eab-128">Par exemple, lors d’une connexion à partir d’un ordinateur non joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="63eab-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="63eab-129">**Authentification universelle Active Directory** pour utiliser une [authentification non interactive ou de type Multi-Factor Authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="63eab-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Se connecter dans SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="63eab-131">Administrateurs de serveur et utilisateurs de base de données</span><span class="sxs-lookup"><span data-stu-id="63eab-131">Server administrators and database users</span></span>
<span data-ttu-id="63eab-132">Dans Azure Analysis Services, il existe deux types d’utilisateur : les administrateurs de serveur et les utilisateurs de base de données.</span><span class="sxs-lookup"><span data-stu-id="63eab-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="63eab-133">Les deux types d’utilisateur doivent exister dans Azure Active Directory et être spécifiés par adresse de messagerie d’organisation ou UPN.</span><span class="sxs-lookup"><span data-stu-id="63eab-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="63eab-134">Pour en savoir plus, consultez l’article [Authentification et autorisations utilisateur](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="63eab-134">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="63eab-135">Résolution des problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="63eab-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="63eab-136">Si vous rencontrez des problèmes lors d’une connexion à l’aide de SSMS, vous devrez peut-être effacer le cache de connexion.</span><span class="sxs-lookup"><span data-stu-id="63eab-136">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="63eab-137">Rien n’est mis en cache sur le disque. Pour effacer le cache, fermez et redémarrez le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="63eab-137">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="63eab-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63eab-138">Next steps</span></span>
<span data-ttu-id="63eab-139">Si vous n’avez pas déjà déployé un modèle tabulaire sur votre nouveau serveur, c’est le moment de le faire.</span><span class="sxs-lookup"><span data-stu-id="63eab-139">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="63eab-140">Pour en savoir plus, voir [Déployer sur Azure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="63eab-140">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="63eab-141">Si vous avez déployé un modèle sur votre serveur, vous êtes prêt à vous connecter à celui-ci à l’aide d’un client ou d’un navigateur.</span><span class="sxs-lookup"><span data-stu-id="63eab-141">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="63eab-142">Pour en savoir plus, voir [Obtenir les données du serveur Azure Analysis Services](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="63eab-142">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

