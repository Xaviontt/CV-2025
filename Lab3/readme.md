# Лабораторная 3: Метод распознавания примесей в составе зерновой продукции с использованием сверточной нейронной сети и спектроскопии

## Теоретическая база
В задаче бинарной классификации мы имеем два класса. Обычно мы обозначаем один класс как положительный (1), а другой как отрицательный (0). Модель должна научиться различать эти два класса.
CNN особенно хорошо подходят для задач классификации изображений, потому что они способны улавливать пространственные иерархии признаков.

Основные компоненты CNN:
1. Сверточные слои (Conv2d): применяют фильтры (ядра) к входному изображению для извлечения признаков. Каждый фильтр скользит по изображению и вычисляет скалярное произведение между своими весами и соответствующими значениями пикселей.
3. Пулинг слои (MaxPool2d): уменьшают размерность карт признаков, сохраняя наиболее важную информацию (например, максимальное значение в окне). Это помогает уменьшить количество параметров и вычислительную сложность, а также обеспечивает инвариантность к небольшим смещениям.
4. Полносвязные слои (Linear): после сверточных и пулинг слоев, карты признаков выравниваются и передаются в полносвязные слои для классификации.

## Описание разработанной системы
### Датасет
Изображения снимаются в двух диапазонах RBG и NIR  
Все изображения приведены к формату 100х200  
Собран датасет который составляет:
- Амброзия - 44102 изображений  
- Бодяк - 45846 изображений  
- Горчак - 45137 изображений  
<img width="848" height="505" alt="image" src="https://github.com/user-attachments/assets/29ea1eab-6041-40a2-8e7d-da81f2e67ae9" />
<img width="1003" height="990" alt="image" src="https://github.com/user-attachments/assets/3dca1902-c1f4-4a7d-870d-aa7defbfa577" />
<img width="1003" height="990" alt="image" src="https://github.com/user-attachments/assets/34a1f0b2-479f-488e-91a4-9ed4bbd3a3e9" />


### Архитектура
Четыре сверточных блока, каждый из которых состоит из свертки, пулинга и активации ReLU.  
Три полносвязных слоя, причем последний выдает два нейрона (по одному на каждый класс).  
Метрика: accuracy  
ModelCheckpoint для сохранение лучшей модели
```
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
ConvNetWheat                             [1, 2]                    --
├─Conv2d: 1-1                            [8, 98, 198]              224
├─Conv2d: 1-2                            [16, 47, 97]              1,168
├─Conv2d: 1-3                            [16, 21, 46]              2,320
├─Conv2d: 1-4                            [8, 8, 21]                1,160
├─Linear: 1-5                            [1, 256]                  82,176
├─Linear: 1-6                            [1, 256]                  65,792
├─Linear: 1-7                            [1, 2]                    514
==========================================================================================
Total params: 153,354
Trainable params: 153,354
Non-trainable params: 0
Total mult-adds (Units.MEGABYTES): 4.22
==========================================================================================
Input size (MB): 0.24
Forward/backward pass size (MB): 1.96
Params size (MB): 0.61
Estimated Total Size (MB): 2.82
==========================================================================================
```

## Список используемой литературы
1. Shen Y. et al. Detection of impurities in wheat using terahertz spectral imaging and convolutional neural networks //Computers and Electronics in Agriculture. – 2021. – Т. 181. – С. 105931.
2. Li G. et al. Research on wheat impurity identification method based on terahertz imaging technology //Spectrochimica Acta Part A: Molecular and Biomolecular Spectroscopy. – 2025. – Т. 326. – С. 125205.
3. Shen Y. et al. Image recognition method based on an improved convolutional neural network to detect impurities in wheat //IEEE access. – 2019. – Т. 7. – С. 162206-162218.
4. AgaAzizi S. et al. Identification of impurity in wheat mass based on video processing using artificial neural network and PSO algorithm //Journal of Food Processing and Preservation. – 2021. – Т. 45. – №. 1. – С. e15067.
5. Ebrahimi E., Mollazade K., Babaei S. Toward an automatic wheat purity measuring device: A machine vision-based neural networks-assisted imperialist competitive algorithm approach //Measurement. – 2014. – Т. 55. – С. 196-205.

