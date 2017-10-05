---
title: "Développer des opérateurs U-SQL définis par l’utilisateur | Microsoft Docs"
description: "Apprenez à développer des opérateurs définis par l’utilisateur pour les utiliser et les réutiliser dans des travaux Data Lake Analytics. "
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
ms.openlocfilehash: fdee02fb60b633c26704fc1774dfc3a7825b5e0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="fdbf8-103">Développer des opérateurs U-SQL définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="fdbf8-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="fdbf8-104">Apprenez à développer des opérateurs définis par l’utilisateur pour traiter les données d’un travail U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-104">Learn how to develop user-defined operators to process data in a U-SQL job.</span></span>

<span data-ttu-id="fdbf8-105">Pour obtenir des instructions concernant le développement des assemblys à usage général pour U-SQL, consultez [Développement d’assemblys U-SQL pour les travaux Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="fdbf8-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="fdbf8-106">Définir et utiliser un opérateur défini par l’utilisateur dans U-SQL</span><span class="sxs-lookup"><span data-stu-id="fdbf8-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="fdbf8-107">**Pour créer et soumettre un travail U-SQL**</span><span class="sxs-lookup"><span data-stu-id="fdbf8-107">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="fdbf8-108">Dans Visual Studio, sélectionnez **Fichier > Nouveau > Projet > Projet U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-108">From the Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="fdbf8-109">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-109">Click **OK**.</span></span> <span data-ttu-id="fdbf8-110">Visual Studio crée une solution avec un fichier Script.usql.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="fdbf8-111">À partir de **l’Explorateur de solutions**, développez Script.usql, puis double-cliquez sur **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="fdbf8-112">Collez le code suivant dans le fichier :</span><span class="sxs-lookup"><span data-stu-id="fdbf8-112">Paste the following code into the file:</span></span>

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
6. <span data-ttu-id="fdbf8-113">Ouvrez **Script.usql** et collez le script U-SQL suivant :</span><span class="sxs-lookup"><span data-stu-id="fdbf8-113">Open **Script.usql**, and paste the following U-SQL script:</span></span>

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
            TO "/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="fdbf8-114">Spécifiez le compte Data Lake Analytics, la base de données et le schéma.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-114">Specify the Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="fdbf8-115">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Générer le script**.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="fdbf8-116">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Soumettre le script**.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="fdbf8-117">Si vous ne vous êtes pas connecté à votre abonnement Azure, vous serez invité à entrer vos informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-117">If you haven't connected to your Azure subscription, you will be prompted to enter your Azure account credentials.</span></span>
11. <span data-ttu-id="fdbf8-118">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-118">Click **Submit**.</span></span> <span data-ttu-id="fdbf8-119">Les résultats de l’envoi et le lien vers le travail sont disponibles dans la fenêtre Résultats quand l’envoi est terminé.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-119">Submission results and job link are available in the Results window when the submission is completed.</span></span>
12. <span data-ttu-id="fdbf8-120">Cliquez sur le bouton **Actualiser** pour afficher le dernier état du travail et actualiser l’écran.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-120">Click the **Refresh** button to see the latest job status and refresh the screen.</span></span>

<span data-ttu-id="fdbf8-121">**Pour afficher la sortie**</span><span class="sxs-lookup"><span data-stu-id="fdbf8-121">**To see the output**</span></span>

1. <span data-ttu-id="fdbf8-122">Dans **l’Explorateur de serveurs**, développez successivement **Azure**, **Data Lake Analytics**, votre compte Data Lake Analytics, **Comptes de stockage**, puis cliquez avec le bouton droit sur le stockage par défaut et sur **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="fdbf8-123">Développez des exemples, des sorties, puis double-cliquez sur **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="fdbf8-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="fdbf8-124">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="fdbf8-124">See also</span></span>
* [<span data-ttu-id="fdbf8-125">Prise en main de Data Lake Analytics à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdbf8-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="fdbf8-126">Prise en main de Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="fdbf8-126">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="fdbf8-127">Utiliser les outils Data Lake pour Visual Studio pour le développement d’applications U-SQL</span><span class="sxs-lookup"><span data-stu-id="fdbf8-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
