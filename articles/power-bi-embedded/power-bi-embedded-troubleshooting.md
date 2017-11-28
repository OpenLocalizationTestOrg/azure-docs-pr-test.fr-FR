---
title: "résolution des problèmes de Power BI incorporée aaaMicrosoft"
description: "Résolution des problèmes de Microsoft Power BI Embedded Preview "
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
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="33192-103">Résolution des problèmes de Microsoft Power BI Embedded Preview </span><span class="sxs-lookup"><span data-stu-id="33192-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="33192-104">Cet article fournit des réponses sur la manière de tootroubleshoot **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="33192-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="33192-105">Définition des chaînes de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="33192-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="33192-106">tooset une chaîne de connexion SQL Server, vous devez toofollow un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="33192-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="33192-107">Voici un exemple de chaîne de connexion pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="33192-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="33192-108">toolearn savoir plus sur les chaînes de connexion SQL Server, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="33192-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="33192-109">Chaînes de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="33192-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="33192-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="33192-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="33192-111">Définition des informations d'identification</span><span class="sxs-lookup"><span data-stu-id="33192-111">Setting credentials</span></span>
<span data-ttu-id="33192-112">Dans les cas de hello où vous disposez des informations d’identification pour un développement ou un environnement intermédiaire, telles que le nom d’utilisateur et mot de passe, vous devrez peut-être les informations d’identification tooupdate qui correspondent à une solution de production.</span><span class="sxs-lookup"><span data-stu-id="33192-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="33192-113">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="33192-113">See Also</span></span>
* [<span data-ttu-id="33192-114">Prise en main de l’exemple</span><span class="sxs-lookup"><span data-stu-id="33192-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="33192-115">Présentation de Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="33192-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

