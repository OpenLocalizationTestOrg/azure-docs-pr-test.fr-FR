---
title: "Élément d’interface utilisateur FileUpload des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Common.FileUpload pour les applications gérées Azure"
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
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="1d90d-103">Élément d’interface utilisateur Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="1d90d-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="1d90d-104">Contrôle qui permet à un utilisateur de spécifier un ou plusieurs fichiers à charger.</span><span class="sxs-lookup"><span data-stu-id="1d90d-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="1d90d-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1d90d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="1d90d-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="1d90d-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="1d90d-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="1d90d-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="1d90d-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="1d90d-109">Remarks</span></span>
- <span data-ttu-id="1d90d-110">`constraints.accept` spécifie les types de fichiers qui figurent dans la boîte de dialogue du navigateur.</span><span class="sxs-lookup"><span data-stu-id="1d90d-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="1d90d-111">Consultez la [spécification HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) pour connaître les valeurs autorisées.</span><span class="sxs-lookup"><span data-stu-id="1d90d-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="1d90d-112">La valeur par défaut est **null**.</span><span class="sxs-lookup"><span data-stu-id="1d90d-112">The default value is **null**.</span></span>
- <span data-ttu-id="1d90d-113">Si `options.multiple` est défini sur **true**, l’utilisateur est autorisé à sélectionner plusieurs fichiers dans la boîte de dialogue du fichier du navigateur.</span><span class="sxs-lookup"><span data-stu-id="1d90d-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="1d90d-114">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="1d90d-114">The default value is **false**.</span></span>
- <span data-ttu-id="1d90d-115">Cet élément prend en charge le chargement de fichiers dans deux modes basés sur la valeur de `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="1d90d-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="1d90d-116">Si **file** est spécifié, la sortie contient le contenu du fichier sous la forme d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="1d90d-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="1d90d-117">Si **url** est spécifié, le fichier est chargé sur un emplacement temporaire et la sortie contient l’URL de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="1d90d-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="1d90d-118">Les objets blob temporaires sont purgés après 24 heures.</span><span class="sxs-lookup"><span data-stu-id="1d90d-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="1d90d-119">La valeur par défaut est **file**.</span><span class="sxs-lookup"><span data-stu-id="1d90d-119">The default value is **file**.</span></span>
- <span data-ttu-id="1d90d-120">La valeur de `options.openMode` détermine la façon dont le fichier est lu.</span><span class="sxs-lookup"><span data-stu-id="1d90d-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="1d90d-121">Si le fichier doit être du texte brut, spécifiez **text** ; sinon, spécifiez **binary**.</span><span class="sxs-lookup"><span data-stu-id="1d90d-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="1d90d-122">La valeur par défaut est **text**.</span><span class="sxs-lookup"><span data-stu-id="1d90d-122">The default value is **text**.</span></span>
- <span data-ttu-id="1d90d-123">Si `options.uploadMode` est défini sur **file** et `options.openMode` sur **binary**, la sortie est codée en base64.</span><span class="sxs-lookup"><span data-stu-id="1d90d-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="1d90d-124">`options.encoding` spécifie l’encodage à utiliser lors de la lecture du fichier.</span><span class="sxs-lookup"><span data-stu-id="1d90d-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="1d90d-125">La valeur par défaut est **UTF-8**et est utilisée uniquement lorsque `options.openMode` est défini sur **text**.</span><span class="sxs-lookup"><span data-stu-id="1d90d-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="1d90d-126">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="1d90d-126">Sample output</span></span>
<span data-ttu-id="1d90d-127">Si options.multiple a la valeur false et options.uploadMode la valeur file, la sortie contient le contenu du fichier sous forme de chaîne JSON :</span><span class="sxs-lookup"><span data-stu-id="1d90d-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="1d90d-128">Si options.multiple a la valeur true et options.uploadMode la valeur file, la sortie contient le contenu des fichiers sous forme de tableau JSON :</span><span class="sxs-lookup"><span data-stu-id="1d90d-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="1d90d-129">Si options.multiple a la valeur false et options.uploadMode la valeur url, la sortie contient une URL sous forme de chaîne JSON :</span><span class="sxs-lookup"><span data-stu-id="1d90d-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="1d90d-130">Si options.multiple a la valeur true et options.uploadMode la valeur url, la sortie contient une liste d’URL sous forme de tableau JSON :</span><span class="sxs-lookup"><span data-stu-id="1d90d-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="1d90d-131">Lorsque vous testez un élément CreateUiDefinition, certains navigateurs (comme Google Chrome) tronquent les URL générées par l’élément Microsoft.Common.FileUpload dans la console du navigateur.</span><span class="sxs-lookup"><span data-stu-id="1d90d-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="1d90d-132">Vous devrez peut-être cliquer avec le bouton droit sur des liens pour copier les URL complètes.</span><span class="sxs-lookup"><span data-stu-id="1d90d-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d90d-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d90d-133">Next steps</span></span>
* <span data-ttu-id="1d90d-134">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d90d-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1d90d-135">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d90d-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="1d90d-136">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="1d90d-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
