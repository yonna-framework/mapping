[![License](https://img.shields.io/github/license/yonna-framework/mapping.svg)](https://packagist.org/packages/yonna/mapping)
[![Repo Size](https://img.shields.io/github/repo-size/yonna-framework/mapping.svg)](https://packagist.org/packages/yonna/mapping)
[![Downloads](https://img.shields.io/packagist/dm/yonna/mapping.svg)](https://packagist.org/packages/yonna/mapping)
[![Version](https://img.shields.io/github/release/yonna-framework/mapping.svg)](https://packagist.org/packages/yonna/mapping)
[![Php](https://img.shields.io/packagist/php-v/yonna/mapping.svg)](https://packagist.org/packages/yonna/mapping)

## Yonna mapping库

```
Mapping是一个极其好用的值对管理器
让你轻松管理项目所有的静态值对值
```

## 

#### 如何安装

##### 可以通过composer安装：`composer require yonna/mapping`

##### 可以通过git下载：`git clone https://github.com/yonna-framework/mapping.git`

> Yonna demo：[GOTO yonna](https://github.com/yonna-framework/yonna)

### Example

> 使用Mapping管理你的静态值吧
```php
<?php
    namespace MapTest;

    use Yonna\Mapping\Mapping;
    // 首先你可以新建一个map类，继承Mapping即可
    
    class Status extends Mapping
    {
    
        // 前面的tag可以作为程序中轻松调用的凭据，后面赋值
        const STATUS_1 = '1';
        const STATUS_2 = '2';
        const STATUS_3 = '3';
        
        // 你（可选地）可以为你的值对添加一些你想要的额外参数，首先新增一个构造函数
        // * 默认有label/status值，当然你也可以自己 setOptions
        
        public function __construct() {
            self::setLabel(self::STATUS_1, '状态1');
            self::setLabel(self::STATUS_2, '状态2');
            self::setLabel(self::STATUS_3, '状态3');
            // 等同于
            self::setOptions(self::STATUS_1, 'label','状态1');
            self::setOptions(self::STATUS_2, 'label','状态2');
            self::setOptions(self::STATUS_3, 'label','状态3');
            // 你还可以自定义值
            self::setOptions(self::STATUS_1, 'power','力量1');
            self::setOptions(self::STATUS_2, 'power','力量2');
            self::setOptions(self::STATUS_3, 'power','力量3');
        }
    }
    
?>
```

> 创建好你的mapping类之后，可以在任何地方轻松调用，以下是一些例子
```php
<?php
    
    use MapTest\Status;
    
    class OtherClass{
        
        public function test(){
            
            // 直接取值
            $val = Status::STATUS_1; // '1'
            
            // 取label
            $val = Status::getLabel(Status::STATUS_2); // '状态2'
            
            // 取自定义值
            $val = Status::getOptions(Status::STATUS_3, 'power'); // '力量3'
            
            // 取值对所有数据
            $val = Status::fetch(); // [['STATUS_1'=>'1'],['STATUS_2'=>'2'],['STATUS_3'=>'3']]
            
            // 取值对所有数据的json
            $val = Status::toJson(); // {"STATUS_1":"1","STATUS_2":"2","STATUS_3":"3"}
                        
            // 取值数组
            $val = Status::toArray(); // ['1','2','3']
            
            // 取值<K,V>
            $val = Status::toKV(); // [['1'=>'状态1'],['2'=>'状态2'],['3'=>'状态3']]
            $val = Status::toKV('power'); // [['1'=>'力量1'],['2'=>'力量2'],['3'=>'力量3']]
            
            // 取逗号序列
            $val = Status::toComma(); // 1,2,3
            
            // mapping默认自带一个status判断，默认为1，你可以设它为其他值达到你想要的逻辑
            Status::setStatus(false);
            
            // 混合取值
            $val = Status::toMixed();
            // [
            //    '1' => ['label'=>'状态1', 'power'=>'力量1', 'status'=>'1',],
            //    '2' => ['label'=>'状态2', 'power'=>'力量2', 'status'=>'1',],
            //    '3' => ['label'=>'状态3', 'power'=>'力量3', 'status'=>'1',]
            // ]
            
        }
        
    }
    
?>
```