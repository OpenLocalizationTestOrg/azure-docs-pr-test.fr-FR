---
title: "les opérateurs définis par l’utilisateur aaaDevelop U-SQL (opérateurs) | Documents Microsoft"
description: "Découvrez comment toodevelop opérateurs définis par l’utilisateur toobe utilisé et réutilisées dans les données de LAC Analytique travaux. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a>Développer des opérateurs U-SQL définis par l’utilisateur
Découvrez comment toodevelop définie par l’utilisateur données de tooprocess d’opérateurs dans un travail U-SQL.

Pour obtenir des instructions concernant le développement des assemblys à usage général pour U-SQL, consultez [Développement d’assemblys U-SQL pour les travaux Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a>Définir et utiliser un opérateur défini par l’utilisateur dans U-SQL
**toocreate et soumettre un travail U-SQL**

1. À partir de Visual Studio de hello sélectionnez **fichier > Nouveau > projet > projet U-SQL**.
2. Cliquez sur **OK**. Visual Studio crée une solution avec un fichier Script.usql.
3. À partir de **l’Explorateur de solutions**, développez Script.usql, puis double-cliquez sur **Script.usql.cs**.
4. Collez hello après le code dans le fichier de hello :

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. Ouvrez **Script.usql**, puis coller hello script U-SQL :

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. Spécifier le compte de données Lake Analytique hello, base de données et schéma.
8. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Générer le script**.
9. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Soumettre le script**.
10. Si vous n’avez pas encore connecté tooyour abonnement Azure, vous allez être invité à tooenter vos informations d’identification de compte Azure.
11. Cliquez sur **Envoyer**. Résultats de l’envoi et de lien de tâche sont disponibles dans la fenêtre des résultats hello lors de la soumission de hello est terminée.
12. Cliquez sur hello **Actualiser** bouton toosee dernière tâche état et l’actualisation hello écran hello.

**sortie de hello toosee**

1. À partir de **l’Explorateur de serveurs**, développez **Azure**, développez **Analytique lac de données**, développez votre compte Analytique lac de données, puis **lescomptesdestockage**, avec le bouton droit hello par défaut de stockage, puis cliquez sur **Explorer**.
2. Développez des exemples, des sorties, puis double-cliquez sur **Drivers.csv**.

## <a name="see-also"></a>Voir aussi
* [Prise en main de Data Lake Analytics à l’aide de PowerShell](data-lake-analytics-get-started-powershell.md)
* [Prise en main Analytique lac de données à l’aide de hello portail Azure](data-lake-analytics-get-started-portal.md)
* [Utiliser les outils Data Lake pour Visual Studio pour le développement d’applications U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
