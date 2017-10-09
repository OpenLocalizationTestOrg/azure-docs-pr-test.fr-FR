---
title: "assemblys aaaDevelop U-SQL pour les travaux de l’Analytique de LAC de données Azure | Documents Microsoft"
description: "Découvrez comment toodevelop assemblys toobe utilisé et réutilisées dans les données de LAC Analytique travaux. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Développer des assemblys U-SQL pour des travaux Azure Data Lake Analytics
Découvrez comment tooturn code-behind dans les assemblys toobe utilisé et réutilisées dans les travaux Analytique lac de données. 

U-SQL rend facile tooadd votre propre code dans les langages .net, tels que c#, VB.Net ou F #. Vous pouvez même déployer votre propre toosupport runtime autres langages.

code personnalisé Hello plus simple façon toouse est toouse hello Data Lake Tools pour les fonctions de code-behind de Visual Studio. Pour plus d’informations, consultez le [didacticiel : Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Il existe quelques inconvénients à l’utilisation de code-behind :

- code source de Hello obtient téléchargé pour chaque demande de script.
- Le fichier code-behind ne peut pas être partagé avec d’autres tâches.

tooaddress ces inconvénients, vous pouvez activer le code-behind dans des assemblys et inscrire le catalogue de hello assemblys toohello Analytique lac de données.

## <a name="prerequisites"></a>Composants requis
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 Update 4 ou Visual Studio 2012 avec Visual C++ installé
* Le kit SDK Microsoft Azure pour .NET version 2.5 ou ultérieure.  Installer à l’aide du programme d’installation de plateforme hello Web ou le programme d’installation de Visual Studio
* Un compte Data Lake Analytics.  Consultez l’article [Prise en main d’Azure Data Lake Analytics à l’aide du Portail Azure](data-lake-analytics-get-started-portal.md).
* Passez en revue hello [prise en main Azure Data Lake Analytique U-SQL Studio](data-lake-analytics-u-sql-get-started.md) didacticiel.
* Se connecter tooAzure.
* Télécharger des données de sources de hello, consultez [prise en main Azure Data Lake Analytique U-SQL Studio](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>Développement d’assemblys pour U-SQL

**toocreate et soumettre un travail U-SQL**

1. À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.
2. Développez **installé**, **modèles**, **Azure Data Lake**, **U-SQL(ADLA)**, sélectionnez hello **bibliothèque de classes (pour U-SQL Application)** modèle, puis cliquez sur **OK**.
3. Écrivez votre code dans le fichier Class1.cs.  Hello Voici un exemple de code.

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. Cliquez sur hello **générer** menu, puis sur **générer la Solution** toocreate hello dll.

## <a name="register-assemblies"></a>Inscription d’assemblys

Consultez [Utilisation du catalogue Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-hello-assemblies"></a>Utiliser des assemblys hello

Consultez [utiliser hello Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>Voir aussi
* [Prise en main de Data Lake Analytics à l’aide de PowerShell](data-lake-analytics-get-started-powershell.md)
* [Prise en main Analytique lac de données à l’aide de hello portail Azure](data-lake-analytics-get-started-portal.md)
* [Utiliser les outils Data Lake pour Visual Studio pour le développement d’applications U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
* [Utilisation du catalogue Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md)
* [Utilisez hello Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
