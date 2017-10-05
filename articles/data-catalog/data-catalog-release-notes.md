---
title: "Notes de publication sur Azure Data Catalog | Microsoft Docs"
description: "Notes de publication d’Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: d3db9bee0558cac5fb4f5b8fb4ab67a35ce0f141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="9f483-103">Notes de publication sur Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="9f483-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="9f483-104">Notes pour la version du 20 novembre 2015 d’Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="9f483-104">Notes for the November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="9f483-105">Ouverture de sources de données dans Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="9f483-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="9f483-106">Lorsque vous utilisez l'option « Ouvrir dans Power BI Desktop » à partir du portail **Catalogue de données Azure** , les utilisateurs peuvent rencontrer un ou deux problèmes dans l'application Power BI Desktop :</span><span class="sxs-lookup"><span data-stu-id="9f483-106">When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:</span></span>

* <span data-ttu-id="9f483-107">Une boîte de dialogue avec le titre « Impossible d’ouvrir le document » s'affiche.</span><span class="sxs-lookup"><span data-stu-id="9f483-107">A dialog box with the title "Unable to Open Document" is displayed</span></span>
* <span data-ttu-id="9f483-108">L'application Power BI Desktop s'ouvre, mais le fichier semble être vide.</span><span class="sxs-lookup"><span data-stu-id="9f483-108">The Power BI Desktop application opens, but the file appears to be empty</span></span>

<span data-ttu-id="9f483-109">Pour chaque cas, le problème peut être résolu en téléchargeant et en installant la dernière version de Power BI Desktop sur [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="9f483-109">For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="9f483-110">Notes pour la version du 13 novembre 2015 d’Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="9f483-110">Notes for the November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-teradata"></a><span data-ttu-id="9f483-111">Inscription et connexion sur Teradata</span><span class="sxs-lookup"><span data-stu-id="9f483-111">Registering and connecting to Teradata</span></span>
<span data-ttu-id="9f483-112">Lors de la connexion aux sources de données Teradata, les utilisateurs doivent avoir installé le pilote ODBC Teradata qui correspond au nombre de bits (32 ou 64) du logiciel utilisé.</span><span class="sxs-lookup"><span data-stu-id="9f483-112">When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

<span data-ttu-id="9f483-113">À compter de cette date de version d’ADC, le [pilote ODBC de Teradata pour Windows (version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) le plus récent est compatible avec Office 2013, mais pas avec Office 2016.</span><span class="sxs-lookup"><span data-stu-id="9f483-113">As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="9f483-114">Notes pour la version du 13 juillet 2015 d’Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="9f483-114">Notes for the July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-oracle-database"></a><span data-ttu-id="9f483-115">Inscription et connexion à Oracle Database</span><span class="sxs-lookup"><span data-stu-id="9f483-115">Registering and connecting to Oracle Database</span></span>
<span data-ttu-id="9f483-116">Lors de la connexion aux sources de données Oracle Database, les utilisateurs doivent avoir installé les pilotes Oracle appropriés qui correspondent au nombre de bits (32 ou 64) du logiciel utilisé.</span><span class="sxs-lookup"><span data-stu-id="9f483-116">When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

* <span data-ttu-id="9f483-117">Lors de l’inscription des sources de données Oracle sur un ordinateur exécutant Windows 32 bits, les pilotes Oracle 32 bits seront utilisés.</span><span class="sxs-lookup"><span data-stu-id="9f483-117">When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="9f483-118">Lors de l’inscription des sources de données Oracle sur un ordinateur exécutant Windows 64 bits, les pilotes Oracle 64 bits seront utilisés.</span><span class="sxs-lookup"><span data-stu-id="9f483-118">When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="9f483-119">Lors de la connexion aux sources de données Oracle à l'aide d'Excel sur un ordinateur exécutant la version 32 bits de Microsoft Office, y compris sur Windows 64 bits, les pilotes Oracle 32 bits seront utilisés.</span><span class="sxs-lookup"><span data-stu-id="9f483-119">When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="9f483-120">Lors de la connexion aux sources de données Oracle à l'aide d'Excel sur un ordinateur exécutant la version 64 bits de Microsoft Office, les pilotes Oracle 64 bits seront utilisés.</span><span class="sxs-lookup"><span data-stu-id="9f483-120">When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a><span data-ttu-id="9f483-121">Inscription et connexion à SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="9f483-121">Registering and connecting to SQL Server Reporting Services</span></span>
<span data-ttu-id="9f483-122">La prise en charge des sources de données SQL Server Reporting Services (SSRS) est actuellement limitée aux serveurs en mode natif.</span><span class="sxs-lookup"><span data-stu-id="9f483-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only.</span></span> <span data-ttu-id="9f483-123">La prise en charge de SSRS en mode SharePoint sera disponible dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9f483-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="9f483-124">Ouverture des ressources de données dans Excel</span><span class="sxs-lookup"><span data-stu-id="9f483-124">Opening data assets in Excel</span></span>
<span data-ttu-id="9f483-125">Au moment de l’ouverture des ressources de données dans Microsoft Excel à partir du portail **Azure Data Catalog**, les utilisateurs peuvent voir apparaître la boîte de dialogue **Avis de sécurité Microsoft Excel**.</span><span class="sxs-lookup"><span data-stu-id="9f483-125">When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="9f483-126">Il s’agit là d’un comportement attendu standard et les utilisateurs peuvent sélectionner **Activer** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="9f483-126">This is standard, expected behavior, and users can select **Enable** to continue.</span></span>

<span data-ttu-id="9f483-127">Pour plus d’informations, consultez [Activer ou désactiver les alertes de sécurité relatives aux liens et aux fichiers de sites web suspects](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="9f483-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="9f483-128">Configuration du proxy et de la stratégie, et inscription de la source de données</span><span class="sxs-lookup"><span data-stu-id="9f483-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="9f483-129">Les utilisateurs parviennent parfois à se connecter au portail d’Azure Data Catalog, mais lorsqu'ils tentent de se connecter à l'outil de référencement de la source de données, un message d'erreur s’affiche et les empêche de se connecter.</span><span class="sxs-lookup"><span data-stu-id="9f483-129">Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="9f483-130">Deux causes possibles à ce problème de comportement :</span><span class="sxs-lookup"><span data-stu-id="9f483-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="9f483-131">**Cause n°1 : configuration d’Active Directory Federation Services** L’outil d’inscription de la source de données utilise l’authentification par formulaire pour valider les connexions utilisateur avec Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9f483-131">**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="9f483-132">Pour une ouverture de session réussie, l'authentification par formulaire doit être activée dans la stratégie d'authentification globale par un administrateur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9f483-132">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="9f483-133">Cette erreur peut également survenir lorsque l'utilisateur est connecté au réseau d'entreprise ou lorsque l'utilisateur se connecte en dehors du réseau d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="9f483-133">In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network.</span></span> <span data-ttu-id="9f483-134">La stratégie d'authentification globale permet d’activer séparément des méthodes d'authentification pour les connexions intranet et extranet.</span><span class="sxs-lookup"><span data-stu-id="9f483-134">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="9f483-135">Des erreurs de connexion peuvent survenir si l'authentification par formulaire n'est pas activée pour le réseau à partir duquel l'utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="9f483-135">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

<span data-ttu-id="9f483-136">Pour plus d’informations, consultez [Configuration des stratégies d’authentification](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f483-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="9f483-137">**Cause n°2 : configuration du proxy réseau** Si le réseau d’entreprise utilise un serveur proxy, l’outil d’inscription ne peut peut-être pas se connecter à Azure Active Directory via le proxy.</span><span class="sxs-lookup"><span data-stu-id="9f483-137">**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy.</span></span> <span data-ttu-id="9f483-138">Les utilisateurs peuvent s’assurer de l'outil d'inscription en modifiant le fichier de configuration de l'outil, et en ajoutant au fichier la section suivante :</span><span class="sxs-lookup"><span data-stu-id="9f483-138">Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="9f483-139">Pour localiser le fichier RegistrationTool.exe.config, lancez l'outil d'inscription, puis ouvrez l'utilitaire Gestionnaire des tâches de Windows.</span><span class="sxs-lookup"><span data-stu-id="9f483-139">To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility.</span></span> <span data-ttu-id="9f483-140">Sous l'onglet Détails du Gestionnaire des tâches, cliquez avec le bouton droit sur RegistrationTool.exe et choisissez Ouvrir l'emplacement du fichier dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="9f483-140">On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.</span></span>
