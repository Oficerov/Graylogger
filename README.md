# Graylogger
[![License: MIT](https://badgen.net/badge/license/MIT/green)](https://opensource.org/licenses/MIT)
[![repo](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com/Oficerov/graylogger)
[![pypi](https://badgen.net/badge/icon/pypi?color=yellow&icon=pypi&label)](https://pypi.org/project/graylogger/)
![version](https://badgen.net/badge/Version/0.2.5/orange)

Однажды в рабочем процессе мне понадобилось отправлять логи из моего python приложения в graylog.
Перебрав все более-менее нормальные библиотеки для работы с gelp http graylog, не нашел ни одной,
которая бы работала так, как от нее ожидается. Некоторые вообще не шлют логи, другие теряют сообщения.

Тогда, на выходных, я решил написать свой мини-хендлер graylog для библиотеки logging для использования в своих проектах.
Так родилась эта библиотека. Возможно, она сэкономит кому-то несколько часов времени.

### Примеры использования:
Установка пакета из пакетного менеджера производится командой:

    pip install graylogger

Импортирование пакета:

    from graylogger import HTTPHandler

Использование хендлера в библиотеке **logging**:

    logger = logging.getLogger(logger_name)
    logger.setLevel(logging.INFO)
    
    # Пример создания хэндлера graylog располагающегося по адресу: http://yourgraylog.ru:80/gelf
    handler = HTTPHandler(host='yourgraylog.ru', path='/gelf', port=80)
    # Пример добавления кастомного поля
    handler.add_field(name='castom_field_name', content='castom_field_content')
    
    logger.addHandler(handler)
    logger.info('Test message to graylog from graylogger')

---
### Возможные ошибки и их решение:
**Ошибка**:

    socket.gaierror: [Errno 11001] getaddrinfo failed
**Решение**: Скорее всего у вас указан протокол (http:// или https://) в параметре host хендлера. Надо убрать.
Либо допущена ошибка в хосте вашего graylog, проверьте, доступен ли указанный вами хост.


Наиболее актуальное readme [смотрите на github](https://github.com/Oficerov/graylogger)
