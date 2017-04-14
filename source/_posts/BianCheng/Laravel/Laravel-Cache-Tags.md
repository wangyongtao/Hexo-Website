---
title: Laravel-缓存标签(Cache::tags)的使用
date: 2017-04-13
tags: 
- PHP
- Laravel
categories:
- PHP
- Laravel
---

缓存标签 Cache Tags

Laravel 缓存系统支持多种驱动方式，包括 file, database, Redis, Memcached 等， 也可以自定义一些其他的驱动方式。

在使用 Redis 驱动时，Laravel 提供了一种 `缓存标签` (Cache Tags), 可以很方便的对缓存进行管理分组。

注意:  
* 缓存标签目前不支持 `file` 或 `database` 缓存驱动。  
* 当使用多标签的缓存被设置为永久存储(forever)时，使用 `memcached` 驱动的缓存有着最佳性能表现，因为 Memcached 会自动清除陈旧记录。

## 存储被打上标签的缓存项 (put)

缓存标签允许你给相关缓存项打上同一个标签以便于后续清除这些缓存值，被打上标签的缓存可以通过传递一个被排序的标签数组来访问。

例如，我们可以通过以下方式在添加缓存的时候设置标签：

```
Cache::tags(['people', 'artists'])->put('John', $john, $minutes);
Cache::tags(['people', 'authors'])->put('Anne', $anne, $minutes);
```

你可以给多个缓存项打上相同标签，这是没有数目限制的。

## 访问被打上标签的缓存项 (get)

要获取被打上标签的缓存项，传递同样的有序标签数组到 tags 方法然后使用你想要获取的key来调用get方法：

```
$john = Cache::tags(['people', 'artists'])->get('John');
$anne = Cache::tags(['people', 'authors'])->get('Anne');
```

## 移除被打上标签的数据项 (flush)

你可以同时清除被打上同一标签/标签列表的所有缓存项。
例如，以下语句会移除被打上 `people` 或 `authors` 标签的所有缓存：

```
Cache::tags(['people', 'authors'])->flush();
```

这样，上面设置的 Anne 和 John 缓存项都会从缓存中移除。

相反，以下语句只移除被打上 `authors` 标签的语句，所以只有 Anne 会被移除, 而 John 不会被移除：

```
Cache::tags('authors')->flush();
```

## Reference

- https://laravel.com/docs/5.4/cache#cache-tags  

- http://laravelacademy.org/post/6858.html

[END]