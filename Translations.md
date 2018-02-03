## OUTDATED

This page has been moved to http://pegasus-frontend.org/docs/dev/translate. The wiki page is kept only for historical reasons.

---

---

### tl;dr

- download the [Qt tools](https://info.qt.io/download-qt-for-application-development)
- download the [translation repo](https://github.com/mmatyas/pegasus-frontend-translations)
- create a copy of `pegasus_en.ts` for your language
- open the new file in *Qt Linguist* and translate the UI strings
- open a new issue in the [translation repo](https://github.com/mmatyas/pegasus-frontend-translations/issues) and attach your TS file


## Translations

Pegasus supports most languages in use today, and you can easily add new translations for any locale. The translations are stored in simple text files in XML format, so the only thing you need is a text editor. There's also a graphical tool to make things easier (see below). The translations themselves are collected in a separate repository [here](https://github.com/mmatyas/pegasus-frontend-translations), which is also included as a Git submodule in the main Pegasus repo.


#### File format and name

The translation files are text files in XML format, encoded in UTF-8. Their file name includes the [*BCP47 language tag*](https://en.wikipedia.org/wiki/IETF_language_tag#Syntax_of_language_tags) of the locale the they're made for. Usually, this means the following structure:

```
pegasus_[language][-script][-country].ts
```

where

- `language` is the language code (two letters, lowercase)
- optionally,`script` defines the writing system (eg. simplified/traditional chinese) (four letters, title case)
- optionally, `country` defines a country-specific variant (two letters, uppercase)

for example, `hi-Deva-IN` means Hindi language, Devanagari script, and used in India.


### Adding translations

#### 1. Preparing the tools

You can use any decent text editor, or you can also use *Qt Linguist*, a graphical translation tool:

![linguist](https://doc.qt.io/qt-5/images/linguist-linguist.png )

It is included with Qt, which you can download from [here](https://info.qt.io/download-qt-for-application-development) (select "open source"). After installation, search for `linguist` in the installation directory of Qt.

#### 2. Prepare the translation files

You can find the translation files in [this repository](https://github.com/mmatyas/pegasus-frontend-translations). If you have no experience with Git, just click on the green *Clone or download* button, then *Download ZIP*.

Then, create a copy of `pegasus_en.ts`, and change `en` to your locale's code (see above).

*Developer note: you can create this file with `lupdate ../src -ts pegasus_en.ts`.*

#### 3. Translate the file

Open your new file in a text editor or in Qt Linguist.

If you're using a text editor, the translateable strings are inside `<message>` tags: you can see the original text in the `<source>` tag, and you can provide your translation in `<translation>`. Also change the language tag on the top of the file (`<TS ...>`).

If you're using Qt Linguist, first set your language in *Edit -> Translation file settings*. After that, you can select a "module" on the left, then see the relevant strings in the upper-middle panel. You can add the translation in the center panel (marked with "1" on the picture above). A detailed guide for Qt Linguist can be found [here](https://doc.qt.io/qt-5/linguist-translators.html).

**IMPORTANT NOTES**

- `%1`, `%2`, ... in the text is a placeholder for additional values, such as numbers, file names, etc.
- You don't have to translate *every* string; most of them won't be visible for the users, and will only be used in debug log files. It's enough to translate only the QML files (hover over the source code panel or check the `<location>` tag for the file name).

#### 4. Add your translation to the QRC file

There's a file called `translations.qrc.in` in the translations repository. It's another XML file that you can open in a text editor, and collects all the translation files. Simply add a new `<file>pegasus_LOCALECODE.qm</file>` entry.

#### 5. Rebuild Pegasus

At the moment, all translation files must be built into Pegasus. See the [build documentation](Building) about how to rebuild the program.

#### 6. Open a pull request

If you know Git, open a pull request in the [translations repository](https://github.com/mmatyas/pegasus-frontend-translations). Alternatively, open a new issue and attach your translation file.
