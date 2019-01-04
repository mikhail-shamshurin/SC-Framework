# SC Framework
SimpleControl Framework - фреймворк, содержащий в себе базовые элементы управления приложением. Фреймворк основан на библиотеке SFML, языка С++.

## Установка
Для работы библиотеки необходимо наличие в проекте установленной, вышеупомянутой, библиотеки SFML. Инструкция по установки библиотеки [здесь](https://www.sfml-dev.org/tutorials/2.5/start-vc.php).

## Начало работы

Подключение осуществляется через заголовок файла: `#include "VirtualControls";`. Далее создайте следующую структуру:

```c++
#include "VirtualControls.h"

using namespace sf;

/*Создание окна*/
RenderWindow window(VideoMode(400, 300), "Testing", Style::Default);

/*Создание объектов*/
Font font;
...
Label label(window, font);

/*Инициализация компонентов*/
void InitializeComponents()
{
	/* Зашрузка шрифта */
   	font.loadFromFile("Consolas.ttf");

	/* Установка свойств для объектов*/
	label.setCaption("Hello, world!");
	...
	Label.setPosition(10, 10);
}

/*Стандартный SFML цикл*/
int main()
{
    InitializeComponents();

    while (window.isOpen())
    {
        Event event;
        while (window.pollEvent(event))
        {
            if (event.type == Event::Closed)
                window.close();
        }

        window.clear(Color::Magenta);
        label.display(); // Выводит надпись
        window.display();
    }
}
```
Данная структура самая оптимальная для использования фреймвока. Глобализация компонентов необходима для более легкой видимости. К примеру, это пригодится при установки событийных методов или процедур.

## Методы

*Comming soon...*

## Пример использования

Ниже представлен простой код счетчика нажатий.

```c++
#include "VirtualControls.h"

using namespace sf;
using namespace std;

RenderWindow window(VideoMode(400, 300), L"Тест", Style::Default, ContextSettings(0, 0, 6));

Font font;
CaptionButton button(window, font); /// Кнопка

/* ПРОЦЕДРУРА ДЛЯ КНОПКИ */
void button_void()
{
	static int clicks = 0;

	++clicks;
	button.setCaption(L"Вы нажали " + to_wstring(clicks) + L" раз.", true); // Изменяет надпись кнопки
}


void InitializeComponents()
{
	/* Зашрузка шрифта */
	font.loadFromFile("Consolas.ttf");

	/* Установка свойств кнопки */
	button.setPosition(10, 15);
	button.setCaptionFont(font);
	button.setCaption(L"Вы нажали 0 раз.", true);
	button.onClick = button_void; // Привязывает процедуру к событию кнопки
}

int main()
{
	InitializeComponents();

	while (window.isOpen())
	{
		Event event;
		while (window.pollEvent(event))
		{
			if (event.type == Event::Closed)
				window.close();

			button.getEvent(event); // Считывает события для кнопки
		}

		window.clear(Color::Magenta);
		button.display(); // Выводит кнопку
		window.display();
	}
}
```
**Вывод**:

![](https://raw.githubusercontent.com/6eremotuk01/SCL-library/master/screenshot.png "Полная версия сайта")
