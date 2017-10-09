---
title: aaaUnity restaurer un didacticiel boule
description: "Étapes toocreate hello Unity de classique restaurer un jeu de balle qui est un composant requis pour tous les didacticiels de Mobile Engagement Unity"
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
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="bc31f-103"><a id="unity-roll-a-ball"></a>Créer un jeu Unity Roll a Ball</span><span class="sxs-lookup"><span data-stu-id="bc31f-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="bc31f-104">Ce didacticiel guide dans les étapes principales de hello pour légèrement modifiée [Unity restaurer un didacticiel boule](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="bc31f-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="bc31f-105">Cette partie de l’exemple se compose d’un objet sphérique 'lecteur' qui est contrôlé par l’utilisateur d’application hello et objectif hello du jeu de hello est too'collect' objets pouvant être collectés par objet de lecteur hello collision avec ces objets pouvant être collectés.</span><span class="sxs-lookup"><span data-stu-id="bc31f-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="bc31f-106">Cela suppose une connaissance de base de l’environnement de Unity Editor.</span><span class="sxs-lookup"><span data-stu-id="bc31f-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="bc31f-107">Si vous rencontrez des problèmes, puis vous devez consulter le didacticiel complet de toohello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="bc31f-108">Configuration d’un jeu de hello</span><span class="sxs-lookup"><span data-stu-id="bc31f-108">Setting up hello game</span></span>
<span data-ttu-id="bc31f-109">étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="bc31f-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="bc31f-110">Ouvrez **Unity Editor** et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="bc31f-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="bc31f-111">Indiquez un **nom de projet** & **emplacement**, sélectionnez **3D** et cliquez sur **Create project**.</span><span class="sxs-lookup"><span data-stu-id="bc31f-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="bc31f-112">Enregistrer la scène par défaut de hello venez de créer en tant que partie du projet hello comme avec le nom de hello **MiniGame** dans un nouvel  **\_scènes** dossier sous **actifs** dossier :</span><span class="sxs-lookup"><span data-stu-id="bc31f-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="bc31f-113">Créer un **objet 3D -> plan** comme hello champ et renommer cet objet de plan en tant que **sol**</span><span class="sxs-lookup"><span data-stu-id="bc31f-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="bc31f-114">Composant de transformation hello de réinitialisation pour ce **sol** afin qu’il soit au hello d’origine de l’objet.</span><span class="sxs-lookup"><span data-stu-id="bc31f-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="bc31f-115">Décochez la case **afficher la grille de** de **menu des trucs** pour hello **sol** objet.</span><span class="sxs-lookup"><span data-stu-id="bc31f-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="bc31f-116">Hello de mise à jour **échelle** composant hello **sol** toobe de l’objet [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="bc31f-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="bc31f-117">Ajouter un nouveau **objet 3D -> sphère** toohello projet et renommer l’objet de ce domaine en tant que **lecteur**.</span><span class="sxs-lookup"><span data-stu-id="bc31f-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="bc31f-118">Sélectionnez hello **lecteur** de l’objet et cliquez sur **rétablir la transformation** objet de plan toohello similaire.</span><span class="sxs-lookup"><span data-stu-id="bc31f-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="bc31f-119">Mise à jour **Transformation -> Position -> coordonnée Y** composant pourquoi le lecteur Y sous la forme 0.5.</span><span class="sxs-lookup"><span data-stu-id="bc31f-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="bc31f-120">Créez un dossier appelé **matériaux** dans le projet hello où nous allons créer le lecteur hello hello toocolor matériel.</span><span class="sxs-lookup"><span data-stu-id="bc31f-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="bc31f-121">Créez un **matériau** appelé **Background** dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="bc31f-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="bc31f-122">Mettre à jour la couleur hello matières hello en mettant à jour hello **Albedo** propriété de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="bc31f-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="bc31f-123">Vous pouvez sélectionner les valeurs RVB hello de [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="bc31f-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="bc31f-124">Faire glisser ce matériel hello scène vue tooapply couleur toohello **sol** objet.</span><span class="sxs-lookup"><span data-stu-id="bc31f-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="bc31f-125">Enfin mettre à jour hello **Transformation -> Rotation -> Y** too60 sur l’objet de lumière directionnelle hello par souci de clarté.</span><span class="sxs-lookup"><span data-stu-id="bc31f-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="bc31f-126">Lecteur hello mobile</span><span class="sxs-lookup"><span data-stu-id="bc31f-126">Moving hello player</span></span>
<span data-ttu-id="bc31f-127">étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="bc31f-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="bc31f-128">Ajouter un **RigidBody** composant toohello **lecteur** objet.</span><span class="sxs-lookup"><span data-stu-id="bc31f-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="bc31f-129">Créez un dossier appelé **Scripts** Bonjour projet.</span><span class="sxs-lookup"><span data-stu-id="bc31f-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="bc31f-130">Cliquez sur **Add Component-> New Script -> C# Script**.</span><span class="sxs-lookup"><span data-stu-id="bc31f-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="bc31f-131">Nommez-le **PlayerController**, puis cliquez sur **Create and Add**.</span><span class="sxs-lookup"><span data-stu-id="bc31f-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="bc31f-132">Cela créera et attacher un objet de lecteur de toohello de script.</span><span class="sxs-lookup"><span data-stu-id="bc31f-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="bc31f-133">Déplacez ce script sous hello **Scripts** dossier de projet de hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="bc31f-134">Ouvrir le script hello pour la modifier dans votre éditeur de script favori, mettre à jour le code de script hello avec hello suivant de code et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="bc31f-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
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
6. <span data-ttu-id="bc31f-135">Notez ce script hello ci-dessus utilise un **vitesse** propriété.</span><span class="sxs-lookup"><span data-stu-id="bc31f-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="bc31f-136">Dans l’éditeur Unity hello, mettre à jour hello vitesse propriété too10.</span><span class="sxs-lookup"><span data-stu-id="bc31f-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="bc31f-137">Accès **lire** Bonjour éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="bc31f-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="bc31f-138">Vous devez maintenant être en mesure de toocontrol boule de hello à l’aide du clavier de hello et il doit faire pivoter et déplacer.</span><span class="sxs-lookup"><span data-stu-id="bc31f-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="bc31f-139">Caméra hello mobile</span><span class="sxs-lookup"><span data-stu-id="bc31f-139">Moving hello camera</span></span>
<span data-ttu-id="bc31f-140">étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) et lie hello **principal caméra** toohello **lecteur** objet.</span><span class="sxs-lookup"><span data-stu-id="bc31f-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="bc31f-141">Hello de mise à jour **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.</span><span class="sxs-lookup"><span data-stu-id="bc31f-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="bc31f-142">Hello de mise à jour **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="bc31f-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="bc31f-143">Ajouter un nouveau script appelé **CameraController** toohello **MainCamera** et déplacez-la sous le dossier de Scripts hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="bc31f-144">Ouvrez script hello pour la modification et ajoutez hello suivant le code qu’il contient :</span><span class="sxs-lookup"><span data-stu-id="bc31f-144">Open up hello script for editing and add hello following code in it:</span></span>
   
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
5. <span data-ttu-id="bc31f-145">Dans l’environnement de Unity - faites glisser la variable de lecteur de hello dans l’emplacement du lecteur hello pour l’objet de la caméra principal hello afin que hello deux associés à un autre.</span><span class="sxs-lookup"><span data-stu-id="bc31f-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="bc31f-146">Si vous rencontrez Play dans l’éditeur Unity hello et objet lecteur hello rotation puis vous voyez à présent hello caméra suit un mouvement hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="bc31f-147">Configuration de la zone de lecture hello</span><span class="sxs-lookup"><span data-stu-id="bc31f-147">Setting up hello Play area</span></span>
<span data-ttu-id="bc31f-148">étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="bc31f-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="bc31f-149">Nous allons créer murs hello entourant hello sol afin que hello objet lecteur ne suppriment zone de lecture hello dans son déplacement.</span><span class="sxs-lookup"><span data-stu-id="bc31f-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="bc31f-150">Cliquez sur **Create -> Create Empty -> Game Object** et nommez-le **Walls**.</span><span class="sxs-lookup"><span data-stu-id="bc31f-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="bc31f-151">Sous cet objet Walls, créez un objet **3D Object -> Cube** et nommez-le « West wall ».</span><span class="sxs-lookup"><span data-stu-id="bc31f-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="bc31f-152">Hello de mise à jour **Transformation -> Position** et **Transformation -> mise à l’échelle** pour cet objet de durée de l’ouest.</span><span class="sxs-lookup"><span data-stu-id="bc31f-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="bc31f-153">Dupliquer hello ouest mur toocreate un **mur d’Extrême-Orient** avec hello mis à jour transformer la position et l’échelle.</span><span class="sxs-lookup"><span data-stu-id="bc31f-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="bc31f-154">Dupliquer hello est mur toocreate un **mur du Nord** avec hello mis à jour transformer la position et l’échelle.</span><span class="sxs-lookup"><span data-stu-id="bc31f-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="bc31f-155">Dupliquer la durée totale du Nord hello et créer un **mur du Sud** avec hello mis à jour transformer la position et l’échelle.</span><span class="sxs-lookup"><span data-stu-id="bc31f-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="bc31f-156">Création d’objets pouvant être collectés</span><span class="sxs-lookup"><span data-stu-id="bc31f-156">Creating Collectible objects</span></span>
<span data-ttu-id="bc31f-157">étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="bc31f-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="bc31f-158">Nous allons créer certains attrayantes recherche les objets qui forment ensemble hello d’objets pouvant être collectés too'collect a besoin de l’objet de lecteur boule hello' en collision avec eux.</span><span class="sxs-lookup"><span data-stu-id="bc31f-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="bc31f-159">Créez un **objet 3D Cube** et nommez-le Pickup.</span><span class="sxs-lookup"><span data-stu-id="bc31f-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="bc31f-160">Ajuster hello **Transformation -> Rotation** & **Transformation -> mise à l’échelle** d’objet de collecte hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="bc31f-161">Créer et attacher un **nouveau Script c#** appelé **Rotator** objet de capture toohello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="bc31f-162">Assurez-vous que script de hello tooput sous le dossier de Scripts hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="bc31f-163">Ouvrez ce script pour modifier et mettre à jour hello toobe suivant :</span><span class="sxs-lookup"><span data-stu-id="bc31f-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="bc31f-164">Maintenant, mode de lecture de positionnement hello dans hello éditeur Unity et votre collecte d’objets-afficher être rotation sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="bc31f-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="bc31f-165">Créez un dossier appelé **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="bc31f-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="bc31f-166">Hello de glisser **collecte** de l’objet et le placer dans le dossier de Prefabs hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="bc31f-167">Créez un **objet Empty Game** appelé **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="bc31f-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="bc31f-168">Réinitialiser son tooorigin position et faites-le glisser objet collecte de hello sous cet objet de jeu.</span><span class="sxs-lookup"><span data-stu-id="bc31f-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="bc31f-169">Hello en double **collecte** de l’objet et de l’étendre sur hello **sol** objet autour de hello **lecteur** objet en mettant à jour hello **de Transform.Position X & Z**  les valeurs de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="bc31f-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="bc31f-170">Créer un **le nouveau matériel** appelé **collecte** et mettre à jour toobe rouge dans la couleur en mettant à jour hello **les propriété Albedo** toowhat similaire nous hello sol de mise à jour de l’objet.</span><span class="sxs-lookup"><span data-stu-id="bc31f-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="bc31f-171">Appliquer des objets collecte hello tooall matériel hello 4.</span><span class="sxs-lookup"><span data-stu-id="bc31f-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="bc31f-172">Collecte des objets de capture hello</span><span class="sxs-lookup"><span data-stu-id="bc31f-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="bc31f-173">étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="bc31f-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="bc31f-174">Nous mettrons à jour hello lecteur afin qu’il soit en mesure de too'collect' hello objets collecte en collision avec eux.</span><span class="sxs-lookup"><span data-stu-id="bc31f-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="bc31f-175">Ouvrez hello **PlayerController** toohello attachée pour la modification d’objet lecteur de script et le mettre à jour toohello suivant :</span><span class="sxs-lookup"><span data-stu-id="bc31f-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
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
2. <span data-ttu-id="bc31f-176">Créer un nouveau **balise** appelé **Pick Up** (elle doit correspondre à ce qui est dans le script de hello)</span><span class="sxs-lookup"><span data-stu-id="bc31f-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="bc31f-177">Appliquer la **balise** objet de collecte Prefab toohello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="bc31f-178">Activer **IsTrigger** case à cocher pour l’objet de PREFABRIQUE polyvalent hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="bc31f-179">Ajoutez un objet de PREFABRIQUE polyvalent tooPickup corps rigide.</span><span class="sxs-lookup"><span data-stu-id="bc31f-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="bc31f-180">Pour optimiser les performances, nous mettrons à jour collider statique de hello que nous avons utilisé les collider dynamique tooa.</span><span class="sxs-lookup"><span data-stu-id="bc31f-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="bc31f-181">Enfin vérifier hello **IsKinematic** propriété pour l’objet prefab hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="bc31f-182">Accès **lire** dans l’éditeur Unity hello et que vous sera en mesure de tooplay cette **restaurer une boule** jeu en déplaçant hello objet de lecteur à l’aide des touches du clavier pour l’entrée de sens.</span><span class="sxs-lookup"><span data-stu-id="bc31f-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="bc31f-183">Mise à jour hello jeu pour play mobile</span><span class="sxs-lookup"><span data-stu-id="bc31f-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="bc31f-184">sections Hello ci-dessus didacticiel de base hello conclu à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="bc31f-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="bc31f-185">Maintenant, nous allons modifier hello toomake jeu il convivial de périphérique mobile.</span><span class="sxs-lookup"><span data-stu-id="bc31f-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="bc31f-186">Notez que nous avons utilisé l’entrée au clavier pour hello jeu jusqu'à présent pour le test.</span><span class="sxs-lookup"><span data-stu-id="bc31f-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="bc31f-187">Maintenant nous allons le modifier afin que nous pouvons contrôler le lecteur à l’aide de mouvement hello Hello hello phone par exemple, à l’aide d’accéléromètre en tant qu’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="bc31f-188">Ouvrez hello **PlayerController** script pour modifier et mettre à jour hello **FixedUpdate** mouvement de hello toouse méthode à partir de l’objet de lecteur hello accéléromètre toomove hello.</span><span class="sxs-lookup"><span data-stu-id="bc31f-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="bc31f-189">Ce didacticiel termine une création de base jeu avec Unity, et vous pouvez le déployer sur un périphérique de votre jeu de hello tooplay choix.</span><span class="sxs-lookup"><span data-stu-id="bc31f-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

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













