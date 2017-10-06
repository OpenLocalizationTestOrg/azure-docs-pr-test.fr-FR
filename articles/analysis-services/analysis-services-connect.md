---
title: aaaConnect tooAzure Analysis Services | Documents Microsoft
description: "Découvrez comment tooconnect tooand obtenir des données à partir d’un serveur Analysis Services dans Azure."
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
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="45fd7-103">Connecter tooan Azure Analysis Services serveur</span><span class="sxs-lookup"><span data-stu-id="45fd7-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="45fd7-104">Cet article décrit le serveur tooa se connectant à l’aide de la modélisation des données et des applications de gestion telles que SQL Server Management Studio (SSMS) ou SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="45fd7-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="45fd7-105">La connexion est également possible avec des applications de création de rapports client telles que Microsoft Excel, Power BI Desktop ou des applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="45fd7-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="45fd7-106">Connexions tooAzure Analysis Services utilisent HTTPS.</span><span class="sxs-lookup"><span data-stu-id="45fd7-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="45fd7-107">Bibliothèques clientes</span><span class="sxs-lookup"><span data-stu-id="45fd7-107">Client libraries</span></span>
[<span data-ttu-id="45fd7-108">Obtenir les bibliothèques clientes plus récentes hello</span><span class="sxs-lookup"><span data-stu-id="45fd7-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="45fd7-109">Tous les serveur tooa de connexions, quel que soit le type, nécessitent des mises à jour AMO, ADOMD.NET et OLEDB bibliothèques tooconnect tooand interface client avec un serveur Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="45fd7-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="45fd7-110">Pour SSMS, SSDT, Excel 2016 et Power BI, les bibliothèques clientes plus récentes hello sont installés ou mis à jour avec les versions mensuelles.</span><span class="sxs-lookup"><span data-stu-id="45fd7-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="45fd7-111">Toutefois, dans certains cas, il est possible qu'une application ne peut pas avoir plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="45fd7-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="45fd7-112">Par exemple, lorsque le délai de stratégies mises à jour ou des mises à jour Office 365 sont sur hello différé canal.</span><span class="sxs-lookup"><span data-stu-id="45fd7-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="45fd7-113">Nom du serveur</span><span class="sxs-lookup"><span data-stu-id="45fd7-113">Server name</span></span>

<span data-ttu-id="45fd7-114">Lorsque vous créez un serveur Analysis Services dans Azure, vous spécifiez une région de hello et de nom unique où le serveur de hello est toobe créé.</span><span class="sxs-lookup"><span data-stu-id="45fd7-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="45fd7-115">Lorsque vous spécifiez le nom du serveur hello dans une connexion, le schéma d’affectation de noms du serveur hello est :</span><span class="sxs-lookup"><span data-stu-id="45fd7-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="45fd7-116">Où protocol est chaîne **asazure**, région est hello Uri où le serveur de hello a été créé (par exemple, westus.asazure.windows.net) et nom de hello de votre serveur unique au sein de la région de hello servername.</span><span class="sxs-lookup"><span data-stu-id="45fd7-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="45fd7-117">Obtenir le nom du serveur hello</span><span class="sxs-lookup"><span data-stu-id="45fd7-117">Get hello server name</span></span>
<span data-ttu-id="45fd7-118">Dans **portail Azure** > serveur > **vue d’ensemble** > **nom du serveur**, copier le nom de serveur entier hello.</span><span class="sxs-lookup"><span data-stu-id="45fd7-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="45fd7-119">Si autres utilisateurs de votre organisation connectez trop toothis serveur, vous pouvez partager ce nom de serveur avec eux.</span><span class="sxs-lookup"><span data-stu-id="45fd7-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="45fd7-120">Lorsque vous spécifiez un nom de serveur, le chemin d’accès complet de hello doit être utilisé.</span><span class="sxs-lookup"><span data-stu-id="45fd7-120">When specifying a server name, hello entire path must be used.</span></span>

![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="45fd7-122">Chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="45fd7-122">Connection string</span></span>

<span data-ttu-id="45fd7-123">Lors de la connexion tooAzure Analysis Services à l’aide de hello modèle d’objet tabulaire, hello utilisation suivant les formats de chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="45fd7-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="45fd7-124">Authentification Azure Active Directory intégrée</span><span class="sxs-lookup"><span data-stu-id="45fd7-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="45fd7-125">L’authentification intégrée, récupère hello cache d’informations d’identification Azure Active Directory s’il est disponible.</span><span class="sxs-lookup"><span data-stu-id="45fd7-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="45fd7-126">Le cas contraire, la fenêtre de connexion Azure hello est affichée.</span><span class="sxs-lookup"><span data-stu-id="45fd7-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="45fd7-127">Authentification Active Directory Azure avec le nom d’utilisateur et le mot de passe</span><span class="sxs-lookup"><span data-stu-id="45fd7-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="45fd7-128">Authentification Windows (sécurité intégrée)</span><span class="sxs-lookup"><span data-stu-id="45fd7-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="45fd7-129">Utiliser compte de Windows hello processus en cours hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="45fd7-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="45fd7-130">Connexion à l’aide d’un fichier .odc</span><span class="sxs-lookup"><span data-stu-id="45fd7-130">Connect using an .odc file</span></span>
<span data-ttu-id="45fd7-131">Avec les versions antérieures d’Excel, les utilisateurs peuvent se connecter serveur des Services d’analyse Azure tooan à l’aide d’un fichier Office Data Connection (.odc).</span><span class="sxs-lookup"><span data-stu-id="45fd7-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="45fd7-132">toolearn, voir [créer un fichier Office Data Connection (.odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="45fd7-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="45fd7-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45fd7-133">Next steps</span></span>
<span data-ttu-id="45fd7-134">[Connexion avec Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="45fd7-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="45fd7-135">[Connexion avec Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="45fd7-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="45fd7-136">Gérer votre serveur</span><span class="sxs-lookup"><span data-stu-id="45fd7-136">Manage your server</span></span>](analysis-services-manage.md)   

