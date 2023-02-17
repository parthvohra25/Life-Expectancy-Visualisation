data_set<-read.csv("C:\\Users\\parth\\OneDrive\\Desktop\\Sem 5\\Data Science (UCS538)\\DS_Project\\Life Expectancy Data.csv")
head(data_set)

library(dplyr)

#SPLITTING
data_set1=select(data_set,Country,Year,Life_expectancy,Adult_Mortality,infant_deaths,under.five_deaths,Population)

data_set2=select(data_set,Country,Year,Alcohol,Hepatitis_B,Measles,BMI,Polio,ii,Diphtheria,HIV.AIDS,thinness._1.19_years,thinness_5.9_years)

data_set3=select(data_set,Country,Status,Year,percentage_expenditure,GDP,Income_composition_of_resources,Schooling)

#DATA CLEANING

for(i in 2:ncol(data_set1)) {                                   
  data_set1[ , i][is.na(data_set1[ , i])] <- mean(data_set1[ , i], na.rm = TRUE)
}

for(i in 2:ncol(data_set2)) {                                   
  data_set2[ , i][is.na(data_set2[ , i])] <- mean(data_set2[ , i], na.rm = TRUE)
}

for(i in 3:ncol(data_set3)) {                                   
  data_set3[ , i][is.na(data_set3[ , i])] <- mean(data_set3[ , i], na.rm = TRUE)
}


data_frame=merge(data_set1,data_set2,by=c("Country","Year"))
new_data=merge(data_set3,data_frame,by=c("Country","Year"))
print(new_data)

write.csv(new_data,"C:\\Users\\parth\\OneDrive\\Desktop\\Sem 5\\Data Science (UCS538)\\DS_Project\\new_data.csv")