---
title: 使用 macro 方法来扩展 Laravel 的基础类的功能
date: 2017-04-13
tags: 
- PHP
- Laravel
categories:
- PHP
- Laravel
---

在一般编程中，我们要扩展一个基础类，我们需要进行继承才能扩充。
然而Laravel利用PHP的特性，编写了一套叫做 Macroable 的 Traits，这样，凡是使用Macroable的类，都是可以使用这个方法扩充的。

基本使用方法

我下面用Collection类来做示范。

要给Collection加一个扩充方法可以这样写：

```
  <?php
  Collection::macro("macro_name", function ($parameters) {
      // Your macro
  });
```

这样就很容易的就扩充了Collection的方法，而不需要进行复杂的继承。

我们再举个具体的例子，把所有Collection的字符数组全部变成大写。那么我们就这样写：

```
<?php
Collection::macro('uppercase', function () {
    return collect($this->items)->map(function ($item) {
        return strtoupper($item);
    });
});
```

collect(["hello", "world"])->uppercase();

这个结果是: ["HELLO", "WORLD"]


关于macro内部的$this


Collection $this 在macro的作用域必须注意，$this不是指向你文件类的对象，而是指向你marco扩充的类。比如例子中的$this是指向Collection的。

这是因为在Marcoable的源代码中，是可以看到static::$macros[$method]->bindTo($this, static::class)这段代码。而bindTo是改变$this上下文指向的方法。

marco的代码应该放在哪里?#

marco的代码应该放在哪里才能让整个项目都能使用， 这个问题其实困扰了我很久， 所以一直没有写这个教程。不过现在研究明白了。

要让marco扩充的类，保证整个项目都能使用， 需要创建一个ServiceProvider，并把扩充的方法，放入boot()的方法中

  <?php
  namespace App\Providers;

  use Collection;
  use Illuminate\Support\ServiceProvider;

  class CollectionMacroServiceProvider extends ServiceProvider {

      public function boot()
      {
         Collection::macro('uppercase', function () {
            return collect($this->items)->map(function ($item) {
                return strtoupper($item);
            });
        });
      }

  }


然后我们就可以在config/app.php中的providers中下面加App\ProvidersCollectionMacroServiceProvider::class即可

哪些类可以使用marco#

Response
Request
Collection
HTML
Form
Filesystem
Cache
Str
Arr
Translator

等等,使用了Marcoable的Traits，如果是自己编写的类，使用了Marcoable，也可以这样扩充使用（写Laravel开源库的时候）

英文简版和参考#

我把经验的部分写在了Stackoverflow的document中了，有兴趣可以支持一下：
http://stackoverflow.com/documentation/laravel/2358/collections/14091/using-macro-to-extend-collections#t=201609231409103600633

参考内容：

https://github.com/laravel/framework/blob/7d116dc5a008e69c97f864af79ac46ab6a8d5895/src/Illuminate/Support/Traits/Macroable.php
https://github.com/laravel/framework/search?utf8=%E2%9C%93&q=macroable
http://laravel-recipes.com/recipes/181/creating-html-macros
https://laravelcollective.com/docs/5.3/html#custom-macros
https://laravel.com/docs/5.3/responses#response-macros