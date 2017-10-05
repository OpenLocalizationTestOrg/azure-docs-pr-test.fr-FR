---
title: "Connexion à Azure Analysis Services | Microsoft Docs"
description: "Découvrez comment vous connecter à un serveur Analysis Services dans Azure et en obtenir les données."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: deb3ef28d20decef01826450bd6091f87dd069de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-an-azure-analysis-services-server"></a><span data-ttu-id="9d1a4-103">Se connecter à un serveur Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="9d1a4-103">Connect to an Azure Analysis Services server</span></span>

<span data-ttu-id="9d1a4-104">Cet article décrit la connexion à un serveur à l’aide de la modélisation des données et des applications de gestion telles que SQL Server Management Studio (SSMS) ou SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="9d1a4-104">This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="9d1a4-105">La connexion est également possible avec des applications de création de rapports client telles que Microsoft Excel, Power BI Desktop ou des applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="9d1a4-106">Les connexions à Azure Analysis Services utilisent HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-106">Connections to Azure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="9d1a4-107">Bibliothèques clientes</span><span class="sxs-lookup"><span data-stu-id="9d1a4-107">Client libraries</span></span>
[<span data-ttu-id="9d1a4-108">Obtention des bibliothèques clientes les plus récentes</span><span class="sxs-lookup"><span data-stu-id="9d1a4-108">Get the latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="9d1a4-109">Toutes les connexions à un serveur, quel que soit le type, nécessitent des bibliothèques clientes AMO, ADOMD.NET et OLEDB mises à jour pour interagir avec un serveur Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-109">All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server.</span></span> <span data-ttu-id="9d1a4-110">Pour SSMS, SSDT, Excel 2016 et Power BI, les bibliothèques clientes les plus récentes sont installées ou mises à jour avec les versions mensuelles.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-110">For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="9d1a4-111">Toutefois, dans certains cas, il est possible qu’une application ne dispose pas de la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-111">However, in some cases, it's possible an application may not have the latest.</span></span> <span data-ttu-id="9d1a4-112">Par exemple, lorsque les stratégies retardent les mises à jour, ou lorsque les mises à jour Office 365 se trouvent sur le canal différé.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-112">For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="9d1a4-113">Nom du serveur</span><span class="sxs-lookup"><span data-stu-id="9d1a4-113">Server name</span></span>

<span data-ttu-id="9d1a4-114">Lorsque vous créez un serveur Analysis Services dans Azure, vous spécifiez un nom unique ainsi que la région dans laquelle le serveur doit être créé.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-114">When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created.</span></span> <span data-ttu-id="9d1a4-115">Lorsque vous spécifiez le nom du serveur dans une connexion, le schéma d’affectation de noms du serveur est le suivant :</span><span class="sxs-lookup"><span data-stu-id="9d1a4-115">When specifying the server name in a connection, the server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="9d1a4-116">Où protocol est la chaîne **asazure**, region est l’URI où le serveur a été créé (par exemple, westus.asazure.windows.net) et servername est le nom de votre serveur unique au sein de la région.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-116">Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.</span></span>

### <a name="get-the-server-name"></a><span data-ttu-id="9d1a4-117">Obtenir le nom du serveur</span><span class="sxs-lookup"><span data-stu-id="9d1a4-117">Get the server name</span></span>
<span data-ttu-id="9d1a4-118">Dans **Portail Azure** > Serveur > **Présentation** > **Nom du serveur**, copiez le nom du serveur entier.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-118">In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name.</span></span> <span data-ttu-id="9d1a4-119">Si d’autres utilisateurs de votre entreprise se connectent également à ce serveur, vous pouvez partager ce nom de serveur avec eux.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-119">If other users in your organization are connecting to this server too, you can share this server name with them.</span></span> <span data-ttu-id="9d1a4-120">Lorsque vous spécifiez un nom de serveur, le chemin d’accès complet doit être utilisé.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-120">When specifying a server name, the entire path must be used.</span></span>

![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="9d1a4-122">Chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="9d1a4-122">Connection string</span></span>

<span data-ttu-id="9d1a4-123">Lorsque vous vous connectez à Azure Analysis Services à l’aide du modèle d’objet tabulaire, utilisez les formats de chaîne de connexion suivants :</span><span class="sxs-lookup"><span data-stu-id="9d1a4-123">When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="9d1a4-124">Authentification Azure Active Directory intégrée</span><span class="sxs-lookup"><span data-stu-id="9d1a4-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="9d1a4-125">L’authentification intégrée utilise le cache d’informations d’identification Azure Active Directory s’il est disponible.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-125">Integrated authentication picks up the Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="9d1a4-126">Si ce n’est pas le cas, la fenêtre de connexion Azure s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-126">If not, the Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="9d1a4-127">Authentification Active Directory Azure avec le nom d’utilisateur et le mot de passe</span><span class="sxs-lookup"><span data-stu-id="9d1a4-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="9d1a4-128">Authentification Windows (sécurité intégrée)</span><span class="sxs-lookup"><span data-stu-id="9d1a4-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="9d1a4-129">Utilisez le compte Windows qui exécute le processus en cours.</span><span class="sxs-lookup"><span data-stu-id="9d1a4-129">Use the Windows account running the current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="9d1a4-130">Connexion à l’aide d’un fichier .odc</span><span class="sxs-lookup"><span data-stu-id="9d1a4-130">Connect using an .odc file</span></span>
<span data-ttu-id="9d1a4-131">Avec les versions antérieures d’Excel, les utilisateurs peuvent se connecter à un serveur Azure Analysis Services à l’aide d’un fichier Office Data Connection (.odc).</span><span class="sxs-lookup"><span data-stu-id="9d1a4-131">With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="9d1a4-132">Pour en savoir plus, consultez [Créer un fichier Office Data Connection (.odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="9d1a4-132">To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9d1a4-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d1a4-133">Next steps</span></span>
<span data-ttu-id="9d1a4-134">[Connexion avec Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="9d1a4-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="9d1a4-135">[Connexion avec Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="9d1a4-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="9d1a4-136">Gérer votre serveur</span><span class="sxs-lookup"><span data-stu-id="9d1a4-136">Manage your server</span></span>](analysis-services-manage.md)   

