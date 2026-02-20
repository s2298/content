---
# -------------------------------------------------------------------------------------------------------------------- #
# GENERAL
# -------------------------------------------------------------------------------------------------------------------- #

title: 'Настройка'
description: ''
icon: 'far fa-file-lines'
categories:
  - 'config'
tags:
  - 'pmgconfig'
authors:
  - 'KaiKimera'
sources:
  - ''
license: 'CC-BY-SA-4.0'
complexity: '0'
toc: 1
comments: 1

# -------------------------------------------------------------------------------------------------------------------- #
# DATE
# -------------------------------------------------------------------------------------------------------------------- #

date: '2026-02-18T22:09:29+03:00'
publishDate: '2026-02-18T22:09:29+03:00'
lastMod: '2026-02-18T22:09:29+03:00'

# -------------------------------------------------------------------------------------------------------------------- #
# META
# -------------------------------------------------------------------------------------------------------------------- #

type: 'articles'
hash: 'e09c5b2d1c717d53c280377a8bdb2c45162b96da'
uuid: 'e09c5b2d-1c71-5d53-a280-377a8bdb2c45'
slug: 'e09c5b2d-1c71-5d53-a280-377a8bdb2c45'

draft: 1
---

Для быстрой шаблонной настройки я создал заранее подготовленный файл `pmg.conf`.

<!--more-->

{{< file "pmg.conf" >}}

Необходимо его скачать в директорию `/etc/pmg` и перезапустить сервисы PMG:

```bash
m='mail@example.com'; f=('pmg.conf'); d='/etc/pmg'; s='https://libpmg.ru/ru/2026/02/4e6fb1f5-fcbe-5141-9e29-eb9e59a33779'; for i in "${f[@]}"; do [[ -f "${d}/${i}" && ! -f "${d}/${i}.orig" ]] && cp "${d}/${i}" "${d}/${i}.orig"; curl -fsSLo "${d}/${i}" "${s}/${i}" && sed -i "s|postmaster@example.org|${m}|g" "${d}/${i}"; done; pmgconfig sync --restart 1
```

## Корректировка

- Заменить `postmaster@example.org` на email администратора сервера:

```bash
sed -i 's|postmaster@example.org|mail@example.com|g' '/etc/pmg/pmg.conf'
```

- Заменить `ExampleCorp` на название своей организации.

```bash
sed -i 's|ExampleCorp|MailCorp|g' '/etc/pmg/pmg.conf'
```

- Заменить `192.168.1.2` на IP-адрес сервера MS Exchange.

```bash
sed -i 's|192.168.1.2|192.168.22.33|g' '/etc/pmg/pmg.conf'
```

- Добавить репозиторий `non-free`:

```bash
sed -i 's|contrib|contrib non-free|g' '/etc/apt/sources.list.d/debian.sources' && apt update
```
