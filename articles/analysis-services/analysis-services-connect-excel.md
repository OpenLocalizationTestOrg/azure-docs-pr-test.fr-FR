---
title: aaaConnect tooAzure Analysis Services avec Excel | Documents Microsoft
description: "Découvrez comment tooconnect tooan Azure Analysis Services serveur à l’aide d’Excel."
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="b1d0b-103">Connexion avec Excel</span><span class="sxs-lookup"><span data-stu-id="b1d0b-103">Connect with Excel</span></span>

<span data-ttu-id="b1d0b-104">Une fois que vous avez créé un serveur dans Azure et déployé un tooit de modèle tabulaire, vous êtes prêt tooconnect et commencez à Explorer les données.</span><span class="sxs-lookup"><span data-stu-id="b1d0b-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="b1d0b-105">Se connecter dans Excel</span><span class="sxs-lookup"><span data-stu-id="b1d0b-105">Connect in Excel</span></span>

<span data-ttu-id="b1d0b-106">La connexion serveur tooa dans Excel est pris en charge à l’aide d’obtenir des données dans Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="b1d0b-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="b1d0b-107">Connexion à l’aide de hello Assistant Importation de Table dans Power Pivot n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b1d0b-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="b1d0b-108">**tooconnect dans Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="b1d0b-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="b1d0b-109">Dans Excel 2016, sur hello **données** du ruban, cliquez sur **obtenir des données externes** > **à partir d’autres Sources** > **à partir d’Analysis Services** .</span><span class="sxs-lookup"><span data-stu-id="b1d0b-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="b1d0b-110">Dans hello Assistant connexion de données dans **nom du serveur**, entrez hello nom du serveur, y compris le protocole et l’URI.</span><span class="sxs-lookup"><span data-stu-id="b1d0b-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="b1d0b-111">Ensuite, dans **informations d’identification d’ouverture de session**, sélectionnez **hello utilisation après le nom d’utilisateur et mot de passe**, puis tapez les nom d’utilisateur d’organisation hello, par exemple nancy@adventureworks.comet le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b1d0b-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Se connecter à partir de l’ouverture de session Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="b1d0b-113">Dans **sélectionner une base de données et de Table**, sélectionnez la base de données hello et perspective ou un modèle, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="b1d0b-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Se connecter à partir du modèle de sélection Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="b1d0b-115">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b1d0b-115">See also</span></span>
<span data-ttu-id="b1d0b-116">[Bibliothèques clientes](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="b1d0b-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="b1d0b-117">Gérer votre serveur</span><span class="sxs-lookup"><span data-stu-id="b1d0b-117">Manage your server</span></span>](analysis-services-manage.md)     


