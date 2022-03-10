# hse_hw2_chip

Ссылка на Google Colab https://colab.research.google.com/drive/1lLp6Pm0xhhftNN_OtpIsqf_o8o-lgbD8#scrollTo=YZOlAXrpdN1t
Для задания была выбрана клеточная линия - GM12878, гистоновая метка - H3K4me1 (https://www.encodeproject.org/experiments/ENCSR000AKF/):

# Анализ Fastq
После анализа графиков Per base sequence quality и Per tile sequence quality (отмечены как непрошедшие проверку качества), для двух чтений было  проведено подрезание с помощью trimmomatic. Графики до подрезания:
ENCFF000ASM

<img width="843" alt="Снимок экрана 2022-03-04 в 21 14 10" src="https://user-images.githubusercontent.com/93148512/156819940-dec681a4-1ddf-4640-89e6-85f55c90ab9e.png">
<img width="867" alt="image" src="https://user-images.githubusercontent.com/93148512/156820532-7e6dd466-968e-43fc-a62b-a56c6c1de9ed.png">
ENCFF000ATK

<img width="860" alt="Снимок экрана 2022-03-04 в 21 13 46" src="https://user-images.githubusercontent.com/93148512/156819955-08c0fd2e-8045-4dbd-9849-c32c92dbb62c.png">
<img width="873" alt="image" src="https://user-images.githubusercontent.com/93148512/156820492-281f5612-d235-413f-ad7d-ca96b7663cfe.png">

После подрезания:

ENCFF000ASM

<img width="875" alt="image" src="https://user-images.githubusercontent.com/93148512/156820832-b26c5be4-b47c-4d30-926d-d86ffa330b45.png">

ENCFF000ATK

<img width="871" alt="image" src="https://user-images.githubusercontent.com/93148512/156820878-d7f74f68-2d26-4974-ad4c-9d3d9c36e2bb.png">


С эим образцом всё не так идеально, но стало получше:

<img width="892" alt="image" src="https://user-images.githubusercontent.com/93148512/156820961-33f06c6b-b725-4c78-80a8-38f8eae7aa0c.png">
<img width="885" alt="image" src="https://user-images.githubusercontent.com/93148512/156820991-321484dc-e3c1-47b3-9cc2-f600ef9d0c10.png">

Контрольный образец ENCFF000ARK выглядел совсем плохо:
<img width="849" alt="image" src="https://user-images.githubusercontent.com/93148512/156823663-0b2eac1c-bf0d-4ca2-870d-7aaf388e4ded.png">
<img width="868" alt="image" src="https://user-images.githubusercontent.com/93148512/156823693-3c2a3706-0491-4945-a985-b1c5f974009d.png">

 После:
 
 <img width="861" alt="image" src="https://user-images.githubusercontent.com/93148512/156823751-0fdb76ad-55d7-4daa-88fb-cda84afb3d82.png">
 <img width="849" alt="image" src="https://user-images.githubusercontent.com/93148512/156823799-25f9d81f-e53a-42c4-a1ac-be022977bc2e.png">
 
 # Анализ выдачи bowtie

ChIP-seq | Общее количество ридов | Кол-во ридов, которые выравнились уникально | Кол-во ридов, которые выравнились не уникально | Кол-во ридов, которые не выравнились | 
 --- |--- |--- |--- |--- 
ENCFF000ASM_trimmed	 | 40418814	| 1752589 (4.34%) | 5282391 (13.07%)	| 33383834 (82.59%) |
ENCFF000ATK_trimmed | 8383067	 | 354648 (4.23%) | 1148618 (13.70%) | 6879801 (82.07%) |
ENCFF000ARK_trimmed | 6446684	 | 283250 (4.39%) | 942356 (14.62%) | 5221078 (80.99%) |

Так как анализ делался только по одной хромосоме, которая составляет небольшую часть генома человека, процент выравниваний чтений получился относительно маленьким. 

# Сравнение результатов
Диаграммы Венна

![image](https://user-images.githubusercontent.com/93148512/157537412-d3461171-0713-4b9a-ac8f-56bd855ef3f6.png)

![image](https://user-images.githubusercontent.com/93148512/157537444-9ce4ec00-a660-458e-bb82-203c6cc8a9c9.png)

Как можно объяснить различия в количестве пересечений?

Различий нет, но если бы они были, то это потому что при расчете пересечения число участков, имеющихся в первом файле, присутствуют и во втором файле (и наоборот). Отсутствие пересечений связано с тем, что выравнивание производится только на одну хромосому, а не на все (как в ENCODE), поэтому шанс того, что пересечений будет много очень маленький.
