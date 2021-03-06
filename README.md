# Swift Formatters

```
import UIKit

extension Date {
    
    enum LocaleIdentifier: String {
        case unitedStates = "en_US"
        case brazil = "pt_BR"
    }

    enum DateFormat: String {
        case dayOfWeek = "EEEE"
        case dayFrom01To31 = "dd"
        case monthFrom1To12 = "M"
        case monthFrom01To12 = "MM"
        case fullNameOfTheMonth = "MMMM"
        case yearWith4Digits = "yyyy"
        case hourFrom0To11 = "h"
        case ampm = "a"
        case hourFrom00To12 = "hh"
        case hourFrom0To23 = "H"
        case hourFrom00To23 = "HH"
        case minuteFrom0To59 = "m"
        case minuteFrom00To59 = "mm"
    }
    
    static func getFormattedDateComponentAsStringUsing(date: Date,
                                                localeIdentifier: LocaleIdentifier,
                                                andDateFormat dateFormat: DateFormat) -> String {
        let dateFormatter = DateFormatter()
        dateFormatter.locale = Locale(identifier: localeIdentifier.rawValue)
        dateFormatter.dateFormat = dateFormat.rawValue
        return dateFormatter.string(from: date)
    }
    
}

// locale - Determines the region, data formats, and cultural preferences of the user.

let en_US_locale = Locale(identifier: "en_US")
let       locale = Locale(identifier: "pt_BR")

// Formatters

// 1. Currency:
let numberFormatter_1 = NumberFormatter()
numberFormatter_1.numberStyle = .currency
numberFormatter_1.locale = locale
let numberAsRealBrasileiro = numberFormatter_1.string(for: 1234.5678) // "R$ 1.234,57"

// 2. Percentage:
let numberFormatter_2 = NumberFormatter()
numberFormatter_2.numberStyle = .percent
let numberAsPercentage = numberFormatter_2.string(for: 0.25) // 25%"

// 3. Quantities:
let numberFormatter_3 = NumberFormatter()
numberFormatter_3.numberStyle = .decimal
let numberWithThousandsSeparator = numberFormatter_3.string(for: 12345) // 12.345

// 4. Dates:

let date = Date()

let dateFormatter_1 = DateFormatter()
dateFormatter_1.locale = locale // or Locale(identifier: LocaleIdentifier.brazil.rawValue)
dateFormatter_1.dateStyle = .short
dateFormatter_1.string(from: date) //"26/08/2020"

let dateFormatter_2 = DateFormatter()
dateFormatter_2.locale = locale
dateFormatter_2.dateStyle = .long
dateFormatter_2.string(from: date) // "26 de agosto de 2020"

let dateFormatter_3 = DateFormatter()
dateFormatter_3.locale = locale
dateFormatter_3.dateStyle = .full
dateFormatter_3.string(from: date) // "quarta-feira, 26 de agosto de 2020"

// 5. Time:

let dateFormatter_4 = DateFormatter()
dateFormatter_4.locale = locale
dateFormatter_4.timeStyle = .short
dateFormatter_4.string(from: date) // "21:11"

let dateFormatter_5 = DateFormatter()
dateFormatter_5.locale = locale
dateFormatter_5.timeStyle = .long
dateFormatter_5.string(from: date) // "21:11"

let today    = Date()
let fromDate = Calendar.current.date(byAdding: .day, value: -3, to: today)!
let toDate   = Calendar.current.date(byAdding: .day, value: +3, to: today)!
let dateIntervalFormatter = DateIntervalFormatter()
dateIntervalFormatter.locale = locale
dateIntervalFormatter.dateStyle = .short
dateIntervalFormatter.timeStyle = .none
dateIntervalFormatter.string(from: fromDate, to: toDate) // "23/08/2020 – 29/08/2020"

// ====================================================================================================================

// 6. Custom Dates

// 6.1. get some date:

let someDate = Date()

// or
let dateFormatter = DateFormatter()
dateFormatter.dateFormat = "yyyy-MM-dd"
let someDate2 = dateFormatter.date(from: "2020-05-20")!

// 6.2. get components:

let dayFrom01To31      = Date.getFormattedDateComponentAsStringUsing(date: someDate, localeIdentifier: .brazil, andDateFormat: .dayFrom01To31)
let monthFrom01To12    = Date.getFormattedDateComponentAsStringUsing(date: someDate, localeIdentifier: .brazil, andDateFormat: .monthFrom01To12)
let fullNameOfTheMonth = Date.getFormattedDateComponentAsStringUsing(date: someDate, localeIdentifier: .brazil, andDateFormat: .fullNameOfTheMonth)
let yearWith4Digits    = Date.getFormattedDateComponentAsStringUsing(date: someDate, localeIdentifier: .brazil, andDateFormat: .yearWith4Digits)

// 6.3. compose your string with components above:

print("\(dayFrom01To31) de \(fullNameOfTheMonth)") // 17 de setembro
print("\(dayFrom01To31)/\(monthFrom01To12)/\(yearWith4Digits)") // 17/09/2020

```
