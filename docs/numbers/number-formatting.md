---
title: Number Formatting
page_title: Number Formatting | Kendo UI Numbers Module
description: "Use the formatting capabilities of the formatNumber method when working with the Kendo UI Internalization package."
slug: numbeformatting_internalization
position: 2
---

# Number Formatting

Number formatting converts a `Number` object to a human-readable string using the locale specific settings. The `formatNumber` method supports standard and custom numeric formats.

## Types of Number Formats

### Standard

Standard number formatting can be specified by passing an options object or a string format.

**The `"n"` specifier**

The `"n"` specifier formats the number as a decimal number based on the locale. Precision is specified by adding a number after `"n"`. By default, the number is formatted and rounded to three decimal digits.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(1234.5678, "n"); // 1,234.568

    formatNumber(1234.5678, "n2", "bg"); // 1 234,57

    formatNumber(1234.5678, "n5"); // 1,234.56780

**The `"c"` specifier**

The `"c"` specifier formats the number as a currency based on the locale. The specified locale latest currency symbol is used for the formatting. Precision is specified by adding a number after `"c"`. By default, the number is formatted and rounded to two decimal digits, or the number of digits in the CLDR `currencyData` fractions data if the currency is available.

> The locale numbers `currencies` data and the supplemental `currencyData` must be loaded for the currency formatting to work.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(1234.5678, "c"); // $1,234.57

    formatNumber(1234.5678, "c3", "de"); // 1.234,568 €

    formatNumber(1234.5678, "c5", "bg"); // 1 234,56780 лв

**The `"p"` specifier**

The `"p"` specifier formats the number as a percentage based on the locale. The passed number is multiplied by 100. Precision is specified by adding a number after `"p"`. By default, the number is formatted and rounded to zero decimal digits.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(0.5678, "p"); // 57%

    formatNumber(0.5678, "p2", "de"); // 56,78 %

    formatNumber(0.5678, "p5"); // 56.78000%

**The `"e"` specifier**

The `"e"` specifier formats the number in exponential notation.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(0.45678, "e0"); // 5e-1

Apart from setting a string, the standard formats can also be specified by passing an object with the style option.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(1234.5678, {
        style: "decimal",
        minimumFractionDigits: 4
    }); // 1,234.5678

    formatNumber(1234.5678, {
        style: "currency",            
        currency: "EUR",
        currencyDisplay: "displayName"
    }, "bg"); // 1 234,57 евро

    formatNumber(0.5678, {
        style: "percent"
    }, "de"); // 123.457 %

For full list of available options check the [`formatNumber` API]({% slug numbersapi_internalization %}#the-formatnumber-method).

### Custom

You are able to create a custom numeric format string using one or more custom numeric specifiers. A custom numeric format string is any string which is not a standard numeric format. The supported format specifiers are listed below.

**The `"0"` specifier**

The `"0"` specifier is a zero placeholder. It replaces the zero with the corresponding digit if one is present. Otherwise, zero appears in the result string.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(1234.5678, "00000"); // 01235    

**The `"#"` specifier**

The `"#"` specifier is a digit placeholder. It replaces the Pound sign with the corresponding digit if one is present. Otherwise, no digit appears in the result string.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(1234.5678, "#####"); // 1235

> The `"#"` specifier cannot be used to format a number, such as a telephone number&mdash;for example, (###)-###-####.

**The `"."` specifier**

The `"."` specifier is a decimal placeholder. It determines the location of the decimal separator in the result string.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(0.45678, "0.00"); // 0.46

**The `","` specifier**

The `","` specifier is a group separator placeholder. It inserts a localized group separator between each group.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(12345678, "##,#"); // 12,345,678

**The `"%"` specifier**

The `"%"` specifier is a percentage placeholder. It multiplies a number by 100 and inserts a localized percentage symbol in the result string.

> The `%` symbol is interpreted as a format specifier in the format string. To prevent this, precede the `%` symbol with a double backslash&mdash;`formatNumber(12, "# \\\%")` resulting in `12 %`.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(1.1, "#.0 %"); // 110.0 %

**The `"$"` specifier**

The `"$"` specifier is a currency placeholder. It is replaced by the locale currency symbol.

> The `$` symbol is interpreted as a format specifier in the format string. To prevent this, precede the `$` symbol with a double backslash&mdash;`formatNumber(12, "# \\\$")` resulting in `12 $`.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(-123, "##,# $", "de"); // 12.345.678 €

**The `";"` specifier**

The `";"` specifier is a section separator. It defines sections with separate format strings for positive, negative, and zero numbers.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(-123, "##,#;(##,#)"); // (123)

**The `"string"/'string'` specifier**

The `"string"/'string'` specifier is a literal string delimiter. It indicates that the enclosed characters should be copied to the result string.

    import { formatNumber } from '@telerik/kendo-intl/numbers';

    formatNumber(12345678, "##,# '$'", "de"); // 12.345.678 $