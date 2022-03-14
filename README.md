# PoseTrack21
PoseTrack21 is a [...]

## Usage
In order to obtain the entire dataset, please run the following command:
```
python3 download_dataset.py --save_path /target/root/path/of/the/dataset
```

## Dataset Structure 
The dataset is organized as follows: 

    .
    ├── images                              # contains all images  
        ├── train
        ├── val
    ├── posetrack_data                      # contains annotations for pose reid tracking
        ├── train
            ├── 000001_bonn_train.json
            ├── ...
        ├── val
            ├── ...
    ├── posetrack_mot                       # contains annotations for multi-object tracking 
        ├── mot
            ├── train
                ├── 000001_bonn_train
                    ├── image_info.json
                    ├── gt
                        ├── gt.txt          # ground truth annotations in mot format
                        ├── gt_kpts.txt     # ground truth poses for each frame
                ├── ...
            ├── val
    ├── posetrack_person_search             # person search annotations
        ├── query.json
        ├── train.json
        ├── val.json



### Pose Reid Tracking 
We adopt the same format proposed in PoseTrack18. A sample annotation file in `posetrack_data` has the following format:
```
{
    "images": [
        {
            "is_labeled": false,                # true,  if a frame contains annotated keypoints 
            "nframes": 76
            "frame_id": 10000010000, 
            "id": 10000010000, 
            "vid_id": 000001, 
            "file_name": images/train/000001_bonn_train/000000.jpg, 
            "has_labeled_person": false,        # true,  if a frame contaisn annotated bounding boxes (with or without keypoints)
            "ignore_regions_y": [
                [y11,  y12,  y13,  ...,  y1n], 
                [y21,  y22,  y23,  ...,  y2n]
            ],  
            "ignore_regions_x": [
                [x11,  x12,  x13,  ...,  x1n], 
                [x21,  x22,  x23,  ...,  x2n]
            ] 
        }
    ], 
    "annotations": [
        {
            "bbox": [x1,  y1, w, h], 
            "bbox_head": [x1,  y1,  w, h], 
            "category_id": 1, 
            "image_id": 10000010000, 
            "id": 1000001000000, 
            "keypoints": [x1, y1, vis1, ..., x17, y17, vis17], 
            "person_id": 1024, 
            "track_id": 0
        }
    ], 

    "categories": [
        {
            "supercategory": "person",
            "id": 1,
            "name": "person",
            "keypoints": [
                "nose",
                "head_bottom",
                "head_top",
                "left_ear",
                "right_ear",
                "left_shoulder",
                "right_shoulder",
                "left_elbow",
                "right_elbow",
                "left_wrist",
                "right_wrist",
                "left_hip",
                "right_hip",
                "left_knee",
                "right_knee",
                "left_ankle",
                "right_ankle"
            ],
            "skeleton": [
                [
                    16,
                    14
                ],
                [
                    14,
                    12
                ],
                [
                    17,
                    15
                ],
                [
                    15,
                    13
                ],
                [
                    12,
                    13
                ],
                [
                    6,
                    12
                ],
                [
                    7,
                    13
                ],
                [
                    6,
                    7
                ],
                [
                    6,
                    8
                ],
                [
                    7,
                    9
                ],
                [
                    8,
                    10
                ],
                [
                    9,
                    11
                ],
                [
                    2,
                    3
                ],
                [
                    1,
                    2
                ],
                [
                    1,
                    3
                ],
                [
                    2,
                    4
                ],
                [
                    3,
                    5
                ],
                [
                    4,
                    6
                ],
                [
                    5,
                    7
                ]
            ]
        }
    ]
}
```

Similarly,  submission files should have the following format: 
___to be done___

### Multi-Object Tracking 
In MOT,  we provide a slightly different format,  compared to related MOT datasets such as MOT17. In particular,  we replace `seqinfo.ini` by `image_info.json` with the following format:

```
[
    {
        "file_name": "images/train/000001_bonn_train/000000.jpg",
        "id": 10000010000,
        "frame_id": 10000010000,
        "vid_id": "000001",
        "frame_index": 1, 
        "ignore_regions_x": [
            [x1,  x2, ..., xn]
        ], 
        "ignore_regions_y": [
            [y1, y2, ..., yn]
        ]

    }, 
    ...
]
```

Each `gt.txt` follows the same format proposed by the MOT17 dataset, where `<x>`, `<y>`, `<z>` are set to `-1` and `<conf>` is set to `1`:
```
<frame>, <id>, <bb_left>, <bb_top>, <bb_width>, <bb_height>, <conf>, <x>, <y>, <z>
```

###  Person Search
`posetrack_person_search/train.json` and `posetrack_person_search/posetrack_person_search/val.json` follows a very similar structure as the annotations for [pose reid tracking](https://github.com/anDoer/PoseTrack21/edit/main/README.md#pose-reid-tracking).

`posetrack_person_search/query.json`,  on the other hand,  has the following format: 

```
{
    "images": [
            "file_name": "images/val/006540_mpii_test/000000.jpg",
            "frame_id": 10065400000,
            "ignore_regions_x": [],
            "ignore_regions_y": [],
            "nframes": 119,
            "vid_id": "006540",
            "annotations": [
                {
                    "bbox": [x1,  y1, w, h], 
                    "bbox_head": [x1,  y1,  w, h], 
                    "category_id": 1, 
                    "image_id": 10000010000, 
                    "id": 1000001000000, 
                    "keypoints": [x1, y1, vis1, ..., x17, y17, vis17], 
                    "person_id": 1024, 
                }, 
                ...
            ]

    ]
}
```
### Cite us here 
