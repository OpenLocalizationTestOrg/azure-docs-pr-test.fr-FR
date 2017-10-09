---
title: "bibliothèques aaaClient requis pour la connexion tooAzure Analysis Services | Documents Microsoft"
description: "Décrit les bibliothèques clientes requises pour le client tooconnect outils et applications Azure Analysis Services"
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
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>Bibliothèques clientes pour connecter tooAzure Analysis Services

Les bibliothèques clientes sont nécessaires pour les applications clientes et les serveurs de Services outils tooconnect tooAnalysis. 

Analysis Services utilise trois bibliothèques clientes. ADOMD.NET et Analysis Services Management Objects (AMO) sont des bibliothèques clientes managées. fournisseur OLE DB pour Analysis Services de Hello (DLL MSOLAP) est une bibliothèque cliente native. En règle générale, les trois sont installés à hello même temps. Azure Analysis Services nécessite les versions les plus récentes hello. 

Les applications clientes Microsoft telles que Power BI Desktop et Excel installent les trois bibliothèques clientes. Toutefois, selon la version de hello ou la fréquence des mises à jour, les bibliothèques clientes peut-être pas hello dernières versions requises par Azure Analysis Services. Hello va de même toocustom applications ou autres interfaces telles que AsCmd, TOM, ADOMD.NET. Ces applications nécessitent l’installation manuelle des bibliothèques de hello. les bibliothèques clientes Hello pour l’installation manuelle sont inclus dans les packs de fonctionnalités de SQL Server en tant que packages distribuables. Toutefois, ces bibliothèques clientes sont la version de SQL Server liée toohello et ne peuvent pas être hello plus récentes.  

Les bibliothèques clientes pour les connexions client sont différentes des données fournisseurs tooconnect requis à partir d’une source de données Azure Analysis Services server tooa. toolearn en savoir plus sur les connexions de source de données, consultez [des connexions de source de données](analysis-services-datasource.md).

## <a name="download-hello-latest-client-libraries"></a>Télécharger les bibliothèques clientes plus récentes hello  
Utilisez hello suivant des bibliothèques clientes si vous êtes dans un environnement de production et que vous requièrent des versions entièrement publiées et pris en charge.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Étapes suivantes
[Connexion avec Excel](analysis-services-connect-excel.md)    
[Connexion avec Power BI](analysis-services-connect-pbi.md)
