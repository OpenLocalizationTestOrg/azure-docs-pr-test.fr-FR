---
ms.assetid: 
title: "environnements de sécurité du coffre de clés aaaAzure | Documents Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="1e915-102">Mondes de sécurité Azure Key Vault et limites géographiques</span><span class="sxs-lookup"><span data-stu-id="1e915-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="1e915-103">Azure Key Vault est un service mutualisé qui utilise un pool de modules de sécurité matériel (HSM) dans chaque emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="1e915-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="1e915-104">Tous les modules de sécurité matériels à des emplacements Azure Bonjour même région géographique partagent hello même limite de services de chiffrement (monde de sécurité Thales).</span><span class="sxs-lookup"><span data-stu-id="1e915-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="1e915-105">Par exemple, est des États-Unis et l’ouest des États-Unis partager Bonjour même sécurité car elles appartiennent géolocalisation toohello des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="1e915-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="1e915-106">De même, tous les emplacements Azure dans le partage de Japon hello même monde de sécurité et de tous les emplacements Azure en Australie, Inde et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="1e915-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="1e915-107">Comportement de sauvegarde et de restauration</span><span class="sxs-lookup"><span data-stu-id="1e915-107">Backup and restore behavior</span></span>

<span data-ttu-id="1e915-108">Une sauvegarde d’une clé à partir d’un coffre de clés dans un emplacement Azure peut être restauré tooa le coffre de clés dans un autre emplacement Azure, tant que ces deux conditions sont remplies :</span><span class="sxs-lookup"><span data-stu-id="1e915-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="1e915-109">Les deux hello Azure emplacements appartiennent toohello même emplacement géographique</span><span class="sxs-lookup"><span data-stu-id="1e915-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="1e915-110">De coffres de clé hello appartenir toohello même abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="1e915-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="1e915-111">Par exemple, une sauvegarde effectuée par un abonnement donné d’une clé dans un coffre de clés dans l’ouest de l’Inde, peut être uniquement de coffre de clés tooanother restaurée Bonjour même abonnement et l’emplacement géographique ; Ouest de l’Inde, Inde centrale ou Inde du Sud.</span><span class="sxs-lookup"><span data-stu-id="1e915-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="1e915-112">Régions et produits</span><span class="sxs-lookup"><span data-stu-id="1e915-112">Regions and products</span></span>

- [<span data-ttu-id="1e915-113">Régions Azure</span><span class="sxs-lookup"><span data-stu-id="1e915-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="1e915-114">Produits Microsoft par région</span><span class="sxs-lookup"><span data-stu-id="1e915-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="1e915-115">Les régions sont mappés toosecurity mondes, affichés en tant qu’en-têtes principales dans les tables de hello :</span><span class="sxs-lookup"><span data-stu-id="1e915-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="1e915-116">Dans les produits hello par l’article de la région, par exemple, hello **Americas** onglet contient EAST US, centre des États-Unis, ouest des États-Unis tous les mappage toohello Americas région.</span><span class="sxs-lookup"><span data-stu-id="1e915-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="1e915-117">US DOD EAST et US DOD CENTRAL sont des exceptions, dans la mesure où ils possèdent leurs propres mondes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="1e915-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="1e915-118">De même, sur hello **Europe** sous l’onglet EUROPE du Nord et EUROPE de l’ouest mappent tous les deux toohello la région Europe.</span><span class="sxs-lookup"><span data-stu-id="1e915-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="1e915-119">Hello vaut également sur hello **Asie Pacifique** onglet.</span><span class="sxs-lookup"><span data-stu-id="1e915-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



