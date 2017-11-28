---
title: certificats aaaManage dans un cluster Azure Service Fabric | Documents Microsoft
description: "Décrit comment supprimer tooadd de nouveaux certificats et certificat de substitution certificat tooor à partir d’un cluster Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="b0a53-103">Ajouter ou supprimer des certificats pour un cluster Service Fabric dans Azure</span><span class="sxs-lookup"><span data-stu-id="b0a53-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="b0a53-104">Il est recommandé de vous familiariser avec la façon dont l’infrastructure de Service utilise des certificats X.509 et être familiarisé avec hello [les scénarios de sécurité du Cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="b0a53-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="b0a53-105">Vous devez comprendre ce qu’est un certificat de cluster et quelle est son utilité avant de passer à la suite.</span><span class="sxs-lookup"><span data-stu-id="b0a53-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="b0a53-106">Sécurité de certificats de service fabric vous permet de que spécifier que deux cluster certificats, un serveur principal et secondaire, lorsque vous configurez lors de la création du cluster, dans les certificats d’addition tooclient.</span><span class="sxs-lookup"><span data-stu-id="b0a53-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="b0a53-107">Consultez trop[création d’un cluster azure via le portail](service-fabric-cluster-creation-via-portal.md) ou [création d’un cluster azure via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) pour plus d’informations sur leur configuration au moment de la création.</span><span class="sxs-lookup"><span data-stu-id="b0a53-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="b0a53-108">Si vous ne spécifiez qu’un seul certificat de cluster lors de la création, puis qui est utilisé en tant que certificat principal de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="b0a53-109">Après la création du cluster, vous pouvez ajouter un certificat en tant que certificat secondaire.</span><span class="sxs-lookup"><span data-stu-id="b0a53-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="b0a53-110">Pour un cluster sécurisé, vous aurez toujours besoin des certificats au moins un cluster valide (non révoqués et n’ayant pas expiré) (principaux ou secondaires) déployé (si ce n’est pas, hello cluster cesse de fonctionner).</span><span class="sxs-lookup"><span data-stu-id="b0a53-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="b0a53-111">90 jours avant que tous les certificats valides atteignent d’expiration, hello système génère un suivi d’avertissement et également un événement d’avertissement d’intégrité sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="b0a53-112">Actuellement, Service Fabric n’envoie aucun courrier électronique ou notification d’aucune sorte à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="b0a53-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="b0a53-113">Ajouter un certificat de cluster secondaire à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="b0a53-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="b0a53-114">Certificat de cluster secondaire ne peut pas être ajouté via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a53-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="b0a53-115">Vous avez toouse Azure powershell pour cela.</span><span class="sxs-lookup"><span data-stu-id="b0a53-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="b0a53-116">processus de Hello est décrit plus loin dans ce document.</span><span class="sxs-lookup"><span data-stu-id="b0a53-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="b0a53-117">Échanger les certificats de cluster hello à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="b0a53-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="b0a53-118">Une fois que vous avez correctement déployé un certificat de cluster secondaire, si vous souhaitez tooswap hello principal et secondaire, puis accédez Panneau de sécurité toohello et sélectionnez option de « D’échange avec principal » de hello dans hello contexte menu tooswap hello secondaire cert avec certificat principal de Hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![Échange de certificat][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="b0a53-120">Suppression d’un certificat de cluster à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="b0a53-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="b0a53-121">Pour un cluster sécurisé, vous devez toujours au moins une valid (non révoqué et n’ayant pas expiré) certificat (principal ou secondaire) déployé dans le cas contraire, hello cluster cesse de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="b0a53-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="b0a53-122">tooremove un certificat secondaire d’être utilisés pour la sécurité du cluster, panneau de sécurité toohello naviguer et sélectionnez hello 'Delete' option à partir du menu contextuel de hello sur certificat secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="b0a53-123">Si votre objectif est de certificat hello tooremove qui est marqué comme principal, vous devez tooswap avec hello secondaire tout d’abord, puis supprimer hello secondaire après la mise à niveau hello a.</span><span class="sxs-lookup"><span data-stu-id="b0a53-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="b0a53-124">Ajouter un certificat secondaire à l’aide de Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0a53-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="b0a53-125">Ces étapes supposent que vous êtes familiarisé avec le fonctionnement du Gestionnaire de ressources et avez déployé au moins un cluster Service Fabric à l’aide d’un modèle de gestionnaire de ressources et modèle hello que vous avez utilisé tooset cluster hello pratique.</span><span class="sxs-lookup"><span data-stu-id="b0a53-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="b0a53-126">Il est également supposé que vous maîtrisez l’utilisation de JSON.</span><span class="sxs-lookup"><span data-stu-id="b0a53-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="b0a53-127">Si vous cherchez un exemple de modèle et les paramètres que vous pouvez utiliser toofollow le long ou comme point de départ, puis le télécharger à partir de ce [-référentiel git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="b0a53-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="b0a53-128">Modifier votre modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b0a53-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="b0a53-129">Pour faciliter le suivre, exemple 5-VM-1-NodeTypes-Secure_Step2.JSON contient toutes les modifications de hello que nous allons.</span><span class="sxs-lookup"><span data-stu-id="b0a53-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="b0a53-130">exemple Hello est disponible à l’adresse [-référentiel git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="b0a53-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="b0a53-131">**Assurez-vous que toofollow toutes les étapes de hello**</span><span class="sxs-lookup"><span data-stu-id="b0a53-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="b0a53-132">**Étape 1 :** ouvrez le modèle de gestionnaire de ressources hello utilisé toodeploy mettre en Cluster.</span><span class="sxs-lookup"><span data-stu-id="b0a53-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="b0a53-133">(Si vous avez téléchargé l’exemple hello de hello au-dessus de référentiel, puis utilisez 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy un cluster sécurisé et puis ouvrir ce modèle).</span><span class="sxs-lookup"><span data-stu-id="b0a53-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="b0a53-134">**Étape 2 :** ajouter **deux nouveaux paramètres** « secCertificateThumbprint » et « secCertificateUrlValue » de type « chaîne » toohello section des paramètres de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b0a53-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="b0a53-135">Vous pouvez copier hello suivant extrait de code et l’ajouter toohello modèle.</span><span class="sxs-lookup"><span data-stu-id="b0a53-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="b0a53-136">En fonction de la source de hello de votre modèle, vous avez peut déjà que ces défini, cas dans ce déplacer l’étape suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="b0a53-137">**Étape 3 :** apporter des modifications toohello **Microsoft.ServiceFabric/clusters** ressource, recherchez la définition de ressource « Microsoft.ServiceFabric/clusters » hello dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b0a53-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="b0a53-138">Sous les propriétés de cette définition, vous trouverez « Certificate » JSON balise, qui doit ressembler à hello suivant extrait de code JSON :</span><span class="sxs-lookup"><span data-stu-id="b0a53-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="b0a53-139">Ajoutez une nouvelle balise « thumbprintSecondary » et donnez-lui la valeur « [parameters(’secCertificateThumbprint’)] ».</span><span class="sxs-lookup"><span data-stu-id="b0a53-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="b0a53-140">Maintenant la définition de ressource hello doit ressembler à hello suivante (selon votre source de modèle de hello, il peut être pas exactement comme hello d’extrait de code ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="b0a53-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="b0a53-141">Si vous souhaitez trop**cert hello de substitution**, puis spécifiez le nouveau certificat de hello en tant que principal actuel de hello principal et le déplacement en tant que base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="b0a53-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="b0a53-142">Cela entraîne la substitution de hello de votre actuel certificat principal toohello nouveau certificat en une seule étape de déploiement.</span><span class="sxs-lookup"><span data-stu-id="b0a53-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="b0a53-143">**Étape 4 :** apporter des modifications trop**tous les** hello **Microsoft.Compute/virtualMachineScaleSets** définitions de ressources - recherchez hello Microsoft.Compute/virtualMachineScaleSets ressource définition.</span><span class="sxs-lookup"><span data-stu-id="b0a53-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="b0a53-144">Faites défiler toohello « éditeur » : « Microsoft.Azure.ServiceFabric », sous « virtualMachineProfile ».</span><span class="sxs-lookup"><span data-stu-id="b0a53-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="b0a53-145">Dans Paramètres du serveur de publication hello service fabric, vous devez voir quelque chose comme ceci.</span><span class="sxs-lookup"><span data-stu-id="b0a53-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="b0a53-147">Ajouter hello nouveau certificat entrées tooit</span><span class="sxs-lookup"><span data-stu-id="b0a53-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="b0a53-148">propriétés de Hello doivent maintenant ressembler à ceci</span><span class="sxs-lookup"><span data-stu-id="b0a53-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="b0a53-150">Si vous souhaitez trop**cert hello de substitution**, puis spécifiez le nouveau certificat de hello en tant que principal actuel de hello principal et le déplacement en tant que base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="b0a53-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="b0a53-151">Cela entraîne la substitution hello de votre actuel certificat toohello nouveau certificat en une seule étape de déploiement.</span><span class="sxs-lookup"><span data-stu-id="b0a53-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="b0a53-152">propriétés de Hello doivent maintenant ressembler à ceci</span><span class="sxs-lookup"><span data-stu-id="b0a53-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="b0a53-154">**Étape 5 :** apporter des modifications trop**tous les** hello **Microsoft.Compute/virtualMachineScaleSets** définitions de ressources - recherchez hello Microsoft.Compute/virtualMachineScaleSets ressource définition.</span><span class="sxs-lookup"><span data-stu-id="b0a53-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="b0a53-155">Faites défiler toohello « vaultCertificates » :, sous « OSProfile ».</span><span class="sxs-lookup"><span data-stu-id="b0a53-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="b0a53-156">Elle devrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b0a53-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="b0a53-158">Ajoutez hello secCertificateUrlValue tooit.</span><span class="sxs-lookup"><span data-stu-id="b0a53-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="b0a53-159">Utilisez hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="b0a53-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="b0a53-160">Maintenant hello résultant Json doit ressembler à ceci.</span><span class="sxs-lookup"><span data-stu-id="b0a53-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="b0a53-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="b0a53-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="b0a53-162">Assurez-vous que vous avez répété étapes 4 et 5 pour toutes les définitions de ressource Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b0a53-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="b0a53-163">Si vous omettez un d’eux, les certificats hello ne seront pas installés sur cette mise et avoir des résultats inattendus dans votre cluster, y compris le cluster hello en panne (si vous vous retrouvez avec aucun certificat valide que ce cluster hello peut utiliser pour la sécurité.</span><span class="sxs-lookup"><span data-stu-id="b0a53-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="b0a53-164">Vérifiez donc bien que vous n’en avez oublié aucune avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="b0a53-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="b0a53-165">Modifier votre modèle fichier tooreflect hello nouveaux paramètres que vous avez ajouté ci-dessus</span><span class="sxs-lookup"><span data-stu-id="b0a53-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="b0a53-166">Si vous utilisez l’exemple hello de hello [-référentiel git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow, vous pouvez démarrer toomake modifications dans l’exemple hello 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="b0a53-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="b0a53-167">Modifier votre paramètre de modèle de gestionnaire de ressources du fichier, ajoutez hello deux nouveaux paramètres pour secCertificateThumbprint et secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="b0a53-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="b0a53-168">Déployer hello modèle tooAzure</span><span class="sxs-lookup"><span data-stu-id="b0a53-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="b0a53-169">Vous est désormais prêt toodeploy tooAzure de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b0a53-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="b0a53-170">Ouvrez une invite de commande Azure PS version 1 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b0a53-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="b0a53-171">Connectez-vous à tooyour compte Azure et sélectionnez l’abonnement azure spécifique de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="b0a53-172">Il s’agit d’une étape importante pour les personnes qui ont toomore d’accès à un seul abonnement azure.</span><span class="sxs-lookup"><span data-stu-id="b0a53-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="b0a53-173">Test toodeploying préalable du modèle hello il.</span><span class="sxs-lookup"><span data-stu-id="b0a53-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="b0a53-174">Utilisez hello même groupe de ressources actuellement déployé sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b0a53-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="b0a53-175">Déployer le groupe de ressources tooyour hello modèle.</span><span class="sxs-lookup"><span data-stu-id="b0a53-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="b0a53-176">Utilisez hello même groupe de ressources actuellement déployé sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b0a53-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="b0a53-177">Exécutez la commande New-AzureRmResourceGroupDeployment de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="b0a53-178">Vous n’avez pas besoin de mode de hello toospecify, étant donné que la valeur par défaut de hello est **incrémentielle**.</span><span class="sxs-lookup"><span data-stu-id="b0a53-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="b0a53-179">Si vous définissez le Mode tooComplete, vous pouvez supprimer par inadvertance des ressources qui ne sont pas dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b0a53-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="b0a53-180">Par conséquent, ne l’utilisez pas dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="b0a53-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="b0a53-181">Voici un remplie exemple Hello même powershell.</span><span class="sxs-lookup"><span data-stu-id="b0a53-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="b0a53-182">Une fois le déploiement de hello est terminée, se connecter à l’aide du cluster tooyour hello nouveau certificat et effectuer des requêtes.</span><span class="sxs-lookup"><span data-stu-id="b0a53-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="b0a53-183">Si vous êtes en mesure de toodo.</span><span class="sxs-lookup"><span data-stu-id="b0a53-183">If you are able toodo.</span></span> <span data-ttu-id="b0a53-184">Vous pouvez supprimer l’ancien certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="b0a53-185">Si vous utilisez un certificat auto-signé, n’oubliez pas de tooimport dans votre magasin de certificats local TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="b0a53-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="b0a53-186">Pour référence rapide ici est cluster sécurisée de hello commande tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="b0a53-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="b0a53-187">Pour référence rapide ici est l’intégrité du cluster tooget hello commande</span><span class="sxs-lookup"><span data-stu-id="b0a53-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="b0a53-188">Déploiement de cluster de toohello Application certificats.</span><span class="sxs-lookup"><span data-stu-id="b0a53-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="b0a53-189">Vous pouvez utiliser hello même étapes comme indiqué dans les étapes 5 ci-dessus toohave hello certificats est déployées à partir d’un toohello keyvault nœuds.</span><span class="sxs-lookup"><span data-stu-id="b0a53-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="b0a53-190">Vous devez simplement définir et utiliser des paramètres différents.</span><span class="sxs-lookup"><span data-stu-id="b0a53-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="b0a53-191">Ajout ou suppression de certificats clients</span><span class="sxs-lookup"><span data-stu-id="b0a53-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="b0a53-192">Dans les certificats de cluster toohello plus, vous pouvez ajouter des opérations de gestion de tooperform de certificats de client sur un cluster service fabric.</span><span class="sxs-lookup"><span data-stu-id="b0a53-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="b0a53-193">Vous pouvez ajouter deux types de certificats clients : administrateur ou en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="b0a53-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="b0a53-194">Ceux-ci peuvent ensuite être opérations d’administration utilisé toocontrol accès toohello et les opérations de requête sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="b0a53-195">Par défaut, les certificats de cluster de hello sont ajoutés toohello Admin certificats liste autorisée.</span><span class="sxs-lookup"><span data-stu-id="b0a53-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="b0a53-196">Vous pouvez spécifier autant de certificats clients que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="b0a53-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="b0a53-197">Chaque ajout ou de suppression des résultats dans un cluster de configuration mise à jour toohello service fabric</span><span class="sxs-lookup"><span data-stu-id="b0a53-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="b0a53-198">Ajout d’un certificat client administrateur ou en lecture seule via le portail</span><span class="sxs-lookup"><span data-stu-id="b0a53-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="b0a53-199">Accédez Panneau de sécurité toohello et sélectionnez hello '+ authentification' bouton sur le panneau de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="b0a53-200">Dans le panneau de « Authentification ajouter » hello, choisissez hello 'Type d’authentification' - 'Client en lecture seule' ou 'Administrateur client'</span><span class="sxs-lookup"><span data-stu-id="b0a53-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="b0a53-201">Choisir d’une méthode hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="b0a53-202">Cela indique tooService Fabric si elle doit rechercher ce certificat à l’aide de nom du sujet hello ou l’empreinte numérique hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="b0a53-203">En règle générale, il n’est pas une méthode d’autorisation sécurité pratique toouse hello, du nom de l’objet.</span><span class="sxs-lookup"><span data-stu-id="b0a53-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![Ajout de certificat client][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="b0a53-205">Suppression de certificats Client - Admin ou en lecture seule à l’aide hello portail</span><span class="sxs-lookup"><span data-stu-id="b0a53-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="b0a53-206">tooremove un certificat secondaire d’être utilisés pour la sécurité du cluster, panneau de sécurité toohello naviguer et sélectionnez hello 'Delete' option à partir du menu contextuel de hello sur certificat spécifique de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a53-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b0a53-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0a53-207">Next steps</span></span>
<span data-ttu-id="b0a53-208">Lisez les articles suivants pour plus d’informations sur la gestion des clusters :</span><span class="sxs-lookup"><span data-stu-id="b0a53-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="b0a53-209">Processus de mise à niveau du cluster Service Fabric et attentes à votre égard</span><span class="sxs-lookup"><span data-stu-id="b0a53-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="b0a53-210">Configurer l’accès en fonction du rôle pour les clients</span><span class="sxs-lookup"><span data-stu-id="b0a53-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


