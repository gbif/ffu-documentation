This page lists dimensions and criterion that could be eventually reused to create:
* Data Quality profiles to assess the fitness for use of biodiversity records
* Create validation report for a dataset
* Create custom validations report for a dataset when more domain knowledge can be provided.

# Dimensions
## Completeness
### Value completion
Completeness defines if a value is provided or not. A value is considered provided if:
* It is not empty (contains at least one printable character)
* It is not equals to one of the predefined placeholder (e.g. NULL, N/A)

| Information Element  | Comments |
| ------------- | ------------- |
| [occurrenceID](http://rs.tdwg.org/dwc/terms/occurrenceID) |   |
| [eventDate](http://rs.tdwg.org/dwc/terms/eventDate) or [year](http://rs.tdwg.org/dwc/terms/year),[month](http://rs.tdwg.org/dwc/terms/month), [day](http://rs.tdwg.org/dwc/terms/day) |   |

## Integrity

### Uniqueness
Uniqueness defines if a value is used only once inside a predefined scope.
This dimension normally implies "Value completion". Eventually, this dimension could be expended to an entire record to flag duplicated records.

| Information Element  | Context | Comments |
| ------------- | ------------- |------------- |
| [occurrenceID](http://rs.tdwg.org/dwc/terms/occurrenceID) | [Occurrence](http://rs.tdwg.org/dwc/terms/Occurrence)  |   |
| [taxonID](http://rs.tdwg.org/dwc/terms/taxonID) | [Taxon](http://rs.tdwg.org/dwc/terms/Taxon)  |   |

### Referential integrity

| Information Element  | Reference | Comments |
| ------------- | ------------- |------------- |
| [parentNameUsageID](http://rs.tdwg.org/dwc/terms/parentNameUsageID) | [taxonID](http://rs.tdwg.org/dwc/terms/taxonID) | [Taxon](http://rs.tdwg.org/dwc/terms/Taxon)  |

### Controlled vocabulary
Controlled vocabulary defines if a value is present in a list of predefined acceptable values. The options to handle empty/missing values and case-sensitivity is up to the implementation.
 
| Information Element  | Comments |
| ------------- | ------------- |
| [basisOfRecord](http://rs.tdwg.org/dwc/terms/basisOfRecord) |   |

### Data type

| Information Element  | Comments |
| ------------- | ------------- |
| [eventDate](http://rs.tdwg.org/dwc/terms/eventDate) | date, including partial date and date range  |
| [year](http://rs.tdwg.org/dwc/terms/year) | integer |
| [month](http://rs.tdwg.org/dwc/terms/month) | integer  |
| [day](http://rs.tdwg.org/dwc/terms/day) | integer  |
| [decimalLatitude](http://rs.tdwg.org/dwc/terms/decimalLatitude) | float/double  |
| [decimalLongitude](http://rs.tdwg.org/dwc/terms/decimalLongitude) | float/double  |
| [minimumDepthInMeters](http://rs.tdwg.org/dwc/terms/minimumDepthInMeters) | numeric  |
| [maximumDepthInMeters](http://rs.tdwg.org/dwc/terms/maximumDepthInMeters) | numeric  |
| [minimumElevationInMeters](http://rs.tdwg.org/dwc/terms/minimumElevationInMeters) | numeric  |
| [maximumElevationInMeters](http://rs.tdwg.org/dwc/terms/maximumElevationInMeters) | numeric  |

### Data format
?

### Minimum/Maximum
Defines that the value of a minimum IE must be smaller (or equals) to the value of a maximum IE.

| Information Element  | Comments |
| ------------- | ------------- |
|<ul><li>[minimumDepthInMeters](http://rs.tdwg.org/dwc/terms/minimumDepthInMeters)</li><li>[maximumDepthInMeters](http://rs.tdwg.org/dwc/terms/maximumDepthInMeters)</li></ul> |  |
|<ul><li>[minimumElevationInMeters](http://rs.tdwg.org/dwc/terms/minimumElevationInMeters)</li><li>[maximumElevationInMeters](http://rs.tdwg.org/dwc/terms/maximumElevationInMeters)</li></ul> |  |

## Likeliness
Defines the bounds within which the values should be considered "possible".

### Coordinates decimal part distribution
Check the distribution of the decimal part of decimalLatitude, decimalLongitude to identify suspicious datasets where the range  0.0-0.6 is over represented. This can be a symptom of incorrect conversion from a degree, minute, seconds coordinates.

## Consistency
Agreement/accordance with characteristics previously shown or stated. Absence of contradiction.

### Mismatch
| Information Element  | Comments |
| ------------- | ------------- |
| <ul><li>[eventDate](http://rs.tdwg.org/dwc/terms/eventDate)</li><li>[year](http://rs.tdwg.org/dwc/terms/year)</li><li>[month](http://rs.tdwg.org/dwc/terms/month)</li><li>[day](http://rs.tdwg.org/dwc/terms/day)</li></ul> |   |
| <ul><li>[countryCode](http://rs.tdwg.org/dwc/terms/countryCode)</li><li>[decimalLongitude](http://rs.tdwg.org/dwc/terms/decimalLongitude)</li><li>[decimalLatitude](http://rs.tdwg.org/dwc/terms/decimalLatitude)</li></ul> |   |

## Resolution/Precision
The precision dimension is not easy to define and can be easily confused with the more formal definition of [precision](https://en.wikipedia.org/wiki/Accuracy_and_precision) - how close repeated measured values are to each other. While this description is correct to express GPS related precision, it is not totally clear when it comes to express the number of digits used to store or export the data. This is the reason we should borrow the word used in the GIS world "resolution" with a simple definition : level or quantity of details provided.

### Geographical Resolution

| Information Element  | Comments |
| ------------- | ------------- |
| [dataGeneralizations](http://rs.tdwg.org/dwc/terms/dataGeneralizations)  |   |
| [coordinateUncertaintyInMeters](http://rs.tdwg.org/dwc/terms/coordinateUncertaintyInMeters)  | Radius in meter  |
| [coordinatePrecision](http://rs.tdwg.org/dwc/terms/coordinatePrecision)  | A decimal representation of the precision of the decimalLatitude, decimalLongitude   |
| [decimalLatitude](http://rs.tdwg.org/dwc/terms/decimalLatitude), [decimalLongitude](http://rs.tdwg.org/dwc/terms/decimalLongitude)  | Number of decimals provided  |
| [geodeticDatum](http://rs.tdwg.org/dwc/terms/geodeticDatum)  |   |

### Taxonomic Resolution

| Information Element  | Comments |
| ------------- | ------------- |
| <ul><li>[kingdom](http://rs.tdwg.org/dwc/terms/index.htm#kingdom)</li><li>[phylum](http://rs.tdwg.org/dwc/terms/phylum)</li><li>[class](http://rs.tdwg.org/dwc/terms/class)</li><li>[order](http://rs.tdwg.org/dwc/terms/order)</li><li>[family](http://rs.tdwg.org/dwc/terms/family)</li><li>[genus](http://rs.tdwg.org/dwc/terms/genus)</li><li>[subgenus](http://rs.tdwg.org/dwc/terms/subgenus)</li></ul> | Taxon classification, number of ranks provided  |

## Interpretability

# DQ Criteria
Criteria are used to evaluate/measure a statement to determine if a record is fit for use or to simply check a known fact (e.g. extracted from the metadata) against the related records.

## Dimension based
All dimensions must be used within a DQ Criterion in order to make it possible to check its fitness for use or its validity.

### Controlled vocabulary
Built on top of a "Controlled vocabulary dimension" the Controlled vocabulary Criterion is used to provided a specific set of accepted values for a specific information element. 

## Range
Can be used to limit coordinates within a bounding box or dates within a specific interval.

