В цій лабораторній роботі необхідно зчитати WEB сторінку з сайту IMDB.com зі 100 фільмами 2020 року виходу за посиланням «http://www.imdb.com/search/title?count=100&release_date=2020,2020&title_type=feature».  Необхідно створити data.frame «movies» з наступними даними: номер фільму (rank_data), назва фільму (title_data), тривалість (runtime_data). Для виконання лабораторної рекомендується використати бібліотеку «rvest». CSS селектори для зчитування необхідних даних: rank_data: «.text-primary», title_data: «.lister-item-header a», runtime_data: «.text-muted .runtime». Для зчитування url використовується функція read_html, для зчитування даних по CSS селектору – html_nodes і для перетворення зчитаних html даних в текст - html_text. Рекомендується перетворити rank_data та runtime_data з тексту в числові значення. При формуванні дата фрейму функцією data.frame рекомендується використати параметр «stringsAsFactors = FALSE».
В результаті виконання лабораторної роботи необхідно відповісти на запитання:


```r
install.packages('rvest')
library('rvest')
install.packages('xml2')
library('xml2')

raw_data = read_html('http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature')
html_rank <- html_text(html_nodes(raw_data,'.text-primary'))
rank_df <- as.numeric(html_rank)
title_df <- html_text(html_nodes(raw_data,'.lister-item-header a'))
runtime_html <- html_text(html_nodes(raw_data,'.text-muted .runtime'))
runtime_df <- as.numeric(gsub(" min", "", runtime_df))

movies <- data.frame(rank = rank_df, title = title_df, runtime = runtime_df, stringsAsFactors = FALSE)
```

1. Виведіть перші 6 назв фільмів дата фрейму.
  ```R
  head(movies, 6)$Title
  ```
  ```cmd
  [1] "Довод"             "Страна Лавкрафта"                               "Чудо-женщина: 1984"            
  [4] "Билл и Тед"        "Люди Икс: Новые мутанты"                       "Проект Power"           
  ```
2. Виведіть всі назви фільмів с тривалістю більше 120 хв.
  ```R
  subset(movies, runtime > 120)$Title
  ```

  ```cmd
 [1] "Довод"                    "Чудо-женщина: 1984"                               
 [3] "Энола Холмс"              "Sadak 2"                  
 [5] "Бессмертная гвардия"      "Гамильтон"                                    
 [7] "Прощание"                 "Евровидение: История группы Fire Saga"         
 [9] "Король Стейтен-Айленда"   "Не время умирать"                    
[11] "Дьявол всегда здесь"      "Пятеро одной крови"                              
[13] "Плохие парни навсегда"    "Форпост"            
[15] "И повсюду тлеют пожары"   "Человек-невидимка"                          
[17] "Будка поцелуев 2"         "Думаю, как всё закончить"                           
  ```
3. Скільки фільмів мають тривалість менше 100 хв.
  ```R
  nrow(movies[movies$runtime < 100, ])
  ```

  ```cmd
  [1] 39
  ```
