---
ms.assetid: 
title: "Mondes de sécurité Azure Key Vault | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 921bbd109c9ea98d8b5c286a7512bed026412d26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="1df0f-102">Mondes de sécurité Azure Key Vault et limites géographiques</span><span class="sxs-lookup"><span data-stu-id="1df0f-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="1df0f-103">Azure Key Vault est un service mutualisé qui utilise un pool de modules de sécurité matériel (HSM) dans chaque emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="1df0f-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="1df0f-104">Tous les modules de sécurité matériel présents dans les emplacements Azure au sein d’une même région géographique partagent la même limite de chiffrement (monde de sécurité Thales).</span><span class="sxs-lookup"><span data-stu-id="1df0f-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="1df0f-105">Par exemple, les régions États-Unis de l’Est et États-Unis de l’Ouest partagent le même monde de sécurité car elles appartiennent à l’emplacement géographique États-Unis.</span><span class="sxs-lookup"><span data-stu-id="1df0f-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="1df0f-106">De même, tous les emplacements Azure au Japon partagent le même monde de sécurité, tout comme les emplacements Azure en Australie, en Inde, etc.</span><span class="sxs-lookup"><span data-stu-id="1df0f-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="1df0f-107">Comportement de sauvegarde et de restauration</span><span class="sxs-lookup"><span data-stu-id="1df0f-107">Backup and restore behavior</span></span>

<span data-ttu-id="1df0f-108">La sauvegarde d’une clé d’un coffre de clés dans un emplacement Azure peut être restaurée dans un coffre de clés situé dans un autre emplacement Azure, tant que les deux conditions suivantes sont remplies :</span><span class="sxs-lookup"><span data-stu-id="1df0f-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="1df0f-109">Les deux emplacements Azure appartiennent à la même région géographique</span><span class="sxs-lookup"><span data-stu-id="1df0f-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="1df0f-110">Les deux coffres de clés appartiennent au même abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="1df0f-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="1df0f-111">Par exemple, la sauvegarde d’une clé effectuée par un abonnement spécifique dans un coffre de clés en Inde de l’Ouest peut uniquement être restaurée dans un coffre de clés appartenant aux mêmes abonnement et emplacement géographique (Inde de l’Ouest, Centre de l’Inde ou Inde du Sud).</span><span class="sxs-lookup"><span data-stu-id="1df0f-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="1df0f-112">Régions et produits</span><span class="sxs-lookup"><span data-stu-id="1df0f-112">Regions and products</span></span>

- [<span data-ttu-id="1df0f-113">Régions Azure</span><span class="sxs-lookup"><span data-stu-id="1df0f-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="1df0f-114">Produits Microsoft par région</span><span class="sxs-lookup"><span data-stu-id="1df0f-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="1df0f-115">Les régions sont mappées aux mondes de sécurité, illustrés sous forme d’en-têtes principaux dans les tableaux :</span><span class="sxs-lookup"><span data-stu-id="1df0f-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="1df0f-116">Dans l’article « Produits par région », par exemple, l’onglet **Amérique** contient les éléments EAST US, CENTRAL US, WEST US, tous mappés à la région Amérique.</span><span class="sxs-lookup"><span data-stu-id="1df0f-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="1df0f-117">US DOD EAST et US DOD CENTRAL sont des exceptions, dans la mesure où ils possèdent leurs propres mondes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="1df0f-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="1df0f-118">De même, dans l’onglet **Europe**, NORTH EUROPE et WEST EUROPE sont tous deux mappés à la région Europe.</span><span class="sxs-lookup"><span data-stu-id="1df0f-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="1df0f-119">Cela vaut également pour l’onglet **Asie Pacifique**.</span><span class="sxs-lookup"><span data-stu-id="1df0f-119">The same is also true on the **Asia Pacific** tab.</span></span>



