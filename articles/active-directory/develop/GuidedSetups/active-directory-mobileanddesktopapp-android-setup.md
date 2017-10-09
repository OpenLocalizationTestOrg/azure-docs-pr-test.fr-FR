---
title: "aaaAzure AD v2 Android prise en main - le programme d’installation | Documents Microsoft"
description: "Cet article explique comment une application Android peut obtenir un jeton d’accès et appeler une ou plusieurs API Microsoft Graph qui nécessitent des jetons d’accès à partir du point de terminaison Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="e7932-103">Configuration de votre projet</span><span class="sxs-lookup"><span data-stu-id="e7932-103">Set up your project</span></span>

> <span data-ttu-id="e7932-104">Vous préférez toodownload de projet Android Studio de cet exemple à la place ?</span><span class="sxs-lookup"><span data-stu-id="e7932-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="e7932-105">[Télécharger un projet](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) et ignorer toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="e7932-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="e7932-106">Création d'un projet</span><span class="sxs-lookup"><span data-stu-id="e7932-106">Create a new project</span></span> 
1.  <span data-ttu-id="e7932-107">Ouvrez Android Studio, puis accédez à : `File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="e7932-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="e7932-108">Donnez un nom à votre application et cliquez sur `Next`</span><span class="sxs-lookup"><span data-stu-id="e7932-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="e7932-109">Assurez-vous que tooselect *21 d’API ou plus récente (Android 5.0)* et cliquez sur`Next`</span><span class="sxs-lookup"><span data-stu-id="e7932-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="e7932-110">Conservez `Empty Activity`, cliquez sur `Next`, puis sur `Finish`</span><span class="sxs-lookup"><span data-stu-id="e7932-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="e7932-111">Ajouter un projet de tooyour hello bibliothèque d’authentification Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="e7932-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="e7932-112">Dans Android Studio, accédez à : `Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="e7932-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="e7932-113">Copie et suit hello de coller du code sous `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="e7932-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="e7932-114">À propos de ce package</span><span class="sxs-lookup"><span data-stu-id="e7932-114">About this package</span></span>

<span data-ttu-id="e7932-115">package Hello ci-dessus installe hello bibliothèque d’authentification Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="e7932-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="e7932-116">MSAL gère l’acquisition, la mise en cache et l’actualisation utilisateur jetons utilisés tooaccess API protégé par le point de terminaison Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="e7932-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="e7932-117">Créer l’interface utilisateur de votre application</span><span class="sxs-lookup"><span data-stu-id="e7932-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="e7932-118">Ouvrez : `activity_main.xml` sous `res` > `layout`</span><span class="sxs-lookup"><span data-stu-id="e7932-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="e7932-119">Modifier la disposition hello activité à partir de `android.support.constraint.ConstraintLayout` ou autres trop`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="e7932-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="e7932-120">Ajouter `android:orientation="vertical"` propriété trop`LinearLayout` nœud</span><span class="sxs-lookup"><span data-stu-id="e7932-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="e7932-121">Copie et suit hello de coller du code dans hello `LinearLayout` nœud, en remplaçant le contenu actuel hello :</span><span class="sxs-lookup"><span data-stu-id="e7932-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

