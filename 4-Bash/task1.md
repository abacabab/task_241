# Скриптуем по полной

1. Что такое шебанг?

шебанг - это первые два символа скрипта, указывающие системе, какой интерпретатор использовать (например, #!/bin/bash).

2. Обязательно ли исполняемый файл дожен иметь соотвествующее расширение?

Нет, главное, чтобы вначале скрипта был указан интерпретатор, расширение вообще не важно. Например, можно создать файл .py, но при этом указать на /bin/bash в первой строке и он выполнится как скрипт bash

3. Напишите скрипт который выполнит автоматически действия из блока работы с файлами. ( не забудьте включить set -euo pipefail для того что бы ваш скрипт было удобнее отлаживать. Опишите что включают эти флаги)

```bash
#!/bin/bash
set -euo pipefail

mkdir ff
cd ff

touch tttt.txt
ls
ls --all

mkdir fl
mkdir fl/fll
mkdir fl/f12

touch fl/file.txt
echo "this was not a first attempt unfortunately" >> fl/file.txt

mv fl/file.txt fl/fll/

cp fl/fll/file.txt fl/f12/file_copy.txt

mv fl/f12/file_copy.txt fl/f12/file_copy_renamed.txt

diff fl/fll/file.txt fl/f12/file_copy_renamed.txt
echo "new line" >> fl/f12/file_copy_renamed.txt
diff fl/fll/file.txt fl/f12/file_copy_renamed.txt

sort fl/f12/file_copy_renamed.txt
sort -r fl/f12/file_copy_renamed.txt

cd ..
rm -rf ff
ls
```

-e — завершать скрипт при любой ошибке
-u — считать ошибкой использование неопределённых переменных
-o pipefail — если какая-либо команда в последовательности команд, соединенных "|" завершится с ошибкой, то статус выхода скрипта её отражает. Без этой опции статус выхода скрипта определяется последней командой в конвейере, даже если предыдущие команды завершились с ошибкой. Это может как бы замаскировать ошибки