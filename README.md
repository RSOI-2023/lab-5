# Что нужно делать

В рамках данной лабораторной необходимо реализовать один из вариантов развития системы и покрыть приложение тестами.
Что ценится при сдаче:

- Если при реализации пришлось затронуть классы, которые вообще не относятся к реализуемой логике, то это плохо.
- При написании тестов ценится уровень покрытия строк и уровень покрытия операторов ветвления.
  Необходимо добиться как минимум 60% по каждому показателю.

Пути развития разделены на простые и сложные. Сложные пути развития обозначены звёздочкой*. За выполнение
усложнённого варианта к итоговой оценке за лабораторные прибавляется 1 балл.

Уточнение: если в первой лабораторной вы выбрали свою предметную область, то необходимо обратиться к преподавателю
за вариантами развития (или предложить свои).
Однако, если вам не нравится ни одно из направлений развития вашей предметной области, также можно придумать и
реализовать своё (предварительно согласовав с преподавателем).

## Варианты развития

### Каршеринг

- Добавить поле "Километраж" в структуре поездки из истории поездок. Добавить метод, который
  вернёт суммарный километраж пользователя за всё время.
- Добавить поле "Премиум пользователь" (логический тип данных). Также позволить пользователю
  ввести данное поле как параметр для фильтрации (см. условие первой лабы).
- Сделать параметр "Общая сумма потраченных средств" промежутком. То есть, пользователь вводит минимальную
  и максимальную сумму. Должны быть выведены записи, у которых сумма лежит в промежутке, заданном пользователем.
  Например, если пользователь задал промежуток 100-200, то туда попадают значения 100, 101, ... 199, 200.

- *Выводить пользователей в порядке убывания рейтинга, также вывести рейтинг. Формулу для рейтинга можно взять любую,
  но понятное дело, если сверху будет пользователь с 1 поездкой и 0 нарушениями, то это плохая формула, так как
  игнорирует действительно важные факторы предметной области. В общем, сверху должны быть самые лояльные и активные
  пользователи.
  Идеи для формул можно найти в этой статье [тык](https://habr.com/ru/company/darudar/blog/143188/).
- *Добавить систему авторизации. Для этого у каждого пользователя должен быть пароль. Пароль нельзя хранить
  в открытом виде.
- *Добавить endpoint для получения автопарка. Также привязать запись Поездки из истории поездок к машине из автопарка.
  Добавить endpoint для получения списка машин, который отсортирован по количеству поездок за последний месяц.
  Структура автомобиля такая:

``` 
VIN | Номер | Модель | Пробег 
```

### Интернет-магазин

- Добавить сущность Пользователь, который может оставлять отзывы к товарам. Через обращение к пользователю,
  как и через обращение к товару, можно получить список отзывов.
- Добавить сущность Пользователь и сущность Корзина. У пользователя есть 1 корзина, в которую можно добавлять товары,
  удалять товары, полностью очищать. Элементы корзины всегда отсортированы по количеству заказов
- *Добавить поле с ценой товара и сделать так, чтобы цена на товар была промежутком (то есть, у каждого товара есть
  минимальная и максимальная цена),
  а также создать endpoint, который выводит информацию о: текущей минимальной цене, текущей максимальной цене, средней
  минимальной цене за 6 месяцев.
  Для всех расчётов, которые были реализованы в первой лабе, использовать минимальную цену.
- *Добавить поле с ценой товара. Также изменить формулу для расчёта средней оценки. Формула может быть любой,
  но должна учитывать количество заказов, оценки пользователей и цену на товар. Идеи для формул можно найти в этой
  статье
  [тык](https://habr.com/ru/company/darudar/blog/143188/).

### Система управления складом

- Добавить тип накладной "Очистка склада", которая обнуляет
  количество всех продуктов на складе. То есть, если на склад пришло 3 накладных, потом накладная очистки,
  а потом ещё 5 накладных, то количество товаров на определённую дату будет зависеть от того, находится
  ли введённая пользователем дата перед датой поступления обнуляющей накладной или после. Если пользователь ввёл более
  раннюю дату,
  чем обнуляющая накладная, то количество будет подсчитано на основании первых трёх накладных (по алгоритму
  из первой лабы). Если же более позднюю, то первые 3 накладные не учитываются.
- Добавить поле "ФИО ответственного" в структуре накладной. Также добавить метод, который вернёт
  список ответственных. Список отсортировать по суммарному количеству товаров в приходных накладных, в которых
  данный человек является ответственным.
- Добавить управление складским автопарком. У каждого склада есть список грузовых автомобилей. К каждому грузовику
  привязана накладная. Если на склад попала приходная накладная, то количество грузовиков увеличивается на 1.
  Если расходная накладная, то количество грузовиков на 1 уменьшилось. При этом если на автопарке склада осталось 0
  грузовиков, то любая расходная накладная должна быть отклонена. Также у стоянки склада есть вместимость (например, 10
  машин).
  Если на стоянке не осталось места, то любая приходная накладная должна быть отклонена. Изначально стоянка
  возле склада заполнена наполовину (то есть, 5 машин при максимальной вместимости 10 машин).
- *Сделать так, чтобы на складах могла храниться только продукция определённого типа.
  Например, на складе с холодильниками можно хранить мясо, но нельзя хранить молоко.
  Также добавить поле с типом продукта в структуру продукта. Если на склад приходит накладная, в которой есть
  продукт неподходящего типа, то такая накладная полностью отклоняется.
  Будет 3 типа складов, но предусмотреть простое увеличение их количества:
    - Мясная продукция
    - Овощная продукция
    - Все остальные продукты
- *Добавить возможность поделить склад между компаниями. Для начала нужно добавить складу поле с вместимостью.
  Допустим, у склада вместимость 1000 товаров, и этот склад разделён между тремя компаниями: 100, 300 и 600 товаров.
  Соответственно, чтобы добавить накладную, в ней должно быть указано название компании. И если приходная накладная
  превышает
  лимит места на складе, который отдан под компанию, то такая накладная должна быть отклонена. Соответственно, нужно
  добавить
  методы для аренды места на складе и отмену аренды.
- *Переделать программу в систему для управления несколькими складами. Добавить функционал по добавлению и удалению
  складов.
  Также добавить endpoint получения списка всех накладных конкретного. Также добавить метод, который вернёт список
  складов с количеством
  товаров на введённую дату.

### Система расчёта зарплаты с учётом бонусов

- Реализовать систему, которая будет брать все конфигурационные данные из файла (или другого источника, не
  предполагающего
  изменение исходного кода). Конфигурационные данные включают в себя базовую зарплату (1000р в примере),
  нижний порог зарплаты (500р в примере), прибыль с одного стола (30р в примере) и так далее.
- Сделать размер бонусов динамическим. За каждый дополнительно обслуженный стол работник получается на 1 рубля больше,
  чем за предыдущий. То есть, за первый дополнительно обслуженный стол размер бонуса составляет 5 рублей, за второй -- 6
  рублей
  за третий -- 7 рублей.
- Добавить поле чаевых. При подсчёте зарплаты сотрудника, прибавить половину от суммарного количества его чаевых за
  месяц. Чаевые прибавляются до вычета штрафов.
- *Добавить систему больничных. Если официант взял больничный, ему не начисляются штрафы за то, что он не обслужил
  все 100 столов. За каждый день больничного норма столов снижается на 5 (то есть, если официант взял 1 день
  больничного,
  то ему необходимо обслужить 95 столов). Однако, в месяц может быть от 0 до 3-х дней больничного.
- *Сделать размер бонусов динамическим. За каждый дополнительно обслуженный стол работник получается на 1 рубля больше,
  чем за предыдущий. То есть, за первый дополнительно обслуженный стол размер бонуса составляет 5 рублей, за второй -- 6
  рублей
  за третий -- 7 рублей. Также изменить функцию расчёта прибыли кафе. Считаем, что из 30 рублей, которые приносит стол,
  чистая прибыль равна 10 рублей. Найти оптимальное количество официантов для следующего месяца опираясь
  на количество столов, которые были обслужены в текущем месяце.

### Система рекомендации телефона исходя из потребностей пользователя (подбор Onliner)

- Сделать параметр "кол-во RAM" промежутком (как цена), но при этом телефон считается подходящим только в том случае,
  если количество RAM телефона строго попадает в промежуток пользователя. Например, если пользователь выбрал 6-8, то
  телефон 5-7 не подходит, как и телефон с 8-10. А если пользователь ввёл 4-10, то оба предыдущих варианта подходят.
- Добавить строковый параметр "Производитель". При выводе подходящих телефонов делать группировку
  по названию производителя. Внутри этих групп сортировать по количеству подошедших параметров.
  Например, сначала идут только телефоны Apple, потом только Google и т.д., а внутри групп уже сортировка
  по подходящим параметрам.
- Добавить вес параметрам. Например, за совпадение цены прибавлять 2 балла, а не 1. В то же время за
  параметр "наличие слота sd-карты" прибавлять 0.5 балла. Веса могут быть любые и заданы в программе.
- *Реализовать нечёткий поиск по названию телефона. Например, если в названии телефона пропущена буква или допущена
  опечатка, программа должна найти наиболее подходящие варианты.
- *Привязать к телефону в каталоге список изображений. Соответственно, реализовать возможность получать, добавлять и
  удалять изображения.

### Система рекомендации музыки (Spotify)

- Добавить песне поле "Нравится" и на основании него сформировать плейлист из любимых песен.
- Сделать размер плейлиста изменяемым (размер задаёт пользователь). При этом нельзя задать размер меньше 3-х и больше 15.
- Добавить список песен, которые нельзя добавлять ни в один из плейстов (независимо от количества прослушиваний).
  То есть, это список песен, которые заблокированы пользователем (пользователь не хочет их слушать).
- *Добавить каждой песне поля: Текст песни (может отсутствовать); Изображение (может отсутствовать);
  Список жанров к которым относится песня. Добавить endpoint, который вернёт песни по введённому пользователем жанру.
- *Добавить альбомы. У альбома есть название, изображение и список песен. Добавить метод, который вернёт 3 самых
  популярных альбома на основании прослушиваний пользователя. Например, если пользователь послушал 2 песни из альбома,
  и каждую из этих песен по 5 раз, то альбому выставляется коэффициент 10. 

