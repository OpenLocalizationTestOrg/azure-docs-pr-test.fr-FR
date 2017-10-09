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
# <a name="connect-with-excel"></a>Connexion avec Excel

Une fois que vous avez créé un serveur dans Azure et déployé un tooit de modèle tabulaire, vous êtes prêt tooconnect et commencez à Explorer les données.


## <a name="connect-in-excel"></a>Se connecter dans Excel

La connexion serveur tooa dans Excel est pris en charge à l’aide d’obtenir des données dans Excel 2016. Connexion à l’aide de hello Assistant Importation de Table dans Power Pivot n’est pas pris en charge. 

**tooconnect dans Excel 2016**

1. Dans Excel 2016, sur hello **données** du ruban, cliquez sur **obtenir des données externes** > **à partir d’autres Sources** > **à partir d’Analysis Services** .

2. Dans hello Assistant connexion de données dans **nom du serveur**, entrez hello nom du serveur, y compris le protocole et l’URI. Ensuite, dans **informations d’identification d’ouverture de session**, sélectionnez **hello utilisation après le nom d’utilisateur et mot de passe**, puis tapez les nom d’utilisateur d’organisation hello, par exemple nancy@adventureworks.comet le mot de passe.

    ![Se connecter à partir de l’ouverture de session Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. Dans **sélectionner une base de données et de Table**, sélectionnez la base de données hello et perspective ou un modèle, puis cliquez sur **Terminer**.
   
    ![Se connecter à partir du modèle de sélection Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>Voir aussi
[Bibliothèques clientes](analysis-services-data-providers.md)   
[Gérer votre serveur](analysis-services-manage.md)     


