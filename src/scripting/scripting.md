# Скриптинг

Игра, основанная на Fyrox, является плагином для движка и редактора. Плагин определяет глобальную логику приложения и может предоставлять набор скриптов, которые можно использовать для назначения пользовательской логики узлам сцены. Каждый скрипт может быть привязан только к одному плагину.

Fyrox использует скрипты для создания пользовательской игровой логики. Скрипты могут быть написаны только на Rust, что гарантирует, что ваша игра будет стабильной, быстрой и легко рефакторимой.

Общая структура плагинов и скриптов может быть описана следующей диаграммой:

![Структура](structure.svg)

Следующие главы охватят все части и помогут вам научиться правильно использовать плагины и скрипты.