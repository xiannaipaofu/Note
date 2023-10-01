## Angular JS
    JS结构化框架

    Angular state inspector 扩展程序

    引入
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>

    const app = angular.module('myApp', []);  //创建angularjs模块

    指令
        ng-app  //绑定容器($rootScope)

        ng-controller="myCtrl"  //添加控制器,并在控制器中定义属性和方法
            app.controller('myCtrl', ['$scope', function($scope){
                $scope.carname = "";
                $scope.seyHello = function(){
                    console.log('hello-angularJS');
                }
            }])

        ng-model=""  //双向绑定数据

        ng-init="name='' "  //初始化当前作用域变量

        ng-repeat="i in arr";  {{i}}  //循环遍历数组生成元素节点(类似v-for)
            $index  //索引
            {{$first}}  //开头为true，后面为false
            {{$last}}  //结尾为true，其余为false
            {{$middle}}  //中间为true,头尾为false
            {{$odd}}  //奇数true，偶数false
            {{$even}}  //偶数true，奇数false

        ng-bind="xxx"  //解决使用{{}}显示数据闪屏问题

        ng-show=""  //显示与隐藏
        ng-hide=""

        事件
            ng-click
            ng-mouseenter  //鼠标移入
            ng-mouseleave  //鼠标移出

        ng-class  //动态引用定义样式{.class: true}
        ng-style  //动态引入通过js指定的样式对象{color: 'red'}

    {{}}  //插值语法
    {{username | uppercase}}  //过滤器currency格式化数字为货币格式。filter	从数组项中选择一个子集。lowercase	格式化字符串为小写。orderBy	根据某个表达式排列数组。uppercase	格式化字符串为大写。

    自定义指令
        const app = angular.module('myApp', []);
        app.directive('myBind', function(){
            return {
                template: "<div>自定义指令myBind</div>";
            }
        })
        <my-bind></my-bind>
        <div my-bind></div>

    发送请求
        传入$http
        $http({
            method: 'get',
            url: ''
        }).then()
        $http.get('url').then(()=>{})

    定时器
        $timeout
        $timeout(()=>{}, 1000)
        $interval  //循环定时器
        $interval(()=>{}, 1000)

    
