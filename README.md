# KittyFakeCamera
- это приватный репозиторий, содержащий код и прочие ресурсы приложения "Kitty Fake Camera" *(название рабочее)*.
Проект разрабатывается на языке C++.

### Репозиторий содержит:
* файлы кода;
* графические ресурсы;
* текст;

### Примеры содержимого репозитория:

Пример кода:
```
 // drawing mouse on top
        if (is_mouse_on_top) {
            window.draw(mouse);
        }

        // drawing arms
        sf::VertexArray fill(sf::TriangleStrip, 26);
        for (int i = 0; i < 26; i += 2) {
            fill[i].position = sf::Vector2f(pss2[i], pss2[i + 1]);
            fill[i + 1].position = sf::Vector2f(pss2[52 - i - 2], pss2[52 - i - 1]);
            fill[i].color = sf::Color(paw_r, paw_g, paw_b, paw_a);
            fill[i + 1].color = sf::Color(paw_r, paw_g, paw_b, paw_a);
        }
        window.draw(fill);

        // drawing first arm arc
        int shad = paw_edge_a / 3;
        sf::VertexArray edge(sf::TriangleStrip, 52);
        double width = 7;
        sf::CircleShape circ(width / 2);
        circ.setFillColor(sf::Color(paw_edge_r, paw_edge_g, paw_edge_b, shad));
        circ.setPosition(pss2[0] - width / 2, pss2[1] - width / 2);
        window.draw(circ);
        for (int i = 0; i < 50; i += 2) {
            double vec0 = pss2[i] - pss2[i + 2];
            double vec1 = pss2[i + 1] - pss2[i + 3];
            double dist = hypot(vec0, vec1);
            edge[i].position = sf::Vector2f(pss2[i] + vec1 / dist * width / 2, pss2[i + 1] - vec0 / dist * width / 2);
            edge[i + 1].position = sf::Vector2f(pss2[i] - vec1 / dist * width / 2, pss2[i + 1] + vec0 / dist * width / 2);
            edge[i].color = sf::Color(paw_edge_r, paw_edge_g, paw_edge_b, shad);
            edge[i + 1].color = sf::Color(paw_edge_r, paw_edge_g, paw_edge_b, shad);
            width -= 0.08;
        }
        double vec0 = pss2[50] - pss2[48];
        double vec1 = pss2[51] - pss2[49];
        dist = hypot(vec0, vec1);
        edge[51].position = sf::Vector2f(pss2[50] + vec1 / dist * width / 2, pss2[51] - vec0 / dist * width / 2);
        edge[50].position = sf::Vector2f(pss2[50] - vec1 / dist * width / 2, pss2[51] + vec0 / dist * width / 2);
        edge[50].color = sf::Color(paw_edge_r, paw_edge_g, paw_edge_b, shad);
        edge[51].color = sf::Color(paw_edge_r, paw_edge_g, paw_edge_b, shad);
        window.draw(edge);
        circ.setRadius(width / 2);
        circ.setPosition(pss2[50] - width / 2, pss2[51] - width / 2);
        window.draw(circ);
```

Пример графического ресурса:
![Image](https://github.com/StupidMoth/UnderTheGravestone/blob..)

## На какой стадии разработки находится проект?
Завершен.

## Кто занимается разработкой игры?
Разработкой занимаются 2 человека, среди них:
* Я - в качестве программиста и художника;
* Antony - в качестве худоника.
