Readme pour lancer sur nos données :

cd ../pointcnn_seg
-> lancer l'apprentissage : train_val_leap.sh -g 0 -x Leap_x8_2048_random
-> lancer l'inférence : test_leap.sh -g 0 -x Leap_x8_2048_random -l C:/Users/aboughra/Documents/3A_these/Segmentation/PointCNN_seg/models/seg/LEAP/pointcnn_seg_Leap_x8_2048_random_2022-03-28-16-12-37_14636/ckpts/iter-21500 -r 1
-> lancer l'inférence 15 : test_leap15.sh -g 0 -x Leap_x8_2048_random -l C:/Users/aboughra/Documents/3A_these/Segmentation/PointCNN_seg/models/seg/LEAP/pointcnn_seg_Leap_x8_2048_random_2022-03-28-16-12-37_14636/ckpts/iter-21500 -r 1