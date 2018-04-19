---
title: "CCPEDDataDump"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Need to add



INSTRMNT_LANG	=1	
LANG_OTHER = NA
GRANT_ID = 	SP021203 # just do this manually
DESIGNGRP = 1
redcap_survey_identifier = PARTID
INTTYPE =3 follow up
INTTYPE = 1 = baseline
INTDUR = 3


Drop

name
email
address
phone_number
redcap_survey_identifier



Need to add and or change the following variables
```{r}
#setwd("T:/prevention/STAFF REPORTS 17-18/Chat HIV    FY2/Evaluation")
#HCCPEBaseDat = read.csv("Question Tracking Sheet FINALBaseline.csv", header = TRUE)
names(HCCPEBaseDat) = toupper(names(HCCPEBaseDat))
n = dim(HCCPEBaseDat)[1]
#firstVars = data.frame(INSTRMNT_LANG = rep(1, n), LANG_OTHER = rep(NA, n), GRANT_ID = rep("SP021693", n), DESIGNGRP = rep(1, n), PARTID = HCCPEBaseDat$PARTICIPANT_ID, MONTH = HCCPEBaseDat$MONTH, DAY= HCCPEBaseDat$DAY, YEAR = HCCPEBaseDat$YEAR, INTTYPE = rep(1, n), INTDUR = rep(3,n))
head(HCCPEBaseDat)
colnames(HCCPEBaseDat)[8] = c("PARTID")
head(HCCPEBaseDat)
HCCPEBaseDat$NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_TIMESTAMP = NULL
HCCPEBaseDat$NAME = NULL
HCCPEBaseDat$EMAIL = NULL
HCCPEBaseDat$ADDRESS = NULL
HCCPEBaseDat$PHONE_NUMBER = NULL
HCCPEBaseDat$REDCAP_SURVEY_IDENTIFIER = NULL
HCCPEBaseDat$NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_COMPLETE = NULL
HCCPEBaseDat$RECORD_ID = NULL

head(HCCPEBaseDat)
HCCPEBaseDat = data.frame(HCCPEBaseDat, INTDUR = rep(3,n))



write.csv(HCCPEBaseDat, "HCCPEBaseDat.csv", row.names = FALSE)
```
Same for 3-month follow up just change 
Get the date
```{r}
Date = HCCPE3monthDat$NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_TIMESTAMP

# Ok need to separate by space first then get rid of actual time
library(dplyr)
library(reshape2)

Date = colsplit(Date, " ", c("Date", "Time"))
Date$Time = NULL
Date =data.frame(Date)
write.csv(Date, "Date.csv", row.names = FALSE)
Date = read.csv("Date.csv", header = TRUE) 
Date = colsplit(Date$Date, "/", c("MONTH", "DAY", "YEAR"))
dim(Date)
Date
```

Need to add the first variables
```{r}
#setwd("T:/prevention/STAFF REPORTS 17-18/Chat HIV    FY2/Evaluation")
#HCCPE3monthDat = read.csv("Question Tracking Sheet FINAL3months.csv", header = TRUE)
names(HCCPE3monthDat) = toupper(names(HCCPE3monthDat))
n = dim(HCCPE3monthDat)[1]
firstVars = data.frame(INSTRMNT_LANG = rep(1, n), LANG_OTHER = rep(NA, n), GRANT_ID = rep("SP021693", n), DESIGNGRP = rep(1, n), PARTID = HCCPE3monthDat$REDCAP_SURVEY_IDENTIFIER, Date, INTTYPE = rep(3, n), INTDUR = rep(3,n), INTERVENTION_A = rep(NA, n), INTERVENTION_B = rep(NA, n), INTERVENTION_C = rep(NA, n))

head(firstVars)

head(HCCPE3monthDat)
HCCPE3monthDat$REDCAP_SURVEY_IDENTIFIER = NULL
HCCPE3monthDat$RECORD_ID = NULL
HCCPE3monthDat$NAME = NULL
HCCPE3monthDat$EMAIL = NULL
HCCPE3monthDat$ADDRESS = NULL
HCCPE3monthDat$PHONE_NUMBER = NULL
HCCPE3monthDat$REDCAP_SURVEY_IDENTIFIER = NULL
HCCPE3monthDat$NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_COMPLETE = NULL
HCCPE3monthDat$RECORD_ID = NULL
HCCPE3monthDat$NATIONAL_MINORITY_SAHIV_PREVENTION_INITIATIVE_ADUL_TIMESTAMP = NULL

### Get rid of the 0 variables
HCCPE3monthDat$DEPLOYEDASIA___0 = NULL
HCCPE3monthDat$DEPLOYEDIRAQ___0 = NULL
HCCPE3monthDat$DEPLOYEDKOR___0 = NULL
HCCPE3monthDat$DEPLOYEDOTH___0 = NULL
HCCPE3monthDat$DEPLOYEDPERS___0 = NULL
HCCPE3monthDat$DEPLOYEDWWII___0 = NULL
HCCPE3monthDat$RESPECT_AGE___0 = NULL
HCCPE3monthDat$RESPECT_DISABLE___0 = NULL 
HCCPE3monthDat$RESPECT_GENDER___0 = NULL
HCCPE3monthDat$RESPECT_HIV___0 = NULL
HCCPE3monthDat$RESPECT_MH___0 = NULL
HCCPE3monthDat$RESPECT_NONE___0 = NULL
HCCPE3monthDat$RESPECT_RACE___0 = NULL
HCCPE3monthDat$RESPECT_REL___0 =NULL
HCCPE3monthDat$RESPECT_SEXPR___0 = NULL


HCCPE3monthDat = rename(HCCPE3monthDat, replace =c("DEPLOYEDASIA___1" = "DEPLOYEDASIA", "DEPLOYEDIRAQ___1" = "DEPLOYEDIRAQ", "DEPLOYEDKOR___1"= "DEPLOYEDKOR", "DEPLOYEDOTH___1"="DEPLOYEDOTH", "DEPLOYEDPERS___1"="DEPLOYEDPERS", "DEPLOYEDWWII___1"="DEPLOYEDWWII", "RESPECT_AGE___1" = "RESPECT_AGE", "RESPECT_DISABLE___1" = "RESPECT_DISABLE", "RESPECT_GENDER___1" = "RESPECT_GENDER", "RESPECT_HIV___1" = "RESPECT_HIV", "RESPECT_MH___1"="RESPECT_MH", "RESPECT_NONE___1"="RESPECT_NONE", "RESPECT_RACE___1"="RESPECT_RACE", "RESPECT_REL___1"="RESPECT_REL", "RESPECT_SEXPR___1"= "RESPECT_SEXPR"))



head(HCCPE3monthDat)
HCCPE3monthDat = data.frame(firstVars, HCCPE3monthDat)
head(HCCPE3monthDat)
setwd("C:/Users/Matthew.Hanauer/Desktop")
write.csv(HCCPE3monthDat, "HCCPE3monthDat.csv", row.names = FALSE)
```
Combine them all for HCCPE before rbind must download one variable is out of order.
```{r}
HCCPEBaseDat = read.csv("HCCPEBaseDat.csv", header = TRUE)
HCCPEDat = rbind(HCCPEBaseDat, HCCPE3monthDat)
head(HCCPEBaseDat)
```

```{r}
head(HCCPE3monthDat)
```

