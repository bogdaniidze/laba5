# Задание 1 - Автоматизация проверки формата файлов при коммите
Создаю новый файл ``` pre-commit ``` в директории ```./git/hooks ```

![Снимок экрана 2024-12-18 214812](https://github.com/user-attachments/assets/c496e070-4f45-4738-baea-c2a4e826e5df)

Наполняю его кодом:
```bash
#!/bin/bash

txt_files=$(git diff --cached --name-only --diff-filter=ACM | grep '\.txt$')

if [[ -z "$txt_files" ]]; then
  echo "No .txt files changed in this commit."
  exit 0
fi

error=0
for file in $txt_files; do
  if [[ ! -f "$file" || -z "$(cat "$file")" ]]; then
    echo "ERROR: File '$file' is empty or does not exist."
    error=1
  fi
done

if [[ $error -eq 0 ]]; then
  echo "All .txt files are valid."
  exit 0
else
  echo "Some .txt files are invalid. Commit aborted."
  exit 1
fi
```
Далее создаю пустой .txt файл и не .txt файл и проверяю их:

![Снимок экрана 2024-12-18 215334](https://github.com/user-attachments/assets/20b521a5-1ead-430e-b2ea-02c4b8e05d5f)

Очищаю staging area, чтобы Git не выдавал ошибку старых файлов перед коммитом новых и добавляю рабочий файл:

![Снимок экрана 2024-12-18 215403](https://github.com/user-attachments/assets/7d70ec72-2e36-4b59-a011-878862f5d247)
![Снимок экрана 2024-12-18 215502](https://github.com/user-attachments/assets/2fc8d98f-fdf6-49ea-9dbc-a6aa15e248b7)

# Задание 2 - Использование Git Flow в проекте

Убедился, что git Flow установлен

![Снимок экрана 2024-12-18 215553](https://github.com/user-attachments/assets/684a52a2-c28e-4ff9-9615-130c9cdbc19f)

В корне репозитория выполнил инициализацию Git Flow.
![Снимок экрана 2024-12-18 234106](https://github.com/user-attachments/assets/2f0fedf7-0619-4a51-9513-aa95ecb04411)

Создал ветку для новой функциональности, допустим она называется "task-management":
![Снимок экрана 2024-12-18 234113](https://github.com/user-attachments/assets/38db0fa7-60a6-4cf2-93ac-4bf19242216d)

Внес изменения в код для добавления функционала управления задачами (например, в файл task_manager.py):
![Снимок экрана 2024-12-18 234402](https://github.com/user-attachments/assets/b47ffe36-2741-4b2a-a723-d2dc773a0df1)
![Снимок экрана 2024-12-18 234415](https://github.com/user-attachments/assets/3abd610d-5f5b-45dd-95d6-a863b8739141)


Выполнил коммит изменения по мере разработки:
![Снимок экрана 2024-12-18 234612](https://github.com/user-attachments/assets/32546dc2-6905-48c7-a8ad-b8570ca998ef)


После завершения разработки функции завершил фичу и объединил ее с основной веткой:
![Снимок экрана 2024-12-18 234544](https://github.com/user-attachments/assets/da99fc37-97eb-4089-85a1-b8ac903cf327)

Git Flow автоматически переключился на ветку develop и выполнил слияние. Если есть конфликты, их нужно разрешить.
Начал создание релиза:
![Снимок экрана 2024-12-18 234654](https://github.com/user-attachments/assets/1d0e66c8-e4f8-4b7f-9f73-36e49796cc9c)

Внес изменения, связанные с релизом (например, обновил версию в файле version.txt):
![Снимок экрана 2024-12-18 234751](https://github.com/user-attachments/assets/437baa29-012a-4da9-97e6-816ec3b6fb10)

Завершил релиз и объединил его с ветками "develop" и "main":
![Снимок экрана 2024-12-18 235052](https://github.com/user-attachments/assets/318e00d8-794f-4afc-bb14-582120783077)

у нас конечно же ошибки никакой не возникло, но hotfix все равно создаем):
![Снимок экрана 2024-12-18 235124](https://github.com/user-attachments/assets/632b1899-3083-4d72-ae7b-fd7f9155b406)

Внес изменения для исправления ошибки и коммитите:
![Снимок экрана 2024-12-18 235308](https://github.com/user-attachments/assets/f0176c7a-0a60-4a9c-a7bb-b44342a74b79)

Завершил hotfix и объединил его с ветками "develop" и "main":
![Снимок экрана 2024-12-18 235403](https://github.com/user-attachments/assets/cd1af90c-07e3-446a-b95e-0ec645a5d935)

Завершение работы и отправка изменений на удаленный репозиторий. Отправил изменения на удаленный репозиторий:
![Снимок экрана 2024-12-18 235439](https://github.com/user-attachments/assets/fef17dd6-5508-431a-96a5-976b7f51747a)
