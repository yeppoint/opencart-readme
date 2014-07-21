**opencart中要了解的PHP基础知识**

1. opencart中用到的built-in function

```
explode
is_dir
array_shift
func_get_args

```


2. 其中一种创建类的方法

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
and more:  
```php
//NOTE:array array_filter ( array $input [, callable $callback = "" ] )

function odd($var)
{
    // returns whether the input integer is odd
    return($var & 1);
}

function even($var)
{
    // returns whether the input integer is even
    return(!($var & 1));
}

$array1 = array("a"=>1, "b"=>2, "c"=>3, "d"=>4, "e"=>5);
$array2 = array(6, 7, 8, 9, 10, 11, 12);

echo "Odd :\n";
print_r(array_filter($array1, "odd")); //called the function odd
echo "Even:\n";
print_r(array_filter($array2, "even"));
```

