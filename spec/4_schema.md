## 2.3 Schema

The optional capabilities defined in sub clauses and requirement statements of this clause MAY be implemented by any GeoPackage file.

#### 2.3.1. Data Columns
##### 2.3.1.1. Data
##### 2.3.1.1.1. Table Definition

> **Req 47:** A GeoPackage file MAY contain a table or updateable view named `gpkg_data_columns`. If present it SHALL be defined per clause 2.3.1.1.1, Table 9 and Table 32.

*Table 9: Data Columns Table or View Definition*

|Column Name | Column Type | Column Description | Null | Key |
|------------|-------------|--------------------|------|-----|
| `table_name` | text | Name of the tiles or feature table | no | PK |
| `column_name` | text | Name of the table column | no | PK|
| `name` | text | A human-readable identifier (e.g. short name) for the column_name content | yes | |
| `title` | text | A human-readable formal title for the column_name content | yes | |
| `description` | text | A human-readable description for the table_name content | yes | |
| `mime_type` | text | [MIME](http://www.iana.org/assignments/media-types/index.html) type of column_name if BLOB type, or NULL for other types | yes | |

GeoPackage applications MAY[^1] use the `gpkg_data_columns` table to store minimal application
schema identifying, descriptive and [MIME](http://www.iana.org/assignments/media-types/index.html)
type [^2] information about columns in user vector feature and tile matrix data tables that
supplements the data available from the SQLite `sqlite_master` table and pragma
`table_info(table_name)` SQL function. The `gpkg_data_columns` data CAN be used to provide more
specific column data types and value ranges and application specific structural and semantic
information to enable more informative user menu displays and more effective user decisions on the
suitability of GeoPackage contents for specific purposes.

See Annex C: Table Definition SQL clause C.8 `gpkg_data_columns`

##### 2.3.1.1.2. Table Data Values

> **Req 48:** Values of the `gpkg_data_columns` table `table_name` column value SHALL reference values in the `gpkg_contents` `table_name` column.

> **Req 49:** The `column_name` column value in a `gpkg_data_columns` table row SHALL contain the name of a column in the SQLite table or view identified by the `table_name` column value.

[^1]: A GeoPackage is not required to contain a `gpkg_data_columns` table. The `gpkg_data_columns` table in a GeoPackage MAY be empty.

[^2]: GeoPackages MAY contain MIME types other than the raster image types specified in clauses 2.2.4, 2.2.5, 3.2.2, 3.2.3, and 3.2.4 as feature attributes, but they are not required to do so