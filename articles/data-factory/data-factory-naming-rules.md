---
title: "aaaRules de nommer les entités d’Azure Data Factory | Documents Microsoft"
description: "Décrit les règles d'affectation de noms pour les entités Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="84f84-103">Azure Data Factory - Règles d’affectation des noms</span><span class="sxs-lookup"><span data-stu-id="84f84-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="84f84-104">Hello tableau suivant fournit des règles d’affectation de noms pour les artefacts de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="84f84-104">hello following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="84f84-105">Nom</span><span class="sxs-lookup"><span data-stu-id="84f84-105">Name</span></span> | <span data-ttu-id="84f84-106">Unicité du nom</span><span class="sxs-lookup"><span data-stu-id="84f84-106">Name Uniqueness</span></span> | <span data-ttu-id="84f84-107">Contrôles de validation</span><span class="sxs-lookup"><span data-stu-id="84f84-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="84f84-108">Data Factory</span><span class="sxs-lookup"><span data-stu-id="84f84-108">Data Factory</span></span> |<span data-ttu-id="84f84-109">Unique sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="84f84-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="84f84-110">Les noms respectent la casse, c'est-à-dire `MyDF` et `mydf` font référence toohello même fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="84f84-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer toohello same data factory.</span></span> |<ul><li><span data-ttu-id="84f84-111">Chaque fabrique de données est liée tooexactly d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="84f84-111">Each data factory is tied tooexactly one Azure subscription.</span></span></li><li><span data-ttu-id="84f84-112">Les noms d’objet doivent commencer par une lettre ou un chiffre et peuvent contenir uniquement des lettres, des chiffres et hello tiret (-).</span><span class="sxs-lookup"><span data-stu-id="84f84-112">Object names must start with a letter or a number, and can contain only letters, numbers, and hello dash (-) character.</span></span></li><li><span data-ttu-id="84f84-113">Chaque tiret (-) doit être immédiatement précédé et suivi par une lettre ou un chiffre.</span><span class="sxs-lookup"><span data-stu-id="84f84-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="84f84-114">Les tirets consécutifs ne sont pas autorisés dans les noms de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="84f84-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="84f84-115">Le nom doit contenir entre 3 et 63 caractères.</span><span class="sxs-lookup"><span data-stu-id="84f84-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="84f84-116">Services/tableaux/pipelines liés</span><span class="sxs-lookup"><span data-stu-id="84f84-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="84f84-117">Unique dans une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="84f84-117">Unique with in a data factory.</span></span> <span data-ttu-id="84f84-118">Les noms sont sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="84f84-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="84f84-119">Un tableau peut contenir un maximum de 260 caractères.</span><span class="sxs-lookup"><span data-stu-id="84f84-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="84f84-120">Les noms d’objet doivent commencer par une lettre, un chiffre ou un trait de soulignement (_).</span><span class="sxs-lookup"><span data-stu-id="84f84-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="84f84-121">Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</span><span class="sxs-lookup"><span data-stu-id="84f84-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="84f84-122">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="84f84-122">Resource Group</span></span> |<span data-ttu-id="84f84-123">Unique sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="84f84-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="84f84-124">Les noms sont sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="84f84-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="84f84-125">Nombre maximal de caractères : 1 000.</span><span class="sxs-lookup"><span data-stu-id="84f84-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="84f84-126">Nom peut contenir des lettres, des chiffres et hello les caractères suivants : «- », « _ «, », « et ». »</span><span class="sxs-lookup"><span data-stu-id="84f84-126">Name can contain letters, digits, and hello following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

