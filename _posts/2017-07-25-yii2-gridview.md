---
layout: default
title: yii2 框架GridView使用小技巧
---
#### {{ page.title }}
{{ page.date | date: "%Y-%m-%d" }}
------

在yii2框架中GridView组件使用的频率很高，常用于数据列渲染。其中很重要的一个
功能就是过滤，而如何在不使用第三方组件的情况下让过滤变成我们想要的样子呢？ 比如可以是下拉框或者时间选择器

```python
  <?= GridView::widget([
    'dataProvider' => $dataProvider,
    'id' => 'contract-grid',
    'columns' => [
        ['class' => 'yii\grid\SerialColumn'],
        ['class' => 'yii\grid\CheckboxColumn'],
        [
            'label' => '学员姓名',
            'attribute' => 'student.name',
        ],
        ...

        [
            // 在不使用第三方组件的情况下使用html5 input[type =date]来实现过滤
            'attribute' => 'created_at',
            'format' => ['date', 'php:Y-m-d'],
            'filter' => Html::activeInput('date', $searchModel, 'created_at', [
              'class' => 'form-control' // 带上样式会比较统一好看
            ])
        ],
        [
          // 也可以有[type=number]类型过滤
          'attribute' => 'times',
          'value' => function ($model) {
              return $model->times ? '已加微信' . $model->times . '次' : null;
          },
          'filter' => Html::activeInput('number', $searchModel, 'times', [
              'class' => 'form-control'
          ])
        ],

        [
          'attribute' => 'category_id',
          ...
          'filter' => $category // 这个变量为分类数组格式为键值对
        ],
```