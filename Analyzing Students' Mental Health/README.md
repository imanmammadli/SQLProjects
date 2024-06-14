

🇬🇧

Does going to university in a different country affect your mental health? An international Japanese university surveyed its students in 2018 and published a study the following year, which was approved by various ethics and regulatory boards.

The study found that international students were at higher risk of experiencing mental health problems than the general population, and that social connectedness (belonging to a social group) and acculturation stress (the stress of joining a new culture) were predictors of depression.

Examine student data using PostgreSQL to see if you can draw a similar conclusion for international students and whether length of stay is a contributing factor.


🇦🇿

Fərqli ölkədə universitetə ​​getmək psixi sağlamlığınıza təsir edirmi? Beynəlxalq Yapon universiteti 2018-ci ildə tələbələri arasında sorğu keçirdi və növbəti il ​​müxtəlif etika və tənzimləyici şuralar tərəfindən təsdiqlənən bir araşdırma dərc etdi.

Tədqiqat əcnəbi tələbələrin ümumi əhali ilə müqayisədə psixi sağlamlıq problemləri ilə üzləşmə riskinin daha yüksək olduğunu və sosial bağlılıq (sosial qrupa mənsubiyyət) və akkulturasiya stressi (yeni mədəniyyətə qoşulma stressi) depressiyanın proqnozlaşdırıcıları olduğunu müəyyən edib.

Beynəlxalq tələbələr üçün oxşar nəticə çıxara biləcəyinizi və qalma müddətinin töhfə verən amil olub-olmadığını görmək üçün PostgreSQL-dən istifadə edərək tələbə məlumatlarını araşdırın.



## The dataset is available here and you can click here to find the commands

## Information about the data set here

| Field Name    | Description                                      |
| ------------- | ------------------------------------------------ |
| `inter_dom`     | Types of students (international or domestic)   |
| `japanese_cate` | Japanese language proficiency                    |
| `english_cate`  | English language proficiency                     |
| `academic`      | Current academic level (undergraduate or graduate) |
| `age`           | Current age of student                           |
| `stay`          | Current length of stay in years                  |
| `todep`         | Total score of depression (PHQ-9 test)           |
| `tosc`          | Total score of social connectedness (SCS test)   |
| `toas`          | Total score of acculturative stress (ASISS test) |


## Query and description

Let us examine and analyse the data of the international students participating in the study to see how their length of stay affects their average mental health diagnosis score.

### The average columns should contain the average of the todep (PHQ-9 test), tosc (SCS test), and toas (ASISS test) columns for each length of stay, rounded to two decimal places.
### Column count_int is the number of international students for each period of stay

SELECT stay, COUNT(inter_dom) AS count_int, ROUND(AVG(todep), 2) AS average_phq, ROUND(AVG(tosc), 2) AS average_scs, ROUND(AVG(toas), 2) AS average_as

FROM students

### Since we are analysing international students, it is necessary to give the condition to bring the rows with "Inter" and not to bring the empty ones.
WHERE stay IS NOT NULL AND inter_dom = 'Inter'

### Then we group these selected rows according to the length of stay and sort them from most to least.
GROUP BY stay
ORDER BY stay DESC;
