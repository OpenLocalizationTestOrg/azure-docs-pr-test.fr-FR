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
# <a id="unity-roll-a-ball"></a>Créer un jeu Unity Roll a Ball
Ce didacticiel guide dans les étapes principales de hello pour légèrement modifiée [Unity restaurer un didacticiel boule](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). Cette partie de l’exemple se compose d’un objet sphérique 'lecteur' qui est contrôlé par l’utilisateur d’application hello et objectif hello du jeu de hello est too'collect' objets pouvant être collectés par objet de lecteur hello collision avec ces objets pouvant être collectés. Cela suppose une connaissance de base de l’environnement de Unity Editor. Si vous rencontrez des problèmes, puis vous devez consulter le didacticiel complet de toohello. 

### <a name="setting-up-hello-game"></a>Configuration d’un jeu de hello
étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Ouvrez **Unity Editor** et cliquez sur **New**. 
   
    ![][51] 
2. Indiquez un **nom de projet** & **emplacement**, sélectionnez **3D** et cliquez sur **Create project**.
   
    ![][52]
3. Enregistrer la scène par défaut de hello venez de créer en tant que partie du projet hello comme avec le nom de hello **MiniGame** dans un nouvel  **\_scènes** dossier sous **actifs** dossier :
   
    ![][53]
4. Créer un **objet 3D -> plan** comme hello champ et renommer cet objet de plan en tant que **sol**
   
    ![][1]
5. Composant de transformation hello de réinitialisation pour ce **sol** afin qu’il soit au hello d’origine de l’objet. 
   
    ![][3]
6. Décochez la case **afficher la grille de** de **menu des trucs** pour hello **sol** objet.
   
    ![][4]
7. Hello de mise à jour **échelle** composant hello **sol** toobe de l’objet [X = 2, Y = 1, Z = 2]. 
   
    ![][5]
8. Ajouter un nouveau **objet 3D -> sphère** toohello projet et renommer l’objet de ce domaine en tant que **lecteur**. 
   
    ![][6]
9. Sélectionnez hello **lecteur** de l’objet et cliquez sur **rétablir la transformation** objet de plan toohello similaire. 
10. Mise à jour **Transformation -> Position -> coordonnée Y** composant pourquoi le lecteur Y sous la forme 0.5.  
    
    ![][7]
11. Créez un dossier appelé **matériaux** dans le projet hello où nous allons créer le lecteur hello hello toocolor matériel. 
12. Créez un **matériau** appelé **Background** dans ce dossier. 
    
    ![][8]
13. Mettre à jour la couleur hello matières hello en mettant à jour hello **Albedo** propriété de celui-ci. Vous pouvez sélectionner les valeurs RVB hello de [0,32,64]. 
    
    ![][9]
14. Faire glisser ce matériel hello scène vue tooapply couleur toohello **sol** objet. 
    
    ![][10]
15. Enfin mettre à jour hello **Transformation -> Rotation -> Y** too60 sur l’objet de lumière directionnelle hello par souci de clarté. 
    
    ![][12]

### <a name="moving-hello-player"></a>Lecteur hello mobile
étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Ajouter un **RigidBody** composant toohello **lecteur** objet. 
   
    ![][13]
2. Créez un dossier appelé **Scripts** Bonjour projet. 
3. Cliquez sur **Add Component-> New Script -> C# Script**. Nommez-le **PlayerController**, puis cliquez sur **Create and Add**. Cela créera et attacher un objet de lecteur de toohello de script.  
   
    ![][14]
4. Déplacez ce script sous hello **Scripts** dossier de projet de hello. 
5. Ouvrir le script hello pour la modifier dans votre éditeur de script favori, mettre à jour le code de script hello avec hello suivant de code et enregistrez-le. 
   
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
6. Notez ce script hello ci-dessus utilise un **vitesse** propriété. Dans l’éditeur Unity hello, mettre à jour hello vitesse propriété too10.  
   
    ![][15]
7. Accès **lire** Bonjour éditeur Unity. Vous devez maintenant être en mesure de toocontrol boule de hello à l’aide du clavier de hello et il doit faire pivoter et déplacer. 

### <a name="moving-hello-camera"></a>Caméra hello mobile
étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) et lie hello **principal caméra** toohello **lecteur** objet. 

1. Hello de mise à jour **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.  
2. Hello de mise à jour **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Ajouter un nouveau script appelé **CameraController** toohello **MainCamera** et déplacez-la sous le dossier de Scripts hello. 
   
    ![][17]
4. Ouvrez script hello pour la modification et ajoutez hello suivant le code qu’il contient :
   
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
5. Dans l’environnement de Unity - faites glisser la variable de lecteur de hello dans l’emplacement du lecteur hello pour l’objet de la caméra principal hello afin que hello deux associés à un autre. 
   
    ![][18]
6. Si vous rencontrez Play dans l’éditeur Unity hello et objet lecteur hello rotation puis vous voyez à présent hello caméra suit un mouvement hello.  

### <a name="setting-up-hello-play-area"></a>Configuration de la zone de lecture hello
étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Nous allons créer murs hello entourant hello sol afin que hello objet lecteur ne suppriment zone de lecture hello dans son déplacement. 

1. Cliquez sur **Create -> Create Empty -> Game Object** et nommez-le **Walls**.
   
    ![][19]
2. Sous cet objet Walls, créez un objet **3D Object -> Cube** et nommez-le « West wall ». 
   
    ![][20]
3. Hello de mise à jour **Transformation -> Position** et **Transformation -> mise à l’échelle** pour cet objet de durée de l’ouest. 
   
    ![][21]
4. Dupliquer hello ouest mur toocreate un **mur d’Extrême-Orient** avec hello mis à jour transformer la position et l’échelle. 
   
    ![][22]
5. Dupliquer hello est mur toocreate un **mur du Nord** avec hello mis à jour transformer la position et l’échelle. 
   
    ![][23]
6. Dupliquer la durée totale du Nord hello et créer un **mur du Sud** avec hello mis à jour transformer la position et l’échelle. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>Création d’objets pouvant être collectés
étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Nous allons créer certains attrayantes recherche les objets qui forment ensemble hello d’objets pouvant être collectés too'collect a besoin de l’objet de lecteur boule hello' en collision avec eux. 

1. Créez un **objet 3D Cube** et nommez-le Pickup. 
2. Ajuster hello **Transformation -> Rotation** & **Transformation -> mise à l’échelle** d’objet de collecte hello. 
   
    ![][25]
3. Créer et attacher un **nouveau Script c#** appelé **Rotator** objet de capture toohello. Assurez-vous que script de hello tooput sous le dossier de Scripts hello. 
   
    ![][26]
4. Ouvrez ce script pour modifier et mettre à jour hello toobe suivant : 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Maintenant, mode de lecture de positionnement hello dans hello éditeur Unity et votre collecte d’objets-afficher être rotation sur l’axe.
6. Créez un dossier appelé **Prefabs** 
   
    ![][27]
7. Hello de glisser **collecte** de l’objet et le placer dans le dossier de Prefabs hello.
   
    ![][28]
8. Créez un **objet Empty Game** appelé **Pickups**. Réinitialiser son tooorigin position et faites-le glisser objet collecte de hello sous cet objet de jeu.  
   
    ![][29]
9. Hello en double **collecte** de l’objet et de l’étendre sur hello **sol** objet autour de hello **lecteur** objet en mettant à jour hello **de Transform.Position X & Z**  les valeurs de manière appropriée. 
   
    ![][30]
10. Créer un **le nouveau matériel** appelé **collecte** et mettre à jour toobe rouge dans la couleur en mettant à jour hello **les propriété Albedo** toowhat similaire nous hello sol de mise à jour de l’objet. 
    
    ![][31]
11. Appliquer des objets collecte hello tooall matériel hello 4.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>Collecte des objets de capture hello
étapes Hello ci-dessous proviennent de hello [didacticiel d’Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Nous mettrons à jour hello lecteur afin qu’il soit en mesure de too'collect' hello objets collecte en collision avec eux. 

1. Ouvrez hello **PlayerController** toohello attachée pour la modification d’objet lecteur de script et le mettre à jour toohello suivant :  
   
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
2. Créer un nouveau **balise** appelé **Pick Up** (elle doit correspondre à ce qui est dans le script de hello)  
   
    ![][33]
   
    ![][34]
3. Appliquer la **balise** objet de collecte Prefab toohello. 
   
    ![][35]
4. Activer **IsTrigger** case à cocher pour l’objet de PREFABRIQUE polyvalent hello.
   
    ![][36]
5. Ajoutez un objet de PREFABRIQUE polyvalent tooPickup corps rigide. Pour optimiser les performances, nous mettrons à jour collider statique de hello que nous avons utilisé les collider dynamique tooa. 
   
    ![][37]
6. Enfin vérifier hello **IsKinematic** propriété pour l’objet prefab hello. 
   
    ![][38]
7. Accès **lire** dans l’éditeur Unity hello et que vous sera en mesure de tooplay cette **restaurer une boule** jeu en déplaçant hello objet de lecteur à l’aide des touches du clavier pour l’entrée de sens. 

### <a name="updating-hello-game-for-mobile-play"></a>Mise à jour hello jeu pour play mobile
sections Hello ci-dessus didacticiel de base hello conclu à partir d’Unity. Maintenant, nous allons modifier hello toomake jeu il convivial de périphérique mobile. Notez que nous avons utilisé l’entrée au clavier pour hello jeu jusqu'à présent pour le test. Maintenant nous allons le modifier afin que nous pouvons contrôler le lecteur à l’aide de mouvement hello Hello hello phone par exemple, à l’aide d’accéléromètre en tant qu’entrée de hello. 

Ouvrez hello **PlayerController** script pour modifier et mettre à jour hello **FixedUpdate** mouvement de hello toouse méthode à partir de l’objet de lecteur hello accéléromètre toomove hello. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Ce didacticiel termine une création de base jeu avec Unity, et vous pouvez le déployer sur un périphérique de votre jeu de hello tooplay choix. 

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













