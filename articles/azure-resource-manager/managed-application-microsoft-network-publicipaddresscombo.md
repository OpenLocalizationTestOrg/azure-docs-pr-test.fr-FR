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
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Élément d’interface utilisateur Microsoft.Network.PublicIpAddressCombo
Groupe de contrôles pour la sélection d’une nouvelle adresse IP publique ou d’une adresse IP publique existante. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Si l’utilisateur de hello sélectionne « None » pour l’adresse IP publique, une zone de texte d’étiquette du nom de domaine hello est masquée.
- Si l’utilisateur de hello sélectionne une adresse IP publique existante, la zone de texte d’étiquette du nom de domaine hello est désactivée. Sa valeur est l’étiquette de nom de domaine hello d’adresse IP de hello sélectionné.
- Hello domaine nom suffixe (par exemple, westus.cloudapp.azure.com) met à jour automatiquement en fonction de l’emplacement de hello sélectionné.

## <a name="schema"></a>Schéma
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

## <a name="remarks"></a>Remarques
- Si `constraints.required.domainNameLabel` est défini trop**true**, utilisateur de hello doit fournir une étiquette de nom de domaine lors de la création d’une nouvelle adresse IP publique. Les adresses IP publiques existantes sans étiquette ne sont pas disponibles à la sélection.
- Si `options.hideNone` est défini trop**true**, puis hello option tooselect **aucun** pour l’adresse IP publique hello adresse est masquée. la valeur par défaut Hello est **false**.
- Si `options.hideDomainNameLabel` est défini trop**true**, puis de la zone de texte hello pour l’étiquette de nom de domaine est masqué. la valeur par défaut Hello est **false**.
- Si `options.hideExisting` a la valeur true, l’utilisateur hello n’est pas en mesure de toochoose une adresse IP publique existante. la valeur par défaut Hello est **false**.

## <a name="sample-output"></a>Exemple de sortie
Si l’utilisateur de hello ne sélectionne aucune adresse IP publique, hello sortie suivante est attendue :
```json
{
  "newOrExistingOrNone": "none"
}
```

Si l’utilisateur de hello sélectionne une adresse IP nouvelle ou existante, hello sortie suivante est attendue :
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- Lorsque `options.hideNone` est spécifié, `newOrExistingOrNone` renvoie toujours **aucune**.
- Lorsque `options.hideDomainNameLabel` est spécifié, `domainNameLabel` n’est pas déclaré.

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
