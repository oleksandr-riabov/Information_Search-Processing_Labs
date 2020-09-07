** 1. За допомогою download.file() завантажте любий excel файл з порталу
http://data.gov.ua та зчитайте його (xls, xlsx – бінарні формати, тому
встановить mode = “wb”. Виведіть перші 6 строк отриманого фрейму
даних. **
  ```R
  download.file("https://data.gov.ua/dataset/2cde453d-a726-40e8-95f5-03eb05d4bfcc/resource/5b7b80af-7b7f-401f-8ea7-ad73c11596bd/download/pasport_naboru_danyh.xlsx","dataset1.xlsx", "auto", TRUE,"wb")
  library("readxl")
  dataset1 <- read_xlsx("data1.xlsx")
  head(data1, n = 5)
  ```

  ```cmd
  # A tibble: 6 x 3
    `Назва набору`          `Інформація про АЕС України`                                                          ...3 
    <chr>                   <chr>                                                                                 <chr>
  1 Шаблон назв файлів      info_aes_blocks_ДД_ММ_РРРР                                                            NA   
  2 Періодичність оприлюдн… У випадку оновлення даних, але не рідше, ніж 1 раз на квартал до 25 числа місяця, на… NA   
  3 NA                      NA                                                                                    NA   
  4 Структура набору:       NA                                                                                    NA   
  5 Назва поля              Назва поля українською                                                                Опис 
  ```
** 2. За допомогою download.file() завантажте файл getdata_data_ss06hid.csv за посиланням https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv та завантажте дані в R. Code book, що пояснює значення змінних знаходиться за посиланням https://www.dropbox.com/s/dijv0rlwo4mryv5/PUMSDataDict06.pdf?dl=0 Необхідно знайти, скільки property мають value $1000000+ **
  ```R
  > download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv", destfile="data2.csv", method="curl")
> data <- read.table("data2.csv", sep=",", header=TRUE)
> sum(!is.na(data$VAL[data$VAL==24]))
[1] 53

  ```
**3. Зчитайте xml файл за посиланням
http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml
Скільки ресторанів мають zipcode 21231?**
  ```R
  download.file("http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml","data3.xml", "auto", TRUE,"wb")
  save_3 <- xmlRoot(xmlTreeParse("data3.xml", useInternal = TRUE ))
  sum(xpathSApply(data3, "//zipcode", xmlValue) == 21231)
  ```

  ```cmd
  [1] 127
  ```
