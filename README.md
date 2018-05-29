# spatsoc [working.title]
Title: Group animal location data by their spatial and temporal relationship


## Style
* group_points
* grp_pts
* GroupPts
* GroupPoints

R source code

* group-pts
* group_pts

**single return per function**



## Tests

* readcsv 
* read_table


do we want to return vertices strictly for kernel?

## TODO
* check that all functions have proper is null DT and colnames present / it didn't break anything
* check for [] for DT and fix so outputs what we want
* what are the incompatibilities between randomization + grouping methods

## Vignettes
* highlight build blocks

### Functions
#### Global
* missing adehabitat, SearchTrees
* if ID is character vector, paste?? (as in ID, Year ---> AN1_2007)
* or: try   as Idate/asITime  pull hours + minutes. if minutes > 30, add 30 else keep hours. thatll round to closest hour
* create example data in xy loc form
* create example data in sp form for lines, points and multipolygons
* must check if provided columns are found in input data, otherwise non descript errors like type closure (since date col similar to date function)
* remove comments from functions
* function for get_group_by_individual speedup
* check improvements in performance given the switch to an integer time group vs posixct

#### Randomizations/Iterations
```
Iterations(z, 'ID', 10, 'group', 'daily', 'datetime')
 Hide Traceback
 
 Rerun with Debug
 Error in .subset2(x, i, exact = exact) : 
  attempt to select less than one element in get1index
```

#### Nearest
* `Error in [.data.table(dt, , FindNearest(.SD, coordFields, idField),  :
  column or expression 1 of 'by' or 'keyby' is type closure. Do not quote column names. Usage: DT[,sum(colC),by=list(colA,month(colB))]`
* above occurs when the column name provided does not match any from the DT

#### GroupTime
* time threshold needs error handling
* warn if minutes are not divisible by 60 or if greater than 60
* is "timegroup" the best output column name
* time zone handling since posixct

#### GroupPts
* flex chaining or not?
* `list(split(spPts@coords, c(col(spPts@coords)))` compare this to `as.list(as.data.frame)` for speed
* add optional return spatial + time groups

#### GroupLines

#### GroupHRs/Polys
* proportional overlap
* add a build polygons step in addition to the homerange
* change group HRs to group Polys?
* sub functions for build HR, build polys.. then group all resulting polys

#### PairwiseDist
* only mean? or flexible stat?

#### Foverlaps
* build clusters
* output from clusters consistent (time start, end + xy)


### Man
* Description...
* check about which are exported
* in vignette descripe how to run within a data.table to update columns etc

### Decisions
* decide if we want to (**as a standard**) allow users to provide column names, or force them to provide things as required. OR add a prep step.
* similarly about time groups
* is it acceptable for a user to be **required** to provide a data.table? https://stackoverflow.com/questions/26069219/using-setdt-inside-a-function
* is the package going to follow suit with data.table's modify on reference or is it going to simply return columns? (or option(modByRef = TRUE))
* should we only return one or few columns so that the functions can integrate in dt[, grp := ...]
* use @importFrom pkg fun to decrease cost of repeated function callsMV917540R0

### Style/Naming
* group polys or group HRs?
* can't use spatsoc, too similar to spatstat
* (later) review all variable, function etc names for conflicts and for clarity/brevity
* do we prefer grp_lines or GroupLines

### Testing
* look at moveBank other forms of data


## To Read
### Build
* read about dt in functions/packages
* wowowow: https://stackoverflow.com/questions/25898162/data-table-anonymous-function-in-j
* suppressing intermediate... http://brooksandrew.github.io/simpleblog/articles/advanced-data-table/
* https://stackoverflow.com/questions/28078640/adding-new-columns-to-a-data-table-by-reference-within-a-function-not-always-wor
* https:/stackoverflow.com/questions/30601332/data-table-assignment-by-reference-within-function/
* https://stackoverflow.com/questions/8030452/pass-by-reference-operator-in-the-data-table-package-modifies-another-data
* https://stackoverflow.com/questions/10527072/using-data-table-package-inside-my-own-package


### Papers/Packages
* http://onlinelibrary.wiley.com/doi/10.1111/j.2041-210X.2011.00169.x/epdf
* wildlifeDI(/TG?)
* asnipe
* tim paco methods ecology evo paper
