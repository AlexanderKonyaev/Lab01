# Lab01
# Лабораторная работа №1
Изучение утилит для разработки проектов

## Tutorial
Сначала зададим нужные переменные для работы в терминале и с github
```sh
$ export GITHUB_USERNAME=AlexanderKonyaev
$ export GIST_TOKEN=<мой токен>
$ alias edit=nano
```

Далее создаем рабочую директорию проекта
```sh
$ mkdir -p ${GITHUB_USERNAME}/workspace
$ cd ${GITHUB_USERNAME}/workspace
$ pwd
```

команда `pwd` вернула следующее: `/mnt/c/Users/user/AlexanderKonyaev/workspace`

Далее создаем директории для заданий, проектов и отчетов внутри рабочей директории
```sh
$ mkdir -p workspace/tasks/
$ mkdir -p workspace/projects/
$ mkdir -p workspace/reports/
$ cd workspace
```

Устанавливаем Node.js, распаковываем архив, переносим в удобную папку и удалем архив
```sh
$ wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
$ mv node-v6.11.5-linux-x64 node
```

Изменяем пути для доступности Node.js, так что теперь файлы будут доступны глобально
```sh
$ export PATH=${PATH}:`pwd`/node/bin
```
Созданиём скрипт активации, который активирует путь для Node.js всякий раз, когда он запускается
```sh
$ mkdir scripts
$ cat > scripts/activate<<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF
$ source scripts/activate
```

Скачиваем gist
```sh
$ sudo apt update
$ sudo apt install ruby-full
$ sudo gem install gist
```

Назначаем специальные права доступа и помещаем токен в защищённый файл
```sh
$ (umask 0077 && echo ${GIST_TOKEN} > ~/.gist)
```

Клонируем репозиторий первой лабораторной работы и создаем для него отдельную папку с отчетом
```sh
$ export LAB_NUMBER=01
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
```

# Homework

## Задание 1
*Скачайте библиотеку boost с помощью утилиты wget.* 
Вводим команду 
```
$ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
```

<details>
<summary> Вывод после использования команды wget</summary>
```sh
--2026-03-07 09:13:20--  https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
Resolving sourceforge.net (sourceforge.net)... 104.18.13.149, 104.18.12.149, 2606:4700::6812:d95, ...
Connecting to sourceforge.net (sourceforge.net)|104.18.13.149|:443... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/ [following]
--2026-03-11 09:13:23--  https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/
Reusing existing connection to sourceforge.net:443.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/download [following]
--2026-03-11 09:13:23--  https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/download
Reusing existing connection to sourceforge.net:443.
HTTP request sent, awaiting response... 302 Found
Location: https://downloads.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?ts=gAAAAABpsQgCV-DsDj5MpZldrgMd1b-ktzLANTC8ZwTnXCU-r5cWw62oZiFLWrzbXxUoL_s1lQxiw9PP0_V_PNmVvTC4rhQpEw%3D%3D&use_mirror=deac-riga&r= [following]
--2026-03-11 09:13:23--  https://downloads.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?ts=gAAAAABpsQgCV-DsDj5MpZldrgMd1b-ktzLANTC8ZwTnXCU-r5cWw62oZiFLWrzbXxUoL_s1lQxiw9PP0_V_PNmVvTC4rhQpEw%3D%3D&use_mirror=deac-riga&r=
Resolving downloads.sourceforge.net (downloads.sourceforge.net)... 104.18.13.149, 104.18.12.149, 2606:4700::6812:d95, ...
Connecting to downloads.sourceforge.net (downloads.sourceforge.net)|104.18.13.149|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://deac-riga.dl.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?viasf=1 [following]
--2026-03-11 09:13:24--  https://deac-riga.dl.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?viasf=1
Resolving deac-riga.dl.sourceforge.net (deac-riga.dl.sourceforge.net)... 89.111.52.100
Connecting to deac-riga.dl.sourceforge.net (deac-riga.dl.sourceforge.net)|89.111.52.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 111710205 (107M) [application/x-gzip]
Saving to: ‘boost_1_69_0.tar.gz’

boost_1_69_0.tar.gz           100%[=================================================>] 106.53M  8.28MB/s    in 21s

2026-03-11 09:13:44 (4.98 MB/s) - ‘boost_1_69_0.tar.gz’ saved [111710205/111710205]
```
</details>

## Задание 2
*Разархивируйте скаченный файл в директорию* `~/boost_1_69_0`

```sh
$ tar -xf boost_1_69_0.tar.gz -C ~/
```

## Задание 3
*Подсчитайте количество файлов в директории* `~/boost_1_69_0` ***не включая** вложенные директории*

Введем следующую команду
```sh
$ find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l
```
`-maxdepth` устанавливает глубину рекурсивного поиска в каталогах, значение 1 означает, что подсчет будет происходить только в указанной директории.
Команда выдала **12**

## Задание 4
*Подсчитайте количество файлов в директории* `~/boost_1_69_0` *включая вложенные директории.*
```sh
$ find ~/boost_1_69_0  -type f | wc -l
```
В этом случае мы не устанавливаем ключ `-maxdepth`. 
В моем случае получилось **61191** файлов.

## Задание 5
*Подсчитайте количество заголовочных файлов, файлов с расширением .cpp, сколько остальных файлов (не заголовочных и не .cpp)*

Также воспользуемся командой `find` с ключем `-name` и шаблоном имени `*.cpp`
```sh
$ find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l
```
Консоль выдала **13774**

Теперь найдем заголовочные файлы. В С++ они обычно имеют расширение `.h` или `.hpp`. Чтобы получить их одной командой, свяжем ключи `-name` через ключ `-o` 
```sh
$ find ~/boost_1_69_0 -type f -name "*.h" -o -name "*.hpp" | wc -l
```
Получаем результат **15208**

И наконец найдем оставшиеся файлы. 
```sh
$ find ~/boost_1_69_0  -type f ! \( -name "*.h" -o -name "*.hpp" -o -name "*.cpp" \) | wc -l
```
Их **32209**
13774+15208+32209 = 61191

## Задание 6
*Найдите полный пусть до файла* `any.hpp` *внутри библиотеки boost.*
Воспользуемся все той же командой `find`
```sh
$ find ~/boost_1_69_0  -type f -name "any.hpp"
```
Терминал выдал 10 файлов с таким именем
```
/home/killer/boost_1_69_0/boost/any.hpp
/home/killer/boost_1_69_0/boost/fusion/algorithm/query/any.hpp
/home/killer/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
/home/killer/boost_1_69_0/boost/fusion/include/any.hpp
/home/killer/boost_1_69_0/boost/proto/detail/any.hpp
/home/killer/boost_1_69_0/boost/type_erasure/any.hpp
/home/killer/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
/home/killer/boost_1_69_0/boost/xpressive/detail/utility/any.hpp
/home/killer/boost_1_69_0/boost/hana/any.hpp
/home/killer/boost_1_69_0/boost/hana/fwd/any.hpp
```

## Задание 7
*Выведите в консоль все файлы, где упоминается последовательность* `boost::asio`
Воспользуемся командой `grep`, которая может читать содержимое текстовых файлов. Ключи у нее будут `-r`, что значит рекурсивный проход всех каталогов, и `-l`, что означает вывод только имен файлов.
```sh
$ grep -rl "boost::asio" ~/boost_1_69_0
```
<details>
<summary> Список файлов </summary>
```
/home/killer/boost_1_69_0/libs/beast/CHANGELOG.md
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/coro-ssl/websocket_server_coro_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/sync/websocket_server_sync.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/coro/websocket_server_coro.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/async/websocket_server_async.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/stackless/websocket_server_stackless.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/sync-ssl/websocket_server_sync_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/fast/websocket_server_fast.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/stackless-ssl/websocket_server_stackless_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/server/async-ssl/websocket_server_async_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/client/coro-ssl/websocket_client_coro_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/client/sync/websocket_client_sync.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/client/coro/websocket_client_coro.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/client/async/websocket_client_async.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/client/sync-ssl/websocket_client_sync_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/websocket/client/async-ssl/websocket_client_async_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/echo-op/echo_op.cpp
/home/killer/boost_1_69_0/libs/beast/example/advanced/server/advanced_server.cpp
/home/killer/boost_1_69_0/libs/beast/example/advanced/server-flex/advanced_server_flex.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/coro-ssl/http_server_coro_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/sync/http_server_sync.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/small/http_server_small.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/flex/http_server_flex.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/coro/http_server_coro.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/async/http_server_async.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/stackless/http_server_stackless.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/sync-ssl/http_server_sync_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/fast/http_server_fast.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/stackless-ssl/http_server_stackless_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/server/async-ssl/http_server_async_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/client/coro-ssl/http_client_coro_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/client/sync/http_client_sync.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/client/coro/http_client_coro.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/client/async/http_client_async.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/client/sync-ssl/http_client_sync_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/client/crawl/http_crawl.cpp
/home/killer/boost_1_69_0/libs/beast/example/http/client/async-ssl/http_client_async_ssl.cpp
/home/killer/boost_1_69_0/libs/beast/example/doc/http_examples.hpp
/home/killer/boost_1_69_0/libs/beast/example/cppcon2018/net.hpp
/home/killer/boost_1_69_0/libs/beast/example/common/detect_ssl.hpp
/home/killer/boost_1_69_0/libs/beast/example/common/root_certificates.hpp
/home/killer/boost_1_69_0/libs/beast/example/common/session_alloc.hpp
/home/killer/boost_1_69_0/libs/beast/example/common/server_certificate.hpp
/home/killer/boost_1_69_0/libs/beast/doc/docca/include/docca/doxygen.xsl
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/more_examples/expect_100_continue_server.html
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/using_io/writing_composed_operations.html
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/using_io/example_detect_ssl.html
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__http__error.html
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__basic_timeout_socket/async_read_some.html
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__basic_timeout_socket/async_write_some.html
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__websocket__async_teardown/overload2.html
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__websocket__async_teardown/overload1.html
/home/killer/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__websocket__async_teardown/overload3.html
/home/killer/boost_1_69_0/libs/beast/doc/qbk/07_concepts/DynamicBuffer.qbk
/home/killer/boost_1_69_0/libs/beast/doc/qbk/07_concepts/Streams.qbk
/home/killer/boost_1_69_0/libs/beast/doc/qbk/reference.qbk
/home/killer/boost_1_69_0/libs/beast/doc/qbk/00_main.qbk
/home/killer/boost_1_69_0/libs/beast/doc/qbk/08_design/4_faq.qbk
/home/killer/boost_1_69_0/libs/beast/doc/qbk/08_design/3_websocket_zaphoyd.qbk
/home/killer/boost_1_69_0/libs/beast/doc/qbk/03_core/1_asio.qbk
/home/killer/boost_1_69_0/libs/beast/test/bench/parser/nodejs_parser.hpp
/home/killer/boost_1_69_0/libs/beast/test/bench/parser/bench_parser.cpp
/home/killer/boost_1_69_0/libs/beast/test/bench/buffers/bench_buffers.cpp
/home/killer/boost_1_69_0/libs/beast/test/bench/wsload/wsload.cpp
/home/killer/boost_1_69_0/libs/beast/test/extras/include/boost/beast/test/yield_to.hpp
/home/killer/boost_1_69_0/libs/beast/test/extras/include/boost/beast/test/websocket.hpp
/home/killer/boost_1_69_0/libs/beast/test/extras/include/boost/beast/test/sig_wait.hpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/bind_handler.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/buffers_prefix.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/read_size.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/buffers_adapter.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/buffer_test.hpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/type_traits.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/static_buffer.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/flat_buffer.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/buffers_suffix.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/buffer.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/multi_buffer.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/buffered_read_stream.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/flat_static_buffer.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/core/buffers_cat.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/handshake.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/test.hpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/read1.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/doc_snippets.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/accept.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/ping.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/write.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/read2.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/utf8_checker.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/stream.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/websocket/close.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/experimental/timeout_service.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/experimental/timeout_socket.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/experimental/flat_stream.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/experimental/icy_stream.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/file_body.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/basic_parser.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/chunk_encode.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/dynamic_body.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/message_fuzz.hpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/serializer.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/span_body.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/test_parser.hpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/read.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/write.cpp
/home/killer/boost_1_69_0/libs/beast/test/beast/http/parser.cpp
/home/killer/boost_1_69_0/libs/beast/test/doc/core_examples.cpp
/home/killer/boost_1_69_0/libs/beast/test/doc/exemplars.cpp
/home/killer/boost_1_69_0/libs/beast/test/doc/core_snippets.cpp
/home/killer/boost_1_69_0/libs/beast/test/doc/http_examples.cpp
/home/killer/boost_1_69_0/libs/beast/test/doc/websocket_snippets.cpp
/home/killer/boost_1_69_0/libs/beast/test/doc/http_snippets.cpp
/home/killer/boost_1_69_0/libs/thread/test/test_9303.cpp
/home/killer/boost_1_69_0/libs/process/example/async_io.cpp
/home/killer/boost_1_69_0/libs/process/example/io.cpp
/home/killer/boost_1_69_0/libs/process/example/wait.cpp
/home/killer/boost_1_69_0/libs/process/doc/extend.qbk
/home/killer/boost_1_69_0/libs/process/doc/tutorial.qbk
/home/killer/boost_1_69_0/libs/process/doc/autodoc.xml
/home/killer/boost_1_69_0/libs/process/test/bind_stderr.cpp
/home/killer/boost_1_69_0/libs/process/test/on_exit3.cpp
/home/killer/boost_1_69_0/libs/process/test/async_system_future.cpp
/home/killer/boost_1_69_0/libs/process/test/bind_stdout.cpp
/home/killer/boost_1_69_0/libs/process/test/exit_code.cpp
/home/killer/boost_1_69_0/libs/process/test/async_system_stackful.cpp
/home/killer/boost_1_69_0/libs/process/test/on_exit.cpp
/home/killer/boost_1_69_0/libs/process/test/async.cpp
/home/killer/boost_1_69_0/libs/process/test/async_system_stackful_error.cpp
/home/killer/boost_1_69_0/libs/process/test/async_pipe.cpp
/home/killer/boost_1_69_0/libs/process/test/async_system_stackless.cpp
/home/killer/boost_1_69_0/libs/process/test/on_exit2.cpp
/home/killer/boost_1_69_0/libs/process/test/spawn_fail.cpp
/home/killer/boost_1_69_0/libs/process/test/wait.cpp
/home/killer/boost_1_69_0/libs/process/test/async_system_stackful_except.cpp
/home/killer/boost_1_69_0/libs/process/test/system_test2.cpp
/home/killer/boost_1_69_0/libs/process/test/async_system_fail.cpp
/home/killer/boost_1_69_0/libs/process/test/spawn.cpp
/home/killer/boost_1_69_0/libs/process/test/bind_stdin.cpp
/home/killer/boost_1_69_0/libs/process/test/system_test1.cpp
/home/killer/boost_1_69_0/libs/process/test/bind_stdout_stderr.cpp
/home/killer/boost_1_69_0/libs/process/test/async_fut.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/iostreams/http_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/local/connect_pair.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/local/stream_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/local/iostream_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/local/stream_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/multicast/receiver.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/multicast/sender.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/executors/bank_account_2.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/executors/pipeline.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/executors/fork_join.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/executors/actor.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/executors/bank_account_1.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/executors/priority_scheduler.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/nonblocking/third_party_lib.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/handler_tracking/async_tcp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/handler_tracking/custom_tracking.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/fork/process_per_connection.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/fork/daemon.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/invocation/prioritised_handlers.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/buffers/reference_counted.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/futures/daytime_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/ssl/client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/ssl/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/chat/chat_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/chat/chat_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/http/server/server.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/http/server/connection.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/http/server/reply.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/http/server/reply.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/http/server/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/http/server/connection.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/timeouts/blocking_token_tcp_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/timeouts/async_tcp_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/timeouts/blocking_udp_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/timeouts/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/timeouts/blocking_tcp_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/allocation/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/echo/blocking_tcp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/echo/blocking_udp_echo_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/echo/async_udp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/echo/blocking_udp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/echo/async_tcp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/echo/blocking_tcp_echo_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/timers/time_t_timer.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/spawn/parallel_grep.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/spawn/echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/operations/composed_2.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/operations/composed_3.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/operations/composed_1.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/operations/composed_4.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/operations/composed_5.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/socks4/socks4.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp11/socks4/sync_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/iostreams/daytime_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/iostreams/daytime_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/iostreams/http_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/windows/transmit_file.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/local/connect_pair.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/local/stream_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/local/iostream_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/local/stream_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/multicast/receiver.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/multicast/sender.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/serialization/client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/serialization/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/serialization/connection.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/nonblocking/third_party_lib.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/fork/process_per_connection.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/fork/daemon.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/invocation/prioritised_handlers.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/buffers/reference_counted.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/services/logger_service.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/services/logger_service.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/services/basic_logger.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/services/daytime_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/porthopper/protocol.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/porthopper/client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/porthopper/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/ssl/client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/ssl/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/chat/chat_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/chat/posix_chat_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/chat/chat_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server/server.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server/connection.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server/reply.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server/reply.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server/connection.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server2/server.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server2/connection.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server2/reply.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server2/reply.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server2/io_context_pool.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server2/io_context_pool.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server2/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server2/connection.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server4/server.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server4/reply.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server4/reply.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server4/request_parser.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server4/main.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server4/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/client/sync_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/client/async_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server3/server.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server3/connection.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server3/reply.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server3/reply.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server3/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/http/server3/connection.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/timeouts/blocking_token_tcp_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/timeouts/async_tcp_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/timeouts/blocking_udp_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/timeouts/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/timeouts/blocking_tcp_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime7/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer1/timer.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime_dox.txt
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime1/client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime3/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime5/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer2/timer.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer3/timer.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime6/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime2/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer5/timer.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer4/timer.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer_dox.txt
/home/killer/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime4/client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/allocation/server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/echo/blocking_tcp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/echo/blocking_udp_echo_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/echo/async_udp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/echo/blocking_udp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/echo/async_tcp_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/echo/blocking_tcp_echo_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/timers/time_t_timer.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/spawn/parallel_grep.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/spawn/echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/icmp/ipv4_header.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/icmp/ping.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/socks4/socks4.hpp
/home/killer/boost_1_69_0/libs/asio/example/cpp03/socks4/sync_client.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/double_buffered_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/chat_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/range_based_for.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/refactored_echo_server.cpp
/home/killer/boost_1_69_0/libs/asio/doc/reference.qbk
/home/killer/boost_1_69_0/libs/asio/doc/examples.qbk
/home/killer/boost_1_69_0/libs/asio/doc/using.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/ConstBufferSequence.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/ConnectHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/HandshakeHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/Handler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/ResolveHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/ReadHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/IteratorConnectHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/WaitHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/MoveAcceptHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/MutableBufferSequence.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/WriteHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/RangeConnectHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/SignalHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/AcceptHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/ShutdownHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/requirements/BufferedHandshakeHandler.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/spawn.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/coroutine.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/cpp2011.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/ssl.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/signals.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/line_based.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/strands.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/posix.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/other_protocols.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/basics.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/allocation.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/coroutines_ts.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/protocols.qbk
/home/killer/boost_1_69_0/libs/asio/doc/overview/buffers.qbk
/home/killer/boost_1_69_0/libs/asio/doc/tutorial.qbk
/home/killer/boost_1_69_0/libs/asio/doc/reference.xsl
/home/killer/boost_1_69_0/libs/asio/test/windows/object_handle.cpp
/home/killer/boost_1_69_0/libs/asio/test/windows/random_access_handle.cpp
/home/killer/boost_1_69_0/libs/asio/test/windows/overlapped_ptr.cpp
/home/killer/boost_1_69_0/libs/asio/test/windows/stream_handle.cpp
/home/killer/boost_1_69_0/libs/asio/test/unit_test.hpp
/home/killer/boost_1_69_0/libs/asio/test/io_context.cpp
/home/killer/boost_1_69_0/libs/asio/test/latency/udp_client.cpp
/home/killer/boost_1_69_0/libs/asio/test/latency/tcp_server.cpp
/home/killer/boost_1_69_0/libs/asio/test/latency/tcp_client.cpp
/home/killer/boost_1_69_0/libs/asio/test/latency/udp_server.cpp
/home/killer/boost_1_69_0/libs/asio/test/local/stream_protocol.cpp
/home/killer/boost_1_69_0/libs/asio/test/local/connect_pair.cpp
/home/killer/boost_1_69_0/libs/asio/test/local/datagram_protocol.cpp
/home/killer/boost_1_69_0/libs/asio/test/is_write_buffered.cpp
/home/killer/boost_1_69_0/libs/asio/test/coroutine.cpp
/home/killer/boost_1_69_0/libs/asio/test/socket_base.cpp
/home/killer/boost_1_69_0/libs/asio/test/serial_port_base.cpp
/home/killer/boost_1_69_0/libs/asio/test/system_timer.cpp
/home/killer/boost_1_69_0/libs/asio/test/streambuf.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/address.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/network_v4.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/address_v4.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/multicast.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/tcp.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/icmp.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/v6_only.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/address_v6.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/network_v6.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/unicast.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/udp.cpp
/home/killer/boost_1_69_0/libs/asio/test/ip/host_name.cpp
/home/killer/boost_1_69_0/libs/asio/test/connect.cpp
/home/killer/boost_1_69_0/libs/asio/test/buffers_iterator.cpp
/home/killer/boost_1_69_0/libs/asio/test/error.cpp
/home/killer/boost_1_69_0/libs/asio/test/read_until.cpp
/home/killer/boost_1_69_0/libs/asio/test/buffered_write_stream.cpp
/home/killer/boost_1_69_0/libs/asio/test/archetypes/async_ops.hpp
/home/killer/boost_1_69_0/libs/asio/test/archetypes/deprecated_async_ops.hpp
/home/killer/boost_1_69_0/libs/asio/test/ssl/stream.cpp
/home/killer/boost_1_69_0/libs/asio/test/serial_port.cpp
/home/killer/boost_1_69_0/libs/asio/test/read_at.cpp
/home/killer/boost_1_69_0/libs/asio/test/write_at.cpp
/home/killer/boost_1_69_0/libs/asio/test/generic/stream_protocol.cpp
/home/killer/boost_1_69_0/libs/asio/test/generic/raw_protocol.cpp
/home/killer/boost_1_69_0/libs/asio/test/generic/datagram_protocol.cpp
/home/killer/boost_1_69_0/libs/asio/test/generic/seq_packet_protocol.cpp
/home/killer/boost_1_69_0/libs/asio/test/signal_set.cpp
/home/killer/boost_1_69_0/libs/asio/test/posix/stream_descriptor.cpp
/home/killer/boost_1_69_0/libs/asio/test/read.cpp
/home/killer/boost_1_69_0/libs/asio/test/buffer.cpp
/home/killer/boost_1_69_0/libs/asio/test/buffered_stream.cpp
/home/killer/boost_1_69_0/libs/asio/test/use_future.cpp
/home/killer/boost_1_69_0/libs/asio/test/write.cpp
/home/killer/boost_1_69_0/libs/asio/test/strand.cpp
/home/killer/boost_1_69_0/libs/asio/test/buffered_read_stream.cpp
/home/killer/boost_1_69_0/libs/asio/test/is_read_buffered.cpp
/home/killer/boost_1_69_0/libs/asio/test/deadline_timer.cpp
/home/killer/boost_1_69_0/libs/coroutine/doc/coro.qbk
/home/killer/boost_1_69_0/libs/coroutine/doc/html/coroutine/motivation.html
/home/killer/boost_1_69_0/libs/coroutine/doc/motivation.qbk
/home/killer/boost_1_69_0/libs/log/src/syslog_backend.cpp
/home/killer/boost_1_69_0/libs/log/doc/tmp/sinks_reference.xml
/home/killer/boost_1_69_0/libs/fiber/examples/asio/round_robin.hpp
/home/killer/boost_1_69_0/libs/fiber/examples/asio/autoecho.cpp
/home/killer/boost_1_69_0/libs/fiber/examples/asio/ps/subscriber.cpp
/home/killer/boost_1_69_0/libs/fiber/examples/asio/ps/publisher.cpp
/home/killer/boost_1_69_0/libs/fiber/examples/asio/ps/server.cpp
/home/killer/boost_1_69_0/libs/fiber/examples/asio/exchange.cpp
/home/killer/boost_1_69_0/libs/fiber/doc/integration.qbk
/home/killer/boost_1_69_0/libs/fiber/doc/fibers.qbk
/home/killer/boost_1_69_0/libs/fiber/doc/callbacks.qbk
/home/killer/boost_1_69_0/libs/fiber/doc/asio.qbk
/home/killer/boost_1_69_0/libs/coroutine2/doc/coro.qbk
/home/killer/boost_1_69_0/libs/coroutine2/doc/motivation.qbk
/home/killer/boost_1_69_0/libs/phoenix/example/adapted_echo_server.cpp
/home/killer/boost_1_69_0/boost/beast/core/ostream.hpp
/home/killer/boost_1_69_0/boost/beast/core/type_traits.hpp
/home/killer/boost_1_69_0/boost/beast/core/bind_handler.hpp
/home/killer/boost_1_69_0/boost/beast/core/buffered_read_stream.hpp
/home/killer/boost_1_69_0/boost/beast/core/flat_static_buffer.hpp
/home/killer/boost_1_69_0/boost/beast/core/multi_buffer.hpp
/home/killer/boost_1_69_0/boost/beast/core/detail/type_traits.hpp
/home/killer/boost_1_69_0/boost/beast/core/detail/bind_handler.hpp
/home/killer/boost_1_69_0/boost/beast/core/detail/buffers_ref.hpp
/home/killer/boost_1_69_0/boost/beast/core/static_buffer.hpp
/home/killer/boost_1_69_0/boost/beast/core/buffers_prefix.hpp
/home/killer/boost_1_69_0/boost/beast/core/buffers_adapter.hpp
/home/killer/boost_1_69_0/boost/beast/core/flat_buffer.hpp
/home/killer/boost_1_69_0/boost/beast/core/buffers_to_string.hpp
/home/killer/boost_1_69_0/boost/beast/core/buffers_suffix.hpp
/home/killer/boost_1_69_0/boost/beast/core/impl/buffers_adapter.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/buffers_prefix.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/read_size.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/buffers_suffix.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/buffered_read_stream.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/flat_buffer.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/buffers_cat.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/multi_buffer.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/handler_ptr.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/static_buffer.ipp
/home/killer/boost_1_69_0/boost/beast/core/impl/flat_static_buffer.ipp
/home/killer/boost_1_69_0/boost/beast/core/buffers_cat.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/rfc6455.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/role.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/teardown.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/detail/pausation.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/detail/utf8_checker.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/detail/stream_base.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/detail/mask.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/detail/frame.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/stream.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/ssl.hpp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/ping.ipp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/accept.ipp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/write.ipp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/close.ipp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/handshake.ipp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/ssl.ipp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/teardown.ipp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/stream.ipp
/home/killer/boost_1_69_0/boost/beast/websocket/impl/read.ipp
/home/killer/boost_1_69_0/boost/beast/experimental/core/ssl_stream.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/core/timeout_service.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/core/detail/timeout_service.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/core/detail/service_base.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/core/detail/flat_stream.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/core/detail/impl/timeout_service.ipp
/home/killer/boost_1_69_0/boost/beast/experimental/core/timeout_socket.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/core/flat_stream.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/core/impl/flat_stream.ipp
/home/killer/boost_1_69_0/boost/beast/experimental/core/impl/timeout_service.ipp
/home/killer/boost_1_69_0/boost/beast/experimental/core/impl/timeout_socket.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/http/icy_stream.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/http/impl/icy_stream.ipp
/home/killer/boost_1_69_0/boost/beast/experimental/test/stream.hpp
/home/killer/boost_1_69_0/boost/beast/experimental/test/impl/stream.ipp
/home/killer/boost_1_69_0/boost/beast/http/string_body.hpp
/home/killer/boost_1_69_0/boost/beast/http/type_traits.hpp
/home/killer/boost_1_69_0/boost/beast/http/error.hpp
/home/killer/boost_1_69_0/boost/beast/http/parser.hpp
/home/killer/boost_1_69_0/boost/beast/http/fields.hpp
/home/killer/boost_1_69_0/boost/beast/http/basic_parser.hpp
/home/killer/boost_1_69_0/boost/beast/http/chunk_encode.hpp
/home/killer/boost_1_69_0/boost/beast/http/detail/chunk_encode.hpp
/home/killer/boost_1_69_0/boost/beast/http/buffer_body.hpp
/home/killer/boost_1_69_0/boost/beast/http/write.hpp
/home/killer/boost_1_69_0/boost/beast/http/vector_body.hpp
/home/killer/boost_1_69_0/boost/beast/http/empty_body.hpp
/home/killer/boost_1_69_0/boost/beast/http/serializer.hpp
/home/killer/boost_1_69_0/boost/beast/http/basic_file_body.hpp
/home/killer/boost_1_69_0/boost/beast/http/read.hpp
/home/killer/boost_1_69_0/boost/beast/http/impl/write.ipp
/home/killer/boost_1_69_0/boost/beast/http/impl/chunk_encode.ipp
/home/killer/boost_1_69_0/boost/beast/http/impl/serializer.ipp
/home/killer/boost_1_69_0/boost/beast/http/impl/fields.ipp
/home/killer/boost_1_69_0/boost/beast/http/impl/read.ipp
/home/killer/boost_1_69_0/boost/beast/http/impl/file_body_win32.ipp
/home/killer/boost_1_69_0/boost/beast/http/impl/basic_parser.ipp
/home/killer/boost_1_69_0/boost/beast/http/basic_dynamic_body.hpp
/home/killer/boost_1_69_0/boost/beast/http/span_body.hpp
/home/killer/boost_1_69_0/boost/process/async_pipe.hpp
/home/killer/boost_1_69_0/boost/process/io.hpp
/home/killer/boost_1_69_0/boost/process/detail/windows/async_in.hpp
/home/killer/boost_1_69_0/boost/process/detail/windows/async_pipe.hpp
/home/killer/boost_1_69_0/boost/process/detail/windows/async_out.hpp
/home/killer/boost_1_69_0/boost/process/detail/windows/io_context_ref.hpp
/home/killer/boost_1_69_0/boost/process/detail/async_handler.hpp
/home/killer/boost_1_69_0/boost/process/detail/posix/async_in.hpp
/home/killer/boost_1_69_0/boost/process/detail/posix/sigchld_service.hpp
/home/killer/boost_1_69_0/boost/process/detail/posix/async_pipe.hpp
/home/killer/boost_1_69_0/boost/process/detail/posix/async_out.hpp
/home/killer/boost_1_69_0/boost/process/detail/posix/io_context_ref.hpp
/home/killer/boost_1_69_0/boost/process/detail/traits/async.hpp
/home/killer/boost_1_69_0/boost/process/async.hpp
/home/killer/boost_1_69_0/boost/process/async_system.hpp
/home/killer/boost_1_69_0/boost/process/spawn.hpp
/home/killer/boost_1_69_0/boost/process/system.hpp
/home/killer/boost_1_69_0/boost/asio/basic_serial_port.hpp
/home/killer/boost_1_69_0/boost/asio/basic_socket_streambuf.hpp
/home/killer/boost_1_69_0/boost/asio/basic_signal_set.hpp
/home/killer/boost_1_69_0/boost/asio/basic_socket.hpp
/home/killer/boost_1_69_0/boost/asio/windows/overlapped_handle.hpp
/home/killer/boost_1_69_0/boost/asio/windows/random_access_handle_service.hpp
/home/killer/boost_1_69_0/boost/asio/windows/basic_stream_handle.hpp
/home/killer/boost_1_69_0/boost/asio/windows/object_handle.hpp
/home/killer/boost_1_69_0/boost/asio/windows/overlapped_ptr.hpp
/home/killer/boost_1_69_0/boost/asio/windows/basic_random_access_handle.hpp
/home/killer/boost_1_69_0/boost/asio/windows/basic_object_handle.hpp
/home/killer/boost_1_69_0/boost/asio/windows/random_access_handle.hpp
/home/killer/boost_1_69_0/boost/asio/windows/stream_handle.hpp
/home/killer/boost_1_69_0/boost/asio/windows/stream_handle_service.hpp
/home/killer/boost_1_69_0/boost/asio/windows/object_handle_service.hpp
/home/killer/boost_1_69_0/boost/asio/windows/basic_handle.hpp
/home/killer/boost_1_69_0/boost/asio/execution_context.hpp
/home/killer/boost_1_69_0/boost/asio/buffers_iterator.hpp
/home/killer/boost_1_69_0/boost/asio/uses_executor.hpp
/home/killer/boost_1_69_0/boost/asio/basic_stream_socket.hpp
/home/killer/boost_1_69_0/boost/asio/local/connect_pair.hpp
/home/killer/boost_1_69_0/boost/asio/local/detail/endpoint.hpp
/home/killer/boost_1_69_0/boost/asio/local/detail/impl/endpoint.ipp
/home/killer/boost_1_69_0/boost/asio/local/basic_endpoint.hpp
/home/killer/boost_1_69_0/boost/asio/local/stream_protocol.hpp
/home/killer/boost_1_69_0/boost/asio/local/datagram_protocol.hpp
/home/killer/boost_1_69_0/boost/asio/error.hpp
/home/killer/boost_1_69_0/boost/asio/basic_raw_socket.hpp
/home/killer/boost_1_69_0/boost/asio/basic_socket_acceptor.hpp
/home/killer/boost_1_69_0/boost/asio/experimental/detached.hpp
/home/killer/boost_1_69_0/boost/asio/experimental/impl/co_spawn.hpp
/home/killer/boost_1_69_0/boost/asio/experimental/impl/detached.hpp
/home/killer/boost_1_69_0/boost/asio/signal_set.hpp
/home/killer/boost_1_69_0/boost/asio/io_context_strand.hpp
/home/killer/boost_1_69_0/boost/asio/buffered_read_stream.hpp
/home/killer/boost_1_69_0/boost/asio/basic_waitable_timer.hpp
/home/killer/boost_1_69_0/boost/asio/placeholders.hpp
/home/killer/boost_1_69_0/boost/asio/buffered_stream.hpp
/home/killer/boost_1_69_0/boost/asio/handler_invoke_hook.hpp
/home/killer/boost_1_69_0/boost/asio/executor.hpp
/home/killer/boost_1_69_0/boost/asio/io_context.hpp
/home/killer/boost_1_69_0/boost/asio/datagram_socket_service.hpp
/home/killer/boost_1_69_0/boost/asio/async_result.hpp
/home/killer/boost_1_69_0/boost/asio/read_at.hpp
/home/killer/boost_1_69_0/boost/asio/detail/descriptor_ops.hpp
/home/killer/boost_1_69_0/boost/asio/detail/resolve_endpoint_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_socket_connect_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/null_thread.hpp
/home/killer/boost_1_69_0/boost/asio/detail/string_view.hpp
/home/killer/boost_1_69_0/boost/asio/detail/conditionally_enabled_event.hpp
/home/killer/boost_1_69_0/boost/asio/detail/handler_type_requirements.hpp
/home/killer/boost_1_69_0/boost/asio/detail/handler_alloc_helpers.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_socket_service_base.hpp
/home/killer/boost_1_69_0/boost/asio/detail/descriptor_write_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/service_registry.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_resolver_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_static_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_send_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_serial_port_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/posix_static_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_resolve_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_wait_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_socket_recv_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_connect_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/null_static_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/null_socket_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_socket_send_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/wait_handler.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_service_base.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_overlapped_ptr.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_socket_recvmsg_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_handle_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_descriptor_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/posix_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_io_context.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_timer_scheduler.hpp
/home/killer/boost_1_69_0/boost/asio/detail/std_static_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/handler_cont_helpers.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_ssocket_service_base.hpp
/home/killer/boost_1_69_0/boost/asio/detail/scheduler.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_recvfrom_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/noncopyable.hpp
/home/killer/boost_1_69_0/boost/asio/detail/handler_invoke_helpers.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_socket_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_socket_recvfrom_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/epoll_reactor.hpp
/home/killer/boost_1_69_0/boost/asio/detail/is_buffer_sequence.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_handle_write_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_recv_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_socket_connect_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/conditionally_enabled_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_socket_recv_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/select_reactor.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_object_handle_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/null_reactor.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winapp_thread.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_accept_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/resolver_service_base.hpp
/home/killer/boost_1_69_0/boost/asio/detail/null_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_ssocket_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_null_buffers_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/completion_handler.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_utils.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_wait_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/deadline_timer_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/strand_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_async_manager.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactor_op_queue.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_serial_port_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/impl/posix_tss_ptr.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/socket_select_interrupter.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/dev_poll_reactor.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_iocp_io_context.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/signal_set_service.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_mutex.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/resolver_service_base.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_iocp_handle_service.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/throw_error.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/strand_service.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/reactive_serial_port_service.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/service_registry.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_iocp_io_context.hpp
/home/killer/boost_1_69_0/boost/asio/detail/impl/winrt_timer_scheduler.hpp
/home/killer/boost_1_69_0/boost/asio/detail/impl/posix_mutex.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/buffer_sequence_adapter.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_iocp_serial_port_service.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_tss_ptr.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/descriptor_ops.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_thread.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/winrt_timer_scheduler.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/winsock_init.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/posix_event.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/select_reactor.hpp
/home/killer/boost_1_69_0/boost/asio/detail/impl/epoll_reactor.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/reactive_socket_service_base.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_static_mutex.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_event.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/select_reactor.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/strand_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/impl/posix_thread.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/dev_poll_reactor.hpp
/home/killer/boost_1_69_0/boost/asio/detail/impl/reactive_descriptor_service.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/socket_ops.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/handler_tracking.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/strand_executor_service.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/kqueue_reactor.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/eventfd_select_interrupter.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/scheduler.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/winrt_ssocket_service_base.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_object_handle_service.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/pipe_select_interrupter.ipp
/home/killer/boost_1_69_0/boost/asio/detail/impl/win_iocp_socket_service_base.ipp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_null_buffers_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_socket_accept_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/consuming_buffers.hpp
/home/killer/boost_1_69_0/boost/asio/detail/signal_set_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/kqueue_reactor.hpp
/home/killer/boost_1_69_0/boost/asio/detail/thread_group.hpp
/home/killer/boost_1_69_0/boost/asio/detail/signal_handler.hpp
/home/killer/boost_1_69_0/boost/asio/detail/dev_poll_reactor.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_sendto_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winsock_init.hpp
/home/killer/boost_1_69_0/boost/asio/detail/winrt_socket_send_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_handle_read_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/reactive_socket_recvmsg_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/timer_queue.hpp
/home/killer/boost_1_69_0/boost/asio/detail/win_iocp_overlapped_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/buffered_stream_storage.hpp
/home/killer/boost_1_69_0/boost/asio/detail/wince_thread.hpp
/home/killer/boost_1_69_0/boost/asio/detail/std_mutex.hpp
/home/killer/boost_1_69_0/boost/asio/detail/handler_tracking.hpp
/home/killer/boost_1_69_0/boost/asio/detail/resolver_service.hpp
/home/killer/boost_1_69_0/boost/asio/detail/resolve_query_op.hpp
/home/killer/boost_1_69_0/boost/asio/detail/socket_option.hpp
/home/killer/boost_1_69_0/boost/asio/detail/buffer_sequence_adapter.hpp
/home/killer/boost_1_69_0/boost/asio/detail/descriptor_read_op.hpp
/home/killer/boost_1_69_0/boost/asio/ip/v6_only.hpp
/home/killer/boost_1_69_0/boost/asio/ip/basic_resolver_query.hpp
/home/killer/boost_1_69_0/boost/asio/ip/basic_resolver_iterator.hpp
/home/killer/boost_1_69_0/boost/asio/ip/udp.hpp
/home/killer/boost_1_69_0/boost/asio/ip/tcp.hpp
/home/killer/boost_1_69_0/boost/asio/ip/icmp.hpp
/home/killer/boost_1_69_0/boost/asio/ip/basic_resolver_entry.hpp
/home/killer/boost_1_69_0/boost/asio/ip/address_v4.hpp
/home/killer/boost_1_69_0/boost/asio/ip/detail/endpoint.hpp
/home/killer/boost_1_69_0/boost/asio/ip/detail/impl/endpoint.ipp
/home/killer/boost_1_69_0/boost/asio/ip/detail/socket_option.hpp
/home/killer/boost_1_69_0/boost/asio/ip/multicast.hpp
/home/killer/boost_1_69_0/boost/asio/ip/basic_resolver.hpp
/home/killer/boost_1_69_0/boost/asio/ip/basic_endpoint.hpp
/home/killer/boost_1_69_0/boost/asio/ip/basic_resolver_results.hpp
/home/killer/boost_1_69_0/boost/asio/ip/unicast.hpp
/home/killer/boost_1_69_0/boost/asio/ip/network_v4.hpp
/home/killer/boost_1_69_0/boost/asio/ip/impl/network_v4.ipp
/home/killer/boost_1_69_0/boost/asio/ip/impl/address_v4.ipp
/home/killer/boost_1_69_0/boost/asio/ip/impl/host_name.ipp
/home/killer/boost_1_69_0/boost/asio/ip/impl/address.ipp
/home/killer/boost_1_69_0/boost/asio/ip/impl/address_v6.ipp
/home/killer/boost_1_69_0/boost/asio/ip/impl/address_v4.hpp
/home/killer/boost_1_69_0/boost/asio/ip/impl/basic_endpoint.hpp
/home/killer/boost_1_69_0/boost/asio/ip/impl/network_v6.ipp
/home/killer/boost_1_69_0/boost/asio/ip/impl/network_v4.hpp
/home/killer/boost_1_69_0/boost/asio/ip/impl/network_v6.hpp
/home/killer/boost_1_69_0/boost/asio/ip/impl/address.hpp
/home/killer/boost_1_69_0/boost/asio/ip/impl/address_v6.hpp
/home/killer/boost_1_69_0/boost/asio/ip/network_v6.hpp
/home/killer/boost_1_69_0/boost/asio/ip/address.hpp
/home/killer/boost_1_69_0/boost/asio/ip/address_v6.hpp
/home/killer/boost_1_69_0/boost/asio/ip/resolver_service.hpp
/home/killer/boost_1_69_0/boost/asio/ts/netfwd.hpp
/home/killer/boost_1_69_0/boost/asio/write.hpp
/home/killer/boost_1_69_0/boost/asio/basic_datagram_socket.hpp
/home/killer/boost_1_69_0/boost/asio/is_executor.hpp
/home/killer/boost_1_69_0/boost/asio/buffered_write_stream.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/rfc2818_verification.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/error.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/io.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/write_op.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/engine.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/buffered_handshake_op.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/read_op.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/impl/openssl_init.ipp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/impl/engine.ipp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/stream_core.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/detail/openssl_init.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/stream.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/impl/error.ipp
/home/killer/boost_1_69_0/boost/asio/ssl/impl/context.ipp
/home/killer/boost_1_69_0/boost/asio/ssl/impl/context.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/stream_base.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/context_base.hpp
/home/killer/boost_1_69_0/boost/asio/ssl/context.hpp
/home/killer/boost_1_69_0/boost/asio/serial_port.hpp
/home/killer/boost_1_69_0/boost/asio/read_until.hpp
/home/killer/boost_1_69_0/boost/asio/serial_port_service.hpp
/home/killer/boost_1_69_0/boost/asio/seq_packet_socket_service.hpp
/home/killer/boost_1_69_0/boost/asio/socket_base.hpp
/home/killer/boost_1_69_0/boost/asio/basic_io_object.hpp
/home/killer/boost_1_69_0/boost/asio/generic/seq_packet_protocol.hpp
/home/killer/boost_1_69_0/boost/asio/generic/detail/endpoint.hpp
/home/killer/boost_1_69_0/boost/asio/generic/detail/impl/endpoint.ipp
/home/killer/boost_1_69_0/boost/asio/generic/basic_endpoint.hpp
/home/killer/boost_1_69_0/boost/asio/generic/stream_protocol.hpp
/home/killer/boost_1_69_0/boost/asio/generic/datagram_protocol.hpp
/home/killer/boost_1_69_0/boost/asio/generic/raw_protocol.hpp
/home/killer/boost_1_69_0/boost/asio/posix/basic_descriptor.hpp
/home/killer/boost_1_69_0/boost/asio/posix/descriptor_base.hpp
/home/killer/boost_1_69_0/boost/asio/posix/basic_stream_descriptor.hpp
/home/killer/boost_1_69_0/boost/asio/posix/descriptor.hpp
/home/killer/boost_1_69_0/boost/asio/posix/stream_descriptor_service.hpp
/home/killer/boost_1_69_0/boost/asio/posix/stream_descriptor.hpp
/home/killer/boost_1_69_0/boost/asio/socket_acceptor_service.hpp
/home/killer/boost_1_69_0/boost/asio/coroutine.hpp
/home/killer/boost_1_69_0/boost/asio/read.hpp
/home/killer/boost_1_69_0/boost/asio/deadline_timer_service.hpp
/home/killer/boost_1_69_0/boost/asio/waitable_timer_service.hpp
/home/killer/boost_1_69_0/boost/asio/use_future.hpp
/home/killer/boost_1_69_0/boost/asio/spawn.hpp
/home/killer/boost_1_69_0/boost/asio/basic_seq_packet_socket.hpp
/home/killer/boost_1_69_0/boost/asio/impl/serial_port_base.ipp
/home/killer/boost_1_69_0/boost/asio/impl/buffered_read_stream.hpp
/home/killer/boost_1_69_0/boost/asio/impl/io_context.hpp
/home/killer/boost_1_69_0/boost/asio/impl/read_at.hpp
/home/killer/boost_1_69_0/boost/asio/impl/io_context.ipp
/home/killer/boost_1_69_0/boost/asio/impl/write.hpp
/home/killer/boost_1_69_0/boost/asio/impl/buffered_write_stream.hpp
/home/killer/boost_1_69_0/boost/asio/impl/read_until.hpp
/home/killer/boost_1_69_0/boost/asio/impl/execution_context.ipp
/home/killer/boost_1_69_0/boost/asio/impl/read.hpp
/home/killer/boost_1_69_0/boost/asio/impl/spawn.hpp
/home/killer/boost_1_69_0/boost/asio/impl/connect.hpp
/home/killer/boost_1_69_0/boost/asio/impl/write_at.hpp
/home/killer/boost_1_69_0/boost/asio/signal_set_service.hpp
/home/killer/boost_1_69_0/boost/asio/basic_streambuf.hpp
/home/killer/boost_1_69_0/boost/asio/completion_condition.hpp
/home/killer/boost_1_69_0/boost/asio/buffer.hpp
/home/killer/boost_1_69_0/boost/asio/stream_socket_service.hpp
/home/killer/boost_1_69_0/boost/asio/raw_socket_service.hpp
/home/killer/boost_1_69_0/boost/asio/basic_deadline_timer.hpp
/home/killer/boost_1_69_0/boost/asio/thread_pool.hpp
/home/killer/boost_1_69_0/boost/asio/connect.hpp
/home/killer/boost_1_69_0/boost/asio/basic_socket_iostream.hpp
/home/killer/boost_1_69_0/boost/asio/write_at.hpp
/home/killer/boost_1_69_0/boost/log/sinks/syslog_backend.hpp
/home/killer/boost_1_69_0/doc/html/boost/process/on_exit.html
/home/killer/boost_1_69_0/doc/html/boost/process/async_pipe.html
/home/killer/boost_1_69_0/doc/html/boost/process/std_in.html
/home/killer/boost_1_69_0/doc/html/boost/process/std_out.html
/home/killer/boost_1_69_0/doc/html/boost/process/spawn.html
/home/killer/boost_1_69_0/doc/html/process/reference.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/use_future_t.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ConstBufferSequence.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__boost__asio__ssl__error__stream_errors__gt_.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/placeholders__endpoint.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffer_sequence_begin.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__leave_group.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/local__stream_protocol/acceptor.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/async_read_some.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/stream_handle.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/write_some/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/read_some/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/stream_handle/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/stream_handle/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/async_write_some.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__address/operator_eq_.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__address/to_v4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__address/to_v6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__address/address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__address/operator_eq_/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__address/operator_eq_/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__address/address/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__address/address/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/mutable_buffer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/placeholders__iterator.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload7.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload12.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload9.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload10.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload8.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload11.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/connect/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/dynamic_buffer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffered_stream/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffered_stream/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/placeholders__bytes_transferred.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/execution_context/add_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/execution_context/make_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffered_write_stream/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffered_write_stream/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__tcp/acceptor.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__tcp/no_delay.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/transfer_at_least.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/steady_timer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/placeholders__signal_number.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ResolveHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/receive_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_receive_from/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_receive_from/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/local_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/local_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/connect/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/connect/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/bind/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/bind/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/open/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/open/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/send/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/shutdown/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/shutdown/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/linger.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/receive_from/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_receive/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_receive/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/send_to/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/wait/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/wait/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/remote_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/remote_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/set_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/set_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/send_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/out_of_band_inline.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/send_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/keep_alive.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/receive/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/reuse_address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/io_control/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/io_control/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/do_not_route.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/debug.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/native_non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/native_non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/native_non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/get_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/get_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_send/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_send/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_connect.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/enable_connection_aborted.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/release/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/release/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_send_to/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_send_to/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/receive_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/broadcast.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__ssl_errors__gt_.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_streambuf.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/generic__raw_protocol.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__outbound_interface.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/overlapped_handle.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/overlapped_handle/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/overlapped_handle/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload15.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload7.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload14.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload12.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload9.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload13.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload16.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload10.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload11.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/object_handle/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/object_handle/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/object_handle.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/error__system_category.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/async_read_some.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/write_some/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/read_some/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/async_write_some.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/serial_port/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_completion/completion_handler_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__ssl_errors__gt_/value.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/AcceptHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__misc_errors__gt_/value.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/const_buffer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffered_read_stream/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffered_read_stream/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ReadHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/receive_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/local_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/local_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/connect/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/connect/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/bind/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/bind/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/open/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/open/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/send/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/send/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/shutdown/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/shutdown/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/linger.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_receive/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_receive/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_read_some.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/wait/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/wait/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/remote_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/remote_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/set_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/set_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/send_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/out_of_band_inline.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/send_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/keep_alive.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/receive/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/receive/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/reuse_address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/io_control/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/io_control/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/write_some/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/do_not_route.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/debug.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/read_some/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/native_non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/native_non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/native_non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/get_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/get_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_send/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_send/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_connect.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/enable_connection_aborted.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_write_some.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/release/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/release/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/receive_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/broadcast.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/async_read_some.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/wait/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/wait/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/io_control/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/io_control/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/stream_descriptor.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/write_some/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/read_some/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/native_non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/native_non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/native_non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/async_write_some.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/release.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/stream_descriptor/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/stream_descriptor/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffer_copy.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_streambuf/expires_after.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_streambuf/expires_at/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_streambuf/expires_from_now/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/error__ssl_category.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/generic__datagram_protocol.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/HandshakeHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__v6_only.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_until.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write_at/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write_at/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write_at/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write_at/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/transfer_all.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/Handler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/receive_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/local_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/local_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/bind/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/bind/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/open/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/open/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/linger.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload7.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload12.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload9.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload10.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload8.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload11.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/wait/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/wait/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/set_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/set_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/listen/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/send_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/out_of_band_inline.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/send_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/keep_alive.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/reuse_address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/io_control/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/io_control/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/do_not_route.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/debug.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/native_non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/native_non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/native_non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/get_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/get_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/enable_connection_aborted.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/release/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/release/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/receive_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/broadcast.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ssl__rfc2818_verification.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__netdb_errors__gt_.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/system_context/add_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/system_context/make_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/system_timer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write/overload9.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write/overload10.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/streambuf.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/MoveAcceptHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/error__misc_category.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__enable_loopback.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor_base/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffer_sequence_end.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__service/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__service/service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__service/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/basic_resolver.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/basic_resolver/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/cancel.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__join_group.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__unicast__hops.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__basic_errors__gt_/value.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/experimental__detached_t.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read/overload9.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read/overload10.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/dynamic_string_buffer/const_buffers_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/dynamic_string_buffer/mutable_buffers_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ConnectHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_at/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_at/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_at/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_at/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/thread_pool.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/yield_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_ptr/overlapped_ptr/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_ptr/reset.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_ptr/reset/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_ptr/overlapped_ptr.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver_query/hints.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ShutdownHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/buffer_cast.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/deadline_timer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/transfer_exactly.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/error__addrinfo_category.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ssl__stream/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ssl__stream/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ssl__stream/native_handle.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ssl__error__stream_category.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_streambuf_ref/const_buffers_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_streambuf_ref/mutable_buffers_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/add_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/receive_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/local_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/local_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/connect/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/connect/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/bind/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/bind/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/open/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/open/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/shutdown/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/shutdown/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/linger.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/wait/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/wait/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/remote_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/remote_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/set_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/set_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/send_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/out_of_band_inline.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/send_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/keep_alive.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/reuse_address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/io_control/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/io_control/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/do_not_route.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/debug.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/native_non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/native_non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/native_non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/get_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/get_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/async_connect.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/enable_connection_aborted.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/release/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/release/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/receive_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/broadcast.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/null_buffers/value_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/basic_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/basic_endpoint/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/basic_endpoint.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/address/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/address/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/BufferedHandshakeHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/wait/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/wait/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/descriptor/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/descriptor/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/io_control/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/io_control/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/native_non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/native_non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/native_non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/release.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/descriptor.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ssl__stream.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload7.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload8.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/basic_deadline_timer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/expires_at/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/expires_at/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/cancel_one/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/cancel_one/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/expires_from_now/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/expires_from_now/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/basic_deadline_timer/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/basic_deadline_timer/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/basic_deadline_timer/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/IteratorConnectHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__boost__asio__ssl__error__stream_errors__gt_/value.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/const_buffers_1/value_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/MutableBufferSequence.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__basic_errors__gt_.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/dynamic_vector_buffer/const_buffers_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/dynamic_vector_buffer/mutable_buffers_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/receive_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/linger.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/send_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/out_of_band_inline.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/send_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/keep_alive.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/reuse_address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/do_not_route.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/debug.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/enable_connection_aborted.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/receive_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/socket_base/broadcast.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__netdb_errors__gt_/value.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/spawn/overload6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand/strand.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand/context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_iostream/expires_after.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_iostream/expires_at/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_iostream/expires_from_now/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/RangeConnectHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/SignalHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/error__netdb_category.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/basic_io_object.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/executor_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/basic_io_object/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/mutable_buffers_1/value_type.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/receive_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_receive_from/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_receive_from/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/local_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/local_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/connect/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/connect/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/bind/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/bind/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/open/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/open/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/send/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/shutdown/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/shutdown/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/linger.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/receive_from/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_receive/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_receive/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/send_to/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/wait/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/wait/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/remote_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/remote_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/set_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/set_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/send_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/out_of_band_inline.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/send_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/keep_alive.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/receive/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/reuse_address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/io_control/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/io_control/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/do_not_route.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/debug.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/native_non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/native_non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/native_non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/get_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/get_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_send/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_send/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_connect.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/enable_connection_aborted.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/release/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/release/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_send_to/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_send_to/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/receive_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/broadcast.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/high_resolution_timer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/generic__stream_protocol.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/placeholders__results.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_after.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_at/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_at/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/cancel_one/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/cancel_one/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_from_now/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_from_now/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/basic_waitable_timer/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/basic_waitable_timer/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/basic_waitable_timer/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/basic_waitable_timer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/thread_pool/add_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/thread_pool/make_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__misc_errors__gt_.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__work/work.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__work/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__work/work/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context__work/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/spawn.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__addrinfo_errors__gt_.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__hops.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/WaitHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context/add_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/io_context/make_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/async_read_some_at.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/async_write_some_at.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/write_some_at/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/random_access_handle/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/random_access_handle/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/read_some_at/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/random_access_handle.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/receive_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/local_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/local_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/connect/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/connect/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_send.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/bind/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/bind/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/open/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/open/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/send/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/shutdown/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/shutdown/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/linger.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/get_io_context.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/close/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/close/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_receive/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_receive/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/cancel/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/cancel/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/wait/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/wait/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/remote_endpoint/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/remote_endpoint/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/set_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/set_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_wait.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/send_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/out_of_band_inline.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/send_low_watermark.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/bytes_readable.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/keep_alive.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/receive/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/receive/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/reuse_address.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/io_control/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/io_control/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/do_not_route.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/debug.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/native_non_blocking/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/native_non_blocking/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/native_non_blocking/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/get_option/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/get_option/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_connect.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/enable_connection_aborted.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/get_io_service.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/release/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/release/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket/overload2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket/overload4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket/overload1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket/overload3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/receive_buffer_size.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/broadcast.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/WriteHandler.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__addrinfo_errors__gt_/value.html
/home/killer/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer.html
/home/killer/boost_1_69_0/doc/html/boost_asio/examples/cpp11_examples.html
/home/killer/boost_1_69_0/doc/html/boost_asio/examples/cpp03_examples.html
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/local/connect_pair.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/local/stream_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/local/iostream_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/local/stream_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/multicast/receiver.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/multicast/sender.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/bank_account_2.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/pipeline.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/fork_join.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/actor.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/bank_account_1.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/priority_scheduler.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/handler_tracking/async_tcp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/handler_tracking/custom_tracking.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/fork/process_per_connection.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/fork/daemon.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/invocation/prioritised_handlers.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/buffers/reference_counted.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/futures/daytime_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/ssl/client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/ssl/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/chat/chat_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/chat/chat_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/server.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/connection.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/reply.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/reply.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/connection.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/blocking_token_tcp_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/async_tcp_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/blocking_udp_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/blocking_tcp_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/allocation/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/blocking_tcp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/blocking_udp_echo_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/async_udp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/blocking_udp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/async_tcp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/blocking_tcp_echo_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/timers/time_t_timer.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/spawn/parallel_grep.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/spawn/echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_2.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_3.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_1.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_4.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_5.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/socks4/socks4.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp11/socks4/sync_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/iostreams/daytime_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/iostreams/daytime_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/iostreams/http_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/windows/transmit_file.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/local/connect_pair.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/local/stream_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/local/iostream_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/local/stream_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/multicast/receiver.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/multicast/sender.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/serialization/client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/serialization/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/serialization/connection.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/nonblocking/third_party_lib.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/fork/process_per_connection.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/fork/daemon.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/invocation/prioritised_handlers.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/buffers/reference_counted.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/services/logger_service.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/services/logger_service.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/services/basic_logger.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/services/daytime_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/porthopper/protocol.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/porthopper/client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/porthopper/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/ssl/client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/ssl/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/chat/chat_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/chat/posix_chat_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/chat/chat_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/server.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/connection.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/reply.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/reply.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/connection.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/server.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/connection.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/reply.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/reply.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/io_context_pool.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/io_context_pool.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/connection.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/server.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/reply.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/reply.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/request_parser.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/main.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/client/sync_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/client/async_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/server.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/connection.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/reply.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/reply.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/connection.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/blocking_token_tcp_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/async_tcp_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/blocking_udp_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/blocking_tcp_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/allocation/server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/blocking_tcp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/blocking_udp_echo_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/async_udp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/blocking_udp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/async_tcp_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/blocking_tcp_echo_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/timers/time_t_timer.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/spawn/parallel_grep.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/spawn/echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/icmp/ipv4_header.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/icmp/ping.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/socks4/socks4.hpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp03/socks4/sync_client.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/double_buffered_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/chat_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/range_based_for.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/refactored_echo_server.cpp
/home/killer/boost_1_69_0/doc/html/boost_asio/index.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer3/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime4.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime6.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime2/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer5/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime5.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime1.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer2/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime4/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime6/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime7.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer1/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer4/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime5/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer2.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer3.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime7/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime3/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime1/src.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/core/allocation.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/core/strands.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/core/line_based.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/core/coroutines_ts.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/core/coroutine.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/core/spawn.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/cpp2011/move_handlers.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/cpp2011/futures.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/posix/fork.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/posix/stream_descriptor.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/signals.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/networking/protocols.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/networking/other_protocols.html
/home/killer/boost_1_69_0/doc/html/boost_asio/overview/ssl.html
/home/killer/boost_1_69_0/doc/html/boost_asio/net_ts.html
/home/killer/boost_1_69_0/doc/html/boost_process/tutorial.html
/home/killer/boost_1_69_0/doc/html/boost_process/extend.html

```
</details>

## Задание 8
*Скомпилирутйе boost.*

С первого раза оно не скомпилировало, но сработали вот эти команды:

```sh
$ cd ~/boost_1_69_0
$ sed -i 's/#if PTHREAD_STACK_MIN > 0/#ifdef PTHREAD_STACK_MIN/' boost/thread/pthread/thread_data.hpp
$ ./bootstrap.sh
$ sudo apt install build-essential
$ ./b2 clean
$ ./b2
```
<details>
<summary> Процесс компиляции </summary>
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
Unicode/ICU support for Boost.Regex?... not found.
Backing up existing Boost.Build configuration in project-config.jam.1
Generating Boost.Build configuration in project-config.jam...

Bootstrapping is done. To build, run:

    ./b2
    
To adjust configuration, edit 'project-config.jam'.
Further information:

   - Command line help:
     ./b2 --help
     
   - Getting started guide: 
     http://www.boost.org/more/getting_started/unix-variants.html
     
   - Boost.Build documentation:
     http://www.boost.org/build/doc/html/index.html

Performing configuration checks

    - default address-model    : 64-bit (cached)
    - default architecture     : x86 (cached)

Building the Boost C++ Libraries.


    - C++11 mutex              : yes (cached)
    - lockfree boost::atomic_flag : yes (cached)
    - Boost.Config Feature Check: cxx11_auto_declarations : yes (cached)
    - Boost.Config Feature Check: cxx11_constexpr : yes (cached)
    - Boost.Config Feature Check: cxx11_defaulted_functions : yes (cached)
    - Boost.Config Feature Check: cxx11_final : yes (cached)
    - Boost.Config Feature Check: cxx11_hdr_mutex : yes (cached)
    - Boost.Config Feature Check: cxx11_hdr_tuple : yes (cached)
    - Boost.Config Feature Check: cxx11_lambdas : yes (cached)
    - Boost.Config Feature Check: cxx11_noexcept : yes (cached)
    - Boost.Config Feature Check: cxx11_nullptr : yes (cached)
    - Boost.Config Feature Check: cxx11_rvalue_references : yes (cached)
    - Boost.Config Feature Check: cxx11_template_aliases : yes (cached)
    - Boost.Config Feature Check: cxx11_thread_local : yes (cached)
    - Boost.Config Feature Check: cxx11_variadic_templates : yes (cached)
    - has_icu builds           : no  (cached)
warning: Graph library does not contain MPI-based parallel components.
note: to enable them, add "using mpi ;" to your user-config.jam
    - zlib                     : no  (cached)
    - bzip2                    : no  (cached)
    - lzma                     : no  (cached)
    - zstd                     : no  (cached)
    - iconv (libc)             : yes (cached)
    - icu                      : no  (cached)
    - icu (lib64)              : no  (cached)
    - native-atomic-int32-supported : yes (cached)
    - native-syslog-supported  : yes (cached)
    - pthread-supports-robust-mutexes : yes (cached)
    - compiler-supports-ssse3  : yes (cached)
    - compiler-supports-avx2   : yes (cached)
    - gcc visibility           : yes (cached)
    - long double support      : yes (cached)
warning: skipping optional Message Passing Interface (MPI) library.
note: to enable MPI support, add "using mpi ;" to user-config.jam.
note: to suppress this message, pass "--without-mpi" to bjam.
note: otherwise, you can safely ignore this message.
warning: No python installation configured and autoconfiguration
note: failed.  See http://www.boost.org/libs/python/doc/building.html
note: for configuration instructions or pass --without-python to
note: suppress this message and silently skip all Boost.Python targets
    - libbacktrace builds      : yes (cached)
    - addr2line builds         : yes (cached)
    - WinDbg builds            : no  (cached)
    - WinDbgCached builds      : no  (cached)
    - BOOST_COMP_GNUC >= 4.3.0 : no  (cached)
    - zlib                     : no  (cached)
    - bzip2                    : no  (cached)
    - lzma                     : no  (cached)
    - zstd                     : no  (cached)

Component configuration:

    - atomic                   : building
    - chrono                   : building
    - container                : building
    - context                  : building
    - contract                 : building
    - coroutine                : building
    - date_time                : building
    - exception                : building
    - fiber                    : building
    - filesystem               : building
    - graph                    : building
    - graph_parallel           : building
    - iostreams                : building
    - locale                   : building
    - log                      : building
    - math                     : building
    - mpi                      : building
    - program_options          : building
    - python                   : building
    - random                   : building
    - regex                    : building
    - serialization            : building
    - stacktrace               : building
    - system                   : building
    - test                     : building
    - thread                   : building
    - timer                    : building
    - type_erasure             : building
    - wave                     : building

...patience...
...patience...
...patience...
...patience...
...patience...
...patience...
...found 12316 targets...
...updating 60 targets...
gcc.compile.c++ bin.v2/libs/context/build/gcc-13.3.0/release/threading-multi/visibility-hidden/posix/stack_traits.o
gcc.link.dll bin.v2/libs/context/build/gcc-13.3.0/release/threading-multi/visibility-hidden/libboost_context.so.1.69.0
common.copy stage/lib/libboost_context.so.1.69.0
ln-UNIX stage/lib/libboost_context.so
gcc.compile.c++ bin.v2/libs/thread/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/pthread/thread.o
In file included from ./boost/thread/thread_only.hpp:17,
                 from libs/thread/src/pthread/thread.cpp:11:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
In file included from ./boost/functional/hash.hpp:6,
                 from ./boost/thread/detail/thread.hpp:38,
                 from ./boost/thread/thread_only.hpp:22:
./boost/container_hash/hash.hpp: At global scope:
./boost/container_hash/hash.hpp:130:33: warning: ‘template<class _Arg, class _Result> struct std::unary_function’ is deprecated [-Wdeprecated-declarations]
  130 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^~~~~~~~~~~~~~
In file included from /usr/include/c++/13/string:49,
                 from ./boost/thread/exceptions.hpp:20,
                 from ./boost/thread/pthread/thread_data.hpp:10:
/usr/include/c++/13/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
In file included from ./boost/concept/assert.hpp:35,
                 from ./boost/concept_check.hpp:20,
                 from ./boost/range/concepts.hpp:19,
                 from ./boost/range/size_type.hpp:20,
                 from ./boost/range/size.hpp:21,
                 from ./boost/range/functions.hpp:20,
                 from ./boost/range/iterator_range_core.hpp:38,
                 from ./boost/algorithm/string/iter_find.hpp:19,
                 from ./boost/algorithm/string/split.hpp:16,
                 from libs/thread/src/pthread/thread.cpp:34:
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::constraint<Model>::failed() [with Model = boost::algorithm::FinderConcept<boost::algorithm::detail::token_finderF<boost::algorithm::detail::is_any_ofF<char> >, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/algorithm/string/iter_find.hpp:77:13:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:47:52: warning: ‘this’ pointer is null [-Wnonnull]
   47 |     static void failed() { ((Model*)0)->constraints(); }
      |                            ~~~~~~~~~~~~~~~~~~~~~~~~^~
In file included from ./boost/algorithm/string/iter_find.hpp:26:
./boost/algorithm/string/concept.hpp:40:18: note: in a call to non-static member function ‘void boost::algorithm::FinderConcept<FinderT, IteratorT>::constraints() [with FinderT = boost::algorithm::detail::token_finderF<boost::algorithm::detail::is_any_ofF<char> >; IteratorT = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   40 |             void constraints()
      |                  ^~~~~~~~~~~
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/concept_check.hpp:167:5:   required from ‘struct boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:125:16:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   [ skipping 14 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
In file included from ./boost/concept_check.hpp:31:
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >]’:
./boost/concept_check.hpp:208:5:   required from ‘struct boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>)>’
./boost/iterator/iterator_concepts.hpp:114:7:   [ skipping 18 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’:
./boost/iterator/iterator_concepts.hpp:114:7:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 13 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::Convertible<X, Y>::~Convertible() [with X = boost::iterators::random_access_traversal_tag; Y = boost::iterators::incrementable_traversal_tag]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:208:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  208 |     BOOST_CONCEPT_USAGE(Convertible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/range/concepts.hpp:136:13:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 13 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/concept_check.hpp:233:5:   required from ‘struct boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 13 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >]’:
./boost/concept_check.hpp:208:5:   required from ‘struct boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>)>’
./boost/range/concepts.hpp:152:13:   [ skipping 17 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’:
./boost/range/concepts.hpp:152:13:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >)>’
./boost/range/concepts.hpp:278:9:   [ skipping 12 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::Convertible<X, Y>::~Convertible() [with X = boost::iterators::random_access_traversal_tag; Y = boost::iterators::single_pass_traversal_tag]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:208:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  208 |     BOOST_CONCEPT_USAGE(Convertible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/range/concepts.hpp:158:13:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >)>’
./boost/range/concepts.hpp:278:9:   [ skipping 12 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/range/concepts.hpp:278:9:   required from ‘struct boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >)>’
./boost/range/algorithm/equal.hpp:174:13:   [ skipping 7 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::range_detail::SinglePassIteratorConcept<Iterator>::~SinglePassIteratorConcept() [with Iterator = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:158:13: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  158 |             BOOST_CONCEPT_USAGE(SinglePassIteratorConcept)
      |             ^~~~~~~~~~~~~~~~~~~
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >]’:
./boost/range/concepts.hpp:284:9:   required from ‘struct boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >)>’
./boost/range/algorithm/equal.hpp:174:13:   [ skipping 7 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/range/algorithm/equal.hpp:174:13:   required from ‘bool boost::range::equal(const SinglePassRange1&, const SinglePassRange2&) [with SinglePassRange1 = boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; SinglePassRange2 = boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/range/iterator_range_core.hpp:646:32:   required from ‘bool boost::operator==(const iterator_range<IteratorT>&, const iterator_range<Iterator2T>&) [with Iterator1T = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >; Iterator2T = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/find_iterator.hpp:333:32:   required from ‘bool boost::algorithm::split_iterator<IteratorT>::equal(const boost::algorithm::split_iterator<IteratorT>&) const [with IteratorT = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
./boost/iterator/iterator_facade.hpp:568:26:   required from ‘static bool boost::iterators::iterator_core_access::equal(const Facade1&, const Facade2&, mpl_::true_) [with Facade1 = boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; Facade2 = boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; mpl_::true_ = mpl_::bool_<true>]’
./boost/iterator/iterator_facade.hpp:900:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator==(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; V1 = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; TC1 = forward_traversal_tag; Reference1 = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >&; Difference1 = long int; Derived2 = boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; V2 = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; TC2 = forward_traversal_tag; Reference2 = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >&; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
./boost/iterator/iterator_adaptor.hpp:305:29:   [ skipping 2 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::SinglePassRangeConcept<T>::~SinglePassRangeConcept() [with T = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:284:9: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  284 |         BOOST_CONCEPT_USAGE(SinglePassRangeConcept)
      |         ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept_check.hpp:167:5:   required from ‘struct boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:125:16:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   [ skipping 15 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::CopyConstructible<TT>::~CopyConstructible() [with TT = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:167:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  167 |     BOOST_CONCEPT_USAGE(CopyConstructible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >]’
./boost/concept_check.hpp:208:5:   required from ‘struct boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 19 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::Convertible<X, Y>::~Convertible() [with X = boost::iterators::random_access_traversal_tag; Y = boost::iterators::incrementable_traversal_tag]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:208:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  208 |     BOOST_CONCEPT_USAGE(Convertible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/range/concepts.hpp:136:13:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   [ skipping 14 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::range_detail::IncrementableIteratorConcept<Iterator>::~IncrementableIteratorConcept() [with Iterator = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:136:13: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  136 |             BOOST_CONCEPT_USAGE(IncrementableIteratorConcept)
      |             ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept_check.hpp:233:5:   required from ‘struct boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   [ skipping 14 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::EqualityComparable<TT>::~EqualityComparable() [with TT = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:233:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  233 |     BOOST_CONCEPT_USAGE(EqualityComparable) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >]’
./boost/concept_check.hpp:208:5:   required from ‘struct boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 18 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::Convertible<X, Y>::~Convertible() [with X = boost::iterators::random_access_traversal_tag; Y = boost::iterators::single_pass_traversal_tag]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:208:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  208 |     BOOST_CONCEPT_USAGE(Convertible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/range/concepts.hpp:158:13:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 13 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::range_detail::SinglePassIteratorConcept<Iterator>::~SinglePassIteratorConcept() [with Iterator = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:158:13: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  158 |             BOOST_CONCEPT_USAGE(SinglePassIteratorConcept)
      |             ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >]’
./boost/range/concepts.hpp:284:9:   required from ‘struct boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 8 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::SinglePassRangeConcept<T>::~SinglePassRangeConcept() [with T = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:284:9: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  284 |         BOOST_CONCEPT_USAGE(SinglePassRangeConcept)
      |         ^~~~~~~~~~~~~~~~~~~
gcc.link.dll bin.v2/libs/thread/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/libboost_thread.so.1.69.0
common.copy stage/lib/libboost_thread.so.1.69.0
ln-UNIX stage/lib/libboost_thread.so
gcc.compile.c++ bin.v2/libs/coroutine/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/posix/stack_traits.o
In file included from ./boost/coroutine/stack_traits.hpp:14,
                 from libs/coroutine/src/posix/stack_traits.cpp:7:
./boost/coroutine/detail/config.hpp:17:4: warning: #warning "Boost.Coroutine is now deprecated. Please switch to Boost.Coroutine2. To disable this warning message, define BOOST_COROUTINES_NO_DEPRECATION_WARNING." [-Wcpp]
   17 | #  warning                  "Boost.Coroutine is now deprecated. Please switch to Boost.Coroutine2. To disable this warning message, define BOOST_COROUTINES_NO_DEPRECATION_WARNING."
      |    ^~~~~~~
In file included from ./boost/thread/thread_only.hpp:17,
                 from ./boost/thread/thread.hpp:12,
                 from ./boost/thread.hpp:13,
                 from libs/coroutine/src/posix/stack_traits.cpp:22:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
In file included from ./boost/functional/hash.hpp:6,
                 from ./boost/thread/detail/thread.hpp:38,
                 from ./boost/thread/thread_only.hpp:22:
./boost/container_hash/hash.hpp: At global scope:
./boost/container_hash/hash.hpp:130:33: warning: ‘template<class _Arg, class _Result> struct std::unary_function’ is deprecated [-Wdeprecated-declarations]
  130 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^~~~~~~~~~~~~~
In file included from /usr/include/c++/13/string:49,
                 from ./boost/thread/exceptions.hpp:20,
                 from ./boost/thread/pthread/thread_data.hpp:10:
/usr/include/c++/13/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
gcc.link.dll bin.v2/libs/coroutine/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/libboost_coroutine.so.1.69.0
common.copy stage/lib/libboost_coroutine.so.1.69.0
ln-UNIX stage/lib/libboost_coroutine.so
gcc.link.dll bin.v2/libs/fiber/build/gcc-13.3.0/release/threading-multi/visibility-hidden/libboost_fiber.so.1.69.0
common.copy stage/lib/libboost_fiber.so.1.69.0
ln-UNIX stage/lib/libboost_fiber.so
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/severity_level.o
In file included from ./boost/thread/thread_only.hpp:17,
                 from ./boost/thread/thread.hpp:12,
                 from libs/log/src/severity_level.cpp:23:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
In file included from ./boost/functional/hash.hpp:6,
                 from ./boost/thread/detail/thread.hpp:38,
                 from ./boost/thread/thread_only.hpp:22:
./boost/container_hash/hash.hpp: At global scope:
./boost/container_hash/hash.hpp:130:33: warning: ‘template<class _Arg, class _Result> struct std::unary_function’ is deprecated [-Wdeprecated-declarations]
  130 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^~~~~~~~~~~~~~
In file included from /usr/include/c++/13/functional:49,
                 from ./boost/config/no_tr1/functional.hpp:21,
                 from ./boost/smart_ptr/intrusive_ptr.hpp:24,
                 from ./boost/log/sources/severity_feature.hpp:20,
                 from libs/log/src/severity_level.cpp:18:
/usr/include/c++/13/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/thread_id.o
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/once_block.o
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/event.o
In file included from ./boost/thread/pthread/condition_variable.hpp:14,
                 from ./boost/thread/condition_variable.hpp:16,
                 from ./boost/log/detail/event.hpp:42,
                 from libs/log/src/event.cpp:23:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
gcc.link.dll bin.v2/libs/log/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/libboost_log.so.1.69.0
common.copy stage/lib/libboost_log.so.1.69.0
ln-UNIX stage/lib/libboost_log.so
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/setup/init_from_settings.o
In file included from ./boost/thread/thread_only.hpp:17,
                 from ./boost/thread/thread.hpp:12,
                 from ./boost/log/sinks/async_frontend.hpp:39,
                 from ./boost/log/sinks.hpp:25,
                 from libs/log/src/setup/init_from_settings.cpp:54:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
In file included from ./boost/functional/hash.hpp:6,
                 from ./boost/thread/detail/thread.hpp:38,
                 from ./boost/thread/thread_only.hpp:22:
./boost/container_hash/hash.hpp: At global scope:
./boost/container_hash/hash.hpp:130:33: warning: ‘template<class _Arg, class _Result> struct std::unary_function’ is deprecated [-Wdeprecated-declarations]
  130 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^~~~~~~~~~~~~~
In file included from /usr/include/c++/13/string:49,
                 from /usr/include/c++/13/bits/locale_classes.h:40,
                 from /usr/include/c++/13/bits/ios_base.h:41,
                 from /usr/include/c++/13/ios:44,
                 from libs/log/src/setup/init_from_settings.cpp:28:
/usr/include/c++/13/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
gcc.link.dll bin.v2/libs/log/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/libboost_log_setup.so.1.69.0
common.copy stage/lib/libboost_log_setup.so.1.69.0
ln-UNIX stage/lib/libboost_log_setup.so
gcc.compile.c++ bin.v2/libs/type_erasure/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/dynamic_binding.o
In file included from ./boost/thread/pthread/condition_variable.hpp:14,
                 from ./boost/thread/condition_variable.hpp:16,
                 from ./boost/thread/pthread/shared_mutex.hpp:15,
                 from ./boost/thread/shared_mutex.hpp:28,
                 from libs/type_erasure/src/dynamic_binding.cpp:14:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
gcc.link.dll bin.v2/libs/type_erasure/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/libboost_type_erasure.so.1.69.0
common.copy stage/lib/libboost_type_erasure.so.1.69.0
ln-UNIX stage/lib/libboost_type_erasure.so
gcc.link.dll bin.v2/libs/wave/build/gcc-13.3.0/release/threadapi-pthread/threading-multi/visibility-hidden/libboost_wave.so.1.69.0
common.copy stage/lib/libboost_wave.so.1.69.0
ln-UNIX stage/lib/libboost_wave.so
gcc.compile.c++ bin.v2/libs/context/build/gcc-13.3.0/release/link-static/threading-multi/visibility-hidden/posix/stack_traits.o
gcc.archive bin.v2/libs/context/build/gcc-13.3.0/release/link-static/threading-multi/visibility-hidden/libboost_context.a
common.copy stage/lib/libboost_context.a
gcc.compile.c++ bin.v2/libs/thread/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/pthread/thread.o
In file included from ./boost/thread/thread_only.hpp:17,
                 from libs/thread/src/pthread/thread.cpp:11:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
In file included from ./boost/functional/hash.hpp:6,
                 from ./boost/thread/detail/thread.hpp:38,
                 from ./boost/thread/thread_only.hpp:22:
./boost/container_hash/hash.hpp: At global scope:
./boost/container_hash/hash.hpp:130:33: warning: ‘template<class _Arg, class _Result> struct std::unary_function’ is deprecated [-Wdeprecated-declarations]
  130 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^~~~~~~~~~~~~~
In file included from /usr/include/c++/13/string:49,
                 from ./boost/thread/exceptions.hpp:20,
                 from ./boost/thread/pthread/thread_data.hpp:10:
/usr/include/c++/13/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
In file included from ./boost/concept/assert.hpp:35,
                 from ./boost/concept_check.hpp:20,
                 from ./boost/range/concepts.hpp:19,
                 from ./boost/range/size_type.hpp:20,
                 from ./boost/range/size.hpp:21,
                 from ./boost/range/functions.hpp:20,
                 from ./boost/range/iterator_range_core.hpp:38,
                 from ./boost/algorithm/string/iter_find.hpp:19,
                 from ./boost/algorithm/string/split.hpp:16,
                 from libs/thread/src/pthread/thread.cpp:34:
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::constraint<Model>::failed() [with Model = boost::algorithm::FinderConcept<boost::algorithm::detail::token_finderF<boost::algorithm::detail::is_any_ofF<char> >, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/algorithm/string/iter_find.hpp:77:13:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:47:52: warning: ‘this’ pointer is null [-Wnonnull]
   47 |     static void failed() { ((Model*)0)->constraints(); }
      |                            ~~~~~~~~~~~~~~~~~~~~~~~~^~
In file included from ./boost/algorithm/string/iter_find.hpp:26:
./boost/algorithm/string/concept.hpp:40:18: note: in a call to non-static member function ‘void boost::algorithm::FinderConcept<FinderT, IteratorT>::constraints() [with FinderT = boost::algorithm::detail::token_finderF<boost::algorithm::detail::is_any_ofF<char> >; IteratorT = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   40 |             void constraints()
      |                  ^~~~~~~~~~~
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/concept_check.hpp:167:5:   required from ‘struct boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:125:16:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   [ skipping 14 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
In file included from ./boost/concept_check.hpp:31:
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >]’:
./boost/concept_check.hpp:208:5:   required from ‘struct boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>)>’
./boost/iterator/iterator_concepts.hpp:114:7:   [ skipping 18 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’:
./boost/iterator/iterator_concepts.hpp:114:7:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 13 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::Convertible<X, Y>::~Convertible() [with X = boost::iterators::random_access_traversal_tag; Y = boost::iterators::incrementable_traversal_tag]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:208:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  208 |     BOOST_CONCEPT_USAGE(Convertible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/range/concepts.hpp:136:13:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 13 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/concept_check.hpp:233:5:   required from ‘struct boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 13 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >]’:
./boost/concept_check.hpp:208:5:   required from ‘struct boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>)>’
./boost/range/concepts.hpp:152:13:   [ skipping 17 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’:
./boost/range/concepts.hpp:152:13:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >)>’
./boost/range/concepts.hpp:278:9:   [ skipping 12 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::Convertible<X, Y>::~Convertible() [with X = boost::iterators::random_access_traversal_tag; Y = boost::iterators::single_pass_traversal_tag]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:208:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  208 |     BOOST_CONCEPT_USAGE(Convertible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/range/concepts.hpp:158:13:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >)>’
./boost/range/concepts.hpp:278:9:   [ skipping 12 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/range/concepts.hpp:278:9:   required from ‘struct boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >)>’
./boost/range/algorithm/equal.hpp:174:13:   [ skipping 7 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::range_detail::SinglePassIteratorConcept<Iterator>::~SinglePassIteratorConcept() [with Iterator = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:158:13: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  158 |             BOOST_CONCEPT_USAGE(SinglePassIteratorConcept)
      |             ^~~~~~~~~~~~~~~~~~~
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >]’:
./boost/range/concepts.hpp:284:9:   required from ‘struct boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >’
./boost/concept/detail/general.hpp:51:8:   required from ‘struct boost::concepts::requirement_<void (*)(boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >)>’
./boost/range/algorithm/equal.hpp:174:13:   [ skipping 7 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:16:5: note: in a call to non-static member function ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |     ^
./boost/concept/detail/general.hpp: In instantiation of ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/range/algorithm/equal.hpp:174:13:   required from ‘bool boost::range::equal(const SinglePassRange1&, const SinglePassRange2&) [with SinglePassRange1 = boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; SinglePassRange2 = boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/range/iterator_range_core.hpp:646:32:   required from ‘bool boost::operator==(const iterator_range<IteratorT>&, const iterator_range<Iterator2T>&) [with Iterator1T = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >; Iterator2T = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/find_iterator.hpp:333:32:   required from ‘bool boost::algorithm::split_iterator<IteratorT>::equal(const boost::algorithm::split_iterator<IteratorT>&) const [with IteratorT = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
./boost/iterator/iterator_facade.hpp:568:26:   required from ‘static bool boost::iterators::iterator_core_access::equal(const Facade1&, const Facade2&, mpl_::true_) [with Facade1 = boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; Facade2 = boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; mpl_::true_ = mpl_::bool_<true>]’
./boost/iterator/iterator_facade.hpp:900:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator==(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; V1 = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; TC1 = forward_traversal_tag; Reference1 = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >&; Difference1 = long int; Derived2 = boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; V2 = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >; TC2 = forward_traversal_tag; Reference2 = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >&; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
./boost/iterator/iterator_adaptor.hpp:305:29:   [ skipping 2 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/detail/general.hpp:39:47: warning: ‘this’ pointer is null [-Wnonnull]
   39 |     static void failed() { ((Model*)0)->~Model(); }
      |                            ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::SinglePassRangeConcept<T>::~SinglePassRangeConcept() [with T = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:284:9: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  284 |         BOOST_CONCEPT_USAGE(SinglePassRangeConcept)
      |         ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept_check.hpp:167:5:   required from ‘struct boost::CopyConstructible<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:125:16:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   [ skipping 15 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::CopyConstructible<TT>::~CopyConstructible() [with TT = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:167:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  167 |     BOOST_CONCEPT_USAGE(CopyConstructible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >]’
./boost/concept_check.hpp:208:5:   required from ‘struct boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag>]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::incrementable_traversal_tag> >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 19 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::Convertible<X, Y>::~Convertible() [with X = boost::iterators::random_access_traversal_tag; Y = boost::iterators::incrementable_traversal_tag]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:208:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  208 |     BOOST_CONCEPT_USAGE(Convertible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/range/concepts.hpp:136:13:   required from ‘struct boost::range_detail::IncrementableIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   [ skipping 14 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::range_detail::IncrementableIteratorConcept<Iterator>::~IncrementableIteratorConcept() [with Iterator = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:136:13: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  136 |             BOOST_CONCEPT_USAGE(IncrementableIteratorConcept)
      |             ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept_check.hpp:233:5:   required from ‘struct boost::EqualityComparable<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/range/concepts.hpp:147:16:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   [ skipping 14 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::EqualityComparable<TT>::~EqualityComparable() [with TT = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:233:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  233 |     BOOST_CONCEPT_USAGE(EqualityComparable) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >]’
./boost/concept_check.hpp:208:5:   required from ‘struct boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag>]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::Convertible<boost::iterators::random_access_traversal_tag, boost::iterators::single_pass_traversal_tag> >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 18 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::Convertible<X, Y>::~Convertible() [with X = boost::iterators::random_access_traversal_tag; Y = boost::iterators::single_pass_traversal_tag]’
   30 |       ~model()
      |       ^
./boost/concept_check.hpp:208:5: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  208 |     BOOST_CONCEPT_USAGE(Convertible) {
      |     ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/range/concepts.hpp:158:13:   required from ‘struct boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::range_detail::SinglePassIteratorConcept<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 13 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::range_detail::SinglePassIteratorConcept<Iterator>::~SinglePassIteratorConcept() [with Iterator = __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:158:13: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  158 |             BOOST_CONCEPT_USAGE(SinglePassIteratorConcept)
      |             ^~~~~~~~~~~~~~~~~~~
./boost/concept/usage.hpp: In instantiation of ‘boost::concepts::usage_requirements<Model>::~usage_requirements() [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’:
./boost/concept/detail/general.hpp:39:47:   required from ‘static void boost::concepts::requirement<boost::concepts::failed************ Model::************>::failed() [with Model = boost::concepts::usage_requirements<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >]’
./boost/range/concepts.hpp:284:9:   required from ‘struct boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >’
./boost/concept/detail/has_constraints.hpp:32:62:   required by substitution of ‘template<class Model> boost::concepts::detail::yes boost::concepts::detail::has_constraints_(Model*, wrap_constraints<Model, (& Model::constraints)>*) [with Model = boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > >]’
./boost/concept/detail/has_constraints.hpp:42:5:   required from ‘const bool boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >::value’
./boost/concept/detail/has_constraints.hpp:45:51:   required from ‘struct boost::concepts::not_satisfied<boost::SinglePassRangeConcept<const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > > > >’
./boost/concept/detail/general.hpp:51:8:   [ skipping 8 instantiation contexts, use -ftemplate-backtrace-limit=0 to disable ]
./boost/iterator/iterator_facade.hpp:901:3:   required from ‘typename boost::iterators::detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<boost::iterators::detail::always_bool2, Derived1, Derived2>::type>::type boost::iterators::operator!=(const iterator_facade<Derived1, V1, TC1, Reference1, Difference1>&, const iterator_facade<Derived2, V2, TC2, Reference2, Difference2>&) [with Derived1 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V1 = std::__cxx11::basic_string<char>; TC1 = forward_traversal_tag; Reference1 = std::__cxx11::basic_string<char>; Difference1 = long int; Derived2 = transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, use_default, use_default>; V2 = std::__cxx11::basic_string<char>; TC2 = forward_traversal_tag; Reference2 = std::__cxx11::basic_string<char>; Difference2 = long int; typename detail::enable_if_interoperable<Derived1, Derived2, typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type>::type = bool; typename boost::mpl::apply2<detail::always_bool2, Derived1, Derived2>::type = bool]’
/usr/include/c++/13/bits/stl_vector.h:1671:21:   required from ‘void std::vector<_Tp, _Alloc>::_M_range_initialize(_InputIterator, _InputIterator, std::input_iterator_tag) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >]’
/usr/include/c++/13/bits/stl_vector.h:711:23:   required from ‘std::vector<_Tp, _Alloc>::vector(_InputIterator, _InputIterator, const allocator_type&) [with _InputIterator = boost::iterators::transform_iterator<boost::algorithm::detail::copy_iterator_rangeF<std::__cxx11::basic_string<char>, __gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::algorithm::split_iterator<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >, boost::iterators::use_default, boost::iterators::use_default>; <template-parameter-2-2> = void; _Tp = std::__cxx11::basic_string<char>; _Alloc = std::allocator<std::__cxx11::basic_string<char> >; allocator_type = std::allocator<std::__cxx11::basic_string<char> >]’
./boost/algorithm/string/iter_find.hpp:178:31:   required from ‘SequenceSequenceT& boost::algorithm::iter_split(SequenceSequenceT&, RangeT&, FinderT) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; FinderT = detail::token_finderF<detail::is_any_ofF<char> >]’
./boost/algorithm/string/split.hpp:146:50:   required from ‘SequenceSequenceT& boost::algorithm::split(SequenceSequenceT&, RangeT&, PredicateT, token_compress_mode_type) [with SequenceSequenceT = std::vector<std::__cxx11::basic_string<char> >; RangeT = std::__cxx11::basic_string<char>; PredicateT = detail::is_any_ofF<char>]’
libs/thread/src/pthread/thread.cpp:537:29:   required from here
./boost/concept/usage.hpp:16:48: warning: ‘this’ pointer is null [-Wnonnull]
   16 |     ~usage_requirements() { ((Model*)0)->~Model(); }
      |                             ~~~~~~~~~~~~~~~~~~~^~
./boost/concept/usage.hpp:30:7: note: in a call to non-static member function ‘boost::SinglePassRangeConcept<T>::~SinglePassRangeConcept() [with T = const boost::iterator_range<__gnu_cxx::__normal_iterator<char*, std::__cxx11::basic_string<char> > >]’
   30 |       ~model()
      |       ^
./boost/range/concepts.hpp:284:9: note: in expansion of macro ‘BOOST_CONCEPT_USAGE’
  284 |         BOOST_CONCEPT_USAGE(SinglePassRangeConcept)
      |         ^~~~~~~~~~~~~~~~~~~
gcc.archive bin.v2/libs/thread/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/libboost_thread.a
common.copy stage/lib/libboost_thread.a
gcc.compile.c++ bin.v2/libs/coroutine/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/posix/stack_traits.o
In file included from ./boost/coroutine/stack_traits.hpp:14,
                 from libs/coroutine/src/posix/stack_traits.cpp:7:
./boost/coroutine/detail/config.hpp:17:4: warning: #warning "Boost.Coroutine is now deprecated. Please switch to Boost.Coroutine2. To disable this warning message, define BOOST_COROUTINES_NO_DEPRECATION_WARNING." [-Wcpp]
   17 | #  warning                  "Boost.Coroutine is now deprecated. Please switch to Boost.Coroutine2. To disable this warning message, define BOOST_COROUTINES_NO_DEPRECATION_WARNING."
      |    ^~~~~~~
In file included from ./boost/thread/thread_only.hpp:17,
                 from ./boost/thread/thread.hpp:12,
                 from ./boost/thread.hpp:13,
                 from libs/coroutine/src/posix/stack_traits.cpp:22:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
In file included from ./boost/functional/hash.hpp:6,
                 from ./boost/thread/detail/thread.hpp:38,
                 from ./boost/thread/thread_only.hpp:22:
./boost/container_hash/hash.hpp: At global scope:
./boost/container_hash/hash.hpp:130:33: warning: ‘template<class _Arg, class _Result> struct std::unary_function’ is deprecated [-Wdeprecated-declarations]
  130 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^~~~~~~~~~~~~~
In file included from /usr/include/c++/13/string:49,
                 from ./boost/thread/exceptions.hpp:20,
                 from ./boost/thread/pthread/thread_data.hpp:10:
/usr/include/c++/13/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
gcc.archive bin.v2/libs/coroutine/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/libboost_coroutine.a
common.copy stage/lib/libboost_coroutine.a
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/severity_level.o
In file included from ./boost/thread/thread_only.hpp:17,
                 from ./boost/thread/thread.hpp:12,
                 from libs/log/src/severity_level.cpp:23:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
In file included from ./boost/functional/hash.hpp:6,
                 from ./boost/thread/detail/thread.hpp:38,
                 from ./boost/thread/thread_only.hpp:22:
./boost/container_hash/hash.hpp: At global scope:
./boost/container_hash/hash.hpp:130:33: warning: ‘template<class _Arg, class _Result> struct std::unary_function’ is deprecated [-Wdeprecated-declarations]
  130 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^~~~~~~~~~~~~~
In file included from /usr/include/c++/13/functional:49,
                 from ./boost/config/no_tr1/functional.hpp:21,
                 from ./boost/smart_ptr/intrusive_ptr.hpp:24,
                 from ./boost/log/sources/severity_feature.hpp:20,
                 from libs/log/src/severity_level.cpp:18:
/usr/include/c++/13/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/thread_id.o
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/once_block.o
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/event.o
In file included from ./boost/thread/pthread/condition_variable.hpp:14,
                 from ./boost/thread/condition_variable.hpp:16,
                 from ./boost/log/detail/event.hpp:42,
                 from libs/log/src/event.cpp:23:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
gcc.archive bin.v2/libs/log/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/libboost_log.a
common.copy stage/lib/libboost_log.a
gcc.compile.c++ bin.v2/libs/log/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/setup/init_from_settings.o
In file included from ./boost/thread/thread_only.hpp:17,
                 from ./boost/thread/thread.hpp:12,
                 from ./boost/log/sinks/async_frontend.hpp:39,
                 from ./boost/log/sinks.hpp:25,
                 from libs/log/src/setup/init_from_settings.cpp:54:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
In file included from ./boost/functional/hash.hpp:6,
                 from ./boost/thread/detail/thread.hpp:38,
                 from ./boost/thread/thread_only.hpp:22:
./boost/container_hash/hash.hpp: At global scope:
./boost/container_hash/hash.hpp:130:33: warning: ‘template<class _Arg, class _Result> struct std::unary_function’ is deprecated [-Wdeprecated-declarations]
  130 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^~~~~~~~~~~~~~
In file included from /usr/include/c++/13/string:49,
                 from /usr/include/c++/13/bits/locale_classes.h:40,
                 from /usr/include/c++/13/bits/ios_base.h:41,
                 from /usr/include/c++/13/ios:44,
                 from libs/log/src/setup/init_from_settings.cpp:28:
/usr/include/c++/13/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
gcc.archive bin.v2/libs/log/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/libboost_log_setup.a
common.copy stage/lib/libboost_log_setup.a
gcc.compile.c++ bin.v2/libs/type_erasure/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/dynamic_binding.o
In file included from ./boost/thread/pthread/condition_variable.hpp:14,
                 from ./boost/thread/condition_variable.hpp:16,
                 from ./boost/thread/pthread/shared_mutex.hpp:15,
                 from ./boost/thread/shared_mutex.hpp:28,
                 from libs/type_erasure/src/dynamic_binding.cpp:14:
./boost/thread/pthread/thread_data.hpp: In member function ‘void boost::thread_attributes::set_stack_size(std::size_t)’:
./boost/thread/pthread/thread_data.hpp:61:19: warning: comparison of integer expressions of different signedness: ‘std::size_t’ {aka ‘long unsigned int’} and ‘long int’ [-Wsign-compare]
   61 |           if (size<PTHREAD_STACK_MIN) size=PTHREAD_STACK_MIN;
      |                   ^
gcc.archive bin.v2/libs/type_erasure/build/gcc-13.3.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/libboost_type_erasure.a
common.copy stage/lib/libboost_type_erasure.a
...updated 60 targets...


The Boost C++ Libraries were successfully built!

The following directory should be added to compiler include paths:

    /home/killer/boost_1_69_0

The following directory should be added to linker library paths:

    /home/killer/boost_1_69_0/stage/lib
</details>

## Задание 9
*Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию* `~/boost-libs`.

```sh
$ mv ~/boost_1_69_0/stage/lib ~/boost-libs
```

## Задание 10
*Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.*

Введем команды:
```sh
$ cd ~/boost-libs
$ ls -lh
```
`-lh` означает вывод полной информации о файлах. В итоге получим такой вывод:

<details>

<summary>Вывод команды ls </summary>

```
total 760K
-rw-r--r--   1 killer killer    0 Mar 29 14:35 C:UsersuserAlexanderKonyaevTEST.md
-rw-r--r--   1 killer killer  291 Dec  5  2018 INSTALL
-rw-r--r--   1 killer killer  13K Dec  5  2018 Jamroot
-rw-r--r--   1 killer killer 1.4K Dec  5  2018 LICENSE_1_0.txt
-rw-r--r--   1 killer killer  207 Mar 23 10:14 README.md
-rwxr-xr-x   1 killer killer 302K Mar 29 14:40 b2
drwxr-xr-x   5 killer killer 4.0K Mar 23 10:26 bin.v2
-rwxr-xr-x   1 killer killer 302K Mar 29 14:40 bjam
drwxr-xr-x 122 killer killer  12K Dec  5  2018 boost
-rw-r--r--   1 killer killer  850 Dec  5  2018 boost-build.jam
-rw-r--r--   1 killer killer  989 Dec  5  2018 boost.css
-rw-r--r--   1 killer killer 6.2K Dec  5  2018 boost.png
-rw-r--r--   1 killer killer  22K Dec  5  2018 boostcpp.jam
-rw-r--r--   1 killer killer 2.7K Dec  5  2018 bootstrap.bat
-rw-r--r--   1 killer killer 2.5K Mar 29 14:39 bootstrap.log
-rwxr-xr-x   1 killer killer  11K Dec  5  2018 bootstrap.sh
drwxr-xr-x   7 killer killer 4.0K Dec  5  2018 doc
-rw-r--r--   1 killer killer  769 Dec  5  2018 index.htm
-rw-r--r--   1 killer killer 5.6K Dec  5  2018 index.html
drwxr-xr-x 133 killer killer 4.0K Dec  5  2018 libs
drwxr-xr-x   4 killer killer 4.0K Dec  5  2018 more
-rw-r--r--   1 killer killer  825 Mar 29 14:40 project-config.jam
-rw-r--r--   1 killer killer  825 Mar 23 10:24 project-config.jam.1
-rw-r--r--   1 killer killer 2.6K Dec  5  2018 rst.css
drwxr-xr-x   2 killer killer 4.0K Mar 29 14:49 stage
drwxr-xr-x   2 killer killer 4.0K Dec  5  2018 status
drwxr-xr-x  11 killer killer 4.0K Dec  5  2018 tools
```

</details>

## Задание 11
*Найдите топ 10 самых тяжелых*

Введем команду
```sh
ls -lhS | head -11
```
Флаг `-S` означает сортировку по размеру файла, `head -11` означает показ только первых 11 строк вывода. Используем 11, так как первая строчка будет `total 53M`, а следующие 10 уже наши файлы.

```
total 760K
-rwxr-xr-x   1 killer killer 302K Mar 29 14:40 b2
-rwxr-xr-x   1 killer killer 302K Mar 29 14:40 bjam
-rw-r--r--   1 killer killer  22K Dec  5  2018 boostcpp.jam
-rw-r--r--   1 killer killer  13K Dec  5  2018 Jamroot
drwxr-xr-x 122 killer killer  12K Dec  5  2018 boost
-rwxr-xr-x   1 killer killer  11K Dec  5  2018 bootstrap.sh
-rw-r--r--   1 killer killer 6.2K Dec  5  2018 boost.png
-rw-r--r--   1 killer killer 5.6K Dec  5  2018 index.html
drwxr-xr-x   5 killer killer 4.0K Mar 23 10:26 bin.v2
drwxr-xr-x   7 killer killer 4.0K Dec  5  2018 doc
```
