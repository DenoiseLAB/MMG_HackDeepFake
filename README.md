<p align="center">
  <img src="https://github.com/user-attachments/assets/81cdbc21-3b92-4116-b04c-4a746beb3e53" height="250">
</p>

<h1 align="center">
    Kryptonite ML Challenge<br>
    Команда MMG
</h1>

<br>

## 📝 Оглавление

<ol type="I">
  <li>
    <b>Шапка</b>
    <ul>
      <li><a href="#description">Описание задачи</a></li>
      <li><a href="#demo">Демо</a></li>
      <li><a href="#links">Ссылки</a></li>
      <li><a href="#data">Данные</a></li>
    </ul>
  </li>
  <li>
    <b>Проект</b>
    <ul>
      <li><a href="#report">Отчет</a></li>
      <li><a href="#tech-stack">Технологический стек</a></li>
      <li><a href="#project-structure">Структура проекта</a></li>
    </ul>
  </li>
  <li>
    <b>Установка</b>
    <ul>
      <li><a href="#cloning">Клонирование</a></li>
      <li><a href="#local">Запуск в локальной среде</a></li>
      <li><a href="#container">Запуск в контейнере</a></li>
    </ul>
  </li>
  <li>
    <b>Запуск скриптов</b>
    <ul>
      <li><a href="#inference">Инференс</a></li>
      <li><a href="#inference-page">Инференс на веб-сайте</a></li>
      <li><a href="#training">Обучение моделей</a></li>
      <li><a href="#new-dataset">Использование другого датасета</a></li>
      <li><a href="#clean-dataset">Отчистка датасета</a></li>
      <li><a href="#onnx">Конвертация в onnx</a></li>
    </ul>
  </li>
  <li>
    <b>Планы на будущее</b>
    <ul>
      <li><a href="#scaling">Масштабирование системы</a></li>
    </ul>
  </li>
</ol>

<a id="description"></a>
## 🧐 Описание задачи
Поддельные изображения и видео, созданные с помощью технологии DeepFake, представляют угрозу для цифровой безопасности. Они могут быть настолько реалистичными, что их сложно отличить от настоящих.

Предстоит создать модель распознавания лиц, которая должна уметь:

* Сравнивать реальные фотографии одного и того же человека
* Различать снимки разных людей
* Распознавать фальшивые изображения, созданные с помощью DeepFake-технологий, без использования модулей защиты от спуфинга

<a id="demo"></a>
## 🎥 Демо
Демо решения запущено на ноутбуке с GeForce GTX 960M (2015г), протестировать его можно [тут](http://5.35.46.26:14500)

Мы постараемся обеспечить 100% uptime на период тестирования и до завершения хакатона, однако могут возникнуть некоторые сложности, связанные аппаратной частью.

<div align="center">
  <img src="https://github.com/user-attachments/assets/1b655ab0-f6b3-480c-bc7f-4e3fc93a1b07" alt="demo" width="100%">
</div>

<a id="links"></a>
## 🔗 Ссылки
**Лендинг:** [kryptonite-ml.ru](https://kryptonite-ml.ru)  
**Репозиторий:** [git.codenrock.com/kryptonite-ml-challenge-1347](https://git.codenrock.com/kryptonite-ml-challenge-1347)  
**Тестирующая система:** [codenrock.com/contests/kryptonite-ml-challenge](https://codenrock.com/contests/kryptonite-ml-challenge)

<a id="data"></a>
## 📁 Данные
Перед началом работы необходимо загрузить данные и разместить их в папке `data`. 

- **Исходные данные для обучения:** [Скачать по ссылке](https://storage.codenrock.com/companies/codenrock-13/contests/kryptonite-ml-challenge/train.zip)
- **Очищенные данные для обучения:** [Скачать по ссылке](https://drive.google.com/file/d/193Vi9JBxdfLlV32nrw8hb-rls4BTpIkU/view?usp=sharing)
- **Данные для претрейна:** [Скачать по ссылке](https://drive.google.com/file/d/1muyIwX8c35Bl0OQTfmETGVjBevk3S6CK/view?usp=sharing)
- **Данные для теста:** [Скачать по ссылке](https://storage.codenrock.com/companies/codenrock-13/contests/kryptonite-ml-challenge/test_public.zip)

<a id="report"></a>
## 📄 Отчёт
Отчёт проделанном исследовании можно найти в файле [Research-Report-MMG.pdf](Research-Report-MMG.pdf).

В нём описаны основные моменты по всей работе и наши умозключения.

<a id="tech-stack"></a>
## 🛠️ Технологический стек
- **Система:** Ubuntu 22.04
- **Инструменты контейнеризации:** Docker
- **Системы управления зависимостями:** conda, pip
- **Язык программирования:** Python 3.12.0
- **Глубокое обучение:** PyTorch
- **Работа с данными:** Transformers, TorchVision, OpenCV, NumPy, SciPy, timm
- **Веб-составляющая:** HTML, CSS, JavaScript, FastAPI, Uvicorn
- **Экспорт и инференс:** ONNX Runtime
- **CLI и утилиты:** argparse, tqdm

<a id="project-structure"></a>
## 📑 Структура проекта
```nushell
.
├── aligner <----------------------------- Модуль для выравнивания лиц
│   ├── aligners
│   ├── config.json <--------------------- Конфигурационный файл
│   ├── pretrained_model <---------------- Тут лежит предобученная модель для выравнивания
│   │   └── model.yaml
│   └── wrapper.py <---------------------- Обёртка для взаимодействия с моделью выравнивания
├── data <-------------------------------- Данные для обучения и тестирования
│   ├── test_public
│   └── train
├── models <------------------------------ Модели верификации
│   ├── checkpoints <--------------------- Контрольные точки обучения
│   ├── pretrained <---------------------- Предобученные модели
│   ├── onnx <---------------------------- Модели в формате ONNX
│   └── download_pretrained_models.py <--- Скрипт для скачивания моделей
├── scripts <----------------------------- Различные скрипты
│   ├── convert.py <---------------------- Скрипт конвертации моделей в ONNX
│   ├── inference.py <-------------------- Скрипт для инференса
│   └── utils <--------------------------- Вспомогательные модули
│       ├── net.py <---------------------- Определение архитектуры
│       └── utils.py <-------------------- Утилиты общего назначения
├── train <------------------------------- Тренировка модели
│   ├── align.py <------------------------ Скрипт дял предобработки изображений (alignment, resize)
│   ├── generate_pairs.py <--------------- Скрипт для создания пар для трейна и валидации
│   ├── train.py <------------------------ Основной цикл тренировки, логирования и сохранения чекпоинтов
│   ├── leaderboard.ipynb <--------------- Оценка сохраненных чекпоинтов
│   ├── compute_similarities.py <--------- Скрипт для подчёта косинусного сходства между изображениями в папках
│   └── clean_data.py <------------------- Алгоритм создания нового очищенного датасета
├── notebooks
│   ├── embeding_visualization.ipynb <---- Визуализация эмбедингов
│   ├── model-attack.ipynb <-------------- Атаки на модель
│   └── <---------------
├── web <--------------------------------- Веб-интерфейс
│   ├── main.py <------------------------- Основной скрипт веб-сервиса
│   └── static <-------------------------- Статические файлы
│       ├── images
│       ├── index.html
│       └── ...
├── submissions <------------------------- Папка для сабмитов
├── Research-Report-MMG.pdf <------------- PDF Отчет о проделанном исследовании
├── Presentation-MMG.pdf <---------------- Презентация
├── docker-compose.yaml <----------------- Конфигурация для docker-compose
├── Dockerfile
├── environment.yml <--------------------- Список зависимостей Conda
├── LICENSE
├── README.md <--------------------------- Документация и инструкция по использованию
├── .dockerignore
└── .gitignore
```

<a id="cloning"></a>
## 📋 Клонирование
```nushell
git clone https://github.com/kekwak/Kryptonite-ML-Challenge.git
cd Kryptonite-ML-Challenge
```

<a id="local"></a>
## 💻 Запуск в локальной среде
В проекте используется анаконда.

*При установке зависимостей этим способом могут возникнуть проблемы.

```nushell
conda env create -f environment.yml && conda activate krypto
conda install conda-forge::onnxruntime
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126 --force-reinstall
pip3 install numpy==2.2.3
```

<a id="container"></a>
## 🐳 Запуск в контейнере
Собрать контейнер самому:
```nushell
docker compose run --rm -it --service-ports app
```
*На данном шаге придется немного подождать...

Как только все создастся, активируйте среду для запуска скриптов:
```nushell
conda activate krypto
```
После этого можно запускать проект в контейнере.

<a id="inference"></a>
## 🚀 Инференс

Для начала нужно скачать обученную модель с гугл диска. Это можно сделать вручную или использовать скрипт для загрузки моделей без аргумента `--all`:
```nushell
python3 models/download_pretrained_models.py
```

Публичный или приватный датасет нужно разместить в папке **data**, вот таким образом:
```nushell
data
└── test_public
   └── images
       ├── 00000000
       │   ├── 0.jpg
       │   └── 1.jpg
       ├── 00000001
       │   ├── 0.jpg
       │   └── 1.jpg
       ├── ...
       ...
```

Как только предыдущие шаги будут выполнены, можно приступать к инференсу. Он запускается следующей командой:
```nushell
python3 scripts/inference.py --model models/onnx/ckpt_epoch1_batch6100_acc0.9831_eer0.0165.onnx
```
В аргументах достаточно указать только модель, но также есть возможность указать другую папку с изображениями с помощью аргумента `--input_dir data/path/to/images`.

*В инференсе используется [aligner](https://huggingface.co/minchul/cvlface_DFA_resnet50) для обрезания и выравнивания изображений.

<a id="inference-page"></a>
## 🌐 Инференс на веб-сайте

Скачиваем все предобученные модели с гугл диска:
```nushell
python3 models/download_pretrained_models.py --all
```

Переходим в директорию `web` и запускаем наш сервер:
```nushell
cd web && python3 -m uvicorn main:app --host 0.0.0.0 --port 8000
```
Веб-страничка будет доступна по ссылке [0.0.0.0:8000](http://0.0.0.0:8000).

<a id="training"></a>
## 📚 Обучение моделей

Перед началом обучения нужно скачать все предобученные модели с гугл диска. Это можно сделать вручную или использовать скрипт для загрузки моделей с аргументом `--all`:
```nushell
python3 models/download_pretrained_models.py --all
```
Уже скачанные модели перезапишутся.

Обучающий датасет нужно разместить в папке **data**, вот таким образом:
```nushell
data
└── train
   ├── meta.json
   └── images
       ├── 00000000
       │   ├── 0.jpg
       │   ├── 1.jpg
       │   └── ...
       ├── 00000001
       │   ├── 0.jpg
       │   ├── 1.jpg
       │   └── ...
       ├── ...
       ...
```

После требуется выровнять входные изображения и привести к нужному формату, используем данный скрипт:
```nushell
python3 train/align.py
```

Запускаем алгоритм генерации пар для обучения и валидации:
```nushell
python3 train/generate_pairs.py
```

Важно упомянуть, что ко всем исполняемым файлам приведена соответсвующая документация и гибкая настройка параметров, вызвать её можно при например так:
```nushell
python3 train/generate_pairs.py --help
```
```nushell
usage: generate_pairs.py [-h] [--meta_path META_PATH] [--images_root IMAGES_ROOT] [--train_split TRAIN_SPLIT] [--output_train OUTPUT_TRAIN] [--output_val OUTPUT_VAL]

Генерация пар изображений для train и val наборов на основе meta.json и изображений.

options:
  -h, --help            show this help message and exit
  --meta_path META_PATH
                        Путь к файлу meta.json
  --images_root IMAGES_ROOT
                        Путь к корневой папке изображений
  --train_split TRAIN_SPLIT
                        Доля людей, отведённая под train (остальные – val)
  --output_train OUTPUT_TRAIN
                        Путь для сохранения CSV файла с train парами
  --output_val OUTPUT_VAL
                        Путь для сохранения CSV файла с val парами
```
Параметры, требуемые для тестового запуска, уже настроены по умолчанию.

Когда все предыдущие шаги будут выполнены, можно приступать к самому обучению, оно запускается так:
```nushell
python3 train/train.py
```

Оценку на валидации и остальные метрики можно смотреть на страничке wandb.

Для более удобного определения победителей существует файлик [leaderboard.ipynb](train/leaderboard.ipynb).

Выбор лучшей модели можно делать в основном по EER на 1-2й эпохах обучения.

Логика сохранения чекпоинтов заключается в:
- сохранении модели только в том случае, если она попадает в топ-5 хотя бы по одной метрике
- совместно с этим информация логируется в `leaderboard.csv`

<a id="new-dataset"></a>
## 📦 Использование другого датасета

В случае, если требуется заменить базовый датасет на какой-либо другой, придётся повторить все шаги из <a href="#training">обучения</a>, кроме скачивания моделей.

Мы возьмём очищенный датасет из секции <a href="#data">данных</a>, на котором обучалась наша финальная модель.

Скачиваем его по ссылке и размещаем его таким же образом как и train датасет.

Изображения в нём были предварительно выровнены, поэтому шаг с выравниванием пропускаем

В ином случае, к `python3 train/align.py` нужно указать аргумент – путь до папки с изображениями, к примеру `--input_dir data/train/images_new_data`.

Подсказка:
```nushell
python3 train/align.py --help
```
```nushell
usage: align.py [-h] [--input_dir INPUT_DIR] [--output_dir OUTPUT_DIR]

Выравнивание датасета изображений и сохранение выровненных копий.

options:
  -h, --help            show this help message and exit
  --input_dir INPUT_DIR
                        Путь к исходной директории с изображениями
  --output_dir OUTPUT_DIR
                        Путь для сохранения выровненных изображений
```

Теперь нужно сгенерировать пары, выведем подсказку:
```nushell
python3 train/generate_pairs.py --help
```
```nushell
usage: generate_pairs.py [-h] [--meta_path META_PATH] [--images_root IMAGES_ROOT]
                         [--train_split TRAIN_SPLIT] [--output_train OUTPUT_TRAIN]
                         [--output_val OUTPUT_VAL]

Генерация пар изображений для train и val наборов на основе meta.json и изображений.

options:
  -h, --help            show this help message and exit
  --meta_path META_PATH
                        Путь к файлу meta.json
  --images_root IMAGES_ROOT
                        Путь к корневой папке изображений
  --train_split TRAIN_SPLIT
                        Доля людей, отведённая под train (остальные – val)
  --output_train OUTPUT_TRAIN
                        Путь для сохранения CSV файла с train парами
  --output_val OUTPUT_VAL
                        Путь для сохранения CSV файла с val парами
```

И сделаем это, указав все нужные параметры:
```nushell
python3 train/generate_pairs.py \
    --meta_path data/train/meta_filtered.json \
    --images_root data/train/images_aligned_filtered \
    --output_train data/train/train_pairs_filtered.csv \
    --output_val data/train/val_pairs_filtered.csv
```

Отлично! Кода пары сгенерировались, можно приступать к обучению.

Таким же образом укажем аргументы для `train.py`.

Подсказочка:
```nushell
python3 train/train.py --help
```
```nushell
usage: train.py [-h] [--checkpoint CHECKPOINT] [--train_csv TRAIN_CSV] [--val_csv VAL_CSV]
                [--epochs EPOCHS] [--batch_size BATCH_SIZE]
                [--learning_rate LEARNING_RATE]
                [--checkpoint_interval CHECKPOINT_INTERVAL] [--s S]
                [--base_margin BASE_MARGIN] [--dynamic_scale DYNAMIC_SCALE]
                [--weight_decay WEIGHT_DECAY] [--architecture ARCHITECTURE]

Обучение модели AdaFace с CSV-датасетом и Adaptive Margin Loss.

options:
  -h, --help            show this help message and exit
  --checkpoint CHECKPOINT
                        Путь к файлу чекпоинта модели.
  --train_csv TRAIN_CSV
                        Путь к CSV файлу с тренировочными парами.
  --val_csv VAL_CSV     Путь к CSV файлу с валидационными парами.
  --epochs EPOCHS       Количество эпох обучения.
  --batch_size BATCH_SIZE
                        Размер батча для обучения.
  --learning_rate LEARNING_RATE
                        Скорость обучения для оптимизатора.
  --checkpoint_interval CHECKPOINT_INTERVAL
                        Интервал (в батчах) для сохранения чекпоинтов.
  --s S                 Параметр масштабирования для Adaptive Margin Loss.
  --base_margin BASE_MARGIN
                        Базовый margin для Adaptive Margin Loss.
  --dynamic_scale DYNAMIC_SCALE
                        Динамический scale для Adaptive Margin Loss.
  --weight_decay WEIGHT_DECAY
                        Weight decay для оптимизатора.
  --architecture ARCHITECTURE
                        Архитектура модели: 'ir_101' или другая.
```

А вот так запускаем само обучение:
```nushell
python3 train/train.py \
    --train_csv data/train/train_pairs_filtered.csv \
    --val_csv data/train/val_pairs_filtered.csv
```

Данных аргументов будет достаточно чтобы запустить обучение на очщенных данных.

Должно выйти что-то похожее:

![image_2025-03-09_19-13-22](https://github.com/user-attachments/assets/96183615-4b56-4771-b77a-34b8b12f718b)

<a id="clean-dataset"></a>
## 🧹 Отчистка датасета

А теперь о самой отчистке датасета.

Для выполнения этой задачи, мы составили 2 скрипта.

- train/compute_similarities.py – скрипт для подчёта косинусного сходства между изображениями в папках
- train/clean_data.py – алгоритм создания нового очищенного датасета

Считаем сходство:
```nushell
python3 train/compute_similarities.py
```

В папку data формируется файл cosine_similarity_results.npz.

Далее запускаем скрипт для отчистки датасета:
```
python3 train/clean_data.py
```

В данном случае алгоритм на графовой основе кластеризует изображения по косинусному сходству.

После датасет пересобирается, с возможностью ручной проверки и исправления ошибок.

<a id="onnx"></a>
## 🔄 Конвертация в onnx

Для конвертации обученной модели в onnx формат достаточно использовать команду:
```nushell
python3 scripts/convert.py --checkpoint path/to/model.ckpt --output_model path/to/onnx_model.onnx
```

<a id="scaling"></a>
## 📈 Масштабирование системы
- Использование более продвинутых и современных DeepFake и FaceSwap моделей
- Увеличение количества обучающих данных
- Верификация личности в реальном времени с помощью эталонных изображений
