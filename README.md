Когда завершите задачу, в этом README опишите свой ход мыслей: как вы пришли к решению, какие были варианты и почему выбрали именно этот. 

# Что нужно сделать

Реализовать интерфейс с методом для проверки правил флуд-контроля. Если за последние N секунд вызовов метода Check будет больше K, значит, проверка на флуд-контроль не пройдена.

- Интерфейс Check располагается в файле main.go.

- Флуд-контроль может быть запущен на нескольких экземплярах приложения одновременно, поэтому нужно предусмотреть общее хранилище данных. Допустимо использовать любое на ваше усмотрение. 

# Необязательно, но было бы круто

Хорошо, если добавите поддержку конфигурации итоговой реализации. Параметры — на ваше усмотрение.

# Использовал

- Redis
- Godotenv
- Cleanenv

# Ход мыслей

- Задача реализовать флуд-контроль. Значит, нам нужна очень высокая скорость проверки, а так же очищение количества 
вызовов от пользователя через N-ое время. Сразу на ум приходит Redis. Вся информация хранится в ОЗУ, что обеспечивает
быстродействие, и можно выставить expire при вставке. Будем использовать его.
- Как мы будем работать с Редисом? Паттерн репозиторий - основной способ работы с любым хранилищем данных. В случае
необходимости сможем потом быстро сменить Редис на любую другую базу данных.
- Где будем реализовывать интерфейс FloodControl? По сути это может являться логикой кого-то сервиса, поэтому создам
отдельный сервис, который в случае чего можно будет встроить куда-либо. 
- Как будем конфигурировать все это? Я выбрал .env для секрет инфы и .yaml для обычной. Приятнее работать с .yaml
при настройке конфигурации. При помощи godotenv подгружаем .env и при помощи cleanenv парсим конфиг из файла.

