---
title: "Élément d’interface utilisateur CredentialsCombo des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Network.PublicIpAddressCombo pour les applications gérées Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="bcd68-103">Élément d’interface utilisateur Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="bcd68-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="bcd68-104">Groupe de contrôles pour la sélection d’une nouvelle adresse IP publique ou d’une adresse IP publique existante.</span><span class="sxs-lookup"><span data-stu-id="bcd68-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="bcd68-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="bcd68-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="bcd68-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="bcd68-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="bcd68-108">Si l’utilisateur sélectionne « Aucune » pour l’adresse IP publique, la zone de texte d’étiquette de nom du domaine est masquée.</span><span class="sxs-lookup"><span data-stu-id="bcd68-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="bcd68-109">Si l’utilisateur sélectionne une adresse IP publique existante, la zone de texte d’étiquette de nom du domaine est masquée.</span><span class="sxs-lookup"><span data-stu-id="bcd68-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="bcd68-110">Sa valeur est l’étiquette de nom de domaine de l’adresse IP sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="bcd68-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="bcd68-111">Le suffixe du nom de domaine (par exemple, westus.cloudapp.azure.com) se met à jour automatiquement en fonction de l’emplacement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="bcd68-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="bcd68-112">Schéma</span><span class="sxs-lookup"><span data-stu-id="bcd68-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="bcd68-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="bcd68-113">Remarks</span></span>
- <span data-ttu-id="bcd68-114">Si `constraints.required.domainNameLabel` est défini sur **true**, l’utilisateur doit fournir une étiquette de nom de domaine lors de la création d’une nouvelle adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="bcd68-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="bcd68-115">Les adresses IP publiques existantes sans étiquette ne sont pas disponibles à la sélection.</span><span class="sxs-lookup"><span data-stu-id="bcd68-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="bcd68-116">Si `options.hideNone` est défini sur **true**, l’option de sélection **Aucune** pour l’adresse IP publique est masquée.</span><span class="sxs-lookup"><span data-stu-id="bcd68-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="bcd68-117">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="bcd68-117">The default value is **false**.</span></span>
- <span data-ttu-id="bcd68-118">Si `options.hideDomainNameLabel` est défini sur **true**, la zone de texte pour l’étiquette de nom de domaine est masquée.</span><span class="sxs-lookup"><span data-stu-id="bcd68-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="bcd68-119">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="bcd68-119">The default value is **false**.</span></span>
- <span data-ttu-id="bcd68-120">Si `options.hideExisting` est défini sur true, l’utilisateur n’est pas en mesure de choisir d’adresse IP publique existante.</span><span class="sxs-lookup"><span data-stu-id="bcd68-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="bcd68-121">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="bcd68-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="bcd68-122">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="bcd68-122">Sample output</span></span>
<span data-ttu-id="bcd68-123">Si l’utilisateur ne sélectionne aucune adresse IP publique, la sortie doit être la suivante :</span><span class="sxs-lookup"><span data-stu-id="bcd68-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="bcd68-124">Si l’utilisateur sélectionne une nouvelle adresse IP publique ou une adresse IP publique existante, la sortie doit être la suivante :</span><span class="sxs-lookup"><span data-stu-id="bcd68-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="bcd68-125">Lorsque `options.hideNone` est spécifié, `newOrExistingOrNone` renvoie toujours **aucune**.</span><span class="sxs-lookup"><span data-stu-id="bcd68-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="bcd68-126">Lorsque `options.hideDomainNameLabel` est spécifié, `domainNameLabel` n’est pas déclaré.</span><span class="sxs-lookup"><span data-stu-id="bcd68-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcd68-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcd68-127">Next steps</span></span>
* <span data-ttu-id="bcd68-128">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcd68-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="bcd68-129">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcd68-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="bcd68-130">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="bcd68-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
