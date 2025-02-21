# Исполнитель (Executor)

Исполнитель (Executor) — это простая обёртка, которая управляет вашими игровыми плагинами. Он предназначен для использования в production-сборках вашей игры. Редактор запускает исполнитель в отдельном процессе, когда вы входите в режим игры. По сути, нет существенной разницы между запуском игры из редактора или запуском её как отдельного приложения. Основное отличие заключается в том, что редактор передаёт параметр `scene_path` исполнителю при входе в режим игры.

## Использование

Исполнитель предназначен для того, чтобы быть частью рабочего пространства вашего проекта. Типичный пример его использования может выглядеть так:

```rust,no_run
# extern crate fyrox;
# use fyrox::{
#     core::{pool::Handle, uuid::Uuid},
#     engine::executor::Executor,
#     plugin::{Plugin, PluginConstructor, PluginContext},
#     scene::{Scene},
# };
# struct GameConstructor;
# impl PluginConstructor for GameConstructor {
#     fn create_instance(
#         &self,
#         _scene_path: Option<&str>,
#         _context: PluginContext,
#     ) -> Box<dyn Plugin> {
#         todo!()
#     }
# }
fn main() {
    let mut executor = Executor::new();
    // Зарегистрируйте ваш конструктор игры здесь.
    executor.add_plugin_constructor(GameConstructor);
    executor.run()
}
```

Исполнитель имеет полный доступ к движку и через него к главному окну приложения. Вы можете свободно изменять нужные части, так как `Executor` реализует трейты `Deref<Target = Engine> + DerefMut`, поэтому вы можете использовать его экземпляр как "псевдоним" для экземпляра движка.

Чтобы добавить плагин в исполнитель, просто используйте метод `add_plugin_constructor`, который принимает любую сущность, реализующую трейт `PluginConstructor`.

## Типичные случаи использования

Этот раздел охватывает типичные случаи использования `Executor`.

### Установка заголовка окна

Вы можете установить заголовок окна при создании экземпляра исполнителя:

```rust,no_run
# extern crate fyrox;
# use fyrox::engine::executor::Executor;
# use fyrox::window::WindowAttributes;
# use fyrox::engine::GraphicsContextParams;
# use fyrox::event_loop::EventLoop;
let executor = Executor::from_params(
    EventLoop::new().unwrap(),
    GraphicsContextParams {
        window_attributes: WindowAttributes {
            title: "My Game".to_string(),
            ..Default::default()
        },
        vsync: true,
    },
);
```