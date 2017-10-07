---
title: "élément de l’interface utilisateur de PublicIpAddressCombo pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Network.PublicIpAddressCombo pour des Applications managées Azure"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="f9c88-103">Élément d’interface utilisateur Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="f9c88-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="f9c88-104">Groupe de contrôles pour la sélection d’une nouvelle adresse IP publique ou d’une adresse IP publique existante.</span><span class="sxs-lookup"><span data-stu-id="f9c88-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="f9c88-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f9c88-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f9c88-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="f9c88-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="f9c88-108">Si l’utilisateur de hello sélectionne « None » pour l’adresse IP publique, une zone de texte d’étiquette du nom de domaine hello est masquée.</span><span class="sxs-lookup"><span data-stu-id="f9c88-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="f9c88-109">Si l’utilisateur de hello sélectionne une adresse IP publique existante, la zone de texte d’étiquette du nom de domaine hello est désactivée.</span><span class="sxs-lookup"><span data-stu-id="f9c88-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="f9c88-110">Sa valeur est l’étiquette de nom de domaine hello d’adresse IP de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="f9c88-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="f9c88-111">Hello domaine nom suffixe (par exemple, westus.cloudapp.azure.com) met à jour automatiquement en fonction de l’emplacement de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="f9c88-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="f9c88-112">Schéma</span><span class="sxs-lookup"><span data-stu-id="f9c88-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="f9c88-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="f9c88-113">Remarks</span></span>
- <span data-ttu-id="f9c88-114">Si `constraints.required.domainNameLabel` est défini trop**true**, utilisateur de hello doit fournir une étiquette de nom de domaine lors de la création d’une nouvelle adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="f9c88-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="f9c88-115">Les adresses IP publiques existantes sans étiquette ne sont pas disponibles à la sélection.</span><span class="sxs-lookup"><span data-stu-id="f9c88-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="f9c88-116">Si `options.hideNone` est défini trop**true**, puis hello option tooselect **aucun** pour l’adresse IP publique hello adresse est masquée.</span><span class="sxs-lookup"><span data-stu-id="f9c88-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="f9c88-117">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="f9c88-117">hello default value is **false**.</span></span>
- <span data-ttu-id="f9c88-118">Si `options.hideDomainNameLabel` est défini trop**true**, puis de la zone de texte hello pour l’étiquette de nom de domaine est masqué.</span><span class="sxs-lookup"><span data-stu-id="f9c88-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="f9c88-119">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="f9c88-119">hello default value is **false**.</span></span>
- <span data-ttu-id="f9c88-120">Si `options.hideExisting` a la valeur true, l’utilisateur hello n’est pas en mesure de toochoose une adresse IP publique existante.</span><span class="sxs-lookup"><span data-stu-id="f9c88-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="f9c88-121">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="f9c88-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f9c88-122">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="f9c88-122">Sample output</span></span>
<span data-ttu-id="f9c88-123">Si l’utilisateur de hello ne sélectionne aucune adresse IP publique, hello sortie suivante est attendue :</span><span class="sxs-lookup"><span data-stu-id="f9c88-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="f9c88-124">Si l’utilisateur de hello sélectionne une adresse IP nouvelle ou existante, hello sortie suivante est attendue :</span><span class="sxs-lookup"><span data-stu-id="f9c88-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="f9c88-125">Lorsque `options.hideNone` est spécifié, `newOrExistingOrNone` renvoie toujours **aucune**.</span><span class="sxs-lookup"><span data-stu-id="f9c88-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="f9c88-126">Lorsque `options.hideDomainNameLabel` est spécifié, `domainNameLabel` n’est pas déclaré.</span><span class="sxs-lookup"><span data-stu-id="f9c88-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9c88-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9c88-127">Next steps</span></span>
* <span data-ttu-id="f9c88-128">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9c88-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f9c88-129">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9c88-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f9c88-130">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f9c88-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
