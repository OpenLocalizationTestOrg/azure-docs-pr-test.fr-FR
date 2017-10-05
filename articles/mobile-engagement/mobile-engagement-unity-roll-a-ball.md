---
title: didacticiel Unity Roll a Ball
description: "Étapes de création du jeu Unity Roll a Ball classique, qui est une condition préalable à tous les didacticiels Unity sur Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6392d1f780b1bc2348fee5947550b05e86ea4de2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="087be-103"><a id="unity-roll-a-ball"></a>Créer un jeu Unity Roll a Ball</span><span class="sxs-lookup"><span data-stu-id="087be-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="087be-104">Ce didacticiel est une version légèrement modifiée du [didacticiel Unity Roll a Ball](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial)et en présente les étapes principales.</span><span class="sxs-lookup"><span data-stu-id="087be-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="087be-105">Cet exemple de jeu consiste en un objet « Player » sphérique contrôlé par l’utilisateur de l’application, et l’objectif du jeu et de « collecter » des objets en les heurtant avec l’objet Player.</span><span class="sxs-lookup"><span data-stu-id="087be-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span></span> <span data-ttu-id="087be-106">Cela suppose une connaissance de base de l’environnement de Unity Editor.</span><span class="sxs-lookup"><span data-stu-id="087be-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="087be-107">Si vous rencontrez des problèmes, reportez-vous au didacticiel complet.</span><span class="sxs-lookup"><span data-stu-id="087be-107">If you run into any issues then you should refer to the full tutorial.</span></span> 

### <a name="setting-up-the-game"></a><span data-ttu-id="087be-108">Configuration du jeu</span><span class="sxs-lookup"><span data-stu-id="087be-108">Setting up the game</span></span>
<span data-ttu-id="087be-109">Les étapes suivantes sont issues du [didacticiel Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="087be-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="087be-110">Ouvrez **Unity Editor** et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="087be-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="087be-111">Indiquez un **nom de projet** & **emplacement**, sélectionnez **3D** et cliquez sur **Create project**.</span><span class="sxs-lookup"><span data-stu-id="087be-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="087be-112">Enregistrer la scène par défaut que vous venez de créer dans le cadre du nouveau projet sous **MiniGame** dans un nouveau dossier **\_Scenes** sous le dossier **Assets** :</span><span class="sxs-lookup"><span data-stu-id="087be-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="087be-113">Créez un objet **3D Object -> Plane** en tant que champ de jeu et renommez cet objet Plane en **Ground**.</span><span class="sxs-lookup"><span data-stu-id="087be-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="087be-114">Réinitialisez le composant de transformation de cet objet **Ground** afin qu’il se trouve à l’origine.</span><span class="sxs-lookup"><span data-stu-id="087be-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="087be-115">Décochez la case **Show Grid** du **menu Gizmos** pour l’objet **Ground**.</span><span class="sxs-lookup"><span data-stu-id="087be-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="087be-116">Mettez à jour le composant **Scale** pour l’objet **Ground** avec les valeurs [X = 2,Y = 1,Z = 2].</span><span class="sxs-lookup"><span data-stu-id="087be-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="087be-117">Ajouter un nouvel objet **3D Object -> Sphere** au projet, puis renommez cet objet Sphere en **Player**.</span><span class="sxs-lookup"><span data-stu-id="087be-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="087be-118">Sélectionnez l’objet **Player** et cliquez sur **Reset Transform** comme pour l’objet Plane.</span><span class="sxs-lookup"><span data-stu-id="087be-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span></span> 
10. <span data-ttu-id="087be-119">Mettez à jour le composant **Transform -> Position -> Y Coordinate** pour l’objet Player avec la valeur 0,5.</span><span class="sxs-lookup"><span data-stu-id="087be-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="087be-120">Créez un nouveau dossier appelé **Materials** dans le projet où nous allons créer le matériau pour colorier l’objet Player.</span><span class="sxs-lookup"><span data-stu-id="087be-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span></span> 
12. <span data-ttu-id="087be-121">Créez un **matériau** appelé **Background** dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="087be-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="087be-122">Mettez à jour la couleur du matériau en mettant à jour la propriété **Albedo** de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="087be-122">Update the color of the material by updating the **Albedo** property of it.</span></span> <span data-ttu-id="087be-123">Vous pouvez sélectionner les valeurs RVB [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="087be-123">You can select the RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="087be-124">Faites glisser ce matériau dans la vue de la scène pour appliquer la couleur à l’objet **Ground** .</span><span class="sxs-lookup"><span data-stu-id="087be-124">Drag this material into the scene view to apply color to the **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="087be-125">Pour terminer, mettez à jour **Transform -> Rotation -> Y** avec la valeur 60 sur l’objet Directional Light pour la clarté.</span><span class="sxs-lookup"><span data-stu-id="087be-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-the-player"></a><span data-ttu-id="087be-126">Déplacement du de l’objet Player</span><span class="sxs-lookup"><span data-stu-id="087be-126">Moving the player</span></span>
<span data-ttu-id="087be-127">Les étapes suivantes sont issues du [didacticiel Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="087be-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="087be-128">Ajoutez un composant **RigidBody** à l’objet **Player**.</span><span class="sxs-lookup"><span data-stu-id="087be-128">Add a **RigidBody** component to the **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="087be-129">Créez un dossier appelé **Scripts** dans le projet.</span><span class="sxs-lookup"><span data-stu-id="087be-129">Create a new folder called **Scripts** in the Project.</span></span> 
3. <span data-ttu-id="087be-130">Cliquez sur **Add Component-> New Script -> C# Script**.</span><span class="sxs-lookup"><span data-stu-id="087be-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="087be-131">Nommez-le **PlayerController**, puis cliquez sur **Create and Add**.</span><span class="sxs-lookup"><span data-stu-id="087be-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="087be-132">Cette opération crée et attache un script à l’objet Player.</span><span class="sxs-lookup"><span data-stu-id="087be-132">This will create and attach a script to the Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="087be-133">Déplacez ce script dans le dossier **Scripts** du projet.</span><span class="sxs-lookup"><span data-stu-id="087be-133">Move this script under the **Scripts** folder in the project.</span></span> 
5. <span data-ttu-id="087be-134">Ouvrez le script pour le modifier dans l’éditeur de script de votre choix, mettez à jour le code de script avec le code suivant et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="087be-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="087be-135">Notez que le script ci-dessus utilise une propriété **Speed** .</span><span class="sxs-lookup"><span data-stu-id="087be-135">Note that the script above uses a **Speed** property.</span></span> <span data-ttu-id="087be-136">Dans Unity Editor, mettez à jour la propriété Speed avec la valeur 10.</span><span class="sxs-lookup"><span data-stu-id="087be-136">In the Unity editor, update the speed property to 10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="087be-137">Appuyez sur **Play** dans Unity Editor.</span><span class="sxs-lookup"><span data-stu-id="087be-137">Hit **Play** in the Unity Editor.</span></span> <span data-ttu-id="087be-138">Vous devez maintenant être en mesure de contrôler la balle à l’aide du clavier, et elle doit pivoter et se déplacer.</span><span class="sxs-lookup"><span data-stu-id="087be-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span></span> 

### <a name="moving-the-camera"></a><span data-ttu-id="087be-139">Déplacement de la caméra</span><span class="sxs-lookup"><span data-stu-id="087be-139">Moving the camera</span></span>
<span data-ttu-id="087be-140">Les étapes suivantes sont issues du [didacticiel Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) et relient l’objet **Main Camera** à l’objet **Player**.</span><span class="sxs-lookup"><span data-stu-id="087be-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span></span> 

1. <span data-ttu-id="087be-141">Mettez à jour **Transform.Position** avec les valeurs X = 0, Y = 10,5, Z = -10.</span><span class="sxs-lookup"><span data-stu-id="087be-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="087be-142">Mettez à jour **Transform.Rotation** avec les valeurs X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="087be-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="087be-143">Ajoutez un script appelé **CameraController** à **MainCamera** et déplacez-le dans le dossier Scripts.</span><span class="sxs-lookup"><span data-stu-id="087be-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="087be-144">Ouvrez le script pour le modifier et ajoutez-y le code suivant :</span><span class="sxs-lookup"><span data-stu-id="087be-144">Open up the script for editing and add the following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="087be-145">Dans l’environnement Unity, faites glisser la variable Player dans l’emplacement Player pour l’objet Main Camera afin de les associer l’un à l’autre.</span><span class="sxs-lookup"><span data-stu-id="087be-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="087be-146">Si vous appuyez sur Play dans Unity Editor et que vous faites pivoter l’objet Player Ball, la caméra suit le mouvement.</span><span class="sxs-lookup"><span data-stu-id="087be-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span></span>  

### <a name="setting-up-the-play-area"></a><span data-ttu-id="087be-147">Configuration de la zone Play</span><span class="sxs-lookup"><span data-stu-id="087be-147">Setting up the Play area</span></span>
<span data-ttu-id="087be-148">Les étapes suivantes sont issues du [didacticiel Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="087be-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="087be-149">Nous allons créer les murs (Walls) entourant le sol (Ground) afin que l’objet Player Ball ne sorte pas de la zone de jeu pendant son déplacement.</span><span class="sxs-lookup"><span data-stu-id="087be-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span></span> 

1. <span data-ttu-id="087be-150">Cliquez sur **Create -> Create Empty -> Game Object** et nommez-le **Walls**.</span><span class="sxs-lookup"><span data-stu-id="087be-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="087be-151">Sous cet objet Walls, créez un objet **3D Object -> Cube** et nommez-le « West wall ».</span><span class="sxs-lookup"><span data-stu-id="087be-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="087be-152">Mettez à jour **Transform -> Position** et **Transform -> Scale** pour cet objet West Wall.</span><span class="sxs-lookup"><span data-stu-id="087be-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="087be-153">Dupliquer l’objet West Wall pour créer un objet **East wall** avec la position et l’échelle de transformation mises à jour.</span><span class="sxs-lookup"><span data-stu-id="087be-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="087be-154">Dupliquer l’objet East Wall pour créer un objet **North wall** avec la position et l’échelle de transformation mises à jour.</span><span class="sxs-lookup"><span data-stu-id="087be-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="087be-155">Dupliquer l’objet North Wall pour créer un objet **South wall** avec la position et l’échelle de transformation mises à jour.</span><span class="sxs-lookup"><span data-stu-id="087be-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="087be-156">Création d’objets pouvant être collectés</span><span class="sxs-lookup"><span data-stu-id="087be-156">Creating Collectible objects</span></span>
<span data-ttu-id="087be-157">Les étapes suivantes sont issues du [didacticiel Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="087be-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="087be-158">Nous allons créer des objets attractifs qui formeront l’ensemble d’objets que l’objet Player Ball doit « collecter » en se heurtant à eux.</span><span class="sxs-lookup"><span data-stu-id="087be-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="087be-159">Créez un **objet 3D Cube** et nommez-le Pickup.</span><span class="sxs-lookup"><span data-stu-id="087be-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="087be-160">Ajustez **Transform -> Rotation** & **Transform -> Scale** pour l’objet Pickup.</span><span class="sxs-lookup"><span data-stu-id="087be-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="087be-161">Créez un **script C#** appelé **Rotator** et attachez-le à l’objet Pickup.</span><span class="sxs-lookup"><span data-stu-id="087be-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span></span> <span data-ttu-id="087be-162">Assurez-vous de placer le script dans le dossier Scripts.</span><span class="sxs-lookup"><span data-stu-id="087be-162">Make sure to put the script under the Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="087be-163">Ouvrez ce script pour le modifier et mettez-le à jour comme suit :</span><span class="sxs-lookup"><span data-stu-id="087be-163">Open this script for editing and update it to be the following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="087be-164">Appuyez à présent sur le mode Play dans Unity Editor : votre objet Pickup pivote sur son axe.</span><span class="sxs-lookup"><span data-stu-id="087be-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="087be-165">Créez un dossier appelé **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="087be-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="087be-166">Faites glisser l’objet **Pickup** et placez-le dans le dossier Prefabs.</span><span class="sxs-lookup"><span data-stu-id="087be-166">Drag the **Pickup** object and put it in the Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="087be-167">Créez un **objet Empty Game** appelé **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="087be-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="087be-168">Réinitialisez sa position à l’origine, puis faites glisser l’objet Pickup sous cet objet de jeu.</span><span class="sxs-lookup"><span data-stu-id="087be-168">Reset its position to origin and then drag the Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="087be-169">Dupliquez l’objet **Pickup** et propagez-le sur l’objet **Ground** autour de l’objet **Player** en mettant à jour les valeurs **X et Z de Transform.Position** de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="087be-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="087be-170">Créez un **matériau** appelé **Pickup** et mettez-le à jour pour qu’il soit de couleur rouge en mettant à jour la **propriété Albedo** comme nous l’avons fait pour l’objet Ground.</span><span class="sxs-lookup"><span data-stu-id="087be-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="087be-171">Appliquez le matériau aux 4 objets Pickup.</span><span class="sxs-lookup"><span data-stu-id="087be-171">Apply the material to all the 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-the-pickup-objects"></a><span data-ttu-id="087be-172">Collecter les objets Pickup</span><span class="sxs-lookup"><span data-stu-id="087be-172">Collecting the Pickup objects</span></span>
<span data-ttu-id="087be-173">Les étapes suivantes sont issues du [didacticiel Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="087be-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="087be-174">Nous allons mettre à jour l’objet Player pour qu’il puisse « collecter » les objets Pickup en se heurtant à eux.</span><span class="sxs-lookup"><span data-stu-id="087be-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="087be-175">Ouvrez le script **PlayerController** joint à l’objet Player pour le modifier et mettez-le à jour comme suit :</span><span class="sxs-lookup"><span data-stu-id="087be-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="087be-176">Créez une **balise** appelée **Pick Up** (elle doit correspondre au contenu du script).</span><span class="sxs-lookup"><span data-stu-id="087be-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="087be-177">Appliquez cette **balise** à l’objet Prefab Pickup.</span><span class="sxs-lookup"><span data-stu-id="087be-177">Apply this **Tag** to the Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="087be-178">Cochez la case **IsTrigger** pour l’objet Prefab.</span><span class="sxs-lookup"><span data-stu-id="087be-178">Enable **IsTrigger** checkbox for the Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="087be-179">Ajoutez un corps rigide à l’objet Pickup Prefab.</span><span class="sxs-lookup"><span data-stu-id="087be-179">Add a Rigid body to Pickup Prefab object.</span></span> <span data-ttu-id="087be-180">Pour optimiser les performances, nous allons mettre à jour le collider statique que nous avons utilisé en collider dynamique.</span><span class="sxs-lookup"><span data-stu-id="087be-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="087be-181">Enfin, vérifiez la propriété **IsKinematic** de l’objet Prefab.</span><span class="sxs-lookup"><span data-stu-id="087be-181">Finally check the **IsKinematic** property for the prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="087be-182">Appuyez sur **Play** dans Unity Editor pour jouer à ce jeu **Roll a Ball** en déplaçant l’objet Player à l’aide des touches de votre clavier pour indiquer la direction.</span><span class="sxs-lookup"><span data-stu-id="087be-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-the-game-for-mobile-play"></a><span data-ttu-id="087be-183">Mise à jour du jeu pour y jouer sur un appareil mobile</span><span class="sxs-lookup"><span data-stu-id="087be-183">Updating the game for mobile play</span></span>
<span data-ttu-id="087be-184">Les sections ci-dessus marquent la fin du didacticiel de base d’Unity.</span><span class="sxs-lookup"><span data-stu-id="087be-184">The sections above concluded the basic tutorial from Unity.</span></span> <span data-ttu-id="087be-185">Maintenant, nous allons modifier le jeu pour qu’il soit compatible avec un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="087be-185">Now we will modify the game to make it mobile device friendly.</span></span> <span data-ttu-id="087be-186">Notez que nous avons utilisé le clavier jusqu’à présent pour tester le jeu.</span><span class="sxs-lookup"><span data-stu-id="087be-186">Note that we used keyboard input for the game so far for testing.</span></span> <span data-ttu-id="087be-187">Nous allons maintenant le modifier pour pouvoir contrôler l’objet Player à l’aide du mouvement du téléphone, par exemple,</span><span class="sxs-lookup"><span data-stu-id="087be-187">Now we will modify it so that we can control the player by using the motion of the phone i.e.</span></span> <span data-ttu-id="087be-188">avec l’accéléromètre.</span><span class="sxs-lookup"><span data-stu-id="087be-188">using Accelerometer as the input.</span></span> 

<span data-ttu-id="087be-189">Ouvrez le script **PlayerController** pour le modifier et mettez à jour la méthode **FixedUpdate** pour utiliser le mouvement de l’accéléromètre pour déplacer l’objet Player.</span><span class="sxs-lookup"><span data-stu-id="087be-189">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="087be-190">Ce didacticiel a permis de créer un jeu de base avec Unity et vous pouvez le déployer sur l’appareil de votre choix pour y jouer.</span><span class="sxs-lookup"><span data-stu-id="087be-190">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













