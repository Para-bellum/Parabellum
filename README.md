## Постраничная навигация

Данная постраничная навигация совместима с Bootstrap (v3 и v4), поэтому Вам не нужно беспокоиться о стилях для блока навигации, если Вы используете пресловутый framework.
Если же Вы не используете Bootstrap, достаточно будет прописать CSS-стили для следующих классов:
```css
.pagination {
    /* Стиль для общего блока с постраничной навигацией */
}
.pagination li {
    /* Стиль для тегов LI (нужно задать float) */
}
.pagination .active {
    /* Стиль для тега LI с текущей ссылкой */
}
.pagination a {
    /* Стиль для ссылок */
}
```

###### Пример использования
```php
use Parabellum\Pagination\Paginator;

# Получение количества записей
$stmt = $db->query('SELECT COUNT(*) FROM news');

$paginator = new Paginator($stmt->fetchColumn(), 10, $_GET);
```
Для ограничения выборки из базы данных используйте следующие методы:
- $paginator->skip() (смещение от начала)
- $paginator->take() (количество выводимых записей)

Например:
```php
$stmt = $db->prepare('SELECT * FROM news LIMIT ?, ?');

$result = $stmt->execute([
    $paginator->skip(),
    $paginator->take()
]);
```

Вывод страниц в представлении
```php
<?=$paginator->render()?>
```

###### Лицензия
Код доступен по лицензии MIT (см. LICENSE)
