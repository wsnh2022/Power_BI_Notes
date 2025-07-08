Absolutely. Here's a **clean, categorized Power Query formula guide** with all 30 formulas + pro tips, organized into themes. Great for practice and quick reference.

---

# 🧠 Power Query Custom Column Formula Guide (Excel-Style)

## 🟩 1. **Math & Calculation Columns**

|  # | What You Want to Do            | Formula                                            |
| -: | ------------------------------ | -------------------------------------------------- |
|  1 | Total Amount (before discount) | `=[Qty] * [UnitPrice]`                             |
|  2 | Discount Amount                | `=[Qty] * [UnitPrice] * [Discount%] / 100`         |
|  3 | Final Price (after discount)   | `=[Qty] * [UnitPrice] * (1 - [Discount%] / 100)`   |
| 14 | Add Tax (18%)                  | `([Qty]*[UnitPrice]) * 0.18`                       |
| 28 | Format Total as ₹1,000 format  | `"₹" & Text.From(Number.Round([Qty]*[UnitPrice]))` |

---

## 🟨 2. **Date & Time Columns**

|   # | What You Want to Do                | Formula                                                                              |
| --: | ---------------------------------- | ------------------------------------------------------------------------------------ |
|   4 | Order Month Name                   | `Date.MonthName([OrderDate])`                                                        |
|   5 | Order Year                         | `Date.Year([OrderDate])`                                                             |
|   6 | Order Quarter                      | `Date.QuarterOfYear([OrderDate])`                                                    |
|   7 | Days Since Order                   | `Duration.Days(DateTime.LocalNow() - [OrderDate])`                                   |
|  23 | Days till Month End                | `Duration.Days(Date.EndOfMonth([OrderDate]) - [OrderDate])`                          |
|  24 | Days till Next Month Start         | `Duration.Days(Date.StartOfMonth(Date.AddMonths([OrderDate], 1)) - [OrderDate])`     |
|  25 | Extract Month Number (1–12)        | `Date.Month([OrderDate])`                                                            |
|  26 | Add Order Week Number              | `Date.WeekOfYear([OrderDate])`                                                       |
|  27 | Show “OLD” if Order > 180 days ago | `if Duration.Days(DateTime.LocalNow() - [OrderDate]) > 180 then "OLD" else "RECENT"` |
|  22 | Is Weekend Order                   | `let d = Date.DayOfWeek([OrderDate]) in d = 0 or d = 6`                              |
|  13 | Extract Day of Week                | `Date.DayOfWeekName([OrderDate])`                                                    |

---

## 🟦 3. **Text & String Operations**

|  # | What You Want to Do                     | Formula                                         |
| -: | --------------------------------------- | ----------------------------------------------- |
| 16 | Length of Customer Name                 | `Text.Length([Customer])`                       |
| 17 | First Letter of Product                 | `Text.Start([Product], 1)`                      |
| 18 | Make Product Name UPPERCASE             | `Text.Upper([Product])`                         |
| 19 | Make Customer Name lowercase            | `Text.Lower([Customer])`                        |
| 20 | Check if Product contains “pen”         | `Text.Contains(Text.Lower([Product]), "pen")`   |
| 21 | Remove Spaces from Customer             | `Text.Trim([Customer])`                         |
| 30 | Replace Missing Discount with 0         | `if [Discount%] = null then 0 else [Discount%]` |
| 12 | Combine Customer + Product              | `[Customer] & " - " & [Product]`                |
| 15 | Convert Date to Text (e.g. 01-Jan-2024) | `Date.ToText([OrderDate], "dd-MMM-yyyy")`       |

---

## 🟧 4. **Conditional Logic Columns**

|  # | What You Want to Do             | Formula                                                  |
| -: | ------------------------------- | -------------------------------------------------------- |
|  8 | Is Bulk Order (Qty > 10)        | `if [Qty] > 10 then "Yes" else "No"`                     |
|  9 | Category Based on Product       | `if [Product] = "Pen" then "Stationery" else "Other"`    |
| 11 | Flag High Value Orders (>₹1000) | `if [Qty]*[UnitPrice] > 1000 then "High" else if [Qty]*[UnitPrice] >= 500 then "Medium" else "Low"`  |
| 29 | Is Order ID Even or Odd         | `if Number.Mod([OrderID], 2) = 0 then "Even" else "Odd"` |

---

## ⚙️ Pro Tips for Working in Power Query

| Tip # | What to Know                                                                                                             |
| ----- | ------------------------------------------------------------------------------------------------------------------------ |
| ✅     | You can nest functions just like Excel: `if condition then Text.Upper(...) else ...`                                     |
| ✅     | Use `Text.Lower(...)` when checking strings to avoid case-sensitivity errors                                             |
| ✅     | `DateTime.LocalNow()` gives current timestamp-great for aging or date difference logic                                   |
| ✅     | `Applied Steps` lets you see and debug every step-no guesswork like DAX                                                  |
| ✅     | Avoid using `New Measure` for row-by-row logic-Power Query is much better suited                                         |
| ✅     | Always rename columns clearly after adding, to make your model readable later                                            |
| ✅     | Keep transformations **clean and lean**-Power Query runs before visuals, so performance is better than DAX for row logic |

---
