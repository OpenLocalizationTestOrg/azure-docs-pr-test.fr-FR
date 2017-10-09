---
title: "aaaAzure Application managée créer des fonctions de définition de l’interface utilisateur | Documents Microsoft"
description: "Décrit les hello fonctions toouse lors de la construction des définitions d’interface utilisateur pour les Applications managées Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>Éléments de CreateUiDefinition
Cet article décrit le schéma de hello et les propriétés de tous les éléments pris en charge d’une CreateUiDefinition. Vous utilisez ces éléments lors de la [création d’une application gérée Azure](managed-application-publishing.md). schéma Hello pour la plupart des éléments est la suivante :

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Propriété | Requis | Description |
| -------- | -------- | ----------- |
| name | Oui | Un identificateur interne tooreference une instance spécifique d’un élément. Bonjour utilisation la plus courante de nom de l’élément hello est dans `outputs`, où les valeurs de sortie hello Hello spécifié d’éléments sont mappés toohello les paramètres du modèle de hello. Vous pouvez également l’utiliser toobind hello valeur de la sortie d’un élément de toohello `defaultValue` d’un autre élément. |
| type | Oui | Bonjour toorender de contrôle d’interface utilisateur pour l’élément de hello. Pour obtenir la liste des types pris en charge, consultez [Éléments](#elements). |
| label | Oui | Hello afficher du texte de l’élément de hello. Certains types d’élément contient plusieurs étiquettes, valeur de hello peut donc être un objet qui contient plusieurs chaînes. |
| defaultValue | Non | valeur par défaut de Hello d’élément de hello. Certains types d’élément prend en charge les valeurs par défaut complexes, valeur de hello peut donc être un objet. |
| toolTip | Non | toodisplay de texte Hello dans hello info-bulle de l’élément de hello. Similaire trop`label`, certains éléments prennent en charge plusieurs chaînes de conseil d’outil. Les liens inline peuvent être intégrés à l’aide de la syntaxe Markdown.
| constraints | Non | Une ou plusieurs propriétés qui sont le comportement de validation utilisé toocustomize hello d’élément de hello. propriétés Hello pris en charge pour les contraintes varient selon le type d’élément. Certains types d’élément ne prend pas en charge la personnalisation du comportement de validation hello et n’ont donc aucune propriété de contraintes. |
| options | Non | Propriétés supplémentaires qui personnalisent le comportement de l’élément de hello hello. Similaire trop`constraints`, propriétés de hello pris en charge varient selon le type d’élément. |
| visible | Non | Indique si l’élément de hello est affiché. Si `true`, élément de hello et les éléments enfants concernés sont affichés. la valeur par défaut Hello est `true`. Utilisez [fonctions logiques](managed-application-createuidefinition-functions.md#logical-functions) toodynamically contrôler la valeur de cette propriété.

## <a name="elements"></a>Éléments

documentation de Hello pour chaque élément contient un exemple d’interface utilisateur, le schéma, la section Notes sur un comportement de l’élément hello (généralement concernant la validation et la personnalisation pris en charge) et le résultat de l’exemple hello.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
