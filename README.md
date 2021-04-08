# STRAB   
Формат последовательности текстовых символов разной длины. Название форматов состоит из трех частей:
- str (сокращенно от string)
- A = число бит в 1 последовательности символов (включая биты для обозначения режима отображения последовательности текстовых символа)
- B = число текстовых символов в одной последовательности    

# Назначение и цели создания      
Универсальный формат текстовых данных, предназначенный для удобной работы с простыми текстовыми данными.   

# Причина создания   
Отсутствуют (не нашел) универсальные решения, позволяющие корректно и просто хранить, передавать, обрабатывать и отображать текстовую информацию.   
Дополнительные преимущества:
- простое побитовое отсечение информации, содержащей информацию об только об оформлении;
- простое побитовое разделения текстовой информации и информации о режиме отображения текста. 

# Форматы последовательности текстовых символов
## STR31: Формат последовательности текстовых символов str31   
Размер символа 8 бит (2^3), включает в себя только значение самого текстового символа.   
Одное из значений = обозначению "пустого", "несуществующего", "незаданного" или "неотображаемого" текстового символа.   
Используемая кодировка символов **UTF8** или другая, подходящая по размеру.   

## STR41: Формат последовательности текстовых символов str41   
Размер символа 16 бит (2^4), включает в себя:   
### (0)   
0...7 бит- обозначение режима отображения текстового символа:   
-- **0й и 1й** биты зарезервированы для обозначения дополнительных данных об оформлении и отображении текста
> например,    
>     об использовании латиницы (=00) или кириллицы (=01),   
>     об указании об использовании обычного (=10) или расширенного (=11) набора символов   
>
-- **2й** бит для обозначения высоты букв:    обычная (=0) или высокая (=1)   
-- **3й** бит для обозначения выделения:      без выделения (=0) или жирный (=1)   
-- **4й** бит для обозначения стиля:          без курсива (=0) или курсив (=1)   
-- **5й** бит для обозначения подчеркивания:  без подчеркивания (=0) или с подчеркиванием (=1)   
-- **6й и 7й** биты для обозначения:          цвета символа или расширенного кода используемого шрифта:
> обычный (=00) или GYR (зеленый=01, желтый=10, красный=11)   
> 

**НЕ рекомендуется** в обозначениях режима отображения текстового символа хранить информацию о зачеркивании ~~символа~~.   
**Причина ограничения**: отсечение информации об оформлении поменяет ~~зачёркнутый~~ текст на обычный, что значительно искажает смысл исходной текстовой информации.   
**Рекомендуется**: Информацию о зачеркивании текстового символа хранить непосредственно в самом значении текстового символа, т.е. в неотсекаемой части текстовой последовательности.   

### (8)
8...15 бит - значение самого текстового символа, размером 8 бит   

## STR51: Формат последовательности текстовых символов str51   
Размер символа 32 бит (2^5), включает в себя:   
### (0)
0...7 бит   - обозначение режима отображения текстового символа (аналогично формату **STR41**).   
### (8)
8...31 бит  - значение самого текстового символа, размером 24 бит.   

## STR53: Формат последовательности текстовых символов str53   
Состоит из 3х (трех) последовательных текстовых символов.   
Если символов меньше 3х, то вместо недостающих значений устанавливаются значение "несуществующего" или "пустого" символа.   
Размер символа 32 бит (2^5), включает в себя обозначение режимов отображения текстовых символов и 3 символа размером 8 бит каждый:   
### (0)
0...7 бит   - обозначение режима отображения текстового символа (аналогично формату **STR41**)   
### (8)
8...15 бит  - значение текстового символа, размером 8 бит   
16...23 бит - значение текстового символа, размером 8 бит   
24...31 бит - значение текстового символа, размером 8 бит   

## STR67: Формат последовательности текстовых символов str67   
Размер 64 бит (2^6) (предназначен для ускорения работы на 64 битных процессорах и экономии памяти):   
Состоит из 7х (семи) последовательных текстовых символов.   
Если символов меньше 7, то вместо недостающих значений устанавливаются значение "несуществующего" или "пустого" символа.   
Размер одного символа в последовательности 8 бит,   
включает в себя обозначение режимов отображения текстовых символов и 7 символов размером 8 бит каждый:   
### (0)
0...7 бит   - обозначение режима отображения текстового символа (аналогично формату **STR41**)   
### (8)
8...15 бит  - значение текстового символа, размером 8 бит   
16...23 бит - значение текстового символа, размером 8 бит   
24...31 бит - значение текстового символа, размером 8 бит   
32...39 бит - значение текстового символа, размером 8 бит   
40...47 бит - значение текстового символа, размером 8 бит   
48...55 бит - значение текстового символа, размером 8 бит   
56...63 бит - значение текстового символа, размером 8 бит   
