# Forecast LDV of Oregon Sales and Stock Specification Reference

**Revised 17 April 2023.**

This document defines the format and structure of a FLOSS file.

_Structure and some content sourced from [GTFS reference.md](https://github.com/google/transit/blob/master/gtfs/spec/en/reference.md)_

## File Requirements

The following requirements apply to the format and contents of the file:

- Comma delimited
- UTF-8 encoded
- `.csv` extension

## Presence

Presence conditions applicable to fields:

- **Required** - The field must be included in the dataset and contain a valid value for each record.
- **Optional** - The field may be omitted from the dataset.
- **Conditionally Required** - The field must be included under conditions outlined in the field or file description.

## Field Types

- **Float** - A floating point number.
- **Integer** - An integer.
- **Enum** - An option from a set of predefined constants defined in the "Description" column. <br> _Example: The `quantity` field contains a `0` for sales and a `1` for stock_

## Field Signs

- **Non-negative** - Greater than or equal to 0.
- **Positive** - Greater than 0.

## Field Definitions

| **Field Name** | **Type** | **Presence** | **Description** |
|---|---|---|---|
| quantity | Enum | Required | Indicates quantity being represented. Valid options are:<br><br>`0` - Sales<br>`1` - Stock |
| year | Positive integer | Required | Indicates year represented conditionally:<br><br>- If `quantity` is `0`: model year<br>- If `quantity` is `1`: as of 31 December |
| class | Enum | Required | Indicates class(es) represented:<br><br>`0` - All light duty<br>`1` - Class 1, <6,000lbs; "Auto"<br>`2` - Class 2, 6,001-10,000lbs; "Light Truck" |
| powertrain | Enum | Required | Indicates primary vehicle powertrain. Valid options are:<br><br>`0` - Conventional internal combustion engine; "ICE"<br>`1` - Mainly consists of motors, conventional internal combustion engine, and battery, but the source of electrical charge for the battery power is provided by the conventional engine and/or regenerative braking; "Hybrid", "HEV"<br>`2` - Mainly consist of motors, conventional internal combustion engine and battery. Plug-in hybrid vehicles are like hybrids, but they have a larger battery pack and can be charged with an external source of electricity by electric vehicle supply equipment; "Plug-in Hybrid", "PHEV"<br>`3` - Have only a battery and electrical motor components and use electricity as the only power source; "BEV" |
| count | Non-negative integer | Conditionally Required | Count of vehicles.<br><br>Conditionally Required:<br>- **Optional** if `proportion` is defined<br>- **Required** otherwise |
| proportion | Non-negative float | Conditionally Required | Proportion of vehicles with shared `year` and `class` possessing indicated `powertrain`.<br><br>Conditionally Required:<br>- **Optional** if `count` is defined<br>- **Required** otherwise |
