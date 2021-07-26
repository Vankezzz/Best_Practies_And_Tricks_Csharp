1. Материализация запросов LINQ:
> При работе с LINQ пользуемся IEnumerable или IQueryable и у нас есть два пути: работать лениво с коллекциями или материализовать (ToList, ToArray)
> В этом примере запрос Where не материализуется. Вызов метода Where просто возвращает объект, реализующий интерфейс IEnumerable. Методы GetEnumerator и MoveNext будут вызываться только при итерации по коллекции в цикле foreach.
```
public void NotMaterializedQueryTest()
{
  var elements = Enumerable.Range(0, 50000000);
  var filtered = 
    elements.Where(e => e % 100000 == 0);

  foreach (var e in filtered)
  { 
    …
  }

  foreach (var e in filtered)
  { 
    …
  }

  foreach (var e in filtered)
  {
    …
  }
}
```
```
public void MaterializedQueryTest()
{
  var elements = Enumerable.Range(0, 50000000);
  var filtered = 
    elements.Where(e => e % 100000 == 0).ToList();

  //остальной код такой же
}
```
|                   Method |       Mean |
|:------------------------:|:----------:|
| NotMaterializedQueryTest | 1,299.6 ms |
|    MaterializedQueryTest |   495.5 ms |

