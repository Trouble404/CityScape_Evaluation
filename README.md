# CityScape_Evaluation
This script based on the panopticapi for coco

## Panoptic segmentation Metric

* PQ (panoptic segmentation) 、SQ ( segmentation quality)、RQ (recognition quality)

![image](https://raw.githubusercontent.com/Trouble404/CityScape_Evaluation/master/readme_pic/equation.png)

RQ是检测中应用广泛的 F1 score，用来计算全景分割中每个实例物体识别的准确性，SQ 表示匹配后的预测 segment与标注 segment 的 mIOU，如下图所示，只有当预测 segment 与标注 segment 的 IOU 严格大于 0.5 时，认为两个 segment 是匹配的。

![image](https://raw.githubusercontent.com/Trouble404/CityScape_Evaluation/master/readme_pic/example.png)


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
