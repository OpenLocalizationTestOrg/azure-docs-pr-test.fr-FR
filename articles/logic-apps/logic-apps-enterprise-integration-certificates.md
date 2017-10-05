---
title: <span data-ttu-id="ecb4b-101">Utilisation de certificats avec Enterprise Integration Pack | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="ecb4b-101">Using certificates with Enterprise Integration Pack | Microsoft Docs</span></span>
description: "<span data-ttu-id=\"ecb4b-102\">Découvrez comment utiliser les certificats avec Enterprise Integration Pack | Azure Logic Apps</span><span class=\"sxs-lookup\"><span data-stu-id=\"ecb4b-102\">Learn how to use certificates with the Enterprise Integration Pack | Azure Logic Apps</span></span>"
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
ms.openlocfilehash: 0570aab14283b38f9efcc50636f0c0c1c8e3ed13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="ecb4b-103">En savoir plus sur les certificats et Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="ecb4b-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="ecb4b-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ecb4b-104">Overview</span></span>
<span data-ttu-id="ecb4b-105">Enterprise Integration utilise des certificats pour sécuriser les communications B2B.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-105">Enterprise integration uses certificates to secure B2B communications.</span></span> <span data-ttu-id="ecb4b-106">Vous pouvez utiliser deux types de certificats dans vos applications Enterprise Integration :</span><span class="sxs-lookup"><span data-stu-id="ecb4b-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="ecb4b-107">Des certificats publics, qui doivent être achetés auprès d’une autorité de certification (CA).</span><span class="sxs-lookup"><span data-stu-id="ecb4b-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="ecb4b-108">Des certificats privés, que vous pouvez créer vous-même.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="ecb4b-109">Ces certificats sont parfois appelés « certificats auto-signés ».</span><span class="sxs-lookup"><span data-stu-id="ecb4b-109">These certificates are sometimes referred to as self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="ecb4b-110">Que sont les certificats ?</span><span class="sxs-lookup"><span data-stu-id="ecb4b-110">What are certificates?</span></span>
<span data-ttu-id="ecb4b-111">Les certificats sont des documents numériques qui vérifient l’identité des participants dans des communications électroniques et qui sécurisent ces communications électroniques.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-111">Certificates are digital documents that verify the identity of the participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="ecb4b-112">Pourquoi utiliser des certificats ?</span><span class="sxs-lookup"><span data-stu-id="ecb4b-112">Why use certificates?</span></span>
<span data-ttu-id="ecb4b-113">Parfois, les communications B2B doivent rester confidentielles.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="ecb4b-114">Enterprise Integration utilise des certificats pour sécuriser ces communications de deux manières :</span><span class="sxs-lookup"><span data-stu-id="ecb4b-114">Enterprise integration uses certificates to secure these communications in two ways:</span></span>

* <span data-ttu-id="ecb4b-115">En chiffrant le contenu des messages</span><span class="sxs-lookup"><span data-stu-id="ecb4b-115">By encrypting the contents of messages</span></span>
* <span data-ttu-id="ecb4b-116">En signant numériquement les messages</span><span class="sxs-lookup"><span data-stu-id="ecb4b-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="ecb4b-117">Téléchargement d’un certificat public</span><span class="sxs-lookup"><span data-stu-id="ecb4b-117">Upload a public certificate</span></span>

<span data-ttu-id="ecb4b-118">Pour utiliser un *certificat public* dans vos applications logiques avec fonctionnalités B2B, vous devez tout d’abord télécharger le certificat dans votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-118">To use a *public certificate* in your logic apps with B2B capabilities, you first need to upload the certificate into your integration account.</span></span>  

<span data-ttu-id="ecb4b-119">Après avoir téléchargé un certificat, vous pouvez l'utiliser pour sécuriser vos messages B2B lorsque vous définissez leurs propriétés dans les [contrats](logic-apps-enterprise-integration-agreements.md) que vous créez.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-119">After you upload a certificate, it's available to help you secure your B2B messages when you define their properties in the [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="ecb4b-120">Voici les étapes détaillées pour télécharger vos certificats publics sur votre compte d’intégration une fois que vous êtes connecté au portail Azure :</span><span class="sxs-lookup"><span data-stu-id="ecb4b-120">Here are the detailed steps for uploading your public certificates into your integration account after you sign in to the Azure portal:</span></span>

1. <span data-ttu-id="ecb4b-121">Sélectionnez **Plus de services** et entrez **intégration** dans la zone de recherche de filtre.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-121">Select **More services** and enter **integration** in the filter search box.</span></span> <span data-ttu-id="ecb4b-122">Sélectionnez **Comptes d’intégration** dans la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-122">Select **Integration Accounts** from the results list</span></span>     
<span data-ttu-id="ecb4b-123">![Sélectionnez Parcourir](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="ecb4b-124">Sélectionnez le compte d’intégration auquel vous ajouterez le certificat.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-124">Select the integration account to which you want to add the certificate.</span></span>  
![Sélectionnez le compte d’intégration auquel vous ajouterez le certificat](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="ecb4b-126">Sélectionnez la mosaïque **Certificats** .</span><span class="sxs-lookup"><span data-stu-id="ecb4b-126">Select the **Certificates** tile.</span></span>  
<span data-ttu-id="ecb4b-127">![Sélectionnez la mosaïque Certificats](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-127">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="ecb4b-128">Dans le panneau **Certificats** qui s’affiche, sélectionnez le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-128">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="ecb4b-129">![Cliquez sur le bouton Ajouter](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-129">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="ecb4b-130">Entrez le **nom** de votre certificat, puis sélectionnez le type de certificat **public** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-130">Enter a **Name** for your certificate, and then select the certificate type as **public** from the dropdown.</span></span>  
6. <span data-ttu-id="ecb4b-131">Sélectionnez l’icône de dossier à droite de la zone de texte **Certificat**.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-131">Select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="ecb4b-132">Lorsque le sélecteur de fichiers apparaît, recherchez puis sélectionnez le fichier de certificat que vous souhaitez télécharger sur votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-132">When the file picker opens, find and select the certificate file that you want to upload to your integration account.</span></span>
7. <span data-ttu-id="ecb4b-133">Sélectionnez le certificat, puis choisissez **OK** dans le sélecteur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-133">Select the certificate, and then select **OK** in the file picker.</span></span> <span data-ttu-id="ecb4b-134">Cette opération valide et télécharge le certificat sur votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-134">This validates and uploads the certificate to your integration account.</span></span>
8. <span data-ttu-id="ecb4b-135">Enfin, de retour dans le panneau **Ajouter un certificat**, sélectionnez le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-135">Finally, back on the **Add certificate** blade, select the **OK** button.</span></span>  
<span data-ttu-id="ecb4b-136">![Cliquez sur le bouton OK](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-136">![Select the OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="ecb4b-137">Sélectionnez la mosaïque **Certificats** .</span><span class="sxs-lookup"><span data-stu-id="ecb4b-137">Select the **Certificates** tile.</span></span> <span data-ttu-id="ecb4b-138">Vous devez voir le certificat qui vient d’être ajouté.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-138">You should see the newly added certificate.</span></span>  
<span data-ttu-id="ecb4b-139">![Consultez le nouveau certificat](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-139">![See the new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="ecb4b-140">Téléchargement d’un certificat privé</span><span class="sxs-lookup"><span data-stu-id="ecb4b-140">Upload a private certificate</span></span>

<span data-ttu-id="ecb4b-141">Pour utiliser un *certificat privé* dans vos applications logiques avec des capacités B2B, vous pouvez télécharger un certificat privé dans votre compte d’intégration en effectuant les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-141">To use a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate to your integration account by taking the following steps</span></span>

1. <span data-ttu-id="ecb4b-142">[Chargez votre clé privée dans Key Vault](../key-vault/key-vault-get-started.md "En savoir plus sur Key Vault") et indiquez un **nom de clé**.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-142">[Upload your private key to Key Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="ecb4b-143">Vous devez autoriser Logic Apps à effectuer des opérations sur Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-143">You must authorize Logic Apps to perform operations on Key Vault.</span></span> <span data-ttu-id="ecb4b-144">Vous pouvez autoriser l’accès au principal du service Logic Apps à l’aide de cette commande PowerShell : `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="ecb4b-144">You can grant access to the Logic Apps service principal by using the following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="ecb4b-145">Après avoir réalisé l’étape précédente, ajoutez un certificat privé au compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-145">After you've taken the previous step, add a private certificate to integration account.</span></span>

<span data-ttu-id="ecb4b-146">Voici les étapes détaillées pour télécharger vos certificats privés sur votre compte d’intégration une fois que vous êtes connecté au portail Azure :</span><span class="sxs-lookup"><span data-stu-id="ecb4b-146">Following are the detailed steps for uploading your private certificates into your integration account after you sign in to the Azure portal:</span></span>  
 
1. <span data-ttu-id="ecb4b-147">Sélectionnez le compte d’intégration auquel vous souhaitez ajouter le certificat, puis sélectionnez la mosaïque **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-147">Select the integration account to which you want to add the certificate and select the **Certificates** tile.</span></span>  
<span data-ttu-id="ecb4b-148">![Sélectionnez la mosaïque Certificats](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-148">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="ecb4b-149">Dans le panneau **Certificats** qui s’affiche, sélectionnez le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-149">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="ecb4b-150">![Cliquez sur le bouton Ajouter](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-150">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="ecb4b-151">Entrez le **nom** de votre certificat, puis sélectionnez le type de certificat **privé** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-151">Enter a **Name** for your certificate, and select the certificate type as **private** from the dropdown.</span></span>   
4. <span data-ttu-id="ecb4b-152">Sélectionnez l’icône de dossier à droite de la zone de texte **Certificat**.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-152">select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="ecb4b-153">Lorsque le sélecteur de fichiers apparaît, recherchez le certificat public que vous souhaitez charger sur votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-153">When the file picker opens, find the corresponding public certificate that you want to upload to your integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="ecb4b-154">Lors de l’ajout d’un certificat privé, il est important d’ajouter le certificat public correspondant à afficher dans les paramètres d’envoi et de réception du [contrat AS2](logic-apps-enterprise-integration-as2.md) pour la signature et le chiffrement des messages.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-154">While adding a private certificate it is important to add corresponding public certificate to show in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting the messages.</span></span>
   > 
   >   

5. <span data-ttu-id="ecb4b-155">Sélectionnez les valeurs appropriées dans les listes déroulantes **Groupe de ressources**, **Key Vault** et **Nom de la clé**, puis cliquez sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-155">Select the **Resource Group**, **Key Vault**, **Key Name** and select the **OK** button.</span></span>  
<span data-ttu-id="ecb4b-156">![Ajouter le certificat](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="ecb4b-157">Sélectionnez la mosaïque **Certificats** .</span><span class="sxs-lookup"><span data-stu-id="ecb4b-157">Select the **Certificates** tile.</span></span> <span data-ttu-id="ecb4b-158">Vous devez voir le certificat qui vient d’être ajouté.</span><span class="sxs-lookup"><span data-stu-id="ecb4b-158">You should see the newly added certificate.</span></span>
<span data-ttu-id="ecb4b-159">![Consultez le nouveau certificat](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="ecb4b-159">![See the new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="ecb4b-160">Créer un contrat B2B</span><span class="sxs-lookup"><span data-stu-id="ecb4b-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="ecb4b-161">En savoir plus sur Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ecb4b-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "En savoir plus sur le coffre de clés")  

