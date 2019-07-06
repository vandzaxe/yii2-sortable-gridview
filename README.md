# yii2-sortable-gridview

[![Latest Stable Version](https://poser.pugx.org/richardfan1126/yii2-sortable-gridview/v/stable)](https://packagist.org/packages/richardfan1126/yii2-sortable-gridview)
[![Total Downloads](https://poser.pugx.org/richardfan1126/yii2-sortable-gridview/downloads)](https://packagist.org/packages/richardfan1126/yii2-sortable-gridview)
[![GitHub stars](https://img.shields.io/github/stars/richardfan1126/yii2-sortable-gridview.svg)](https://github.com/richardfan1126/yii2-sortable-gridview/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/richardfan1126/yii2-sortable-gridview.svg)](https://github.com/richardfan1126/yii2-sortable-gridview/issues)

This is an extension of Yii2 GridView.

This extension render a sortable GridView which you can drag and drop the record items from the list, and store the order in ActiveRecord.

## Getting Started
### Installing
Install with Composer:

    composer require vandzaxe/yii2-sortable-gridview "*"

or

    php composer.phar require vandzaxe/yii2-sortable-gridview "*"

or add

    "vandzaxe/yii2-sortable-gridview":"*"
to the require section of your composer.json file.

### Setting up SortableAction
In your controller, add the SortableAction into action():
```php
use vandzaxe\sortable\SortableAction;

public function actions(){
    return [
        'sortItem' => [
            'class' => SortableAction::className(),
            'activeRecordClassName' => YourActiveRecordClass::className(),
            'orderColumn' => 'name_of_field_storing_ordering',
        ],
        // your other actions
    ];
}
```

### Setting up SortableGridView
In the view file, use SortableGridView as using the Yii default GridView
```php
use vandzaxe\sortable\SortableGridView;

<?= SortableGridView::widget([
    'dataProvider' => $dataProvider,
    
    // you can choose how the URL look like,
    // but it must match the one you put in the array of controller's action()
    'sortUrl' => Url::to(['sortItem']),
    // The starting number of the sort. Default sort starts at 0.
    'startNumber' => 0,
    // The incremental number of the sort. Default increment is 1.
    'incrementalNumber' => 1,
    
    'columns' => [
        // Data Columns
    ],
]); ?>
```

You may also want to disable the pagination of data provider, in order to allow reordering across pages.

You can do it by calling below before passing data provider into SortableGridView
```php
$dataProvider->pagination = false;
```
## Configurations
### SortableAction
example:
```php
use vandzaxe\sortable\SortableAction;

public function actions(){
    return [
        'sortItem' => [
            'class' => SortableAction::className(),
            'activeRecordClassName' => Articles::className(),
            'orderColumn' => 'sortOrder',
        ],
        // your other actions
    ];
}
```

* **activeRecordClassName**  (required)The ActiveRecrod class name. Use the full class name with namespace.
* **orderColumn**  (required) The column name which store the sorting order of each records. The column should be integer.

---

### SortableGridView
example:
```php
use vandzaxe\sortable\SortableGridView;

<?= SortableGridView::widget([
    'dataProvider' => $dataProvider,
    
    // SortableGridView Configurations
    'sortUrl' => Url::to(['sortItem']),
    'startNumber' => 0,
    'incrementalNumber' => 1,
    'sortingPromptText' => 'Loading...',
    'failText' => 'Fail to sort',
    
    'columns' => [
        // Data Columns
    ],
]); ?>
```

* **sortUrl**  (required) The URL link to the SortableAction defined in controller's action().
* **startNumber**  (optional) The starting number of the sort. Default to 0.
* **incrementalNumber**  (optional) The incremental number of the sort. Default to 1.
* **sortingPromptText**  (optional) The text shown in the model while the server is reordering model. You can use HTML tag in this attribute. Default to "Loading...".
* **failText**  (optional) The text shown in alert box when sorting failed. Default to "Fail to sort".

## License
yii2-sortable-gridview is released under the MIT License. See the bundled LICENSE for details.
