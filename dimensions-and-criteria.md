# Glossary
 * Information Element (IE): value to be measured or evaluated
 * Dimension: what to measure in the IE
 * Criteria: evaluate the dimension or the value directly of the IE and generate a result compliant or not compliant
 * Enhancement: new value proposed after a not compliant criteria evaluation

# Scope

This document focus on Criteria and not Enhancements.

This page lists dimensions and criteria that could eventually be (re)used to create:
* Generic validation reports for biodiversity datasets
* Customized validation reports for biodiversity datasets when more domain knowledge is known
* Data quality profiles to assess the fitness for use of biodiversity data

# Dimensions

## 1. Completeness

### 1.1 Value completion

*Value completion* defines if a value is provided or not. A value is considered provided if:

* It is not empty (contains at least one printable character)
* It is not equal to one of the predefined placeholders (e.g. `NULL`, `N/A`)

| ID | Terms | Comments |
| --- | ----- | -------- |
| COMPLETION_OCCURRENCE_ID | `occurrenceID` |  |
| COMPLETION_OCCURRENCE_EVENT_DATE | `eventDate` or `year`, `month`, `day` |  |
| COMPLETION_BASIS_OF_RECORD | `dwc:basisOfRecord` |  |

## 2. Integrity

### 2.1 Uniqueness

*Uniqueness* defines if a value is used only once in a predefined scope. It normally implies *Value completion*. This dimension could be expended to an entire record to flag duplicated records.

| ID | Terms | Context | Scope |
| --- | ----- | ------- |------ |
| INTEGRITY_UNIQUENESS_OCCURRENCE_ID | `occurrenceID` | [Occurrence](http://rs.tdwg.org/dwc/terms/Occurrence) | dataset |
| INTEGRITY_UNIQUENESS_TAXON_ID | `taxonID` | [Taxon](http://rs.tdwg.org/dwc/terms/Taxon) | dataset |

### 2.2 Referential integrity

| Terms | Reference | Scope | Comment |
| ----_ | --------- | ----- | ------- |
| `parentNameUsageID` | `taxonID` | [Taxon](http://rs.tdwg.org/dwc/terms/Taxon) dataset | Note, this would not be expected to hold if dwc:taxonID was an identifier specific to the dataset, and the ...NameUsageID values were external identifiers. |

### 2.3 Controlled vocabulary

*Controlled vocabulary* defines whether a value is present in a list of predefined acceptable values.  Missing values should be treated as a separate Completeness test.  Case-sensitivity is up to the definition in the vocabulary, which will generally be case sensitive.  Support for fully qualified term names (e.g. http://rs.tdwg.org/dwc/terms/PreservedSpecimen) or short names (e.g. PreservedSpecimen) MAY BE left to the implementation.
 
| ID | Terms | Comments |
| ---|------ | -------- |
| INTEGRITY_CTRL_VOCAB_BASIS_OF_RECORD | [basisOfRecord](http://rs.tdwg.org/dwc/terms/basisOfRecord) | Terms in the old [Darwin Core Type Vocabulary](http://rs.gbif.org/vocabulary/dwc/basis_of_record.xml) are in widespread use, and the string constants (e.g. PreservedSpecimen) therein are appropriate, though the namespace has changed. See: Darwin Core documentation [Decision-2009-12-07_2](http://rs.tdwg.org/dwc/terms/history/decisions/#Decision-2009-12-07_2) and [Decision-2014-10-26_15](http://rs.tdwg.org/dwc/terms/history/decisions/#Decision-2014-10-26_15) |


### 2.4 Minimum/maximum

*Minimum/maximum* defines that the value of a minimum term must be smaller or equal to the value of a maximum term.

| ID | Terms | Comments |
| ---|------ | -------- |
| INTEGRITY_MIN_MAX_DEPTH |`minimumDepthInMeters`, `maximumDepthInMeters` |  |
| INTEGRITY_MIN_MAX_ELEVATION |`minimumElevationInMeters`, `maximumElevationInMeters` |  |

## 3. Conformity

### 3.1 Data type

| ID | Terms | Comments |
| ---|---------- | ------------- |
| CONFORMITY_DATATYPE_YEAR | `year` | integer |
| CONFORMITY_DATATYPE_MONTH | `month` | integer  |
| CONFORMITY_DATATYPE_DAY | `day` | integer |
| CONFORMITY_DATATYPE_DECIMAL_LATITUDE | `decimalLatitude` | float/double |
| CONFORMITY_DATATYPE_DECIMAL_LONGITUDE | `decimalLongitude` | float/double |
| CONFORMITY_DATATYPE_DEPTH | `minimumDepthInMeters`, `maximumDepthInMeters` | numeric |
| CONFORMITY_DATATYPE_ELEVATION | `minimumElevationInMeters`, `maximumElevationInMeters` | numeric |

### Data format

| ID | Terms | Comments |
| ---|---------- | ------------- |
| CONFORMITY_DATAFORMAT_EVENT_DATE | `dwc:eventDate` | Format conforms to recommended best practice "Recommended best practice is to use an encoding scheme, such as ISO 8601:2004(E)." See: [ISO date](https://en.wikipedia.org/wiki/Iso_date), this can include partial date and date range. |

## 4. Likeliness

*Likeliness* defines the bounds within which the values should be considered "possible".

### 4.1 Coordinates 

| ID | Terms | Check | Scope | Comment |
| ---| ----- | ----- | ----- | ------- |
| LIKELINESS_COORDINATES_ZEROZERO | `decimalLatitude`, `decimalLongitude` | Do not exactly match 0,0 | record | |
| LIKELINESS_COORDINATES_BOUNDS | `decimalLatitude`, `decimalLongitude` | [-90, 90] and [-180, 180] | record | |
| LIKELINESS_COORDINATES_DIGIT_DISTRIBUTION | `decimalLatitude`, `decimalLongitude` | The decimal part in the range `0.0-0.6` is not overrepresented | dataset | Symptom of incorrect conversion from a DMS coordinates |
 
### 4.2 Dates
| ID | Terms | Check | Comment |
| ---|------ | ----- | ------- |
| LIKELINESS_DATES_EVENT_SEQUENCE |`eventDate`,`year`,`month`,`day`,`dateIdentified`,`dcterms:modified`,`georeferencedDate` | `eventDate` or `year`,`month`,`day` is before `dateIdentified`, `dcterms:modified`, `georeferencedDate` | Assuming the eventDate, year, month and day are properties of a dwc:Occurrence and are thus the date recorded. |
| LIKELINESS_DATES_EVENT |`eventDate`, `dateIdentified` | Are after 1600 and before the current date | Assuming the eventDate is a property of a dwc:Occurrence and is thus the date recorded. |
| LIKELINESS_DATES_COMPUTER |`dcterms:modified` | Is after 1970 and before the current date | Assumes that the resource is electronic.  |

## 5. Consistency

Agreement/accordance with characteristics previously shown or stated. Absence of contradiction.

### 5.1 Mismatch

| ID | Terms | Comments |
| ---|------------- | ------------- |
| CONCISTENCY_EVENT_DATE | [eventDate](http://rs.tdwg.org/dwc/terms/eventDate), [year](http://rs.tdwg.org/dwc/terms/year), [month](http://rs.tdwg.org/dwc/terms/month), [day](http://rs.tdwg.org/dwc/terms/day) |  dwc:eventDate may represent a range, values of dwc:year dwc:month, and dwc:day are not defined in this case. |
| CONCISTENCY_LOCATION| [countryCode](http://rs.tdwg.org/dwc/terms/countryCode), [decimalLongitude](http://rs.tdwg.org/dwc/terms/decimalLongitude), [decimalLatitude](http://rs.tdwg.org/dwc/terms/decimalLatitude) |  |

## 6. Resolution/precision

The precision dimension is not easy to define and can be easily confused with the more formal definition of [precision](https://en.wikipedia.org/wiki/Accuracy_and_precision): how close repeated measured values are to each other. While this description is correct to express GPS related precision, it is not totally clear when it comes to express the number of digits used to store or export the data. This is the reason we should borrow the word used in the GIS world "resolution" with a simple definition: level or quantity of details provided.

### 6.1 Coordinates resolution

| ID | Terms | Check | Scope | Comment |
| ---| ----- | ----- | ----- | ------- |
| RESOLUTION_COORDINATES_COUNTRY_CENTROID | `decimalLatitude`, `decimalLongitude`, `countryCode` | Do not exactly match the centroid of the country | record | Maybe we should tolerate it if `uncertaintyInMeter` is provided |

### Geographical resolution

| Terms | Comments |
| ------------- | ------------- |
| [dataGeneralizations](http://rs.tdwg.org/dwc/terms/dataGeneralizations)  |   |
| [coordinateUncertaintyInMeters](http://rs.tdwg.org/dwc/terms/coordinateUncertaintyInMeters)  | Radius in meter |
| [coordinatePrecision](http://rs.tdwg.org/dwc/terms/coordinatePrecision)  | A decimal representation of the precision of the `decimalLatitude`, `decimalLongitude`  |
| [decimalLatitude](http://rs.tdwg.org/dwc/terms/decimalLatitude), [decimalLongitude](http://rs.tdwg.org/dwc/terms/decimalLongitude)  | Number of decimals provided  |
| [geodeticDatum](http://rs.tdwg.org/dwc/terms/geodeticDatum)  |   |

### Taxonomic resolution

| Terms | Comments |
| ------------- | ------------- |
| [kingdom](http://rs.tdwg.org/dwc/terms/index.htm#kingdom), [phylum](http://rs.tdwg.org/dwc/terms/phylum), [class](http://rs.tdwg.org/dwc/terms/class), [order](http://rs.tdwg.org/dwc/terms/order), [family](http://rs.tdwg.org/dwc/terms/family), [genus](http://rs.tdwg.org/dwc/terms/genus), [subgenus](http://rs.tdwg.org/dwc/terms/subgenus) | Taxon classification, number of ranks provided |


# Criteria (for data quality)

Criteria are used to evaluate/measure a statement to determine if a record is fit for use or to simply check a known fact (e.g. extracted from the metadata) against the related records.

## 1. Dimension based

All dimensions must be used within a DQ criterion in order to make it possible to check its fitness for use or its validity.

### Controlled vocabulary

Built on top of a *Controlled vocabulary dimension* the Controlled vocabulary criterion is used to provided a specific set of accepted values for a specific information element. 

## 2. Range

Can be used to limit coordinates within a bounding box or dates within a specific interval.

# Contributors
* Lee Belbin
* Peter Desmet
