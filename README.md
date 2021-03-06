# IsoCountryAndLanguageCodes for Swift
![version](https://img.shields.io/badge/version-1.0-brightgreen.svg)
![Swift Version](https://img.shields.io/badge/swift-4.2-orange.svg?style=flat)

Iso country codes - defines codes for the names of countries, dependent territories, and special areas of geographical interest.

Iso language codes - defines the ISO-standard and native names of languages and their ISO 639-1 or -2 codes.

### What?
This is an **iOS Swift** library/class  files that does a simple lookup depending on a [alpha2](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 "alpha2"), [alpha3](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-3 "alpha3") or [numeric](http://en.wikipedia.org/wiki/ISO_3166-1_numeric "numeric") value you give it. Currently it holds all the 249 countries, territories, or areas of geographical interest that are assigned official codes in [ISO 3166-1](http://en.wikipedia.org/wiki/ISO_3166-1 "ISO 3166-1").

It also holds around 500 languages with their associated codes and alternative names and spellings.

### Features:

This library returns ISO codes, names and currencies for countries, and languages/ISO language codes

- [x] Find by alpha-2, alpha-3 or numeric (String - yes I know...)
- [x] Search by (partial) name, case- and diacritic insensitive
- [x] Search by currency code
- [x] Search by phone dialing code (+31 for Netherlands, +1 for USA, etc...)
- [x] Retrieve a corresponding emoji flag for a country code.

- [x] Find languages by ISO-639-2(B), ISO-639-2(T) or ISO-639-1
- [x] Search by (partial) name, case- and diacritic insensitive

### Usage:

You can search via numeric, alpha-2 or alpha-3 format. 
Searching an ISO code returns a struct. 

```swift
print(IsoCountryCodes.find(key: "020").name) //Andorra
print(IsoCountryCodes.find(key: "TK").name) //Tokelau
print(IsoCountryCodes.find(key: "TKL").currency) //NZD
```
You can also search by country name, currency or calling/dialing code:

```swift
dump(IsoCountryCodes.searchByName("Netherlands")
print(IsoCountryCodes.searchByCurrency("EUR").count ) // 31
print(IsoCountryCodes.searchByCallingCode("+31").first ) // Netherlands

let country = IsoCountryCodes.searchByName("Netherlands")
dump(country) // This dumps the full struct in console
```
This returns a `IsoCountryInfo` struct:

```swift
▿ IsoCountryCodes.IsoCountryInfo
    - name: Netherlands
    - numeric: 528
    - alpha2: NL
    - alpha3: NLD
    - calling: +31
    - currency: EUR
    - continent: EU
```
You can also search languages by country name or ISO-639-1 or ISO-639-2 Code,

```swift
dump(IsoLanguageCodes.searchByNativeName("Deutsch")
print(IsoLanguageCodes.searchByISO6392B("ger").first ) // German

let language = IsoLanguageCodes.searchByIsoName("German")
dump(language) // This dumps the full struct in console
```
This returns a `IsoLanguageInfo` struct:

```swift
▿ IsoLanguageCodes.IsoLanguageInfo
    - isoName: German
    - nativeName: Deutsch
    - iso6391: de
    - iso6392T: deu
    - iso6392B: ger
```

Searching by name is case- and diacritic insensitive:

```swift
dump(IsoCountryCodes.searchByName("netherlands"))
dump(IsoCountryCodes.searchByName("NETHERLANDS"))

dump(IsoCountryCodes.searchByName("Réunion"))
dump(IsoCountryCodes.searchByName("Reunion"))
```
If no full match is found, a partial match is tried:

```swift
// Full name is "Venezuela, Bolivarian Republic of"
dump(IsoCountryCodes.searchByName("Venezuela"))
```
but nothing is returned if the search results would be ambiguous:

```swift
// There are two Virgin Islands country codes:
// "Virgin Islands, British" and "Virgin Islands, U.S."
dump(IsoCountryCodes.searchByName("Virgin Islands"))

```

### Fun with flags
Retrieve a corresponding emoji flag from a country code. (Thanks to @lorismaz for this addition!)

```swift
let emojiString = IsoCountries.flag(countryCode: "NL")
// Prints 🇳🇱
``` 
or

```swift
let emojiString = IsoCountryCodes.find(key: "USA").flag
// Prints 🇺🇸
```

### Usage:

Copy/add files to your project

### License:

The 'do-whatever-you-please-with-it license. Use it or abuse it. Just keep my name at the top of the files.
