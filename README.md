# Graylog Handlers
[![License: MIT](https://badgen.net/badge/license/MIT/green)](https://opensource.org/licenses/MIT)
[![repo](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com/Oficerov/graylogger)
[![pypi](https://badgen.net/badge/icon/pypi?color=yellow&icon=pypi&label)](https://pypi.org/project/graylogger/)
![version](https://badgen.net/badge/Version/0.2.1/orange)

Однажды в рабочем процессе мне понадобилось отправлять логи из моего python приложения в graylog.
Перебрав все более-менее нормальные библиотеки для работы с gelp http graylog, не нашел ни одной,
которая бы работала так, как от нее ожидается. Некоторые вообще не шлют логи, другие теряют сообщения.

Тогда, на выходных, я решил написать свой мини-хендлер graylog для библиотеки logger для использования в своих проектах.
Так родилась эта библиотека. Возможно, она сэкономит кому-то несколько часов времени.

### Версии:
 + 0.1.*: Базовый HTTP хендлер для GELF Graylog.
 + 0.2.0: Функционал добавления кастомных полей в HTTP хендлер.
 + 0.2.1: Пакет в pip пакетном менеджере.
 + 0.2.2: Пайплайн автоматической сборки пакета, выкатки релиза после пуша в мастер и прохождения всех тестов.

### Примеры использования:
Установка пакета из пакетного менеджера производится командой:

    pip install graylog

Импортирование пакета:

    import grayloggging

Использование хендлера в библиотеке **logging**:

    logger = logging.getLogger(logger_name)
    logger.setLevel(logging.INFO)
    handler = grayloggging.HTTPHandler(host='yourgraylog.ru', path='/gelf', port=80)
    handler.add_field(name='castom_field_name', content='castom_field_content')
    logger.addHandler(handler)

---
#### Возможные ошибки и их решение:
**Ошибка**:

    socket.gaierror: [Errno 11001] getaddrinfo failed
**Решение**: Скорее всего у вас указан протокол (http:// или https://) в параметре host хендлера. Надо убрать.

