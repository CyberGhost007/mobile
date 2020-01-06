# Сatalog app

## Легаси версия. Актуальная [тут, как и демо со скринами][CatalogAppBloc]. Важная с точки зрения истории.

После прохождения [теста][FirstApp], весь сентябрь занимался разработкой учебного приложения с использованием старой архитектуры версии Clean, практикуемой в [организации][Pmobi]. Основной идеей прилжения является создание каталога интернет магазина. Учебное приложения не только позволило заложить во мне фундамент для дальнейшего развития, но произвести апробацию пары архитектруных идей: 
 - Внедрение ORM-слоя. Полуголые запросы в репозиториях предоставляют недостаточную абстракцию с точки зрения бизнес-логики. Хочется оперерировать понятиями и действиями используемые сущностью, например: проверка срока жизни кэша товаров из каталога, добавление товара в корзину. Поиск готовых решений, показал, что ничего интересного отчего стоило бы зависить нет. К тому же достаточно сложная сущность как товар в итоге реализации потянула пару маперов.
 - Внедрение BLoC. Текущая реализация управления состояними не позволяла в должной мере отделить данные от методов связанных с рендером вёрстки в экране. По простому данные были в вёрстке. Другим недостатком была реализация смена состояний посредством callback-ов и вызова set-state для обновления данных.
 
  В этом репозитории содержится реализация **ORM-слоя** и других функций, что-то я пролобировал, а что коллеги: 
  
<details>
 <summary>Список всего что было сделано</summary>
 
  1. Авторизация. Вход возможен при вводе любых строк, кроме пустых строк;
  2. В приложении сведены к минимуму резкие переходы, поэтому есть лоадеры, fade-эффект, даже для отсутвующих данных, например пуста корзина, предусмотрена соответвующая вёрсткая;
  3. Запись/чтение данных shared preferences;
  4. Заполнение данными приложение. У нас ведь каталог товаров, реализованы следующие варинты аполнения каталоа: сгенерировать полностью товары локально, с использованием API для получения строк с описанием товара, полноценное получение товаров из REST API;
  5. Изображения для товаров сначала грузились из ассетов, а потом уже из прекрасного интернета, с последующим кэшированием;
  6. Кэширование получаемого товара. Реализован упрощённый, если определённая таблица пуста, значит надо заполнить товарами и потом данные брать оттуда. По началу товары локально генерировались, а потом с сервера поступали. **Эта функция потянула за собой реализацию ORM;**
  7. Добавление в корзину товаров.
  8. Синхронизация отображаемого в корзине и БД. Если пользователь закроет приложение, то его данные не потярются. **Эта функция потянула за собой реализацию ORM;**
  9. Итоговоя сумма набранных в корзине товаров отображается на всех экранах кроме авторизации. Реализовано с помощью Stream;
  10. Диалоговые окна используются в приложении, например: добавление, удаление товаров, обработке исключени;
  11. Есть обработка Exception. В приложении реализована авторская ситема "орёл/решка" - при входе в на экран каталога после авторизации с вероятностью 50% получить диалоговое с шуточным сообщением "Сегодня не ваш день. Пробуйте завтра" или перейти на экран на кталаога. В случае неудачи можно нажать на  кнопку "Повторить";
  12. У товаров есть галлерея;
  13. У товаров есть продавец с краткой информацией;
  14. Есть смена темы;
  15. У приложения есть своя иконка;
  16. Реализован только 1 вариант вёрстки;
  17. Адаптивная вёрстка;
  18. Невозможно изменить вертикальную ориентацию. Реализован 1 вариант вёрстки - пришлось заблокировать смену ориантации, иначе бы парочка  новых багов появилась и внешний вид ухудшился бы;
  
</details>  
  
[Pmobi]:<https://pmobi.ru/>
[CatalogAppBloc]:<https://github.com/iebrosalin/mobile/tree/flutter/catalog_app/bloc>
[FirstApp]:<https://github.com/iebrosalin/mobile/tree/flutter/first_app_flutter>
