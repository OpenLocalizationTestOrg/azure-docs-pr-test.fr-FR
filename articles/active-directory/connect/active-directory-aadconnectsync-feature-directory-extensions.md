---
title: "Azure AD Connect Sync : extensions d’annuaire | Microsoft Docs"
description: "Cette rubrique décrit la fonctionnalité d’extensions d’annuaire dans Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="e0b72-103">Azure AD Connect Sync : extensions d’annuaire</span><span class="sxs-lookup"><span data-stu-id="e0b72-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="e0b72-104">Les extensions d'annuaire vous permettent d'étendre le schéma dans Azure AD avec vos propres attributs à partir d'un annuaire Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="e0b72-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="e0b72-105">Cette fonctionnalité vous permet de créer des applications métier avec les attributs que vous continuez à gérer en local.</span><span class="sxs-lookup"><span data-stu-id="e0b72-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="e0b72-106">Ces attributs peuvent être utilisés via des [extensions d’annuaire Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) ou [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="e0b72-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="e0b72-107">Vous pouvez voir les attributs disponibles à l’aide de [l’explorateur d’Azure AD Graph](https://graphexplorer.cloudapp.net) et de [l’Explorateur Microsoft Graph](https://graphexplorer2.azurewebsites.net/) respectivement.</span><span class="sxs-lookup"><span data-stu-id="e0b72-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="e0b72-108">Actuellement, aucune charge de travail Office 365 n’utilise ces attributs.</span><span class="sxs-lookup"><span data-stu-id="e0b72-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="e0b72-109">Vous pouvez configurer les attributs supplémentaires à synchroniser dans le chemin d’accès des paramètres personnalisés dans l’Assistant d’installation.</span><span class="sxs-lookup"><span data-stu-id="e0b72-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="e0b72-110">![Assistant d’extension de schéma](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="e0b72-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="e0b72-111">L’installation affiche les attributs suivants, qui sont des candidats valides :</span><span class="sxs-lookup"><span data-stu-id="e0b72-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="e0b72-112">Types d’utilisateur et d’objet de groupe</span><span class="sxs-lookup"><span data-stu-id="e0b72-112">User and Group object types</span></span>
* <span data-ttu-id="e0b72-113">Attributs à valeur unique : chaîne, booléen, entier, binaire</span><span class="sxs-lookup"><span data-stu-id="e0b72-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="e0b72-114">Attributs à valeurs multiples : chaîne, binaire</span><span class="sxs-lookup"><span data-stu-id="e0b72-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="e0b72-115">La liste des attributs est lue depuis le cache du schéma créé pendant l’installation d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="e0b72-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="e0b72-116">Si vous avez étendu le schéma Active Directory avec des attributs supplémentaires, alors le [schéma doit être actualisé](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) avant que ces nouveaux attributs ne soient visibles.</span><span class="sxs-lookup"><span data-stu-id="e0b72-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="e0b72-117">Un objet dans Azure AD peut avoir jusqu’à 100 attributs d’extension d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="e0b72-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="e0b72-118">La longueur maximale est de 250 caractères.</span><span class="sxs-lookup"><span data-stu-id="e0b72-118">The max length is 250 characters.</span></span> <span data-ttu-id="e0b72-119">Si une valeur d’attribut est plus longue, alors elle est tronquée par le moteur de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="e0b72-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="e0b72-120">Lors de l’installation d’Azure AD Connect, une application dans laquelle ces attributs sont disponibles est enregistrée.</span><span class="sxs-lookup"><span data-stu-id="e0b72-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="e0b72-121">Vous pouvez voir cette application dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b72-121">You can see this application in the Azure portal.</span></span>  
![Application d’extension de schéma](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="e0b72-123">Ces attributs sont désormais disponibles via Graph : </span><span class="sxs-lookup"><span data-stu-id="e0b72-123">These attributes are now available through Graph:</span></span>  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="e0b72-125">Les attributs ont pour préfixe extension \_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="e0b72-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="e0b72-126">L’AppClientId a la même valeur pour tous les attributs de votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0b72-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0b72-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0b72-127">Next steps</span></span>
<span data-ttu-id="e0b72-128">En savoir plus sur la configuration de la [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="e0b72-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="e0b72-129">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="e0b72-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
