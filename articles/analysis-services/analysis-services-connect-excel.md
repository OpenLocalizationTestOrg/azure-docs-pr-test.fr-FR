---
title: "Se connecter à Azure Analysis Services avec Excel | Microsoft Docs"
description: "Découvrez comment vous connecter à un serveur Azure Analysis Services à l’aide d’Excel."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: d51b6980120f1cf9bc8d053d463a73ac600b915f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="68092-103">Connexion avec Excel</span><span class="sxs-lookup"><span data-stu-id="68092-103">Connect with Excel</span></span>

<span data-ttu-id="68092-104">Une fois que vous avez créé un serveur dans Azure avant d’y déployer un modèle tabulaire, vous êtes prêt à vous y connecter et à explorer les données.</span><span class="sxs-lookup"><span data-stu-id="68092-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="68092-105">Se connecter dans Excel</span><span class="sxs-lookup"><span data-stu-id="68092-105">Connect in Excel</span></span>

<span data-ttu-id="68092-106">La connexion à un serveur dans Excel est prise en charge grâce à la fonction Obtenir les données dans Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="68092-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="68092-107">La connexion à l’aide de l’Assistant d’importation de table dans Power Pivot n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="68092-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="68092-108">**Se connecter dans Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="68092-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="68092-109">Dans Excel 2016, sur le ruban **Données**, cliquez sur **Obtenir les données externes** > **À partir d’autres sources** > **À partir d’Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="68092-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="68092-110">Dans l’Assistant de connexion de données, dans **Nom du serveur**, entrez le nom du serveur avec le protocole et l’URI.</span><span class="sxs-lookup"><span data-stu-id="68092-110">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="68092-111">Ensuite, dans **Informations d’identification d’ouverture de session**, sélectionnez **Utiliser le nom d’utilisateur et le mot de passe suivants**, puis tapez le nom d’utilisateur professionnel, par exemple nancy@adventureworks.com, et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="68092-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Se connecter à partir de l’ouverture de session Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="68092-113">Dans **Sélectionner une base de données et une table**, sélectionnez la base de données et un modèle ou une perspective, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="68092-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Se connecter à partir du modèle de sélection Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="68092-115">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="68092-115">See also</span></span>
<span data-ttu-id="68092-116">[Bibliothèques clientes](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="68092-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="68092-117">Gérer votre serveur</span><span class="sxs-lookup"><span data-stu-id="68092-117">Manage your server</span></span>](analysis-services-manage.md)     


