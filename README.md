# Levels Cascade Alerts (LCA)
Levels Cascade Alerts - скрипт, включающий в себя алгоритм поиска каскадов уровней на криптовалютах и отправку сигналов в телеграм-канал.

Телеграм-канал с сигналами: https://t.me/lcalerts

## Использование каскадов уровней

Каскад уровней - несколько близлежащих ценовых уровней. Каждый уровень - это локальный экстремум (хай или лой) в радиусе, задаваемый в настройках к скрипту (<i><b>settings.py</b></i>)

Эти уровни используются в торговле, т.к при пробоях таких уровней часто следует импульсное движение, вызываемое исполнением отложенных заявок (за этими уровнями часто находится ликвидность (стоп-лоссы и ликвидации)). 

Каскад уровней более интересен для торговли, т.к выход ликвидности после пробоя одного уровня может привести к пробою следующего и начинается лавинообразное движение.

![Image alt](https://i.ibb.co/sj3gsmW/34324.png)

<i>Каскады уровней SOLUSDT (28.03.22), ETHUSDT (11.04.22)</i>

## Поиска сигналов

Скрипт каждые 5 минут получает новую свечу с Binance и обновляет датасет, затем находит все локальные неснятые (до которых цена еще не доходила) экстремумы, записывает их в массив и анализирует: 
<ul>
<li>Если до 3-х уровней вверх расстояние от текущей цены ближе, чем до 2-х уровней вниз, то это сигнал в лонг</li>
<li>Если до 3-х уровней вниз расстояние от текущей цены ближе, чем до 2-х уровней вверх, то это сигнал в шорт</li>
</ul>
Если сигнал есть, скрипт отправляет его в телеграм-канал: отрисовывает график и уровни, а также определяет удаленность уровней в % от текущей цены. 
Если такой сигнал уже был отправлен, скрипт будет его пропускать, пока не изменится массив экстремумов

## Установка 
<i>Скрипт работает на версии Python 3.10.2</i>

<ul>
<li>Скачайте архив со скриптом</li>
<li>Создайте виртуальное окружение и установите все необходимые библиотеки из файла <i><b>requirements.txt</b></i></li>
<li>В файле <i><b>settings.py</b></i> укажите свои API ключи (Binance), токен телеграм-бота, id канала и список криптовалют (только Binance Futures), на которых скрипт будет искать сигналы
  </li>
<li>Запустите файл <i><b>lca.py</b></i></li>
</ul>