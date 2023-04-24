# Forecast Oregon Vehicle Sales and Stock Specification Reference

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
| powertrain | Enum | Required | Indicates primary vehicle powertrain. Valid options are:<br><br>`0` - Internal combustion engine with no electrical propulsion; "ICE"<br>`1` - Internal combustion engine with an electrical propulsion component; "Hybrid", "HEV"<br>`2` - Internal combustion engine with an electrical propulsion component that can receive electrical power from an external source; "Plug-in Hybrid", "PHEV"<br>`3` - Electrical motor propulsion; "BEV" |
| count | Non-negative integer | Conditionally Required | Count of vehicles.<br><br>Conditionally Required:<br>- **Optional** if `proportion` is defined<br>- **Required** otherwise |
| proportion | Non-negative float | Conditionally Required | Proportion of vehicles with shared `year` and `class` possessing indicated `powertrain`.<br><br>Conditionally Required:<br>- **Optional** if `count` is defined<br>- **Required** otherwise |