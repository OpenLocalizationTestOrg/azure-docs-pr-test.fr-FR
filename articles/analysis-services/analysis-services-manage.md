---
title: aaaManage Azure Analysis Services | Documents Microsoft
description: "Découvrez comment toomanage un Analysis Services server dans Azure."
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
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="7835f-103">Gérer Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7835f-103">Manage Analysis Services</span></span>
<span data-ttu-id="7835f-104">Une fois que vous avez créé un serveur Analysis Services dans Azure, il est peut-être certaines des tâches d’administration et de gestion vous devez tooperform immédiatement ou plus tard bas hello route.</span><span class="sxs-lookup"><span data-stu-id="7835f-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="7835f-105">Par exemple, exécutez le traitement des données d’actualisation toohello, contrôler qui peut accéder aux modèles de hello sur votre serveur, ou surveiller l’intégrité de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="7835f-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="7835f-106">Certaines tâches de gestion ne peuvent être effectuées que dans le portail Azure, d’autres dans SQL Server Management Studio (SSMS), et certaines tâches encore peuvent être effectuées dans les deux.</span><span class="sxs-lookup"><span data-stu-id="7835f-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="7835f-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="7835f-107">Azure portal</span></span>
<span data-ttu-id="7835f-108">[Portail Azure](http://portal.azure.com/) est où vous pouvez créer et supprimer des serveurs, surveillance des ressources serveur, modifier la taille et gérer les utilisateurs ayant des serveurs d’accès tooyour.</span><span class="sxs-lookup"><span data-stu-id="7835f-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="7835f-109">Si vous rencontrez des problèmes, vous pouvez également envoyer une demande de support.</span><span class="sxs-lookup"><span data-stu-id="7835f-109">If you're having some problems, you can also submit a support request.</span></span>

![Obtenir le nom du serveur dans Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="7835f-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="7835f-111">SQL Server Management Studio</span></span>
<span data-ttu-id="7835f-112">La connexion serveur tooyour dans Azure est identique à la connexion tooa instance de serveur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="7835f-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="7835f-113">À partir de SSMS, vous pouvez effectuer un grand nombre de hello même tâches telles que les données de processus ou créer un script de traitement, gérer les rôles et utiliser PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7835f-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="7835f-115">Téléchargement et installation de SSMS</span><span class="sxs-lookup"><span data-stu-id="7835f-115">Download and install SSMS</span></span>
<span data-ttu-id="7835f-116">tooget tous hello dernières fonctionnalités et expérience plus lissé de hello lors de la connexion du serveur de Azure Analysis Services tooyour, veillez à ce que vous utilisez la version la plus récente de SSMS hello.</span><span class="sxs-lookup"><span data-stu-id="7835f-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="7835f-117">[Téléchargez SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="7835f-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="7835f-118">tooconnect avec SSMS</span><span class="sxs-lookup"><span data-stu-id="7835f-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="7835f-119">Lors de l’utilisation de SSMS, avant la connexion tooyour messages hello du serveur première fois, vérifiez que votre nom d’utilisateur est inclus dans le groupe d’administrateurs de Services d’analyse hello.</span><span class="sxs-lookup"><span data-stu-id="7835f-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="7835f-120">toolearn, voir [les administrateurs de serveur](#server-administrators) plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="7835f-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="7835f-121">Avant de vous connectez, vous devez le nom du serveur tooget hello.</span><span class="sxs-lookup"><span data-stu-id="7835f-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="7835f-122">Dans **portail Azure** > serveur > **vue d’ensemble** > **nom du serveur**, copier le nom de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="7835f-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="7835f-124">Dans SSMS > **Explorateur d’objets**, cliquez sur **Se connecter** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="7835f-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="7835f-125">Bonjour **connecter tooServer** boîte de dialogue, coller dans le nom du serveur hello, puis en **authentification**, choisissez une des hello les types d’authentification suivants :</span><span class="sxs-lookup"><span data-stu-id="7835f-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="7835f-126">**L’authentification Windows** toouse vos informations d’identification Windows domaine\nom d’utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7835f-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="7835f-127">**Authentification du mot de passe Active Directory** toouse un compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="7835f-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="7835f-128">Par exemple, lors d’une connexion à partir d’un ordinateur non joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="7835f-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="7835f-129">**L’authentification Active Directory universel** toouse [non interactif ou multi-Factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7835f-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Se connecter dans SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="7835f-131">Administrateurs de serveur et utilisateurs de base de données</span><span class="sxs-lookup"><span data-stu-id="7835f-131">Server administrators and database users</span></span>
<span data-ttu-id="7835f-132">Dans Azure Analysis Services, il existe deux types d’utilisateur : les administrateurs de serveur et les utilisateurs de base de données.</span><span class="sxs-lookup"><span data-stu-id="7835f-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="7835f-133">Les deux types d’utilisateur doivent exister dans Azure Active Directory et être spécifiés par adresse de messagerie d’organisation ou UPN.</span><span class="sxs-lookup"><span data-stu-id="7835f-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="7835f-134">toolearn, voir [d’authentification et les autorisations utilisateur](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="7835f-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="7835f-135">Résolution des problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="7835f-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="7835f-136">Lors de la connexion à l’aide de SSMS, si vous rencontrez des problèmes, vous devrez peut-être le cache de connexion tooclear hello.</span><span class="sxs-lookup"><span data-stu-id="7835f-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="7835f-137">Rien n’est toodisc mis en cache.</span><span class="sxs-lookup"><span data-stu-id="7835f-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="7835f-138">processus de connexion tooclear hello cache, fermez et redémarrez hello.</span><span class="sxs-lookup"><span data-stu-id="7835f-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7835f-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7835f-139">Next steps</span></span>
<span data-ttu-id="7835f-140">Si vous n’avez pas déjà déployé un nouveau serveur de tooyour modèle tabulaire, est judicieux.</span><span class="sxs-lookup"><span data-stu-id="7835f-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="7835f-141">toolearn, voir [déployer tooAzure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7835f-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="7835f-142">Si vous avez déployé un serveur tooyour de modèle, vous êtes tooit tooconnect prêt à l’aide d’un client ou un navigateur.</span><span class="sxs-lookup"><span data-stu-id="7835f-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="7835f-143">toolearn, voir [obtenir des données à partir d’Azure Analysis Services](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7835f-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

