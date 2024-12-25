# Практическая работа №1. Обработка изображений с использованием библиотеки OpenCV

## Описание программы

Программа реализует различные фильтры с использованием базовых операций над изображениями (представленными в виде матриц) в OpenCV.

## Реализованные алгоритмы

### 1) Фильтр "Оттенки серого"

Преобразованное изображение будет одноканальным, при этом каждый пиксель будет иметь интенсивность, вычисляемую как:

I = 0.299 * (R) + 0.587 * (G) + 0.114 * (B),

где (R), (G) и (B) - значения красного, зелёного и синего каналов соответственно в исходном изображение.

### 2) Фильтр "Сепия"

Каналы преобразованного изображения будут иметь значения, получаемые следующим образом:

R = (I) + 2.0 * (p),
G = (I) + 0.5 * (p), 
B = (I) - 1.0 * (p),

где (I) - интенсивность пикселя, вычисляемая по формуле из предыдущего пункта, (p) - произвольный положительный параметр. Если значения каналов выходят за пределы допустимого диапазона (0–255), они обрезаются до его границ.

### 3) Изменение размера изображения

Преобразованное изображение будет либо сжатым, либо растянутым вариантом исходного. Для этого генерируются сетки по горизонтали и вертикали из целочисленных индексов соответствующей размерности нового изображения: горизонтальная - значения от 0 до ширины исходного изображения минус 1, расположенные на равных расстояниях и округлённые вниз; то же самое для вертикали, но с верхним значением, равным высоте исходного изображения минус 1. Новые пиксели получают значения старых пикселей, индекс которых находится из соответствующего новому элементу значения наложения этих сеток друг на друга.

### 4) Фильтр "Виньетка"

Преобразованное изображение будет иметь более тёмные края: интенсивность пикселей будет убывать по мере удаления от круга заданного радиуса с центром в центре изображения. Убывание будет происходить как экспонента с отрицательным показателем, зависящим от расстояния от границы круга квадратично и с некоторым заданным коэффициентом.

### 5) Фильтр "Пикселизация"

Пользователь выбирает область на картинке, которая будет пикселизирована. На преобразованном изображении данная область будет заменена блоками заданных размеров, при этом цвет каждого блока будет усреднённым по тому же блоку в исходном изображении. Пользователь может дополнительно выбрать, перемешивать ли блоки.

## Описание параметров запуска программы

При запуске через командную строку могут быть указаны следующие параметры:

- `--input (-i)`: Путь к входному изображению.
- `--output (-o)`: Путь к файлу для записи обработанного изображения. Если не указан, запись результатов производиться не будет.
- `--mode (-m)`: Режим работы (оттенки серого `Greyscale`, сепия `Sepia`, изменение размера изображения `Resize`, виньетка `Vignette`, пикселизация `Pixelization`).
- `--param (-p)`: Параметры выбранного фильтра, при необходимости разделённые с помощью запятой (`Sepia`: интенсивность сепии, `Resize`: два новых размера, `Vignette`: радиус круга и скорость затемнения, `Pixelization`: размер блока и перемешивать ли блоки (`True` или `False`)).

## Пример использования

1) Просмотр доступных параметров:
   ```bash
   python lab1.py --help
2) Оттенки серого:
   ```bash
   python lab1.py -m Greyscale -i test_img.jpg
3) Сепия:
   ```bash
   python lab1.py -m Sepia -i test_img.jpg -p 10
4) Изменение размера изображения:
   ```bash
   python lab1.py -m Resize -i test_img.jpg -p 1024,1024
5) Виньетка:
   ```bash
   python lab1.py -m Vignette -i test_img.jpg -p 50,0.01
6) Пикселизация:
   ```bash
   python lab1.py -m Pixelization -i test_img.jpg -p 20,False