# What's new in babel 3.42

2020-03-22

## Getting properties from `ini` files

Let's say you need the string for the chapter name in Hebrew. You can write:
```tex
\getlocaleproperty{\hechap}{hebrew}{captions/chapter}
```
And `\hechap` is set to the corresponding value.
{% raw %}

`\LocaleForEach` loops the loaded `ini` files with `#1` as the locale name. Here is a somewhat low level example:
```tex
\LocaleForEach{%
  \getlocaleproperty\savetag{#1}{identification/tag.bcp47}%
  \expandafter\xdef\csname tagtolocale\savetag\endcsname{#1}%
}
```
{% endraw %}

[**Update**. This command raises an error if the property doesn’t exist.
`\getlocaleproperty*` doesn’t.]

## Coptic, Church Slavic, Syriac, Armenian, Sanskrit

`ini` files for 3 locales have been added:
* **Coptic**, with 2 numerals: `epact` and `lower.letters`.
* **Church Slavic**, in 3 scripts: the ‘default’ `Cyrl`, plus `Cyrs` and
  `Glag`
* **Syriac**. See an example in https://github.com/latex3/babel/blob/master/samples/lua-syriac.pdf .

Armenian now has captions and numerals. <del>[**Warning**. There are also numerals, but
their names are not correct: they are `lower` and `upper`, but must be
`lower.letters` and `upper.letters`. It will be fixed in the next
release. Sorry for the slip.]</del>[Fixed]

A few mistakes has been fixed in Sanskrit and Belarusian.

Also, a new property named `tag.bcp47.likely` has been added to many locales, based on the Unicode data.

## Improved line breaking with xetex

It should work with most South East Asian, Indic and CJK languages supported by XeTeX.

## Fixes

* The main fix is a bug introduced in 3.41, an extra space with languages loaded on the fly.
* Line breaking was no always correct with languages loaded on the fly.
* Avoid a harmless warning about redefining a protected command (#52). 
* Locale was not switched correctly with COMBINING characters (#54).


