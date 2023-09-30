---
title: "Resume Parser"
datePublished: Thu Sep 09 2021 20:01:11 GMT+0000 (Coordinated Universal Time)
cuid: cldr99k0q01zzz6nveax16gbv
slug: resume-parser

---

Parsing Resume is not an easy task. This tasks comes with lot of challenges such as 
- resumes for different doamins(IT, commerce, etc) have differnet parsing challenges
- dealing with different fileformats. (docx,pdf,images)
- dealing with resume formats. (structure of resumes)
- Identifying sections within resumes (Education, Work Experience, personal details, etc)
- Develping an ontology for categorization of domain,skills, designation, etc 


## Hybrid approach
- Rule Based Approach
- Statistical Apporach
- Machine Learning Based Approach

1. **Rules Based Approach**
   - Write rules to parse resume and detect diferent sections of resumes using headings.
   - Then write separate rules for each section 
     - Work experience: parse comapny name, company location, duration(from-to-end Date)
     - Education: Parse Instituion name, year, etc

2. **Statistical Based Approach**
   - Use statistics to identify the common skills in a particular domain, a very basic way is to count the number of times that skill is mentioned. 
   - This method also helps to identify if new skill has arised in a particular industry. As more and more candidate start mentioning it the parser will increment the count of that skill in our database. And a threshold will help to qualify the skill.

3. **Machine Learning Based Approach**
   - On having enough data from above two approach, train model to classify the section
   - Trail model to detect NER (location, dates,etc) 

You will always feel your parser lack in perfection, so the correct approach would be to set the threshold around your parser and not getting overwhelmed by all the problems at the same time. and you will also experience the chicken-and-egg problem at start.




Paid tools 
- [Daxtra](https://www.daxtra.com/resume-database-software/resume-parsing-software/)
- [Turbohire](https://turbohire.co/)
- [Burning Glass](https://www.burning-glass.com/products/lens-suite/)


I will Keep updating more on this, Please let me know if you are looking for depth on any specific thing for resume parser.


