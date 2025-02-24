# Наследование свойств

Наследование свойств используется для распространения изменений неизменённых свойств из префаба на его экземпляры. Например, вы можете изменить масштаб узла в префабе, и его экземпляры также будут иметь тот же масштаб, если только масштаб не задан явно в экземпляре. Такая функция позволяет вам настраивать экземпляры, добавлять к ним некоторые уникальные детали, но брать общие свойства из родительских префабов.

Наследование свойств работает для иерархий префабов любой глубины, это означает, что вы можете создать что-то вроде этого: префаб комнаты может содержать несколько экземпляров различных префабов мебели, в то время как префабы мебели также могут быть построены из других префабов и так далее. В этом случае, если вы измените свойство в одном из префабов в цепочке, все экземпляры немедленно синхронизируют свои неизменённые свойства.

## Как создать наследуемые свойства

Можно использовать наследование свойств для переменных скриптов. Чтобы сделать свойство вашего скрипта наследуемым, всё, что вам нужно, — это обернуть его значение с помощью обёртки `InheritableVariable`.

```rust,no_run
{{#include ../code/snippets/src/scene/inheritance.rs:my_script}}
```

Движок автоматически определит правильное значение для свойства при загрузке сцены со скриптом. Если ваше свойство было изменено, то его значение останется прежним, оно не будет перезаписано значением из родительского префаба. Имейте в виду, что тип наследуемой переменной должен быть клонируемым и поддерживать рефлексию.

`InheritableVariable` реализует трейты `Deref<Target = T> + DerefMut`, это означает, что любой доступ через трейт `DerefMut` пометит свойство как изменённое. Это может быть нежелательно в некоторых случаях, поэтому `InheritableVariable` поддерживает специальные методы `xxx_silent`, которые не затрагивают внутренние модификаторы и позволяют вам заменить "незаметно" значение на другое — без пометки переменной как изменённой.

## Какие поля должны быть наследуемыми?

Наследуемые переменные предназначены для хранения "атомарных" данных — это означает, что переменная хранит какое-то простое значение (`f32`, `String`, `Handle<Node>` и т.д.). Хотя возможно хранить "составные" переменные (`InheritableVariable<YourStruct>`), это не рекомендуется из-за механизма наследования. Когда движок видит наследуемую переменную, он ищет ту же переменную в родительской сущности и копирует её значение в дочернюю, полностью заменяя её содержимое. В этом случае, даже если у вас есть наследуемые переменные внутри составного поля, они не будут наследоваться корректно. Давайте продемонстрируем это в следующем фрагменте кода:

```rust,no_run
{{#include ../code/snippets/src/scene/inheritance.rs:complex_inheritance}}
```

Этот фрагмент кода должен прояснить, что наследуемые поля должны содержать "простые" данные и в случае крайней необходимости — сложные структуры.

## Редактор

Редактор оборачивает все наследуемые свойства в специальный виджет, который поддерживает отмену изменений. Отмена позволяет вам сбросить текущие изменения и взять значение свойства из родительского префаба. Это полезно, если вы хотите, чтобы свойство наследовало значение из родительского префаба. В Инспекторе это выглядит так:

![Отмена](./revert.png)

Нажатие на кнопку `<` возьмёт значение из родительского префаба, и свойство больше не будет помечено как изменённое. В случае, если нет родительского префаба, кнопка просто сбросит флаг `modified`.