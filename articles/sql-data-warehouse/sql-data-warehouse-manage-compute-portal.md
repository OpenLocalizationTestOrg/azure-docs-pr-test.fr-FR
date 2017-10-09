---
title: "aaaManage de calcul power dans l’entrepôt de données SQL Azure (portail Azure) | Documents Microsoft"
description: "Tâches du portail Azure toomanage une puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou bien, suspendre et reprendre des coûts toosave des ressources de calcul."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Gestion de la puissance de calcul dans Azure SQL Data Warehouse (portail Azure)
> [!div class="op_single_selector"]
> * [Vue d'ensemble](sql-data-warehouse-manage-compute-overview.md)
> * [Portail](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>Mise à l’échelle de la puissance de calcul
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange des ressources de calcul :

1. Ouvrez hello [portail Azure][Azure portal], ouvrez votre base de données, puis cliquez sur **échelle**.

    ![Cliquez sur Mettre à l’échelle.][1]
2. Dans le panneau de mise à l’échelle de hello, déplacez le curseur de hello gauche ou vers la droite toochange valeur dwu hello.

    ![Déplacez le curseur][2]
3. Cliquez sur **Save**. Un message de confirmation s’affiche. Cliquez sur **Oui** tooconfirm ou **aucun** toocancel.

    ![Cliquez sur Enregistrer.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Suspension du calcul
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause une base de données :

1. Ouvrez hello [portail Azure] [ Azure portal] et ouvrez votre base de données. Notez que hello état est **Online**.

    ![État En ligne][6]
2. Cliquez sur les ressources de calcul et de mémoire toosuspend, **Pause**, puis un message de confirmation s’affiche. Cliquez sur **Oui** tooconfirm ou **aucun** toocancel.

    ![Confirmer la pause][7]
3. Pendant le démarrage de l’entrepôt de données SQL de la base de données hello, état de hello est **interruption**.
4. Lorsque le statut de hello est **suspendu**, opération de suspension hello est effectuée et que vous êtes en cours n’est plus facturé pour Dwu.

    ![État Pause][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Reprise du calcul
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume une base de données :

1. Ouvrez hello [portail Azure] [ Azure portal] et ouvrez votre base de données. Notez que hello état est **suspendu**.

    ![Suspendre la base de données][4]
2. Cliquez sur base de données de hello tooresume **Démarrer**, puis un message de confirmation s’affiche. Cliquez sur **Oui** tooconfirm ou **aucun** toocancel.

    ![Confirmer la reprise][5]
3. Pendant le démarrage de l’entrepôt de données SQL de la base de données hello, statut de hello est « Reprise ».
4. Lorsque le statut de hello est **online**, base de données hello est prêt.

    ![État En ligne][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez la [vue d’ensemble de la gestion][Management overview].

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
