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
INTDUR = rep(3,n)

head(HCCPEBaseDat)
HCCPEBaseDat = data.frame(HCCPEBaseDat, INTDUR)

write.csv(HCCPEBaseDat, "HCCPEBaseDat.csv", row.names = FALSE)
```



