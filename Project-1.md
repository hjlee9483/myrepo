Project 1: Environment and Society
================

## Hye Jeong Lee (HL9563)

### Step 1: Explore Data/ Introduction

``` r
# load data
library(readxl)

#import downloaded data No.1
se <- read.csv("SustainableEnergy.csv")
esg <- read.csv("ESG.csv")

#get a glimpse of each data set
head (se)
```

    ##   ï..Country_Name country_code Time Time_code access_cft_tot
    ## 1       Australia          AUS 1990    YR1990             ..
    ## 2       Australia          AUS 1991    YR1991             ..
    ## 3       Australia          AUS 1992    YR1992             ..
    ## 4       Australia          AUS 1993    YR1993             ..
    ## 5       Australia          AUS 1994    YR1994             ..
    ## 6       Australia          AUS 1995    YR1995             ..
    ##   access_electricity_tot ren_electricity_output share_re_in_electricity
    ## 1                    100                  14898             9.656030644
    ## 2                    100                  16590             10.59820105
    ## 3                    100                  16019             10.06686525
    ## 4                    100                  17220             10.54914357
    ## 5                    100                  17042             10.19447386
    ## 6                    100                  16631              9.62414282
    ##   re_consumption total_electricity_output share_total_re_in_TEFC
    ## 1       176729.7                   154287            8.009577159
    ## 2       181011.2                   156536             8.24547226
    ## 3       166746.4                   159126            7.516470972
    ## 4       197804.9                   163236            8.616993882
    ## 5       193855.2                   167169            8.259946779
    ## 6       199700.4                   172805            8.217805712
    ##   total_final_energy_consum primary_energy_intensity
    ## 1               2206479.774              7.416865313
    ## 2               2195279.958              7.341423042
    ## 3                2218413.41              7.448726037
    ## 4               2295520.952              7.502966324
    ## 5               2346930.376              7.206735771
    ## 6               2430093.957              7.076343308

``` r
head (esg)
```

    ##   ï..Country_Name Country_Code                         Series_Name
    ## 1       Australia          AUS natural_resources_depletion (%_GNI)
    ##         Series_Code X1972..YR1972. X1973..YR1973. X1974..YR1974. X1975..YR1975.
    ## 1 NY.ADJ.DRES.GN.ZS    0.493969132    0.814230981    1.647922025    1.671735262
    ##   X1976..YR1976. X1977..YR1977. X1978..YR1978. X1979..YR1979. X1980..YR1980.
    ## 1    1.818564419    2.019455936    1.737946626    3.130167589    3.115184645
    ##   X1981..YR1981. X1982..YR1982. X1983..YR1983. X1984..YR1984. X1985..YR1985.
    ## 1    2.143180151    1.529902982    1.947409259    2.077254025    2.556443232
    ##   X1986..YR1986. X1987..YR1987. X1988..YR1988. X1989..YR1989. X1990..YR1990.
    ## 1    1.382489732     1.78210907    1.348613783    1.302598753    1.986605415
    ##   X1991..YR1991. X1992..YR1992. X1993..YR1993. X1994..YR1994. X1995..YR1995.
    ## 1    1.165255885    1.098696142    0.987061165     1.06293539    1.039770762
    ##   X1996..YR1996. X1997..YR1997. X1998..YR1998. X1999..YR1999. X2000..YR2000.
    ## 1    1.148803256    0.980743714    0.702340884    0.842331651    1.717975754
    ##   X2001..YR2001. X2002..YR2002. X2003..YR2003. X2004..YR2004. X2005..YR2005.
    ## 1    1.420710594     1.32027277    1.204369323    1.506764645    2.489737828
    ##   X2006..YR2006. X2007..YR2007. X2008..YR2008. X2009..YR2009. X2010..YR2010.
    ## 1    3.147992817     3.96846308    4.221239329    2.632311358    3.314323959
    ##   X2011..YR2011. X2012..YR2012. X2013..YR2013. X2014..YR2014. X2015..YR2015.
    ## 1    3.831052125    3.017861237    2.668798722    2.840678674    2.012305341
    ##   X2016..YR2016. X2017..YR2017. X2018..YR2018. X2019..YR2019. X2020..YR2020.
    ## 1    2.573529242    2.512060119    3.475789511             ..             ..
    ##   X2050..YR2050.
    ## 1             ..
    ##  [ reached 'max' / getOption("max.print") -- omitted 5 rows ]

*The purpose of this project is to compare the data and see if there are
strong correlation between any environmental-related variables and
social-related variables, and also to see if there is any correlation
with GDP. The first data set se is obtained from Sustainable Energy for
All, which has data related to energy. The second data set esg is
obtained from Environment Social and Governance (ESG) data, which
contains socioeconomic factors and other environment-related variables.*

*I find them interesting because there is a strong bias about how living
a sustainable lifestyle costs more and it is for people with money, even
though it is not true. I also find them interesting because it is hard
to visualize how sustainability affects social factors positively. I
hope to find some correlation between environmental-related variables
and social-related variables to promote for more renewable energy, and
no strong correlation between environmental-related variables and GDP.*

**From se data:**

1.  access\_cft\_tot: access to clean fuel and technologies for cooking
    (% of total popluation)

2.  access\_electricity\_tot:Access to electricity (% of total
    population)

3.  ren\_electricity\_output: Renewable electricity output (GWh)

4.  share\_re\_in\_electricity: Renewable electricity share of total
    electricity output (%)

5.  re\_consumption:Renewable energy consumption (TJ)

6.  total\_electricity\_output:Total electricity output (GWh)

7.  share\_total\_re\_in\_TEFC: Renewable energy share of TFEC (%)

8.  total\_final\_energy\_consum: Total final energy consumption (TFEC)
    (TJ)

9.  primary\_energy\_intensity:Energy intensity level of primary energy
    (MJ/2011 USD PPP)

**From esg data:**

1.  Adjusted savings: net forest depletion (% of GNI) - Net forest
    depletion is calculated as the product of unit resource rents and he
    excess of roundwood harvest over natural growth.

2.  Annual freshwater withdrawals, total (% of internal resources) -
    total water withdrawals, not counting evaporation losses from
    storage basins. Withdrawals also include water from desalination
    plants in countries where they are a significant source. Withdrawals
    can exceed 100 percent of total renewable resources where extraction
    from nonrenewable aquifers or desalination plants is considerable or
    where there is significant water reuse. Withdrawals for agriculture
    and industry are total withdrawals for irrigation and livestock
    production and for direct industrial use (including withdrawals for
    cooling thermoelectric plants). Withdrawals for domestic uses
    include drinking water, municipal use or supply, and use for public
    services, commercial establishments, and homes. Data are for the
    most recent year available for 1987-2002.

3.  Agricultural land (% of land area) - the share of land area that is
    arable, under permanent crops, and under permanent pastures.

4.  Arable land includes land defined by the FAO as land under temporary
    crops (double-cropped areas are counted once), temporary meadows for
    mowing or for pasture, land under market or kitchen gardens, and
    land temporarily fallow. Land abandoned as a result of shifting
    cultivation is excluded. Land under permanent crops is land
    cultivated with crops that occupy the land for long periods and need
    not be replanted after each harvest, such as cocoa, coffee, and
    rubber. This category includes land under flowering shrubs, fruit
    trees, nut trees, and vines, but excludes land under trees grown for
    wood or timber. Permanent pasture is land used for five or more
    years for forage, including natural and cultivated crops.

5.  Agriculture, value added (% of GDP) - includes forestry, hunting,
    and fishing, as well as cultivation of crops and livestock
    production. Value added is the net output of a sector after adding
    up all outputs and subtracting intermediate inputs. It is calculated
    without making deductions for depreciation of fabricated assets or
    depletion and degradation of natural resources. The origin of value
    added is determined by the International Standard Industrial
    Classification (ISIC), revision 3. Note: For VAB countries, gross
    value added at factor cost is used as the denominator.

6.  CO2 emissions (metric tons per capita) - those stemming from the
    burning of fossil fuels and the manufacture of cement. They include
    carbon dioxide produced during consumption of solid, liquid, and gas
    fuels and gas flaring.

7.  Cooling Degree Days (projected change in degree Celsius) -
    measurement designed to quantify the demand for energy needed to
    cool buildings. It is the number of degrees that a day’s average
    temperature is above 18°C.

8.  Control of Corruption: Estimate - perceptions of the extent to which
    public power is exercised for private gain, including both petty and
    grand forms of corruption, as well as capture" of the state by
    elites and private interests. Estimate gives the country’s score on
    the aggregate indicator

9.  Droughts, floods, extreme temperatures (% of population, average
    1990-2009) - annual average percentage of the population that is
    affected by natural disasters classified as either droughts, floods,
    or extreme temperature events. A drought is an extended period of
    time characterized by a deficiency in a region’s water supply that
    is the result of constantly below average precipitation. A drought
    can lead to losses to agriculture, affect inland navigation and
    hydropower plants, and cause a lack of drinking water and famine. A
    flood is a significant rise of water level in a stream, lake,
    reservoir or coastal region. Extreme temperature events are either
    cold waves or heat waves. A cold wave can be both a prolonged period
    of excessively cold weather and the sudden invasion of very cold air
    over a large area. Along with frost it can cause damage to
    agriculture, infrastructure, and property. A heat wave is a
    prolonged period of excessively hot and sometimes also humid weather
    relative to normal climate patterns of a certain region. Population
    affected is the number of people injured, left homeless or requiring
    immediate assistance during a period of emergency resulting from a
    natural disaster; it can also include displaced or evacuated people.
    Average percentage of population affected is calculated by dividing
    the sum of total affected for the period stated by the sum of the
    annual population figures for the period stated.

10. Electricity production from coal sources (% of total) - Sources of
    electricity refer to the inputs used to generate electricity. Coal
    refers to all coal and brown coal, both primary (including hard coal
    and lignite-brown coal) and derived fuels (including patent fuel,
    coke oven coke, gas coke, coke oven gas, and blast furnace gas).
    Peat is also included in this category. Energy imports, net (% of
    energy use) - Net energy imports are estimated as energy use less
    production, both measured in oil equivalents. A negative value
    indicates that the country is a net exporter. Energy use refers to
    use of primary energy before transformation to other end-use fuels,
    which is equal to indigenous production plus imports and stock
    changes, minus exports and fuels supplied to ships and aircraft
    engaged in international transport.

11. Energy intensity level of primary energy (MJ/$2011 PPP GDP) - the
    ratio between energy supply and gross domestic product measured at
    purchasing power parity. Energy intensity is an indication of how
    much energy is used to produce one unit of economic output. Lower
    ratio indicates that less energy is used to produce one unit of
    output.

12. Energy use (kg of oil equivalent per capita) - use of primary energy
    before transformation to other end-use fuels, which is equal to
    indigenous production plus imports and stock changes, minus exports
    and fuels supplied to ships and aircraft engaged in international
    transport.

13. Fertility rate, total (births per woman) - the number of children
    that would be born to a woman if she were to live to the end of her
    childbearing years and bear children in accordance with age-specific
    fertility rates of the specified year. Food production index
    (2004-2006 = 100) - covers food crops that are considered edible and
    that contain nutrients. Coffee and tea are excluded because,
    although edible, they have no nutritive value.

14. Forest area (% of land area) - Forest area is land under natural or
    planted stands of trees of at least 5 meters in situ, whether
    productive or not, and excludes tree stands in agricultural
    production systems (for example, in fruit plantations and
    agroforestry systems) and trees in urban parks and gardens.

15. GDP growth (annual %) - Annual percentage growth rate of GDP at
    market prices based on constant local currency. Aggregates are based
    on constant 2010 U.S. dollars. GDP is the sum of gross value added
    by all resident producers in the economy plus any product taxes and
    minus any subsidies not included in the value of the products. It is
    calculated without making deductions for depreciation of fabricated
    assets or for depletion and degradation of natural resources.

16. Fossil fuel energy consumption (% of total) - Fossil fuel comprises
    coal, oil, petroleum, and natural gas products.

17. GHG net emissions/removals by LUCF (Mt of CO2 equivalent) - GHG net
    emissions/removals by LUCF refers to changes in atmospheric levels
    of all greenhouse gases attributable to forest and land-use change
    activities, including but not limited to (1) emissions and removals
    of CO2 from decreases or increases in biomass stocks due to forest
    management, logging, fuelwood collection, etc.; (2) conversion of
    existing forests and natural grasslands to other land uses; (3)
    removal of CO2 from the abandonment of formerly managed lands
    (e.g. croplands and pastures); and (4) emissions and removals of CO2
    in soil associated with land-use change and management. For Annex-I
    countries under the UNFCCC, these data are drawn from the annual GHG
    inventories submitted to the UNFCCC by each country; for non-Annex-I
    countries, data are drawn from the most recently submitted National
    Communication where available. Because of differences in reporting
    years and methodologies, these data are not generally considered
    comparable across countries. Data are in million metric tons.

18. Government expenditure on education, total (% of government
    expenditure) - percentage of total general government expenditure on
    all sectors (including health, education, social services, etc.). It
    includes expenditure funded by transfers from international sources
    to government. General government usually refers to local, regional
    and central governments.

19. Heat Index 35 (projected change in days) - Total count of days per
    year where the daily mean Heat Index rose above 35°C. The Heat Index
    is a measure of how hot it really feels when relative humidity is
    factored in with the actual air temperature.

20. Individuals using the Internet (% of population) - individuals who
    have used the Internet (from any location) in the last 3 months. The
    Internet can be used via a computer, mobile phone, personal digital
    assistant, games machine, digital TV etc.

21. Income share held by lowest 20% - the share that accrues to
    subgroups of population indicated by deciles or quintiles.
    Percentage shares by quintile may not sum to 100 because of
    rounding.

22. Life expectancy at birth, total (years) - the number of years a
    newborn infant would live if prevailing patterns of mortality at the
    time of its birth were to stay the same throughout its life.

23. Literacy rate, adult total (% of people ages 15 and above) -
    percentage of people ages 15 and above who can both read and write
    with understanding a short simple statement about their everyday
    life.

24. Mean Drought Index (projected change, unitless) - The Standardized
    Precipitation Evapotranspiration Index (SPEI), or Mean Drought
    Index, calculated for a 12-month period, has been found to be
    closely related to drought impacts on ecosystems, crop, and water
    resources. The SPEI is designed to take into account both
    precipitation and potential evapotranspiration (PET) in determining
    drought.

25. Methane emissions (metric tons of CO2 equivalent per capita) - those
    stemming from human activities such as agriculture and from
    industrial methane production.

26. Mortality rate, under-5 (per 1,000 live births) - probability per
    1,000 that a newborn baby will die before reaching age five, if
    subject to age-specific mortality rates of the specified year.

27. Net migration - Net migration is the net total of migrants during
    the period, that is, the total number of immigrants less the annual
    number of emigrants, including both citizens and noncitizens. Data
    are five-year estimates.

28. Nitrous oxide emissions (metric tons of CO2 equivalent per capita) -
    emissions from agricultural biomass burning, industrial activities,
    and livestock management.

29. People using safely managed drinking water services (% of
    population) - The percentage of people using drinking water from an
    improved source that is accessible on premises, available when
    needed and free from faecal and priority chemical contamination.
    Improved water sources include piped water, boreholes or tubewells,
    protected dug wells, protected springs, and packaged or delivered
    water.

30. People using safely managed sanitation services (% of population) -
    The percentage of people using improved sanitation facilities that
    are not shared with other households and where excreta are safely
    disposed of in situ or transported and treated offsite. Improved
    sanitation facilities include flush/pour flush to piped sewer
    systems, septic tanks or pit latrines: ventilated improved pit
    latrines, compositing toilets or pit latrines with slabs.

31. PM2.5 air pollution, mean annual exposure (micrograms per cubic
    meter) - the average level of exposure of a nation’s population to
    concentrations of suspended particles measuring less than 2.5
    microns in aerodynamic diameter, which are capable of penetrating
    deep into the respiratory tract and causing severe health damage.
    Exposure is calculated by weighting mean annual concentrations of
    PM2.5 by population in both urban and rural areas.

32. Population density (people per sq. km of land area) - midyear
    population divided by land area in square kilometers. Population is
    based on the de facto definition of population, which counts all
    residents regardless of legal status or citizenship–except for
    refugees not permanently settled in the country of asylum, who are
    generally considered part of the population of their country of
    origin. Land area is a country’s total area, excluding area under
    inland water bodies, national claims to continental shelf, and
    exclusive economic zones. In most cases the definition of inland
    water bodies includes major rivers and lakes.

33. Prevalence of overweight (% of adults) - percentage of adults ages
    18 and over whose Body Mass Index (BMI) is more than 25 kg/m2. Body
    Mass Index (BMI) is a simple index of weight-for-height, or the
    weight in kilograms divided by the square of the height in meters.

34. Prevalence of undernourishment (% of population) - percentage of the
    population whose food intake is insufficient to meet dietary energy
    requirements continuously. Data showing as 5 may signify a
    prevalence of undernourishment below 5%. Proportion of seats held by
    women in national parliaments (%) - the percentage of parliamentary
    seats in a single or lower chamber held by women.

35. Ratio of female to male labor force participation rate (%) (modeled
    ILO estimate) - Labor force participation rate is the proportion of
    the population ages 15 and older that is economically active: all
    people who supply labor for the production of goods and services
    during a specified period. Ratio of female to male labor force
    participation rate is calculated by dividing female labor force
    participation rate by male labor force participation rate and
    multiplying by 100.

36. Renewable energy consumption (% of total final energy consumption) -
    share of renewable energy in total final energy consumption.
    Renewable electricity output (% of total electricity output) - the
    share of electricity generated by renewable power plants in total
    electricity generated by all types of plants.

37. Research and development expenditure (% of GDP) - Gross domestic
    expenditures on research and development (R&D), expressed as a
    percent of GDP. They include both capital and current expenditures
    in the four main sectors: Business enterprise, Government, Higher
    education and Private non-profit. R&D covers basic research, applied
    research, and experimental development.

38. School enrollment, primary (% gross) - Gross enrollment ratio is the
    ratio of total enrollment, regardless of age, to the population of
    the age group that officially corresponds to the level of education
    shown. Primary education provides children with basic reading,
    writing, and mathematics skills along with an elementary
    understanding of such subjects as history, geography, natural
    science, social science, art, and music.

39. Unmet need for contraception (% of married women ages 15-49) - the
    percentage of fertile, married women of reproductive age who do not
    want to become pregnant and are not using contraception.

40. Unemployment, total (% of total labor force) (modeled ILO
    estimate) - the share of the labor force that is without work but
    available for and seeking employment.

### Step 2: Tidy up the dataset

``` r
library(tidyverse)
library(dplyr)

#tidy up the first data set

se_clean <- se %>%
  # get rid of unnecessary or redundant variable
  select (-country_code,-Time_code) %>%
  # rename some variables 
  rename("year" = Time, "country" = ï..Country_Name  ) %>%
  # change all the non-numerical variable to NA
  mutate_all(na_if, "..")

#check se data
glimpse (se_clean)
```

    ## Rows: 270
    ## Columns: 11
    ## $ country                   <chr> "Australia", "Australia", "Australia", "A...
    ## $ year                      <int> 1990, 1991, 1992, 1993, 1994, 1995, 1996,...
    ## $ access_cft_tot            <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, "...
    ## $ access_electricity_tot    <chr> "100", "100", "100", "100", "100", "100",...
    ## $ ren_electricity_output    <chr> "14898", "16590", "16019", "17220", "1704...
    ## $ share_re_in_electricity   <chr> "9.656030644", "10.59820105", "10.0668652...
    ## $ re_consumption            <chr> "176729.7", "181011.2", "166746.4", "1978...
    ## $ total_electricity_output  <chr> "154287", "156536", "159126", "163236", "...
    ## $ share_total_re_in_TEFC    <chr> "8.009577159", "8.24547226", "7.516470972...
    ## $ total_final_energy_consum <chr> "2206479.774", "2195279.958", "2218413.41...
    ## $ primary_energy_intensity  <chr> "7.416865313", "7.341423042", "7.44872603...

``` r
dim(se_clean)
```

    ## [1] 270  11

``` r
#tidy up the second data set

esg_clean <- esg %>%
  #get rid of unnecessary or redundant variable
  select(-Country_Code, -Series_Code) %>%
  #tidy up the year variable
  pivot_longer(cols=contains('YR'), names_to = "year", values_to = "value") %>%
  separate(year, into=c("year_num", "year_code"), sep="X|\\..|\\.") %>%
  select(-year_num)%>%
  #rename some variable to common variable
  rename("year" = year_code, "country"= ï..Country_Name)

# tidy up the rest of the indicator variables
esg_clean <- esg_clean %>%
  # separate the column series_name to get rid of unit
  separate(Series_Name, into=c("indicator","Unit"), sep="\\(|\\)") %>%
  select(-Unit)%>%
  # pivot wider so that each indicator is a unique variable
  pivot_wider(names_from=indicator, values_from= value) %>%
  #to match up the year between 1990 and 2016
  filter(between(year, 1990, 2016))%>%
  # delete any variables with too many NA or no data
  select(-'Cooling_Degree_Days ', -'Heat_Index_35 ', -'Mean_Drought_Index ', -'Unmet_need_for_contraception ') %>%
  # have all non-numerical values to NA other than country variable
  mutate_all(na_if, "..")
  
# combine variables that are technically same
esg_clean <- esg_clean %>%
  unite('Annual_freshwater_withdrawals_total', 'Annual_freshwater_withdrawals_total ',
        'Annual_freshwater_withdrawals _total ', sep = "", na.rm=T) %>%
  unite('Agriculture_forestry_and_fisihing_value_added', 'Agriculture_forestry_and_fishing_value_added ',
        'Agriculture _forestry _and_fishing _value_added ', sep="", na.rm=T)%>%
  unite('Droughts_floods_extreme_temperatures', 'Droughts_floods_extreme_temperatures ',
        'Droughts _floods _extreme_temperatures ', sep="", na.rm=T) %>%
  unite('Energy_imports_net', 'Energy_imports_net ', 'Energy_imports _net ', sep="", na.rm=T) %>%
  unite('Fertility_rate_tot', 'Fertility_rate_total ', 'Fertility_rate _total ', sep="", na.rm=T) %>%
  unite('Research_development_expenditure', 'Research_and_development_expenditure ',
        'research_and_development_expenditure ', sep="", na.rm=T)

esg_clean <- esg_clean %>%
  mutate_all(na_if, "")

#to check %NA of each variable 
map(esg_clean, ~mean(is.na(.)))
```

    ## $country
    ## [1] 0
    ## 
    ## $year
    ## [1] 0
    ## 
    ## $`natural_resources_depletion `
    ## [1] 0
    ## 
    ## $`net_forest_depletion `
    ## [1] 0
    ## 
    ## $Annual_freshwater_withdrawals_total
    ## [1] 0.8814815
    ## 
    ## $`Agricultural_land `
    ## [1] 0
    ## 
    ## $Agriculture_forestry_and_fisihing_value_added
    ## [1] 0.0962963
    ## 
    ## $`CO2_emissions `
    ## [1] 0.007407407
    ## 
    ## $Control_of_Corruption_Estimate
    ## [1] 0.4
    ## 
    ## $Droughts_floods_extreme_temperatures
    ## [1] 0.9703704
    ## 
    ## $`Electricity_production_from_coal_sources `
    ## [1] 0.03703704
    ## 
    ## $Energy_imports_net
    ## [1] 0.04444444
    ## 
    ## $`Energy_use `
    ## [1] 0.04814815
    ## 
    ## $Fertility_rate_tot
    ## [1] 0
    ## 
    ## $`Food_production_index `
    ## [1] 0.007407407
    ## 
    ## $`Forest_area `
    ## [1] 0
    ## 
    ## $`GDP_growth `
    ## [1] 0
    ## 
    ## $`Fossil_fuel_energy_consumption `
    ## [1] 0.04444444
    ## 
    ## $`GHG_net_emissions/removals_by_LUCF `
    ## [1] 0.5481481
    ## 
    ## $`Government_expenditure_on_education _total `
    ## [1] 0.4481481
    ## 
    ## $`Individuals_using_the_Internet `
    ## [1] 0
    ## 
    ## $`Income_share_held_by_lowest_20%`
    ## [1] 0.6481481
    ## 
    ## $`Life_expectancy_at_birth _total `
    ## [1] 0
    ## 
    ## $`Literacy_rate _adult_total `
    ## [1] 0.762963
    ## 
    ## $`Methane_emissions `
    ## [1] 0.1481481
    ## 
    ## $`Mortality_rate _under-5 `
    ## [1] 0
    ## 
    ## $Net_migration
    ## [1] 0.8148148
    ## 
    ## $`Nitrous_oxide_emissions `
    ## [1] 0.1481481
    ## 
    ## $`People_using_safely_managed_drinking_water_services `
    ## [1] 0.5222222
    ## 
    ## $`People_using_safely_managed_sanitation_services `
    ## [1] 0.4555556
    ## 
    ## $`PM2.5_air_pollution _mean_annual_exposure `
    ## [1] 0.5925926
    ## 
    ## $`Population_density `
    ## [1] 0
    ## 
    ## $`Prevalence_of_overweight `
    ## [1] 0
    ## 
    ## $`Prevalence_of_undernourishment `
    ## [1] 0.4666667
    ## 
    ## $`Proportion_of_seats_held_by_women_in_national_parliaments `
    ## [1] 0.2666667
    ## 
    ## $`Ratio_of_female_to_male_labor_force_participation_rate `
    ## [1] 0
    ## 
    ## $Research_development_expenditure
    ## [1] 0.2851852
    ## 
    ## $`School_enrollment _primary `
    ## [1] 0.2148148
    ## 
    ## $`Unemployment _total `
    ## [1] 0.03703704

``` r
#get rid of variables with more than 30% NA or any insignificant variables
esg_clean <-  esg_clean %>%
  select(-Annual_freshwater_withdrawals_total, -Droughts_floods_extreme_temperatures,
         -`Literacy_rate _adult_total `, -Net_migration, -`Prevalence_of_undernourishment `,
         - `GHG_net_emissions/removals_by_LUCF `,-`Government_expenditure_on_education _total `,
         - `Income_share_held_by_lowest_20%`, -`People_using_safely_managed_drinking_water_services `,
         - `People_using_safely_managed_sanitation_services `,-`PM2.5_air_pollution _mean_annual_exposure `)

#check esg data
glimpse (esg_clean)
```

    ## Rows: 270
    ## Columns: 28
    ## $ country                                                      <chr> "Austr...
    ## $ year                                                         <chr> "1990"...
    ## $ `natural_resources_depletion `                               <chr> "1.986...
    ## $ `net_forest_depletion `                                      <chr> "0.179...
    ## $ `Agricultural_land `                                         <chr> "60.46...
    ## $ Agriculture_forestry_and_fisihing_value_added                <chr> "4.209...
    ## $ `CO2_emissions `                                             <chr> "15.45...
    ## $ Control_of_Corruption_Estimate                               <chr> NA, NA...
    ## $ `Electricity_production_from_coal_sources `                  <chr> "78.73...
    ## $ Energy_imports_net                                           <chr> "-82.3...
    ## $ `Energy_use `                                                <chr> "5061....
    ## $ Fertility_rate_tot                                           <chr> "1.902...
    ## $ `Food_production_index `                                     <chr> "69.98...
    ## $ `Forest_area `                                               <chr> "16.73...
    ## $ `GDP_growth `                                                <chr> "3.570...
    ## $ `Fossil_fuel_energy_consumption `                            <chr> "93.91...
    ## $ `Individuals_using_the_Internet `                            <chr> "0.585...
    ## $ `Life_expectancy_at_birth _total `                           <chr> "76.99...
    ## $ `Methane_emissions `                                         <chr> "6.747...
    ## $ `Mortality_rate _under-5 `                                   <chr> "9.2",...
    ## $ `Nitrous_oxide_emissions `                                   <chr> "3.685...
    ## $ `Population_density `                                        <chr> "2.221...
    ## $ `Prevalence_of_overweight `                                  <chr> "50.3"...
    ## $ `Proportion_of_seats_held_by_women_in_national_parliaments ` <chr> NA, NA...
    ## $ `Ratio_of_female_to_male_labor_force_participation_rate `    <chr> "69.02...
    ## $ Research_development_expenditure                             <chr> NA, NA...
    ## $ `School_enrollment _primary `                                <chr> "106.3...
    ## $ `Unemployment _total `                                       <chr> NA, "9...

``` r
dim(esg_clean)
```

    ## [1] 270  28

*After tidying the data, the first data set ‘se’ has 270 rows and 11
columns while the second data set ‘esg’ has 270 rows and 28 columns.*

### Step 3: Join or Merge two datasets as one

``` r
#combine both data by country and year
sesg <- merge(se_clean, esg_clean, by=c("country", "year"))

sesg <- sesg %>%
  # change numerical variable to numeric from character
  mutate_at (vars(-country),as.numeric) %>%
  #rename to shorten for convenience
    rename("acc_cft_t" = access_cft_tot,"acc_elct_t"= access_electricity_tot, "re_elect_out"=ren_electricity_output,
         "re_consum"=re_consumption, "elect_out_t"= total_electricity_output, "re_elect_prcnt"=share_re_in_electricity,
         "e_consum_t"=total_final_energy_consum, "re_consum_prcnt" = share_total_re_in_TEFC,
         "e_int_prim" = primary_energy_intensity, "nat_res_depl"=`natural_resources_depletion `,
         "net_for_depl"=`net_forest_depletion `, "agri_land"=`Agricultural_land `, 
         "agri_for_fish_val" = Agriculture_forestry_and_fisihing_value_added, "ctrl_corrupt"=Control_of_Corruption_Estimate,
         "elect_prd_coal_prcnt" =`Electricity_production_from_coal_sources `, "e_import_net" = Energy_imports_net,
         "e_use"=`Energy_use `, "fertil_r_t" = Fertility_rate_tot, "food_prd" = `Food_production_index `, 
         "forest_a" = `Forest_area `, "GDP_r"=`GDP_growth `, "fssil_e_consum_prcnt" = `Fossil_fuel_energy_consumption `,
         "Intrnt_prcnt"=`Individuals_using_the_Internet `, "life_expct" = `Life_expectancy_at_birth _total `,
         "mortality_r_5-" = `Mortality_rate _under-5 `, "pop_dens"= `Population_density `, 
         "prev_ovrweight" = `Prevalence_of_overweight `, "rd_expend" = Research_development_expenditure,
         "women_legis_prcnt"=`Proportion_of_seats_held_by_women_in_national_parliaments `,  
         "ftom_laborF_r"= `Ratio_of_female_to_male_labor_force_participation_rate `,
         "prim_schl_enrll"= `School_enrollment _primary `, "unemply_t" = `Unemployment _total `)

#check the new combined data
head(sesg)
```

    ##     country year acc_cft_t acc_elct_t re_elect_out re_elect_prcnt re_consum
    ## 1 Australia 1990        NA        100        14898       9.656031  176729.7
    ## 2 Australia 1991        NA        100        16590      10.598201  181011.2
    ##   elect_out_t re_consum_prcnt e_consum_t e_int_prim nat_res_depl net_for_depl
    ## 1      154287        8.009577    2206480   7.416865     1.986605    0.1797516
    ## 2      156536        8.245472    2195280   7.341423     1.165256    0.0568211
    ##   agri_land agri_for_fish_val CO2_emissions  ctrl_corrupt elect_prd_coal_prcnt
    ## 1  60.46119          4.209132       15.45288           NA             78.73508
    ## 2  60.26502          3.182262       15.12797           NA             80.35085
    ##   e_import_net    e_use fertil_r_t food_prd forest_a      GDP_r
    ## 1    -82.37047 5061.508      1.902    69.98  16.7321  3.5709981
    ## 2    -96.08562 4927.782      1.849    69.26  16.7360 -0.3978177
    ##   fssil_e_consum_prcnt Intrnt_prcnt life_expct Methane_emissions 
    ## 1             93.91129     0.585095   76.99463           6.747690
    ## 2             93.68872     1.097200   77.27561           6.977609
    ##   mortality_r_5- Nitrous_oxide_emissions  pop_dens prev_ovrweight
    ## 1            9.2                 3.685500 2.221353           50.3
    ## 2            8.7                 3.928233 2.249847           50.9
    ##   women_legis_prcnt ftom_laborF_r rd_expend prim_schl_enrll unemply_t
    ## 1                NA      69.02971        NA        106.3717        NA
    ## 2                NA      69.54226        NA        106.0968     9.579
    ##  [ reached 'max' / getOption("max.print") -- omitted 4 rows ]

``` r
dim(sesg)
```

    ## [1] 270  37

*After combining two datasets, there are 270 rows and 37 columns in
total. *

### Step 4: Create summary statistics

``` r
# 6 core dplyr functions (filter, select, arrange, group_by, mutate, summarize)

# new numerical variable summary
sesg %>% 
  filter (country != "World", year==2014) %>%
  mutate(ren_consumToout = re_consum*0.2777778/re_elect_out, na.rm=T) %>%
  select(country, ren_consumToout, GDP_r) %>%
  arrange(desc(GDP_r))%>%
  summarize(min_renR = min(ren_consumToout), mean_renR = mean(ren_consumToout),
            median_renR = median(ren_consumToout), max_renR = max(ren_consumToout),
            var_renR = var(ren_consumToout), sd_renR = sd(ren_consumToout))
```

    ##    min_renR mean_renR median_renR max_renR var_renR sd_renR
    ## 1 0.9398817  3.457648    2.213333 14.03557 17.03493 4.12734

``` r
#categorical variable summary + numerical variable
sesg%>%
  filter(country != "World") %>%
  mutate(GDP_share = case_when(country %in% c("United States","Japan","Italy") ~"high",
                               country %in% c("Korea, Rep.","Australia","Spain") ~ "mid",
                               country %in% c("Greece","Thailand", "Singapore") ~ "low")) %>%
  group_by(GDP_share)%>%
  summarize(avg_diff_bt_fuel_re_consum_prcnt = mean(fssil_e_consum_prcnt-re_consum_prcnt,na.rm=T),
            avg_fssil_e_consum = mean(fssil_e_consum_prcnt, na.rm=T),
            avg_re_consum_prcnt = mean(re_consum_prcnt, na.rm=T)) %>%
  arrange(desc(avg_diff_bt_fuel_re_consum_prcnt))
```

    ## # A tibble: 3 x 4
    ##   GDP_share avg_diff_bt_fuel_re_consum_pr~ avg_fssil_e_consum avg_re_consum_prc~
    ##   <chr>                              <dbl>              <dbl>              <dbl>
    ## 1 high                                80.0               86.1               6.11
    ## 2 mid                                 78.9               85.5               6.58
    ## 3 low                                 78.4               89.4              11.0

``` r
#Overall summary of All numerical variables
sesg_num <- sesg %>%
  select_if(is.numeric) %>%
  # deselect non-numerically significant variables
  select(-year,-`Methane_emissions `,-`CO2_emissions `, -`Nitrous_oxide_emissions `, -re_consum)

sesg_sd <- sesg_num %>%
  summarize_all(sd,na.rm=T)%>%
  pivot_longer(cols=c(acc_cft_t:unemply_t), names_to="Variables", values_to="sd")
sesg_sd <-data.frame(sesg_sd)

library(stringr)
remove_all_ws<- function(string){
    return(gsub(" ", "", str_squish(string)))
}

summary_table <-data.frame(summary(sesg_num))
summary_table <- summary_table %>%
  select(-Var1) %>%
  rename("Variables" = Var2)%>%
  mutate_if(is.character, remove_all_ws)%>%
  separate(Freq, into=c("indicator","stats"), sep=":") %>%
  pivot_wider(names_from = indicator, values_from = stats)%>%
  select(-"NA") %>%
  mutate_at("NA's",replace_na, 0)

stat_summary <- merge(summary_table, sesg_sd, by="Variables")
library(kableExtra)
stat_summary %>%
  kbl() %>%
  kable_styling()
```

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Variables
</th>
<th style="text-align:left;">
Min.
</th>
<th style="text-align:left;">
1stQu.
</th>
<th style="text-align:left;">
Median
</th>
<th style="text-align:left;">
Mean
</th>
<th style="text-align:left;">
3rdQu.
</th>
<th style="text-align:left;">
Max.
</th>
<th style="text-align:left;">
NA’s
</th>
<th style="text-align:right;">
sd
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
acc\_cft\_t
</td>
<td style="text-align:left;">
68.04
</td>
<td style="text-align:left;">
96.57
</td>
<td style="text-align:left;">
100.00
</td>
<td style="text-align:left;">
95.60
</td>
<td style="text-align:left;">
100.00
</td>
<td style="text-align:left;">
100.00
</td>
<td style="text-align:left;">
117
</td>
<td style="text-align:right;">
8.972143e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
acc\_elct\_t
</td>
<td style="text-align:left;">
75.90
</td>
<td style="text-align:left;">
100.00
</td>
<td style="text-align:left;">
100.00
</td>
<td style="text-align:left;">
98.86
</td>
<td style="text-align:left;">
100.00
</td>
<td style="text-align:left;">
100.00
</td>
<td style="text-align:left;">
32
</td>
<td style="text-align:right;">
4.228216e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
agri\_for\_fish\_val
</td>
<td style="text-align:left;">
0.03162
</td>
<td style="text-align:left;">
1.37118
</td>
<td style="text-align:left;">
2.76896
</td>
<td style="text-align:left;">
3.38322
</td>
<td style="text-align:left;">
4.16509
</td>
<td style="text-align:left;">
12.64983
</td>
<td style="text-align:left;">
26
</td>
<td style="text-align:right;">
2.807997e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
agri\_land
</td>
<td style="text-align:left;">
0.9309
</td>
<td style="text-align:left;">
19.6932
</td>
<td style="text-align:left;">
43.2774
</td>
<td style="text-align:left;">
38.5930
</td>
<td style="text-align:left;">
54.0818
</td>
<td style="text-align:left;">
71.5438
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
1.984262e+01
</td>
</tr>
<tr>
<td style="text-align:left;">
ctrl\_corrupt
</td>
<td style="text-align:left;">
-0.4934
</td>
<td style="text-align:left;">
0.3492
</td>
<td style="text-align:left;">
1.1039
</td>
<td style="text-align:left;">
0.9692
</td>
<td style="text-align:left;">
1.6572
</td>
<td style="text-align:left;">
2.3256
</td>
<td style="text-align:left;">
108
</td>
<td style="text-align:right;">
8.247650e-01
</td>
</tr>
<tr>
<td style="text-align:left;">
e\_consum\_t
</td>
<td style="text-align:left;">
129565
</td>
<td style="text-align:left;">
1803158
</td>
<td style="text-align:left;">
3168827
</td>
<td style="text-align:left;">
9474584
</td>
<td style="text-align:left;">
5283889
</td>
<td style="text-align:left;">
59567475
</td>
<td style="text-align:left;">
36
</td>
<td style="text-align:right;">
1.668162e+07
</td>
</tr>
<tr>
<td style="text-align:left;">
e\_import\_net
</td>
<td style="text-align:left;">
-192.02
</td>
<td style="text-align:left;">
21.52
</td>
<td style="text-align:left;">
65.95
</td>
<td style="text-align:left;">
41.28
</td>
<td style="text-align:left;">
81.70
</td>
<td style="text-align:left;">
99.39
</td>
<td style="text-align:left;">
12
</td>
<td style="text-align:right;">
6.407250e+01
</td>
</tr>
<tr>
<td style="text-align:left;">
e\_int\_prim
</td>
<td style="text-align:left;">
2.395
</td>
<td style="text-align:left;">
3.839
</td>
<td style="text-align:left;">
4.991
</td>
<td style="text-align:left;">
5.134
</td>
<td style="text-align:left;">
6.251
</td>
<td style="text-align:left;">
8.743
</td>
<td style="text-align:left;">
36
</td>
<td style="text-align:right;">
1.547765e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
e\_use
</td>
<td style="text-align:left;">
741.6
</td>
<td style="text-align:left;">
2319.0
</td>
<td style="text-align:left;">
3180.0
</td>
<td style="text-align:left;">
3724.3
</td>
<td style="text-align:left;">
5089.8
</td>
<td style="text-align:left;">
8056.9
</td>
<td style="text-align:left;">
13
</td>
<td style="text-align:right;">
1.875527e+03
</td>
</tr>
<tr>
<td style="text-align:left;">
elect\_out\_t
</td>
<td style="text-align:left;">
15714
</td>
<td style="text-align:left;">
89891
</td>
<td style="text-align:left;">
228544
</td>
<td style="text-align:left;">
692962
</td>
<td style="text-align:left;">
449741
</td>
<td style="text-align:left;">
4354363
</td>
<td style="text-align:left;">
36
</td>
<td style="text-align:right;">
1.194243e+06
</td>
</tr>
<tr>
<td style="text-align:left;">
elect\_prd\_coal\_prcnt
</td>
<td style="text-align:left;">
0.00
</td>
<td style="text-align:left;">
16.76
</td>
<td style="text-align:left;">
34.30
</td>
<td style="text-align:left;">
34.68
</td>
<td style="text-align:left;">
50.41
</td>
<td style="text-align:left;">
84.00
</td>
<td style="text-align:left;">
10
</td>
<td style="text-align:right;">
2.259689e+01
</td>
</tr>
<tr>
<td style="text-align:left;">
fertil\_r\_t
</td>
<td style="text-align:left;">
1.076
</td>
<td style="text-align:left;">
1.300
</td>
<td style="text-align:left;">
1.464
</td>
<td style="text-align:left;">
1.633
</td>
<td style="text-align:left;">
1.857
</td>
<td style="text-align:left;">
3.248
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
4.467570e-01
</td>
</tr>
<tr>
<td style="text-align:left;">
food\_prd
</td>
<td style="text-align:left;">
67.08
</td>
<td style="text-align:left;">
91.89
</td>
<td style="text-align:left;">
99.16
</td>
<td style="text-align:left;">
102.81
</td>
<td style="text-align:left;">
104.34
</td>
<td style="text-align:left;">
490.79
</td>
<td style="text-align:left;">
2
</td>
<td style="text-align:right;">
3.795679e+01
</td>
</tr>
<tr>
<td style="text-align:left;">
forest\_a
</td>
<td style="text-align:left;">
16.04
</td>
<td style="text-align:left;">
27.27
</td>
<td style="text-align:left;">
31.30
</td>
<td style="text-align:left;">
36.07
</td>
<td style="text-align:left;">
34.35
</td>
<td style="text-align:left;">
68.48
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
1.609751e+01
</td>
</tr>
<tr>
<td style="text-align:left;">
fssil\_e\_consum\_prcnt
</td>
<td style="text-align:left;">
63.84
</td>
<td style="text-align:left;">
80.79
</td>
<td style="text-align:left;">
84.40
</td>
<td style="text-align:left;">
86.31
</td>
<td style="text-align:left;">
93.46
</td>
<td style="text-align:left;">
99.39
</td>
<td style="text-align:left;">
12
</td>
<td style="text-align:right;">
7.143750e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
ftom\_laborF\_r
</td>
<td style="text-align:left;">
50.11
</td>
<td style="text-align:left;">
64.39
</td>
<td style="text-align:left;">
67.69
</td>
<td style="text-align:left;">
69.48
</td>
<td style="text-align:left;">
77.90
</td>
<td style="text-align:left;">
83.89
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
8.233145e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
GDP\_r
</td>
<td style="text-align:left;">
-9.132
</td>
<td style="text-align:left;">
1.419
</td>
<td style="text-align:left;">
2.897
</td>
<td style="text-align:left;">
2.928
</td>
<td style="text-align:left;">
4.319
</td>
<td style="text-align:left;">
14.526
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
3.282824e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
Intrnt\_prcnt
</td>
<td style="text-align:left;">
0.00
</td>
<td style="text-align:left;">
2.51
</td>
<td style="text-align:left;">
30.04
</td>
<td style="text-align:left;">
35.04
</td>
<td style="text-align:left;">
65.31
</td>
<td style="text-align:left;">
93.18
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
3.068711e+01
</td>
</tr>
<tr>
<td style="text-align:left;">
life\_expct
</td>
<td style="text-align:left;">
65.43
</td>
<td style="text-align:left;">
75.63
</td>
<td style="text-align:left;">
78.50
</td>
<td style="text-align:left;">
77.50
</td>
<td style="text-align:left;">
80.81
</td>
<td style="text-align:left;">
83.98
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
4.381511e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
mortality\_r\_5-
</td>
<td style="text-align:left;">
2.70
</td>
<td style="text-align:left;">
4.20
</td>
<td style="text-align:left;">
6.25
</td>
<td style="text-align:left;">
13.50
</td>
<td style="text-align:left;">
9.70
</td>
<td style="text-align:left;">
93.00
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
1.966756e+01
</td>
</tr>
<tr>
<td style="text-align:left;">
nat\_res\_depl
</td>
<td style="text-align:left;">
0.000000
</td>
<td style="text-align:left;">
0.005991
</td>
<td style="text-align:left;">
0.058201
</td>
<td style="text-align:left;">
0.549862
</td>
<td style="text-align:left;">
0.715073
</td>
<td style="text-align:left;">
4.221239
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
8.819440e-01
</td>
</tr>
<tr>
<td style="text-align:left;">
net\_for\_depl
</td>
<td style="text-align:left;">
0.000000
</td>
<td style="text-align:left;">
0.000000
</td>
<td style="text-align:left;">
0.000000
</td>
<td style="text-align:left;">
0.047951
</td>
<td style="text-align:left;">
0.002403
</td>
<td style="text-align:left;">
0.679568
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
1.317750e-01
</td>
</tr>
<tr>
<td style="text-align:left;">
pop\_dens
</td>
<td style="text-align:left;">
2.221
</td>
<td style="text-align:left;">
50.025
</td>
<td style="text-align:left;">
102.107
</td>
<td style="text-align:left;">
767.482
</td>
<td style="text-align:left;">
348.811
</td>
<td style="text-align:left;">
7908.721
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
1.867608e+03
</td>
</tr>
<tr>
<td style="text-align:left;">
prev\_ovrweight
</td>
<td style="text-align:left;">
14.20
</td>
<td style="text-align:left;">
26.70
</td>
<td style="text-align:left;">
42.80
</td>
<td style="text-align:left;">
41.40
</td>
<td style="text-align:left;">
56.48
</td>
<td style="text-align:left;">
67.90
</td>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
1.612634e+01
</td>
</tr>
<tr>
<td style="text-align:left;">
prim\_schl\_enrll
</td>
<td style="text-align:left;">
90.27
</td>
<td style="text-align:left;">
98.93
</td>
<td style="text-align:left;">
101.50
</td>
<td style="text-align:left;">
101.13
</td>
<td style="text-align:left;">
103.61
</td>
<td style="text-align:left;">
108.19
</td>
<td style="text-align:left;">
58
</td>
<td style="text-align:right;">
3.373464e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
rd\_expend
</td>
<td style="text-align:left;">
0.1021
</td>
<td style="text-align:left;">
1.0385
</td>
<td style="text-align:left;">
1.9841
</td>
<td style="text-align:left;">
1.8317
</td>
<td style="text-align:left;">
2.5576
</td>
<td style="text-align:left;">
4.2887
</td>
<td style="text-align:left;">
77
</td>
<td style="text-align:right;">
9.800110e-01
</td>
</tr>
<tr>
<td style="text-align:left;">
re\_consum\_prcnt
</td>
<td style="text-align:left;">
0.1948
</td>
<td style="text-align:left;">
3.8314
</td>
<td style="text-align:left;">
6.8494
</td>
<td style="text-align:left;">
7.9060
</td>
<td style="text-align:left;">
8.9894
</td>
<td style="text-align:left;">
33.6391
</td>
<td style="text-align:left;">
36
</td>
<td style="text-align:right;">
6.837544e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
re\_elect\_out
</td>
<td style="text-align:left;">
85
</td>
<td style="text-align:left;">
4589
</td>
<td style="text-align:left;">
18382
</td>
<td style="text-align:left;">
73568
</td>
<td style="text-align:left;">
91048
</td>
<td style="text-align:left;">
568439
</td>
<td style="text-align:left;">
36
</td>
<td style="text-align:right;">
1.241248e+05
</td>
</tr>
<tr>
<td style="text-align:left;">
re\_elect\_prcnt
</td>
<td style="text-align:left;">
0.5409
</td>
<td style="text-align:left;">
5.9661
</td>
<td style="text-align:left;">
9.1400
</td>
<td style="text-align:left;">
10.6644
</td>
<td style="text-align:left;">
13.7306
</td>
<td style="text-align:left;">
43.3916
</td>
<td style="text-align:left;">
36
</td>
<td style="text-align:right;">
8.237212e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
unemply\_t
</td>
<td style="text-align:left;">
0.489
</td>
<td style="text-align:left;">
3.700
</td>
<td style="text-align:left;">
5.650
</td>
<td style="text-align:left;">
7.154
</td>
<td style="text-align:left;">
9.083
</td>
<td style="text-align:left;">
27.466
</td>
<td style="text-align:left;">
10
</td>
<td style="text-align:right;">
5.493492e+00
</td>
</tr>
<tr>
<td style="text-align:left;">
women\_legis\_prcnt
</td>
<td style="text-align:left;">
3.01
</td>
<td style="text-align:left;">
10.66
</td>
<td style="text-align:left;">
15.80
</td>
<td style="text-align:left;">
16.97
</td>
<td style="text-align:left;">
22.75
</td>
<td style="text-align:left;">
41.14
</td>
<td style="text-align:left;">
72
</td>
<td style="text-align:right;">
8.664581e+00
</td>
</tr>
</tbody>
</table>

``` r
# correlation across numerical variables
sesg_cor <- data.frame(cor(sesg_num, use = "pairwise.complete.obs"))

sesg_cor %>%
  mutate_if(is.numeric, ~cell_spec(.x,"html", color = ifelse(.x < 0, "red"," black")))%>%
  kable(format = "html", escape = FALSE) %>%
  kable_styling("striped", full_width = FALSE)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
acc\_cft\_t
</th>
<th style="text-align:left;">
acc\_elct\_t
</th>
<th style="text-align:left;">
re\_elect\_out
</th>
<th style="text-align:left;">
re\_elect\_prcnt
</th>
<th style="text-align:left;">
elect\_out\_t
</th>
<th style="text-align:left;">
re\_consum\_prcnt
</th>
<th style="text-align:left;">
e\_consum\_t
</th>
<th style="text-align:left;">
e\_int\_prim
</th>
<th style="text-align:left;">
nat\_res\_depl
</th>
<th style="text-align:left;">
net\_for\_depl
</th>
<th style="text-align:left;">
agri\_land
</th>
<th style="text-align:left;">
agri\_for\_fish\_val
</th>
<th style="text-align:left;">
ctrl\_corrupt
</th>
<th style="text-align:left;">
elect\_prd\_coal\_prcnt
</th>
<th style="text-align:left;">
e\_import\_net
</th>
<th style="text-align:left;">
e\_use
</th>
<th style="text-align:left;">
fertil\_r\_t
</th>
<th style="text-align:left;">
food\_prd
</th>
<th style="text-align:left;">
forest\_a
</th>
<th style="text-align:left;">
GDP\_r
</th>
<th style="text-align:left;">
fssil\_e\_consum\_prcnt
</th>
<th style="text-align:left;">
Intrnt\_prcnt
</th>
<th style="text-align:left;">
life\_expct
</th>
<th style="text-align:left;">
mortality\_r\_5.
</th>
<th style="text-align:left;">
pop\_dens
</th>
<th style="text-align:left;">
prev\_ovrweight
</th>
<th style="text-align:left;">
women\_legis\_prcnt
</th>
<th style="text-align:left;">
ftom\_laborF\_r
</th>
<th style="text-align:left;">
rd\_expend
</th>
<th style="text-align:left;">
prim\_schl\_enrll
</th>
<th style="text-align:left;">
unemply\_t
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
acc\_cft\_t
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.676098437185345</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.268110070857824</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.196382313164569</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.236688196493663</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.711281462800956</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.215888750976517</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.135784816536082</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.460933564948545</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.92962742427806</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.120627051076005</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.931011698841653</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.657918333543023</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.114805262806973</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0374316854003469</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.567606938173647</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0355539964846596</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.32740288450848</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0817505418968662</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.166473720089183</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.262403001697567</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.617252504648898</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.802283397280409</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.869106523536839</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.177407761894142</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.391111127983294</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.386911549572759</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.256406960003933</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.54734347214046</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.46732093852829</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.289033054625551</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
acc\_elct\_t
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.676098437185345</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.152087860191029</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.109846935913764</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.142197148634936</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.675774680720879</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.128790799901396</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0213843678256343</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.139507162896302</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.553658237655379</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.017610604009345</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.657464522474893</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.343859491979175</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.159474799965291</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.01728690116718</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.431562773105299</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.302429550510051</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.130533263589369</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0890887977543036</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.222612437272361</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.457759688753226</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.301506212658779</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.666550627077389</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.909846852231151</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.100892264290126</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.413438437545353</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.253619220630997</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.298382763685522</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.38784018407508</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.29469300445278</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.260539717326102</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
re\_elect\_out
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.268110070857824</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.152087860191029</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.164592779287561</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.9677224879486</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0808605434661192</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.963947376212867</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.303436055098841</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0588343241000773</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.175651586857829</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0773933363916001</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.310441559622219</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.218012637224748</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.132222014368413</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.085520536110743</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.628411758467528</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.507812371968007</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0656281937355938</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0648247431657104</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.163769370499371</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.176401542050732</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.213621225078217</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0489022081907251</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0538746187969495</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.224614993551188</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.376173501843618</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0291790430056672</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.375917889124497</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.363521627006681</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.13424137773124</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.00372401593672054</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
re\_elect\_prcnt
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.196382313164569</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.109846935913764</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.164592779287561</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.00351006776533308</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.375424951498652</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0065538761475256</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.457674731130512</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0996557297822727</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.136543296665193</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.517803400354684</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0411231992052354</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.252231107345595</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0442091267663841</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0113592631060325</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.275513662475269</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.161066723996859</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.187383080558848</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.164815307705812</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.464414027162415</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.333315954931338</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0687356472243777</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.378766214759684</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.168801612696399</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.420058647797614</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.552029095360425</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.559987076147214</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0696576750572546</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.34943328851831</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.278403677714419</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.712626651921219</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
elect\_out\_t
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.236688196493663</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.142197148634936</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.9677224879486</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.00351006776533308</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.148171354113927</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.995859800914973</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.421130589686944</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0353922311958849</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.160949482395864</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0148781466044219</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.301484942909339</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.242891038975912</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.184606678261023</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.09605300521189</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.69828063263482</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.548345059638101</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.063866780826261</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.118978587626624</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.109048362830512</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.151034494556277</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.216760933246566</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0123226783355014</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0268186617229654</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.206628605949836</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.299933817919028</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0874163779343658</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.393482379625481</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.449241597158243</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0976522771441432</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.11302545248307</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
re\_consum\_prcnt
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.711281462800956</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.675774680720879</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0808605434661192</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.375424951498652</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.148171354113927</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.130917777688931</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.198927838544267</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.42390109162448</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.734865896884391</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.440905619517138</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.767061278020762</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.639081049653718</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0234310352183946</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.182059889290373</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.554166744610909</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.223538869512662</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.178492269641863</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.292882505670447</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.122740181445964</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.563718096141614</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.174264275442267</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.390920386640145</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.669229293063522</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.407366025312213</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0263459015089395</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.160155109312843</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.409035805031644</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.67149719580827</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.222237991718121</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.125535423968409</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
e\_consum\_t
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.215888750976517</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.128790799901396</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.963947376212867</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0065538761475256</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.995859800914973</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.130917777688931</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.432271994760837</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0228833298692753</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.144930413423854</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0510367388477191</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.273709262881283</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.223187844568386</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.186862951536715</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.10398076038999</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.693336210604496</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.569513327843077</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0712277575964062</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0714588784737458</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0951048757048782</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.143080472933911</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.171711817539495</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0562566107675242</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.00364348228794137</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.209306588299947</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.323581884411744</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0787087910462828</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.391145406510823</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.397176304904479</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.101051277110007</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.104236484229165</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
e\_int\_prim
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.135784816536082</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0213843678256343</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.303436055098841</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.457674731130512</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.421130589686944</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.198927838544267</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.432271994760837</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.261194669993195</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0391663909352348</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0875822161329208</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.131676175827936</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0154988527714248</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.431361100597531</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.380306644826843</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.525303437271204</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.557671355794801</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0530782851056231</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.275450903543946</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.252419548228465</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0795139492924021</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0839196081435645</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.399536240919544</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.199086953146786</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.276913566093664</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.128366226237115</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.348043968437877</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.314285290155828</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.430355671682105</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.185721429200036</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.400184783277498</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
nat\_res\_depl
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.460933564948545</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.139507162896302</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0588343241000773</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0996557297822727</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0353922311958849</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.42390109162448</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0228833298692753</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.261194669993195</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.505154437666334</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.238299408415328</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.393328682393689</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0208466034430866</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.355501178488992</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.734468909381798</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0131694928580211</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.458392649322474</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0327301981940342</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.389433524485464</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0417954859527303</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0323844716458287</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0336648217629174</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.268816289421771</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.25958361230325</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.238032082080708</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0717418306858045</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0943449182396803</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.497870693714257</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.206114521554322</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.158387927859014</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.285317056927301</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
net\_for\_depl
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.92962742427806</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.553658237655379</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.175651586857829</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.136543296665193</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.160949482395864</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.734865896884391</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.144930413423854</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0391663909352348</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.505154437666334</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0359091618530851</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.789774271102659</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.54088167987481</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.186811729410062</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0360124451681225</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.414431030107314</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.102842958502765</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0082781297217322</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.107955913798585</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.120366279209506</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.356237994010961</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.229783290362216</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.426036808136996</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.182818047457468</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.127187225778897</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.380211194690777</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.25535198419992</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.376961200290208</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.4730379054627</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.238881990912382</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.352017772892787</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
agri\_land
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.120627051076005</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.017610604009345</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0773933363916001</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.517803400354684</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0148781466044219</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.440905619517138</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0510367388477191</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0875822161329208</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.238299408415328</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0359091618530851</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.340022735254055</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.315068822322426</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.616433919645689</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.422824474122601</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.184145487733992</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0760159631490804</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.299772653383489</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.503202005459073</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.289074966688934</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.084810090347242</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.239693644025406</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0347763616916372</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0268489715651181</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.662262943139979</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.739226341026295</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.348825831207402</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0275045249217939</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.57951081141779</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0598142233166902</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.523054564025414</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
agri\_for\_fish\_val
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.931011698841653</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.657464522474893</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.310441559622219</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0411231992052354</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.301484942909339</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.767061278020762</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.273709262881283</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.131676175827936</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.393328682393689</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.789774271102659</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.340022735254055</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.695389462387315</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0695976795905822</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.112826325002511</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.677168388318208</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.203121932582299</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.197931010665068</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0751150475440272</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.157794751665377</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.4887432956254</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.525152448677007</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.636355917642155</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.402607273649067</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.416232662839221</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.298944635935298</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.235913297521621</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.178012588610091</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.609778022899023</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.416904859510096</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.163323169258899</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
ctrl\_corrupt
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.657918333543023</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.343859491979175</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.218012637224748</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.252231107345595</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.242891038975912</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.639081049653718</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.223187844568386</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0154988527714248</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0208466034430866</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.54088167987481</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.315068822322426</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.695389462387315</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0943083197039223</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.319061749660782</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.718117465796753</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.249711741240684</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0367953478461998</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.186228178016954</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.24496093157714</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.528341625549676</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.391077041411241</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.405829072151801</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.471035913769272</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.49528036972629</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.118649678663525</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.243036991555523</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.136103631878401</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.485620458238191</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.472476044722556</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.131978020778751</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
elect\_prd\_coal\_prcnt
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.114805262806973</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.159474799965291</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.132222014368413</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0442091267663841</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.184606678261023</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0234310352183946</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.186862951536715</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.431361100597531</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.355501178488992</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.186811729410062</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.616433919645689</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0695976795905822</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0943083197039223</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.709770438064467</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.24517758636693</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.255210601145701</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.260977805989028</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.22860325925576</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.14327571014466</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.138324200329282</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0344930345840161</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.00827238413716076</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0409379725489493</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.53165016789625</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.515013053687943</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0469891667404816</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.157685078564472</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.137186180096214</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0692539977445689</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.13552995619658</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
e\_import\_net
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0374316854003469</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.01728690116718</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.085520536110743</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0113592631060325</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.09605300521189</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.182059889290373</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.10398076038999</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.380306644826843</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.734468909381798</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0360124451681225</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.422824474122601</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.112826325002511</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.319061749660782</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.709770438064467</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.239996835974279</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.525827064773307</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.161708786976865</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.476423483421619</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0272116323752606</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.107969566153535</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0604931664486824</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.13860418260921</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.230736165469648</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.333391741236339</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.36450746459854</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.257991772249529</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.459880430395706</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0128991529541136</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.206329031669733</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0699765986915525</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
e\_use
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.567606938173647</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.431562773105299</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.628411758467528</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.275513662475269</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.69828063263482</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.554166744610909</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.693336210604496</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.525303437271204</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0131694928580211</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.414431030107314</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.184145487733992</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.677168388318208</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.718117465796753</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.24517758636693</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.239996835974279</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.00752565363605134</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0900821180562888</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0322932987998982</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0848626169369166</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.400680272625438</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.425994732684991</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.408842616251684</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.431433614453568</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.237686825228593</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.337425101544104</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0539849164005974</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.35488026054882</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.592565040661913</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.319006122009467</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.169569723406691</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
fertil\_r\_t
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0355539964846596</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.302429550510051</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.507812371968007</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.161066723996859</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.548345059638101</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.223538869512662</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.569513327843077</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.557671355794801</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.458392649322474</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.102842958502765</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0760159631490804</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.203121932582299</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.249711741240684</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.255210601145701</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.525827064773307</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.00752565363605134</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.044058193455846</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.252952817210183</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0706707615066381</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.222992196356184</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.242567109646563</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.734803053409229</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.839816179688733</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.214402049244923</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0591875075044087</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0163779324631047</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.279329344861605</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0933311838537072</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0280352813398128</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.267370698105437</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
food\_prd
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.32740288450848</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.130533263589369</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0656281937355938</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.187383080558848</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.063866780826261</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.178492269641863</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0712277575964062</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0530782851056231</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0327301981940342</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0082781297217322</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.299772653383489</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.197931010665068</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0367953478461998</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.260977805989028</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.161708786976865</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0900821180562888</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.044058193455846</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0568734514409134</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.18914894768274</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.265135959031231</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0266432762468709</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0412465029436439</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.134633813816973</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.32926261913496</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.120768845402592</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0542067023782268</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.086690415671757</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.024249926894486</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0402683029671573</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.166495888762004</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
forest\_a
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0817505418968662</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0890887977543036</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0648247431657104</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.164815307705812</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.118978587626624</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.292882505670447</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0714588784737458</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.275450903543946</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.389433524485464</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.107955913798585</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.503202005459073</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0751150475440272</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.186228178016954</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.22860325925576</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.476423483421619</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0322932987998982</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.252952817210183</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0568734514409134</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0178358080244934</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.35620683356003</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.169035655236923</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.133162624304524</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.121318299363482</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.183181230951596</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.523404056518167</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.402389511801002</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.166058951913307</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.598166827923329</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.021979751165858</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.227871368652409</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
GDP\_r
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.166473720089183</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.222612437272361</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.163769370499371</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.464414027162415</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.109048362830512</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.122740181445964</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0951048757048782</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.252419548228465</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0417954859527303</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.120366279209506</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.289074966688934</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.157794751665377</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.24496093157714</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.14327571014466</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0272116323752606</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0848626169369166</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0706707615066381</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.18914894768274</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0178358080244934</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0950329500032275</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.186113066829853</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.272106627027786</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0634569973418211</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.309369738565861</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.341350334274435</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0993484691757416</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0206146533458392</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0506752378108141</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0334677431547046</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.385975101516301</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
fssil\_e\_consum\_prcnt
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.262403001697567</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.457759688753226</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.176401542050732</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.333315954931338</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.151034494556277</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.563718096141614</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.143080472933911</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0795139492924021</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0323844716458287</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.356237994010961</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.084810090347242</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.4887432956254</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.528341625549676</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.138324200329282</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.107969566153535</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.400680272625438</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.222992196356184</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.265135959031231</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.35620683356003</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0950329500032275</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0733242068830326</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.358302466270167</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.383287850110793</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.507326615949291</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.22569795884425</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.139430283889934</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.201148798692923</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.00109131673492675</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.107554202168616</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.101603489492744</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
Intrnt\_prcnt
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.617252504648898</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.301506212658779</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.213621225078217</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0687356472243777</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.216760933246566</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.174264275442267</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.171711817539495</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0839196081435645</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0336648217629174</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.229783290362216</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.239693644025406</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.525152448677007</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.391077041411241</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0344930345840161</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0604931664486824</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.425994732684991</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.242567109646563</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0266432762468709</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.169035655236923</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.186113066829853</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0733242068830326</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.638521783489175</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.372658366905458</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.155861998904152</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.237169215399954</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.392218697132129</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.464248950467756</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.573796491276918</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.237427776087367</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0245272572908683</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
life\_expct
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.802283397280409</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.666550627077389</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0489022081907251</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.378766214759684</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0123226783355014</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.390920386640145</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0562566107675242</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.399536240919544</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.268816289421771</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.426036808136996</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0347763616916372</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.636355917642155</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.405829072151801</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.00827238413716076</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.13860418260921</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.408842616251684</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.734803053409229</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0412465029436439</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.133162624304524</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.272106627027786</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.358302466270167</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.638521783489175</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.841378650176199</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.165283350674773</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.409001529119572</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.338203276141583</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.00396107307025052</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.23309639455994</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.257156420621361</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.314072687202159</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
mortality\_r\_5-
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.869106523536839</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.909846852231151</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0538746187969495</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.168801612696399</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0268186617229654</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.669229293063522</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.00364348228794137</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.199086953146786</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.25958361230325</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.182818047457468</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0268489715651181</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.402607273649067</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.471035913769272</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0409379725489493</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.230736165469648</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.431433614453568</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.839816179688733</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.134633813816973</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.121318299363482</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0634569973418211</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.383287850110793</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.372658366905458</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.841378650176199</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.183963544876894</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.291375327215385</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0953455881322371</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0176132238643564</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0379901970524806</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.17581062180761</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.168914575260277</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
pop\_dens
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.177407761894142</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.100892264290126</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.224614993551188</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.420058647797614</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.206628605949836</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.407366025312213</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.209306588299947</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.276913566093664</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.238032082080708</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.127187225778897</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.662262943139979</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.416232662839221</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.49528036972629</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.53165016789625</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.333391741236339</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.237686825228593</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.214402049244923</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.32926261913496</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.183181230951596</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.309369738565861</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.507326615949291</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.155861998904152</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.165283350674773</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.183963544876894</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.301642624133121</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0181279283664274</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0227676241047317</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0969312966872697</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0153162987975221</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.206210293138177</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
prev\_ovrweight
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.391111127983294</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.413438437545353</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.376173501843618</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.552029095360425</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.299933817919028</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0263459015089395</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.323581884411744</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.128366226237115</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0717418306858045</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.380211194690777</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.739226341026295</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.298944635935298</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.118649678663525</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.515013053687943</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.36450746459854</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.337425101544104</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0591875075044087</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.120768845402592</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.523404056518167</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.341350334274435</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.22569795884425</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.237169215399954</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.409001529119572</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.291375327215385</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.301642624133121</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.579132648631863</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.109486828153358</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.244393201614977</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.251296859453772</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.611950832763205</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
women\_legis\_prcnt
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.386911549572759</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.253619220630997</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0291790430056672</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.559987076147214</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0874163779343658</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.160155109312843</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0787087910462828</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.348043968437877</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0943449182396803</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.25535198419992</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.348825831207402</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.235913297521621</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.243036991555523</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0469891667404816</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.257991772249529</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0539849164005974</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0163779324631047</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0542067023782268</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.402389511801002</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0993484691757416</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.139430283889934</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.392218697132129</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.338203276141583</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0953455881322371</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0181279283664274</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.579132648631863</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.287200107293529</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.14648390705625</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.589954844276027</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.510932860053907</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
ftom\_laborF\_r
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.256406960003933</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.298382763685522</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.375917889124497</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0696576750572546</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.393482379625481</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.409035805031644</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.391145406510823</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.314285290155828</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.497870693714257</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.376961200290208</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0275045249217939</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.178012588610091</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.136103631878401</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.157685078564472</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.459880430395706</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.35488026054882</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.279329344861605</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.086690415671757</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.166058951913307</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0206146533458392</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.201148798692923</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.464248950467756</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.00396107307025052</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0176132238643564</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0227676241047317</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.109486828153358</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.287200107293529</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.029611497858936</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.115230632952725</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.214122061247041</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
rd\_expend
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.54734347214046</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.38784018407508</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.363521627006681</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.34943328851831</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.449241597158243</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.67149719580827</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.397176304904479</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.430355671682105</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.206114521554322</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.4730379054627</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.57951081141779</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.609778022899023</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.485620458238191</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.137186180096214</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0128991529541136</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.592565040661913</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0933311838537072</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.024249926894486</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.598166827923329</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0506752378108141</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.00109131673492675</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.573796491276918</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.23309639455994</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0379901970524806</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0969312966872697</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.244393201614977</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.14648390705625</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.029611497858936</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.132451282056391</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.340386752457409</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
prim\_schl\_enrll
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.46732093852829</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.29469300445278</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.13424137773124</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.278403677714419</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0976522771441432</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.222237991718121</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.101051277110007</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.185721429200036</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.158387927859014</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.238881990912382</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0598142233166902</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.416904859510096</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.472476044722556</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0692539977445689</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.206329031669733</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.319006122009467</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0280352813398128</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0402683029671573</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.021979751165858</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0334677431547046</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.107554202168616</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.237427776087367</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.257156420621361</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.17581062180761</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.0153162987975221</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.251296859453772</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.589954844276027</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.115230632952725</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.132451282056391</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.23123216068139</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
unemply\_t
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.289033054625551</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.260539717326102</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.00372401593672054</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.712626651921219</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.11302545248307</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.125535423968409</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.104236484229165</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.400184783277498</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.285317056927301</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.352017772892787</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.523054564025414</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.163323169258899</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.131978020778751</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.13552995619658</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0699765986915525</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.169569723406691</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.267370698105437</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.166495888762004</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.227871368652409</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.385975101516301</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.101603489492744</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.0245272572908683</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.314072687202159</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.168914575260277</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.206210293138177</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.611950832763205</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.510932860053907</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.214122061247041</span>
</td>
<td style="text-align:left;">
<span style="     color: red !important;">-0.340386752457409</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">0.23123216068139</span>
</td>
<td style="text-align:left;">
<span style="     color: black !important;">1</span>
</td>
</tr>
</tbody>
</table>

### Step 5: Make Visualizations

``` r
# correlation heatmap - see the last page to see better heat map with values
cor(sesg_num, use = "pairwise.complete.obs") %>%
  # Save as a data frame
  as.data.frame %>%
  # Convert row names to an explicit variable
  rownames_to_column %>%
  # Pivot so that all correlations appear in the same column
  pivot_longer(-1, names_to = "other_var", values_to = "correlation") %>%
  ggplot(aes(rowname, other_var, fill=correlation)) +
  # Heatmap with geom_tile
  geom_tile() +
    theme(axis.text.x=element_text(angle=90,hjust=1))+
  # Change the scale to make the middle appear neutral
  scale_fill_gradient2(low="red",mid="white",high="blue") +
  # Overlay values
  geom_text(aes(label = round(correlation,2)), color = "black", size = 3) +
  # Give title and labels
  labs(title = "Correlation matrix for the dataset sesg", x = "variable 1", y = "variable 2")
```

<img src="Project-1_files/figure-gfm/unnamed-chunk-5-1.png" style="display: block; margin: auto;" />

``` r
# plot 1
sesg_clean <- sesg %>%
  filter(country !="World") %>%
  select(-`Methane_emissions `, -`CO2_emissions `, -`Nitrous_oxide_emissions `)%>%
  mutate(GDP_share = case_when(country %in% c("United States","Japan","Italy") ~"high",
                               country %in% c("Korea, Rep.","Australia","Spain") ~ "mid",
                               country %in% c("Greece","Thailand", "Singapore") ~ "low"))

ggplot(sesg_clean, aes(x=re_consum_prcnt, y=ctrl_corrupt, color= country, shape= GDP_share))+
  geom_jitter()+
  geom_violin(draw_quantiles=0:4/4, trim=FALSE)+
  labs(title="Renewable energy consumption percentage vs. Govt. corruption estimate",
       x= "Renewable Energy Consumption percentage (%)",
       y="Government Corruption Estimate")
```

<img src="Project-1_files/figure-gfm/unnamed-chunk-5-2.png" style="display: block; margin: auto;" />

``` r
# plot 2
ggplot(sesg_clean, aes(x=re_consum_prcnt, y= agri_for_fish_val, color=GDP_share))+
  geom_point()+
  geom_boxplot()+
  labs(title="Renewable Energy Consumption percentage vs. Agriculture forest and fishing value added", 
       x= "Renewable Energy Consumption percentage (%)",
       y= "Agriculture, value added (% of GDP)")
```

<img src="Project-1_files/figure-gfm/unnamed-chunk-5-3.png" style="display: block; margin: auto;" />

*Geom\_point is added to the graph to show the actual data points and
ranges that box plots cannot show.*

*Variables “renewable energy consumption percentage” and “control of
corruption” are selected because they show negative correlation to one
another (-0.64). The first ggplot shows that government corruption
estimate decreases as renewable energy consumption percentage increases.
Colors represent country and the shape of each data points shows the GDP
share that each country belongs. GDP share follows ordinal manner with
these variables. *

*Variables "agriculture (fishing and forest), value added, and renewable
energy consumption percentage are selected because they show positive
correlation to one another (0.77). The second ggplot shows that as
renewable energy consumption percentage increases the agriculture, value
added percentage also increases. Colors represent GDP share of each
country. It is clear that GDP does not show any significant relationship
with any variables. Low GDP share countries has the greatest variance.*

### Step 6: Perform k-means/PAM clustering or PCA

``` r
#clean the data
sesg_clean <- sesg_clean %>%
  na.omit
  
#scale
sesg_scaled <- sesg_clean %>%
  select(where(is.numeric))%>%
  scale

#peform PCA
sesg_pca <- sesg_scaled %>%
  prcomp()
sesg_pca
```

    ## Standard deviations (1, .., p=33):
    ##  [1] 2.99635536 2.68403285 2.45335483 1.86355325 1.55631983 1.24865359
    ##  [7] 1.00740439 0.83261471 0.69153685 0.57698419 0.48293921 0.40403904
    ## [13] 0.29481915 0.27090934 0.25279452 0.22416598 0.19706149 0.15855587
    ## [19] 0.14203593 0.12779983 0.12072657 0.10461232 0.09578949 0.07081732
    ## [25] 0.06682523 0.05890469 0.04670075 0.04126604 0.03281694 0.02706400
    ## [31] 0.02018267 0.01598123 0.01025107
    ## 
    ## Rotation (n x k) = (33 x 33):
    ##                              PC1          PC2           PC3          PC4
    ## year                  0.07641058 -0.070672560 -0.0411819580 -0.264472904
    ## acc_cft_t             0.30133106 -0.112722743  0.0880653158  0.047521405
    ## acc_elct_t            0.21569271 -0.098262531  0.0852086433  0.030623740
    ##                               PC5           PC6          PC7         PC8
    ## year                  0.378319163 -0.3798507874  0.035255560 -0.10250133
    ## acc_cft_t            -0.042805836  0.0946999687 -0.052662220 -0.05936092
    ## acc_elct_t            0.073092987 -0.1772580799 -0.494667836  0.08163528
    ##                                PC9         PC10          PC11         PC12
    ## year                  0.3396232814 -0.031312328  0.0922734433 -0.292657422
    ## acc_cft_t             0.0088941701 -0.022234793 -0.0357205184  0.245466357
    ## acc_elct_t           -0.0956814387  0.630154949 -0.1751333473  0.072838164
    ##                               PC13         PC14         PC15          PC16
    ## year                  0.0876904195 -0.090336261 -0.114590858  0.0552568510
    ## acc_cft_t             0.0204775767  0.018568800 -0.030946302 -0.1166950430
    ## acc_elct_t            0.0559931710  0.192462060 -0.101657469  0.1276022940
    ##                              PC17        PC18          PC19          PC20
    ## year                  0.063246840  0.25333872 -0.2021202163 -0.1665765276
    ## acc_cft_t            -0.089412628  0.19887501  0.1004292089  0.2380008616
    ## acc_elct_t            0.042189759 -0.05970662 -0.2161992991 -0.0004186898
    ##                              PC21         PC22        PC23         PC24
    ## year                 -0.232200371 -0.101685072 -0.16031544  0.093404217
    ## acc_cft_t             0.119437088  0.009863649 -0.17386443 -0.127855238
    ## acc_elct_t           -0.047304740  0.065053808  0.25702929  0.100621712
    ##                               PC25         PC26         PC27          PC28
    ## year                  0.2554214639  0.003071709  0.075769530  0.0858962464
    ## acc_cft_t             0.0257394783  0.357688178 -0.289434870  0.1585410877
    ## acc_elct_t           -0.0176348009 -0.003545333 -0.003064981  0.0397601194
    ##                               PC29         PC30         PC31         PC32
    ## year                  0.1611946813  0.158337245  0.059911551  0.079960203
    ## acc_cft_t             0.1485666714  0.468158997  0.194060691  0.314565325
    ## acc_elct_t           -0.0231616400  0.031848211 -0.008491021 -0.012851759
    ##                               PC33
    ## year                  0.0311801435
    ## acc_cft_t             0.0368458019
    ## acc_elct_t            0.0055597975
    ##  [ reached getOption("max.print") -- omitted 30 rows ]

``` r
summary(sesg_pca)
```

    ## Importance of components:
    ##                           PC1    PC2    PC3    PC4    PC5     PC6     PC7
    ## Standard deviation     2.9964 2.6840 2.4534 1.8636 1.5563 1.24865 1.00740
    ## Proportion of Variance 0.2721 0.2183 0.1824 0.1052 0.0734 0.04725 0.03075
    ## Cumulative Proportion  0.2721 0.4904 0.6728 0.7780 0.8514 0.89864 0.92940
    ##                            PC8     PC9    PC10    PC11    PC12    PC13    PC14
    ## Standard deviation     0.83261 0.69154 0.57698 0.48294 0.40404 0.29482 0.27091
    ## Proportion of Variance 0.02101 0.01449 0.01009 0.00707 0.00495 0.00263 0.00222
    ## Cumulative Proportion  0.95040 0.96490 0.97498 0.98205 0.98700 0.98963 0.99186
    ##                           PC15    PC16    PC17    PC18    PC19    PC20    PC21
    ## Standard deviation     0.25279 0.22417 0.19706 0.15856 0.14204 0.12780 0.12073
    ## Proportion of Variance 0.00194 0.00152 0.00118 0.00076 0.00061 0.00049 0.00044
    ## Cumulative Proportion  0.99379 0.99532 0.99649 0.99725 0.99787 0.99836 0.99880
    ##                           PC22    PC23    PC24    PC25    PC26    PC27    PC28
    ## Standard deviation     0.10461 0.09579 0.07082 0.06683 0.05890 0.04670 0.04127
    ## Proportion of Variance 0.00033 0.00028 0.00015 0.00014 0.00011 0.00007 0.00005
    ## Cumulative Proportion  0.99913 0.99941 0.99956 0.99970 0.99980 0.99987 0.99992
    ##                           PC29    PC30    PC31    PC32    PC33
    ## Standard deviation     0.03282 0.02706 0.02018 0.01598 0.01025
    ## Proportion of Variance 0.00003 0.00002 0.00001 0.00001 0.00000
    ## Cumulative Proportion  0.99995 0.99998 0.99999 1.00000 1.00000

``` r
#screeplot
library(factoextra)
fviz_screeplot(sesg_pca, addlabels=T)
```

<img src="Project-1_files/figure-gfm/unnamed-chunk-6-1.png" style="display: block; margin: auto;" />

``` r
sesg_pca_data <- data.frame (sesg_pca$x, country=sesg_clean$country, year= sesg_clean$year, GDP_share=sesg_clean$GDP_share)
sesg_pca_data
```

    ##         PC1      PC2       PC3      PC4       PC5       PC6         PC7
    ## 11 1.316478 1.422277 -1.622280 4.321394 0.4433142 0.5164144  0.32524679
    ## 13 1.533632 1.311723 -1.765784 4.418963 0.7861210 0.1813412 -0.06213938
    ##          PC8        PC9        PC10       PC11      PC12       PC13       PC14
    ## 11 1.2320606 -0.3733798  0.03365052 -0.7530325 1.1396768 -0.2052246 -0.3796168
    ## 13 0.9699856 -0.1229936 -0.38316616 -0.1923841 0.7431989 -0.2010072  0.2567010
    ##          PC15      PC16       PC17        PC18       PC19        PC20      PC21
    ## 11 -0.1214301 0.2433418  0.1663641  0.04708629 0.10786641  0.30195147 0.3465292
    ## 13 -0.1352014 0.7247896 -0.5751256 -0.13068539 0.07848027 -0.07249932 0.3236152
    ##           PC22        PC23        PC24       PC25        PC26        PC27
    ## 11 -0.06544367  0.18566773  0.03221849  0.1037505 -0.05760459  0.05170172
    ## 13 -0.01398674 -0.07884984 -0.06310103 -0.1364906  0.01837284 -0.08619016
    ##            PC28        PC29        PC30          PC31         PC32         PC33
    ## 11 -0.096550254  0.05575692 -0.03054125 -0.0007931805 -0.003411123 -0.003984882
    ## 13  0.001697674 -0.02885397  0.03347031 -0.0282097067  0.017444535  0.004749140
    ##      country year GDP_share
    ## 11 Australia 2000       mid
    ## 13 Australia 2002       mid
    ##  [ reached 'max' / getOption("max.print") -- omitted 88 rows ]

``` r
ggplot(sesg_pca_data, aes(x = PC1, y = PC2, color = country, shape=GDP_share)) + 
  geom_point() +
  labs(title="PC1 vs. PC2")
```

<img src="Project-1_files/figure-gfm/unnamed-chunk-6-2.png" style="display: block; margin: auto;" />

``` r
#each variable contribution to each PC
sesg_pca$rotation
```

    ##                              PC1          PC2           PC3          PC4
    ## year                  0.07641058 -0.070672560 -0.0411819580 -0.264472904
    ## acc_cft_t             0.30133106 -0.112722743  0.0880653158  0.047521405
    ## acc_elct_t            0.21569271 -0.098262531  0.0852086433  0.030623740
    ##                               PC5           PC6          PC7         PC8
    ## year                  0.378319163 -0.3798507874  0.035255560 -0.10250133
    ## acc_cft_t            -0.042805836  0.0946999687 -0.052662220 -0.05936092
    ## acc_elct_t            0.073092987 -0.1772580799 -0.494667836  0.08163528
    ##                                PC9         PC10          PC11         PC12
    ## year                  0.3396232814 -0.031312328  0.0922734433 -0.292657422
    ## acc_cft_t             0.0088941701 -0.022234793 -0.0357205184  0.245466357
    ## acc_elct_t           -0.0956814387  0.630154949 -0.1751333473  0.072838164
    ##                               PC13         PC14         PC15          PC16
    ## year                  0.0876904195 -0.090336261 -0.114590858  0.0552568510
    ## acc_cft_t             0.0204775767  0.018568800 -0.030946302 -0.1166950430
    ## acc_elct_t            0.0559931710  0.192462060 -0.101657469  0.1276022940
    ##                              PC17        PC18          PC19          PC20
    ## year                  0.063246840  0.25333872 -0.2021202163 -0.1665765276
    ## acc_cft_t            -0.089412628  0.19887501  0.1004292089  0.2380008616
    ## acc_elct_t            0.042189759 -0.05970662 -0.2161992991 -0.0004186898
    ##                              PC21         PC22        PC23         PC24
    ## year                 -0.232200371 -0.101685072 -0.16031544  0.093404217
    ## acc_cft_t             0.119437088  0.009863649 -0.17386443 -0.127855238
    ## acc_elct_t           -0.047304740  0.065053808  0.25702929  0.100621712
    ##                               PC25         PC26         PC27          PC28
    ## year                  0.2554214639  0.003071709  0.075769530  0.0858962464
    ## acc_cft_t             0.0257394783  0.357688178 -0.289434870  0.1585410877
    ## acc_elct_t           -0.0176348009 -0.003545333 -0.003064981  0.0397601194
    ##                               PC29         PC30         PC31         PC32
    ## year                  0.1611946813  0.158337245  0.059911551  0.079960203
    ## acc_cft_t             0.1485666714  0.468158997  0.194060691  0.314565325
    ## acc_elct_t           -0.0231616400  0.031848211 -0.008491021 -0.012851759
    ##                               PC33
    ## year                  0.0311801435
    ## acc_cft_t             0.0368458019
    ## acc_elct_t            0.0055597975
    ##  [ reached getOption("max.print") -- omitted 30 rows ]

``` r
fviz_pca_var(sesg_pca, col.var = "black")
```

<img src="Project-1_files/figure-gfm/unnamed-chunk-6-3.png" style="display: block; margin: auto;" />

``` r
# the ideal number of clustering
library(cluster)
sesg_pca_data %>%
  select(where(is.numeric)) %>%
  fviz_nbclust(FUNcluster = pam, method = "s")
```

<img src="Project-1_files/figure-gfm/unnamed-chunk-6-4.png" style="display: block; margin: auto;" />

``` r
# pam algorithm
sesg_pam <- sesg_pca_data %>%
  select(PC1,PC2) %>%
  pam(k=3)
sesg_pam
```

    ## Medoids:
    ##     ID        PC1       PC2
    ## 11   1  1.3164784  1.422277
    ## 75  30  0.1976394 -2.666481
    ## 205 69 -6.9883468  2.428537
    ## Clustering vector:
    ##  11  13  15  17  19  21  22  24  26  41  42  43  44  45  48  49  50  51  52  53 
    ##   1   1   1   1   1   1   1   1   1   2   2   2   2   2   2   2   2   2   2   2 
    ##  65  67  68  69  70  71  72  73  74  75  76  77  78  79  80 119 121 122 123 124 
    ##   2   2   2   2   2   2   2   2   2   2   2   2   2   2   2   1   1   1   1   1 
    ## 125 126 127 128 129 130 131 132 133 134 173 175 176 177 178 179 180 181 182 183 
    ##   1   1   1   1   1   1   1   1   1   1   2   2   2   2   2   2   2   2   2   2 
    ## 184 185 186 187 188 200 202 204 205 206 207 208 209 211 213 214 229 230 231 232 
    ##   2   2   2   2   2   3   3   3   3   3   3   3   3   3   3   3   1   1   1   1 
    ## 233 234 235 236 237 238 239 240 241 242 
    ##   1   1   1   1   1   1   1   1   1   1 
    ## Objective function:
    ##    build     swap 
    ## 1.570696 1.432291 
    ## 
    ## Available components:
    ##  [1] "medoids"    "id.med"     "clustering" "objective"  "isolation" 
    ##  [6] "clusinfo"   "silinfo"    "diss"       "call"       "data"

``` r
#clustering
sesg_pamclust <- sesg_pca_data %>%
  mutate(cluster=as.factor(sesg_pam$clustering))
sesg_pamclust
```

    ##         PC1      PC2       PC3      PC4       PC5       PC6         PC7
    ## 11 1.316478 1.422277 -1.622280 4.321394 0.4433142 0.5164144  0.32524679
    ## 13 1.533632 1.311723 -1.765784 4.418963 0.7861210 0.1813412 -0.06213938
    ##          PC8        PC9        PC10       PC11      PC12       PC13       PC14
    ## 11 1.2320606 -0.3733798  0.03365052 -0.7530325 1.1396768 -0.2052246 -0.3796168
    ## 13 0.9699856 -0.1229936 -0.38316616 -0.1923841 0.7431989 -0.2010072  0.2567010
    ##          PC15      PC16       PC17        PC18       PC19        PC20      PC21
    ## 11 -0.1214301 0.2433418  0.1663641  0.04708629 0.10786641  0.30195147 0.3465292
    ## 13 -0.1352014 0.7247896 -0.5751256 -0.13068539 0.07848027 -0.07249932 0.3236152
    ##           PC22        PC23        PC24       PC25        PC26        PC27
    ## 11 -0.06544367  0.18566773  0.03221849  0.1037505 -0.05760459  0.05170172
    ## 13 -0.01398674 -0.07884984 -0.06310103 -0.1364906  0.01837284 -0.08619016
    ##            PC28        PC29        PC30          PC31         PC32         PC33
    ## 11 -0.096550254  0.05575692 -0.03054125 -0.0007931805 -0.003411123 -0.003984882
    ## 13  0.001697674 -0.02885397  0.03347031 -0.0282097067  0.017444535  0.004749140
    ##      country year GDP_share cluster
    ## 11 Australia 2000       mid       1
    ## 13 Australia 2002       mid       1
    ##  [ reached 'max' / getOption("max.print") -- omitted 88 rows ]

``` r
# graph with clusters
sesg_pamclust %>% 
  ggplot(mapping = aes(x= PC1, y= PC2)) +
  geom_point(aes(color=country, shape= GDP_share))+
  stat_ellipse(aes(group=cluster))
```

<img src="Project-1_files/figure-gfm/unnamed-chunk-6-5.png" style="display: block; margin: auto;" />
*By the rule of cumulative proportion being 80%, PC1 through PC5 are
considered, while PC1 through PC7 need to be considered by Kaiser’s rule
where eigenvalues are greater than 1.*

*primary energy intensity, female to male ratio in labor force,
fertility rate, renewable energy consumption, renewable energy output,
control of corruption, internet user percentage, research and
development expenditure, electricity production from fossil fuel, energy
use, fossil fuel energy consumption percentage are positively
contributed to both PC1 and PC2 *

*k=3 is selected because the GDP share is divided into 3 categories. It
wouldn’t make sense to choose k=7*

### Main Findings

*The first main finding: Some environmental-related variables show some
correlation to social-related variables. For example, life expectancy
has a positive correlation with access to clean fuel and technology in
total (0.80). Net forest depletion has a negative correlation with
access to clean fuel and technology (-0.93). *

*The second main fining: It shows that GDP rate does not have any strong
correlation with amount of renewable energy (-0.12). In addition GDP
share does not show any significant correlation with other
sustainability-related factors.*

``` r
Sys.info()
```

    ##        sysname        release        version       nodename        machine 
    ##      "Windows"       "10 x64"  "build 19042" "<U+C774><U+D61C><U+C815>"       "x86-64" 
    ##          login           user effective_user 
    ##        "hjlee"        "hjlee"        "hjlee"
