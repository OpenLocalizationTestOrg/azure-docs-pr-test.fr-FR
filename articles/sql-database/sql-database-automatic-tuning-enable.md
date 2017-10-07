---
title: "aaaEnable automatique de paramétrage de base de données SQL Azure | Documents Microsoft"
description: "Vous pouvez facilement activer le réglage automatique sur Azure SQL Database."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a>Activer le réglage automatique

Base de données SQL Azure est un service de données managées automatiquement constamment surveille vos requêtes et identifie l’action hello que vous puissiez effectuer tooimprove les performances de votre charge de travail. Vous pouvez consulter les recommandations et les appliquer manuellement ou laisser Azure SQL Database appliquer automatiquement des actions correctives : il s’agit du **mode de réglage automatique**. Le paramétrage automatique peut être activé au niveau de base de données de hello ou de serveur de hello.

## <a name="enable-automatic-tuning-on-server"></a>Activer le réglage automatique sur le serveur

tooenable automatique de paramétrage sur le serveur de base de données SQL Azure, accédez à serveur toohello dans Azure portail, puis sélectionnez **le paramétrage automatique** dans le menu de hello. Sélectionnez hello des options de paramétrage automatique souhaitée tooenable **appliquer**:

![Serveur](./media/sql-database-automatic-tuning-enable/server.png)

Options de serveur de réglage automatiques sont tooall appliqué des bases de données sur le serveur de hello. Par défaut, toutes les bases de données héritent la configuration de hello depuis le serveur de leur parent, mais cela peut être substituée et être spécifiée individuellement pour chaque base de données.

## <a name="configure-automatic-tuning-on-database"></a>Configurer le réglage automatique sur la base de données

Bonjour Azure permet de portail tooindividually vous spécifiez la configuration de réglage automatique hello sur chaque base de données.

> [!NOTE]
> recommandation générale de Hello est toomanage hello paramétrage configuration automatique au niveau serveur hello dans ce même paramètres de configuration peuvent être appliquées automatiquement sur chaque base de données. Configurez le paramétrage automatique sur une base de données si la base de données hello est autre que d’autres membres de hello même serveur.
>

tooenable automatique de paramétrage sur une base de données, accédez à base de données toohello Bonjour portail Azure et puis sélectionnez **le paramétrage automatique**. Vous pouvez configurer une seule base de données tooinherit hello les paramètres de base de données hello en sélectionnant la case à cocher hello ou vous pouvez spécifier individuellement configuration hello pour une base de données.

![Base de données](./media/sql-database-automatic-tuning-enable/database.png)

Une fois que vous avez sélectionné la configuration appropriée, cliquez sur **Appliquer**.

## <a name="next-steps"></a>Étapes suivantes
* Hello de lecture [article Paramétrage automatique](sql-database-automatic-tuning.md) toolearn plus d’informations sur le paramétrage automatique et comment il peut vous aider à améliorer les performances.
* Consultez [Recommandations en matière de performances](sql-database-advisor.md) pour obtenir une vue d’ensemble des recommandations relatives aux performances Azure SQL Database.
* Consultez [analyse des performances des requêtes](sql-database-query-performance.md) toolearn sur l’affichage des performances hello de vos requêtes principales.
