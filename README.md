# Описания оповещений

Библиотека предназначена для создания и обработки объектов ОписаниеОповещения.

Основное назначение: использование ОписаниеОповещения как коллбэков функций с ручным вызовом и упрощение портирования 1сного кода на OneScript.

Синтаксис создания объектов максимально приближен к синтаксису 1С:Предприятие 8.

## Возможности

* Задание модуля и процедуры для описания оповещения
* Передача произвольного параметра "ДополнительныеПараметры" в процедуру (опционально)
* Задание обработчиков ошибки при выполнении оповещения (опционально)

## Использование

```bsl
// Подключение библиотеки
#Использовать notify

// Процедура-обработчик описания оповещения.
//
Процедура СообщитьПриветМир(Результат, ДополнительныеПараметры = Неопределено) Экспорт
    Сообщить("Привет, " + ДополнительныеПараметры + "!");
    ВызватьИсключение "Что-то произошло!";
КонецПроцедуры

// Процедура-обработчик ошибки.
//
Процедура ОбработкаОшибки(ИнформацияОбОшибке, СтандартнаяОбработка, ДополнительныеПараметры) Экспорт
    Сообщить("Шеф, усё пропало!");
    Сообщить("Информация об ошибке: " + ИнформацияОбОшибке);
КонецПроцедуры

// Создание объекта ОписаниеОповещения. Аналогично использованию "Новый ОписаниеОповещения("СообщитьПриветМир", ЭтотОбъект)" в 1С.
ОписаниеОповещения = ОписанияОповещений.Создать("СообщитьПриветМир", ЭтотОбъект, "Мир", "ОбработкаОшибки", ЭтотОбъект);

// Выполнение обработки оповещения. Аналогично использованию ВыполнитьОбработкуОповещения(ОписаниеОповещения) в 1С.
ОписанияОповещений.ВыполнитьОбработкуОповещения(ОписаниеОповещения);
```

## Особенности

* Для корректной работы параметра "СтандартнаяОбработка" у Обработчика ошибки требуется OneScript версии 1.0.15.211 и старше.
