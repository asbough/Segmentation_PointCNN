# Segmentation

Ici nous réalisons la segmentation sur les données synthétiques et réelles après un apprentissage purement sur données synthétiques.
# Apprentissage synthétique
Pour lancer l'apprentissage sur données synthétiques : 
```
cd PointCNN
cd pointcnn_seg
train_val_leap.sh -g 0 -x Leap_x8_2048_random
```
NB: categories.txt doit contenir les classes qui sont lancées en apprentissage. Ce document fait correspondre le nombre de catégories par classe (nombre de labels différents). Ici on dénote 2 catégories par classe (le support (label 1) et le background (label 0)). 

# Inférence sur données synthétiques
Pour l'inférence sur les données synthétiques, on fait une classe à la fois et mettre dans data/LEAP_seg/categories_synth.txt et data/LEAP_seg/Test.txt la classe à lancer:
```
cd PointCNN
cd pointcnn_seg
test_leap.sh -g 0 -x Leap_x8_2048_random -l ../../models/seg/LEAP/pointcnn_seg_Leap_x8_2048_random_2022-03-28-16-12-37_14636/ckpts/iter-21500 -r 1
```
(Prêt à l'emploi pour la classe 0) 

# Inférence sur données réelles
Pour l'inférence sur les données réelles, on fait une classe à la fois et mettre dans data/LEAP_seg/categories_real.txt et data/LEAP_seg/Test_real.txt la classe à lancer:
```
cd PointCNN
cd pointcnn_seg
test_leap_real.sh -g 0 -x Leap_x8_2048_random -l ../../models/seg/LEAP/pointcnn_seg_Leap_x8_2048_random_2022-03-28-16-12-37_14636/ckpts/iter-21500 -r 1
```
(Prêt à l'emploi pour la classe 2)

Après cette commande deux dossiers sont crées dans data/LEAP_seg/Test_real.
- Real_data_pred_leap_1
- Real_data_pred_leap_ply

Dans le dossier Test_real :
```
Real_data : les nuages de la classe choisie au format '.pts' (nécessaire pour avoir la segmentation sur nuage .ply)
Real_h5 : les nuages de la classe choisie au format '.h5' (tous les nuages dans le même '.h5')
Real_data_pred_leap_1 : les nuages de la classe choisie après la segmentation donnée par le modèle appris sur le synthétique.
Real_data_pred_leap_ply : les nuages de la classe choisie après la segmentation donnée par le modèle mis au format '.ply' pour visualisation en beige (label 1) pour symboliser la pièce et en noir (label 0) symboliser ce qui est reconnu comme background.
```
# Métrique d'évaluation

## MIoU
Pour calculer la MIoU il faut :
* Real_data_pred_leap_1 :  la segmentation donnée par PointCNN (fichiers .seg)
* Real_Files_label_complete : la labellisation des nuages (annotation automatique)
* Real_Files_data_complete : les coordonnées des points de chaque nuage (fichiers .pts)
```
cd evaluation
python eval_LEAP.py -g ../../data/LEAP_MIOU_reel/Real_Files_label_complete -p ../../data/LEAP_MIOU_reel/Real_data_pred_leap_1 -d ../../data/LEAP_MIOU_reel/Real_Files_data_complete
```
Les résultats de MIoU par classe et Avg MIoU s'affichent directement dans la fenêtre de commande.
Un dossier (Real_data_pred_leap_1_err_ply) est crée dans LEAP_MIOU_reel pour visuliser sur les nuages les erreurs de segmentation.

## MIoU Part

Même principe que pour MIoU seul la commande change. On ajoute -a en fin de commande.

```
cd evaluation
python eval_LEAP.py -g ../../data/LEAP_MIOU_reel/Real_Files_label_complete -p ../../data/LEAP_MIOU_reel/Real_data_pred_leap_1 -d ../../data/LEAP_MIOU_reel/Real_Files_data_complete -a
```






