---
title: aaaGet en main de Microsoft Power BI Embedded
description: "Power BI incorporée, ajoutez des rapports interactifs Power BI dans votre application business intelligence"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Prise en main de Microsoft Power BI Embedded

**Power BI Embedded** est un service Azure qui tooadd de développeurs active application interactif Power BI des rapports dans leurs propres applications. **Power BI Embedded** fonctionne avec les applications existantes sans avoir besoin de nouvelle conception ou la modification de hello manière dont les utilisateurs se connecter.

Ressources pour **Microsoft Power BI Embedded** approvisionnés via hello [Azure ARM API](https://msdn.microsoft.com/library/mt712306.aspx). Dans ce cas, la ressource hello vous approvisionner est un **collecte d’espace de travail Power BI**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Création d’une collection d’espaces de travail

A **Collection de l’espace de travail** est une ressource de Azure de niveau supérieur hello et un conteneur pour le contenu de hello qui est incorporé dans votre application. Pour créer une **collection d’espaces de travail** , deux possibilités s’offrent à vous :

* Manuellement à l’aide de hello portail Azure
* Par programmation à l’aide de hello API Manager(ARM) de ressources Azure

Examinons hello étapes toobuild un **Collection de l’espace de travail** à l’aide de hello portail Azure.

1. Ouvrez le **portail Azure**à l’adresse [http://portal.azure.com](http://portal.azure.com)et connectez-vous-y.
2. Cliquez sur **+ nouveau** sur le panneau supérieur de hello.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. Sous **Données + analyse**, cliquez sur **Power BI Embedded**.
4. Sur hello **espace de travail de Collection panneau**, entrez les informations de hello requis. Pour connaître la **tarification**, consultez la page [Tarification de Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Cliquez sur **Créer**.

Hello **Collection de l’espace de travail** prendra quelques instants tooprovision. Issue, vous serez dirigé toohello **Panneau de collecte d’espace de travail**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Hello **création panneau** contient les informations de hello nécessaires toocall hello API qui créent des espaces de travail et de déployer du contenu toothem.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Affichage des touches d’accès rapide aux API de Power BI

Un des principaux éléments d’informations nécessaires toocall hello API REST de Power BI de hello sont hello **clés d’accès**. Ceux-ci sont utilisés toogenerate hello **jetons d’application** qui sont utilisé tooauthenticate vos demandes API. tooview votre **clés d’accès**, cliquez sur **clés d’accès** sur hello **panneau paramètres**. Pour en savoir plus sur les **jetons d’application**, voir [Authentification et autorisation avec Power BI Embedded](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

Vous allez constater que vous disposez de deux touches.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Copiez-les et stockez-les de manière sécurisée dans votre application. Il est très important de traiter ces clés comme vous le feriez pour un mot de passe, car ils vous fournirons accès tooall hello contenu dans votre **Collection de l’espace de travail**.

Même si deux touches sont répertoriées, une seule est nécessaire à un moment donné. deuxième clé de Hello est fournie afin de régénérer régulièrement les clés sans interrompre le service d’accès toohello.

Maintenant que vous disposez d’une instance de Power BI pour votre application, ainsi que des **touches d’accès rapide**, vous pouvez importer un rapport dans votre propre application. Avant, vous allez apprendre comment tooimport un rapport, la section suivante de hello décrit la création tooembed de jeux de données et rapports Power BI dans une application.

## <a name="working-with-workspaces"></a>Utilisation des espaces de travail

Après avoir créé votre collection de l’espace de travail, vous devez toocreate un espace de travail qui héberger vos rapports et les jeux de données. toocreate un espace de travail, vous devez toouse hello [Post espace de travail REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>Créer des tooembed de jeux de données et rapports Power BI dans une application à l’aide de Power BI Desktop

Maintenant que vous avez créé une instance de Power BI pour votre application et avoir **clés d’accès**, vous devez toocreate hello Power BI datasets et les rapports que vous souhaitez tooembed. Vous pouvez créer des rapports et des jeux de données à l’aide de **Power BI Desktop**. Vous pouvez télécharger [Power BI Desktop gratuitement](https://go.microsoft.com/fwlink/?LinkId=521662). Ou, tooquickly prise en main, vous pouvez télécharger hello [PBIX d’exemple Retail Analysis](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> plus sur la façon de toolearn toouse **Power BI Desktop**, consultez [prise en main de Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

Avec **Power BI Desktop**, vous vous connectez la source de données tooyour en important une copie de données hello dans **Power BI Desktop** ou se connectant directement toohello données source à l’aide **DirectQuery**.

Voici hello les différences entre l’utilisation de **importation** et **DirectQuery**.

| Importer | DirectQuery |
| --- | --- |
| Les tables, colonnes *et données* sont importées ou copiées dans **Power BI Desktop**. Lorsque vous travaillez avec des visualisations, **Power BI Desktop** interroge une copie des données de hello. toosee des modifications des données sous-jacentes toohello s’est produite, vous devez actualiser ou importez, à nouveau un dataset complet, en cours. |Seules les *tables et colonnes* sont importées ou copiées dans **Power BI Desktop**. Lorsque vous travaillez avec des visualisations, **Power BI Desktop** requêtes hello source de données sous-jacente, ce qui signifie que vous visualisez toujours des données en cours. |

Pour plus d’informations sur la source de données tooa connexion, consultez [source de données de se connecter tooa](power-bi-embedded-connect-datasource.md).

Lorsque vous enregistrez votre travail dans **Power BI Desktop**, un fichier PBIX est créé. Ce fichier contient votre rapport. En outre, si vous importez hello données PBIX contient hello dans le jeu de données complet, ou si vous utilisez **DirectQuery**, hello PBIX contient uniquement le schéma d’un dataset. Vous déployez par programme hello PBIX dans votre espace de travail à l’aide de hello [API de Power BI importation](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** dispose d’autres API toochange hello serveur et base de données que votre jeu de données pointe tooand ensemble une information d’identification du compte de service qui hello dataset utilisera tooconnect tooyour base de données. Consultez les pages [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) et [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Création de rapports et de jeux de données Power BI avec des API

### <a name="datsets"></a>Jeux de données

Vous pouvez créer des jeux de données dans Power BI Embedded à l’aide des API REST de hello. Vous pouvez ensuite transmettre les données dans votre jeu de données. Cela vous permet de toowork avec des données sans avoir besoin de hello de Power BI Desktop. Pour plus d’informations, consultez [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Opération Post Datasets).

### <a name="reports"></a>Rapports

Vous pouvez créer un rapport à partir d’un jeu de données directement dans votre application à l’aide de hello API JavaScript. Pour plus d’informations, consultez [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Créer un rapport à partir d’un jeu de données dans Power BI Embedded).

## <a name="see-also"></a>Voir aussi

[Prise en main de l’exemple](power-bi-embedded-get-started-sample.md)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Intégrer un rapport)  
[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Créer un rapport à partir d’un jeu de données dans Power BI Embedded)
[Save reports in Power BI Embedded](power-bi-embedded-save-reports.md) (Enregistrer des rapports dans Power BI Embedded)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)

