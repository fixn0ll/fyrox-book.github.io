# Трансформация

Трансформация — это специальная сущность, которая изменяет систему координат из одной в другую. Она используется в основном в узлах сцены для хранения их положения/вращения/масштаба/опорных точек и т.д. Fyrox имеет довольно сложные трансформации, которые поддерживают:

1) Позицию (`T`)
2) Вращение (`R`)
3) Масштаб (`S`)
4) Предварительное вращение (`Rpre`)
5) Пост-вращение (`Rpost`)
6) Опорную точку вращения (`Rp`)
7) Смещение вращения (`Roff`)
8) Смещение масштабирования (`Soff`)
9) Опорную точку масштабирования (`Sp`)

Итоговая матрица трансформации будет `Transform = T * Roff * Rp * Rpre * R * Rpost * Rp⁻¹ * Soff * Sp * S * Sp⁻¹`. В 99.9% случаев первых трёх компонентов достаточно для практически любой задачи. Остальные шесть компонентов используются для специфических задач (в основном для узлов, импортированных из формата FBX).