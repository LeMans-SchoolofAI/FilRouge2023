# Générer le modèle
Utiliser MobileSAM : https://github.com/ChaoningZhang/MobileSAM/

Exporter le modèle en ONNX
```
python scripts/export_onnx_model.py --checkpoint ./weights/mobile_sam.pt --model-type vit_t --return-single-mask --output ./mobile_sam.onnx
```
A noter le critère "--return-single-mask" qui permet de limiter la consommation CPU lors de l'inférence puisque l'on n'a besoin que d'un masque


# Paramètres du modèle

Pour déterminer les paramètres d'entrée, utiliser le script get_size.py
Ce qui donne pour le modèle actuel :

```
Inputs:
image_embeddings: 1, 256, 64, 64, 
point_coords: 1, num_points, 2, 
point_labels: 1, num_points, 
mask_input: 1, 1, 256, 256, 
has_mask_input: 1, 
orig_im_size: 2, 


Outputs:
masks: Resizemasks_dim_0, Resizemasks_dim_1, Resizemasks_dim_2, Resizemasks_dim_3, 
iou_predictions: Unsqueezeiou_predictions_dim_0, 1, 
low_res_masks: Unsqueezelow_res_masks_dim_0, 1, Unsqueezelow_res_masks_dim_2, Unsqueezelow_res_masks_dim_3, 
```