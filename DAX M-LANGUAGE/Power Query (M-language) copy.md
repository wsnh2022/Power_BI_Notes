---

# 🧠 Power Query (M-language) Custom Column Formula Guide.

---

<details>
<summary>
<h2>🟩 1. Math & Calculation Columns</h2>
</summary>

|  # | What You Want to Do            | Formula                                            |
| -: | ------------------------------ | -------------------------------------------------- |
|  1 | Total Amount (before discount) | `=[Qty] * [UnitPrice]`                             |
|  2 | Discount Amount                | `=[Qty] * [UnitPrice] * [Discount%] / 100`         |
|  3 | Final Price (after discount)   | `=[Qty] * [UnitPrice] * (1 - [Discount%] / 100)`   |
|  4 | Add Tax (18%)                  | `([Qty]*[UnitPrice]) * 0.18`                       |
|  5 | Format Total as ₹1,000 format  | `"₹" & Text.From(Number.Round([Qty]*[UnitPrice]))` |

</details>

---

<details>
<summary><h2>🟨 2. Date & Time Columns</h2></summary>

|  # | What You Want to Do                | Formula                                                                              |
| -: | ---------------------------------- | ------------------------------------------------------------------------------------ |
|  6 | Order Month Name                   | `Date.MonthName([OrderDate])`                                                        |
|  7 | Order Year                         | `Date.Year([OrderDate])`                                                             |
|  8 | Order Quarter                      | `Date.QuarterOfYear([OrderDate])`                                                    |
|  9 | Days Since Order                   | `Duration.Days(DateTime.LocalNow() - [OrderDate])`                                   |
| 10 | Days till Month End                | `Duration.Days(Date.EndOfMonth([OrderDate]) - [OrderDate])`                          |
| 11 | Days till Next Month Start         | `Duration.Days(Date.StartOfMonth(Date.AddMonths([OrderDate], 1)) - [OrderDate])`     |
| 12 | Extract Month Number (1–12)        | `Date.Month([OrderDate])`                                                            |
| 13 | Add Order Week Number              | `Date.WeekOfYear([OrderDate])`                                                       |
| 14 | Show “OLD” if Order > 180 days ago | `if Duration.Days(DateTime.LocalNow() - [OrderDate]) > 180 then "OLD" else "RECENT"` |
| 15 | Is Weekend Order                   | `let d = Date.DayOfWeek([OrderDate]) in d = 0 or d = 6`                              |
| 16 | Extract Day of Week                | `Date.DayOfWeekName([OrderDate])`                                                    |

</details>

---

<details>
<summary><h2>🟦 3. Text & String Operations</h2></summary>

|  # | What You Want to Do                     | Formula                                         |
| -: | --------------------------------------- | ----------------------------------------------- |
| 17 | Length of Customer Name                 | `Text.Length([Customer])`                       |
| 18 | First Letter of Product                 | `Text.Start([Product], 1)`                      |
| 19 | Make Product Name UPPERCASE             | `Text.Upper([Product])`                         |
| 20 | Make Customer Name lowercase            | `Text.Lower([Customer])`                        |
| 21 | Check if Product contains “pen”         | `Text.Contains(Text.Lower([Product]), "pen")`   |
| 22 | Remove Spaces from Customer             | `Text.Trim([Customer])`                         |
| 23 | Replace Missing Discount with 0         | `if [Discount%] = null then 0 else [Discount%]` |
| 24 | Combine Customer + Product              | `[Customer] & " - " & [Product]`                |
| 25 | Convert Date to Text (e.g. 01-Jan-2024) | `Date.ToText([OrderDate], "dd-MMM-yyyy")`       |

</details>

---

<details>
<summary><h2>🟧 4. Conditional Logic Columns</h2></summary>

|  # | What You Want to Do                 | Formula                                                                                             |
| -: | ----------------------------------- | --------------------------------------------------------------------------------------------------- |
| 26 | Is Bulk Order (Qty > 10)            | `if [Qty] > 10 then "Yes" else "No"`                                                                |
| 27 | Category Based on Product           | `if [Product] = "Pen" then "Stationery" else "Other"`                                               |
| 28 | Flag Order Value: High, Medium, Low | `if [Qty]*[UnitPrice] > 1000 then "High" else if [Qty]*[UnitPrice] >= 500 then "Medium" else "Low"` |
| 29 | Is Order ID Even or Odd             | `if Number.Mod([OrderID], 2) = 0 then "Even" else "Odd"`                                            |

</details>

---

<details>
<summary><h2>⚙️ Pro Tips</h2></summary>

| Tip # | What to Know                                                                                                             |
| ----- | ------------------------------------------------------------------------------------------------------------------------ |
| ✅     | You can nest functions just like Excel: `if condition then Text.Upper(...) else ...`                                     |
| ✅     | Use `Text.Lower(...)` when checking strings to avoid case-sensitivity errors                                             |
| ✅     | `DateTime.LocalNow()` gives current timestamp—great for aging or date difference logic                                   |
| ✅     | `Applied Steps` lets you see and debug every step—no guesswork like DAX                                                  |
| ✅     | Avoid using `New Measure` for row-by-row logic—Power Query is much better suited                                         |
| ✅     | Always rename columns clearly after adding, to make your model readable later                                            |
| ✅     | Keep transformations **clean and lean**—Power Query runs before visuals, so performance is better than DAX for row logic |

</details>

---
