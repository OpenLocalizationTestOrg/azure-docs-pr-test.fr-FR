---
title: Application Extensions - Azure AD B2C | Microsoft Docs
description: Restauration des extensions b2c-application hello
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="2d599-103">Azure AD B2C : application Extensions</span><span class="sxs-lookup"><span data-stu-id="2d599-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="2d599-104">Lors de la création d’un annuaire Azure AD B2C, une application appelée `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` est automatiquement créé à l’intérieur de hello nouveau répertoire.</span><span class="sxs-lookup"><span data-stu-id="2d599-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="2d599-105">Cette application, le tooas référencé hello **b2c-extensions-app**, est visible dans *inscriptions d’application*.</span><span class="sxs-lookup"><span data-stu-id="2d599-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="2d599-106">Il est utilisé par hello Azure AD B2C service toostore informations utilisateurs et les attributs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="2d599-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="2d599-107">Si l’application hello est supprimée, Azure AD B2C ne fonctionnera pas correctement et votre environnement de production est affectée.</span><span class="sxs-lookup"><span data-stu-id="2d599-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d599-108">Ne supprimez pas les extensions b2c-application hello, sauf si vous envisagez de supprimer des tooimmediately votre client.</span><span class="sxs-lookup"><span data-stu-id="2d599-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="2d599-109">Si l’application hello reste supprimée depuis plus de 30 jours, les informations utilisateur seront définitivement perdues.</span><span class="sxs-lookup"><span data-stu-id="2d599-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="2d599-110">Vérification de cette application d’extensions hello est présente</span><span class="sxs-lookup"><span data-stu-id="2d599-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="2d599-111">tooverify qui hello b2c-extensions-app est présente :</span><span class="sxs-lookup"><span data-stu-id="2d599-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="2d599-112">À l’intérieur de votre locataire Azure AD B2C, cliquez sur **davantage de services** dans le menu de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="2d599-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="2d599-113">Recherchez et ouvrez **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="2d599-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="2d599-114">Recherchez une application dont le nom commence par **b2c-extensions-app**</span><span class="sxs-lookup"><span data-stu-id="2d599-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="2d599-115">Récupérer l’application des extensions hello</span><span class="sxs-lookup"><span data-stu-id="2d599-115">Recover hello extensions app</span></span>

<span data-ttu-id="2d599-116">Si vous avez supprimé accidentellement hello b2c-extensions-app, vous avez 30 jours toorecover il.</span><span class="sxs-lookup"><span data-stu-id="2d599-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="2d599-117">Vous pouvez restaurer l’application hello hello API Graph à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="2d599-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="2d599-118">Parcourir trop[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="2d599-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="2d599-119">Connectez-vous toohello site comme un administrateur global pour le répertoire d’Azure AD B2C hello souhaité toorestore d’application hello supprimé pour.</span><span class="sxs-lookup"><span data-stu-id="2d599-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="2d599-120">Émettre un verbe HTTP GET pour l’URL de hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` avec api-version = 1,6.</span><span class="sxs-lookup"><span data-stu-id="2d599-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="2d599-121">Assurez-vous que tooreplace `{tenantName}` avec votre nom de client.</span><span class="sxs-lookup"><span data-stu-id="2d599-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="2d599-122">Cette opération répertorie toutes les applications hello qui ont été supprimées dans hello 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="2d599-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="2d599-123">Application hello de trouver dans la liste hello où le nom de hello commence avec 'b2c-extension-app' et copie son `objectid` valeur de propriété.</span><span class="sxs-lookup"><span data-stu-id="2d599-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="2d599-124">Émettre une requête HTTP POST par rapport à l’URL de hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="2d599-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="2d599-125">Remplacez hello `{OBJECTID}` partie de l’URL de hello avec hello `objectid` à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="2d599-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="2d599-126">Vous devez maintenant être en mesure de trop[consultez application hello restauré](#verifying-that-the-extensions-app-is-present) Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d599-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="2d599-127">Une application ne peut être restaurée que si elle a été supprimée dans hello 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="2d599-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="2d599-128">Après ce délai, les données sont définitivement perdues.</span><span class="sxs-lookup"><span data-stu-id="2d599-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="2d599-129">Pour obtenir de l’aide, soumettez un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="2d599-129">For more assistance, file a support ticket.</span></span>
