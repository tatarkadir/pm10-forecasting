# OASI dataset

The dataset, stored in `TI_MOR_20160101_20221231_dataset_final.csv`, contains measurements and meteorological forecasts related 
to various locations of Canton Ticino acquired and predicted during the period 2016-2022. It is constituted of a 2557x8536 matrix.
The first 8488 columns are input features to use to predict the targets stored in the last 48 columns of the matrix.
The basic idea is to forecast the daily means of PM10 pollutants in different locations of the Ticino region.
For more information about how these data are acquired and managed, please refer to https://www.oasi.ti.ch.

## File structure: 

<pre>
date,input1,input2,input3,...,inputN,target1,target2,...,targetM
2016-01-01,2.3,6.5,8.9,....,0.25,12.5,13.7,...,15.8
2016-01-02,...
...
2022-12-31,...
</pre>

## Input naming conventions:

### Measurements:

<pre>
$LOCATION__$SIGNAL__$HOUR
</pre>

Where:

* `$LOCATION` is the station code where the data was measured (e.g. MEN (Mendrisio), please see the locations section for details)
* `$SIGNAL` is the signal code related to the measured data (e.g. RH (relative humidity), please see the signals section for details)
* `$HOUR` is the temporal distance in the past between the measurement and 04:00 UTC. 

Example: `BIO__NO2__m2` is the NO2 measured in Bioggio (BIO) at 02:00 UTC, two hours before 04:00 UTC. 

### Meteorological forecast:

<pre>
$LOCATION__$SIGNAL__$STEP
</pre>

Where:

* `$LOCATION` is the location code related to the forecast (e.g. GEN (Monte Generoso), please see the locations section for details)
* `$SIGNAL` is the signal code related to the forecast data (e.g. GLOB (global irradiance), please see the signals section for details)
* `$STEP` is the temporal distance in the future between the forecast and 01:00 UTC. 

Example: `MTR__GLOB__step9` is the forecast irradiance in Matro (MTR) at 10:00 UTC, nine hours after 01:00 UTC. 

## Targets naming conventions:

<pre>
$LOCATION__$SIGNAL__$DAY_AHEAD
</pre>

Where:

* `$LOCATION` is the location code related to the forecast (e.g. GEN (Monte Generoso), please see the locations section for details)
* `$SIGNAL` is the signal code related to the forecast data (e.g. GLOB (global irradiance), please see the signals section for details)
* `$DAY_AHEAD` is the prediction forecast (`d0` is the present day to predict, `d1` one day ahead and so on until `d5`). 

Example: `BRI__YPM10-dailymean__d3` is the PM10 daily average measured in Brione (BRI) three days ahead compared to the present day. 

## Locations codes:

### Measurements:

<pre>
'Bioggio': 'BIO',
'Brione sopra Minusio': 'BRI',
'Chiasso': 'CHI',
'Giubiasco': 'GIU',
'Locarno': 'LOC',
'Mendrisio': 'MEN',
'Sagno': 'SAG',
'Tesserete': 'TES',
'Lugano': 'LUG',
'Magadino': 'NA-MAG',
'Comprovasco (Meteosvizzera)': 'MS-COM',
'Cimetta (Meteosvizzera)': 'MS-CIM',
'Monte Generoso (Meteosvizzera)': 'MS-GEN',
'Gutsch (Meteosvizzera)': 'MS-GUT',
'Kloten (Meteosvizzera)': 'MS-KLO',
'Locarno Monti (Meteosvizzera)': 'MS-OTL',
'Magadino (Meteosvizzera)': 'MS-MAG',
'Matro (Meteosvizzera)': 'MS-MAT',
'Lugano (Meteosvizzera)': 'MS-LUG',
'Stabio (Meteosvizzera)': 'MS-STB',
</pre>

### Meteorological forecast:

<pre>
'Comprovasco': 'COM', 
'Magadino': 'MAG', 
'Matro': 'MTR', 
'Locarno Monti': 'OTL', 
'Brione sopra Minusio': 'P_BSM', 
'Locarno': 'P_LOC', 
'Giubiasco': 'TIGIU', 
'Monte Generoso': 'GEN', 
'Bioggio': 'P_BIO', 
'Capriasca': 'P_CAP',
'Sagno': 'P_SAG', 
'Stabio': 'SBO', 
'Chiasso': 'TICIA'
</pre>

## Signals codes:

### Measurements:

<pre>
PM10
NO
NO2
NOx
O3
CN
Gl
P
Prec
RH
T
WDvect
WSgust
WSvect
</pre>

### Meteorological forecast:

<pre>
GLOB
PS
TOT_PREC
RELHUM_2M
T_2M
TD_2M
DD_10M
FF_10M
CLCT
PS_c2
TOT_PREC_c2
RELHUM_2M_c2
T_2M_c2
TD_2M_c2
CLCT_c2
</pre>


