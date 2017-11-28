---
title: "Azure AD Connect Sync : extensions d’annuaire | Microsoft Docs"
description: "Cette rubrique décrit la fonctionnalité d’extensions de répertoire hello dans Azure AD Connect."
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
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="422f3-103">Azure AD Connect Sync : extensions d’annuaire</span><span class="sxs-lookup"><span data-stu-id="422f3-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="422f3-104">Extensions d’annuaire vous permet de schéma de hello tooextend dans Azure AD avec vos propres attributs à partir d’Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="422f3-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="422f3-105">Cette fonctionnalité permet des applications métier toobuild consommation attributs vous continuez toomanage local.</span><span class="sxs-lookup"><span data-stu-id="422f3-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="422f3-106">Ces attributs peuvent être utilisés via des [extensions d’annuaire Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) ou [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="422f3-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="422f3-107">Vous pouvez voir hello disponible à l’aide des attributs [explorer d’Azure AD Graph](https://graphexplorer.cloudapp.net) et [l’Explorateur Microsoft Graph](https://graphexplorer2.azurewebsites.net/) respectivement.</span><span class="sxs-lookup"><span data-stu-id="422f3-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="422f3-108">Actuellement, aucune charge de travail Office 365 n’utilise ces attributs.</span><span class="sxs-lookup"><span data-stu-id="422f3-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="422f3-109">Vous configurez les attributs supplémentaires souhaitées toosynchronize dans chemin d’accès des paramètres personnalisés hello dans l’Assistant installation hello.</span><span class="sxs-lookup"><span data-stu-id="422f3-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="422f3-110">![Assistant d’extension de schéma](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="422f3-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="422f3-111">installation de Hello montre hello suivant des attributs qui sont des candidats valides :</span><span class="sxs-lookup"><span data-stu-id="422f3-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="422f3-112">Types d’utilisateur et d’objet de groupe</span><span class="sxs-lookup"><span data-stu-id="422f3-112">User and Group object types</span></span>
* <span data-ttu-id="422f3-113">Attributs à valeur unique : chaîne, booléen, entier, binaire</span><span class="sxs-lookup"><span data-stu-id="422f3-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="422f3-114">Attributs à valeurs multiples : chaîne, binaire</span><span class="sxs-lookup"><span data-stu-id="422f3-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="422f3-115">liste de Hello d’attributs est lue à partir du cache de schéma hello créé pendant l’installation d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="422f3-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="422f3-116">Si vous avez étendu le schéma Active Directory de hello avec des attributs supplémentaires, puis hello [schéma doit être actualisé](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) avant que ces nouveaux attributs sont visibles.</span><span class="sxs-lookup"><span data-stu-id="422f3-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="422f3-117">Un objet dans Azure AD peut avoir les attributs de too100 répertoire extensions.</span><span class="sxs-lookup"><span data-stu-id="422f3-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="422f3-118">la longueur maximale Hello est de 250 caractères.</span><span class="sxs-lookup"><span data-stu-id="422f3-118">hello max length is 250 characters.</span></span> <span data-ttu-id="422f3-119">Si une valeur d’attribut est plus longue, il est tronqué par le moteur de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="422f3-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="422f3-120">Lors de l’installation d’Azure AD Connect, une application dans laquelle ces attributs sont disponibles est enregistrée.</span><span class="sxs-lookup"><span data-stu-id="422f3-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="422f3-121">Vous pouvez voir cette application Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="422f3-121">You can see this application in hello Azure portal.</span></span>  
![Application d’extension de schéma](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="422f3-123">Ces attributs sont désormais disponibles via Graph : </span><span class="sxs-lookup"><span data-stu-id="422f3-123">These attributes are now available through Graph:</span></span>  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="422f3-125">attributs de Hello sont préfixés avec l’extension\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="422f3-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="422f3-126">Hello AppClientId a hello même valeur pour tous les attributs dans votre locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="422f3-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="422f3-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="422f3-127">Next steps</span></span>
<span data-ttu-id="422f3-128">En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.</span><span class="sxs-lookup"><span data-stu-id="422f3-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="422f3-129">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="422f3-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
