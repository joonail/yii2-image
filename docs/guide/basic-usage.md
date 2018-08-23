Form upload widgets
====================

Model configuration
-------------------

Add this to behaviours:

```php
[
    // other behaviors
    ... 
    'image' => [
        'class' => ImageBehavior::className(),
        'thumb_sizes' => [
            [
                'width' => 200,
                'height' => 200,
            ],
        ],
        'cdn_upload' => true,
    ],
]
```

Add this to rules:

```php
[
    // other rules
    ...
    ['image_type', 'safe'],
]
```

Controller configuration
-----------------------
Upload multiple images

```php
if ($model->save()) {
    ...
    $model->uploadImages('images');
}
```

Form configuration
------------------

List of images with an upload form:

```php
<?= $form->field($model, 'images')->widget(\common\widgets\image_upload\ImageList::classname(), [
    'form' => $form,
]); ?>
```

Upload a single image:

```php
<?= $form->field($model, 'image')->widget(\common\widgets\image_upload\ImageUpload::classname(), [
    'image_id' => $model->image_id,
    'form' => $form,
    'image_type' => \common\models\ImageType::MAIN_TYPE,
]); ?>
```

There are 3 default image types for the model:

* ImageType::DEFAULT_TYPE - all images
* ImageType::MAIN_TYPE - main image
* ImageType::PREVIEW_TYPE - preview image