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
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="b1de4-103">Développer des opérateurs U-SQL définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b1de4-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="b1de4-104">Découvrez comment toodevelop définie par l’utilisateur données de tooprocess d’opérateurs dans un travail U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b1de4-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="b1de4-105">Pour obtenir des instructions concernant le développement des assemblys à usage général pour U-SQL, consultez [Développement d’assemblys U-SQL pour les travaux Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="b1de4-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="b1de4-106">Définir et utiliser un opérateur défini par l’utilisateur dans U-SQL</span><span class="sxs-lookup"><span data-stu-id="b1de4-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="b1de4-107">**toocreate et soumettre un travail U-SQL**</span><span class="sxs-lookup"><span data-stu-id="b1de4-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="b1de4-108">À partir de Visual Studio de hello sélectionnez **fichier > Nouveau > projet > projet U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="b1de4-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="b1de4-109">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1de4-109">Click **OK**.</span></span> <span data-ttu-id="b1de4-110">Visual Studio crée une solution avec un fichier Script.usql.</span><span class="sxs-lookup"><span data-stu-id="b1de4-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="b1de4-111">À partir de **l’Explorateur de solutions**, développez Script.usql, puis double-cliquez sur **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="b1de4-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="b1de4-112">Collez hello après le code dans le fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="b1de4-112">Paste hello following code into hello file:</span></span>

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
6. <span data-ttu-id="b1de4-113">Ouvrez **Script.usql**, puis coller hello script U-SQL :</span><span class="sxs-lookup"><span data-stu-id="b1de4-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

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
7. <span data-ttu-id="b1de4-114">Spécifier le compte de données Lake Analytique hello, base de données et schéma.</span><span class="sxs-lookup"><span data-stu-id="b1de4-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="b1de4-115">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Générer le script**.</span><span class="sxs-lookup"><span data-stu-id="b1de4-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="b1de4-116">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Soumettre le script**.</span><span class="sxs-lookup"><span data-stu-id="b1de4-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="b1de4-117">Si vous n’avez pas encore connecté tooyour abonnement Azure, vous allez être invité à tooenter vos informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b1de4-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="b1de4-118">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="b1de4-118">Click **Submit**.</span></span> <span data-ttu-id="b1de4-119">Résultats de l’envoi et de lien de tâche sont disponibles dans la fenêtre des résultats hello lors de la soumission de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="b1de4-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="b1de4-120">Cliquez sur hello **Actualiser** bouton toosee dernière tâche état et l’actualisation hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="b1de4-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="b1de4-121">**sortie de hello toosee**</span><span class="sxs-lookup"><span data-stu-id="b1de4-121">**toosee hello output**</span></span>

1. <span data-ttu-id="b1de4-122">À partir de **l’Explorateur de serveurs**, développez **Azure**, développez **Analytique lac de données**, développez votre compte Analytique lac de données, puis **lescomptesdestockage**, avec le bouton droit hello par défaut de stockage, puis cliquez sur **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b1de4-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="b1de4-123">Développez des exemples, des sorties, puis double-cliquez sur **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="b1de4-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="b1de4-124">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b1de4-124">See also</span></span>
* [<span data-ttu-id="b1de4-125">Prise en main de Data Lake Analytics à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1de4-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="b1de4-126">Prise en main Analytique lac de données à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b1de4-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="b1de4-127">Utiliser les outils Data Lake pour Visual Studio pour le développement d’applications U-SQL</span><span class="sxs-lookup"><span data-stu-id="b1de4-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
