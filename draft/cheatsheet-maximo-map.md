# Cheatsheet - Maximo Map

References: [Maximo Mange Modules](https://maximosecrets.com/2024/04/16/maximo-manage-modules/)


## Administrations

## Analytics

## Assets

### Assets

### Asset Templates

### Locations

### Meters

Used to define a type of meter before it is associated with other application records, assets, locations, PMs, items, and condition monitoring. There are three types of meters, continuous, gauge and characteristic.

**References**
- [Meters, Meter Groups and Conditions Monitoring](https://maximosecrets.com/2022/07/15/meters-meter-groups-and-condition-monitoring-2/)

**Conceptions**
1. The three types of meters
   - Continuous
     - A CONTINUOUS meter is one where the meter reading increments over time unless it is reset, or it rolls over.
     - This is the most common meter type as it is the type used with meter-based Preventive Maintenance.
     - With a CONTINUOUS meter you need to decide whether the meter reading type is an ACTUAL or a DELTA reading when compared to the previous reading. 
   - Characteristic
     - A CHARACTERISTIC meter is used for an observation, the values of which can be selected from a domain set of values. 
     - This might be how filthy your car is from Clean, Minor Dirt, Dirty, to Very Dirty, and you would take action when the observation value you make at the beginning of the week assesses your car as Dirty or Very Dirty. 
     - With a CHARACTERISTIC meter you will need to specify the ALN Domain to be used for the observations, other types of domain can’t be used. 
   - Gauge
     - The third type is a GAUGE meter that records a numeric measurement the readings of which can fluctuate over time.
     - Think of the pressure gauge on a car tyre, you could record the measurement at the start of each week and when it drops below a certain level you need to take action. 
- For a CONTINUOUS or GAUGE meter it is a good idea to indicate the unit of measure, this is not needed for a CHARACTERISTIC meter.
- The Where Used tab indicates where the meter has been referenced, and there are five tabs to show the Assets, Locations, PMs, Items, or Condition Monitoring records where the meter is used. A meter on an Item or Tool is most often used for measuring fluid consumption, for example the diesel or petrol you put in your car.


**Pages**
1. Meter
- Meter: METER.METERNAME
- Domain: DOMAINID
- Meter Type: METERTYPE
- Unit of Measure: MEASUREUNITID
- Reading Type: READINGTYPE

**Object and Relationships**
- Table - Assets: ASSETMETER
- Table - Locations: LOCATIONMETER
- Table - PMs: PMMETER
- Table - Items: ITEM
- Table - Condition Monitoring: MEASUREPOINT


### Meter Groups

Meters can be grouped together. When a meter group is applied to an asset or location all the meters of the group will be created for it. 

**References**
- [Meters, Meter Groups and Conditions Monitoring](https://maximosecrets.com/2022/07/15/meters-meter-groups-and-condition-monitoring-2/)

**Conceptions**
- A Meter Group as the name implies is a set of meters that are used together. 
- When a meter group is applied to an asset or location, the meters in the meter group are copied over to become asset meters or location meters. All three meter types can exist in a meter group. 
- One advantage of using a meter group is that a new meter can be added to the meter group, and you can choose whether it should also be added to all assets and locations that reference this meter group. The table field ‘Apply This Meter Where Group Is Used?’  is defaulted from the header field ‘Apply New Meters Where Group Is Used?’ . When adding a new meter the table field can be modified until you save the meter to the meter group, when it then becomes read-only.
- There is no status field for a Meter Group and Meters Groups are added at the System level in Maximo, the same as for Meters.
- Meter Groups can be referenced on an Asset Template, and this adds the associated meters to the asset template. 
- A Meter Group can also be referenced on an Item or Tool of type Rotating. When an asset is created and references the item or tool, then the meter group is copied, and the asset meters created for the set of meters in the meter group. The same process also applies to a location that references a Rotating Item.
- For CONTINUOUS meters only, additional setup is required in the details area of the meter in the meter group
  - For continuous meters you should add the point at which the meter will rollover , and I would use the decimal places.
  - The field Average Calculation Method  determines how the average units per day field is calculated for the asset or location meter. This is used by meter-based Preventive Maintenance to determine when the PM will fall due. The Select Value shows four options:
    - LL is the default and takes into account all previous meter readings. This is fine to use where an asset is in constant operation and does not stand idle for long periods of time.
    - STATIC is where there is no recalculation and you enter an average value in the Static Average field  at the bottom right corner of the details area. This might be used when you don’t have a history of meter readings in Maximo but you can work out a historical average, or you have an average that you wish to apply for meter based PMs.
    - STATIC is where there is no recalculation and you enter an average value in the Static Average field  at the bottom right corner of the details area. This might be used when you don’t have a history of meter readings in Maximo but you can work out a historical average, or you have an average that you wish to apply for meter based PMs.
    - STATIC is where there is no recalculation and you enter an average value in the Static Average field  at the bottom right corner of the details area. This might be used when you don’t have a history of meter readings in Maximo but you can work out a historical average, or you have an average that you wish to apply for meter based PMs.
  - If a meter reading is performed each day of the week, the SLIDING-READINGS will give the same result as SLIDING-DAYS. However, if no meter readings are taken on a Saturday or Sunday, then there will be a difference in the average between the two calculation methods.
  - To determine whether to use SLIDING-READINGS or SLIDING-DAYS you need to ascertain how often you take a meter reading and whether the pattern is regular or irregular. With either of these two settings you need to bear in mind that an average over two readings is not a good average, you do need a larger number of readings. You also need to consider the pattern of use of the asset and you may need to take meter readings more frequently to use these settings.


**Pages**
1. Meter Group
- Meter Group: METERGROUP.GROUPNAME
- Apply New Meters Where Group Is Used?: PROPAGATEMOD
- Table - Meters in Group: METERINGROUP
  - Meter Rollover: ROLLOVER
  - Apply This Meter Where Group Is Used: PROPAGATEMETERGROUPMOD
  - Average Calculation Method: AVGCALCMETHOD
  - Sliding Window Size: SLIDINGWINDOWSIZE
  - Static Average: STATICAVERAGE

### Condition Monitoring

Used to create a measurement point for an asset or location. A measurement point is defined for a type of gauge or characteristic meter. When a measurement is received, and it is outside the action limits or is of a specific characteristic then a work order can be generated for it.

**References**
- [Meters, Meter Groups and Conditions Monitoring](https://maximosecrets.com/2022/07/15/meters-meter-groups-and-condition-monitoring-2/)

**Conceptions**
- The Condition Monitoring application is used to create measurement points for GAUGE meters or observation points for CHARACTERISTIC meters. The application is not used with CONTINUOUS meters. As these records will always reference either a location or asset (and not both), then this is a Site level object  in Maximo. There is no status field for a Condition Monitoring Point.
- To create a Condition Monitoring Point you need to reference a location or asset , and a meter. The Point field , called POINTNUM in the table, is often a field which has been generated by the autokey, it is the unique identifier for the record. Some clients use a prefix aligned with the asset class. However, I would leave this as an autokey with no prefix for the reason that the proliferation of sensors and alarm conditions would slow down the process of creating MEASUREPOINT records if you gave meaning to the structure of the identifier. You can always configure the asset class onto the application using a relationship back to the ASSETS object and add it to the Advanced Search or List tab to make it easier to query.
- The measurement or observation is recorded as part of a meter reading. You create a Condition Monitoring point if you wish to take action when a measurement exceeds upper or lower action limits, or an observation reaches a certain value. If you are not going to generate work orders when this occurs then there is little point in creating a Condition Monitoring record. You can record the measurement or observation direct in the Condition Monitoring application or through an integration point from an external source, but it is now normal to record these values through meter readings because meter readings are also used for CONTINUOUS meters.
- Meters of type GAUGE or CHARACTERISTIC can be referenced with their asset or location to create a condition monitoring point. When a record is created in the Condition Monitoring application the key field, POINTNUM, is copied to the asset meter or location meter record, which must, obviously, exist first. For GAUGE or CHARACTERISTIC meters the meter reading is copied through to the MEASUREMENTS table and the Measurement or Observation fields using the POINTNUM field as the key.
- When setting up a Condition Monitoring point you need to specify the upper/lower action limits  and the Job Plan or PM that will be used to generate a work order if the action limits are exceeded. The work order’s priority is also normally set. It is slightly different for CHARACTERISTIC meters in that you enter the values from the meter’s ALN domain that require an action, which does mean that you could use different job plans, PMs or priorities for each value.
- Work orders are generated either manually or through a background Cron Task and the work orders generated are visible in the Condition Monitoring record. The work order status will be Waiting to be Approved (WAPPR) and there will be a blank work type.
- For GAUGE meters you can also enter the upper/lower warning limits but there is no Maximo functionality that uses this. There is also no Maximo functionality that allows Condition Monitoring records to be created from a template and unusually for a Maximo application there is no Duplicate action. An Application Import could be configured to allow condition monitoring points to be created from a spreadsheet.

**Pages**
1. condition Monitoring
- Point: MEASUREPOINT.POINTNUM
- Site:
- Location:
- Asset:
- Meter: METERNAME
- Unit of Measure: MEASUREUNITID
- Section - Upper Limits
  - Upper Warning Limit: UPPERWARNING
  - Upper Action Limit: UPPERACTION
  - Upper Limit PM: ULPMNUM
  - Upper Limit Job Plan: ULJPNUM
  - Upper Limit Priority: ULPRIORITY
- Section - Lower Limits
  - LL...
- Table - Characteristic Action Values: CHARPOINTACTION
  - Value: VALUE
  - PM: PMNUM
  - Job Plan: JPNUM
  - Priority: PRIORITY
- Table - Measurements: MEASUREMENT
  - Measurement Date: MEASUREDATE
  - Measurement: MEASUREMENTVALUE
  - Observation: OBSERVATION
  - Start Measure: STARTMEASURE
    - just Characteristic
  - End Measure: ENDMEASURE
    - Characteristic
- Table - History: POINTWO
  - Work Order: WONUM
  - Effective Date: EFFECTIVEDATE

### Failure Codes

### Asset Management

### Reliability Strategies

## Building Information Models

## Contracts

## Financial

## IT Infrastructure

## Integration

## Inventory

## Planning

## Planning and Scheduling

## Preventive Maintenance

## Purchasing

## Security

## Self Service

## Service Desk

## Service Level

## System Configuration

## Task Management

## Work Orders

## Non Module Applications

### Start Center Applications

### Other Applications