## Установить git

1. [Для Windows](https://git-scm.com/download/win) скачать и запустить Standalone Installer
2. [Для Linux](https://git-scm.com/download/linux)
3. Для MacOS
	1. На официальном сайте [Homebrew](https://brew.sh/) скопировать команду и выполнить в консоли
	2. Выполнить в консоли команду `brew install git`

Чтобы удостовериться, что git установлен в систему, должна вылететь инфа о версии программы. Если не вылетело, значит git не установлен.
```bash
$ git --version
```

## Прописать пользователя в git

Чтобы коммиты были от чьего-то имени, надо заполнить некоторые настройки. В консоли выполнить:
```bash
$ git config --global user.name "User Namovich" 
# имя или ник нужно написать латиницей и в кавычках

$ git config --global user.email username@yandex.ru
# здесь нужно указать свой настоящий email
```

Все глобальные настройки Git хранит в файле `.gitconfig` в домашней директории. Команда запишет в этот файл указанные имя и почту. Чтобы убедиться в этом, можно вызвать команду для чтения файлов.
```bash
$ cat ~/.gitconfig
```

Другой способ проверки — вывести содержимое файла конфигурации Git той же командой `git config` с флагом `--list` (англ. «список»).
```bash
$ git config --list
```

## Минимальная работа в консоли
### Навигация: **`cd, pwd, ls`**

```bash
$ cd ~ # перейти в домашнюю директорию
$ pwd  # запомни, это домашняя директория
```

Например, есть такое дерево директорий (папок):
```
/home
	/username
		/projects
		    /github
		        /open source project
		    /practicum
		        /my-project
		/desktop
		/documents
			doc.txt
			/photos
```

```bash
$ pwd # вывести директорию, в которой сейчас находишься
$ /home # вывелось, что мы в home
```

```bash
$ cd username/projects/practicum # перешли в practicum
```

```bash
$ cd ..     # переметситься в родительскую директорию (на директорию выше текущей)
            # в нашем примере из practicum попадем в projects
$ cd ../..  # переместиться уже из projects на две директории выше, то есть в home
$ cd u[Tab] # сработает автодополнение до возможного варианта, если вариант один
            # иначе надо нажать еще раз [Tab] -- выведутся все варианты перехода,
            # начинающиеся с 'u'
```

```bash
$ pwd
$ /home/username/
$ cd [Tab][Tab] # показать варианты директорий,
                # куда можно переместиться из текущей директории
                # выведется projects, desktop и documents, в них и можно перейти 
```

```bash
$ cd projects/practicum # перешли в practicum
$ cd my-project         # перешли в my-project
```

Чтобы перейти в `username`, надо либо указать абсолютный путь (это путь от корня, корень это '/'), либо переходить двумя точками и слешами
```bash
$ cd /home/username # вариант 1, кстати все 'cd путь' -- путь назывался относительным
$ cd ../../..       # вариант 2
```

> [!tip]
> Символами `cd /` и `cd ~` можно быстро перемещаться к корневой и домашней директориям.

```bash
$ ls     # вывести список файлов и директорий в текущей директории
$ ls -la # вывести список в том числе скрытых файлов и директорий в текущей
         # директории
```

```bash
$ clear # очистить окно консоли
```

### Создание, копирование, перемещение файлов и папок: **`touch, mkdir, cp, mv`**

```bash
$ touch my-new-file.txt # создали файл my-new-file.txt в текущей директории
```

```bash
$ mkdir new-dir # создали директорию new-dir
```

Можно создать целую структуру директорий одной командой с помощью флага `-p`.
```bash
$ mkdir -p dir1/dir-inside/dir-deeper-inside
# создали папку dir-deeper-inside в папке dir-inside, которая находится в папке dir1
```

```bash
# комадны можно объединять через &&
$ mkdir first-project && cd first-project # создать директорию first-project и
                                          # перейти в нее
```

```bash
$ mkdir ~/my-git-projects # создаст папку `my-git-projects` внутри домашней директории
```

```bash
$ touch ../../file.txt # создаст файл file.txt на две папки выше по иерархии
```

```bash
$ cp что_копируем куда_копируем

$ cp index.html src/
# скопировали index.html в папку src
```

```bash
$ cp что_копируем что_копируем что_копируем куда_копируем

$ cp index.html style.css script.js src/
# скопировали три файла (index.html, style.css и script.js) в папку src
```

> [!faq]
> [Подробнее про `cp`](https://losst.pro/komanda-cp-v-linux)

```bash
$ mv ../file.txt me.png important-files
# Переместить файлы `file.txt` из родительской директории и `me.png`
# из текущей директории в папку `important-files` в рабочей директории
```

### Удаление файлов и директорий: **`rm, rm -r, rmdir`**

```bash
$ rm example.txt # удалили файл example.txt из текущей папки
```

```bash
$ rmdir images # команда удалит папку images из текущей директории, 
               # если папка images пуста
```

```bash
$ rm -r images # удалили папку images со всем её содержимым из текущей директории
```

> [!ATTENTION]
> 💡 Будьте осторожны: удаление объектов командами `rm` и `rmdir` необратимо — в этом случае файлы и папки не попадают в корзину и исчезают навсегда.

> [!tip]
> Примечание: для удаления файла используют `rm`, для удаления пустой директории — `rmdir`, а для директории с файлами — `rm -r`.

### Чтение и редактирование файлов: **`cat, nano`**

```bash
$ cat myfile.txt # распечатали содержимое файла myfile.txt
```

```bash
$ nano myfile.txt # открыли в редакторе nano содержимое файла myfile.txt
                  # внизу будут символы, позволяющие многое сделать с файлом,
                  # главное понимать, что ^X это Ctrl + X :)
```

> [!tip]
> Стрелками вверх и вниз можно вызывать ранее набранные команды.

## Работа с локальным репозиторием

> [!attention]
> Все команды, начинающиеся с `git...` надо выполнять в локальном репозитории. То есть надо сначала перейти в директорию с репозиторием, и только потом давать команды git.
### Создание, удаление и проверка локального репозитория: **`init, status`**

```bash
$ git init # сделать директорию локальным git-репозиторием, который потом можно
           # синхронизировать с удаленным репозиторием на github
$ ls -la
total 8
drwxr-xr-x 1 username 197121 0 авг 27 time ./
drwxr-xr-x 1 username 197121 0 авг 27 time ../
drwxr-xr-x 1 username 197121 0 авг 27 time .git/ # В подпапке `.git` Git будет
										         # хранить всю служебную информацию
```

> [!faq]
> Директория, в которой лежит `.git` называется локальным репозиторием.

> [!ATTENTION]
> Помните, что не рекомендуется создавать репозиторий Git внутри другого Git-репозитория. Это может вызывать проблемы с отслеживанием изменений.

#IDEA (идея: написать программу, которая проверяет, что текущая директория не является дочерней директорией другого репозитория)

В некоторых случаях при инициализации репозитория Git может показать объёмное сообщение, которое начинается со слов `Using 'master' as the name…`. Это не ошибка, подробнее тут -- [Black Lives Matter](https://blacklivesmatter.com/).

```bash
$ cd <папка с репозиторием> # перешли в папку

$ rm -rf .git # удалили подпапку .git чтобы "разгитить" ее
```

> [!ATTENTION]
> Будьте осторожны: в подпапке `.git` хранится история изменений. Если удалить `.git`, то вся история проекта будет стёрта без возможности восстановления — останется только последняя версия файлов.

```bash
$ git status # показывает текущее состояние репозитория
             # (что нового, старого, измененного в нем есть)
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Команда `git status` выведет:
- название текущей ветки: `On branch master` или `On branch main`;
- сообщение о том, что в репозитории ещё нет коммитов: `No commits yet`;
- сообщение, которое говорит: «чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать» — `nothing to commit (create/copy files and use "git add" to track)`.

> [!faq]
> **Коммит** — фиксация состояния файлов в Git.

> [!faq]
> Команда `git status` выводит текущее состояние проекта: есть ли незакоммиченные (изменённые) файлы и название текущей ветки.

> [!tip]
> В отличие от `git init`, команду `git status` используют часто. В любой непонятной ситуации стоит посмотреть состояние (статус) репозитория, а потом решить, что делать дальше.

### Подготовить файлы к сохранению: `git add`

Когда в локальном репозитории появились файлы, их надо начать отслеживать. Помогает в этом команда `git add` тремя способами.

```bash
$ git add --all # добавили
$ git status    # проверили, что добавилось
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   <какой-то файл 1> # зеленый шрифт
        new file:   <какой-то файл 2> # зеленый шрифт
        <...>
```

```bash
$ git add <какой-то файл 1>
$ git add <какой-то файл 2>
```

Также можно добавить текущую папку целиком — в этом случае все файлы в ней тоже будут добавлены. Обратиться к текущей папке в Bash позволяет точка (`.`).
```bash
$ git add . # добавить всю текущую папку
$ git status
```

Если сейчас отредактировать любой из «зелёных» файлов в папке `first-project`, он перейдёт в состояние `modified` (англ. «изменённый») и будет и в «зелёном», и в «красном» списках.
Отредактируем и снова вызовем `git status` в консоли:
```bash
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   <какой-то файл 1>
        new file:   <какой-то файл 2>

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   <какой-то измененный файл 1>
```

### Выполнить коммит: `git commit`

Ключ `-m` позволяем задать сообщение для коммита, в котором будут пояснения к этому самому коммиту.
```bash
$ git commit -m ‘Мой первый коммит!’
```

> [!faq]
> 💡 **Чем отличается запоминание от сохранения?**
> 
> Команда `git add` не сохраняет содержимое файлов в репозитории. Само сохранение, или фиксацию состояния файлов, называют **коммитом** (от англ. _commit_ — «совершать», «фиксировать»). «Сделать коммит» значит сохранить текущую версию файла.
> 
> Если провести аналогию, команду `git add` можно сравнить с расстановкой людей в кадр, а коммит — сама сделанная фотография.

Команда `git commit` выведет информацию о коммите.
- `[master (root-commit) baa3b6e]` значит:
    - коммит был в ветке `master`;
    - `root-commit` — это самый первый, или «корневой» (англ. _root_), коммит в ветке, у следующих коммитов такой надписи не будет;
    - `baa3b6e` — сокращённый идентификатор коммита (подробнее об этом мы ещё расскажем).
- `2 files changed, 1 insertion(+)` значит:
    - изменились два файла (`readme.txt` и `todo.txt`);
    - одна строка была добавлена (`1. Пройти пару уроков по Git.`).
- Строки вида `create mode 100644 readme.txt` — это более подробная информация о новых (добавленных в Git) файлах.
    - `create` (англ. «создать») говорит, что файл был создан. Если бы файл был удалён, на этом месте было бы слово `delete` (англ. «удалить»).
    - `mode 100644` сообщает, что это обычный файл. Также возможны варианты `100755` для исполняемых файлов (например, `что-нибудь.exe`) и `120000` для файлов-ссылок в Linux. Файлы-ссылки не содержат данных сами по себе, а только ссылаются на другие файлы — как «ярлыки» в Windows.

> [!note]
> 💡 Обратите внимание: после того как вы сделали первый коммит, команда `git status` перестала выводить сообщение `No commits yet` (англ. «ещё нет коммитов»).

### Просмотреть историю коммитов: `git log`
```bash
$ git log
commit 0cc2241f3b2314760ffab951cbe10efefed154ee (HEAD -> master)
Author: user_name user_email # инфа из git config
Date:   <дата в определенном формате>

    Мой первый коммит! # сообщение к коммиту
```

## Работа с удаленным репозиторием

> [!faq]
> Удаленный репозиторий это не тот, который удалили. Это тот, который на GitHub.

### Создать репозиторий
Надо иметь аккаунт на github, чтобы работать дальше. После регистрации заходим с главного экрана Repositories -> New -> задаем имя репозиторию и делаем его приватным или публичным -> Create repository.

### SSH или как убедить github, что вы это вы, и убедиться, что github это github

> [!faq]
> Чтобы получить доступ к репозиторию на GitHub, вам тоже нужно предоставить ключ, который подтверждает вашу личность и права на чтение или изменение данных.

Когда компьютеры обмениваются данными в сети, они следуют **сетевым протоколам** (англ. _network protocols_) — правилам обмена данными между компьютерами. Один из наиболее распространённых сетевых протоколов — **SSH** (от англ. _**S**ecure **Sh**ell Protocol_). Он обеспечивает безопасный обмен данными в сети.

SSH использует пару ключей для обеспечения безопасности — публичный и приватный:
- **Приватный ключ** (англ. _private key_) хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для расшифровки данных.
- **Публичный ключ** (англ. _public key_) доступен всем и используется для шифрования данных. Они могут быть расшифрованы парным приватным ключом.

Только вы можете расшифровать данные с помощью приватного ключа, но любой владелец публичного ключа может их для вас зашифровать. Эти два ключа связаны и образуют **SSH-пару**.

### Инструкция по генерации SSH-ключа

Прежде чем генерировать SSH-ключи, убедитесь, что у вас их ещё нет. По умолчанию директория с SSH-ключами находится в домашней директории пользователя. Обычно SSH-ключи находятся в директории `.ssh/`. Проверить наличие этой директории и файлов в ней можно с помощью следующей команды.
```bash
$ cd ~
$ ls -la .ssh/
total 36
drwxr-xr-x 1 grine 197121    0 апр 11 14:03 ./
drwxr-xr-x 1 grine 197121    0 авг 28 17:03 ../
-rw-r--r-- 1 grine 197121 3434 июл  7  2022 id_rsa
-rw-r--r-- 1 grine 197121  747 июл  7  2022 id_rsa.pub
-rw-r--r-- 1 grine 197121  828 апр 11 14:03 known_hosts
-rw-r--r-- 1 grine 197121  656 авг  8  2022 known_hosts.old
```

Если папка пустая или её нет, всё в порядке. Иначе можно удалить ее, если ключи в ней не нужны. Если не удаляли, то при генерации надо будет прописать путь до нее.

Итак:
1. Для генерации SSH-пары можно использовать программу `ssh-keygen`. Откройте терминал и введите следующую команду.
```bash
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
```
Используйте электронную почту, к которой привязан ваш GitHub-аккаунт.

Если вы видите сообщение об ошибке, то, скорее всего, ваша система не поддерживает алгоритм шифрования `ed25519`. Ничего страшного: используйте другой алгоритм.
```bash
$ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
```

После ввода отобразится такое сообщение.
```bash
> Generating public/private rsa key pair. # сгенерированы публичный и приватный ключи
> Enter file in which to save the key (/c/Users/grine/.ssh/id_ed25519):
```

2. Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите `Enter`.

> [!NOTE]
> Вот тут если я ввожу какой-то набор символов, например, `my_new_key`, то в домашней директории появляются `my_new_key` и `my_new_key.pub`, а если нажимаю `Enter`, как говорит практикум, то в домашней директории появляется директория `.ssh/`, в которой будут ключи (видимо, с именами по умолчанию) `id_ed25519` и `id_ed25519.pub`

3. Программа запросит **кодовую фразу** (англ. _passphrase_) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите `Enter`, а затем ещё раз `Enter` для подтверждения.
```bash
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

> [!NOTE]
> 💡 **Быть или не быть кодовой фразе — вот в чём вопрос**
> 
> Как бы странно ни звучало, кодовая фраза — это «пароль от ключа». Представьте, что SSH-ключ лежит в шкатулке. А на самой шкатулке — кодовый замок, который открывается кодовой фразой.
> 
> Многие пользователи Git не используют кодовую фразу для защиты своего SSH-ключа. Если такой фразы нет, то её не нужно вводить всякий раз при взаимодействии с удалённым репозиторием.
> 
> С другой стороны, применение кодовой фразы усиливает безопасность ключей. Если вы используете эту фразу, ключ будет надёжно защищён в случае несанкционированного доступа к вашему компьютеру.

4. Готово! Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду.
```bash
ls -a ~/.ssh
```

```bash
$ ls -la .ssh/
total 18
drwxr-xr-x 1 grine 197121   0 авг 29 12:04 ./
drwxr-xr-x 1 grine 197121   0 авг 29 12:03 ../
-rw-r--r-- 1 grine 197121 411 авг 29 12:04 id_ed25519
-rw-r--r-- 1 grine 197121 103 авг 29 12:04 id_ed25519.pub
```

> [!ATTENTION]
> На экране должны появиться два файла — один с расширением `.pub`, другой — без. Файл в `.pub` — публичный, им можно делиться с веб-сайтами или коллегами. Файл без расширения `.pub` — приватный. Ни в коем случае не передавайте его никому!

### Привязка ssh-ключа к github

1. После выполнения команды `ssh-keygen` из предыдущего урока в директории `~/.ssh` будет создано два файла — `id_ed25519` и `id_ed25519.pub` (или `id_rsa` и `id_rsa.pub` — в зависимости от того, какой алгоритм вы использовали):
    - `id_ed25519`/`id_rsa` — приватный ключ (файл без `.pub` в конце). Ни в коем случае не копируйте его и не делитесь им.
    - `id_ed25519.pub`/`id_rsa.pub` — публичный ключ (на это указывает расширение `.pub`).
        
        Скопируйте содержимое файла с публичным ключом в буфер обмена.

**macOS**
```bash
# скопировать содержимое ключа в буфер обмена:
$ pbcopy < ~/.ssh/id_rsa.pub
# для ed25519:
$ pbcopy < ~/.ssh/id_ed25519.pub
```

Здесь используется команда `pbcopy` — она копирует поток данных в буфер обмена. Запись `pbcopy < ~/.ssh/id_rsa.pub` означает: «Скопируй в буфер обмена всё содержимое файла `~/.ssh/id_rsa.pub`».

**Windows**
```bash
# скопировать содержимое ключа в буфер обмена:
$ clip < ~/.ssh/id_rsa.pub
# для ed25519:
$ clip < ~/.ssh/id_ed25519.pub 
```

В качестве альтернативы вы можете распечатать файл на экран с помощью `cat ~/.ssh/id_rsa.pub` и скопировать его вручную.

2. Перейдите на GitHub и выберите пункт **Settings** (англ. «настройки») в меню аккаунта (справа, сверху).
3. В меню слева нажмите на пункт **SSH and GPG keys**.
4. В открывшейся вкладке выберите **New SSH key** (англ. «новый SSH-ключ»).
5. В поле **Title** (англ. «заголовок») напишите название ключа. Например, **Personal key** (англ. «личный ключ»).
6. В поле **Key type** (англ. «тип ключа») должно быть **Authentication Key** (англ. «ключ аутентификации»).
7. В поле **Key** скопируйте ваш ключ из буфера обмена.
8. Нажмите на кнопку **Add SSH key** (англ. «добавить SSH-ключ»).
9. Проверьте правильность ключа с помощью следующей команды.
```bash
$ ssh -T git@github.com
```

Если это первый раз, когда вы используете Git, чтобы поделиться проектом на GitHub, появится похожее предупреждение.
```bash
The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Это предупреждение сообщает, что вы никогда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что сервер является тем, за кого он себя выдаёт.

#NEW_FOR_ME 
Для подтверждения подлинности сервер генерирует и публикует ключи SHA256. Вы можете проверить ключи GitHub [по этой ссылке](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints). Если ключ в предупреждении совпадает с тем, что вы видите на сайте, значит, сервер является действительным. Введите `yes`, чтобы продолжить. Вы увидите приветствие на экране.
```bash
Hi %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access.
```

### Связываем локальный и удаленный репозитории

1. Перейдите на страницу удалённого репозитория, выберите тип `SSH` и скопируйте URL. Кнопка справа позволит сделать это мгновенно.
2. Откройте консоль, перейдите в каталог локального репозитория и введите команду `git remote add` (от англ. _remote_ — «удалённый» и _add_ — «добавить»).
```bash
$ cd <путь до локального репозитория>
$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/%НАЗВАНИЕ_РЕПОЗИТОРИЯ%.git
```

Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово `origin`. А URL вы скопировали со страницы удалённого репозитория.

> [!faq]
> `origin` (англ. «источник») — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один). Это значительно упрощает работу.

3. Убеждаемся, что репозитории связаны
```
$ git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push) 
```
В выводе вы должны увидеть две строчки, аналогичные тем, что показаны выше.

Флаг `-v` — короткая форма флага `--verbose` (англ. «подробный»). Он позволяет показать больше информации в выводе.

> [!faq]
> Команда `git remote add` принимает имя удалённого репозитория (или псевдоним `origin`) и его адрес.

### Синхронизируем локальный и удаленный репозитории
Локальный и удалённый репозитории связаны! Теперь надо их синхронизировать.

> [!faq]
> Каждый коммит сохраняет актуальное состояние файлов. Сами же коммиты хранятся в **ветках** (англ. _branch_).

Если коммит — это снимок состояния файлов, то ветка — временна́я шкала, на которой расположены эти снимки. Ветка всегда начинается от одного из коммитов.

Самая первая ветка в репозитории появляется автоматически и называется `main` (англ. «основная») или `master`. Её имя нужно указывать при отправке коммитов на удалённый репозиторий или при получении их из него.

Мы уже прошли весь «цикл коммита»: подготовили файлы с помощью `git add`, закоммитили их с комментарием командой `git commit -m`. Осталось загрузить содержимое локального репозитория на GitHub. За это отвечает команда `git push` (от англ. _push_ — «толкать»).

В первый раз эту команду нужно вызвать с флагом `-u` и параметрами `origin` (имя удалённого репозитория) и `main` или `master` (название текущей ветки). Флаг `-u` свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории в предыдущем уроке, так же и здесь нужно дополнительно связать ветки.
```bash
$ git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master.
```

> [!ATTENTION]
> Без коммитов в репозитории эта команда не выполнится

> [!faq]
> 💡 Команда git push имеет несколько флагов, которые можно использовать для дополнительной настройки:
> 
> **-u** или **--set-upstream** - устанавливает отслеживание для ветки, что позволяет вам использовать git push и git pull без указания имени удаленного репозитория и названия ветки;  
> **-f** или **--force** - заставляет Git принудительно заменить удаленную ветку измененной локальной веткой, даже если это приведет к потере данных;  
> **-n** или **--dry-run** - позволяет вам протестировать команду git push, не отправляя реальных изменений в удаленный репозиторий;  
> **-v** или **--verbose** - выводит дополнительную информацию о процессе отправки изменений.
> 
> Пример использования команды `git push` с флагом:
> 
> `git push -u origin main`
> _Эта команда отправляет изменения из вашей локальной ветки main в удаленный репозиторий с именем origin и устанавливает отслеживание для этой ветки._

При взаимодействии с удалёнными репозиториями Git выводит в консоль отладочную информацию: количество объектов (файлов), которые отправляются на сервер, информацию о прогрессе сжатия и записи и так далее.
```bash
$ git push -u origin master
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 12 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (10/10), 956 bytes | 95.00 KiB/s, done.
Total 10 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:%ИМЯ_ПОЛЬЗОВАТЕЛЯ%/%ИМЯ_РЕПОЗИТОРИЯ%.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
```

Если вы указывали кодовую фразу при настройке SSH-ключей, её нужно будет ввести.

Теперь можно зайти в репозиторий на github и убедиться, что в нем появились все коммиты и последний содержит актуальное состояние локального репозитория.

> [!attention]
> В дальнейшем при работе с удалённым репозиторием флаг `-u` можно опустить и писать просто `git push`.

## Оформлять работу в репозитории
### Файл **`README.md`**

Чтобы другие пользователи, а также потенциальные клиенты или работодатели могли понять, что представляет собой проект, его нужно описать. Такое описание принято указывать в файле `README.md` (от англ. _read_ — «прочитай» и _me_ — «меня»).

Как правило, в `README.md` проекта можно найти следующую информацию:
1. Название проекта и его краткое описание: кем создан, для чего, какие решает задачи и какие закрывает проблемы.
2. Технологии, которые применяются в проекте. В чём его отличие от аналогичных.
3. Документация проекта — подробная инструкция о том, что представляет собой проект.
4. Планы проекта, если они есть.
Вот пример файла `README.md` для Git [на GitHub](https://github.com/git/git/blob/master/README.md).

`README.md` — текстовый файл, который можно создать командой `touch`, а затем редактировать так же, как и любой другой текстовый документ. Например, в блокноте.

Преимущество `README.md` в том, что средства командной работы (такие, как GitHub) могут отображать его содержимое в браузере в виде удобной разметки. Для этого нужно не просто залить текст, но и настроить шрифт, заголовки и отступы с помощью markdown. **Маркда́ун** — это специальный язык разметки. Он позволяет красиво отформатировать текстовый документ.

[Гайд раз](https://www.markdownguide.org/cheat-sheet/)<br>
[Гайд два](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax)

### Коммиты

Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или **родительский** (англ. _parent_), коммит.

Git [хеширует](https://emn178.github.io/online-tools/sha1.html) (преобразует) информацию о коммите и получает для каждого коммита свой уникальный хеш. Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов.

Все хеши и таблицу `хеш → информация о коммите` Git сохраняет в служебные файлы. Они находятся в скрытой папке `.git` в репозитории проекта. 

После вызова `git log` появляется список коммитов. Вот так выглядит описание самого первого коммита в репозитории Git.
```bash
commit e83c5163316f89bfbde7d9ab23ca2e25604af290                  # хеш коммита
Author: Linus Torvalds <torvalds@linux-foundation.org>           # автор коммита
Date:   Thu Apr 7 15:13:13 2005 -0700                            # дата и время коммита

    Initial revision of "git", the information manager from hell # сообщение к коммиту
```

Когда в репозитории много коммитов, удобно вызывать сокращенный лог.
```bash
$ git log --oneline
a9e32da (HEAD -> master, origin/master) Добавил README.md
2d41c56 make homework complete
0cc2241 Изменен todo.txt
3bf522a Отредактирован readme.txt
d44a27b Мой первый коммит!
```

> [!NOTE]
> Команда `git log --oneline` автоматически подбирает такую длину сокращённых хешей, чтобы они были уникальными в пределах репозитория и Git всегда мог понять, о каком коммите идёт речь.

При вызове команды `git log` вы также можно заметить надпись `(HEAD -> master)` после хеша одного из коммитов. Файл `HEAD` (англ. «голова», «головной») — один из служебных файлов папки `.git`. Он указывает на коммит, который сделан последним (то есть на самый новый).
```bash
$ cd .git/
$ cat HEAD
ref: refs/heads/master
$ cat HEAD # команда cat показывает содержимое файла
ref: refs/heads/master # в файле вот такая ссылка
$ cat refs/heads/master # взяли ссылку из файла HEAD
a9e32da54fa9665add1cfb5dbfc75ea25ff8d0d6 # внутри хеш

# сверяем с хешем последнего коммита
$ git log
commit a9e32da54fa9665add1cfb5dbfc75ea25ff8d0d6 (HEAD -> master, origin/master)
Author: gr_nikita <grinev-nikk@yandex.ru>
Date:   Wed Aug 30 15:45:54 2023 +0300

    Добавил README.md
```

> [!tip]
> При работе с Git указатель `HEAD` используется довольно часто. Мы уже упоминали, что многие команды Git принимают в качестве параметра хеш коммита. Если нужно передать последний коммит, то вместо его хеша можно просто написать слово `HEAD` — Git поймёт, что вы имели в виду последний коммит.

## Жизненный цикл файла в git

Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные.

- коммитов не было
```bash
$ git status
On branch master

No commits yet # коммитов еще не было

# нечего коммитить, рабочая директория чиста
nothing to commit (create/copy files and use "git add" to track)
```
- **`untracked`** (англ. «неотслеживаемый»)
    Новые файлы в Git-репозитории помечаются как `untracked`, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У `untracked`-файла нет предыдущих версий, зафиксированных в коммитах или через команду `git add`.
```bash
$ touch file.txt # создали новый файл в локальном репозитории
$ git status
On branch master

No commits yet # коммитов еще не было

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file.txt # красный, неотслеживаемый

nothing added to commit but untracked files present (use "git add" to track)
```
- **`staged`** (англ. «подготовленный»)
    После выполнения команды `git add` файл попадает в **staging area** (от англ. _stage_ — «сцена», «этап [процесса]» и _area_ — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии `staged`.
```bash
$ git add .  # добавим неотслеживаемый ранее файл в staging area
$ git status # снова запросим состояние репозитория
On branch master

No commits yet # коммитов еще не было

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   file.txt # зеленый, пока не закоммитили его, он будет 'new file'

```

> [!NOTE]
> 💡 **Staging area, index и cache**
> 
> Staging area также называют **index** (англ. «каталог») или **cache** (англ. «кеш»), а состояние файла `staged` иногда называют `indexed` или `cached`.
> 
> Все три варианта могут встречаться в документации и в качестве флагов команд Git. А также в интернете — например, в вопросах и ответах [на сайте Stack Overflow](https://stackoverflow.com/).

- **`tracked`** (англ. «отслеживаемый»)
    Состояние `tracked` — это противоположность `untracked`. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью `git commit`, а также файлы, которые были добавлены в staging area командой `git add`. То есть все файлы, в которых Git так или иначе отслеживает изменения.
- **`modified`** (англ. «изменённый»)
    Состояние `modified` означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия.
```bash
# не делаем коммит, меняем file.txt (содержимое "1")
$ git status
On branch master

No commits yet                 # коммитов еще не было

Changes to be committed:       # если далее сделать коммит,
                               # будет зафиксирована эта версия содержимого
  (use "git rm --cached <file>..." to unstage)
        new file:   file.txt   # прежнее содержимое (пустой файл), зеленый
                               # пока не закоммитили его, он будет 'new file'

Changes not staged for commit: # чтобы закоммитить эту версию содержимого,
                               # надо сделать git add file.txt
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file.txt   # содержимое "1", красный
                               # здесь его новое воплощение, уже без 'new', так как
                               # он modified

$ git commit -m 'Информативное сообщение к коммиту' # делаем коммит
# лог коммита

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file.txt # содержимое "1", красный
                             # больше он никогда не будет 'new', потому что
                             # был закоммичен, но будет modified, если
                             # его изменить

no changes added to commit (use "git add" and/or "git commit -a")

$ git add .

$ git commit -m "Еще один информативный коммит"
# лог коммита

$ git status
On branch master
nothing to commit, working tree clean

# изменили file.txt (содержимое "2")
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file.txt # содержимое "2", красный
                             # больше он никогда не будет 'new', потому что
                             # был закоммичен, но будет modified, если
                             # его изменить

no changes added to commit (use "git add" and/or "git commit -a")
```
