---
title: "aaaSet d’Azure Key Vault avec rotation de clés de bout en bout et d’audit | Documents Microsoft"
description: "Utilisez cette procédure-tootoohelp que vous être défini sur la rotation des clés et l’analyse des journaux de coffre de clés."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="07f4f-103">Configurer Azure Key Vault avec une rotation des clés et un audit de bout en bout</span><span class="sxs-lookup"><span data-stu-id="07f4f-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="07f4f-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="07f4f-104">Introduction</span></span>
<span data-ttu-id="07f4f-105">Après avoir créé votre coffre de clés, vous serez en mesure de toostart à l’aide de ce coffre toostore vos clés et les clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="07f4f-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="07f4f-106">Vos applications n’est plus nécessaire toopersist vos clés ou les clés secrètes, mais au lieu de cela demande les hello coffre de clés en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="07f4f-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="07f4f-107">Ainsi, vous tooupdate clés et les secrets sans affecter le comportement de hello de votre application, ce qui ouvre un éventail de possibilités autour de votre clé et la gestion des secrets.</span><span class="sxs-lookup"><span data-stu-id="07f4f-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="07f4f-108">Cet article assiste un exemple d’utilisation d’Azure Key Vault toostore un secret, dans ce cas, une clé de compte de stockage Azure qui est accessible par une application.</span><span class="sxs-lookup"><span data-stu-id="07f4f-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="07f4f-109">Il vous propose également une démonstration d’implémentation d’une rotation planifiée de cette clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="07f4f-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="07f4f-110">Enfin, il décrit une démonstration de comment toomonitor hello les journaux d’audit de coffre de clés et de déclencher des alertes lorsque des demandes inattendus sont effectuées.</span><span class="sxs-lookup"><span data-stu-id="07f4f-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="07f4f-111">Ce didacticiel n’est pas prévue tooexplain détail hello la configuration initiale de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="07f4f-112">Pour plus d’informations, consultez [Prise en main d’Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="07f4f-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="07f4f-113">Pour connaître la marche à suivre avec l’interface de ligne de commande interplateforme, consultez la rubrique [Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI)](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="07f4f-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="07f4f-114">Configuration d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="07f4f-114">Set up Key Vault</span></span>
<span data-ttu-id="07f4f-115">tooenable un tooretrieve application un secret de coffre de clés, vous devez tout d’abord créer la clé secrète de hello et téléchargez-le tooyour coffre.</span><span class="sxs-lookup"><span data-stu-id="07f4f-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="07f4f-116">Cela peut être accompli en démarrant une session Azure PowerShell et de signature dans tooyour compte Azure avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07f4f-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="07f4f-117">Dans la fenêtre contextuelle du navigateur de hello, entrez votre nom d’utilisateur de compte Azure et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="07f4f-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="07f4f-118">PowerShell Obtient tous les abonnements hello qui sont associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="07f4f-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="07f4f-119">PowerShell utilise hello premier celui par défaut.</span><span class="sxs-lookup"><span data-stu-id="07f4f-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="07f4f-120">Si vous avez plusieurs abonnements, vous pouvez avoir toospecify qui a été utilisé toocreate hello votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="07f4f-121">Entrez hello suivant toosee les abonnements de hello pour votre compte :</span><span class="sxs-lookup"><span data-stu-id="07f4f-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="07f4f-122">abonnement hello toospecify associé avec le coffre de clés hello vous se connectent, entrez :</span><span class="sxs-lookup"><span data-stu-id="07f4f-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="07f4f-123">Cet article présentant le stockage d’une clé de compte de stockage sous la forme d’un secret, vous devez obtenir cette clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="07f4f-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="07f4f-124">Après avoir récupéré votre secret (dans ce cas, votre clé de compte de stockage), vous devez convertir cette chaîne sécurisée tooa et ensuite créer une clé secrète avec cette valeur dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="07f4f-125">Ensuite, obtenez hello URI pour secret hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="07f4f-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="07f4f-126">Cela est utilisé dans une étape ultérieure lorsque vous appelez hello coffre de clés tooretrieve votre clé secrète.</span><span class="sxs-lookup"><span data-stu-id="07f4f-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="07f4f-127">Exécutez hello suivant de commande PowerShell et prenez note de la valeur d’ID hello, qui est un secret hello URI :</span><span class="sxs-lookup"><span data-stu-id="07f4f-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="07f4f-128">Configurer application hello</span><span class="sxs-lookup"><span data-stu-id="07f4f-128">Set up hello application</span></span>
<span data-ttu-id="07f4f-129">Maintenant que vous avez une clé secrète stockée, vous pouvez utiliser le code tooretrieve et l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="07f4f-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="07f4f-130">Il existe quelques tooachieve requis d’étapes cela.</span><span class="sxs-lookup"><span data-stu-id="07f4f-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="07f4f-131">Bonjour première étape la plus importante est l’inscription de votre application avec Azure Active Directory et puis indiquant le coffre de clés les informations de votre application afin qu’il peut autoriser les demandes à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="07f4f-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="07f4f-132">Votre application doit être créée sur hello même locataire Azure Active Directory en tant que votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="07f4f-133">Ouvrez l’onglet d’applications hello d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07f4f-133">Open hello applications tab of Azure Active Directory.</span></span>

![Ouvrir des applications dans Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="07f4f-135">Choisissez **ajouter** tooadd un tooyour application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07f4f-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![Choisir AJOUTER](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="07f4f-137">Laissez le type d’application hello **WEB APPLICATION et/ou API WEB** et donnez un nom à votre application.</span><span class="sxs-lookup"><span data-stu-id="07f4f-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Application hello nom](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="07f4f-139">Attribuez à votre application une **URL DE CONNEXION** et un **URI ID D’APPLICATION**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="07f4f-140">Pour cette démonstration, il peut s’agir de n’importe quel URL/URI, et vous pouvez les modifier ultérieurement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="07f4f-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Fournir les URI nécessaires](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="07f4f-142">Après l’application hello tooAzure Active Directory, vous seront mises en page de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="07f4f-143">Cliquez sur hello **configurer** onglet, puis recherchez et copiez hello **ID Client** valeur.</span><span class="sxs-lookup"><span data-stu-id="07f4f-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="07f4f-144">Prenez note de l’ID de client hello pour les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="07f4f-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="07f4f-145">Ensuite, générez une clé pour votre application afin qu’elle puisse interagir avec votre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07f4f-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="07f4f-146">Vous pouvez le créer sous hello **clés** section Bonjour **Configuration** onglet. Prenez note de clé hello qui vient d’être généré à partir de votre application Azure Active Directory pour une utilisation dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="07f4f-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Clés d’application Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="07f4f-148">Avant d’établir tous les appels à partir de votre application dans le coffre de clés hello, vous devez indiquer le coffre de clés hello sur votre application et ses autorisations.</span><span class="sxs-lookup"><span data-stu-id="07f4f-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="07f4f-149">Hello commande suivante prend hello coffre nom et ID de client hello à partir de votre application d’Azure Active Directory et les allocations **obtenir** tooyour clé forte pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="07f4f-150">À ce stade, vous êtes prêt toostart générer votre application appelle.</span><span class="sxs-lookup"><span data-stu-id="07f4f-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="07f4f-151">Dans votre application, vous devez installer hello NuGet packages requis toointeract avec le coffre de clés Azure et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07f4f-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="07f4f-152">À partir de la console du Gestionnaire de Package Visual Studio hello, entrez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="07f4f-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="07f4f-153">À l’écriture de hello de cet article, hello version actuelle du package d’Azure Active Directory hello est 3.10.305231913, vous souhaitez que la version la plus récente tooconfirm hello et mettre à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="07f4f-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="07f4f-154">Dans votre code d’application, créez une méthode de hello toohold classe pour l’authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07f4f-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="07f4f-155">Dans cet exemple, la classe est appelée **Utils**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="07f4f-156">Ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="07f4f-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="07f4f-157">Ensuite, ajoutez hello suivant un jeton JWT méthode tooretrieve hello d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07f4f-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="07f4f-158">Pour faciliter la maintenance, vous pouvez choisir les valeurs de chaîne codée en dur toomove hello dans votre configuration de l’application web ou.</span><span class="sxs-lookup"><span data-stu-id="07f4f-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="07f4f-159">Ajouter hello code nécessaire toocall le coffre de clés et récupérer la valeur de votre secret principal.</span><span class="sxs-lookup"><span data-stu-id="07f4f-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="07f4f-160">Vous devez d’abord ajouter suivant de hello à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="07f4f-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="07f4f-161">Ajouter tooinvoke les appels de méthode hello coffre de clés et de récupérer votre clé secrète.</span><span class="sxs-lookup"><span data-stu-id="07f4f-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="07f4f-162">Dans cette méthode, vous indiquez hello question secrète URI que vous avez enregistré à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="07f4f-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="07f4f-163">Notez que hello hello **GetToken** méthode hello **Utils** classe créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="07f4f-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="07f4f-164">Lorsque vous exécutez votre application, vous devez maintenant authentification tooAzure Active Directory et puis la récupération de la valeur de votre secret principal dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="07f4f-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="07f4f-165">Rotation des clés à l’aide d’Azure Automation</span><span class="sxs-lookup"><span data-stu-id="07f4f-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="07f4f-166">Diverses options de mise en œuvre d’une stratégie de rotation sont possibles pour les valeurs que vous stockez sous forme de secrets Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="07f4f-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="07f4f-167">La rotation des secrets peut être manuelle, elle peut également être effectuée par programmation à l’aide d’appels d’API ou à l’aide d’un script Automation.</span><span class="sxs-lookup"><span data-stu-id="07f4f-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="07f4f-168">Pour des raisons de hello de cet article, vous serez à l’aide d’Azure PowerShell combinées avec Azure Automation toochange une clé d’accès de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="07f4f-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="07f4f-169">Ensuite, vous mettrez à jour un secret de coffre de clés avec cette nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="07f4f-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="07f4f-170">tooallow Azure Automation tooset les valeurs des secrets dans votre coffre de clés, vous devez obtenir les ID de client hello pour connexion hello nommée AzureRunAsConnection, qui a été créée lorsque vous avez établi votre instance Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="07f4f-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="07f4f-171">Vous pouvez obtenir cet ID en choisissant **Actifs** dans votre instance Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="07f4f-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="07f4f-172">À partir de là, vous choisissez **connexions** , puis sélectionnez hello **AzureRunAsConnection** principe de service.</span><span class="sxs-lookup"><span data-stu-id="07f4f-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="07f4f-173">Prenez note de hello **ID de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-173">Take note of hello **Application ID**.</span></span>

![ID client Azure Automation](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="07f4f-175">Dans **Actifs**, choisissez **Modules**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="07f4f-176">À partir de **Modules**, sélectionnez **galerie**, puis recherchez et **importation** mis à jour les versions de chacune des hello suivant des modules :</span><span class="sxs-lookup"><span data-stu-id="07f4f-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="07f4f-177">À hello l’écriture de cet article, uniquement hello précédemment notées modules nécessaires toobe mis à jour pour hello script suivant.</span><span class="sxs-lookup"><span data-stu-id="07f4f-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="07f4f-178">Si vous constatez un échec de votre tâche d’automatisation, vérifiez que tous les modules nécessaires et leurs dépendances ont été importés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="07f4f-179">Une fois que vous avez extrait l’ID de l’application hello pour votre connexion Azure Automation, vous devez indiquer votre coffre de clés que cette application a accès tooupdate secrets dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="07f4f-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="07f4f-180">Cela peut être accompli par hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="07f4f-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="07f4f-181">Sélectionnez ensuite **Runbooks** sous votre instance Azure Automation, puis **Ajouter un runbook**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="07f4f-182">Sélectionnez **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-182">Select **Quick Create**.</span></span> <span data-ttu-id="07f4f-183">Nom de votre runbook, puis choisissez **PowerShell** en tant que type de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="07f4f-184">Vous avez hello option tooadd une description.</span><span class="sxs-lookup"><span data-stu-id="07f4f-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="07f4f-185">Pour finir, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-185">Finally, click **Create**.</span></span>

![Créer un runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="07f4f-187">Collez hello script PowerShell dans le volet de l’éditeur pour votre nouveau runbook hello suivant :</span><span class="sxs-lookup"><span data-stu-id="07f4f-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="07f4f-188">Dans le volet de l’éditeur hello, choisissez **volet Test** tootest votre script.</span><span class="sxs-lookup"><span data-stu-id="07f4f-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="07f4f-189">Une fois le script de hello s’exécute sans erreur, vous pouvez sélectionner **publier**, et vous pouvez ensuite appliquer une planification pour le runbook hello dans le volet de configuration de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="07f4f-190">Pipeline d’audit de Key Vault</span><span class="sxs-lookup"><span data-stu-id="07f4f-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="07f4f-191">Lorsque vous configurez un coffre de clés, vous pouvez activer l’audit des journaux de toocollect sur les demandes d’accès effectuées toohello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="07f4f-192">Ces journaux sont stockés dans un compte de stockage Azure spécifié et peuvent être récupérés, contrôlés et analysés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="07f4f-193">Hello scénario suivant utilise des fonctions Azure, les applications de la logique d’Azure et toocreate de journaux d’audit de coffre de clés un toosend pipeline un message électronique quand une application qui ne correspond pas aux ID de l’application hello de hello web application récupère les clés secrètes de coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="07f4f-194">Vous devez tout d’abord activer la journalisation sur votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="07f4f-195">Cela est possible via hello suivant de commandes PowerShell (détails complets peuvent être consultés à [journalisation de coffre de clé](key-vault-logging.md)) :</span><span class="sxs-lookup"><span data-stu-id="07f4f-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="07f4f-196">Une fois cette option est activée, les journaux d’audit commencer à collecter dans hello désigné du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="07f4f-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="07f4f-197">Ces journaux contiennent des événements indiquant la méthode et la date/l’heure d’accès à vos coffres de clés, et qui y a accédé.</span><span class="sxs-lookup"><span data-stu-id="07f4f-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="07f4f-198">Vous pouvez accéder à vos informations de journalisation 10 minutes après l’opération de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="07f4f-199">Elles sont généralement disponibles plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="07f4f-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="07f4f-200">étape suivante de Hello est trop[créer une file d’attente Azure Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="07f4f-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="07f4f-201">C’est dans celle-ci que les journaux d’audit de coffre de clés sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="07f4f-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="07f4f-202">Lors de la file d’attente de hello des messages du journal d’audit hello, application logique de hello les récupère et agit sur eux.</span><span class="sxs-lookup"><span data-stu-id="07f4f-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="07f4f-203">Créer un service bus avec hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="07f4f-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="07f4f-204">Créer un espace de noms Service Bus (si vous disposez déjà de celui que vous voulez toouse pour ce faire, ignorer tooStep 2).</span><span class="sxs-lookup"><span data-stu-id="07f4f-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="07f4f-205">Parcourir toohello service bus dans hello portail Azure et sélectionnez hello espace de noms que vous souhaitez file d’attente de toocreate hello dans.</span><span class="sxs-lookup"><span data-stu-id="07f4f-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="07f4f-206">Sélectionnez **nouveau** et choisissez **Service Bus > file d’attente** et entrez les détails de hello requis.</span><span class="sxs-lookup"><span data-stu-id="07f4f-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="07f4f-207">Sélectionnez les informations de connexion de Service Bus hello en choisissant l’espace de noms hello en cliquant sur **les informations de connexion**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="07f4f-208">Vous devez ces informations pour la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="07f4f-209">Ensuite, [créer une fonction Azure](../azure-functions/functions-create-first-azure-function.md) toopoll les journaux de coffre de clés dans hello compte de stockage et de chercher de nouveaux événements.</span><span class="sxs-lookup"><span data-stu-id="07f4f-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="07f4f-210">Il s’agit d’une fonction déclenchée de manière planifiée.</span><span class="sxs-lookup"><span data-stu-id="07f4f-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="07f4f-211">toocreate une fonction d’Azure, choisissez **Nouveau > application de la fonction** Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="07f4f-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="07f4f-212">Lors de la création, vous pouvez utiliser un plan d’hébergement existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="07f4f-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="07f4f-213">Vous pouvez également opter pour un hébergement dynamique.</span><span class="sxs-lookup"><span data-stu-id="07f4f-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="07f4f-214">Vous trouverez plus d’informations sur les options d’hébergement de fonction à [comment tooscale Azure fonctions](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="07f4f-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="07f4f-215">Lors de la création de hello fonction Azure, accédez tooit et choisir un minuteur de fonction et C\#.</span><span class="sxs-lookup"><span data-stu-id="07f4f-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="07f4f-216">Cliquez ensuite sur **Créer cette fonction**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-216">Then click **Create this function**.</span></span>

![Panneau d’accueil d’Azure Functions](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="07f4f-218">Sur hello **développer** onglet, remplacez le code de run.csx hello par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="07f4f-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="07f4f-219">Rendre les variables de hello tooreplace vraiment Bonjour précédant compte de stockage de code toopoint tooyour où sont écrits les journaux de coffre de clés hello, vous avez créé précédemment, le bus des services hello et hello des journaux de stockage de coffre de clés toohello chemin d’accès spécifique.</span><span class="sxs-lookup"><span data-stu-id="07f4f-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="07f4f-220">fonction Hello récupère hello du dernier fichier journal à partir du compte de stockage hello où hello coffre de clés sont écrits les journaux, extrait les événements les plus récents hello à partir de ce fichier, et les transmet la file d’attente du Bus des services tooa.</span><span class="sxs-lookup"><span data-stu-id="07f4f-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="07f4f-221">Dans la mesure où un seul fichier peut avoir plusieurs événements, vous devez créer un fichier de sync.txt fonction hello examine également horodatage toodetermine hello de hello du dernier événement qui a été récupéré.</span><span class="sxs-lookup"><span data-stu-id="07f4f-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="07f4f-222">Cela garantit que vous n’effectuez un push hello même événement plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="07f4f-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="07f4f-223">Ce fichier sync.txt contient un horodatage pour le dernier événement de rencontré hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="07f4f-224">les journaux, lors du chargement, Hello ont toobe trié selon tooensure d’horodatage hello qu’ils sont ordonnés correctement.</span><span class="sxs-lookup"><span data-stu-id="07f4f-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="07f4f-225">Pour cette fonction, nous faire référence à quelques bibliothèques supplémentaires qui ne sont pas disponibles en dehors de la zone hello dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="07f4f-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="07f4f-226">tooinclude, nous avons besoin de fonctions de Azure toopull les à l’aide de NuGet.</span><span class="sxs-lookup"><span data-stu-id="07f4f-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="07f4f-227">Choisissez hello **afficher les fichiers** option.</span><span class="sxs-lookup"><span data-stu-id="07f4f-227">Choose hello **View Files** option.</span></span>

![Option Afficher les fichiers](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="07f4f-229">Et ajoutez un fichier appelé project.json avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="07f4f-229">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="07f4f-230">Fonction **enregistrer**, les fonctions Azure téléchargera les fichiers binaires de hello requis.</span><span class="sxs-lookup"><span data-stu-id="07f4f-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="07f4f-231">Commutateur toohello **intégrer** onglet et donner de paramètre de minuteur hello un toouse nom explicite au sein de la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="07f4f-232">Bonjour précédant le code, il attend toobe de minuteur hello appelé *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="07f4f-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="07f4f-233">Spécifiez un [expression CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) comme suit : 0 \* \* \* \* \* de minuterie hello qui provoque hello fonction toorun une fois par minute.</span><span class="sxs-lookup"><span data-stu-id="07f4f-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="07f4f-234">Sur hello même **intégrer** onglet, ajouter une entrée de type de hello **stockage d’objets Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="07f4f-235">Cela pointe toohello sync.txt fichier qui contient l’horodatage de hello de hello du dernier événement de fonction hello consulté.</span><span class="sxs-lookup"><span data-stu-id="07f4f-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="07f4f-236">Ce sera disponible au sein de la fonction hello par nom de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="07f4f-237">Bonjour précédant le code, entrée de stockage d’objets Blob Azure hello attend toobe de nom de paramètre hello *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="07f4f-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="07f4f-238">Choisissez le compte de stockage hello où se trouve hello sync.txt fichier (il peut être hello même ou à un autre compte de stockage).</span><span class="sxs-lookup"><span data-stu-id="07f4f-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="07f4f-239">Dans le champ de chemin d’accès de hello, indiquez le chemin de hello où les fichiers hello résident dans le format hello {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="07f4f-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="07f4f-240">Ajouter une sortie de type de hello *stockage d’objets Blob Azure* sortie.</span><span class="sxs-lookup"><span data-stu-id="07f4f-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="07f4f-241">Ce fichier de sync.txt toohello que vous défini dans l’entrée de hello pointe.</span><span class="sxs-lookup"><span data-stu-id="07f4f-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="07f4f-242">Ceci est utilisé par hello fonction toowrite hello timestamp de hello du dernier événement étudié.</span><span class="sxs-lookup"><span data-stu-id="07f4f-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="07f4f-243">code précédent Hello attend ce toobe paramètre appelé *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="07f4f-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="07f4f-244">À ce stade, la fonction hello est prête.</span><span class="sxs-lookup"><span data-stu-id="07f4f-244">At this point, hello function is ready.</span></span> <span data-ttu-id="07f4f-245">Rendre toohello de retour que tooswitch **développer** onglet et enregistrer le code de hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="07f4f-246">Consultez la fenêtre de sortie hello pour les erreurs de compilation et corrigez-les en conséquence.</span><span class="sxs-lookup"><span data-stu-id="07f4f-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="07f4f-247">Si le code hello compilé, puis hello doit maintenant être la vérification du code hello coffre de clés journaux toutes les minutes et en exécutant un push de tous les nouveaux événements sur hello défini de file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="07f4f-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="07f4f-248">Vous devez voir les informations de journalisation écrivent les fenêtre du journal toohello chaque fois que la fonction de hello est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="07f4f-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="07f4f-249">Application logique Azure</span><span class="sxs-lookup"><span data-stu-id="07f4f-249">Azure logic app</span></span>
<span data-ttu-id="07f4f-250">Ensuite, vous devez créer une application Azure logique qui sélectionne les événements hello que fonction hello repousse file d’attente du Service Bus toohello, analyse le contenu de hello et envoie un message électronique selon une condition de correspondance.</span><span class="sxs-lookup"><span data-stu-id="07f4f-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="07f4f-251">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) en accédant trop**Nouveau > Application logique**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="07f4f-252">Une fois que l’application logique de hello est créée, accédez tooit et choisissez **modifier**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="07f4f-253">Dans l’éditeur de l’application hello logique, choisissez **file d’attente du Bus de Service** et entrez votre tooconnect d’informations d’identification de Service Bus il file d’attente toohello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Service Bus d’application logique Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="07f4f-255">Choisissez ensuite **Ajouter une condition**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="07f4f-256">Dans la condition de hello, basculez toohello éditeur avancé, puis entrez hello suivant de code, en remplaçant APP_ID par hello APP_ID réel de votre application web :</span><span class="sxs-lookup"><span data-stu-id="07f4f-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="07f4f-257">Cette expression retourne essentiellement **false** si hello *appid* de hello événement entrant (qui est le corps de hello du message d’appel du Service Bus) n’est pas hello *appid* Hello application.</span><span class="sxs-lookup"><span data-stu-id="07f4f-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="07f4f-258">Créez maintenant une action sous **Si non, ne rien faire**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-258">Now, create an action under **If no, do nothing**.</span></span>

![Choisir une action d’application logique Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="07f4f-260">Pour l’action de hello, choisissez **Office 365 - envoyer un e-mail**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="07f4f-261">Remplir hello champs toocreate un toosend par courrier électronique lorsque hello définie par la condition retourne **false**.</span><span class="sxs-lookup"><span data-stu-id="07f4f-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="07f4f-262">Si vous n’avez pas d’Office 365, vous pouvez examiner alternatives tooachieve hello les mêmes résultats.</span><span class="sxs-lookup"><span data-stu-id="07f4f-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="07f4f-263">À ce stade, vous disposez d’un pipeline tooend fin qui se présente pour les nouveaux journaux d’audit de coffre de clés, une fois par minute.</span><span class="sxs-lookup"><span data-stu-id="07f4f-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="07f4f-264">Il exécute un push de nouveaux journaux qu’il trouve la file d’attente de bus de service tooa.</span><span class="sxs-lookup"><span data-stu-id="07f4f-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="07f4f-265">application de la logique de Hello est déclenchée lorsqu’un nouveau message arrive dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="07f4f-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="07f4f-266">Si hello *appid* dans hello événement ne correspond pas à ID de l’application hello Hello appel d’application, il envoie un message électronique.</span><span class="sxs-lookup"><span data-stu-id="07f4f-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
