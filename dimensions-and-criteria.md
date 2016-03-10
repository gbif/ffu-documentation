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

| Information element | Comments |
| ------------- | ------------- |
| [occurrenceID](http://rs.tdwg.org/dwc/terms/occurrenceID) |  |
| [eventDate](http://rs.tdwg.org/dwc/terms/eventDate) or [year](http://rs.tdwg.org/dwc/terms/year),[month](http://rs.tdwg.org/dwc/terms/month), [day](http://rs.tdwg.org/dwc/terms/day) |  |

## 2. Integrity

### 2.1 Uniqueness

*Uniqueness* defines if a value is used only once in a predefined scope. It normally implies *Value completion*. This dimension could be expended to an entire record to flag duplicated records.

| Information element | Context | Comments |
| ------------- | ------------- |------------- |
| [occurrenceID](http://rs.tdwg.org/dwc/terms/occurrenceID) | [Occurrence](http://rs.tdwg.org/dwc/terms/Occurrence) |  |
| [taxonID](http://rs.tdwg.org/dwc/terms/taxonID) | [Taxon](http://rs.tdwg.org/dwc/terms/Taxon) |  |

### 2.2 Referential integrity

| Information element | Reference | Comments |
| ------------- | ------------- |------------- |
| [parentNameUsageID](http://rs.tdwg.org/dwc/terms/parentNameUsageID) | [taxonID](http://rs.tdwg.org/dwc/terms/taxonID) | [Taxon](http://rs.tdwg.org/dwc/terms/Taxon) |

### 2.3 Controlled vocabulary

*Controlled vocabulary* defines if a value is present in a list of predefined acceptable values. The options to handle empty/missing values and case-sensitivity is up to the implementation.
 
| Information element | Comments |
| ------------- | ------------- |
| [basisOfRecord](http://rs.tdwg.org/dwc/terms/basisOfRecord) |  |


### 2.4 Minimum/maximum

*Minimum/maximum* defines that the value of a minimum IE must be smaller or equal to the value of a maximum IE.

| Information element | Comments |
| ------------- | ------------- |
| [minimumDepthInMeters](http://rs.tdwg.org/dwc/terms/minimumDepthInMeters), [maximumDepthInMeters](http://rs.tdwg.org/dwc/terms/maximumDepthInMeters) |  |
| [minimumElevationInMeters](http://rs.tdwg.org/dwc/terms/minimumElevationInMeters), [maximumElevationInMeters](http://rs.tdwg.org/dwc/terms/maximumElevationInMeters) |  |

## 3. Conformity

### 3.1 Data type

| Information element | Comments |
| ------------- | ------------- |
| [eventDate](http://rs.tdwg.org/dwc/terms/eventDate) | date, including partial date and date range |
| [year](http://rs.tdwg.org/dwc/terms/year) | integer |
| [month](http://rs.tdwg.org/dwc/terms/month) | integer  |
| [day](http://rs.tdwg.org/dwc/terms/day) | integer |
| [decimalLatitude](http://rs.tdwg.org/dwc/terms/decimalLatitude) | float/double |
| [decimalLongitude](http://rs.tdwg.org/dwc/terms/decimalLongitude) | float/double |
| [minimumDepthInMeters](http://rs.tdwg.org/dwc/terms/minimumDepthInMeters) | numeric |
| [maximumDepthInMeters](http://rs.tdwg.org/dwc/terms/maximumDepthInMeters) | numeric |
| [minimumElevationInMeters](http://rs.tdwg.org/dwc/terms/minimumElevationInMeters) | numeric |
| [maximumElevationInMeters](http://rs.tdwg.org/dwc/terms/maximumElevationInMeters) | numeric |

### Data format

?

## 4. Likeliness

*Likeliness** defines the bounds within which the values should be considered "possible".

### 4.1 Suspicious Coordinates 

Checks the `decimalLatitude`, `decimalLongitude` to ensure they do not match exactly one of the following values:
 * 0,0
 * The centroid of the country represented by `country` or `countryCode`.
 
### 4.2 Suspicious Dates
* Check that `eventDate` or `year`,`month`,`day` is before `dateIdentified`, `dcterms:modified`, `georeferencedDate`
* Check that `eventDate` and `dateIdentified` is after 1600
* Check that `dcterms:modified` is after 1970

### 4.3 Coordinates decimal part distribution

Checks the distribution of the decimal part of `decimalLatitude`, `decimalLongitude` to identify suspicious datasets where the range `0.0-0.6` is overrepresented. This can be a symptom of incorrect conversion from a DMS coordinates.

## 5. Consistency

Agreement/accordance with characteristics previously shown or stated. Absence of contradiction.

### 5.1 Mismatch

| Information element | Comments |
| ------------- | ------------- |
| [eventDate](http://rs.tdwg.org/dwc/terms/eventDate), [year](http://rs.tdwg.org/dwc/terms/year), [month](http://rs.tdwg.org/dwc/terms/month), [day](http://rs.tdwg.org/dwc/terms/day) |  |
| [countryCode](http://rs.tdwg.org/dwc/terms/countryCode), [decimalLongitude](http://rs.tdwg.org/dwc/terms/decimalLongitude), [decimalLatitude](http://rs.tdwg.org/dwc/terms/decimalLatitude) |  |

## 6. Resolution/precision

The precision dimension is not easy to define and can be easily confused with the more formal definition of [precision](https://en.wikipedia.org/wiki/Accuracy_and_precision): how close repeated measured values are to each other. While this description is correct to express GPS related precision, it is not totally clear when it comes to express the number of digits used to store or export the data. This is the reason we should borrow the word used in the GIS world "resolution" with a simple definition: level or quantity of details provided.

### Geographical resolution

| Information element | Comments |
| ------------- | ------------- |
| [dataGeneralizations](http://rs.tdwg.org/dwc/terms/dataGeneralizations)  |   |
| [coordinateUncertaintyInMeters](http://rs.tdwg.org/dwc/terms/coordinateUncertaintyInMeters)  | Radius in meter |
| [coordinatePrecision](http://rs.tdwg.org/dwc/terms/coordinatePrecision)  | A decimal representation of the precision of the `decimalLatitude`, `decimalLongitude`  |
| [decimalLatitude](http://rs.tdwg.org/dwc/terms/decimalLatitude), [decimalLongitude](http://rs.tdwg.org/dwc/terms/decimalLongitude)  | Number of decimals provided  |
| [geodeticDatum](http://rs.tdwg.org/dwc/terms/geodeticDatum)  |   |

### Taxonomic resolution

| Information element | Comments |
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
