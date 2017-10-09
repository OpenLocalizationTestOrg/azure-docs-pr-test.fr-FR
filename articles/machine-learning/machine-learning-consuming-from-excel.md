---
title: "aaaConsume un Service de Web Machine Learning à partir d’Excel | Documents Microsoft"
description: "Utilisation d’un service web Microsoft Azure Machine Learning à partir de Microsoft Excel."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Utilisation d’un service web Microsoft Azure Machine Learning à partir de Microsoft Excel.
 Azure Machine Learning Studio rend toocall facilement les services web directement à partir d’Excel sans hello besoin toowrite n’importe quel code.

Si vous utilisez Excel 2013 (ou version ultérieure) ou Excel Online, nous vous recommandons d’utiliser hello Excel [complément Excel](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Étapes
Publiez un service web. [Cette page](machine-learning-walkthrough-5-publish-web-service.md) explique comment toodo il. Fonctionnalité de classeur Excel hello est actuellement uniquement pris en charge pour les services de demande/réponse qui ont une seule sortie (autrement dit, une étiquette de score unique). 

Une fois que vous avez un service web, cliquez sur hello **SERVICES WEB** section sur la gauche hello de studio de hello et sélectionnez hello web service tooconsume à partir d’Excel.

**Service web classique**

1. Sur hello **tableau de bord** onglet service web de hello est une ligne pour hello **demande/réponse** service. Si ce service dispose d’une sortie unique, vous devez voir hello **télécharger un classeur Excel** lien de la ligne.
   
    ![][1]
2. Cliquez sur **Télécharger un classeur Excel**.

**Nouveau service web**

1. Dans le portail du Service Web de Azure Machine Learning hello, sélectionnez **consommer**.
2. Hello consommer dans la page hello **options de la consommation de service Web** , cliquez sur icône Excel de hello.

**À l’aide du classeur de hello**

1. Classeur de hello ouvert.
2. Un avertissement de sécurité s’affiche ; Cliquez sur hello **activer la modification** bouton.
   
    ![][2]
3. Un avertissement de sécurité apparaît. Cliquez sur hello **activer le contenu** bouton toorun macros de votre feuille de calcul.
   
    ![][3]
4. Une fois les macros activées, une table est générée. Les colonnes en bleu sont requises en tant qu’entrée dans hello service web d’enregistrements de ressources, ou **paramètres**. Notez la sortie hello Hello service RR **valeurs prédites** en vert. Lorsque toutes les colonnes d’une ligne donnée sont remplis, hello classeur automatiquement appelle hello API de calcul de score et affiche hello résultats évalué.
   
    ![][4]
5. tooscore plus d’une ligne, remplissage hello deuxième ligne avec des données et hello prévisible de valeurs sont produites. Vous pouvez même coller plusieurs lignes à la fois.

Vous pouvez utiliser une des fonctionnalités d’Excel hello (graphiques, mappage de l’alimentation, conditionnelle mise en forme, etc.) avec hello prédit les valeurs toohelp visualiser les données de hello.    

## <a name="sharing-your-workbook"></a>Partage de votre classeur
Pour hello macros toowork, votre clé API doit être la partie de la feuille de calcul hello. Cela signifie que vous devez partager le classeur de hello uniquement avec les entités/personnes de que confiance.

## <a name="automatic-updates"></a>Mises à jour automatiques
Un appel RRS est initié dans les deux cas suivants :

1. Hello la première fois une ligne a contenu dans toutes ses **paramètres**
2. Chaque fois qu’un des hello **paramètres** modifications d’une ligne qui a toutes ses **paramètres** entré.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
