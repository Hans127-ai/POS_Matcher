
Хороший результат. Давай продолжим редактирование файла. 

1. Я переписал код импорта данных по продажам в ячейке 1.3 под новый источник данных. Теперь код выглядит так. Проверь его на корректность и замени старый код на этот. 

`'''`
`Ячейка номер: 1.3. Назначение: Импортируем и преобразуем в нужные форматы данные по объему продаж торговой точки за неделю`

 `Структура данных в загружаемых файлах:`

`"SHIP_TO" - уникальный ID торговой точки вида 850023988`
`"YEAR_WEEK" - номер недели в формВате 202602", где первы 4 цифры это год, а последние 2 цифры это номер недели в году`
`"kCAF" - объем продаж за неделю в тысячах рублей. В источнике sales_sellout данные по продажам представлены в рублях а не в тысячах рублей, потому добавлен пересчёт.`
 `'''`

`df_sales = pd.DataFrame()`

`sales_path_sellin = r'C:\Users\rokotyev\Yandex.Disk\_Main Data Rokotyan\2. Проекты\60. Подбор пар ТТ для тестов\_data\sales_sellin'`
`for filename in os.listdir(sales_path_sellin):`
    `df_tmp = pd.read_csv(sales_path_sellin + '\\' + filename, sep=',', dtype='str')`
    `df_tmp[['SHIP_TO', 'YEAR_WEEK']] = df_tmp[['SHIP_TO', 'YEAR_WEEK']].astype('int')`
    `df_tmp['kCAF'] = df_tmp['kCAF'].astype('float')`
    `df_sales = pd.concat([df_sales, df_tmp])`
    `df_tmp = pd.DataFrame()`
  

`sales_path_sellout = r'C:\Users\rokotyev\Yandex.Disk\_Main Data Rokotyan\2. Проекты\60. Подбор пар ТТ для тестов\_data\sales_sellout'`
`for filename in os.listdir(sales_path_sellout):`
    `df_tmp = pd.read_csv(sales_path_sellout + '\\' + filename, sep=',', dtype='str')`
    `df_tmp[['SHIP_TO', 'YEAR_WEEK']] = df_tmp[['SHIP_TO', 'YEAR_WEEK']].astype('int')`
    `df_tmp['kCAF'] = df_tmp['CAF'].astype('float')/1000`
    `df_tmp.drop(columns=['CAF'], inplace=True)`
    `df_sales = pd.concat([df_sales, df_tmp])`
    `df_tmp = pd.DataFrame()`


2.  Ты прав.  В  ячейке 2.4. умножение на коэффициент  для  SALES TREND и  MS TREND не интуитивно. Давай заменим для этих двух показателей подход. Пользователю будет удобнее задавать допустимую разницу между двумя линейными трендами в градусах. Либо можешь предложить свой подход, но согласуй его со мной прежде чем делать. 

3. В ячейке номер: 2.4. в виджете названия KPI   'FACING', 'SHELF SHARE', 'MARKET SHARE', 'SALES TREND', 'MS TREND'  после чек-боксов не отображаются полностью и выглядят как  FACIN...', 'SHEL...', 'MAR...', 'SALE...', 'MS T...'. Скорректируй вёрстку виджета так чтобы названия отображались полностью.

4. При выполнении ячейки  4.1.  на одной из итераций я получил ошибку, текст которой привожу ниже.  Я задал в ячейке 3.3. поиск 5 тестовых точек для каждой контрольной точки. Почему она возникла я не понимаю. Можешь дописать обработчик или дать мне инструкцию как выяснить причину. Возможно эта ошибка связана с тем что "ActiveFlag" у данной ТТ равен 0?

	`---------------------------------------------------------------------------`
`UnboundLocalError                         Traceback (most recent call last)`
`File c:\Users\rokotyev\AppData\Local\miniconda3\Lib\site-packages\ipywidgets\widgets\widget.py:191, in CallbackDispatcher.__call__(self, *args, **kwargs)`
    `189 for callback in self.callbacks:`
    `190     try:`
`--> 191         local_value = callback(*args, **kwargs)`
    `192     except Exception as e:`
    `193         ip = get_ipython()`

`Cell In[20], line 28, in on_calculate_click(button)`
     `24             #display(df_pair_list)`
     `25` 
     `26         except Exception as e:`
     `27             print(f"Ошибка: {e}")`
`---> 28     return df_pair_list`

`UnboundLocalError: cannot access local variable 'df_pair_list' where it is not associated with a value` 


5. По итогам выполнения задачи подготовь файл matchmaker_new_2.ipynb, который я смогу скачать на свой компьютер и протестировать. 

 

