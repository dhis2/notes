# `/api/schemas` update for 2.36

Several fixes/bugfixes has been merged into 2.36 for the `/api/schemas` endpoint, please see table below for full overview.


| type                                         | property                    | schema change    | old value | new value   |
| -------------------------------------------- | --------------------------- | ---------------- | --------- | ----------- |
| `Attribute`                                  | `unique`                    | `required`       | `false`   | `true`      |
| `Attribute`                                  | `dataElementAttribute`      | `required`       | `true`    | `false`     |
| `Attribute`                                  | `indicatorAttribute`        | `required`       | `true`    | `false`     |
| `Attribute`                                  | `organisationUnitAttribute` | `required`       | `true`    | `false`     |
| `Attribute`                                  | `userAttribute`             | `required`       | `true`    | `false`     |
| `AttributeValue`                             | `value`                     | `required`       | `false`   | `true`      |
| `AttributeValue`                             |                             | `embeddedObject` | `false`   | `true`      |
| `objectStyle`                                |                             | `embeddedObject` | `false`   | `true`      |
| `access`                                     |                             | `embeddedObject` | `false`   | `true`      |
| `translation`                                |                             | `embeddedObject` | `false`   | `true`      |
| `categoryDimension`                          | `category`                  | `required`       | `false`   | `true`      |
| `categoryOptionGroupSetDimension`            | `categoryOptionGroupSet`    | `required`       | `false`   | `true`      |
| `chart`                                      | `type`                      | `propertyType`   | `TEXT`    | `CONSTANT`  |
| `eventChart`                                 | `type`                      | `propertyType`   | `TEXT`    | `CONSTANT`  |
| `reportingRate`                              | `dataSet`                   | `required`       | `false`   | `true`      |
| `reportingRate`                              | `metric`                    | `propertyType`   | `TEXT`    | `CONSTANT`  |
| `dataElementGroupSetDimension`               | `dataElementGroupSet`       | `required`       | `false`   | `true`      |
| `dataElementGroupSetDimension`               | `dataElementGroups`         | `required`       | `false`   | `true`      |
| `externalFileResource`                       |                             | `metadata`       | `true`    | `false`     |
| `organisationUnitGroupSetDimension`          | `organisationUnitGroupSet`  | `required`       | `false`   | `true`      |
| `organisationUnitGroupSetDimension`          | `organisationUnitGroups`    | `required`       | `false`   | `true`      |
| `predictor`                                  | `generator`                 | `required`       | `false`   | `true`      |
| `analyticsPeriodBoundary`                    | `programIndicator`          | `propertyType`   | `TEXT`    | `REFERENCE` |
| `programDataElementDimensionItem`            | `program`                   | `required`       | `false`   | `true`      |
| `programDataElementDimensionItem`            | `dataElement`               | `required`       | `false`   | `true`      |
| `programTrackedEntityAttributeDimensionItem` | `program`                   | `required`       | `false`   | `true`      |
| `programTrackedEntityAttributeDimensionItem` | `attribute`                 | `required`       | `false`   | `true`      |
| `jobConfiguration`                           | `jobParameters`             | `propertyType`   | `TEXT`    | `COMPLEX`   |
| `userAccess`                                 | `access`                    | `required`       | `false`   | `true`      |
| `userAccess`                                 | `id`                        | `required`       | `false`   | `true`      |
| `userAccess`                                 | `id`                        | `persisted`      | `false`   | `true`      |
| `userGroupAccess`                            | `access`                    | `required`       | `false`   | `true`      |
| `userGroupAccess`                            | `id`                        | `required`       | `false`   | `true`      |
| `userGroupAccess`                            | `id`                        | `persisted`      | `false`   | `true`      |
