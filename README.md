# Chocolate Competition

В данном исследовании решается задача предсказания рейтинга плитки шоколада на основании данных о нём: процента содержания какао, даты оценки, названия компании, региона происхождения шоколада и других параметров. Так как задача решалась в рамках соревнования на kaggle, основной целью исследования было получить занчение метрики R2 на тестовой выборке более 0.2 (как бы странно это ни звучало) и занять наиболее высокую позицию в таблице лидеров. В качестве основной модели для предсказания был выбран классификатор CatBoost. Выбор обусловлен тем, что в данных содержится множество категориальных признаков и CatBoost хорошо решает задачу их кодирования.

Для достижения наилучшего результата было выполнено следующее:
1. Опробованы различные стратегии заполнения пропусков в данных: уникальным значением и значениями, полученными с помощью многоклассового классификатора CatBoost. Обе модели оказались жизнеспособными и позже я сделал piplines с обеими из них.
2. Разработка новых признаков, таких как более общая локация компании и происхождения какао-бобов, длина и количество специфических символов в названии региона происхождения какао-бобов.
3. Stacking пайплайнов наиболее удачных моделей.

Наиболее интересным этапом работы для меня была разработка собственных классов для предобработки данных и предсказания рейтинга, наследующих соотвтетствующим базовым классам Sklearn. Это было необходимо, так как я принял решения применить Stacking двух наилучших цепочек обработки данных и обучения (с заполнением пропусков CatBoost и уникальными значениями).

В итоге цель получения R2 > 0.2 на тренировочной выборке была достигнута именно с помощью этого подхода с применением линейной регресси, как финальной модели, принимающей на вход в качестве признаков результаты двух пайплайнов.

Ссылка на таблицу лидеров на kaggle:
https://www.kaggle.com/competitions/practical-ml-chocolate/leaderboard
