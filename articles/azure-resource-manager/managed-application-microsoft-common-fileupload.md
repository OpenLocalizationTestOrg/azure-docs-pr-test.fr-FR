---
title: "élément de l’interface utilisateur de FileUpload pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.FileUpload pour des Applications managées Azure"
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="26594-103">Élément d’interface utilisateur Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="26594-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="26594-104">Un contrôle qui permet une toospecify d’utilisateur, un ou plusieurs fichiers tooupload.</span><span class="sxs-lookup"><span data-stu-id="26594-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="26594-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="26594-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="26594-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="26594-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="26594-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="26594-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="26594-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="26594-109">Remarks</span></span>
- <span data-ttu-id="26594-110">`constraints.accept`Spécifie les types de hello de fichiers qui figurent dans la boîte de dialogue de fichier du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="26594-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="26594-111">Consultez hello [spécification HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) pour les valeurs autorisées.</span><span class="sxs-lookup"><span data-stu-id="26594-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="26594-112">la valeur par défaut Hello est **null**.</span><span class="sxs-lookup"><span data-stu-id="26594-112">hello default value is **null**.</span></span>
- <span data-ttu-id="26594-113">Si `options.multiple` est défini trop**true**, utilisateur de hello est autorisé tooselect, et plusieurs fichiers dans la boîte de dialogue de fichier du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="26594-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="26594-114">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="26594-114">hello default value is **false**.</span></span>
- <span data-ttu-id="26594-115">Cet élément prend en charge le téléchargement de fichiers dans les deux modes, selon la valeur hello `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="26594-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="26594-116">Si **fichier** est spécifié, la sortie de hello contient contenu hello du fichier hello comme un objet blob.</span><span class="sxs-lookup"><span data-stu-id="26594-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="26594-117">Si **url** est spécifié, le fichier de hello est alors téléchargé tooa un emplacement temporaire et sortie de hello contient hello des URL de blob de hello.</span><span class="sxs-lookup"><span data-stu-id="26594-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="26594-118">Les objets blob temporaires sont purgés après 24 heures.</span><span class="sxs-lookup"><span data-stu-id="26594-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="26594-119">la valeur par défaut Hello est **fichier**.</span><span class="sxs-lookup"><span data-stu-id="26594-119">hello default value is **file**.</span></span>
- <span data-ttu-id="26594-120">Hello valeur `options.openMode` détermine la façon dont les fichiers hello sont en lecture.</span><span class="sxs-lookup"><span data-stu-id="26594-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="26594-121">Si le fichier de hello est toobe attendu du texte brut, spécifiez **texte**; sinon, spécifiez **binaire**.</span><span class="sxs-lookup"><span data-stu-id="26594-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="26594-122">la valeur par défaut Hello est **texte**.</span><span class="sxs-lookup"><span data-stu-id="26594-122">hello default value is **text**.</span></span>
- <span data-ttu-id="26594-123">Si `options.uploadMode` est défini trop**fichier** et `options.openMode` est défini trop**binaire**, sortie de hello est codée en base64.</span><span class="sxs-lookup"><span data-stu-id="26594-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="26594-124">`options.encoding`Spécifie les toouse codage hello lors de la lecture du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="26594-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="26594-125">la valeur par défaut Hello est **UTF-8**et est utilisée uniquement lorsque `options.openMode` est défini trop**texte**.</span><span class="sxs-lookup"><span data-stu-id="26594-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="26594-126">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="26594-126">Sample output</span></span>
<span data-ttu-id="26594-127">Si options.multiple a la valeur false et options.uploadMode est le fichier, la sortie contient contenu hello du fichier de hello sous forme de chaîne JSON :</span><span class="sxs-lookup"><span data-stu-id="26594-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="26594-128">Si options.multiple a la valeur true and'options.uploadMode est le fichier, puis la sortie contient du contenu hello des fichiers de hello en un tableau JSON :</span><span class="sxs-lookup"><span data-stu-id="26594-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="26594-129">Si options.multiple a la valeur false et options.uploadMode la valeur url, la sortie contient une URL sous forme de chaîne JSON :</span><span class="sxs-lookup"><span data-stu-id="26594-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="26594-130">Si options.multiple a la valeur true et options.uploadMode la valeur url, la sortie contient une liste d’URL sous forme de tableau JSON :</span><span class="sxs-lookup"><span data-stu-id="26594-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="26594-131">Lorsque vous testez une CreateUiDefinition, certains navigateurs (comme Google Chrome) tronquent les URL générées par l’élément de Microsoft.Common.FileUpload hello dans la console du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="26594-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="26594-132">Vous devrez peut-être tooright-cliquez sur les liens toocopy hello URL complètes.</span><span class="sxs-lookup"><span data-stu-id="26594-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="26594-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26594-133">Next steps</span></span>
* <span data-ttu-id="26594-134">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26594-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="26594-135">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26594-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="26594-136">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="26594-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
