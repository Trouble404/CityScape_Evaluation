# CityScape_Evaluation
This script based on the panopticapi for coco

## Panoptic segmentation Metric

* PQ (panoptic segmentation) 、SQ ( segmentation quality)、RQ (recognition quality)



## Test Data Preparation

* Generate 2-channel format data (Pixels with the same label and id belong to the same object, for stuff labels the instance id is ignored). Put it to the sample_data/cityscape_2ch_format folder.

* Transfor 2-channel format to panoptic cityscale format based on the label file
```
python converters/2channels2panoptic_coco_format.py --source_folder sample_data/cityscape_2ch_format/ 
--images_json_file sample_data/cityscape_img_info.json --categories_json_file panoptic_city_categories.json
--segmentations_folder eva/pre/ --predictions_json_file eva/predition_coco.json
```

## Evaluation

* Running evaluation script to get the result
```
python evaluation.py --gt_json_file eva/cityscapes_panoptic_val.json --pred_json_file eva/predition_coco.json
--gt_folder eva/gt --pred_folder eva/pre
```
