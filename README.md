Yii2 Highcharts Widget
======================

[![Latest Stable Version](https://poser.pugx.org/miloschuman/yii2-highcharts-widget/v/stable.png)](https://packagist.org/packages/miloschuman/yii2-highcharts-widget)
[![Total Downloads](https://poser.pugx.org/miloschuman/yii2-highcharts-widget/downloads.png)](https://packagist.org/packages/miloschuman/yii2-highcharts-widget)
[![License](https://poser.pugx.org/miloschuman/yii2-highcharts-widget/license.png)](https://packagist.org/packages/miloschuman/yii2-highcharts-widget)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/miloschuman/yii2-highcharts-widget/badges/quality-score.png?s=cbb3ef746c21cd8a9f98bd91328fb317fee7e1d6)](https://scrutinizer-ci.com/g/miloschuman/yii2-highcharts-widget/)

Easily add [Highcharts, Highstock and Highmaps](http://www.highcharts.com/) graphs to your Yii2 application.

![Screen Shot](http://www.yiiframework.com/extension/yii2-highcharts/files/screenshot.png)


About
-----

### Highcharts ###
> Create interactive charts easily for your web projects. Used by tens of thousands of developers and 59 out of the world's 100 largest companies, Highcharts is the simplest yet most flexible charting API on the market.

### Highstock ###
> Highstock lets you create stock or general timeline charts in pure JavaScript. Including sophisticated navigation options like a small navigator series, preset date ranges, date picker, scrolling and panning.

### Highmaps ###
> Build interactive maps to display sales, election results or any other information linked to geography. Perfect for standalone use or in dashboards in combination with Highcharts!


Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist miloschuman/yii2-highcharts-widget "dev-master"
```

or add

```
"miloschuman/yii2-highcharts-widget": "dev-master"
```

to the require section of your `composer.json` file.


Usage
-----

### Preferred Method (using PHP arrays) ###

To use this widget, insert the following code into a view file:
```php
use miloschuman\highcharts\Highcharts;

echo Highcharts::widget([
   'options' => [
      'title' => ['text' => 'Fruit Consumption'],
      'xAxis' => [
         'categories' => ['Apples', 'Bananas', 'Oranges']
      ],
      'yAxis' => [
         'title' => ['text' => 'Fruit eaten']
      ],
      'series' => [
         ['name' => 'Jane', 'data' => [1, 0, 4]],
         ['name' => 'John', 'data' => [5, 7, 3]]
      ]
   ]
]);
```
By configuring the `options` property, you can specify the options that need to be passed to the Highcharts JavaScript object. Please refer to the demo gallery and documentation on the [Highcharts website](http://www.highcharts.com/) for possible options.

See [/doc/examples](https://github.com/miloschuman/yii2-highcharts/tree/master/doc/examples) for more usage examples.

### Alternative Method (using JSON string) ###

Alternatively, you can use a valid JSON string in place of an associative array to specify options:
```php
Highcharts::widget([
   'options'=>'{
      "title": { "text": "Fruit Consumption" },
      "xAxis": {
         "categories": ["Apples", "Bananas", "Oranges"]
      },
      "yAxis": {
         "title": { "text": "Fruit eaten" }
      },
      "series": [
         { "name": "Jane", "data": [1, 0, 4] },
         { "name": "John", "data": [5, 7,3] }
      ]
   }'
]);
```

*Note:* You must provide a *valid* JSON string (with double quotes) when using the second option. You can quickly validate your JSON string online using [JSONLint](http://jsonlint.com/).

### Just the Assets ###

If you merely want to include the Highcharts/Highstock/Highmaps javascript libraries in your view, you can bypass the widget and access the asset bundle directly:

```php
use miloschuman\highcharts\HighchartsAsset;

HighchartsAsset::register($this)->withScripts(['highstock', 'modules/exporting', 'modules/drilldown']);
```

In this scenario, you would need to write and include your own JavaScript to display the charts, just as illustrated in the [Highcharts Demo](http://www.highcharts.com/demo) and [Highstock Demo](http://www.highcharts.com/stock/demo) pages.


Tips
----

* If you need to use JavaScript in any of your configuration options, use Yii's [[JsExpression]] object. For instance:

  ```php
  ...
  'tooltip' => [
     'formatter' => new JsExpression('function(){ return this.series.name; }')
  ],
  ...
  ```
  Note, this is currently only possible when using a PHP associative array ([Preferred Method](#preferred-method-using-php-arrays)) for configuration.
* Highcharts by default displays a small credits label in the lower right corner of the chart. This can be removed using the following top-level option.

  ```php
  ...
  'credits' => ['enabled' => false],
  ...
  ```
* All adapters, modules, themes, and supplementary chart types must be enabled through the top-level 'scripts' option.

  ```php
  ...
  'scripts' => [
     'highcharts-more',   // enables supplementary chart types (gauge, arearange, columnrange, etc.)
     'modules/exporting', // adds Exporting button/menu to chart
     'themes/grid'        // applies global 'grid' theme to all charts
  ],
  ...
  ```
  For a list of available scripts, see the contents of `vendor/miloschuman/yii2-highcharts-widget/src/assets/`.


Change Log
----------

### [v4.0.4](https://github.com/miloschuman/yii2-highcharts/releases/tag/v4.0.4) (2014-09-25) ###
* Upgraded Highcharts core library to the latest release (4.0.4). See the Highcharts [changelog](http://highcharts.com/documentation/changelog) for more information about what's new in this version. 
* Added usage examples in [/doc/examples](https://github.com/miloschuman/yii2-highcharts/tree/master/doc/examples).
* Added HighmapsWidget. See included [Highmaps Widget Example](https://github.com/miloschuman/yii2-highcharts/tree/master/doc/examples/highmaps.md) for usage.
* Added callback option to make AJAX loading easier. See included [Highstock Widget Example](https://github.com/miloschuman/yii2-highcharts/tree/master/doc/examples/highstock.md) for usage.

### [v4.0.1](https://github.com/miloschuman/yii2-highcharts/releases/tag/v4.0.1) (2014-04-24) ###
* Upgraded Highcharts core library to the latest release (4.0.1).

### [v3.0.10](https://github.com/miloschuman/yii2-highcharts/releases/tag/v3.0.10) (2014-03-17) ###
* Upgraded Highcharts core library to the latest release (3.0.10).

### [v3.0.9](https://github.com/miloschuman/yii2-highcharts/releases/tag/v3.0.9) (2014-02-17) ###
* Upgraded Highcharts core library to the latest release (3.0.9).
