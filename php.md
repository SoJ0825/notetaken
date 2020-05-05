###### tags: `GitHub同步` `隨手筆記` `PHP`

# PHP 相關

## 語法

### stdClass

其實，stdClass在PHP5才開始被流行。而stdClass也是zend的一個保留類。似乎沒有其他作用。也幾乎沒有任何說明。

或者，我們可以這麼理解：stdClass是PHP的一個基類，所有的類幾乎都繼承這個類，所以任何時候都可以被new，可以讓這個變數成為一個object。同時，**這個基類又有一個特殊的地方，就是沒有方法**。

凡是用new stdClass()的變數，都不可能會出現$a->test()這種方式的使用方法。

或者，我們可以又這麼理解一下，正因為PHP5的物件的獨特性，物件在任何地方被呼叫，都是引用位址型的，所以相對消耗的資源會少一點。在其它頁面為它賦值時是直接修改，而不是引用一個拷貝。

```php
<?php
    $user = new stdClass();
    $user->name = 'gouki';
    $myUser = $user;
    $myUser->name = 'flypig';
    echo $user->name;    // flypig
    echo $myUser->name;  // flypig
```