# Задача о рюкзаке

## Условие

У вас есть рюкзак, в котором можно унести товары общим весом до 4 фунтов.

Есть три предмета, которые можно уложить в рюкзак:

Предмет|Цена|Вес
-|-|-
Магнитофон|3000|4
Ноутбук|2000|3
Гитара|1500|1

Какие предметы следует положить в рюкзак, чтобы стоимость добычи была максимальной?

## Динамическое программирование

Процедура начинается с решения подзадач с по­степенным переходом к решению полной задачи.

В задаче о рюкзаке начать следует с реше­ния задачи для меньшего рюкзака (или подрюкзака), а потом на этой основе попытаться решить исходную задачу.

Начинаем с таблицы, в которой каждый предмет представлен отдельной строкой. В качестве столбцов - размеры "подрюкзаков" в фунтах.

Фунты|1|2|3|4
-|-|-|-|-
Гитара||||
Магнитофон||||
Ноутбук||||

[Заполнение таблицы и зачем это нужно](./fill-table.md)

### Формула

Для заполнения каждой ячейки существует формула:

```
cell[row][col] = max(
  //предыдущий max
  cell[row - 1][col],

  // стоимость текущего элемента
  // + стоимость оставшегося пространства
  cell[row - 1][col - вес предмета]
)
```

***
***

**Решение задачи о рюкзаке**

Код:

```
const recorder = {
	name: 'Магнитофон',
	price: 3000,
	size: 4
};
const laptop = {
	name: 'Ноутбук',
	price: 2000,
	size: 3
};
const guitar = {
	name: 'Гитара',
	price: 1500,
	size: 1
};
const iPhone = {
	name: 'iPhone',
	price: 2000,
	size: 1
};
const player = {
  name: "MP3 player",
  price: 1000,
  size: 1
};

knapsack([recorder, laptop, guitar], 4); // 3500, Ноутбук + Гитара
knapsack([recorder, laptop, guitar, iPhone], 4); // 4000, iPhone + Ноутбук
knapsack([recorder, laptop, guitar, iPhone, player], 4); // 4500, плеер+ iPhone + Гитара
```

[Код функции knapsack](./knapsack.js)

Команда для проверки:

```
npm run knapsack
```

***
***