
# Project Yolo V3
<p align="center">
   <img src="https://media.giphy.com/media/VYPDYUBR9bGEIYtz5s/giphy.gif?cid=ecf05e47pdggmnkmdmfzgcp00hq8cg5nmxrnb2w5m8e8c36t&ep=v1_gifs_search&rid=giphy.gif&ct=g" width="300">
</p>

## About (Eng)



## About (Rus)
* Цель:
Создать нейронную сеть для детектирования объектов на изображении. Это тренировочный проект для работы с компьютерным зрением и библиотеками tensorflow.
* Результат:
Была создана нейронная сеть, способная определять 80 классов на изображении с хорошей точностью (~ 85%) и работать достаточно быстро.

Пример работы:

Входное изображение:

Обработанное изображение:

YOLO – это передовая сеть для распознавания объектов (object detection)
* YOLO может обнаруживать сразу несколько объектов, предсказывать классы и идентифицировать объекты на изображении.
* В YOLO, распознавание объектов было реализовано как задача регрессии к раздельным ограничивающим рамкам, с которыми связаны вероятности принадлежности к разным классам.
* Поскольку YOLO смотрит на изображение только один раз, плавающее окно – это неправильный подход. Вместо этого, все изображение разбивается с помощью сетки на ячейки размером 𝑆∗𝑆. После этого каждая ячейка отвечает за предсказание нескольких вещей
* В YOLO для предсказания содержащих рамок используются якорные рамки (anchor boxes). 
Якоря были рассчитаны на датасете COCO с помощью k-means кластеризации. Всего сеть распознает 80 классов объектов
* YOLO использует 53 CNN слоя (darknet-53) и соединены с ещё 53-мя слоями. В сумме 106 слоев, где 3 слоя отвечают за обнаружение (82,94,106)
* Версия 3 включает в себя несколько важных элементов. А именно: residual blocks (остаточные блоки), skip connections (пропуск соединений), и up-sampling (повышение частоты дискретизации). За каждым сверточным слоем (CNN) следует слой batch normalization (пакетная нормализации), Leaky ReLu (функция активации релу).

Для создания модели YOLOv3 (You Only Look Once Version 3) ключевые компоненты включают в себя:
* Реализацию на Python, используя фреймворк глубокого обучения TensorFlow.
* Реализацию алгоритма якорных рамок и подавления не-максимумов.
* Берём готовые веса DarkNet из оригинальной тренированной модели.
* Подачу изображения на вход и выход обработанного изображения.

Дополнительная информация:
* На вход сети подаются изображения формы (n, 416, 416, 3), где n-кол-во изображений,  416- ширина и высота изображений, 3 -  кол-во каналов цветов (rgb). Размер изображений можно менять, но он должен делиться на 32 без остатка (608, 1024 и т.д)
* Пример работы якорей для предсказания:

![image](https://github.com/InfinityBlazze/YoloV3CV/assets/131138862/21d56247-c8f2-4940-99ed-b4f7f6874f71)

* Далее сеть проходит по изображению и создает по 3 рамки на каждый объект. Испуользуя функцию nonMaximumSuppression мы отбрасываем рамки с наименьшим процентов вероятности и выводим рамку с объектом, где наибольшая увернность (соотношение каждой рамки).

![image](https://github.com/InfinityBlazze/YoloV3CV/assets/131138862/2069f460-e1c0-4ddc-9a39-d5f1a35f051a)
    
* На выходе мы получаем обработанное изображение с рамкой, уверенностью (в %) и названием объекта.
