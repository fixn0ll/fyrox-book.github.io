# Системные требования

Как и любое другое программное обеспечение, Fyrox имеет свои системные требования, которые обеспечат наилучший пользовательский опыт.

- **Процессор (CPU)** — как минимум 2-ядерный процессор с частотой 1,5 ГГц на каждое ядро. Чем больше, тем лучше.
- **Видеокарта (GPU)** — любая относительно современная видеокарта с поддержкой OpenGL 3.3+. Если редактор не запускается, скорее всего, ваша видеокарта не поддерживает OpenGL 3.3+. **Не** пытайтесь запускать редактор на виртуальных машинах, так как большинство из них имеют ограниченную поддержку графических API, что не позволит запустить редактор.
- **Оперативная память (RAM)** — как минимум 1 Гб оперативной памяти. Чем больше, тем лучше.
- **Видеопамять (VRAM)** — как минимум 256 Мб видеопамяти. Это сильно зависит от вашей игры.

## Поддерживаемые платформы

| Платформа   | Движок | Редактор |
|-------------|--------|----------|
| Windows     | ✅      | ✅        |
| Linux       | ✅      | ✅        |
| macOS       | ✅¹     | ✅        |
| WebAssembly | ✅      | ❌²       |
| Android     | ✅      | ❌²       |
| iOS         | ✅      | ❌²       |

- ✅ — поддержка первого класса
- ❌ — не поддерживается
- ¹ — на macOS наблюдается низкая производительность GPU на чипсетах Intel, на M1+ работает хорошо.
- ² — редактор работает только на PC, так как требует расширенных возможностей файловой системы и поддержки многопоточности.