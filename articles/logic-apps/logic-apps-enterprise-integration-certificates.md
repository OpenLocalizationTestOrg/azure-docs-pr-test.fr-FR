---
title: "certificats aaaUsing avec le Pack d’intégration Enterprise | Documents Microsoft"
description: "En savoir plus l’utilisation des certificats avec hello Pack d’intégration Enterprise toouse | Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="e9e3e-103">En savoir plus sur les certificats et Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="e9e3e-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="e9e3e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e9e3e-104">Overview</span></span>
<span data-ttu-id="e9e3e-105">Intégration d’entreprise utilise les communications de certificats toosecure B2B.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="e9e3e-106">Vous pouvez utiliser deux types de certificats dans vos applications Enterprise Integration :</span><span class="sxs-lookup"><span data-stu-id="e9e3e-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="e9e3e-107">Des certificats publics, qui doivent être achetés auprès d’une autorité de certification (CA).</span><span class="sxs-lookup"><span data-stu-id="e9e3e-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="e9e3e-108">Des certificats privés, que vous pouvez créer vous-même.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="e9e3e-109">Ces certificats sont parfois tooas auxquels les certificats auto-signés.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="e9e3e-110">Que sont les certificats ?</span><span class="sxs-lookup"><span data-stu-id="e9e3e-110">What are certificates?</span></span>
<span data-ttu-id="e9e3e-111">Les certificats sont des documents numériques qui vérifient l’identité hello de participants hello dans les communications électroniques et qui également sécuriser les communications électroniques.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="e9e3e-112">Pourquoi utiliser des certificats ?</span><span class="sxs-lookup"><span data-stu-id="e9e3e-112">Why use certificates?</span></span>
<span data-ttu-id="e9e3e-113">Parfois, les communications B2B doivent rester confidentielles.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="e9e3e-114">Intégration d’entreprise utilise des certificats toosecure ces communications de deux manières :</span><span class="sxs-lookup"><span data-stu-id="e9e3e-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="e9e3e-115">En chiffrant contenu hello des messages</span><span class="sxs-lookup"><span data-stu-id="e9e3e-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="e9e3e-116">En signant numériquement les messages</span><span class="sxs-lookup"><span data-stu-id="e9e3e-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="e9e3e-117">Téléchargement d’un certificat public</span><span class="sxs-lookup"><span data-stu-id="e9e3e-117">Upload a public certificate</span></span>

<span data-ttu-id="e9e3e-118">toouse un *certificat public* dans vos applications logiques avec les fonctionnalités B2B, vous devez tout d’abord certificat de hello tooupload à votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="e9e3e-119">Après avoir téléchargé un certificat, il est disponible toohelp vous sécuriser vos messages B2B lorsque vous définissez leurs propriétés Bonjour [accords](logic-apps-enterprise-integration-agreements.md) que vous créez.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="e9e3e-120">Voici hello des instructions détaillées sur le téléchargement de vos certificats publics dans votre compte d’intégration après vous être connecté toohello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="e9e3e-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="e9e3e-121">Sélectionnez **davantage de services** et entrez **intégration** dans la zone de recherche filtre hello.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="e9e3e-122">Sélectionnez **comptes d’intégration** à partir de la liste des résultats hello</span><span class="sxs-lookup"><span data-stu-id="e9e3e-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="e9e3e-123">![Sélectionnez Parcourir](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="e9e3e-124">Sélectionnez hello intégration compte toowhich tooadd hello certificat.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Sélectionnez hello intégration compte toowhich tooadd hello certificat](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="e9e3e-126">Sélectionnez hello **certificats** vignette.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="e9e3e-127">![Sélectionnez hello certificats vignette](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="e9e3e-128">Bonjour **certificats** panneau s’ouvre, sélectionnez hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="e9e3e-129">![Sélectionnez le bouton Ajouter de hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="e9e3e-130">Entrez un **nom** pour votre certificat et le type de certificat puis hello en tant que **public** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="e9e3e-131">Icône de dossier hello SELECT sur le côté droit de hello Hello **certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="e9e3e-132">Lorsque le sélecteur de fichier hello s’ouvre, recherchez et sélectionnez hello fichier de certificat que vous souhaitez le compte d’intégration tooupload tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="e9e3e-133">Sélectionnez le certificat de hello, puis **OK** dans le sélecteur de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="e9e3e-134">Cela valide et télécharge le compte d’intégration tooyour hello certificat.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="e9e3e-135">Enfin, de retour sur hello **ajouter un certificat** panneau, sélectionnez hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="e9e3e-136">![Sélectionnez le bouton OK de hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="e9e3e-137">Sélectionnez hello **certificats** vignette.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="e9e3e-138">Vous devez voir hello certificat a été ajouté récemment.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="e9e3e-139">![Consultez le nouveau certificat de hello](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="e9e3e-140">Téléchargement d’un certificat privé</span><span class="sxs-lookup"><span data-stu-id="e9e3e-140">Upload a private certificate</span></span>

<span data-ttu-id="e9e3e-141">toouse un *certificat privé* dans vos applications logiques avec les fonctionnalités B2B, vous pouvez télécharger un compte d’intégration tooyour certificat privé à hello en prenant comme suit</span><span class="sxs-lookup"><span data-stu-id="e9e3e-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="e9e3e-142">[Télécharger votre tooKey de clé privée coffre](../key-vault/key-vault-get-started.md "en savoir plus sur le coffre de clés") et fournir un **nom de la clé**</span><span class="sxs-lookup"><span data-stu-id="e9e3e-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="e9e3e-143">Vous devez autoriser les opérations de tooperform Logic Apps sur le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="e9e3e-144">Vous pouvez accorder principal du service accès toohello Logic Apps à l’aide de hello suivant de commande PowerShell :`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="e9e3e-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="e9e3e-145">Une fois que vous avez effectuées précédemment hello, ajoutez un compte de toointegration de certificat privé.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="e9e3e-146">Suivantes sont hello des instructions détaillées sur le téléchargement de vos certificats privés dans votre compte d’intégration après que vous être connecté toohello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="e9e3e-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="e9e3e-147">Sélectionnez hello intégration compte toowhich vous tooadd hello certificat et sélectionnez hello **certificats** vignette.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="e9e3e-148">![Sélectionnez hello certificats vignette](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="e9e3e-149">Bonjour **certificats** panneau s’ouvre, sélectionnez hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="e9e3e-150">![Sélectionnez le bouton Ajouter de hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="e9e3e-151">Entrez un **nom** pour votre certificat et le type de certificat hello sélectionnez en tant que **privé** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="e9e3e-152">Sélectionnez l’icône de dossier hello sur le côté droit de hello Hello **certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="e9e3e-153">Lorsque le sélecteur de fichier hello s’ouvre, trouver le certificat public correspondant hello compte d’intégration tooupload tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="e9e3e-154">Lors de l’ajout d’un certificat privé, il est important de tooadd correspondant publique du certificat tooshow dans [accord AS2](logic-apps-enterprise-integration-as2.md) recevoir et envoyer des paramètres pour signer et chiffrer les messages de type hello.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="e9e3e-155">Sélectionnez hello **groupe de ressources**, **le coffre de clés**, **nom de la clé** et sélectionnez hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="e9e3e-156">![Ajouter le certificat](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="e9e3e-157">Sélectionnez hello **certificats** vignette.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="e9e3e-158">Vous devez voir hello certificat a été ajouté récemment.</span><span class="sxs-lookup"><span data-stu-id="e9e3e-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="e9e3e-159">![Consultez le nouveau certificat de hello](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="e9e3e-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="e9e3e-160">Créer un contrat B2B</span><span class="sxs-lookup"><span data-stu-id="e9e3e-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="e9e3e-161">En savoir plus sur Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e9e3e-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "En savoir plus sur le coffre de clés")  

