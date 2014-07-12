**opencart中要了解的PHP基础知识**

1. 其中一种创建类的方法

```
class FooBar {
    public function foo {
        echo "foo\n";
    }

    public function bar {
        echo "bar\n";
    }
}

$cls = "foobar";
$foobar_obj = new $cls;
$foobar_obj->foo();
$foobar_obj->bar();

$cls = "Foobar";
$foobar_obj = new $cls;
$foobar_obj->foo();
$foobar_obj->bar();

$cls = "fOoBAr";
$foobar_obj = new $cls;
$foobar_obj->foo();
$foobar_obj->bar();

```
