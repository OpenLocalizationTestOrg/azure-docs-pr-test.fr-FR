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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Résolution des problèmes de Microsoft Power BI Embedded Preview 
Cet article fournit des réponses sur la manière de tootroubleshoot **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Définition des chaînes de connexion SQL Server
tooset une chaîne de connexion SQL Server, vous devez toofollow un format spécifique. Voici un exemple de chaîne de connexion pour SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

toolearn savoir plus sur les chaînes de connexion SQL Server, consultez hello suivant des articles :

* [Chaînes de connexion SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Définition des informations d'identification
Dans les cas de hello où vous disposez des informations d’identification pour un développement ou un environnement intermédiaire, telles que le nom d’utilisateur et mot de passe, vous devrez peut-être les informations d’identification tooupdate qui correspondent à une solution de production.

## <a name="see-also"></a>Voir aussi
* [Prise en main de l’exemple](power-bi-embedded-get-started-sample.md)
* [Présentation de Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

