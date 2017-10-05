---
title: "Résolution des problèmes de Microsoft Power BI Embedded Preview"
description: "Résolution des problèmes de Microsoft Power BI Embedded Preview"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="a177f-103">Résolution des problèmes de Microsoft Power BI Embedded Preview </span><span class="sxs-lookup"><span data-stu-id="a177f-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="a177f-104">Cet article apporte des réponses concernant la résolution des problèmes de **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="a177f-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="a177f-105">Définition des chaînes de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="a177f-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="a177f-106">Pour définir une chaîne de connexion SQL Server, vous devez suivre un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="a177f-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="a177f-107">Voici un exemple de chaîne de connexion pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a177f-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="a177f-108">Pour en savoir plus sur les chaînes de connexion SQL Server, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="a177f-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="a177f-109">Chaînes de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="a177f-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="a177f-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="a177f-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="a177f-111">Définition des informations d'identification</span><span class="sxs-lookup"><span data-stu-id="a177f-111">Setting credentials</span></span>
<span data-ttu-id="a177f-112">Dans le cas où vous possédez des informations d'identification pour un environnement intermédiaire ou de développement, en particulier un nom d'utilisateur et un mot de passe, vous devrez peut-être mettre à jour les informations d'identification qui correspondent à une solution en production.</span><span class="sxs-lookup"><span data-stu-id="a177f-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="a177f-113">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a177f-113">See Also</span></span>
* [<span data-ttu-id="a177f-114">Prise en main de l’exemple</span><span class="sxs-lookup"><span data-stu-id="a177f-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="a177f-115">Présentation de Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a177f-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

