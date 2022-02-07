# yii2框架使用局部刷新表格分页问题解决
2017-09-02
------

使用pjax局部刷新，首先使用的是jquery.form.js中的表单异步提交
任务要求使用modal弹窗，表单异步提交，后台返回要替换的数据。在
源码中有提示使用方法：
```phyton
$(document).ready(function() {
    $('#myForm').on('submit', function(e) {
        e.preventDefault(); // <-- important
        $(this).ajaxSubmit({
            target: '#output'
        });
    });
});
```
target属性指定的是要替换的dom节点，这样的话我就把gridview组件
给提出来，单独创建一个文件：grid-view.php

index.php:
```phython
<?php Pjax::begin(['id'=>'user-contracts']); ?>
    <?= $this->render('grid-view', [
        'dataProvider' => $dataProvider,
    ]) ?>
<?php Pjax::end() ?>
```
后台控制器方法：
```phyton
...
$searchModel = $this->searchModelClass;
$searchModel = new $searchModel;
$params = $this->request->queryParams;
$dataProvider = $searchModel->search($params);

return $this->renderPartial('grid-view', [
    'dataProvider' => $dataProvider
]);
```
局部刷新的问题解决了，但是分页不支持，这个时候就找yii框架的pagination组件
最开始解决思路：既然分页不支持，那么干脆单独使用分页组件，gridview分页不显示
这样单独出去的分页不参与刷新，那么问题就解决了。结果与我设想的不一样，问题是
通过searchModel查询到的数据并没有当前页信息，就不会正确局部替换数据怎么办。这个时候，就需要改造searchModel模型，该模型使用的是yii\data\ActiveDataProvider组件，内置属性pagination ,应该可以通过pagination来增加分页信息, 而这个pagination使用的是
yii\data\Pagination模型，模型内找到一个疑似参数params，通过单词的字面意思可以看出这个属性意思，尝试设置这个属性，设置page=> $params['page'], 而这个params['page']是从前台传过来的值,也是当前页路由中的page,可以用$_GET['page']，来获取。所以这个
值得通过ajax传。解决了这个问题后，searchModel查询到的数据，就支持分页了，但是还有一点问题，就是分页的链接问题。看到Paginaiton模型内一个属性为route说明If not set, it means using the currently requested route.这个意思就是，如果不设置，该属性就是当前请求的路由，这个肯定不是我们想要的，所以就给它设置为固定路由（index）,这个属性是个字符串。解决了这个问题之后分页支持局部刷新了。所以果断的去掉前面单独使用的分页组件，开启gridview分页，ok整个问题解决

总结：可能个人理解的局限性，功能实现，代码正确性有待商榷。但是从这个功能中还是可以学习到查看源码的重要性
