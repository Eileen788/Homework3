#Readme

Author: Eileen Eghan

The dataset Class1survey was obtained by a survey completed by students in Dr Kim's Advanced Data Analysis class. The survey had a total of 27 questions which included student's favorite food, favorite drink, highest level of education and other descriptive questions.

2. This project involves analyzing a survey dataset named class1survey.

  i. Number of people who filled out the survey was 29.

  ii. Number of variables was 27.

3. The variables were renamed to shorter and more descriptive names making it easier to read using this code:

  i. names(class1survey)[1:27]<-c("id", "like_cats", "like_dogs", "have_desert", "slogan",
"fav_day", "larkORowl", "fav_food", "fav_drink", "fav_season", "fav_month", "hobby",
"program", "specialization", "stat_software", "R_exp", "coding_comfort", "coding_length",
"top_three","public_health_interest", "fav_num", "bday", "bmonth", "country", "state",
"city", "highest_educ_level")

4. The number of factor, integer, numerical, and character variables in the dataset was determined using sapply and table functions with the code:

  i. table(sapply(class1survey,class))
  
5a. The bday and bmonth variables were checked for unusual or missing values using the code:

  i. class1survey$bday
  ii. class1survey$bmonth
  
b. The unusual non numerical values in bmonth and bday were recoded to numeric format using ifelse() with the code:

  i. class(class1survey$bday)
class1survey$bday<-ifelse(class1survey$bday == "March 31st","31", class1survey$bday)
class1survey$bday<-ifelse(class1survey$bday == "May 21-report 21","21",class1survey$bday)

  ii. class(class1survey$bmonth)
class1survey$bmonth<-ifelse(class1survey$bmonth == "March","3", class1survey$bmonth)
class1survey$bmonth<-ifelse(class1survey$bmonth == "February","2", class1survey$bmonth)
class1survey$bmonth<-ifelse(class1survey$bmonth == "July","7", class1survey$bmonth)
class1survey$bmonth<-ifelse(class1survey$bmonth == "May 21-report 5","5", class1survey$bmonth)
class1survey$bmonth<-ifelse(class1survey$bmonth == "September","9", class1survey$bmonth)

c. The class of bday and bmonth variables was checked and converted from character to numeric. Median was then calculated for both variables. 

  i. class(class1survey$bday)
    class(class1survey$bmonth)
    
  ii. class1survey$bday_n<-as.numeric(class1survey$bday)
      class1survey$bmonth_n<-as.numeric(class1survey$bmonth)
      
  iii. median(class1survey$bday_n, na.rm=TRUE)
       median(class1survey$bmonth_n, na.rm=TRUE)
       
  iv. The median of birthday was 14
      The median birth month was 7(July) 
      

6a. A new variable bseason was created to give the season according to Northern Meteorological season in which respondents were born using the code:

  i. class1survey <- class1survey %>%
  mutate(bseason=case_when(bmonth_n %in% c(12,1,2) ~"winter",
                           bmonth_n %in% c(3,4,5) ~"spring",
                           bmonth_n %in% c(6,7,8) ~"summer",
                           bmonth_n %in% c(9,10,11) ~"fall"))
                           
b. A table was created of with bseason in the columns and bmonths in the rows to check that the coding was correct using the code:

  i. table(class1survey$bmonth_n, class1survey$bseason)
  
c. The addmargins function was used to answer the question of how many classmates were born in each season? The code used was:

  i. tab<-addmargins(table(class1survey$bmonth_n, class1survey$bseason, useNA = "always"), 1) 
    tab
    
  ii. 4 students were born in Fall, 9 students in spring, 8 students in summer and 8 students in winter.
  

7a. The variables I chose to analyse was highest level of educatation(highest_educ_level).

The question was "How many students had each level of education?". The code I used was:

  i. summary(class1survey$highest_educ_level)
  ii. table(class1survey$highest_educ_level)

  
The answer I got was:

  iii. 20 students have a Bachelor's degree, 5 students have a master's degree and 4 students have a doctoral degree.
 

