# flbridge-modules

**English** · [Русский](#русский)

Module catalogue for **FL Bridge** — a VST3 host that runs FL Studio's native plugins inside any DAW.

## What this is

This repository holds a single file, `manifest.json`: the list of modules with sizes and checksums.
The archives themselves are not in git — they are attached to the
[`modules-1`](../../releases/tag/modules-1) release as assets. This is deliberate: 343 MB in git
history would stay there forever.

FL Bridge reads the manifest from
`https://raw.githubusercontent.com/broscauk/flbridge-modules/main/manifest.json`
and uses it to show the list of modules you can install from the **MODULES** panel of the plugin,
one at a time or with **install all missing**. The product page shows the same list.

| | |
|---|---|
| Modules | 140 — 89 effects, 51 generators |
| Source | FL Studio 2025 |
| Compressed | 343 MB |
| On disk | 858 MB |
| Integrity | sha256 per archive, verified by the plugin before unpacking |

## Manifest format

```json
{
  "version": 1,
  "base": "https://github.com/broscauk/flbridge-modules/releases/download/modules-1/",
  "plugins": [
    {
      "id": "effect-control-surface",
      "kind": "effect",
      "name": "Control Surface",
      "file": "effect-control-surface.zip",
      "size": 2007095,
      "unpacked": 5748484,
      "files": 118,
      "sha256": "e2e224d4..."
    }
  ]
}
```

| Field | Meaning |
|---|---|
| `id` | Install key. Includes the kind, because `Fruity Wrapper` exists both as an effect and as an instrument — two different modules with the same folder name |
| `kind` | `effect` or `generator` — which folder to unpack into |
| `name` | Module folder name; also the folder name inside the archive |
| `file` | Asset name; full URL is `base` + `file` |
| `size` | Archive size in bytes |
| `unpacked` | Size on disk after unpacking |
| `files` | Number of files in the archive; some modules ship their own data next to the DLL |
| `sha256` | Archive checksum |

Each archive contains the whole module folder (`<Name>/<files...>`), so unpacking needs no rules.

## Where modules go

The plugin unpacks modules into its own folder and looks for them there, right after an installed
FL Studio:

```
<Program Files>\FL Bridge\FL Studio Modules\Plugins\Fruity\Effects\
<Program Files>\FL Bridge\FL Studio Modules\Plugins\Fruity\Generators\
```

If FL Studio is installed on the machine, you do not need any of this: the plugin takes the modules
from the FL Studio installation, together with its content (impulses for Fruity Convolver, samples for
the sampler generators), which the archives here do not include.

## Downloading without the plugin

If the plugin cannot reach the network (proxy, antivirus), download `manifest.json` and the `.zip`
files you need from the release page into one folder and run `FL Bridge Modules.cmd -From "<folder>"`
from the FL Bridge program folder. It verifies sha256 and puts the modules where the plugin looks for
them.

## License

**The modules are Image-Line's files**, not ours. They are here so that FL Bridge can deliver them
to a machine without FL Studio. No license is granted or checked: the rights stay with Image-Line,
and the modules run under your FL Studio license — or in demo mode without one, exactly as they
would in an unregistered FL Studio.

FL Bridge is an independent product and is not affiliated with Image-Line. Should Image-Line ask for
the distribution to be taken down, it will be.

VST is a trademark of Steinberg Media Technologies GmbH.

---

# Русский

[English](#flbridge-modules) · **Русский**

Каталог модулей для **FL Bridge** — VST3-хоста, который запускает нативные плагины FL Studio в
любой DAW.

## Что это

В репозитории один файл — `manifest.json`: список модулей с размерами и контрольными суммами.
Сами архивы не в git — они приложены к релизу [`modules-1`](../../releases/tag/modules-1) как
ассеты. Так сделано намеренно: 343 МБ в истории git остались бы там навсегда.

FL Bridge читает манифест по адресу
`https://raw.githubusercontent.com/broscauk/flbridge-modules/main/manifest.json`
и по нему показывает список модулей в панели **MODULES** плагина — ставить можно по одному или
кнопкой **install all missing**. Тот же список показывает страница продукта.

| | |
|---|---|
| Модулей | 140 — 89 эффектов, 51 генератор |
| Источник | FL Studio 2025 |
| Сжато | 343 МБ |
| На диске | 858 МБ |
| Целостность | sha256 на каждый архив, плагин сверяет до распаковки |

## Формат манифеста

```json
{
  "version": 1,
  "base": "https://github.com/broscauk/flbridge-modules/releases/download/modules-1/",
  "plugins": [
    {
      "id": "effect-control-surface",
      "kind": "effect",
      "name": "Control Surface",
      "file": "effect-control-surface.zip",
      "size": 2007095,
      "unpacked": 5748484,
      "files": 118,
      "sha256": "e2e224d4..."
    }
  ]
}
```

| Поле | Что значит |
|---|---|
| `id` | Ключ установки. Включает вид, потому что `Fruity Wrapper` существует и как эффект, и как инструмент — это два разных модуля с одинаковым именем папки |
| `kind` | `effect` или `generator` — в какую папку распаковывать |
| `name` | Имя папки модуля; оно же имя внутри архива |
| `file` | Имя ассета; полный адрес — `base` + `file` |
| `size` | Размер архива в байтах |
| `unpacked` | Сколько займёт на диске распакованным |
| `files` | Сколько файлов в архиве; у части модулей рядом с DLL лежат свои данные |
| `sha256` | Контрольная сумма архива |

Внутри каждого архива — папка модуля целиком (`<Имя>/<файлы...>`), чтобы распаковка не требовала
никаких правил.

## Куда ложатся модули

Плагин распаковывает модули в свою папку и ищет их там же — сразу после установленной FL Studio:

```
<Program Files>\FL Bridge\FL Studio Modules\Plugins\Fruity\Effects\
<Program Files>\FL Bridge\FL Studio Modules\Plugins\Fruity\Generators\
```

Если FL Studio на машине установлена, ничего из этого не нужно: плагин берёт модули из установки
FL Studio вместе с контентом (импульсы для Fruity Convolver, сэмплы для сэмплерных генераторов),
которого в здешних архивах нет.

## Загрузка без плагина

Если плагин не достаёт сеть (прокси, антивирус) — скачайте `manifest.json` и нужные `.zip` со
страницы релиза в одну папку и запустите `FL Bridge Modules.cmd -From "<папка>"` из папки программ
FL Bridge. Он сверит sha256 и положит модули туда, где их ищет плагин.

## Лицензия

**Модули — файлы Image-Line**, а не наши. Они здесь для того, чтобы FL Bridge мог доставить их на
машину без FL Studio. Лицензия на них не выдаётся и не проверяется:
права остаются у Image-Line, модули работают по лицензии вашей FL Studio, а без неё — в демо-режиме,
так же, как в незарегистрированной FL Studio.

FL Bridge — независимый продукт и с Image-Line не аффилирован. Если Image-Line попросит убрать
раздачу — она будет убрана.

VST is a trademark of Steinberg Media Technologies GmbH.
