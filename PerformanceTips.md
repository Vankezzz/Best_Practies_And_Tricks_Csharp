1. Материализация запросов LINQ:
> При работе с LINQ пользуемся IEnumerable или IQueryable и у нас есть два пути: работать лениво с коллекциями или материализовать (ToList, ToArray)

|            NotMaterializedQuery              	|						MaterializedQuery                       |
|:---------------------------------------------:|:-------------------------------------------------------------:|
|public void NotMaterializedQueryTest()         |public void MaterializedQueryTest()                            
{                                              	 {                                                              
  var elements = Enumerable.Range(0, 50000000);	   var elements = Enumerable.Range(0, 50000000);                
  var filtered =                               	   var filtered = elements.Where(e => e % 100000 == 0).ToList();
    elements.Where(e => e % 100000 == 0);      	   //остальной код такой же										
												 }                                                              
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
|:---------------------------------------------:|:-------------------------------------------------------------:|
|											TestSpeed(Mean)			 											|
|:---------------------------------------------:|:-------------------------------------------------------------:|
|**1,299.6 ms**									|													**495.5 ms**|
