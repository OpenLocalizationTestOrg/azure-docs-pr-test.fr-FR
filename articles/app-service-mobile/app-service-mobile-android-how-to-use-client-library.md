---
title: "Comment utiliser le Kit de développement logiciel (SDK) Azure Mobile Apps pour Android | Microsoft Docs"
description: "Comment utiliser le Kit de développement logiciel (SDK) Azure Mobile Apps pour Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 4b15d024ca6d5bbafe83d321a64021aecd78c4a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="a12dc-103">Comment utiliser le Kit de développement logiciel (SDK) Azure Mobile Apps pour Android</span><span class="sxs-lookup"><span data-stu-id="a12dc-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="a12dc-104">Ce guide vous montre comment utiliser le Kit de développement logiciel (SDK) du client Android pour Mobile Apps afin d’implémenter des scénarios courants tels que :</span><span class="sxs-lookup"><span data-stu-id="a12dc-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="a12dc-105">Interrogation des données (insertion, mise à jour et suppression).</span><span class="sxs-lookup"><span data-stu-id="a12dc-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="a12dc-106">Authentification.</span><span class="sxs-lookup"><span data-stu-id="a12dc-106">Authentication.</span></span>
* <span data-ttu-id="a12dc-107">Gestion des erreurs.</span><span class="sxs-lookup"><span data-stu-id="a12dc-107">Handling errors.</span></span>
* <span data-ttu-id="a12dc-108">Personnalisation du client.</span><span class="sxs-lookup"><span data-stu-id="a12dc-108">Customizing the client.</span></span>

<span data-ttu-id="a12dc-109">Ce guide est axé sur le kit de développement logiciel Android côté client.</span><span class="sxs-lookup"><span data-stu-id="a12dc-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="a12dc-110">Pour plus d’informations sur les Kits de développement logiciel (SDK) côté serveur pour Mobile Apps, consultez les articles [Utiliser le Kit de développement logiciel (SDK) de serveur principal .NET pour Azure Mobile Apps][10] ou [Comment utiliser le Kit de développement logiciel Node.js dans Azure Mobile Apps][11].</span><span class="sxs-lookup"><span data-stu-id="a12dc-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="a12dc-111">Documentation de référence</span><span class="sxs-lookup"><span data-stu-id="a12dc-111">Reference Documentation</span></span>

<span data-ttu-id="a12dc-112">La [référence de l’API Javadocs][12] pour la bibliothèque cliente Android se trouve sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a12dc-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="a12dc-113">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="a12dc-113">Supported Platforms</span></span>

<span data-ttu-id="a12dc-114">Le Kit de développement logiciel (SDK) Azure Mobile Apps pour Android prend en charge les niveaux d’API compris entre 19 et 24 (de KitKat à Nougat) pour les facteurs de forme tablette et téléphone.</span><span class="sxs-lookup"><span data-stu-id="a12dc-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="a12dc-115">L’authentification utilise en particulier une approche courante d’infrastructure web pour recueillir des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="a12dc-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="a12dc-116">L’authentification de flux serveur ne fonctionne pas avec les appareils compacts comme les montres.</span><span class="sxs-lookup"><span data-stu-id="a12dc-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="a12dc-117">Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="a12dc-117">Setup and Prerequisites</span></span>

<span data-ttu-id="a12dc-118">Terminez le [didacticiel de démarrage rapide Mobile Apps](app-service-mobile-android-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="a12dc-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="a12dc-119">Cette tâche garantit que toutes les conditions préalables au développement d’Azure Mobile Apps ont été remplies.</span><span class="sxs-lookup"><span data-stu-id="a12dc-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="a12dc-120">Le didacticiel de démarrage rapide vous aide également à configurer et à créer votre premier backend Mobile App.</span><span class="sxs-lookup"><span data-stu-id="a12dc-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="a12dc-121">Si vous décidez de ne pas suivre le didacticiel de démarrage rapide, effectuez les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a12dc-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="a12dc-122">[créer un backend Mobile Apps][13] à utiliser avec votre application Android ;</span><span class="sxs-lookup"><span data-stu-id="a12dc-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="a12dc-123">dans Android Studio, [mettre à jour les fichiers de construction Gradle](#gradle-build);</span><span class="sxs-lookup"><span data-stu-id="a12dc-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="a12dc-124">[activer les autorisations Internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="a12dc-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="a12dc-125"><a name="gradle-build"></a>Mise à jour du fichier de construction Gradle</span><span class="sxs-lookup"><span data-stu-id="a12dc-125"><a name="gradle-build"></a>Update the Gradle build file</span></span>

<span data-ttu-id="a12dc-126">Modifiez les deux fichiers **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="a12dc-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="a12dc-127">ajoutez ce code au fichier de niveau *projet* **build.gradle** à l’intérieur de la balise *buildscript* :</span><span class="sxs-lookup"><span data-stu-id="a12dc-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="a12dc-128">Ajoutez ce code au fichier de niveau *Module app* **build.gradle** à l’intérieur de la balise *dependencies* :</span><span class="sxs-lookup"><span data-stu-id="a12dc-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="a12dc-129">La version la plus récente est la 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="a12dc-129">Currently the latest version is 3.3.0.</span></span> <span data-ttu-id="a12dc-130">Les versions prises en charge sont répertoriées [sur Bintray][14].</span><span class="sxs-lookup"><span data-stu-id="a12dc-130">The supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="a12dc-131"><a name="enable-internet"></a>activer les autorisations Internet.</span><span class="sxs-lookup"><span data-stu-id="a12dc-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="a12dc-132">Pour accéder à Azure, l’autorisation INTERNET doit être activée sur votre application.</span><span class="sxs-lookup"><span data-stu-id="a12dc-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="a12dc-133">Si ce n’est pas déjà fait, ajoutez la ligne de code suivante à votre fichier **AndroidManifest.xml** :</span><span class="sxs-lookup"><span data-stu-id="a12dc-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="a12dc-134">Créer une connexion cliente</span><span class="sxs-lookup"><span data-stu-id="a12dc-134">Create a Client Connection</span></span>

<span data-ttu-id="a12dc-135">Azure Mobile Apps propose quatre fonctions à votre application mobile :</span><span class="sxs-lookup"><span data-stu-id="a12dc-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="a12dc-136">Accès aux données et synchronisation hors connexion avec un service Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="a12dc-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="a12dc-137">Appel des API personnalisées écrites avec le Kit de développement logiciel (SDK) de serveur Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="a12dc-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="a12dc-138">Authentification avec l’authentification et l’autorisation Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a12dc-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="a12dc-139">Inscription de notifications Push avec Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="a12dc-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="a12dc-140">Pour chacune de ces fonctions, vous devez créer un objet `MobileServiceClient` au préalable.</span><span class="sxs-lookup"><span data-stu-id="a12dc-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="a12dc-141">Seul un objet `MobileServiceClient` doit être créé au sein de votre client mobile (autrement dit, il doit être un modèle de Singleton).</span><span class="sxs-lookup"><span data-stu-id="a12dc-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="a12dc-142">Pour créer un objet `MobileServiceClient` :</span><span class="sxs-lookup"><span data-stu-id="a12dc-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="a12dc-143">`<MobileAppUrl>` est soit une chaîne, soit un objet d’URL qui pointe vers votre serveur principal mobile.</span><span class="sxs-lookup"><span data-stu-id="a12dc-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="a12dc-144">Si vous utilisez Azure App Service pour héberger votre serveur principal mobile, veillez à utiliser la version `https://` sécurisée de l’URL.</span><span class="sxs-lookup"><span data-stu-id="a12dc-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="a12dc-145">Le client nécessite aussi un accès à l’activité ou au contexte (le paramètre `this` dans l’exemple).</span><span class="sxs-lookup"><span data-stu-id="a12dc-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="a12dc-146">La construction de MobileServiceClient doit se produire dans la méthode `onCreate()` de l’activité référencée dans le fichier `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="a12dc-147">Nous vous recommandons d’extraire la communication du serveur dans sa propre classe (modèle singleton).</span><span class="sxs-lookup"><span data-stu-id="a12dc-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="a12dc-148">Dans ce cas, vous devez transmettre l’activité dans le constructeur pour configurer correctement le service.</span><span class="sxs-lookup"><span data-stu-id="a12dc-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="a12dc-149">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a12dc-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="a12dc-150">Vous pouvez maintenant appeler `AzureServiceAdapter.Initialize(this);` dans la méthode `onCreate()` de votre activité principale.</span><span class="sxs-lookup"><span data-stu-id="a12dc-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="a12dc-151">Toutes les autres méthodes nécessitant un accès au client utilisent `AzureServiceAdapter.getInstance();` pour obtenir une référence à l’adaptateur de services.</span><span class="sxs-lookup"><span data-stu-id="a12dc-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="a12dc-152">Opérations de données</span><span class="sxs-lookup"><span data-stu-id="a12dc-152">Data Operations</span></span>

<span data-ttu-id="a12dc-153">L’objectif principal du Kit de développement logiciel (SDK) Azure Mobile Apps consiste à fournir l’accès aux données stockées dans SQL Azure sur le serveur principal de l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="a12dc-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="a12dc-154">Vous pouvez accéder à ces données à l’aide de classes fortement typées (recommandé) ou de requêtes non typées (déconseillé).</span><span class="sxs-lookup"><span data-stu-id="a12dc-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="a12dc-155">La majeure partie de cette section s’intéresse à l’utilisation des classes fortement typées.</span><span class="sxs-lookup"><span data-stu-id="a12dc-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="a12dc-156">Définir des classes de données client</span><span class="sxs-lookup"><span data-stu-id="a12dc-156">Define client data classes</span></span>

<span data-ttu-id="a12dc-157">Pour accéder aux données à partir des tables SQL Azure, définissez des classes de données client qui correspondent aux tables du backend Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="a12dc-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="a12dc-158">Les exemples de cette rubrique reposent sur une table nommée **MyDataTable**, qui contient les colonnes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a12dc-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="a12dc-159">id</span><span class="sxs-lookup"><span data-stu-id="a12dc-159">id</span></span>
* <span data-ttu-id="a12dc-160">text</span><span class="sxs-lookup"><span data-stu-id="a12dc-160">text</span></span>
* <span data-ttu-id="a12dc-161">terminé</span><span class="sxs-lookup"><span data-stu-id="a12dc-161">complete</span></span>

<span data-ttu-id="a12dc-162">L’objet côté client typé correspondant se trouve dans un fichier appelé **MyDataTable.java** :</span><span class="sxs-lookup"><span data-stu-id="a12dc-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="a12dc-163">Incluez des méthodes getter et setter pour chaque champ que vous ajoutez.</span><span class="sxs-lookup"><span data-stu-id="a12dc-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="a12dc-164">Si votre table SQL Azure contient davantage de colonnes, vous devez ajouter les champs correspondants à cette classe.</span><span class="sxs-lookup"><span data-stu-id="a12dc-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="a12dc-165">Pour exemple, si l’objet de transfert de données (DTO, data transfer object) comporte une colonne d’entiers Priority, vous pouvez ajouter ce champ, ainsi que ses méthodes getter et setter :</span><span class="sxs-lookup"><span data-stu-id="a12dc-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="a12dc-166">Pour savoir comment créer des tables supplémentaires dans votre backend Mobile Apps, consultez [Définir un contrôleur de table][15] (backend .NET) ou [Définir des tables à l’aide d’un schéma dynamique][16] (backend Node.js).</span><span class="sxs-lookup"><span data-stu-id="a12dc-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="a12dc-167">Une table de serveur principal Azure Mobile Apps définit cinq champs spéciaux, dont quatre sont disponibles pour les clients :</span><span class="sxs-lookup"><span data-stu-id="a12dc-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="a12dc-168">`String id` : l’ID global unique pour l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="a12dc-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="a12dc-169">Nous vous recommandons de faire de l’ID la représentation de chaîne d’un objet [UUID][17].</span><span class="sxs-lookup"><span data-stu-id="a12dc-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="a12dc-170">`DateTimeOffset updatedAt` : la date/l’heure de la dernière mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a12dc-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="a12dc-171">Le champ updatedAt est défini par le serveur et ne doit jamais être défini par votre code client.</span><span class="sxs-lookup"><span data-stu-id="a12dc-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="a12dc-172">`DateTimeOffset createdAt` : la date/l’heure de création de l’objet.</span><span class="sxs-lookup"><span data-stu-id="a12dc-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="a12dc-173">Le champ createdAt est défini par le serveur et ne doit jamais être défini par votre code client.</span><span class="sxs-lookup"><span data-stu-id="a12dc-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="a12dc-174">`byte[] version` : généralement représentée sous forme de chaîne, la version est également définie par le serveur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="a12dc-175">`boolean deleted` : indique que l’enregistrement a été supprimé mais pas encore vidé.</span><span class="sxs-lookup"><span data-stu-id="a12dc-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="a12dc-176">N’utilisez pas `deleted` en tant que propriété dans votre classe.</span><span class="sxs-lookup"><span data-stu-id="a12dc-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="a12dc-177">Le champ `id` est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="a12dc-177">The `id` field is required.</span></span>  <span data-ttu-id="a12dc-178">Les champs `updatedAt` et `version` sont utilisés pour la synchronisation hors connexion (pour la synchronisation incrémentielle et la résolution des conflits, respectivement).</span><span class="sxs-lookup"><span data-stu-id="a12dc-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="a12dc-179">Le champ `createdAt` est un champ de référence et n’est pas utilisé par le client.</span><span class="sxs-lookup"><span data-stu-id="a12dc-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="a12dc-180">Les noms sont des noms « à travers le câble » des propriétés et ne sont pas réglables.</span><span class="sxs-lookup"><span data-stu-id="a12dc-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="a12dc-181">Toutefois, vous pouvez créer un mappage entre votre objet et les noms « à travers le câble » à l’aide de la bibliothèque [gson][3].</span><span class="sxs-lookup"><span data-stu-id="a12dc-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="a12dc-182">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a12dc-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="a12dc-183">Créer une référence de table</span><span class="sxs-lookup"><span data-stu-id="a12dc-183">Create a Table Reference</span></span>

<span data-ttu-id="a12dc-184">Pour accéder à une table, vous devez d’abord créer un objet [MobileServiceTable][8] en appelant la méthode **getTable** sur le [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="a12dc-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="a12dc-185">Cette méthode comporte deux surcharges :</span><span class="sxs-lookup"><span data-stu-id="a12dc-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="a12dc-186">Dans le code suivant, **mClient** est une référence à votre objet MobileServiceClient.</span><span class="sxs-lookup"><span data-stu-id="a12dc-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="a12dc-187">La première surcharge est utilisée quand le nom de la classe et le nom de la table sont identiques. Elle est reprise dans le didacticiel de démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="a12dc-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="a12dc-188">La deuxième surcharge est utilisée quand le nom de la table est différent du nom de la classe : le premier paramètre correspond au nom de la table.</span><span class="sxs-lookup"><span data-stu-id="a12dc-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="a12dc-189"><a name="query"></a>Interroger une table de serveur principal</span><span class="sxs-lookup"><span data-stu-id="a12dc-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="a12dc-190">Commencez par obtenir une référence de table.</span><span class="sxs-lookup"><span data-stu-id="a12dc-190">First, obtain a table reference.</span></span>  <span data-ttu-id="a12dc-191">Ensuite, exécutez une requête sur la référence de table.</span><span class="sxs-lookup"><span data-stu-id="a12dc-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="a12dc-192">Une requête est une combinaison des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a12dc-192">A query is any combination of:</span></span>

* <span data-ttu-id="a12dc-193">Une [clause de filtre](#filtering) `.where()`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="a12dc-194">Une [clause de classement](#sorting) `.orderBy()`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="a12dc-195">Une [clause de sélection de champ](#selection) `.select()`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="a12dc-196">Un élément `.skip()` et `.top()` pour les [résultats paginés](#paging).</span><span class="sxs-lookup"><span data-stu-id="a12dc-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="a12dc-197">Les clauses doivent être présentées dans l’ordre indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a12dc-197">The clauses must be presented in the preceding order.</span></span>

### <span data-ttu-id="a12dc-198"><a name="filter"></a> Filtrage des résultats</span><span class="sxs-lookup"><span data-stu-id="a12dc-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="a12dc-199">La forme générale d’une requête est :</span><span class="sxs-lookup"><span data-stu-id="a12dc-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="a12dc-200">L’exemple précédent renvoie tous les résultats (jusqu’à la taille de page maximale définie par le serveur).</span><span class="sxs-lookup"><span data-stu-id="a12dc-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="a12dc-201">La méthode `.execute()` exécute la requête sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="a12dc-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="a12dc-202">La requête est convertie en une requête [OData v3][19] avant sa transmission au serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="a12dc-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="a12dc-203">À la réception, le serveur principal Mobile Apps convertit la requête en une instruction SQL avant de l’exécuter sur l’instance SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a12dc-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="a12dc-204">Étant donné que l’activité réseau prend du temps, la méthode `.execute()` renvoie un élément [`ListenableFuture<E>`][18].</span><span class="sxs-lookup"><span data-stu-id="a12dc-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="a12dc-205"><a name="filtering"></a>Filtrer les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="a12dc-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="a12dc-206">L’exécution de la requête suivante retourne tous les éléments de la table **ToDoItem** dont le paramètre **complete** est égal à **false**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="a12dc-207">**mToDoTable** est la référence à la table des services mobiles que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="a12dc-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="a12dc-208">Définissez un filtre en appelant la méthode **where** sur la référence de table.</span><span class="sxs-lookup"><span data-stu-id="a12dc-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="a12dc-209">La méthode **where** est suivie d’une méthode **field**, suivie d’une méthode qui spécifie le prédicat logique.</span><span class="sxs-lookup"><span data-stu-id="a12dc-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="a12dc-210">Méthodes de prédicat possibles : **eq** (égal à), **ne** (différent de), **gt** (supérieur à), **ge** (supérieur ou égal à), **lt** (inférieur à), **le** (inférieur ou égal à).</span><span class="sxs-lookup"><span data-stu-id="a12dc-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="a12dc-211">Ces méthodes vous permettent de comparer les champs de nombre et de chaîne à des valeurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="a12dc-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="a12dc-212">Vous pouvez activer des filtres sur les dates.</span><span class="sxs-lookup"><span data-stu-id="a12dc-212">You can filter on dates.</span></span> <span data-ttu-id="a12dc-213">Les méthodes suivantes vous permettent de comparer le champ de date complet ou des parties de la date : **year**, **month**, **day**, **hour**, **minute** et **second**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="a12dc-214">L’exemple suivant ajoute un filtre pour les éléments dont la date d’échéance *due date* est égale à 2013.</span><span class="sxs-lookup"><span data-stu-id="a12dc-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="a12dc-215">Les méthodes suivantes prennent en charge des filtres complexes sur les champs de chaîne : **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="a12dc-216">L’exemple suivant filtre les lignes de la table dans lesquelles la colonne *text* commence par « PRI0 ».</span><span class="sxs-lookup"><span data-stu-id="a12dc-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="a12dc-217">Les méthodes d’opérateur suivantes sont prises en charge sur les champs numériques : **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="a12dc-218">L’exemple suivant filtre les lignes de la table dans lesquelles la colonne **duration** est un nombre pair.</span><span class="sxs-lookup"><span data-stu-id="a12dc-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="a12dc-219">Vous pouvez combiner les prédicats avec les méthodes logiques **and**, **or** et **not**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="a12dc-220">L’exemple suivant combine deux des exemples précédents.</span><span class="sxs-lookup"><span data-stu-id="a12dc-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="a12dc-221">Regrouper et imbriquer des opérateurs logiques :</span><span class="sxs-lookup"><span data-stu-id="a12dc-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="a12dc-222">Pour obtenir plus de détails et des exemples de filtres, consultez la page [Exploring the richness of the Mobile Services Android client query model][20](Exploration de la richesse du modèle de requête client Android Mobile Services).</span><span class="sxs-lookup"><span data-stu-id="a12dc-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <span data-ttu-id="a12dc-223"><a name="sorting"></a>Trier les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="a12dc-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="a12dc-224">Le code qui suit renvoie tous les éléments de la table **ToDoItem** triés par ordre croissant sur le champ *text* .</span><span class="sxs-lookup"><span data-stu-id="a12dc-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="a12dc-225">*mToDoTable* est la référence à la table de back-end créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="a12dc-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="a12dc-226">Le premier paramètre de la méthode **orderBy** est une chaîne équivalente au nom du champ sur lequel effectuer le tri.</span><span class="sxs-lookup"><span data-stu-id="a12dc-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="a12dc-227">Le second paramètre utilise l’énumération **QueryOrder** pour spécifier si le tri doit être croissant ou décroissant.</span><span class="sxs-lookup"><span data-stu-id="a12dc-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="a12dc-228">Si vous filtrez avec la méthode ***where***, la méthode ***where*** doit être appelée avant la méthode ***orderBy***.</span><span class="sxs-lookup"><span data-stu-id="a12dc-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <span data-ttu-id="a12dc-229"><a name="selection"></a>Sélectionner des colonnes spécifiques</span><span class="sxs-lookup"><span data-stu-id="a12dc-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="a12dc-230">Le code qui suit illustre comment renvoyer tous les éléments d’une table **ToDoItems**, mais uniquement en affichant les champs **complete** et **text**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="a12dc-231">**mToDoTable** est la référence à la table de back-end créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="a12dc-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="a12dc-232">Les paramètres associés à la fonction select sont les noms de chaîne des colonnes de table à renvoyer.</span><span class="sxs-lookup"><span data-stu-id="a12dc-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="a12dc-233">La méthode **select** doit suivre des méthodes telles que **where** et **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="a12dc-234">Elle peut être suivie de méthodes de pagination telles que **skip** et **top**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="a12dc-235"><a name="paging"></a>Renvoyer les données de pages</span><span class="sxs-lookup"><span data-stu-id="a12dc-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="a12dc-236">Les données sont **TOUJOURS** renvoyées dans les pages.</span><span class="sxs-lookup"><span data-stu-id="a12dc-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="a12dc-237">Le nombre maximal d’enregistrements renvoyés est défini par le serveur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="a12dc-238">Si le client demande plus d’enregistrements, le serveur renvoie le nombre maximal d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a12dc-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="a12dc-239">Par défaut, la taille de page maximale sur le serveur est de 50 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a12dc-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="a12dc-240">Le premier exemple présente comment sélectionner les cinq premiers éléments d'une table.</span><span class="sxs-lookup"><span data-stu-id="a12dc-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="a12dc-241">Cette requête renvoie les éléments d’une table **ToDoItem**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="a12dc-242">**mToDoTable** est la référence à la table de back-end créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="a12dc-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="a12dc-243">Voici maintenant une requête qui ignore les cinq premiers éléments, puis renvoie les cinq suivants :</span><span class="sxs-lookup"><span data-stu-id="a12dc-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="a12dc-244">Si vous souhaitez obtenir tous les enregistrements dans une table, implémentez le code pour effectuer une itération sur toutes les pages :</span><span class="sxs-lookup"><span data-stu-id="a12dc-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="a12dc-245">Une demande pour tous les enregistrements à l’aide de cette méthode crée un minimum de deux demandes à destination du serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="a12dc-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="a12dc-246">Le choix de la taille de page appropriée est un équilibre entre l’utilisation de la mémoire pendant l’exécution de la demande, l’utilisation de la bande passante et le délai de réception de toutes les données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="a12dc-247">La valeur par défaut (50 enregistrements) convient à tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="a12dc-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="a12dc-248">Si vous travaillez exclusivement sur des appareils avec une grande capacité de mémoire, augmentez cette valeur jusqu’à 500.</span><span class="sxs-lookup"><span data-stu-id="a12dc-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="a12dc-249">Nous avons constaté que l’augmentation de la taille de page au-delà de 500 enregistrements engendre des retards inacceptables et d’importants problèmes de mémoire.</span><span class="sxs-lookup"><span data-stu-id="a12dc-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="a12dc-250"><a name="chaining"></a>Procédure de concaténation de méthodes de requête</span><span class="sxs-lookup"><span data-stu-id="a12dc-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="a12dc-251">Les méthodes utilisées dans les requêtes de tables de backend peuvent être concaténées.</span><span class="sxs-lookup"><span data-stu-id="a12dc-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="a12dc-252">La concaténation des méthodes de requêtes vous permet de sélectionner des colonnes spécifiques de lignes filtrées, qui sont triées et paginées.</span><span class="sxs-lookup"><span data-stu-id="a12dc-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="a12dc-253">Vous pouvez créer des filtres logiques complexes.</span><span class="sxs-lookup"><span data-stu-id="a12dc-253">You can create complex logical filters.</span></span>  <span data-ttu-id="a12dc-254">Chaque méthode de requête retourne un objet de requête.</span><span class="sxs-lookup"><span data-stu-id="a12dc-254">Each query method returns a Query object.</span></span> <span data-ttu-id="a12dc-255">Pour mettre fin à la série de méthodes et exécuter la requête, appelez la méthode **execute** .</span><span class="sxs-lookup"><span data-stu-id="a12dc-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="a12dc-256">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a12dc-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="a12dc-257">Les méthodes de requête concaténées doivent être classées comme suit :</span><span class="sxs-lookup"><span data-stu-id="a12dc-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="a12dc-258">Filtrage des méthodes (**where**).</span><span class="sxs-lookup"><span data-stu-id="a12dc-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="a12dc-259">Tri des méthodes (**orderBy**).</span><span class="sxs-lookup"><span data-stu-id="a12dc-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="a12dc-260">Sélection des méthodes (**select**).</span><span class="sxs-lookup"><span data-stu-id="a12dc-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="a12dc-261">pagination des méthodes (**skip** et **top**).</span><span class="sxs-lookup"><span data-stu-id="a12dc-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="a12dc-262"><a name="binding"></a>Lier des données à l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="a12dc-262"><a name="binding"></a>Bind data to the user interface</span></span>

<span data-ttu-id="a12dc-263">La liaison des données nécessite trois composants :</span><span class="sxs-lookup"><span data-stu-id="a12dc-263">Data binding involves three components:</span></span>

* <span data-ttu-id="a12dc-264">la source de données ;</span><span class="sxs-lookup"><span data-stu-id="a12dc-264">The data source</span></span>
* <span data-ttu-id="a12dc-265">la mise en page à l’écran ;</span><span class="sxs-lookup"><span data-stu-id="a12dc-265">The screen layout</span></span>
* <span data-ttu-id="a12dc-266">l’adaptateur qui lie ces deux éléments.</span><span class="sxs-lookup"><span data-stu-id="a12dc-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="a12dc-267">Dans notre exemple de code, nous renvoyons les données de la table SQL Azure Mobile Apps **ToDoItem** dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="a12dc-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="a12dc-268">Cette activité est un cas de figure très courant pour les applications de données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="a12dc-269">Les requêtes de base de données renvoient souvent une suite de lignes que le client récupère dans une liste ou un tableau.</span><span class="sxs-lookup"><span data-stu-id="a12dc-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="a12dc-270">Dans cet exemple, le tableau est la source des données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="a12dc-271">Ce code spécifie une mise en page à l'écran qui définit la façon dont les données sont affichées sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="a12dc-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="a12dc-272">Les deux sont liés par un adaptateur, qui, dans ce code, est une extension de la classe **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="a12dc-273"><a name="layout"></a>Définir la mise en page</span><span class="sxs-lookup"><span data-stu-id="a12dc-273"><a name="layout"></a>Define the Layout</span></span>

<span data-ttu-id="a12dc-274">La mise en page est définie par plusieurs éléments de code XML.</span><span class="sxs-lookup"><span data-stu-id="a12dc-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="a12dc-275">En nous basant sur une mise en page existante, le code qui suit représente la vue **ListView** que nous souhaitons remplir avec les données du serveur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="a12dc-276">Dans le code précédent, l'attribut *listitem* spécifie l'ID de la mise en page de chaque ligne dans la liste.</span><span class="sxs-lookup"><span data-stu-id="a12dc-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="a12dc-277">Ce code spécifie une case à cocher ainsi que le texte associé, et il est instancié une fois pour chaque élément dans la liste.</span><span class="sxs-lookup"><span data-stu-id="a12dc-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="a12dc-278">Cette mise en page n’affiche pas le champ **id** ; une mise en page plus complexe spécifierait d’autres champs dans l’affichage.</span><span class="sxs-lookup"><span data-stu-id="a12dc-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="a12dc-279">Le code se trouve dans le fichier **row_list_to_do.xml**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-279">This code is in the **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="a12dc-280"><a name="adapter"></a>Définir l’adaptateur</span><span class="sxs-lookup"><span data-stu-id="a12dc-280"><a name="adapter"></a>Define the adapter</span></span>
<span data-ttu-id="a12dc-281">Comme la source de données de notre vue est un tableau **ToDoItem**, nous créons une sous-classe de notre adaptateur à partir de la classe **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="a12dc-282">Cette sous-classe produit une vue pour chaque élément **ToDoItem** utilisant la mise en page **row_list_to_do**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="a12dc-283">Dans notre code, nous définissons la classe suivante, qui est une extension de la classe **ArrayAdapter&lt;E&gt;** :</span><span class="sxs-lookup"><span data-stu-id="a12dc-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="a12dc-284">Ignorez la méthode **getView** de l'adaptateur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="a12dc-285">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a12dc-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="a12dc-286">Nous créons une instance de cette classe dans notre activité, comme suit :</span><span class="sxs-lookup"><span data-stu-id="a12dc-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="a12dc-287">Le deuxième paramètre du constructeur ToDoItemAdapter est une référence à la mise en page.</span><span class="sxs-lookup"><span data-stu-id="a12dc-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="a12dc-288">Nous pouvons maintenant instancier l’élément **ListView** et attribuer l’adaptateur à **ListView**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="a12dc-289"><a name="use-adapter"></a>Utiliser l’adaptateur pour effectuer la liaison à l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="a12dc-289"><a name="use-adapter"></a>Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="a12dc-290">Vous êtes désormais prêt à utiliser la liaison des données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-290">You are now ready to use data binding.</span></span> <span data-ttu-id="a12dc-291">Le code suivant montre comment obtenir les éléments du tableau et remplit l’adaptateur local en utilisant les éléments renvoyés.</span><span class="sxs-lookup"><span data-stu-id="a12dc-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="a12dc-292">Appelez l’adaptateur chaque fois que vous modifiez le tableau **ToDoItem** .</span><span class="sxs-lookup"><span data-stu-id="a12dc-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="a12dc-293">Comme les modifications se font enregistrement par enregistrement, vous ne gérez qu’une seule ligne, et non une collection.</span><span class="sxs-lookup"><span data-stu-id="a12dc-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="a12dc-294">Lorsque vous insérez un élément, appelez la méthode **add** de l'adaptateur. Et lorsque vous supprimez un élément, appelez la méthode **remove**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="a12dc-295">Vous trouverez un exemple complet dans le [projet de démarrage rapide Android][21].</span><span class="sxs-lookup"><span data-stu-id="a12dc-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="a12dc-296"><a name="inserting"></a>Insérer des données dans le serveur principal</span><span class="sxs-lookup"><span data-stu-id="a12dc-296"><a name="inserting"></a>Insert data into the backend</span></span>

<span data-ttu-id="a12dc-297">Créez une instance de la classe *ToDoItem* et définissez ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="a12dc-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="a12dc-298">Utilisez ensuite **insert()** pour insérer un objet :</span><span class="sxs-lookup"><span data-stu-id="a12dc-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="a12dc-299">L’entité renvoyée correspond aux données insérées dans la table du serveur principal, incluant l’ID et toutes les autres valeurs (telles que les champs `createdAt`, `updatedAt` et `version`) définies sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="a12dc-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="a12dc-300">Les tables Mobile Apps nécessitent une colonne de clé primaire nommée **id**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-300">Mobile Apps tables require a primary key column named **id**.</span></span> <span data-ttu-id="a12dc-301">Cette colonne doit être une chaîne.</span><span class="sxs-lookup"><span data-stu-id="a12dc-301">This column must be a string.</span></span> <span data-ttu-id="a12dc-302">La valeur par défaut de la colonne ID est un GUID.</span><span class="sxs-lookup"><span data-stu-id="a12dc-302">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="a12dc-303">Vous pouvez fournir d’autres valeurs uniques, telles que des adresses de messagerie ou des noms d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a12dc-303">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="a12dc-304">Lorsqu’aucune valeur d’ID de chaîne n’est fournie pour un enregistrement inséré, le backend génère une nouvelle valeur GUID.</span><span class="sxs-lookup"><span data-stu-id="a12dc-304">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="a12dc-305">Les valeurs d’ID de chaîne offrent les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a12dc-305">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="a12dc-306">Les ID peuvent être générés sans effectuer d’aller-retour vers la base de données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-306">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="a12dc-307">Il est plus facile de fusionner des enregistrements de plusieurs tables ou bases de données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-307">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="a12dc-308">Les valeurs d’ID s’intègrent mieux à la logique d’une application.</span><span class="sxs-lookup"><span data-stu-id="a12dc-308">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="a12dc-309">Les valeurs d’ID de chaîne sont **obligatoires** pour la prise en charge de la synchronisation hors connexion.</span><span class="sxs-lookup"><span data-stu-id="a12dc-309">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="a12dc-310">Vous ne pouvez pas modifier un ID une fois stocké dans la base de données principale.</span><span class="sxs-lookup"><span data-stu-id="a12dc-310">You cannot change an Id once it is stored in the backend database.</span></span>

## <span data-ttu-id="a12dc-311"><a name="updating"></a>Mettre à jour des données dans une application mobile</span><span class="sxs-lookup"><span data-stu-id="a12dc-311"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="a12dc-312">Pour mettre à jour les données d’une table, transmettez le nouvel objet à la méthode **update()** .</span><span class="sxs-lookup"><span data-stu-id="a12dc-312">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="a12dc-313">Dans cet exemple, *l’élément* est une référence à une ligne dans la table *ToDoItem*, qui a été modifiée.</span><span class="sxs-lookup"><span data-stu-id="a12dc-313">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="a12dc-314">La ligne avec le même **id** est mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a12dc-314">The row with the same **id** is updated.</span></span>

## <span data-ttu-id="a12dc-315"><a name="deleting"></a>Supprimer des données dans une application mobile</span><span class="sxs-lookup"><span data-stu-id="a12dc-315"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="a12dc-316">Le code suivant montre comment supprimer les données d’une table en spécifiant l’objet de données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-316">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="a12dc-317">Vous pouvez également supprimer un élément en spécifiant le champ **id** de la ligne à supprimer.</span><span class="sxs-lookup"><span data-stu-id="a12dc-317">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="a12dc-318"><a name="lookup"></a>Rechercher un élément spécifique par ID</span><span class="sxs-lookup"><span data-stu-id="a12dc-318"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="a12dc-319">Recherchez un élément avec un champ **id** spécifique avec la méthode **lookUp()** :</span><span class="sxs-lookup"><span data-stu-id="a12dc-319">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="a12dc-320"><a name="untyped"></a>Procédure : utilisation de données non typées</span><span class="sxs-lookup"><span data-stu-id="a12dc-320"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="a12dc-321">Le modèle de programmation non typé vous offre un contrôle total de la sérialisation JSON.</span><span class="sxs-lookup"><span data-stu-id="a12dc-321">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="a12dc-322">Il existe certains scénarios courants où vous pouvez utiliser un modèle de programmation non typé.</span><span class="sxs-lookup"><span data-stu-id="a12dc-322">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="a12dc-323">Par exemple, si la table de votre backend contient un grand nombre de colonnes et que vous n’avez besoin de faire référence qu’à quelques-unes d’entre elles.</span><span class="sxs-lookup"><span data-stu-id="a12dc-323">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="a12dc-324">Avec le modèle typé, vous devez définir toutes les colonnes du serveur principal Mobile Apps dans votre classe de données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-324">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="a12dc-325">La plupart des appels d'API permettant d'accéder aux données sont similaires à ceux des appels de programmation typés.</span><span class="sxs-lookup"><span data-stu-id="a12dc-325">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="a12dc-326">La principale différence est que, dans le modèle non typé, vous appelez des méthodes dans l'objet **MobileServiceJsonTable** plutôt que dans l'objet **MobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-326">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <span data-ttu-id="a12dc-327"><a name="json_instance"></a>Créer une instance de table non typée</span><span class="sxs-lookup"><span data-stu-id="a12dc-327"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="a12dc-328">Comme pour le modèle typé, vous commencez par obtenir une référence de table, mais il s'agit dans ce cas d'un objet **MobileServicesJsonTable** .</span><span class="sxs-lookup"><span data-stu-id="a12dc-328">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="a12dc-329">Obtenez la référence en appelant la méthode **getTable** sur une instance du client :</span><span class="sxs-lookup"><span data-stu-id="a12dc-329">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="a12dc-330">Une fois que vous avez créé une instance de l’objet **MobileServiceJsonTable**, celui-ci a pratiquement la même API disponible qu’avec le modèle de programmation typé.</span><span class="sxs-lookup"><span data-stu-id="a12dc-330">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="a12dc-331">Dans certains cas, les méthodes utilisent un paramètre non typé au lieu d’un paramètre typé.</span><span class="sxs-lookup"><span data-stu-id="a12dc-331">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="a12dc-332"><a name="json_insert"></a>Insérer une table non typée</span><span class="sxs-lookup"><span data-stu-id="a12dc-332"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="a12dc-333">Le code suivant vous explique comment effectuer une insertion.</span><span class="sxs-lookup"><span data-stu-id="a12dc-333">The following code shows how to do an insert.</span></span> <span data-ttu-id="a12dc-334">La première étape consiste à créer un objet [JsonObject][1], qui fait partie de la bibliothèque [gson][3].</span><span class="sxs-lookup"><span data-stu-id="a12dc-334">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="a12dc-335">Ensuite, utilisez **insert()** pour insérer l’objet non typé dans la table.</span><span class="sxs-lookup"><span data-stu-id="a12dc-335">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="a12dc-336">Si vous avez besoin d’obtenir l’ID de l’objet inséré, utilisez la méthode **getAsJsonPrimitive()** .</span><span class="sxs-lookup"><span data-stu-id="a12dc-336">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="a12dc-337"><a name="json_delete"></a>Supprimer d’une table non typée</span><span class="sxs-lookup"><span data-stu-id="a12dc-337"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="a12dc-338">Le code qui suit montre comment supprimer une instance, dans ce cas la même instance de l'objet **JsonObject** créé dans l'exemple *insert* précédent.</span><span class="sxs-lookup"><span data-stu-id="a12dc-338">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="a12dc-339">Le code est identique à la casse typée, mais la méthode a une signature différente puisqu’elle fait référence à un objet **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-339">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="a12dc-340">Vous pouvez aussi directement supprimer une instance avec son ID :</span><span class="sxs-lookup"><span data-stu-id="a12dc-340">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="a12dc-341"><a name="json_get"></a>Renvoyer toutes les lignes d’une table non typée</span><span class="sxs-lookup"><span data-stu-id="a12dc-341"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="a12dc-342">Le code suivant montre comment récupérer toute une table.</span><span class="sxs-lookup"><span data-stu-id="a12dc-342">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="a12dc-343">Étant donné que vous utilisez un tableau JSON, vous pouvez extraire uniquement certaines colonnes de la table, de manière sélective.</span><span class="sxs-lookup"><span data-stu-id="a12dc-343">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="a12dc-344">Les mêmes méthodes de filtrage et de pagination disponibles pour le modèle typé le sont également pour le modèle non typé.</span><span class="sxs-lookup"><span data-stu-id="a12dc-344">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <span data-ttu-id="a12dc-345"><a name="offline-sync"></a>Implémenter la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="a12dc-345"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="a12dc-346">Le Kit de développement logiciel (SDK) Azure Mobile Apps Client implémente également la synchronisation hors connexion des données à l’aide d’une base de données SQLite pour stocker une copie des données du serveur en local.</span><span class="sxs-lookup"><span data-stu-id="a12dc-346">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="a12dc-347">Les opérations effectuées sur une table en mode hors connexion ne nécessitent pas de connectivité mobile pour fonctionner.</span><span class="sxs-lookup"><span data-stu-id="a12dc-347">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="a12dc-348">La synchronisation hors connexion contribue à la résilience et aux performances au détriment d’une logique plus complexe pour la résolution des conflits.</span><span class="sxs-lookup"><span data-stu-id="a12dc-348">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="a12dc-349">Le Kit de développement logiciel (SDK) Azure Mobile Apps Client implémente les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="a12dc-349">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="a12dc-350">Synchronisation incrémentielle : seuls les enregistrements nouveaux et mis à jour sont téléchargés, ce qui permet d’économiser de la bande passante et de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="a12dc-350">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="a12dc-351">Accès concurrentiel optimiste : les opérations sont supposées réussir.</span><span class="sxs-lookup"><span data-stu-id="a12dc-351">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="a12dc-352">La résolution des conflits est différée jusqu’à ce que des mises à jour soient effectuées sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-352">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="a12dc-353">Résolution des conflits : le Kit de développement logiciel (SDK) détecte les modifications conflictuelles ayant été apportées au niveau du serveur et fournit des hooks pour avertir l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-353">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="a12dc-354">Suppression réversible : les enregistrements supprimés sont marqués comme supprimés, ce qui permet à d’autres appareils de mettre à jour leur cache hors connexion.</span><span class="sxs-lookup"><span data-stu-id="a12dc-354">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="a12dc-355">Initialiser la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="a12dc-355">Initialize Offline Sync</span></span>

<span data-ttu-id="a12dc-356">Chaque table hors connexion doit être définie dans le cache hors connexion avant toute utilisation.</span><span class="sxs-lookup"><span data-stu-id="a12dc-356">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="a12dc-357">En règle générale, la définition de table s’effectue immédiatement après la création du client :</span><span class="sxs-lookup"><span data-stu-id="a12dc-357">Normally, table definition is done immediately after the creation of the client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="a12dc-358">Obtenir une référence à la table de cache hors connexion</span><span class="sxs-lookup"><span data-stu-id="a12dc-358">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="a12dc-359">Pour une table en ligne, vous utilisez `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-359">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="a12dc-360">Pour une table hors connexion, utilisez `.getSyncTable()` :</span><span class="sxs-lookup"><span data-stu-id="a12dc-360">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="a12dc-361">Toutes les méthodes disponibles pour les tables en ligne (y compris le filtrage, le tri, la pagination, l’insertion de données, la mise à jour de données et la suppression de données) fonctionnent de la même façon sur les tables hors connexion.</span><span class="sxs-lookup"><span data-stu-id="a12dc-361">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="a12dc-362">Synchroniser le cache hors connexion local</span><span class="sxs-lookup"><span data-stu-id="a12dc-362">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="a12dc-363">La synchronisation est sous le contrôle de votre application.</span><span class="sxs-lookup"><span data-stu-id="a12dc-363">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="a12dc-364">Voici un exemple de méthode de synchronisation :</span><span class="sxs-lookup"><span data-stu-id="a12dc-364">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="a12dc-365">Si un nom de requête est fourni à la méthode `.pull(query, queryname)`, la synchronisation incrémentielle est utilisée pour renvoyer uniquement les enregistrements qui ont été créés ou modifiés depuis la dernière extraction complète.</span><span class="sxs-lookup"><span data-stu-id="a12dc-365">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="a12dc-366">Gérer les conflits lors de la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="a12dc-366">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="a12dc-367">Si un conflit se produit pendant une opération `.push()`, une exception `MobileServiceConflictException` est levée.</span><span class="sxs-lookup"><span data-stu-id="a12dc-367">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="a12dc-368">L’élément émis par le serveur est intégré à l’exception et peut être récupéré par `.getItem()` sur l’exception.</span><span class="sxs-lookup"><span data-stu-id="a12dc-368">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="a12dc-369">Ajustez l’opération push en appelant les éléments suivants sur l’objet MobileServiceSyncContext :</span><span class="sxs-lookup"><span data-stu-id="a12dc-369">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="a12dc-370">Une fois tous les conflits marqués comme vous le souhaitez, appelez `.push()` pour résoudre tous les conflits.</span><span class="sxs-lookup"><span data-stu-id="a12dc-370">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <span data-ttu-id="a12dc-371"><a name="custom-api"></a>Appeler une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="a12dc-371"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="a12dc-372">Une API personnalisée vous permet de définir des points de terminaison exposant une fonctionnalité de serveur qui ne mappe pas vers une opération d'insertion, de mise à jour, de suppression ou de lecture.</span><span class="sxs-lookup"><span data-stu-id="a12dc-372">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="a12dc-373">En utilisant une API personnalisée, vous pouvez exercer davantage de contrôle sur la messagerie, notamment lire et définir des en-têtes de message HTTP et définir un format de corps de message autre que JSON.</span><span class="sxs-lookup"><span data-stu-id="a12dc-373">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="a12dc-374">À partir d’un client Android, vous appelez la méthode **invokeApi** pour appeler le point de terminaison de l’API personnalisée.</span><span class="sxs-lookup"><span data-stu-id="a12dc-374">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="a12dc-375">L’exemple suivant montre comment appeler un point de terminaison d’API nommé **completeAll**, qui retourne une classe de collection nommée **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-375">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="a12dc-376">La méthode **invokeApi** est appelée sur le client pour envoyer une requête POST à la nouvelle API personnalisée.</span><span class="sxs-lookup"><span data-stu-id="a12dc-376">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="a12dc-377">Le résultat renvoyé par l'API personnalisée apparaît dans la boîte de message, avec les erreurs éventuelles.</span><span class="sxs-lookup"><span data-stu-id="a12dc-377">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="a12dc-378">Les autres versions de la méthode **invokeApi** vous permettent éventuellement d’envoyer un objet dans le corps de la demande, de spécifier la méthode HTTP et d’envoyer des paramètres de requête avec la demande.</span><span class="sxs-lookup"><span data-stu-id="a12dc-378">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="a12dc-379">Des versions non typées de la méthode **invokeApi** sont également fournies.</span><span class="sxs-lookup"><span data-stu-id="a12dc-379">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="a12dc-380"><a name="authentication"></a>Ajouter l’authentification à votre application</span><span class="sxs-lookup"><span data-stu-id="a12dc-380"><a name="authentication"></a>Add authentication to your app</span></span>

<span data-ttu-id="a12dc-381">Les didacticiels décrivent déjà en détail l’ajout de ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="a12dc-381">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="a12dc-382">App Service prend en charge [l’authentification des utilisateurs d’applications](app-service-mobile-android-get-started-users.md) via divers fournisseurs d’identité externes : Facebook, Google, compte Microsoft, Twitter et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a12dc-382">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="a12dc-383">Vous pouvez définir des autorisations sur les tables pour limiter l'accès à certaines opérations aux seuls utilisateurs authentifiés.</span><span class="sxs-lookup"><span data-stu-id="a12dc-383">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="a12dc-384">Vous pouvez également utiliser l’identité des utilisateurs authentifiés pour implémenter des règles d’autorisation dans votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="a12dc-384">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="a12dc-385">Deux flux d’authentification sont pris en charge : un flux **serveur** et un flux **client**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-385">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="a12dc-386">Le flux serveur fournit l'authentification la plus simple, car il repose sur l'interface Web des fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="a12dc-386">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="a12dc-387">Aucun SDK supplémentaires n’est requis pour implémenter l’authentification de flux serveur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-387">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="a12dc-388">L’authentification de flux serveur ne fournit pas une intégration approfondie dans l’appareil mobile et elle est uniquement recommandée dans des scénarios de preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="a12dc-388">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="a12dc-389">Le flux client permet une intégration approfondie avec les fonctionnalités propres aux appareils, telles que l'authentification unique, car il repose sur des Kits de développement logiciel (SDK) proposés par le fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="a12dc-389">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="a12dc-390">Par exemple, vous pouvez intégrer le SDK Facebook dans votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="a12dc-390">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="a12dc-391">Le client mobile permute dans l’application Facebook et confirme votre ouverture de session avant de rebasculer vers votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="a12dc-391">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="a12dc-392">Quatre étapes sont nécessaires pour activer l'authentification dans votre application :</span><span class="sxs-lookup"><span data-stu-id="a12dc-392">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="a12dc-393">inscription de votre application pour l’authentification auprès d’un fournisseur d’identité ;</span><span class="sxs-lookup"><span data-stu-id="a12dc-393">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="a12dc-394">configuration de votre backend App Service ;</span><span class="sxs-lookup"><span data-stu-id="a12dc-394">Configure your App Service backend.</span></span>
* <span data-ttu-id="a12dc-395">restriction des autorisations de table aux utilisateurs authentifiés uniquement sur le backend App Service ;</span><span class="sxs-lookup"><span data-stu-id="a12dc-395">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="a12dc-396">ajout de code d’authentification à votre application.</span><span class="sxs-lookup"><span data-stu-id="a12dc-396">Add authentication code to your app.</span></span>

<span data-ttu-id="a12dc-397">Vous pouvez définir des autorisations sur les tables pour limiter l'accès à certaines opérations aux seuls utilisateurs authentifiés.</span><span class="sxs-lookup"><span data-stu-id="a12dc-397">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="a12dc-398">Vous pouvez également utiliser le SID d’un utilisateur authentifié pour modifier des demandes.</span><span class="sxs-lookup"><span data-stu-id="a12dc-398">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="a12dc-399">Pour plus d’informations, consultez la rubrique [Prise en main de l’authentification] et les instructions pour le Kit de développement logiciel (SDK) Server.</span><span class="sxs-lookup"><span data-stu-id="a12dc-399">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="a12dc-400"><a name="caching"></a>Authentification : flux serveur</span><span class="sxs-lookup"><span data-stu-id="a12dc-400"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="a12dc-401">Le code suivant démarre un processus de connexion du flux serveur à l’aide du fournisseur Google.</span><span class="sxs-lookup"><span data-stu-id="a12dc-401">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="a12dc-402">Une configuration supplémentaire est nécessaire en raison des exigences de sécurité pour le fournisseur Google :</span><span class="sxs-lookup"><span data-stu-id="a12dc-402">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="a12dc-403">En outre, ajoutez la méthode suivante à la classe d’activité principale :</span><span class="sxs-lookup"><span data-stu-id="a12dc-403">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="a12dc-404">L’élément `GOOGLE_LOGIN_REQUEST_CODE` défini dans votre activité principale est utilisé pour la méthode `login()` et dans la méthode `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-404">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="a12dc-405">Vous pouvez choisir n’importe quel nombre unique, tant que le même nombre est utilisé dans les méthodes `login()` et `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-405">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="a12dc-406">Si vous extrayez le code client dans un adaptateur de services (comme indiqué précédemment), vous devez appeler les méthodes appropriées sur l’adaptateur de services.</span><span class="sxs-lookup"><span data-stu-id="a12dc-406">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="a12dc-407">Vous devez également configurer le projet pour customtabs.</span><span class="sxs-lookup"><span data-stu-id="a12dc-407">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="a12dc-408">Commencez par spécifier une URL de redirection.</span><span class="sxs-lookup"><span data-stu-id="a12dc-408">First specify a redirect-URL.</span></span>  <span data-ttu-id="a12dc-409">Ajoutez l’extrait de code suivant à `AndroidManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="a12dc-409">Add the following snippet to `AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="a12dc-410">Ajoutez **redirectUriScheme** au fichier `build.gradle` de votre application :</span><span class="sxs-lookup"><span data-stu-id="a12dc-410">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="a12dc-411">Enfin, ajoutez `com.android.support:customtabs:23.0.1` à la liste des dépendances dans le fichier `build.gradle` :</span><span class="sxs-lookup"><span data-stu-id="a12dc-411">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="a12dc-412">Obtenez l’ID de l’utilisateur connecté à partir d’un **MobileServiceUser** à l’aide de la méthode **getUserId**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-412">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="a12dc-413">Pour obtenir un exemple de la manière d’utiliser Futures pour appeler les API de connexion asynchrones, consultez la rubrique [Prise en main de l’authentification].</span><span class="sxs-lookup"><span data-stu-id="a12dc-413">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="a12dc-414">Le schéma d’URL mentionné respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="a12dc-414">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="a12dc-415">Assurez-vous que toutes les occurrences de `{url_scheme_of_you_app}` respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="a12dc-415">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="a12dc-416"><a name="caching"></a>Mettre en cache des jetons d’authentification</span><span class="sxs-lookup"><span data-stu-id="a12dc-416"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="a12dc-417">Pour cela, vous devez stocker localement l'ID utilisateur et le jeton d'authentification sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="a12dc-417">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="a12dc-418">Au prochain démarrage de l'application, vous vérifiez le cache, et si ces valeurs sont présentes, vous pouvez ignorer la procédure d'ouverture de session et rafraîchir le client avec ces données.</span><span class="sxs-lookup"><span data-stu-id="a12dc-418">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="a12dc-419">Mais ces données sont sensibles et elles doivent être stockées sous forme chiffrée au cas où le téléphone serait volé.</span><span class="sxs-lookup"><span data-stu-id="a12dc-419">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="a12dc-420">Vous pouvez obtenir un exemple complet illustrant la mise en cache des jetons d’authentification dans la section [Mise en cache de jetons d’authentification][7].</span><span class="sxs-lookup"><span data-stu-id="a12dc-420">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="a12dc-421">Lorsque vous tentez d’utiliser un jeton qui a expiré, vous recevez un message *401 - Connexion non autorisée* .</span><span class="sxs-lookup"><span data-stu-id="a12dc-421">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="a12dc-422">Vous pouvez gérer les erreurs d’authentification à l’aide de filtres.</span><span class="sxs-lookup"><span data-stu-id="a12dc-422">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="a12dc-423">Les filtres interceptent les requêtes adressées au backend App Service.</span><span class="sxs-lookup"><span data-stu-id="a12dc-423">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="a12dc-424">Le code de filtre teste la réponse pour une erreur 401, déclenche le processus de connexion, puis reprend la demande qui a généré l’erreur 401.</span><span class="sxs-lookup"><span data-stu-id="a12dc-424">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <span data-ttu-id="a12dc-425"><a name="refresh"></a>Utiliser des jetons d’actualisation</span><span class="sxs-lookup"><span data-stu-id="a12dc-425"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="a12dc-426">Le jeton renvoyé par l’authentification et l’autorisation Azure App Service a une durée de vie définie d’une heure.</span><span class="sxs-lookup"><span data-stu-id="a12dc-426">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="a12dc-427">Passé ce délai, vous devez de nouveau authentifier l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-427">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="a12dc-428">Si vous utilisez un jeton de longue durée reçu via l’authentification de flux client, vous pouvez procéder à la nouvelle authentification avec l’authentification et l’autorisation Azure App Service à l’aide du même jeton.</span><span class="sxs-lookup"><span data-stu-id="a12dc-428">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="a12dc-429">Un autre jeton Azure App Service est généré avec une nouvelle durée de vie.</span><span class="sxs-lookup"><span data-stu-id="a12dc-429">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="a12dc-430">Vous pouvez également inscrire le fournisseur pour qu’il utilise des jetons d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="a12dc-430">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="a12dc-431">Un jeton d’actualisation n’est pas toujours disponible.</span><span class="sxs-lookup"><span data-stu-id="a12dc-431">A Refresh Token is not always available.</span></span>  <span data-ttu-id="a12dc-432">Une configuration supplémentaire est nécessaire :</span><span class="sxs-lookup"><span data-stu-id="a12dc-432">Additional configuration is required:</span></span>

* <span data-ttu-id="a12dc-433">Pour **Azure Active Directory**, configurez une clé secrète client pour l’application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a12dc-433">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="a12dc-434">Spécifiez la clé secrète client dans Azure App Service lors de la configuration de l’authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a12dc-434">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="a12dc-435">Lorsque vous appelez `.login()`, transmettez `response_type=code id_token` en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="a12dc-435">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="a12dc-436">Pour **Google**, transmettez `access_type=offline` en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="a12dc-436">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="a12dc-437">Pour un **compte Microsoft**, sélectionnez la portée `wl.offline_access`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-437">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="a12dc-438">Pour actualiser un jeton, appelez `.refreshUser()` :</span><span class="sxs-lookup"><span data-stu-id="a12dc-438">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="a12dc-439">Nous vous recommandons de créer un filtre qui détecte une réponse 401 à partir du serveur et tente d’actualiser le jeton utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a12dc-439">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="a12dc-440">Se connecter avec l’authentification de flux client</span><span class="sxs-lookup"><span data-stu-id="a12dc-440">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="a12dc-441">Le processus général de connexion avec l’authentification de flux client se déroule comme suit :</span><span class="sxs-lookup"><span data-stu-id="a12dc-441">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="a12dc-442">Configurez l’authentification et l’autorisation Azure App Service comme vous le feriez pour l’authentification de flux client.</span><span class="sxs-lookup"><span data-stu-id="a12dc-442">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="a12dc-443">Intégrez le Kit de développement logiciel (SDK) du fournisseur d’authentification pour que l’authentification puisse générer un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="a12dc-443">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="a12dc-444">Appelez la méthode `.login()` comme suit :</span><span class="sxs-lookup"><span data-stu-id="a12dc-444">Call the `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="a12dc-445">Remplacez la méthode `onSuccess()` par le code que vous souhaitez utiliser sur une connexion réussie.</span><span class="sxs-lookup"><span data-stu-id="a12dc-445">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="a12dc-446">La chaîne `{provider}` est un fournisseur valide : **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount** ou **twitter**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-446">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="a12dc-447">Si vous avez implémenté l’authentification personnalisée, vous pouvez également utiliser la balise de fournisseur d’authentification personnalisée.</span><span class="sxs-lookup"><span data-stu-id="a12dc-447">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <span data-ttu-id="a12dc-448"><a name="adal"></a>Authentifier des utilisateurs avec la bibliothèque ADAL (Active Directory Authentication Library)</span><span class="sxs-lookup"><span data-stu-id="a12dc-448"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="a12dc-449">Vous pouvez utiliser la bibliothèque d’authentification Active Directory (ADAL) pour authentifier des utilisateurs dans votre application à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a12dc-449">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="a12dc-450">L’utilisation d’une connexion par flux de client est souvent préférable à l’utilisation des méthodes `loginAsync()` , car elle offre une interface UX native plus simple et permet une personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a12dc-450">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="a12dc-451">Si vous souhaitez configurer le serveur d’applications mobiles back-end pour utiliser la connexion AAD, suivez le didacticiel [Configurer votre application App Service pour utiliser la connexion Azure Active Directory][22].</span><span class="sxs-lookup"><span data-stu-id="a12dc-451">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="a12dc-452">Bien que cette étape soit facultative, veillez à inscrire une application cliente native.</span><span class="sxs-lookup"><span data-stu-id="a12dc-452">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="a12dc-453">Installez la bibliothèque ADAL en modifiant votre fichier build.gradle pour inclure les définitions suivantes :</span><span class="sxs-lookup"><span data-stu-id="a12dc-453">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="a12dc-454">Ajoutez le code suivant à votre application, en procédant aux remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="a12dc-454">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="a12dc-455">Remplacez **INSERT-AUTHORITY-HERE** par le nom du client dans lequel vous avez approvisionné votre application.</span><span class="sxs-lookup"><span data-stu-id="a12dc-455">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="a12dc-456">Le format doit être https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="a12dc-456">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="a12dc-457">Remplacez **INSERT-RESOURCE-ID-HERE** par l’ID client du serveur principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="a12dc-457">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="a12dc-458">Vous pouvez obtenir l’ID client sur le portail, sous l’onglet **Avancé** du menu **Paramètres Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-458">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="a12dc-459">Remplacez **INSERT-CLIENT-ID-HERE** par l’ID client que vous avez copié depuis l’application cliente native.</span><span class="sxs-lookup"><span data-stu-id="a12dc-459">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="a12dc-460">Remplacez **INSERT-REDIRECT-URI-HERE** par le point de terminaison */.auth/login/done* de votre site, en utilisant le modèle HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a12dc-460">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="a12dc-461">Cette valeur doit être semblable à *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="a12dc-461">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="a12dc-462"><a name="filters"></a>Ajuster la communication client-serveur</span><span class="sxs-lookup"><span data-stu-id="a12dc-462"><a name="filters"></a>Adjust the Client-Server Communication</span></span>

<span data-ttu-id="a12dc-463">La connexion client est normalement une connexion HTTP de base utilisant la bibliothèque HTTP sous-jacente fournie avec le Kit de développement logiciel (SDK) Android.</span><span class="sxs-lookup"><span data-stu-id="a12dc-463">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="a12dc-464">Vous voulez peut-être la modifier pour plusieurs raisons :</span><span class="sxs-lookup"><span data-stu-id="a12dc-464">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="a12dc-465">Vous souhaitez utiliser une autre bibliothèque HTTP pour régler les délais d’expiration.</span><span class="sxs-lookup"><span data-stu-id="a12dc-465">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="a12dc-466">Vous souhaitez fournir une barre de progression.</span><span class="sxs-lookup"><span data-stu-id="a12dc-466">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="a12dc-467">Vous souhaitez ajouter un en-tête personnalisé pour prendre en charge la fonctionnalité de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="a12dc-467">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="a12dc-468">Vous souhaitez intercepter une réponse indiquant un échec pour pouvoir implémenter la procédure de nouvelle authentification.</span><span class="sxs-lookup"><span data-stu-id="a12dc-468">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="a12dc-469">Vous souhaitez enregistrer les demandes du serveur principal sur un service analytique.</span><span class="sxs-lookup"><span data-stu-id="a12dc-469">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="a12dc-470">Utilisation d’une autre bibliothèque HTTP</span><span class="sxs-lookup"><span data-stu-id="a12dc-470">Using an alternate HTTP Library</span></span>

<span data-ttu-id="a12dc-471">Appelez la méthode `.setAndroidHttpClientFactory()` juste après avoir créé votre référence client.</span><span class="sxs-lookup"><span data-stu-id="a12dc-471">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="a12dc-472">Par exemple, pour définir le délai d’expiration de connexion sur 60 secondes (au lieu de la valeur par défaut de 10 secondes) :</span><span class="sxs-lookup"><span data-stu-id="a12dc-472">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="a12dc-473">Implémenter un filtre de progression</span><span class="sxs-lookup"><span data-stu-id="a12dc-473">Implement a Progress Filter</span></span>

<span data-ttu-id="a12dc-474">Vous pouvez implémenter une interception de chaque demande en implémentant un élément `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="a12dc-474">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="a12dc-475">Par exemple, le code suivant met à jour une barre de progression créée au préalable :</span><span class="sxs-lookup"><span data-stu-id="a12dc-475">For example, the following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="a12dc-476">Vous pouvez attacher ce filtre au client comme suit :</span><span class="sxs-lookup"><span data-stu-id="a12dc-476">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="a12dc-477">Personnaliser des en-têtes de demande</span><span class="sxs-lookup"><span data-stu-id="a12dc-477">Customize Request Headers</span></span>

<span data-ttu-id="a12dc-478">Utilisez l’élément `ServiceFilter` suivant et attachez le filtre comme vous le feriez pour l’élément `ProgressFilter` :</span><span class="sxs-lookup"><span data-stu-id="a12dc-478">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="a12dc-479"><a name="conversions"></a>Configurer la sérialisation automatique</span><span class="sxs-lookup"><span data-stu-id="a12dc-479"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="a12dc-480">Vous pouvez spécifier une stratégie de conversion qui s’applique à chaque colonne à l’aide de l’API [gson][3].</span><span class="sxs-lookup"><span data-stu-id="a12dc-480">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="a12dc-481">La bibliothèque cliente Android utilise [gson][3] en arrière-plan pour sérialiser les objets Java en données JSON, qui sont ensuite envoyées à Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a12dc-481">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="a12dc-482">Le code suivant utilise la méthode **setFieldNamingStrategy()** pour définir la stratégie.</span><span class="sxs-lookup"><span data-stu-id="a12dc-482">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="a12dc-483">Cet exemple supprimera le premier caractère (un « m »), puis mettra le caractère suivant en minuscule, ce pour tous les noms de champ.</span><span class="sxs-lookup"><span data-stu-id="a12dc-483">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="a12dc-484">Par exemple, il changera « mId » en « id ».</span><span class="sxs-lookup"><span data-stu-id="a12dc-484">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="a12dc-485">Implémentez une stratégie de conversion pour réduire le besoin d’annotations `SerializedName()` sur la plupart des champs.</span><span class="sxs-lookup"><span data-stu-id="a12dc-485">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="a12dc-486">Ce code doit être exécuté avant de créer une référence de client mobile à l’aide de **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="a12dc-486">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
<span data-ttu-id="a12dc-487">[Prise en main de l’authentification]: app-service-mobile-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="a12dc-487">[Get started with authentication]: app-service-mobile-android-get-started-users.md</span></span>
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
