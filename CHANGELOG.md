# 2.78.0

* Fix potential infinite loops in as-needed dropping and coalescing.
  When the threshold cannot be increased, it is now an error, rather than
  falling back to trying to lower the detail.
* Cleaning of complex polygon geometries now happens in stages
  to avoid performance problems when there are very large numbers
  of vertices.
* Label point generation happens earlier in tiling, to avoid doing slow
  operations on polygons that will not be retained anyway.

# 2.77.0

* Add --deduplicate-by-id option to tippecanoe-overzoom

# 2.76.0

* Add missing case for accumulating the mean of attributes that are inconsistently present
* Add --keep-point-cluster-position (#326)

# 2.75.1

* Further reduce memory consumption in attribute sorting and tilestats tracking

# 2.75.0

* Reduce memory consumption in attribute accumulation and feature sorting

# 2.74.0

* Add the option to join attributes from a sqlite database in tile-join
* Improve tile-join's tileset bounding box calculations

# 2.73.0

* Correctly clip features down to nothing when the clip region doesn't intersect the tile at all

# 2.72.0

* Add --clip-polygon-file and --feature-filter-file options to tippecanoe-overzoom

# 2.71.0

* Add --clip-bounding-box and --clip-polygon options to tippecanoe-overzoom

# 2.70.1

* Raise tippecanoe-decode limit on the size of individual tiles

# 2.70.0

* Performance improvements to tippecanoe-overzoom with attribute exclusion

# 2.69.0

* Fix crash when the first bin gets clipped away

# 2.68.0

* Adds `--no-tile-compression` option to `tippecanoe-overzoom`
* Make `tippecanoe-overzoom` clip the output tile to the tile buffer after assigning points to bins
* Adds `--include`/`-y` option to `tippecanoe-decode` to decode only specified attributes
* Cleans up some inconsistent handling of variable tile extents in overzooming code
* Speeds up overzooming slightly in `tile-join` by doing less preflighting to discover which child tiles contain features

# 2.67.0

* Reduce memory consumption of duplicate attribute names in `serial_feature`
* The maxzoom guess calculation now takes into account the number of duplicate feature locations

# 2.66.0

* Only bin by ID, not by geometry, if --bin-by-id-list is specified
* Do attribute accumulation in overzoom in mvt_value instead of converting to serial_val
* Fix bool values read from flatgeobuf sources (#289)

# 2.65.0

* Improve spatial distribution of --retain-points-multiplier features
* Add --preserve-multiplier-density-threshold option to maintain minimum density of multiplier features

# 2.64.0

* Add --bin-by-id to overzoom

# 2.63.0

* Top-level null filter now evaluates to true

# 2.62.6

* Remove buggy optimization to avoid reclipping in tippecanoe-overzoom

# 2.62.5

* More aggressive binning when points fail the point-in-polygon test

# 2.62.4

* Fix accumulation of count and mean in overzoom

# 2.62.3

* Summary statistics with --accumulate-numeric-attributes make it from tiling through to binning
* Prefix can be specified for --accumulate-numeric-attributes
* Added --exclude and --exclude-prefix to tippecanoe-overzoom

# 2.62.2

* Pass feature ID through with bins

# 2.62.1

* More work in progress on binning point features in overzoom

# 2.62.0

* Fix another bad interaction, this time between dropping-as-needed and --limit-tile-feature-count

# 2.61.0

* Added --calculate-feature-index option
* Added "count" accumulation type to --accumulate-attribute
* Work in progress on binning of point features in overzoom. Not ready for use yet.

# 2.60.0

* Fix bad interaction between --retain-points-multiplier and stopping early when the tile feature limit is reached
* Fix another bad interaction between --retain-points-multiplier, dropping-as-needed, and variable depth tile pyramids
* Add optional BUILD_INFO string to version
* Reorder overzoom logic to clip before dealing with multiplier and filters
* When --generate-variable-depth-tile-pyramid is in use, report the actual highest zoom generated as tileset maxzoom

# 2.59.0

* Correct `antimeridian_adjusted_bounds` latitude calculation when vertices extend beyond the edge of the Mercator plane

# 2.58.0

* Add --generate-variable-depth-tile-pyramid option
* Add --line-simplification and --tiny-polygon-size options to tippecanoe-overzoom
* Adjust tile feature limit for --retain-points-multiplier
* Tune convergence rate for --coalesce-densest and --drop-densest
* Fix overreported drop and coalesce counts in strategies

# 2.57.0

* Add multi-tile input to tippecanoe-overzoom

# 2.56.0

* Rework --coalesce-densest-as-needed and --drop-densest-as-needed to look better
* Add --maximum-string-attribute-length option

# 2.55.0

* Fix hash collisions in the string pool

# 2.53.0

* Stop trying to add features to the tile after the feature limit is reached

# 2.52.0

* Fix accidental loss (at all zooms) of features that specify an explicit minzoom

# 2.51.0

* Fix null behavior in "in" expressions
* But they are back to not using unidecode

# 2.50.0

* FSL-style "in" expressions use unidecode again

# 2.49.0

* FSL-style "in" expressions now allow numeric comparisons, but they no longer use unidecode to remove diacritics.

# 2.48.0

* Fix some undefined behavior bugs, one of which results in slight changes to line simplification choices

# 2.47.0

* Stabilize feature order in tippecanoe-overzoom when --preserve-feature-order is specified but the sequence attribute is not present

# 2.46.0

* Polygon dust returns to having the attributes of the contributing feature nearest the placeholder instead of the contributing feature with the largest area.

# 2.45.0

* Adjust tile size limit with --retain-points-multiplier dynamically within each tile, to allow multiplier features at high zooms if other features are being dropped as-needed

# 2.44.0

* Add --unidecode-data option to allow case-insensitive filter comparisons of transliterated strings

# 2.43.0

* Change -fraction-as-needed feature dropping to be consistent across tiles and zoom levels, and to follow the same pattern as point dropping by zoom level
* With -as-needed feature dropping, drop or retain entire multiplier clusters instead of individual features
* Sort the features within each multiplier cluster by its retention priority, for more consistency between zoom levels in filtered feature choice

# 2.42.0

* Improve tiling speed
* Generate tilestats for the --retain-points-multiplier attributes

# 2.41.3

* Performance optimizations to tile reading, writing, and overzooming
* Automatically vary the tile size limit by zoom level to match the intended retain-points-multiplier multiplication
* Fix decompression error when bailing out because a tile can't be made small enough
* Search harder for a feature size threshold to make the tile small enough before giving up

# 2.41.2

* Add --accumulate-attribute to tippecanoe-overzoom
* Go back to ordering features within each multiplier cluster spatially, not in the order specified for tile feature order

# 2.41.1

* Make --preserve-input-order, --order-by, --order-descending-by, --order-smallest-first, and --order-largest-first cooperate with --retain-points-multiplier. The clusters will be ordered by their lead feature in the specified sequence. The other features in each cluster will continue to be physically near the lead feature, but ordered as specified within the cluster.

# 2.41.0

* Add Felt-style expression support for -j feature filters
* Add --retain-points-multiplier option
* Add tippecanoe_decisions metadata field to record basezoom, drop rate, and multiplier
* Add multiplier thinning (-m) and feature filters (-j) to tippecanoe-overzoom

# 2.40.0

* Slightly reduce compression aggressiveness to improve as-needed dropping speed

# 2.39.0

* Reduce memory usage during tiling

# 2.38.0

* Tolerate polygon rings with insuffiently many points in input

# 2.37.1

* Reduce maximum memory used for vertex sorting

# 2.37.0

* Speed up tile-join overzooming and make it use less memory, by not including empty child tiles in the enumeration

# 2.36.0

* Make tile-join distrust the source tilesets' metadata maxzoom and minzoom
* Add a special case in --detect-longitude-wraparound not to wrap around jumps of exactly 360°

# 2.35.0

* Fix a bug in --detect-longitude-wraparound when there are multiple rings

# 2.34.1

* Further improvements to tile-join speed

# 2.34.0

* Improve speed of overzooming in tile-join

# 2.33.0

* Further reduce memory usage of --no-simplification-of-shared-nodes by calculating the list of shared nodes globally using temporary files rather than in memory for each individual tile
* Make --no-simplification-of-shared-nodes behave for LineStrings as it does for Polygons, preventing simplification only at crossings, convergences, and divergences, not at every point along collinear segments

# 2.32.1

* Reduce memory usage of --no-simplification-of-shared-nodes for polygons

# 2.32.0

* Extend --no-simplification-of-shared-nodes to also simplify shared polygon borders consistently

# 2.31.0

* Fix tile-join crash when trying to join empty tilesets
* Add --no-tiny-polygon-reduction-at-maximum-zoom option

# 2.30.1

* Fix spurious reports of tiny polygons and 0-length LineStrings in "strategies"

# 2.30.0

* Add --extend-zooms-if-still-dropping-maximum option
* Add --overzoom option to tile-join

# 2.29.0

* Add tippecanoe-overzoom tool

# 2.28.1

* Allow --set-attribute to override an existing attribute value

# 2.28.0

* Add --preserve-point-density-threshold option to reduce blank areas of the map at low zooms
* Fix tile-join bug where use of --read-from would also accidentally enable --quiet

# 2.27.0

* Do more of line simplification in integer coordinates, to make behavior consistent across platforms
* Reduce excessive logging during pmtiles conversion
* Add --set-attribute option
* Accept JSON form of --accumulate-attribute

# 2.26.1

* Avoid crashing if there is a polygon ring with only one point

# 2.26.0

* Fix bugs in --no-simplification-of-shared-nodes
* Updated dockerfile (jtmiclat)
* Set build options to use C++-17 (james2432)
* Use std::fpclassify instead of plain fpclassify (james)
* Fix pmtiles warnings (bdon)

# 2.25.0

* Add `--include`/`-y` option to tile-join

# 2.24.0

* Add --cluster-maxzoom option to limit zoom levels that receive clustering
* Add `point_count_abbreviated` attribute to clustered features, for consistency with supercluster
* Makefile changes to support FreeBSD
* Add -r option to tile-join to provide a file containing a list of input files
* Add antimeridian_adjusted_bounds field to tileset metadata

## 2.23.0

* Remove the concept of "separate metadata." Features now always directly reference their keys and values rather than going through a second level of indirection.
* Limit the size of the string pool to 1/5 the size of memory, to prevent thrashing during feature ingestion.
* Avoid using writeable memory maps. Instead, explicitly copy data in and out of memory.
* Compress streams of features in the temporary files, to reduce disk usage and I/O latency

## 2.22.0

* Speed up feature dropping by removing unnecessary search for other small features

## 2.21.0

* Improve label placement to avoid placing labels in polygon holes

## 2.20.0

* Round coordinates instead of truncating them, for better precision when overzooming

## 2.19.0

* Don't guess an excessively large maxzoom when there is only one feature
* Set the base zoom for -Bg as part of the --smallest-maximum-zoom-guess logic

## 2.18.0

* Fix crash when using tile-join to join an empty pmtiles tileset

## 2.17.0

* Add pmtiles output format

## 2.16.0

* During tiling, limit the size of the statistics that are kept for -as-needed calculations, because they can get quite large for sources with hundreds of millions of features.

## 2.15.2

* Change tile hash function to fnv1a
* Report JSON object context on the same line as the error message

## 2.15.1

* Correct mbtiles inserts to use text instead of blob
* Add an internal data structure to represent tileset metadata

## 2.15.0

* Generate label points in a more straightforward checkerboard, and fewer of them at high zoom levels.

## 2.14.0

* Don't preflight each zoom level if one of the as-needed options is specified. Instead, go ahead and write out the tiles, and then clear out the zoom level for another try if necessary.

## 2.13.1

* Simplify geometry earlier when the in-memory representation of a tile gets large, to reduce peak memory usage

## 2.13.0

* Add --limit-tile-feature-count and --limit-tile-feature-count-at-maximum-zoom
* Coalesce small features only onto other small features with `--coalesce-smallest-as-needed`, never to large features
* Clean coalesced-as-needed features before simplifying them, to improve simplification quality

## 2.12.0

* Add `--drop-denser` option to drop points in dense clusters in preference
  to those in sparse areas.

## 2.11.0

* Change sqlite3 schema to deduplicate identical tiles
* Limit guessed maxzoom to avoid spending too many tiles on polygon fill

## 2.10.0

* Upgrade flatbuffers version

## 2.9.1

* Do label generation after simplification, not before.

## 2.9.0

* Add an option to generate label points in place of polygons
* Add --order-smallest-first and --order-largest-first options
* When tiny polygons are being aggregated into dust, keep the attributes of the largest.

## 2.8.1

* Improve precision of polygon ring area calculations

## 2.8.0

* Add the option to use a different simplification level at maxzoom

## 2.7.0

* Add the option to use the Visvalingam simplification algorithm

## 2.6.4

* Update tests that should have been updated in 2.6.2

## 2.6.3

* Fix crash in tile-join caused by wrong-way comparison

## 2.6.2

* Stop adding features to a tile if it can't possibly work, to limit memory use
* Add --integer and --fraction options to tippecanoe-decode
* Carry `strategies` field from tileset metadata through tile-join

## 2.6.1

* Upgrade protozero to version 1.7.1

## 2.6.0

* Add another drop rate guessing options, from the same metrics -zg uses
* Reduce maxzooms being guessed a little:
  * Use 1.5 standard deviations, not 2, as the minimum distinguishable
  * Give overlapping polygons and linestrings more distinct indices

## 2.5.0

* Add an option to add extra detail at maxzoom that does not factor into guessing
* Restore the intended behavior that tiny polygons don't get further simplified
* Add an option to use single-precision floating point in tiles
* Improve polygon simplification by choosing a better start/end point
* Sort attribute values in tiles to make them compress a little better
* Fix dropping of "largest" points when there are duplicate points
* Add an option to prevent guessing a basezoom higher than the maxzoom
* Add --order-by and --order-descending options

## 2.4.1

* Accept tilestats limiting options in tile-join, not just tippecanoe

## 2.4.0

* Change maxzoom guessing to take into account the standard deviation of the distances between features, so data with tight clusters will choose a higher maxzoom

## 2.3.2

* Add --smallest-maximum-zoom-guess to guess maxzoom starting at some minimum

## 2.3.1

* Track the desired tile size (the maximum size if no features were dropped) in each zoom level too.

## 2.3.0

* Drop and coalesce points too as part of smallest-as-needed dropping and coalescing
* Keep statistics in the tileset metadata of what tile size reduction strategies were used at each zoom level

## 2.2.0

* Reduce memory consumption when parsing large JSON objects
* Don't exit with an error if free disk space can't be determined

## 2.1.0

* Add barebones support for FlatGeobuf input files

## 2.0.0

* Fork of [mapbox/tippecanoe 1.36.0](https://github.com/mapbox/tippecanoe/tree/1.36.0) to http://github.com/protomaps/tippecanoe

## 1.36.0

* Update Wagyu to version 0.5.0

## 1.35.0

* Fix calculation of mean when accumulating attributes in clusters

## 1.34.6

* Fix crash when there are null entries in the metadata table

## 1.34.5

* Fix line numbers in GeoJSON feature parsing error messages

## 1.34.4

* Be careful to avoid undefined behavior from shifting negative numbers

## 1.34.3

* Add an option to keep intersection nodes from being simplified away

## 1.34.2

* Be more consistent about when longitudes beyond 180 are allowed.
  Now if the entire feature is beyond 180, it will still appear.

## 1.34.1

* Don't run shell filters if the current zoom is below the minzoom
* Fix -Z and -z for tile directories in tile-join and tippecanoe-decode
* Return a successful error status for --help and --version

## 1.34.0

* Record the command line options in the tileset metadata

## 1.33.0

* MultiLineStrings were previously ignored in Geobuf input

## 1.32.12

* Accept .mvt as well as .pbf in directories of tiles
* Allow tippecanoe-decode and tile-join of directories with no metadata

## 1.32.11
* Don't let attribute exclusion apply to the attribute that has been specified
  to become the feature ID

## 1.32.10

* Fix a bug that disallowed a per-feature minzoom of 0

## 1.32.9

* Limit tile detail to 30 and buffer size to 127 to prevent coordinate
  delta overflow in vector tiles.

## 1.32.8

* Better error message if the output tileset already exists

## 1.32.7

* Point features may now be coalesced into MultiPoint features with --coalesce.
* Add --hilbert option to put features in Hilbert Curve sequence

## 1.32.6

* Make it an error, not a warning, to have missing coordinates for a point

## 1.32.5

* Use less memory on lines and polygons that are too small for the tile
* Fix coordinate rounding problem that was causing --grid-low-zooms grids
  to be lost at low zooms if the original polygons were not aligned to
  tile boundaries

## 1.32.4

* Ignore leading zeroes when converting string attributes to feature IDs

## 1.32.3

* Add an option to convert stringified number feature IDs to numbers
* Add an option to use a specified feature attribute as the feature ID

## 1.32.2

* Warn in tile-join if tilesets being joined have inconsistent maxzooms

## 1.32.1

* Fix null pointer crash when reading filter output that does not
  tag features with their extent
* Add `--clip-bounding-box` option to clip input geometry

## 1.32.0

* Fix a bug that allowed coalescing of features with mismatched attributes
  if they had been passed through a shell prefilter

## 1.31.7

* Create the output tile directory even if there are no valid features

## 1.31.6

* Issue an error message in tile-join if minzoom is greater than maxzoom

## 1.31.5

* Add options to change the tilestats limits

## 1.31.4

* Keep tile-join from generating a tileset name longer than 255 characters

## 1.31.3

* Fix the missing filename in JSON parsing warning messages

## 1.31.2

* Don't accept anything inside another JSON object's properties as a
  feature or geometry of its own.

## 1.31.1

* Add --exclude-all to tile-join

## 1.31.0

* Upgrade Wagyu to version 0.4.3

## 1.30.6

* Take cluster distance into account when guessing a maxzoom

## 1.30.4

* Features within the z0 tile buffer of the antimeridian (not only
  those that cross it) are duplicated on both sides.

## 1.30.3

* Add an option to automatically assign ids to features

## 1.30.2

* Don't guess a higher maxzoom than is allowed for manual selection

## 1.30.1

* Ensure that per-feature minzoom and maxzoom are integers
* Report compression errors in tippecanoe-decode
* Add the ability to specify the file format with -L{"format":"…"}
* Add an option to treat empty CSV columns as nulls, not empty strings

## 1.30.0

* Add a filter extension to allow filtering individual attributes

## 1.29.3

* Include a generator field in tileset metadata with the Tippecanoe version

## 1.29.2

* Be careful to remove null attributes from prefilter/postfilter output

## 1.29.1

* Add --use-source-polygon-winding and --reverse-source-polygon-winding

## 1.29.0

* Add the option to specify layer file, name, and description as JSON
* Add the option to specify the description for attributes in the
  tileset metadata
* In CSV input, a trailing comma now counts as a trailing empty field
* In tippecanoe-json-tool, an empty CSV field is now an empty string,
  not null (for consistency with tile-join)

## 1.28.1

* Explicitly check for infinite and not-a-number input coordinates

## 1.28.0

* Directly support gzipped GeoJSON as input files

## 1.27.16

* Fix thread safety issues related to the out-of-disk-space checker

## 1.27.15

* --extend-zooms-if-still-dropping now also extends zooms if features
  are dropped by --force-feature-limit

## 1.27.14

* Use an exit status of 100 if some zoom levels were successfully
  written but not all zoom levels could be tiled.

## 1.27.13

* Allow filtering features by zoom level in conditional expressions
* Lines in CSV input with empty geometry columns will be ignored

## 1.27.12

* Check integrity of sqlite3 file before decoding or tile-joining

## 1.27.11

* Always include tile and layer in tippecanoe-decode, fixing corrupt JSON.
* Clean up writing of JSON in general.

## 1.27.10

* Add --progress-interval setting to reduce progress indicator frequency

## 1.27.9

* Make clusters look better by averaging locations of clustered points

## 1.27.8

* Add --accumulate-attribute to keep attributes of dropped, coalesced,
  or clustered features
* Make sure numeric command line arguments are actually numbers
* Don't coalesce features whose non-string-pool attributes don't match

## 1.27.7

* Add an option to produce only a single tile
* Retain non-ASCII characters in layernames generated from filenames
* Remember to close input files after reading them
* Add --coalesce-fraction-as-needed and --coalesce-densest-as-needed
* Report distances in both feet and meters

## 1.27.6

* Fix opportunities for integer overflow and out-of-bounds references

## 1.27.5

* Add --cluster-densest-as-needed to cluster features
* Add --maximum-tile-features to set the maximum number of features in a tile

## 1.27.4

* Support CSV point input
* Don't coalesce features that have different IDs but are otherwise identical
* Remove the 700-point limit on coalesced features, since polygon merging
  is no longer a performance problem

## 1.27.3

* Clean up duplicated code for reading tiles from a directory

## 1.27.2

* Tippecanoe-decode can decode directories of tiles, not just mbtiles
* The --allow-existing option works on directories of tiles
* Trim .geojson, not just .json, when making layer names from filenames

## 1.27.1

* Fix a potential null pointer when parsing GeoJSON with bare geometries
* Fix a bug that could cause the wrong features to be coalesced when
  input was parsed in parallel

## 1.27.0

* Add tippecanoe-json-tool for sorting and joining GeoJSON files
* Fix problem where --detect-shared-borders could simplify polygons away
* Attach --coalesce-smallest-as-needed leftovers to the last feature, not the first
* Fix overflow when iterating through 0-length lists backwards

## 1.26.7

* Add an option to quiet the progress indicator but not warnings
* Enable more compiler warnings and fix related problems

## 1.26.6

* Be more careful about checking for overflow when parsing numbers

## 1.26.5

* Support UTF-16 surrogate pairs in JSON strings
* Support arbitrarily long lines in CSV files.
* Treat CSV fields as numbers only if they follow JSON number syntax

## 1.26.4

* Array bounds bug fix in binary to decimal conversion library

## 1.26.3

* Guard against impossible coordinates when decoding tilesets

## 1.26.2

* Make sure to encode tile-joined integers as ints, not doubles

## 1.26.1

* Add tile-join option to rename layers

## 1.26.0

Fix error when parsing attributes with empty-string keys

## 1.25.0

* Add --coalesce-smallest-as-needed strategy for reducing tile sizes
* Add --stats option to tipppecanoe-decode

## 1.24.1

* Limit the size and depth of the string pool for better performance

## 1.24.0

* Add feature filters using the Mapbox GL Style Specification filter syntax

## 1.23.0

* Add input support for Geobuf file format

## 1.22.2

* Add better diagnostics for NaN or Infinity in input JSON

## 1.22.1

* Fix tilestats generation when long string attribute values are elided
* Add option not to produce tilestats
* Add tile-join options to select zoom levels to copy

## 1.22.0

* Add options to filter each tile's contents through a shell pipeline

## 1.21.0

* Generate layer, feature, and attribute statistics as part of tileset metadata

## 1.20.1

* Close mbtiles file properly when there are no valid features in the input

## 1.20.0

* Add long options to tippecanoe-decode and tile-join. Add --quiet to tile-join.

## 1.19.3

* Upgrade protozero to version 1.5.2

## 1.19.2

* Ignore UTF-8 byte order mark if present

## 1.19.1

* Add an option to increase maxzoom if features are still being dropped

## 1.19.0

* Tile-join can merge and create directories, not only mbtiles
* Maxzoom guessing (-zg) takes into account resolution within each feature

## 1.18.2

* Fix crash with very long (>128K) attribute values

## 1.18.1

* Only warn once about invalid polygons in tippecanoe-decode

## 1.18.0

* Fix compression of tiles in tile-join
* Calculate the tileset bounding box in tile-join from the tile boundaries

## 1.17.7

* Enforce polygon winding and closure rules in tippecanoe-decode

## 1.17.6

* Add tile-join options to set name, attribution, description

## 1.17.5

* Preserve the tileset names from the source mbtiles in tile-join

## 1.17.4

* Fix RFC 8142 support: Don't try to split *all* memory mapped files

## 1.17.3

* Support RFC 8142 GeoJSON text sequences

## 1.17.2

* Organize usage output the same way as in the README

## 1.17.1

* Add -T option to coerce the types of feature attributes

## 1.17.0

* Add -zg option to guess an appropriate maxzoom

## 1.16.17

* Clean up JSON parsing at the end of each FeatureCollection
  to avoid running out of memory

## 1.16.16

* Add tile-join options to include or exclude specific layers

## 1.16.15

* Add --output-to-directory and --no-tile-compression options

## 1.16.14

* Add --description option for mbtiles metadata
* Clean up some utility functions

## 1.16.13

* Add --detect-longitude-wraparound option

## 1.16.12

* Stop processing higher zooms when a feature reaches its explicit maxzoom tag

## 1.16.11

* Remove polygon splitting, since polygon cleaning is now fast enough

## 1.16.10

* Add a tippecanoe-decode option to specify layer names

## 1.16.9

* Clean up layer name handling to fix layer merging crash

## 1.16.8

* Fix some code that could sometimes try to divide by zero
* Add check for $TIPPECANOE_MAX_THREADS environmental variable

## 1.16.7

* Fix area of placeholders for degenerate multipolygons

## 1.16.6

* Upgrade Wagyu to 0.3.0; downgrade C++ requirement to C++ 11

## 1.16.5

* Add -z and -Z options to tippecanoe-decode

## 1.16.4

* Use Wagyu's quick_lr_clip() instead of a separate implementation

## 1.16.3

* Upgrade Wagyu to bfbf2893

## 1.16.2

* Associate attributes with the right layer when explicitly tagged

## 1.16.1

* Choose a deeper starting tile than 0/0/0 if there is one that contains
  all the features

## 1.16.0

* Switch from Clipper to Wagyu for polygon topology correction

## 1.15.4

* Dot-dropping with -r/-B doesn't apply if there is a per-feature minzoom tag

## 1.15.3

* Round coordinates in low-zoom grid math instead of truncating

## 1.15.2

* Add --grid-low-zooms option to snap low-zoom features to the tile grid

## 1.15.1

* Stop --drop-smallest-as-needed from always dropping all points

## 1.15.0

* New strategies for making tiles smaller, with uniform behavior across
  the whole zoom level: --increase-gamma-as-needed,
  --drop-densest-as-needed, --drop-fraction-as-needed,
  --drop-smallest-as-needed.
* Option to specify the maximum tile size in bytes
* Option to turn off tiny polygon reduction
* Better error checking in JSON parsing

## 1.14.4

* Make -B/-r feature-dropping consistent between tiles and zoom levels

## 1.14.3

* Add --detect-shared-borders option for better polygon simplification

## 1.14.2

* Enforce that string feature attributes must be encoded as UTF-8

## 1.14.1

* Whitespace after commas in tile-join .csv input is no longer significant

## 1.14.0

* Tile-join is multithreaded and can merge multiple vector mbtiles files together

## 1.13.0

* Add the ability to specify layer names within the GeoJSON input

## 1.12.11

* Don't try to revive a placeholder for a degenerate polygon that had negative area

## 1.12.10

* Pass feature IDs through in tile-join

## 1.12.9

* Clean up parsing and serialization. Provide some context with parsing errors.

## 1.12.8

* Fix the spelling of the --preserve-input-order option

## 1.12.7

* Support the "id" field of GeoJSON objects and vector tile features

## 1.12.6

* Fix error reports when reading from an empty file with parallel input

## 1.12.5

* Add an option to vary the level of line and polygon simplification
* Be careful not to produce an empty tile if there was a feature with
  empty geometry.

## 1.12.4

* Be even more careful not to produce features with empty geometry

## 1.12.3

* Fix double-counted progress in the progress indicator

## 1.12.2

* Add ability to specify a projection to tippecanoe-decode

## 1.12.1

* Fix incorrect tile layer version numbers in tile-join output

## 1.12.0

* Fix a tile-join bug that would retain fields that were supposed to be excluded

## 1.11.9

* Add minimal support for alternate input projections (EPSG:3857).

## 1.11.8

* Add an option to calculate the density of features as a feature attribute

## 1.11.7

* Keep metadata together with geometry for features that don't span many tiles,
  to avoid extra memory load from indexing into a separate metadata file

## 1.11.6

* Reduce the size of critical data structures to reduce dynamic memory use

## 1.11.5

* Let zoom level 0 have just as much extent and buffer as any other zoom
* Fix tippecanoe-decode bug that would sometimes show outer rings as inner

## 1.11.4

* Don't let polygons with nonzero area disappear during cleaning

## 1.11.3

* Internal code cleanup

## 1.11.2

* Update Clipper to fix potential crash

## 1.11.1

* Make better use of C++ standard libraries

## 1.11.0

* Convert C source files to C++

## 1.10.0

* Upgrade Clipper to fix potential crashes and improve polygon topology

## 1.9.16

* Switch to protozero as the library for reading and writing protocol buffers

## 1.9.15

* Add option not to clip features

## 1.9.14

* Clean up polygons after coalescing, if necessary

## 1.9.13

* Don't trust the OS so much about how many files can be open

## 1.9.12

* Limit the size of the parallel parsing streaming input buffer
* Add an option to set the tileset's attribution

## 1.9.11

* Fix a line simplification crash when a segment degenerates to a single point

## 1.9.10

* Warn if temporary disk space starts to run low

## 1.9.9

* Add --drop-polygons to drop a fraction of polygons by zoom level
* Only complain once about failing to clean polygons

## 1.9.8

* Use an on-disk radix sort for the index to control virtual memory thrashing
  when the geometry and index are too large to fit in memory

## 1.9.7

* Fix build problem (wrong spelling of long long max/min constants)

## 1.9.6

* Add an option to give specific layer names to specific input files

## 1.9.5

* Remove temporary files that were accidentally left behind
* Be more careful about checking memory allocations and array bounds
* Add GNU-style long options

## 1.9.4

* Tippecanoe-decode can decode .pbf files that aren't in an .mbtiles container

## 1.9.3

* Don't get stuck in a loop trying to split up very small, very complicated polygons

## 1.9.2

* Increase maximum tile size for tippecanoe-decode

## 1.9.1

* Incorporate Mapnik's Clipper upgrades for consistent results between Mac and Linux

## 1.9.0

* Claim vector tile version 2 in mbtiles
* Split too-complex polygons into multiple features

## 1.8.1

* Bug fixes to maxzoom, and more tests

## 1.8.0

* There are tests that can be run with "make test".

## 1.7.2

* Feature properties that are arrays or hashes get stringified
  rather than being left out with a warning.

## 1.7.1

* Make clipping behavior with no buffer consistent with Mapnik.
  Features that are exactly on a tile boundary appear in both tiles.

## 1.7.0

* Parallel processing of input with -P works with streamed input too
* Error handling if unsupported options given to -p or -a

## 1.6.4

* Fix crashing bug when layers are being merged with -l

## 1.6.3

* Add an option to do line simplification only at zooms below maxzoom

## 1.6.2

* Make sure line simplification matches on opposite sides of a tile boundary

## 1.6.1

* Use multiple threads for line simplification and polygon cleaning

## 1.6.0

* Add option of parallelized input when reading from a line-delimited file

## 1.5.1

* Fix internal error when number of CPUs is not a power of 2
* Add missing #include

## 1.5.0

* Base zoom for dot-dropping can be specified independently of
  maxzoom for tiling.
* Tippecanoe can calculate a base zoom and drop rate for you.

## 1.4.3

* Encode numeric attributes as integers instead of floating point if possible

## 1.4.2

* Bug fix for problem that would occasionally produce empty point geometries
* More bug fixes for polygon generation

## 1.4.1

* Features that cross the antimeridian are split into two parts instead
  of being partially lost off the edge

## 1.4.0

* More polygon correctness
* Query the system for the number of available CPUs instead of guessing
* Merge input files into one layer if a layer name is specified
* Document and install tippecanoe-enumerate and tippecanoe-decode

## 1.3.0

* Tile generation is multithreaded to take advantage of multiple CPUs
* More compact data representation reduces memory usage and improves speed
* Polygon clipping uses [Clipper](http://www.angusj.com/delphi/clipper/documentation/Docs/_Body.htm)
  and makes sure interior and exterior rings are distinguished by winding order
* Individual GeoJSON features can specify their own minzoom and maxzoom
* New `tile-join` utility can add new properties from a CSV file to an existing tileset
* Feature coalescing, line-reversing, and reordering by attribute are now options, not defaults
* Output of `decode` utility is now in GeoJSON format
* Tile generation with a minzoom spends less time on unused lower zoom levels
* Bare geometries without a Feature wrapper are accepted
* Default tile resolution is 4096 units at all zooms since renderers assume it

## 1.2.0

* Switched to top-down rendering, yielding performance improvements
* Add a dot-density gamma feature to thin out especially dense clusters
* Add support for multiple layers, making it possible to include more
  than one GeoJSON featurecollection in a map. [#29](https://github.com/mapbox/tippecanoe/pull/29)
* Added flags that let you optionally avoid simplifying lines, restricting
  maximum tile sizes, and coalescing features [#30](https://github.com/mapbox/tippecanoe/pull/30)
* Added check that minimum zoom level is less than maximum zoom level
* Added `-v` flag to check tippecanoe's version
